# SoulByte Schulung Ex-Rohr | 07.08.2026

Interaktive Reveal.js-Praesentation (1920x1080, Single-File `index.html`) fuer die
SoulByte-Erstschulung von 12 Ex-Rohr-Nutzern. Aufbau nach Emres Leitfaden
(Zeitplan 10:00 bis 12:00, AP1 bis AP5 plus Kahoot).

**Die Praesi wird als Website gezeigt, nicht als PDF.** Optimiert wird auf den
Live-Eindruck im Browser. PDF-Export existiert nur als Notnagel.

## Live

**https://edgarpauledge.github.io/exrohr-soulbyte-schulung/**
GitHub Pages aus `main`, Repo `EdgarPaulEDGE/exrohr-soulbyte-schulung`, oeffentlich.
Jeder Push auf `main` geht automatisch live (etwa eine Minute).

**Zweite Adresse: https://exrohr-soulbyte-schulung.onrender.com**
Render Static Site (Workspace EDGE Digital, `srv-d9qd23ugekts7390o810`),
auto-deploy aus `main`. Am 06.08.2026 als Ausweichweg angelegt, weil GitHub
Pages stundenlang gestoert war; Render klont nur per Git und umgeht damit
die Actions/Pages-Schicht. Achtung: Render kodiert PNGs beim Ausliefern
leicht um (kleinere Dateien, minimal andere Pixel an Freisteller-Kanten),
Hash-Vergleiche gegen lokale Dateien schlagen dort deshalb fehl.

## Starten

```bash
npm run serve        # http://localhost:8080
npm run build        # prueft, ob alle verlinkten Dateien existieren
```

`npm run build` ist kein Kompilat, sondern eine Bauprüfung (`pruefe.mjs`):
sie liest index.html, sammelt alle lokalen Verweise und meldet fehlende
Dateien. Der globale Commit-Hook ruft dieses Skript, deshalb muss es da sein.

`?nofrag` in der URL zeigt alle Einblend-Fragmente sofort (fuer Pruefung).

## Design (Stand nach Edgars Feedback-Runden, 04.08.2026)

- Raumschwarz `#030309`, Avenir Next ueberall (KEIN Monospace), Weiss `#F4F6FF`
- **Galaxie-Hintergrund:** `kosmos.js` (1:1 aus `CC/edge-tools`, three.js in
  `vendor/`): Spiralarme, Sternschichten, Milchstrassenband, langsame Rotation,
  traege Maus-Parallaxe, 2D-Fallback ohne WebGL. Dazu atmender Nebel (CSS)
  und Sternschnuppen alle 6,5 s (1:1 aus dem EdgeVision-Wizard, hinter den Folien).
  `.reveal-viewport` ist auf transparent gezwungen, sonst weisser Hintergrund.
- **Logo: das alte EDGE-Logo** (`assets/logos/edge-logo-white.png`, blauer
  Wuerfel plus Wortmarke, Stand Sparkasse-Praesi). NICHT das Fold-Lockup.
- **Akzente: Schluesselwoerter als Farbverlaufs-Text** (`.schimmer`,
  Purple/Blau/Cyan). Balken-Flaechen hinter Text wurden getestet und VERWORFEN.
- **Keine Ueberzeilen/Kicker** ueber den Headlines: bewusst entfernt, die
  Headline traegt allein (Edgars Wahl: Vorschlag 1 von 3).
- Inhaltsbloecke liegen auf EINEM grossen `.feld` pro Abschnitt (dunkles Glas
  mit leichtem Cyan/Blau-Schimmer, wie die EDGE-Tools-Karten), damit der Text
  vor der Galaxie nicht untergeht. KEINE vielen kleinen Karten. Innen offene
  Spalten und Zeilen mit Hairline-Trennern (`.spalten`, `.zeilen`), Takeaways
  als freies Statement mit Gradient-Strich (`.takeaway`).
- Oben viel Luft: `.slide` hat 150px padding-top, damit die Titel Abstand zur
  Logo-Zeile halten (Edgars Wunsch).
- Fusszeile: nur Seitenzahl unten links. Chrome (Logos, Zahl) verschwindet
  auf `data-chrome="aus"`-Folien.

## Regeln (zwingend)

- Keine Dashes, kein Wort "oder", keine Emojis im Deck. Slogans GROSS.
- Kein box-shadow. Kein Monospace.
- Folien scrollen nicht: Overflow wird kommentarlos abgeschnitten, jede
  Aenderung im Browser pruefen.

## Offene Punkte vor Freitag (Platzhalter im Deck)

1. ERLEDIGT: Folie 2 hat den echten Link `dev.soulbyte.com` plus weissen Punkt-QR
   (`assets/images/qr-soulbyte.png`, mit zxing als lesbar verifiziert).
2. Folie 3: Collage-Bilder (5 Kacheln, Material von LinkedIn, vor Einbau Emre zeigen).
3. ERLEDIGT: Folie 4 hat die echten Portraits in `assets/images/team/`.
   Quelle waren `Desktop/men/`. Weil EDGE-Fotos auf Dunkelblau und die
   Ex-Rohr-Fotos auf Weiss im Querformat lagen, wurden alle sechs per KI
   freigestellt und auf dieselbe Glas-Scheibe gesetzt.
   **Neue Person einsetzen:** freistellen, dann mit dem YuNet-Gesichtsdetektor
   (OpenCV `FaceDetectorYN`) Gesichtsbreite und Augenmitte messen und darauf
   normalisieren: Gesichtsbreite 178px, Augen auf 42 Prozent Hoehe, Ausgabe
   600x600 PNG. NICHT nach Schulterbreite skalieren, sonst wirken schmale
   Personen zu stark herangezoomt.
   **Nadiras Bild ist generativ erweitert:** ihr Originalfoto war zu nah
   aufgenommen, der Anzug endete mitten im Kreis. Per `nano_banana_pro` mit
   dem Original als Referenz herausgezoomt (Gesicht unveraendert, nur mehr
   Oberkoerper), danach freigestellt und normalisiert.
4. Folie 16: SoulByte-Fakten mit Emre gegenpruefen. Datenschutz-Karte nutzt belegte
   Fakten aus der HanseBelt-Praesi (EU-Modell Mistral, Anonymisierung vor KI, DSGVO).
5. ERLEDIGT: Vergleichstabelle ist vollstaendig. **Wichtig fuers Nachschaerfen:**
   die Kategorien muessen so gewaehlt sein, dass ein Kreuz bei ChatGPT und
   Claude auch stimmt. "Datenschutz nach deutschem Standard" ging NICHT,
   weil beide Anbieter AVV und DSGVO-Konformitaet vorweisen; ein Kreuz dort
   waere vor der Runde angreifbar gewesen. Stattdessen auf harte, pruefbare
   Unterschiede gehen: europaeisches Modell, Anonymisierung vor der
   Verarbeitung, Firmenwissen, Ansprechpartner, Arbeitsablaeufe.
6. Folien 20/21: SoulByte-Screenshots plus Stichpunkte.
7. Folie 23: Kahoot-QR und Gewinn festlegen.

## Tempo-Folie (Folie 12)

Zeigt Moores Gesetz gegen KI-Scaling als Log-Chart. Zahlen sind belegt
(Epoch AI, "Compute Trends Across Three Eras of Machine Learning"):
vor 2010 verdoppelte sich KI-Rechenleistung im Moore-Takt (~20 Monate),
seit 2010 alle ~6 Monate. In 10 Jahren also 2^5 = 32-fach gegen
2^20 = 1.048.576-fach. Die Log-Achse ist Absicht: nur so sind beide Kurven
gleichzeitig sichtbar. Quellenzeile steht auf der Folie.

## Nebenakten

- `headline-varianten.html` und `tempo-varianten.html` waren Entscheidungshilfen
  (je 3 Vorschlaege). Koennen weg, sobald nichts mehr daraus geholt wird.
- `3d-experiment/` enthaelt einen ausrangierten Versuch: der ExRohr-Saugwagen
  als 3D-Modell auf der Titelfolie (Foto -> Bild-zu-3D -> GLB -> three.js).
  Technisch fertig und lauffaehig (`fahrzeug.js` plus GLTFLoader), von Edgar
  verworfen. Wiederbelebung: Dateien zurueckschieben, `<canvas id="fahrzeug">`
  in die Titelfolie, Importmap fuer "three" und Modul-Script einhaengen.
