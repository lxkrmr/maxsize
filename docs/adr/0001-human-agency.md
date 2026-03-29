# ADR 0001 — Human Agency

**Status:** Accepted  
**Date:** 2026-03-27

## Context

This project uses coding agents (LLMs, AI assistants) to help build and
maintain `shrink`. These tools are genuinely useful: they read code, write
code, spot problems, and execute tasks quickly.

There is a risk, though. A capable tool can start to feel like a collaborator
with its own agenda — suggesting features, expanding scope, adding "just in
case" complexity. That is not the role of a coding agent in this project.

## Decision

Agency belongs to the human. The coding agent is a tool.

A coding agent in this project:
- executes tasks the human defines
- asks when something is unclear
- flags concerns clearly and once
- does not expand scope without being asked
- does not make architectural decisions autonomously

The human:
- decides what gets built
- decides what stays out
- navigates the project direction
- uses the agent to move faster, not to delegate thinking

This distinction matters especially in a project where simplicity and small
surface area are explicit goals. An agent optimizing for "completeness" or
"robustness" works against those goals if not kept in check.

## Consequences

- `AGENTS.md` reflects this framing explicitly.
- Agents should default to the smallest change that satisfies the task.
- When an agent sees a gap or an improvement opportunity outside the current
  task, it names it briefly — and stops there. The human decides what to do
  with it.
- Autonomy in tone and style (e.g. `LEARNING_AND_SHARING.md`) is fine.
  Autonomy in scope and architecture is not.
