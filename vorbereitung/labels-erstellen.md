# Labels im Repository erstellen

Für den Use Case 2 (Smart Issue Triage) müssen diese Labels im Repository existieren.

## Manuell erstellen

Gehe in deinem Repo zu **Issues** → **Labels** → **New Label** und erstelle:

| Name | Farbe (Hex) | Beschreibung |
|------|-------------|--------------|
| `bug` | `#d73a4a` | Etwas funktioniert nicht |
| `feature` | `#0075ca` | Neue Funktionalität |
| `frage` | `#d876e3` | Frage an das Team |
| `dokumentation` | `#0e8a16` | Dokumentation verbessern |
| `prio-hoch` | `#b60205` | Hohe Priorität |
| `prio-mittel` | `#fbca04` | Mittlere Priorität |
| `prio-niedrig` | `#c5def5` | Niedrige Priorität |

## Per Script erstellen

Setze deinen Token und Repo-Infos:

```bash
export GH_TOKEN="ghp_DEIN_TOKEN"
export REPO="DEIN-USERNAME/DEIN-REPO"
API="https://api.github.com"
AUTH="Authorization: Bearer $GH_TOKEN"

curl -s -X POST -H "$AUTH" "$API/repos/$REPO/labels" -d '{"name":"bug","color":"d73a4a","description":"Etwas funktioniert nicht"}'
curl -s -X POST -H "$AUTH" "$API/repos/$REPO/labels" -d '{"name":"feature","color":"0075ca","description":"Neue Funktionalität"}'
curl -s -X POST -H "$AUTH" "$API/repos/$REPO/labels" -d '{"name":"frage","color":"d876e3","description":"Frage an das Team"}'
curl -s -X POST -H "$AUTH" "$API/repos/$REPO/labels" -d '{"name":"dokumentation","color":"0e8a16","description":"Dokumentation verbessern"}'
curl -s -X POST -H "$AUTH" "$API/repos/$REPO/labels" -d '{"name":"prio-hoch","color":"b60205","description":"Hohe Priorität"}'
curl -s -X POST -H "$AUTH" "$API/repos/$REPO/labels" -d '{"name":"prio-mittel","color":"fbca04","description":"Mittlere Priorität"}'
curl -s -X POST -H "$AUTH" "$API/repos/$REPO/labels" -d '{"name":"prio-niedrig","color":"c5def5","description":"Niedrige Priorität"}'
```

## Alternative: Repo forken

Wenn du das Workshop-Repository forkst, werden die Labels automatisch mit übernommen. Das ist der einfachste Weg.
