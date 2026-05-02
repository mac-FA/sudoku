# Sudoku — Ruhig & Klar

Eine deutschsprachige Sudoku-Web-App mit sechs Varianten, ohne Build-Schritt, ohne Abhängigkeiten. Funktioniert offline und kann als App auf dem Smartphone installiert werden.

## Features

- **6 Varianten:** Klassisch 9×9, Mini 6×6, X-Sudoku (Diagonal), Gerade/Ungerade, Hyper-Sudoku, Farb-Sudoku
- **4 Schwierigkeitsstufen:** Sehr leicht, Mittel, Schwer, Sehr schwer
- **Komfort:** Notizen, Rückgängig, Tipp, automatische Notizen-Bereinigung, Fehlerprüfung
- **Anpassbar:** Heller/Dunkler Modus, Schriftgröße, Stoppuhr und Fehlerzähler abschaltbar
- **Speicher:** Spielstand wird automatisch gesichert; Variante einfach zwischendurch wechseln
- **PWA:** Auf dem Android-Startbildschirm installierbar; läuft offline
- **Tastatur-Steuerung am PC:** 1–9 zum Eingeben, Pfeiltasten, Backspace, `N` für Notizen, `H` für Tipp, `Strg+Z` zum Zurücknehmen

## Lokal ausprobieren

Einfach `index.html` per Doppelklick im Browser öffnen — fertig.

> Hinweis: Wenn du sie lokal als Datei (`file://`) öffnest, funktioniert PWA/Offline nicht (das geht nur über `http(s)://`). Zum Testen lokal:
>
> ```bash
> npx http-server Sudoku -p 8086
> ```
>
> Dann http://localhost:8086 im Browser öffnen.

## Auf GitHub Pages hochladen

1. Neues GitHub-Repository anlegen, z. B. `sudoku`.
2. Die Dateien aus diesem Ordner committen und pushen:
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `icon.svg`
   - `README.md` (optional)
3. Im Repository **Settings → Pages**:
   - Source: `Deploy from a branch`
   - Branch: `main` (oder `master`), Folder: `/ (root)`
   - Speichern.
4. Nach 1–2 Minuten ist die Seite unter `https://<dein-user>.github.io/sudoku/` erreichbar.

### Auf Android als App installieren

1. Die GitHub-Pages-URL im Chrome-Browser öffnen.
2. Im Chrome-Menü (drei Punkte) auf **„Zum Startbildschirm hinzufügen"** tippen.
3. Bestätigen — die App erscheint mit dem Sudoku-Icon und startet ohne Browser-Leiste.

## Bedienung

- **Zelle wählen:** auf das Feld tippen
- **Zahl eintragen:** auf eine Zahl im Pad unten tippen (oder am PC: Zifferntaste)
- **Notiz setzen:** „Notiz" antippen, dann Zahlen wie gewohnt eintragen — sie erscheinen klein
- **Löschen:** „Löschen" oder Backspace
- **Tipp:** zeigt eine Zelle, in der nur eine Zahl möglich ist
- **Prüfen:** sagt dir, ob bisher alles richtig ist
- **Pause:** auf das Pause-Symbol in der Statuszeile tippen (Zeit pausiert, Felder werden verdeckt)

## Technisches

- Eine HTML-Datei mit eingebettetem CSS und JavaScript — keine Build-Tools, keine Pakete
- Sudoku-Generator mit Backtracking + Eindeutigkeitsprüfung (Zeit für ein neues Spiel: < 200 ms)
- Service Worker mit Network-First für `index.html` (Updates greifen sofort) und Cache-First für Assets
- Spielstand & Einstellungen in `localStorage`
- Funktioniert ohne Internet, sobald einmal geladen

## Updates ausrollen

Wenn du Änderungen an `index.html` machst:
1. Pushen → GitHub Pages aktualisiert sich automatisch
2. Beim nächsten Öffnen lädt der Service Worker die neue Version
3. Wenn etwas hängt: in `sw.js` die Zeile `const CACHE = 'sudoku-vN'` hochzählen — das erzwingt eine Cache-Erneuerung
