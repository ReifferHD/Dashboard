# Dashboard

Web-App zur Verwaltung von Einkäufen über mehrere Accounts — mit automatischer Berechnung der Beträge pro Account, Auszahlungs-Verwaltung und Live-Synchronisation zwischen allen Geräten.

## Funktionen

- **Produkte erfassen**: Datum, ASIN, Bestellnummer, Einkaufs- und Verkaufspreis, Korrekturen — Differenz und Netto-Differenz werden automatisch berechnet
- **Accounts**: beliebig viele Accounts anlegen; pro Account werden erwirtschafteter Betrag, Auszahlungen und offener Rest automatisch geführt
- **Auszahlungen**: Zahlungen pro Account und Monat eintragen; Monatsübersicht mit Erwirtschaftet / Ausgezahlt / Verbleibend
- **Status-Tracking**: Storno, Zustellung und Rechnungsstellung pro Produkt, mit Filtern und Suche
- **Automatische Storno-Erkennung**: optionales Gmail-Script markiert stornierte Bestellungen anhand der Bestellnummer von selbst
- **Cloud-Sync**: alle Geräte und Nutzer arbeiten live auf demselben Datenstand (Firebase Firestore)
- **Backups**: automatisches wöchentliches Backup als JSON-Download, zusätzlich manueller Export/Import im Menü
- **Als App installierbar** (PWA): auf Android, iOS und Desktop, funktioniert auch offline

## Nutzung

1. Seite öffnen (GitHub-Pages-Adresse dieses Repositories)
2. Auf dem Gerät als App installieren:
   - **Android/Chrome**: Menü ⋮ → „App installieren"
   - **iPhone/Safari**: Teilen → „Zum Home-Bildschirm"
   - **PC/Chrome/Edge**: Installieren-Symbol in der Adressleiste
3. Zahnrad ⚙ → **Cloud-Sync einrichten** → Firebase-Konfiguration und Workspace-Name eintragen (beides beim Betreiber erfragen)

## Technik

- Eine einzelne `index.html` — kein Build, keine Abhängigkeiten
- Speicherung: Firebase Firestore (geteilt) + lokale Kopie je Gerät
- `sw.js` (Service Worker) für Offline-Betrieb, `manifest.webmanifest` für die App-Installation

## Dateien

| Datei | Zweck |
|---|---|
| `index.html` | Die komplette App |
| `sw.js` | Offline-Cache |
| `manifest.webmanifest` | App-Manifest |
| `icon-*.png` | App-Icons |
