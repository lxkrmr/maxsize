# ADR 0005 — One file per purpose

**Status:** Accepted  
**Date:** 2026-03-27

## Context

The project had several markdown files whose responsibilities overlapped.
AGENTS.md referenced ADRs. ADRs referenced AGENTS.md. README mixed tool
documentation with design rationale. This made each file harder to read and
harder to maintain — changing one thing meant checking multiple files.

Attention is finite. An agent or human reading a file should get exactly what
they came for, nothing else.

## Decision

Each markdown file has one purpose. Responsibilities do not overlap.

| File | Purpose |
|---|---|
| `README.md` | How to install and use the tool. Nothing else. |
| `AGENTS.md` | Roles, working style, and the collaboration log format. |
| `CONTRIBUTOR.md` | Commit conventions and contribution rules. |
| `LEARNING_AND_SHARING.md` | The agent's log. |
| `docs/adr/*.md` | Architecture decisions, one per file. |

Rules:
- Files do not reference each other. Whoever needs context will be pointed
  to the right file explicitly by the human.
- Design decisions live in ADRs, not scattered across other files.
- README stays focused on usage. No architecture, no philosophy.
- AGENTS.md stays focused on roles and collaboration. No tool documentation,
  no ADR summaries.

## Consequences

- Each file can be read independently and completely.
- Agents and humans can be given exactly the context they need.
- When something changes, there is exactly one file to update.
