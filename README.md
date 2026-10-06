# Grav-Plugin «Medienseite»

Downloadseite in Bereichen (z.B. Pressebilder, Berichte, Grafiken, Logos). Jeder
Bereich ist entweder öffentlich oder nur für registrierte Nutzerinnen und Nutzer
zugänglich.

- **Anmeldung per E-Mail-Code**, ohne Passwort. Neue Personen registrieren sich
  (Name, Organisation/Medium, Einwilligung), bestätigen die Adresse per Code und
  werden per Freigabe-Link freigeschaltet (oder sofort, Modus `open`).
  Konten mit Admin-Rechten melden sich weiterhin mit Passwort an.
- **Ablage ausserhalb des Webverzeichnisses**; Dateien werden nur nach der
  Zugriffsprüfung ausgeliefert. Erlaubte Typen: Bilder, SVG, PDF, ZIP, Office.
  SVGs werden mit Sandbox-Header ausgeliefert.
- **Verwaltung direkt auf der Seite** für Konten mit `admin.login`:
  Hochladen (mehrere Dateien), Titel/Beschreibung/Copyright bearbeiten, Löschen.
- **Vorschaubilder** für Bilder (GD) sowie TIFF/PDF (Imagick, PDF nur mit Ghostscript).

Die Anmeldung per E-Mail-Code stammt aus dem Heftarchiv-Plugin von
schwand-baeregg.ch.

## Voraussetzungen

Grav 1.7/2.x mit den Plugins `login` und `email` (Mailversand eingerichtet).

## Einrichten

1. Plugin nach `user/plugins/medienseite` kopieren.
2. Eine Seite mit dem Template `medienseite` anlegen, z.B. `user/pages/07.medien/medienseite.md`:

   ```yaml
   ---
   title: Medien
   visible: false
   cache_enable: false
   ---
   Einleitungstext …
   ```

3. Konfiguration in `user/config/plugins/medienseite.yaml` (oder im Admin unter
   Plugins → Medienseite), z.B.:

   ```yaml
   seitenname: 'example.ch'
   media_dir: '../example-medien'      # ausserhalb des Webverzeichnisses
   seite: '/medien'
   datenschutz_seite: '/datenschutz'
   auth:
     benachrichtigung: 'webmaster@example.ch'
   bereiche:
     - { schluessel: pressebilder, titel: 'Pressebilder', oeffentlich: false }
     - { schluessel: logos, titel: 'Logos', oeffentlich: true }
   ```

Alle Optionen mit Kommentaren: `medienseite.yaml`.

## Routen

| Route | Zweck |
|---|---|
| `/mediendaten/datei/<bereich>/<datei>` | Datei (`?dl=1` = Download) |
| `/mediendaten/vorschau/<bereich>/<datei>` | Vorschaubild |
| `/mediendaten/auth/start`, `/verify` | Anmeldung (JSON, POST) |
| `/mediendaten/auth/freigeben?token=…` | Freigabe einer Registrierung |
| `/mediendaten/verwalten` | Hochladen/Bearbeiten/Löschen (POST, Nonce) |

## Lizenz

MIT
