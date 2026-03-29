# ADR 0002 — YAGNI

**Status:** Accepted  
**Date:** 2026-03-27

## Context

`shrink` is a simple tool: take images, shrink them if they are too large,
report what happened. That is the whole job.

During early development, the project accumulated things that were not strictly
needed: a self-describing `describe` command with ~200 lines of static JSON,
an `init` command that writes config files, a `config-example` command, a
multi-profile resolution algorithm, a platform guard that does not actually
prevent anything, and a CLI framework (Typer) that brought Rich, Pygments, and
Shellingham along for a ride nobody asked for.

Each of these made sense in isolation. Together they created a tool with a
larger surface, more moving parts, and more dependencies than the core problem
requires.

## Decision

We build what is needed now, for the use cases we actually have.

Concretely:
- **No dependency gets added unless it solves a real problem** the stdlib
  cannot handle.
- **No command gets added** because it might be useful someday.
- **No config feature gets added** to support a workflow that does not exist
  yet.
- If the tool can be understood in five minutes and explained in one paragraph,
  that is a feature, not a limitation.

This applies to dependencies especially. Every external package is a supply
chain entry point, a maintenance obligation, and a source of unexpected
behavior. The question is not "does this package help?" but "is the problem
real enough to justify taking this package in?"

## Consequences

- Fewer dependencies means a smaller attack surface and less to audit.
- Simpler code is easier to reason about — for humans and for agents.
- Features that are cut today can be added later when there is actual demand.
  The reverse is harder: removing things that exist is expensive because people
  start depending on them.
- When a task could be done with stdlib and a small amount of code, that is
  the default choice.
- Scope creep from agents is explicitly out of bounds (see ADR 0001).
