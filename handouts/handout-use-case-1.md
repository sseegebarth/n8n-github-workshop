# Kurzreferenz: Zitat des Tages

## Workflow

```
Manual Trigger → Zitat holen → Felder extrahieren → KI-Kommentar
```

## Schritte

| Nr | Was tun | Node |
|----|---------|------|
| 1 | Workflow erstellen: "Zitat des Tages" | – |
| 2 | Manual Trigger hinzufügen | Manual Trigger |
| 3 | Zitat holen: GET `https://dummyjson.com/quotes/random` | HTTP Request |
| 4 | Felder: `zitat` = `{{ $json.quote }}`, `autor` = `{{ $json.author }}` | Edit Fields |
| 5 | KI-Kommentar generieren (gpt-4o-mini) | OpenAI |
| 6 | Test Workflow klicken – fertig! | – |

## OpenAI Prompt

**System:**
```
Du bist ein witziger und kluger Kommentator. Du bekommst ein Zitat
und schreibst einen kurzen, unterhaltsamen Kommentar dazu.
Der Kommentar soll maximal 2 Sätze lang sein.
Schreibe auf Deutsch.
```

**User:**
```
Zitat: "{{ $json.zitat }}"
– {{ $json.autor }}
```
