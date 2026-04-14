# Architecture

## High-level design

The `claw-doc` pattern separates the public reference, the operator workspace, and the running gateway.

```text
Operator
  |
  v
Telegram or another approved channel
  |
  v
Dedicated OpenClaw gateway
  |
  +--> breakglass agent runtime
  |
  +--> isolated workspace prompts and templates
  |
  +--> dedicated credentials and auth tokens
  |
  +--> task state, logs, and runtime artifacts kept private
```

## Design principles

### 1. Dedicated gateway first

The gateway is its own trust boundary.

Do not colocate this breakglass agent with unrelated personal assistants unless you deliberately accept the wider blast radius.

### 2. Docs-first workspace

The agent should be guided by explicit docs and prompt files instead of tribal knowledge.

### 3. Sanitized-by-default publication

Public documentation should come from templates and hand-reviewed docs, not from live runtime exports.

### 4. Tight scope

A breakglass agent should have a narrow mission, clear escalation behavior, and tooling that matches its intended role.

For some operators, that means full operational access. For others, it means an advisor-only posture with tighter restrictions. The important thing is to choose deliberately and document the consequences.

## Recommended separation

### Public repo

Contains:

- documentation
- example config
- prompt scaffolding

Does not contain:

- runtime state
- real secrets
- device metadata
- real logs or transcripts

### Private deployment repo or host state

Contains:

- real `openclaw.json`
- system/service wiring for the dedicated gateway
- runtime logs
- auth material
- host-specific scripts
- local operational state

## Suggested components

- dedicated gateway service, separate from the main/personal assistant gateway
- dedicated bot token: `${TELEGRAM_BOT_TOKEN}`
- dedicated gateway auth token: `${GATEWAY_AUTH_TOKEN}`
- dedicated workspace root such as `/path/to/claw-doc/workspace`
- optional notification channel IDs such as `-1001234567890`

These are examples only.

## Exec tradeoff

A true breakglass deployment may intentionally allow `exec=full` so the agent can diagnose and remediate issues in the real environment.

That power is not free. It increases the consequences of bad routing, bad prompts, or weak operational boundaries.

If you disable or restrict exec access, `claw-doc` can still be useful, but its role changes:

- with `exec=full`, it is a doctor
- with restricted exec, it is an advisor

Neither mode is universally correct. The right choice depends on your risk tolerance and whether you want recommendations or hands-on intervention.
