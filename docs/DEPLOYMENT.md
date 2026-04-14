# Deployment

## Deployment stance

This template favors clarity over cleverness. Start with a simple dedicated deployment, then add automation only after the boundary is working.

Decide early whether your deployment is meant to be:

- an operational doctor with powerful environment access
- an advisor that primarily reads, inspects, and recommends

That choice affects tooling, routing, and trust assumptions.

## Example directory layout

```text
/path/to/claw-doc/
  config/openclaw.json
  workspace/
  runtime/
  logs/
```

## Example deployment flow

1. Create a dedicated host directory, for example `/path/to/claw-doc`
2. Create or assign a dedicated OpenClaw home/runtime root for this gateway only
3. Copy `templates/openclaw.example.json` to `config/openclaw.json`
4. Copy files from `templates/workspace/` into the runtime workspace
5. Replace placeholders like `${TELEGRAM_BOT_TOKEN}` and `${GATEWAY_AUTH_TOKEN}`
6. Point all runtime paths at dedicated directories
7. Start the dedicated gateway service
8. Validate routing, auth, and channel access in a non-public test channel first

## Placeholder values to replace

- `${TELEGRAM_BOT_TOKEN}`
- `${GATEWAY_AUTH_TOKEN}`
- `${OPENAI_API_KEY}`
- `${PRIMARY_CHAT_ID}`
- `${ALERT_CHAT_ID}`
- `${WORKSPACE_ROOT}`
- `${RUNTIME_ROOT}`

## Example validation checklist

- gateway starts with the dedicated config
- agent can read the workspace prompt files
- bot can send a test message to the intended chat
- secrets are loaded from private local storage, not from this repo
- no runtime artifacts are being written into the public repo tree

## Before going live

- review `docs/SANITIZATION.md`
- make sure the channel IDs are your own, not copied examples
- confirm the bot token is dedicated to this deployment
- confirm logs and task state stay outside the public repo
- decide whether you are intentionally enabling operational access or keeping the agent in advisor mode
- if granting powerful tool access, require strong routing boundaries and a human approval model for state-changing actions

## Do not do this

- do not run directly from the public repo with real secrets checked in
- do not treat the example config as production-ready without review
- do not merge personal and breakglass gateway state into one directory
- do not treat a separate workspace alone as sufficient isolation if the same gateway/runtime still serves unrelated agents
