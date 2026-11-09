# CLAUDE.md – Projektbericht (LaTeX, Gruppenarbeit über GitHub)

Diese Datei fasst Struktur und Regeln des Projekts für Claude zusammen.
Sprache des Dokuments und der Kommunikation: **Deutsch** (neue Rechtschreibung, korrekte Zeichensetzung und Grammatik).

## Projektstruktur

```
main.tex              Hauptdatei: Klassenoptionen, \title, \author, \include der Kapitel, Verzeichnisse
praeambel.tex         Pakete, Layout, Hilfsbefehle – nur nach Rücksprache ändern
kapitel/aufgabeN.tex  ein Kapitel pro Aufgabe (\chapter), endet immer mit der Umgebung „beitraege“
literatur.bib         alle Quellen (APA 7), inkl. KI-Tools als @software
bilder/               Abbildungen (PDF/PNG), per \graphicspath eingebunden
.latexmkrc            pdflatex + biber, Ausgabe nach build/
.gitignore            Hilfsdateien, build/ und main.pdf werden nicht committet
README.md             Anleitung und Abgabe-Checkliste für die Gruppe
```

## Kompilieren und prüfen

- `latexmk main.tex` → `build/main.pdf` (benötigt pdflatex, biber, biblatex-apa, lmodern, Sprachpaket ngerman).
- Nach jeder Änderung kompilieren und `build/main.log` sowie `build/main.blg` auf Warnungen prüfen
  (undefinierte Verweise/Zitate, Overfull-Boxen, biber-Warnungen). Ziel: keine Warnungen.

## Feste Vorgaben (nicht verändern)

- Klasse `scrreprt`, `paper=a4`, `fontsize=10pt`, Sprache `ngerman`.
- Einheitliche Schrift: Latin Modern (`lmodern`, T1). Überschriften in der Grundschrift (`\setkomafont{disposition}`),
  Bildunterschriften in `\normalsize`. **Im Text keine** `\small`, `\large`, `\fontfamily`, `\textsf` o. Ä.
- Titel = vorläufiges Projektthema; alle Gruppenmitglieder in `\author{… \and …}`.
- Zitierstil: `biblatex` mit `style=apa`, `backend=biber`; Quellenverzeichnis heißt „Quellenverzeichnis“.

## Konventionen beim Schreiben

- **Neues Kapitel** = neue Aufgabe: `kapitel/aufgabeN.tex` anlegen (Vorlage: `aufgabe1.tex`), in `main.tex` per `\include{kapitel/aufgabeN}` einbinden.
  Kopf: `\chapter{Titel}` mit inhaltlichem Titel **ohne** „Aufgabe N“ (z. B. `\chapter{Formative Evaluation}`)
  + `\label{chap:inhalt}` (z. B. `chap:formative_evaluation`).
- **Labels:** Präfix (`chap:`, `sec:`, `fig:`, `tab:`) + inhaltlicher Name, **keine** Aufgabennummer,
  z. B. `chap:projektthema`, `sec:pt-einleitung`, `fig:tick_it_s1`, `tab:themen`. Labels müssen im ganzen Dokument eindeutig sein.
- **Verweise** nur dynamisch mit `\cref{…}` / `\Cref{…}` (Satzanfang), nie Nummern von Hand.
- **Abbildungen:** `figure` mit `\centering`, `\includegraphics`, `\caption` **unter** dem Bild, danach `\label`.
  Nicht selbst erstellte Bilder: `\caption{… \bildquelle{bibkey}}` + Eintrag in `literatur.bib`.
- **Tabellen:** `table` mit `\caption` **über** der Tabelle, `booktabs` (`\toprule`, `\midrule`, `\bottomrule`), keine senkrechten Linien.
- **Zitate:** `\parencite{key}` (in Klammern), `\textcite{key}` (im Satz). Anführungszeichen mit `\enquote{…}`.
- **Ein Satz pro Zeile** im Quelltext (bessere Git-Diffs, weniger Konflikte).
- Deutsche Typografie: Dezimalkomma, `z.\,B.`, `d.\,h.`, geschützte Leerzeichen wie `Aufgabe~1`.

## Quellen (`literatur.bib`)

- Schlüssel: `nachnameJahr` (z. B. `wilkinson2016`) bzw. `organisation-thema` (z. B. `github-docs-repos`).
- Wissenschaftliche Quellen mit DOI, wenn vorhanden.
- **Internetquellen (`@online`): immer `url` UND `urldate` (Format `JJJJ-MM-TT`).** Ohne Erscheinungsjahr das
  `year`-Feld weglassen (wird automatisch „o. J.“). URLs müssen funktionieren – nicht erfinden.
- Keine Quellen, DOIs oder URLs erfinden. Unsichere Angaben als `% TODO prüfen` markieren.

## KI-Tools und Automatisierung

Jede Nutzung wird dreifach gekennzeichnet:
1. **An der Stelle im Text:** `\kihinweis{Tool}{Zweck/Umfang}{bibkey}` (erzeugt eine Fußnote mit Zitat).
2. **Im Quellenverzeichnis:** Eintrag `@software` mit `author` (Hersteller), `title` (Tool), `version` (Modell + Stand),
   `year`, `type = {Large language model}`, `url`, `urldate` (Datum der Nutzung). Beispiel: `openai2026`.
3. **Im Abschnitt „Beiträge“** des betroffenen Kapitels (erneut) nennen.

Auch Hilfe durch Claude selbst ist so zu kennzeichnen. Wenn Claude Text, Gliederung, Code, Abbildungen oder
Bib-Einträge für dieses Projekt erzeugt oder überarbeitet, weist Claude darauf hin, dass dies gekennzeichnet werden muss,
und schlägt einen passenden `@software`-Eintrag (`author = {{Anthropic}}`, `title = {{Claude}}`) sowie `\kihinweis` vor.
Die genaue Form richtet sich nach den Folien der Lehrveranstaltung – bei Abweichungen gelten die Folien.

## Abschnitt „Beiträge“ (Pflicht am Ende jedes Kapitels)

```latex
\begin{beitraege}
  Recherche und Literaturauswahl   & Name \\
  Text \cref{sec:pt-einleitung}     & Name \\
  \midrule
  KI/Automatisierung: Tool, Zweck \parencite{bibkey} & Name \\
\end{beitraege}
```
Für jeden Arbeitsschritt und jeden Textanteil das verantwortliche Gruppenmitglied angeben;
ohne KI-Nutzung: `KI/Automatisierung: keine & --`.

## Git

- Vor dem Arbeiten `git pull`, kleine Commits mit aussagekräftiger Nachricht, dann `git push`.
- Möglichst nur die eigene Kapiteldatei bearbeiten; `praeambel.tex` und `main.tex` nur nach Absprache.
- Keine Hilfsdateien oder `build/` committen.

## Vor der Abgabe

- Platzhalter (Namen, Titel, Beispielquellen und Beispielbilder) ersetzt bzw. entfernt.
- PDF ohne „??“, keine Warnungen zu fehlenden Zitaten oder Verweisen.
- Alle URLs aufgerufen, Abrufdaten stimmen.
- Rechtschreib-/Grammatikprüfung (z. B. LanguageTool/LTeX) und gegenseitiges Korrekturlesen.
- Jedes Kapitel hat einen vollständigen Abschnitt „Beiträge“.
