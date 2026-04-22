---
name: claw-doc
description: Public-safe docs-first breakglass OpenClaw agent template for operators who want a dedicated-gateway troubleshooting and documentation agent without publishing live environment state.
metadata:
  {
    "openclaw":
      {
        "emoji": "🩺"
      }
  }
---

# claw-doc

`claw-doc` is a public-safe template for a docs-first breakglass OpenClaw agent deployed behind its own dedicated gateway.

## When to use this

Use this pattern when you want an operator-focused agent that:
- diagnoses issues clearly
- treats documentation as a primary source of truth
- supports breakglass workflows during incidents
- stays isolated from everyday assistant runtime state

## Core idea

A breakglass agent often needs stronger access and a tighter mission than a normal personal assistant.
This template treats gateway isolation as the default architectural choice so operators can reduce blast radius, keep runtime state cleaner, and reason more clearly about trust boundaries.

## Deployment postures

Two valid operating modes are documented in this repo:

- **Doctor mode**: may intentionally use stronger access such as `exec=full` for real diagnosis and remediation
- **Advisor mode**: uses more restricted access and focuses on guidance rather than direct action

The correct posture depends on environment and risk tolerance.

## Recommended capability boost

A docs-first breakglass agent gets much better with a strong documentation skill or retrieval layer.

Recommended example:
- ClawHub: <https://clawhub.ai/nicholasspisak/clawddocs>

This is not a hard dependency, but it materially improves:
- doc lookup speed
- config verification
- incident-time accuracy
- explanation quality for proposed fixes

## What this repo includes

- architecture and deployment docs
- dedicated-gateway guidance
- sanitization guidance for public publication
- a redacted OpenClaw config example
- example workspace prompt files
- an intentionally public-safe publication surface built from docs and templates rather than live runtime state

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

## Read first

1. `README.md`
2. `docs/OVERVIEW.md`
3. `docs/ARCHITECTURE.md`
4. `docs/DEDICATED_GATEWAY.md`
5. `docs/DEPLOYMENT.md`
6. `docs/SANITIZATION.md`

## Important publication rule

This repo is meant to be **public-safe**.
Do not add real secrets, live config values, internal logs, pairing artifacts, or environment-specific operational state before publishing.

## Expected publish surface

Keep the published bundle lean and documentation-first.
The core publishable surface is:
- `SKILL.md`
- `README.md`
- `docs/ARCHITECTURE.md`
- `docs/DEDICATED_GATEWAY.md`
- `docs/DEPLOYMENT.md`
- `docs/OVERVIEW.md`
- `docs/SANITIZATION.md`
- `templates/openclaw.example.json`
- `templates/workspace/AGENTS.md`
- `templates/workspace/HEARTBEAT.md`
- `templates/workspace/IDENTITY.md`
- `templates/workspace/SOUL.md`
- `templates/workspace/TOOLS.md`

Keep planning/admin extras out of the publish bundle unless they add direct end-user value.
