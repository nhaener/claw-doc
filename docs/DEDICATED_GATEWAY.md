# Dedicated Gateway

## Why isolation matters

For a breakglass agent, the dedicated gateway is the main safety feature.

This matters even more if the operator chooses an operational posture with powerful tooling such as `exec=full`.

If the same gateway handles unrelated assistants, experiments, or personal workflows, then:

- credentials accumulate in one place
- logs and runtime state become harder to reason about
- operational risk increases
- publication mistakes become more likely

## Recommended pattern

Use one gateway per high-trust operational role.

For `claw-doc`, that means:

- separate gateway process or service
- separate OpenClaw home/runtime root for that gateway
- separate config file
- separate auth token
- separate bot or channel routing where appropriate
- separate workspace directory
- separate runtime storage

This is stronger than just using a different prompt set or folder. The goal is a genuinely separate operational boundary.

## Example separation

```text
/path/to/claw-doc/
  config/openclaw.json
  workspace/
    AGENTS.md
    SOUL.md
    IDENTITY.md
    TOOLS.md
    HEARTBEAT.md
  runtime/
  logs/
```

## Minimum isolation checklist

- do not reuse personal gateway auth tokens
- do not point the repo at a live runtime directory
- do not share a workspace full of unrelated prompts
- do not publish files copied from `.openclaw/` or other runtime roots
- do not commit local `.git/config` or credential helper output

## Strong recommendation

If you are deciding between convenience and isolation here, choose isolation.

If you want `claw-doc` to act as a real doctor in your environment, isolation is what makes that power tolerable. Without that boundary, you are just widening blast radius.

If you are not comfortable granting that level of access, run it in a more restricted advisor mode instead.
