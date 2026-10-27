# Das Kuchlbauer-Quiz mit Flaschl

**Version 1.2.1, Stand 27.10.2026.** Eigenständige Web-App (PWA) rund um die Brauerei zum Kuchlbauer in Abensberg (https://kuchlbauer.de/), gebaut nach dem Vorbild von DANCECHANCE (Referenz in `referenz/`, unverändert).

## Starten (lokal)
Die App braucht einen kleinen Webserver (wegen Service Worker und PWA):

```powershell
powershell -NoProfile -File "C:\Users\NorbertSzpak\.claude\skills\demo-app-bauen\assets\testserver_projekt.ps1" -Root "C:\Users\NorbertSzpak\OneDrive - Ninox Software GmbH\Desktop\NOBBIS_SUPER_FIRMA\02_Erstellte_Apps\kuchlbauer" -Port 8765
```

Dann http://localhost:8765/ im Browser öffnen. Die Datei `index.html` läuft auch per Doppelklick, dann ohne Offline-Funktion (Service Worker).

## Inhalt
- **Sieben Lektionen** mit je drei Quizfragen: Familienbrauerei, Turm und KunstHaus, Führungen und Tickets, Braukurs, Veranstaltungen und Genuss, Besucherinfo, Bossrunde (Weitblick/Nachhaltigkeit).
- **Vier Sprachen:** Deutsch, Englisch, Italienisch, Bairisch (Umschalter DE EN IT BAY, wird gespeichert).
- **Flaschl**, die selbst gezeichnete Weissbier-Flasche (SVG): hüpft beim Start herein, begrüßt, gibt Sprüche, reagiert auf richtige und falsche Antworten, spricht immer in der gewählten Sprache. Abschaltbar (Auge-Symbol oben), aus bei „Bewegung reduzieren“. Kein Logo und kein Bild von kuchlbauer.de.
- **Spielmechanik:** 1 bis 3 Sterne je Lektion (ab 2 von 3 bestanden), fünf Ränge, Konfetti.
- **Urkunden:** je bestandener Lektion, dazu die Meister-Urkunde nach allen sieben. Als PNG speichern, drucken oder **teilen** (Teilen-Menü mit Bild, sonst Fenster mit WhatsApp, E-Mail, Link kopieren). Sprache der Urkunde = Menüsprache.
- **Namensfeld** mit Speichern-Knopf (grau, aktiv, grün „Gespeichert“), Name bleibt nur im Browser.
- **PWA:** installierbar, läuft offline, Update-Hinweis. Icons mit Bootstrap Icons (lokal in `vendor/`, kein CDN).
- Farben aus den Kuchlbauer-Screenshots: Dunkelgrün `#0b3b2e`/`#0f4a3a` (Kopf, Fuß), Gold `#d4a40a`/`#f0c53a`, Kupfer/Braun als Hintergrund, Weiß für Text.

## Dateien (alle ins Hauptverzeichnis, `vendor/` mit Unterordnern)
`index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `favicon.png`, `apple-touch-icon.png`, `kuchlbauer_vorschau.png`, `vendor/bootstrap-icons/bootstrap-icons.min.css`, `vendor/bootstrap-icons/fonts/bootstrap-icons.woff2`. Bei jeder neuen Version `VERSION` in `index.html` **und** `sw.js` gemeinsam erhöhen.

## Quellen (ausschließlich kuchlbauer.de, abgerufen 27.10.2026)
Startseite https://kuchlbauer.de/ · Bier & Kunst https://kuchlbauer.de/bier-und-kunst/ · Familienbrauerei https://kuchlbauer.de/en/beer-and-art/family-brewery/ · Kuchlbauer Turm https://kuchlbauer.de/en/beer-and-art/the-kuchlbauer-tower/ · Führungen & Tickets https://kuchlbauer.de/tickets-2/ · Veranstaltungen & Genuss https://kuchlbauer.de/veranstaltungen-genuss/ · Braukurs https://kuchlbauer.de/braukurs/ · Besucherinfo https://kuchlbauer.de/besucherinfo/

## Bekannte Grenzen und offene Punkte
- **Keine Preise, Zeiten oder Termine** im Quiz (bewusst; die Seite nennt Braukurs-Preis und -Termine ohne Datumsstand). Nur Verweis auf die offizielle Seite.
- Ausnahme Besucherinfo: feste Führungszeiten (11, 13, 15 Uhr), Ruhetage und Winterpause stehen im Quiz, weil die Besucherinfo sie ausdrücklich nennt; sie können sich ändern.
- „Ältestes Braurecht“ und „neun Generationen“ sind Eigenangaben der Brauerei und im Text als „laut Website/Brauerei“ formuliert. Die Namen der Weissbiere nennt die Quelle nicht, das Quiz auch nicht.
- Höhe des Turms (35 m) stammt von der Braukurs-Seite; die Turm-Seite selbst nennt nur den 70-m-Entwurf von 1999 und die Bauzeit 2007 bis 2010.
- **Mundart (Bairisch), Englisch und Italienisch sind liebevoll, aber nicht muttersprachlich geprüft.** Bitte gegenlesen lassen.
- **Produktiv-Adresse** ist angenommen: `https://nosz.github.io/kuchlbauer/` (canonical, og:*, `SHARE_URL`, Manifest-`id` `/kuchlbauer/`). Bei anderer Adresse in `index.html` und im Manifest anpassen. Es wurde nichts veröffentlicht.
- Das Verhältnis zur Brauerei (offiziell oder inoffiziell) ist nicht geklärt; die App behauptet nichts dazu. Vor einer Veröffentlichung mit der Brauerei abstimmen.
- Karriere-Link: kuchlbauer.de nutzt selbst `http://`; die App verlinkt die https-Adresse.
- Service-Worker-Registrierung ließ sich im eingebetteten Browserfenster nicht prüfen (Fehler dort von der Umgebung); Syntax von `sw.js` ist geprüft. Bitte einmal in Chrome/Edge unter http://localhost:8765/ gegenprüfen (DevTools, Application).

## Tests
Automatische Suite: 	ests/kuchlbauer.test.js (1048 Prüfungen, Stand 1.1.0, 0 Fehler). Ausführen bei laufendem Testserver in der Browser-Konsole auf http://localhost:8765/ :

```js
const s = await (await fetch('tests/kuchlbauer.test.js')).text(); const r = await (0, eval)(s + '\nrunSuite()'); console.log(r.summary, r.fails);
```

Nicht automatisch prüfbar: Service-Worker-Registrierung und Installation (in Chrome/Edge unter localhost nachprüfen).

## Änderungsprotokoll
- 1.2.1 (27.10.2026): Witze: Zähler „x von y“ entfernt. Die Witze kommen in zufälliger Reihenfolge (ohne Wiederholung in einer Runde), mal mit, mal ohne Pointe.
- 1.2.0 (27.10.2026): Viel mehr Witze: jetzt 32 (20 Witze mit Pointe, 12 Sprüche ohne Pointe) in vier Sprachen. Sprüche ohne Pointe zeigen nur den Text, Flaschl sagt ihn direkt. Alle selbst formuliert.
- 1.1.0 (27.10.2026): Neuer Abschnitt „Flaschl erzählt Witze“ (8 Bierwitze in vier Sprachen, Pointe zum Aufdecken, Flaschl spricht die Pointe, Reihenfolge ohne Wiederholung). Konfetti sind jetzt lauter süße Flaschen mit Gesicht. Die Web-Suche lieferte nur Wortspiel-Listen und Wirtshaus-Motive, keine abschreibbaren Witze: Die Witze sind selbst formuliert (Motive: leere Flaschen, Maß halten, abgelagert, aufgeschäumt, Pfand, trüb).
- 1.0.5 (27.10.2026): Testsuite `tests/kuchlbauer.test.js` (999 Prüfungen) eingeführt. Gefunden und behoben: zu geringer Kontrast bei richtiger Antwort (Grün abgedunkelt), lange Namen auf der Urkunde (Name bricht kleiner um, Meister-Liste kompakter).
- 1.0.4 (27.10.2026): Urkunde mit Verschnörkelungen: Eck-Schnörkel mit Ranken und Blättern, Zierranken statt einfacher Linien, Lorbeerkranz um das Medaillon.
- 1.0.3 (27.10.2026): Urkunde neu gestaltet: Pergament-Hintergrund, bairische Raute (blau-weiß) im Rahmen, Goldrahmen mit Eckornamenten, Medaillon mit Flaschl, goldenes Siegel mit Sternen, Zierlinien, Unterschriftenlinie.
- 1.0.2 (27.10.2026): Kopfzeile: Flaschen-Symbol (Umriss der Flaschl-Figur, Bootstrap Icons hat keine Flasche) statt Becher-Symbol.
- 1.0.1 (27.10.2026): Auf Wunsch: Fuß der Startseite zeigt statt des Autoren-Links nur den Text „Design by Anja“, Kopfzeile „Kuchlbauer Quiz by Anja“ (die Link-Pflicht-Prüfung des Skills gilt hierfür nicht mehr).
- 1.0.0 (27.10.2026): Erstversion: sieben Lektionen mit 21 Fragen in vier Sprachen (DE, EN, IT, Bairisch), Flaschl als SVG-Figur, Urkunden mit Teilen-Funktion, PWA, Farben der Kuchlbauer-Startseite.
