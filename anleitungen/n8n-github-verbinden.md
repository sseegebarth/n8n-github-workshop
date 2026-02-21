# n8n mit GitHub verbinden

## Übersicht

In dieser Anleitung verbindest du deinen n8n Cloud Account mit GitHub über einen **Personal Access Token (PAT)**.

**Dauer:** ca. 5 Minuten

---

## Teil A: Personal Access Token in GitHub erstellen

### 1. GitHub öffnen und einloggen

Öffne [github.com](https://github.com) und melde dich mit deinem Account an.

### 2. Token-Einstellungen öffnen

Klicke oben rechts auf dein **Profilbild** → **Settings** → scrolle links nach unten → **Developer settings** → **Personal access tokens** → **Tokens (classic)**

### 3. Neuen Token erstellen

Klicke auf **Generate new token** → **Generate new token (classic)**.

### 4. Token konfigurieren

| Feld | Wert |
|------|------|
| **Note** | `n8n-workshop` |
| **Expiration** | `7 days` |

Setze folgende **Berechtigungen (Scopes)**:

- [x] `repo` *(gesamter Zugriff auf Repositories)*
- [x] `admin:repo_hook` *(Webhooks erstellen und verwalten)*

> ⚠️ **Wichtig:** Ohne `admin:repo_hook` kann n8n keine Webhooks erstellen und der GitHub Trigger funktioniert nicht!

### 5. Token kopieren

Klicke auf **Generate token**. Kopiere den Token sofort (beginnt mit `ghp_`). Er wird nur einmal angezeigt!

---

## Teil B: Token in n8n hinterlegen

### 6. n8n öffnen

Öffne deinen n8n Cloud Account im Browser.

### 7. Credential erstellen

Linke Seitenleiste → **Credentials** (Schlüssel-Symbol) → **Add Credential**

### 8. GitHub auswählen

Suche nach **GitHub API** (nicht "GitHub OAuth2 API"!).

### 9. Token einfügen

| Feld | Wert |
|------|------|
| **Credential Name** | `GitHub Workshop` |
| **GitHub Server** | `https://api.github.com` |
| **Access Token** | *(deinen kopierten Token einfügen)* |

### 10. Verbindung testen

Klicke auf **Save**. Bei einer grünen Erfolgsmeldung ist alles korrekt.

**Falls Fehler auftreten:**

- Token vollständig kopiert (mit `ghp_` am Anfang)?
- Richtige Scopes gewählt (`repo` und `admin:repo_hook`)?
- GitHub Server ist `https://api.github.com`?

---

## Kurzfassung

```
GitHub: Profilbild → Settings → Developer settings → Tokens (classic) → Generate new token
  → Note: n8n-workshop | Expiration: 7 days | Scopes: repo, admin:repo_hook
  → Generate → Token kopieren

n8n: Credentials → Add Credential → GitHub API
  → Name: GitHub Workshop | Server: https://api.github.com | Token einfügen → Save
```
