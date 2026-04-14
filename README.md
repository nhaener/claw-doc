# claw-doc

A public-safe reference repo for a docs-first breakglass OpenClaw agent pattern that runs on its own dedicated gateway.

This repository is intentionally sanitized. It is not Beth, not a production export, and not a backup of any live environment. It exists to show the pattern, the structure, and the operating philosophy without exposing private runtime state.

The key design choice is isolation: the docs/breakglass agent lives on a separate gateway so risky troubleshooting, docs work, and operational experiments do not share the same failure domain as a personal assistant.

## Why this repo exists

`claw-doc` captures a practical design for a high-trust, operator-facing OpenClaw deployment:

- docs-first setup and maintenance
- a dedicated gateway isolated from day-to-day personal agents and their runtime state
- explicit breakglass behavior for urgent interventions
- public-safe templates with obvious placeholders
- sanitization guidance for publishing safely

## Core idea

The dedicated gateway is a first-class boundary, not an implementation detail.

That means:

- the breakglass agent runs on its own gateway
- credentials and routing are scoped to that gateway only
- workspace prompts and operating rules are kept separate from personal environments
- public docs describe the pattern without leaking machine-specific values

## Exec posture

For a real breakglass doctor, `exec=full` is the intended functionality because diagnosis and remediation often require direct access to the live environment.

That said, it is not a requirement to use this pattern.

You can also run `claw-doc` in a more restricted mode if you want a safer, more advisory deployment. The tradeoff is simple:

- `exec=full` = operational doctor that can inspect and fix
- restricted exec = advisor that can inspect less and may only recommend fixes

Both are valid. This repo documents the operational form honestly, while encouraging operators to choose the risk level that matches their environment.

## Repository layout

- `docs/` explains the model, architecture, deployment approach, and sanitization rules
- `templates/openclaw.example.json` provides a redacted config example
- `templates/workspace/` contains example prompt files for a docs-first agent workspace

## Documentation-expert skill

A specialized documentation skill is one of the highest-value additions you can give this kind of agent.

It is not a critical dependency, and this repo does not require a specific implementation. But if your goal is a real docs/breakglass doctor instead of a generic assistant with a scary title, a strong documentation lookup layer materially improves the result.

## Intended audience

This repo is for operators who want a public reference before building their own dedicated-gateway OpenClaw setup.

## What this repo does not include

- real tokens, secrets, or credentials
- pairing artifacts or device identity files
- transcripts, logs, or task databases
- environment-specific hostnames, paths, IDs, or remotes
- local git configuration from a real machine

## Start here

1. Read `docs/OVERVIEW.md`
2. Review `docs/ARCHITECTURE.md`
3. Read `docs/DEDICATED_GATEWAY.md`
4. Copy the templates and replace placeholders with your own values
5. Read `docs/SANITIZATION.md` before publishing anything derived from this repo

## Publishing note

Before this repository is published, Nick should review every file for accidental environment leakage and confirm the language matches the intended public positioning.
