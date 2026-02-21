# Hands on: n8n meets GitHub

Workshop-Materialien für den Hands-on Workshop zu n8n und GitHub.

## Was erwartet euch?

In diesem Workshop baut ihr zwei Automatisierungs-Workflows mit n8n:

1. **Zitat des Tages** (Aufwärmübung, ~15 Min.) – Ein zufälliges Zitat aus dem Internet holen und von einer KI kommentieren lassen
2. **Smart Issue Triage** (~40 Min.) – GitHub Issues automatisch mit KI analysieren, kategorisieren und kommentieren

## Voraussetzungen

- Ein GitHub-Account (eigener oder neu erstellt)
- Ein n8n Cloud Account
- Ein Browser
- Euren Zugangsdaten-Zettel (bekommt ihr am Workshop-Tag)

## Materialien

### Anleitungen

- [n8n mit GitHub verbinden](anleitungen/n8n-github-verbinden.md)
- [Use Case 1: Zitat des Tages](anleitungen/use-case-1-zitat-des-tages.md)
- [Use Case 2: Smart Issue Triage](anleitungen/use-case-2-smart-issue-triage.md)

### Handouts

- [Kurzreferenz Use Case 1](handouts/handout-use-case-1.md)
- [Kurzreferenz Use Case 2](handouts/handout-use-case-2.md)

### Workflow-JSONs (zum Importieren in n8n)

Wenn du im Workshop nicht mitkommst, kannst du die fertigen Workflows importieren:

- `workflows/01-zitat-des-tages.json` (wird nach dem Workshop bereitgestellt)
- `workflows/02-smart-issue-triage.json` (wird nach dem Workshop bereitgestellt)

**So importierst du einen Workflow:**
1. Öffne n8n
2. Klicke auf "Add Workflow"
3. Oben rechts: ⋯ → "Import from File"
4. Wähle die JSON-Datei aus

## Labels für Use Case 2

Für den Smart Issue Triage Workflow müssen folgende Labels im Repository existieren:

| Label | Farbe |
|-------|-------|
| `bug` | `#d73a4a` |
| `feature` | `#0075ca` |
| `frage` | `#d876e3` |
| `dokumentation` | `#0e8a16` |
| `prio-hoch` | `#b60205` |
| `prio-mittel` | `#fbca04` |
| `prio-niedrig` | `#c5def5` |

Wenn du dieses Repository forkst, werden die Labels automatisch mit übernommen.

## Ressourcen

- [n8n Dokumentation](https://docs.n8n.io)
- [n8n Community](https://community.n8n.io)
- [n8n Workflow Templates](https://n8n.io/workflows)
- [GitHub REST API Docs](https://docs.github.com/en/rest)
- [OpenAI API Docs](https://platform.openai.com/docs)
