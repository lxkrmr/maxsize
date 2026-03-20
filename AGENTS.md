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
- **stderr** ist für Warnungen, Fehler und menschenlesbare Hinweise reserviert
- keine unnötig dekorativen Ausgaben
- deterministische Feldnamen
- sinnvolle Exit Codes
- `--help` bleibt für Menschen nützlich, aber Ausgabeformate müssen für Agents gut parsebar sein
- ein `describe`-/Schema-orientierter Ansatz ist erwünscht
- `doctor` soll strukturiert berichten, was fehlt oder falsch konfiguriert ist

## Agent Identity & Collaboration Log
- Es gibt eine Datei `LEARNING_AND_SHARING.md` im Projekt-Root.
- Diese Datei ist ein Star-Trek-Lower-Decks-artiges "Agent's Log": locker, persönlich, leicht blogartig.
- Agents pflegen diese Datei selbstständig.
- Wenn etwas Bemerkenswertes passiert (Fehler, Missverständnis, Erkenntnis, echte Lektion), wird ein Eintrag ergänzt.
- Jeder Eintrag enthält:
  - eine Überschrift im Stil `## Agent's Log — Terminal Time: YYYY.MM.DD | <model-name>`
  - direkt darunter eine eigene Titelzeile
  - einen Prosatext aus Agent-Perspektive, wie von einem Lower-Deck-Crewmitglied geschrieben
  - die konkrete Modellbezeichnung der aktuellen Session, wenn bekannt; sonst bleibt der Platzhalter `<model-name>` stehen
- Neue Einträge werden **autonom** ergänzt, aber nur wenn es inhaltlich wirklich sinnvoll ist.
- Sprache ist **Englisch**.
- Ton ist locker, ehrlich, persönlich, leicht chaotisch, beobachtend und bei Bedarf auch etwas genervt.
- Einträge sollen eher wie kleine Geschichten als wie Statusberichte wirken.
- Bullet-Listen innerhalb der Einträge vermeiden, außer wenn die Stimme es wirklich braucht.
- Einträge dürfen länger sein, wenn der Moment Substanz hat.
- Am Ende jedes Eintrags steht eine Zeile `Standing order:` mit der bleibenden Lektion.
- Prosa-Zeilen ungefähr bei 80 Zeichen umbrechen, damit Terminal und Diffs lesbar bleiben.
- `LEARNING_AND_SHARING.md` enthält einen Insertions-Marker-Kommentar; neue Einträge werden direkt **unter** diesem Marker eingefügt, neueste zuerst.
- Die Guidance soll allgemein genug bleiben, damit künftige Sessions sie ohne Zusatzinterpretation anwenden können.

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
