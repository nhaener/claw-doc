# claw-doc

`claw-doc` is a public-safe reference repo for building a docs-first breakglass OpenClaw agent on a dedicated gateway.

It is designed for operators who want a high-trust troubleshooting and documentation agent without publishing a live environment dump.

## What claw-doc is

`claw-doc` is a pattern for an operational agent with a narrow mission:

- diagnose issues clearly
- use documentation as a primary source of truth
- support breakglass workflows when something is wrong
- stay isolated from everyday personal-assistant runtime state

## Why a dedicated gateway matters

The dedicated gateway is the core architectural choice.

A breakglass agent often needs stronger access than a normal assistant. Running it on a separate gateway reduces blast radius, keeps runtime state cleaner, and makes it easier to reason about trust boundaries.

## Doctor mode vs advisor mode

This repo documents both valid deployment postures:

- **Doctor mode**: may intentionally use powerful access such as `exec=full` so the agent can diagnose and remediate issues in the real environment
- **Advisor mode**: uses more restricted access, giving recommendations without the same hands-on capability

Neither is universally correct. The right choice depends on your environment and risk tolerance.

## Documentation-expert skill

A strong documentation skill or retrieval layer is one of the highest-value additions you can give this kind of agent.

Recommended example:
- ClawHub: <https://clawhub.ai/nicholasspisak/clawddocs>

It is not a hard dependency, but it makes `claw-doc` much better at:

- finding current docs quickly
- verifying config and command behavior
- reducing guesswork during incidents
- explaining why a fix is recommended

## What this repo includes

- architecture and deployment docs
- dedicated-gateway guidance
- sanitization guidance for public publication
- a redacted OpenClaw config example
- example workspace prompt files

## What this repo does not include

- live credentials or secrets
- pairing or device identity artifacts
- logs, transcripts, or task databases
- machine-specific runtime state
- copied local git configuration

## Repository layout

- `docs/` for architecture, deployment, and sanitization guidance
- `templates/openclaw.example.json` for a public-safe config example
- `templates/workspace/` for example workspace files

## Getting started

1. Read `docs/OVERVIEW.md`
2. Read `docs/ARCHITECTURE.md`
3. Read `docs/DEDICATED_GATEWAY.md`
4. Review `docs/DEPLOYMENT.md`
5. Read `docs/SANITIZATION.md` before publishing any derivative work
6. Copy the templates and replace placeholders with your own values

## License

MIT
