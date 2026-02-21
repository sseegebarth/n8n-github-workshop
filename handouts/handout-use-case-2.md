# Kurzreferenz: Smart Issue Triage

## Workflow

```
GitHub Trigger → Felder extrahieren → Issue analysieren → Labels setzen → Analyse posten
```

## Schritte

| Nr | Was tun | Node |
|----|---------|------|
| 1 | Workflow erstellen: "Smart Issue Triage" | – |
| 2 | GitHub Trigger (Event: issues) | GitHub Trigger |
| 3 | Felder extrahieren (issue_nummer, issue_titel, etc.) | Edit Fields |
| 4 | KI-Analyse (gpt-4o-mini + JSON Schema) | OpenAI |
| 5 | Labels setzen (kategorie + prio-prioritaet) | GitHub |
| 6 | Analyse-Kommentar posten | GitHub |
| 7 | Workflow aktivieren und testen | – |

## Edit Fields (Schritt 3)

| Feld-Name | Wert |
|-----------|------|
| `issue_nummer` | `{{ $json.body.issue.number }}` |
| `issue_titel` | `{{ $json.body.issue.title }}` |
| `issue_beschreibung` | `{{ $json.body.issue.body }}` |
| `issue_url` | `{{ $json.body.issue.html_url }}` |
| `issue_autor` | `{{ $json.body.issue.user.login }}` |

## KI-Prompt (Schritt 4)

**System:**
```
Du bist ein erfahrener Software-Projektmanager. Analysiere das folgende GitHub Issue und antworte AUSSCHLIESSLICH mit einem JSON-Objekt:

{
  "kategorie": "bug" | "feature" | "frage" | "dokumentation",
  "prioritaet": "hoch" | "mittel" | "niedrig",
  "zusammenfassung": "Ein Satz, der das Issue beschreibt",
  "begruendung": "Warum diese Kategorie und Priorität?",
  "empfehlung": "Was sollte das Team als nächstes tun?"
}

Priorisierung:
- hoch: Sicherheitsprobleme, Datenverlust, Produktionsausfälle
- mittel: Funktionale Bugs, blockierende fehlende Features
- niedrig: Kosmetik, Nice-to-have, Dokumentationswünsche
```

**User:**
```
Issue-Titel: {{ $json.issue_titel }}

Issue-Beschreibung:
{{ $json.issue_beschreibung }}
```

## JSON Schema (Response Format)

```json
{
  "type": "object",
  "properties": {
    "kategorie": {
      "type": "string",
      "enum": ["bug", "feature", "frage", "dokumentation"]
    },
    "prioritaet": {
      "type": "string",
      "enum": ["hoch", "mittel", "niedrig"]
    },
    "zusammenfassung": { "type": "string" },
    "begruendung": { "type": "string" },
    "empfehlung": { "type": "string" }
  },
  "required": ["kategorie", "prioritaet", "zusammenfassung", "begruendung", "empfehlung"],
  "additionalProperties": false
}
```

## Kommentar-Template (Schritt 6)

```
🤖 **Automatische Issue-Analyse**

**Issue:** [#{{ $('Felder extrahieren').item.json.issue_nummer }} – {{ $('Felder extrahieren').item.json.issue_titel }}]({{ $('Felder extrahieren').item.json.issue_url }})

| | |
|---|---|
| **Kategorie** | {{ $('Issue analysieren').item.json.output[0].content[0].text.kategorie }} |
| **Priorität** | {{ $('Issue analysieren').item.json.output[0].content[0].text.prioritaet }} |
| **Zusammenfassung** | {{ $('Issue analysieren').item.json.output[0].content[0].text.zusammenfassung }} |

**Begründung:** {{ $('Issue analysieren').item.json.output[0].content[0].text.begruendung }}

**Empfehlung:** {{ $('Issue analysieren').item.json.output[0].content[0].text.empfehlung }}

---
*Diese Analyse wurde automatisch erstellt.*
```

## Verfügbare Labels

| Label | Farbe |
|-------|-------|
| `bug` | 🔴 rot |
| `feature` | 🔵 blau |
| `frage` | 🟣 lila |
| `dokumentation` | 🟢 grün |
| `prio-hoch` | 🔴 dunkelrot |
| `prio-mittel` | 🟡 gelb |
| `prio-niedrig` | 🔵 hellblau |

## Test-Issues

**Bug (hohe Prio):**
> Datenbankverbindung bricht nach 10 Minuten ab – Alle Nutzer betroffen, Bestellungen gehen verloren.

**Feature (niedrige Prio):**
> Dark Mode für das Dashboard – Wäre schön für Nutzer die abends arbeiten.

**Mehrdeutig:**
> Performance Problem – Die Seite ist manchmal langsam.

**Sicherheit (hohe Prio):**
> Passwörter werden im Klartext geloggt – Schweres Sicherheitsproblem.
