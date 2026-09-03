# Dashboard als App auf Handy & PC — Anleitung

Alles hier ist **komplett kostenlos** (GitHub Pages: kostenlos, Firebase Spark-Tarif: kostenlos, für diese Nutzung mehr als ausreichend). Es wird keine Kreditkarte benötigt.

Der Ordner enthält:

| Datei | Zweck |
|---|---|
| `index.html` | Das Dashboard selbst |
| `manifest.webmanifest` | Macht es als App installierbar |
| `sw.js` | Sorgt dafür, dass es auch offline startet |
| `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` | App-Icons |
| `dashboard-icon.ico` | Icon für Windows-Verknüpfungen (optional) |

---

## Teil A: Online stellen mit GitHub Pages (~10 Min.)

1. Auf **github.com** ein kostenloses Konto erstellen (falls noch keins vorhanden).
2. Oben rechts auf **+** → **New repository**.
   - Name: z. B. `dashboard`
   - **Public** auswählen (nötig für kostenloses Pages), dann **Create repository**.
   - Hinweis: „Public" heißt nur, dass der *Programmcode* öffentlich ist — deine eingetragenen Daten liegen **nicht** dort.
3. Auf der Repository-Seite: **uploading an existing file** anklicken (oder „Add file → Upload files").
4. Alle Dateien aus diesem Ordner hineinziehen (`index.html`, `sw.js`, `manifest.webmanifest`, die 3 PNG-Icons) → unten **Commit changes**.
5. Oben auf **Settings** → links **Pages**.
6. Bei „Build and deployment": Source = **Deploy from a branch**, Branch = **main**, Ordner = **/ (root)** → **Save**.
7. 1–2 Minuten warten, Seite neu laden — oben erscheint deine Adresse, z. B.
   `https://DEINNAME.github.io/dashboard/`

Diese Adresse ist ab jetzt dein Dashboard. Die kannst du auch deinem Freund schicken.

**Später mal etwas ändern?** Einfach die neue `index.html` im Repository wieder hochladen (ersetzt die alte automatisch).

---

## Teil B: Als App installieren

**Android (Chrome):** Adresse öffnen → Menü ⋮ → **App installieren** (oder „Zum Startbildschirm hinzufügen"). Icon erscheint wie eine normale App.

**iPhone (Safari):** Adresse öffnen → **Teilen-Symbol** → **Zum Home-Bildschirm**.

**PC (Chrome/Edge):** Adresse öffnen → in der Adressleiste rechts erscheint ein **Installieren-Symbol** (Monitor mit Pfeil) → klicken. Alternativ Menü ⋮ → „Cast, speichern und teilen" → „Seite als App installieren". Die App landet im Startmenü und kann an Taskleiste/Desktop geheftet werden — mit Icon, eigenem Fenster, ohne Browser-Leisten.

---

## Teil C: Cloud-Sync einrichten (gemeinsame Daten auf allen Geräten)

Ohne diesen Teil hat jedes Gerät seine eigenen Daten. Mit Sync sehen alle verbundenen Geräte (auch die deines Freundes) denselben Stand — Änderungen erscheinen live.

1. **console.firebase.google.com** öffnen, mit Google-Konto anmelden.
2. **Projekt erstellen** → Name z. B. `dashboard` → Google Analytics **deaktivieren** (nicht nötig) → Projekt erstellen.
3. Links im Menü: **Build → Firestore Database** → **Datenbank erstellen**.
   - Standort: `europe-west3` (Frankfurt) oder egal → Weiter
   - Modus: **Produktionsmodus** → Erstellen
4. Oben auf den Reiter **Regeln** und den Inhalt komplett ersetzen durch:

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /workspaces/{ws} {
         allow read, write: if true;
       }
     }
   }
   ```

   Dann **Veröffentlichen**.
5. Zur **Projektübersicht** (Zahnrad oben links → Projekteinstellungen) → unten bei „Meine Apps" auf das **`</>`-Symbol** (Web-App) → Spitzname z. B. `dashboard` → **App registrieren**.
6. Es erscheint ein Code-Block mit `const firebaseConfig = { apiKey: "...", ... }`.
   Den Teil **in den geschweiften Klammern** kopieren (oder einfach alles — das Dashboard erkennt es).
7. Im Dashboard: **Zahnrad ⚙ → Cloud-Sync einrichten** → Konfiguration einfügen → einen **Workspace-Namen** vergeben → **Speichern & verbinden**.
8. Auf jedem weiteren Gerät (Handy, PC deines Freundes): dieselbe Konfiguration + **exakt denselben Workspace-Namen** eintragen. Fertig — alle arbeiten auf denselben Daten.

### Wichtig: Workspace-Name = Passwort

Die Daten sind über den Workspace-Namen geschützt: Nur wer ihn kennt, kommt an die Daten. Deshalb:

- **Lang und zufällig wählen**, z. B. `dashboard-luis-x93kf2pqv7` — nicht `test` oder `dashboard`.
- Nur an Personen weitergeben, die mitarbeiten sollen.

### Verhalten bei gleichzeitigem Eintragen

Es gilt „der letzte gewinnt": Wenn zwei Personen im exakt selben Moment speichern, überschreibt der spätere Eintrag den früheren. Bei normalem Eintragen nacheinander passiert das praktisch nie — durch die Live-Synchronisation seht ihr die Änderungen des anderen sofort.

---

## Kosten & Grenzen (Stand der kostenlosen Tarife)

- **GitHub Pages:** dauerhaft kostenlos für öffentliche Repositories.
- **Firebase Spark:** dauerhaft kostenlos, u. a. 50.000 Lesezugriffe und 20.000 Schreibzugriffe **pro Tag** — selbst bei intensiver Nutzung zu mehreren erreicht ihr davon nur einen Bruchteil. Es kann nichts abgebucht werden, da kein Zahlungsmittel hinterlegt ist; im Extremfall pausiert der Dienst bis zum nächsten Tag.

## Hinweise

- Die lokale Datei-Speicherung („Datendatei verknüpfen") und die Backups im Zahnrad-Menü funktionieren weiterhin — als zusätzliche Absicherung sinnvoll.
- Die `index.html` funktioniert auch weiterhin lokal per Doppelklick (nur ohne App-Installation).
- Erste Verbindung mit Sync: Das Gerät mit den vorhandenen Daten zuerst verbinden — es lädt seinen Stand hoch. Danach die anderen Geräte verbinden, sie übernehmen den Stand automatisch.
