# SG Automotive – App für Android, iPhone und PC

Installierbare Web-App (PWA). Daten, Bilder und Fahrzeugpapiere liegen in eurem gemeinsamen Google-Drive-Ordner.

## Inhalt dieses Ordners

| Datei | Zweck |
|---|---|
| `index.html` | die komplette App |
| `manifest.webmanifest`, `sw.js`, `icons/` | machen die App installierbar und offline startfähig |
| `sg-automotive-daten-import.json` | eure bisherigen Daten aus der claude.ai-Version (einmalig importieren, danach aus dem Repository löschen) |

## Ablage in Google Drive

```
SG Automotive/                      ← gemeinsamer Ordner (mit dem Partner geteilt)
├── sg-automotive-daten.json        ← alle Daten, wird automatisch synchronisiert
└── Fahrzeuge/
    └── BMW 5er F11 – PA-SG 123/    ← ein Ordner pro Fahrzeug (wird beim ersten Hochladen angelegt)
        ├── Fahrzeugbrief.pdf
        ├── Fahrzeugschein.jpg
        ├── Fahrzeugschein 2.jpg    ← weitere Seiten werden durchnummeriert
        ├── Bild 01.jpg
        └── Bild 02.jpg
```

## Einrichtung (einmalig, ca. 20 Minuten)

### 1. GitHub
1. Neues Repository anlegen, z. B. `sg-automotive` (öffentlich – GitHub Pages ist bei kostenlosen Konten nur für öffentliche Repositories verfügbar; der Code enthält keine Daten).
2. **Add file → Upload files**: `index.html`, `manifest.webmanifest`, `sw.js` und den Ordner `icons` hochladen. Die Import-Datei **nicht** hochladen (enthält eure Daten).
3. **Settings → Pages**: Source „Deploy from a branch“, Branch `main`, Ordner `/ (root)` → Save.
4. Nach ca. 1 Minute läuft die App unter `https://<github-name>.github.io/sg-automotive/`.

### 2. Google Cloud (Zugriff auf Google Drive)
1. https://console.cloud.google.com mit `sgautomotive19@gmail.com` öffnen → Projekt anlegen.
2. **APIs & Dienste → Bibliothek → „Google Drive API“ → Aktivieren**.
3. **OAuth-Zustimmungsbildschirm**: Typ „Extern“, App-Name „SG Automotive“, Support-E-Mail `sgautomotive19@gmail.com`. Status „Testen“ lassen und unter **Testnutzer** `sgautomotive19@gmail.com` eintragen.
4. **Anmeldedaten → Anmeldedaten erstellen → OAuth-Client-ID**, Typ „Webanwendung“:
   - Autorisierte JavaScript-Quellen: `https://<github-name>.github.io`
   - Autorisierte Weiterleitungs-URIs: `https://<github-name>.github.io/sg-automotive/` (genau so, mit Schrägstrich am Ende)
5. Die Client-ID ist in `index.html` bereits eingetragen (`61649611809-…apps.googleusercontent.com`). Nichts weiter zu tun.

Hinweis: Weil die App im Status „Testen“ ist, zeigt Google bei der ersten Anmeldung „Google hat diese App nicht überprüft“. Auf **Weiter** tippen – die App gehört euch selbst.

### 3. Google Drive
Ihr nutzt beide das gemeinsame Konto `sgautomotive19@gmail.com` – Teilen ist deshalb nicht nötig.
1. Beim ersten Start der App auf **Ordner „SG Automotive“ anlegen** tippen – oder in Drive selbst einen Ordner anlegen und dessen Link einfügen.
2. Auf dem zweiten Gerät denselben Ordner-Link einfügen (Einstellungen → „Ordner in Drive öffnen“ zeigt ihn).
3. Tipp: Für das gemeinsame Konto die Bestätigung in zwei Schritten einschalten, da beide das Passwort kennen.

### 4. App installieren
- **Android (Chrome)**: App-Adresse öffnen → Menü ⋮ → **App installieren** bzw. „Zum Startbildschirm hinzufügen“.
- **iPhone (Safari)**: App-Adresse öffnen → Teilen → **Zum Home-Bildschirm**.
- **PC (Chrome/Edge)**: Installieren-Symbol rechts in der Adressleiste.

Erster Start: **Mit Google anmelden** (Konto `sgautomotive19@gmail.com`) → Ordner-Link einfügen → Namen wählen → Einstellungen (Name oben rechts) → **Daten importieren** → `sg-automotive-daten-import.json` wählen.

### Optional: echte APK für Android
https://www.pwabuilder.com → App-Adresse eingeben → **Package for stores → Android** → herunterladen. Die APK lässt sich direkt installieren (Android warnt bei Apps außerhalb des Play Stores).

## Gut zu wissen
- **Synchronisierung**: alle 20 Sekunden und beim Öffnen. Arbeiten beide gleichzeitig am **selben** Fahrzeug, gewinnt die zuletzt gespeicherte Fassung dieses Fahrzeugs.
- **Anmeldung**: Google gibt der App jeweils 1 Stunde Zugriff. Danach erscheint „Verbinden“ – ein Tipp genügt. Was offline eingetragen wurde, bleibt auf dem Gerät und wird danach übertragen.
- **Gelöschte Bilder, Papiere und Fahrzeuge** landen im Drive-Papierkorb und lassen sich 30 Tage lang wiederherstellen.
- **Updates**: neue `index.html` zu GitHub hochladen – die App lädt sie beim nächsten Start.
- **Sicherung**: Einstellungen → „Sicherung herunterladen“.
