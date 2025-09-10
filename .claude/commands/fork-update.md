---
allowed-tools: ["bash", "curl", "mcp__ide__*", "WebFetch"]
description: "Aktualisiert deinen Fork mit den neuesten Änderungen aus dem Original-Repository"
---

## Context

Dein aktueller Branch: !git branch --show-current
Dein Repository Origin: !git config --get remote.origin.url
Anzahl lokaler Commits (nicht gepusht): !git rev-list --count origin/$(git branch --show-current)..HEAD
Lokale Änderungen: !git status --porcelain

## Your task

Aktualisiere den aktuellen Fork mit den neuesten Änderungen aus dem Original-Repository.

### Voraussetzungen prüfen:

1. **Branch überprüfen**: Stelle sicher, dass wir uns im `main` oder `master` Branch befinden
2. **Lokale Commits**: Wenn es lokale Commits gibt (Anzahl > 0), gib eine Fehlermeldung aus:
   ```
   ❌ Du hast lokale Commits, die noch nicht gepusht wurden.
   Bitte erstelle einen Feature-Branch für deine Änderungen:
   git checkout -b feature/deine-aenderungen
   git checkout main
   ```
3. **Ungespeicherte Änderungen**: Wenn es lokale Änderungen gibt, gib eine Fehlermeldung aus

### Fork-Update durchführen:

Wenn alle Voraussetzungen erfüllt sind:

1. **Upstream URL ermitteln**:
   a) Hole die aktuelle Repository-URL (Fork-URL) aus Git:
      ```bash
      git config --get remote.origin.url
      ```
   
   b) Konvertiere SSH zu HTTPS falls nötig:
      - `git@github.com:user/repo.git` → `https://github.com/user/repo`
   
   c) Rufe die GitHub-Seite des Forks auf:
      - Verwende WebFetch (falls verfügbar) oder curl
      - Suche nach dem "forked from" Element im HTML
      - Das Element enthält einen Link zum Original-Repository
      - Beispiel: `<a href="/getAsterisk/claudia">forked from getAsterisk/claudia</a>`
   
   d) Extrahiere die Original-Repository-URL:
      - Aus dem gefundenen Link die vollständige URL konstruieren
      - Format: `https://github.com/[ORIGINAL_USER]/[ORIGINAL_REPO].git`
   
   e) Falls die automatische Erkennung fehlschlägt:
      - Frage den Benutzer nach der Original-Repository-URL
      - Zeige ein Beispiel: `https://github.com/getAsterisk/claudia.git`

2. **Updates holen**:
   ```bash
   git fetch [UPSTREAM_URL] main
   ```

3. **Unterschiede anzeigen** (optional, wenn gewünscht):
   ```bash
   git log HEAD..FETCH_HEAD --oneline
   ```

4. **Updates mergen**:
   ```bash
   git pull [UPSTREAM_URL] main
   ```

5. **Ergebnis anzeigen**:
   - Zeige die Zusammenfassung der aktualisierten Dateien
   - Bestätige den erfolgreichen Update

### Wichtige Hinweise:
- Dieser Command ändert NICHT deine Remote-URLs
- Dein Fork bleibt weiterhin mit deinem eigenen Repository verbunden
- Die Updates werden nur lokal gemerged
- Um die Änderungen zu deinem Fork zu pushen, verwende danach: `git push origin main`