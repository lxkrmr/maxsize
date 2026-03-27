# ADR 0003 — maxsize is a human tool

**Status:** Accepted  
**Date:** 2026-03-27

## Context

`maxsize` was conceived as "agent-first". The idea was that an AI agent would
call the tool, interpret its output, and act on it. This framing drove several
decisions: structured JSON output for every command, a `describe` command
exporting the full tool contract, an `init` command so agents could set up
config programmatically, and detailed error codes for machine consumption.

Looking at the actual workflow: the human takes screenshots. The human decides
they are too large. The human runs `maxsize run`. Done.

An agent telling a human "please check your screenshots and run maxsize" is
strictly worse than the human just running `maxsize run` themselves. The human
is already in the loop at the only moment that matters — when the screenshots
exist.

Instructing an agent to invoke maxsize on the human's behalf adds a layer of
indirection with no benefit. It is slower, less direct, and requires the agent
to have context (which profile? which directory?) that the human already has.

## Decision

`maxsize` is a human tool. It lives in the human's workflow, not the agent's.

This means:
- JSON output on `run` and `doctor` is still fine — it is unambiguous and
  scriptable, which is useful for humans too.
- The `describe` command is unnecessary. A human reads `--help` or the README.
  An agent that needs to understand the tool reads the source or the README.
- The `init` command is unnecessary. A human writes a TOML file once.
- Error messages should be clear to a human reading a terminal, not optimized
  for machine parsing of edge cases nobody hits.
- "Agent-first" as a design constraint is dropped.

## Consequences

- The `describe` and `init` commands are candidates for removal (see ADR 0002).
- Output can be JSON where it is genuinely useful (`run`, `doctor`) without
  every detail being machine-optimized.
- The README and `--help` are the documentation. No runtime schema export
  needed.
- Less code. Smaller surface. Easier to understand and audit.
