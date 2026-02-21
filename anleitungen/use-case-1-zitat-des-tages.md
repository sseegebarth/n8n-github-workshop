# Use Case 1: Zitat des Tages – mit KI-Kommentar

## Was bauen wir?

Einen Workflow, der per Knopfdruck ein zufälliges Zitat aus dem Internet holt und die KI einen unterhaltsamen Kommentar dazu schreiben lässt.

## Workflow-Übersicht

```
Klick → Zitat holen → Felder extrahieren → KI-Kommentar
```

---

## Schritt 1: Workflow erstellen (2 Min.)

1. Klicke in n8n auf **Add Workflow**
2. Benenne den Workflow: **"Zitat des Tages"**
3. Klicke auf das **+** in der Mitte

---

## Schritt 2: Manual Trigger hinzufügen (1 Min.)

1. Suche im Node-Menü nach **Manual Trigger**
2. Wähle **"On clicking 'Test workflow'"**

**Was macht dieser Node?** Er startet den Workflow wenn du auf "Test Workflow" klickst.

---

## Schritt 3: Zitat per HTTP Request abrufen (5 Min.)

1. Klicke auf **+** rechts neben dem Trigger
2. Suche nach **HTTP Request**
3. Konfiguriere:

| Feld | Wert |
|------|------|
| **Method** | GET |
| **URL** | `https://dummyjson.com/quotes/random` |

4. Klicke auf **Test Step**
5. Du siehst ein JSON mit `id`, `quote` und `author`

> 💡 Klicke ruhig 2-3 Mal auf Test Step – jedes Mal kommt ein anderes Zitat.

**Benenne den Node um:** **"Zitat holen"**

---

## Schritt 4: Daten aufbereiten (5 Min.)

1. Klicke auf **+** → suche nach **Edit Fields** (oder **Set**)
2. Füge diese Felder hinzu:

| Feld-Name | Wert |
|-----------|------|
| `zitat` | `{{ $json.quote }}` |
| `autor` | `{{ $json.author }}` |

3. Klicke auf **Test Step**

**Benenne den Node um:** **"Felder extrahieren"**

---

## Schritt 5: OpenAI einrichten (3 Min.)

1. Klicke auf **+** → suche nach **OpenAI**
2. Klicke auf **Create New Credential**
3. Trage den API Key ein (von deinem Zugangsdaten-Zettel)
4. Speichern

---

## Schritt 6: KI-Kommentar generieren (5 Min.)

Konfiguriere den OpenAI Node:

| Feld | Wert |
|------|------|
| **Resource** | Message |
| **Operation** | Send |
| **Model** | `gpt-4o-mini` |

> ⚠️ **Wichtig:** Wähle **gpt-4o-mini**, nicht gpt-4-turbo!

**System Message:**

```
Du bist ein witziger und kluger Kommentator. Du bekommst ein Zitat
und schreibst einen kurzen, unterhaltsamen Kommentar dazu.
Der Kommentar soll maximal 2 Sätze lang sein.
Schreibe auf Deutsch.
```

**User Message:**

```
Zitat: "{{ $json.zitat }}"
– {{ $json.autor }}
```

Klicke auf **Test Step**. Du solltest einen witzigen Kommentar sehen!

**Benenne den Node um:** **"KI-Kommentar"**

> 💡 **Experimentiere!** Ändere die System Message:
> - "Du bist ein Philosoph und kommentierst tiefsinnig."
> - "Du bist ein Stand-Up-Comedian."
> - "Erkläre das Zitat einem 5-Jährigen."

---

## Schritt 7: Gesamttest (2 Min.)

1. Klicke oben auf **Test Workflow**
2. Alle Nodes sollten grüne Haken bekommen
3. Mehrfach klicken – jedes Mal ein neues Zitat!

---

## Troubleshooting

| Problem | Lösung |
|---------|--------|
| HTTP Request gibt Fehler | URL prüfen: `https://dummyjson.com/quotes/random` |
| "Invalid API Key" | Key muss mit `sk-` beginnen, keine Leerzeichen |
| "Model not found" | `gpt-4o-mini` auswählen, nicht manuell eintippen |
| Leere Felder im Set Node | Vorherigen Node erst einzeln testen (Test Step) |

---

## Bonus-Aufgaben

1. Ändere den Prompt – wer schreibt den lustigsten Kommentar?
2. Hole ein zweites Zitat und lass die KI beide vergleichen
3. Wechsel auf `gpt-4o` – ist der Kommentar besser?
