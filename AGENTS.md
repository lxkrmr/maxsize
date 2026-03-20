# AGENTS.md

Projekt: `maxsize`

## Zweck
`maxsize` ist ein agent-first CLI für **macOS**, das Screenshots und andere Bilder anhand einer konfigurierten Maximalgröße skaliert.

Das Tool ist:
- für **AI-/LLM-Agents** gebaut
- **JSON-first** im Output
- stark an **MCP-Protokoll-Ideen** orientiert
- lokal, einfach und vorhersehbar

## Wichtige Produktentscheidungen
- Zielplattform ist **macOS**.
- Bildverarbeitung darf auf macOS-Bordmitteln aufbauen, insbesondere `sips`.
- CLI-UX ist **agent-first**: strukturiert, stabil, maschinenlesbar.
- Antworten sollen klar, vollständig und zuverlässig sein.
- Das Tool soll deutlich kommunizieren, dass es für macOS gedacht ist.

## Architektur-Leitplanken
- Sprache/Runtime: **Python mit `uv`**.
- Keine globale Python-Paketinstallation.
- CLI-Basis: **Typer**.
- Installation soll direkt aus dem GitHub-Repo mit `uv` möglich sein.
- Konfiguration liegt in `~/.config/maxsize/` als **TOML**.
- Die Config unterstützt **mehrere Profile**.
- Es gibt einen `doctor`-Command, der die lokale Konfiguration prüft.
- Resize-Regeln sollen mindestens unterstützen:
  - maximale Breite
  - maximale Höhe
- Working directory und Limits kommen aus der Config, nicht hartkodiert in User-Workflows.

## Agent-/CLI-Design
Wir orientieren uns stark an agent-safe CLI-Prinzipien:
- **stdout** bevorzugt maschinenlesbar, insbesondere JSON
- keine unnötig dekorativen Ausgaben
- deterministische Feldnamen
- sinnvolle Exit Codes
- `--help` bleibt für Menschen nützlich, aber Ausgabeformate müssen für Agents gut parsebar sein
- ein `describe`-/Schema-orientierter Ansatz ist erwünscht
- `doctor` soll strukturiert berichten, was fehlt oder falsch konfiguriert ist

## Dateien und Doku
- `README.md` beschreibt:
  1. Name
  2. Warum
  3. Quickstart
- `CONTRIBUTOR.md` enthält Beitragsregeln, insbesondere Commit-Konventionen.
- Commit-Konventionen bitte **nicht** in diesem Dokument duplizieren, sondern auf `CONTRIBUTOR.md` verweisen.

## Commit-Richtlinie
- Kleine, sinnvolle Commits bevorzugen.
- Commit-Messages folgen **Conventional Commits** mit **Scope**.
- Details stehen in `CONTRIBUTOR.md`.

## Arbeitsweise für Agents
- Erst lesen, dann ändern.
- Änderungen klein und nachvollziehbar halten.
- Bestehende Struktur respektieren.
- KISS bevorzugen.
- Bei CLI-Entscheidungen immer fragen:
  - ist die Ausgabe maschinenlesbar?
  - ist sie stabil?
  - ist sie für Agents leichter konsumierbar als für Menschen?
- Wenn menschliche Ergonomie und Agent-Ergonomie kollidieren, Agent-Ergonomie im Kern priorisieren, ohne die CLI unnötig unfreundlich zu machen.

## Noch offen / zu konkretisieren
- finales Config-Schema
- Profil-Auswahlmechanismus
- exaktes JSON-Ausgabeformat
- Exit-Code-Semantik
- Umgang mit nicht unterstützten Dateitypen
- Umgang mit In-Place-Resize vs. Dry-Run vs. zukünftigen Sicherheitsmechanismen
