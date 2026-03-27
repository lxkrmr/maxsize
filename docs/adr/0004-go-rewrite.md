# ADR 0004 — Rewrite in Go

**Status:** Accepted  
**Date:** 2026-03-27

## Context

The original implementation used Python, Typer, Rich, Pillow, and a config
file with profile support. This was more than the problem required.

The actual problem: resize images in a directory to fit within a maximum width
and height. That is one function. It does not need a framework, a config file,
or a runtime that must be installed separately.

The user is on macOS and already has Go installed. `go install` puts a binary
in `~/go/bin`, which is already in `$PATH`. No additional setup needed.

## Decision

Rewrite in Go. No config file. Flags only.

- **Language:** Go
- **Image resampling:** `golang.org/x/image/draw` — CatmullRom, same authors
  as Go stdlib, no third-party maintainer
- **CLI parsing:** `flag` from stdlib
- **Image I/O:** `image/png`, `image/jpeg` from stdlib
- **Installation:** `go install github.com/<repo>/maxsize@latest`
- **No config file.** Defaults live in a shell alias.

## Consequences

- Single static binary. No runtime, no pip, no uv.
- Supply chain: one dependency (`golang.org/x/image`), maintained by the
  Go team under `golang.org`.
- Profile support, `init`, `describe`, `doctor`, `config-example` are all
  gone. The tool does one thing.
- Python source, pyproject.toml, uv.lock, and config.example.toml are
  removed.
