# Projektbericht – LaTeX-Vorlage

## Struktur

| Datei | Inhalt |
|---|---|
| `main.tex` | Titel, Autor*innen, Einbindung der Kapitel |
| `praeambel.tex` | Layout, Pakete, Hilfsbefehle (nur nach Absprache ändern) |
| `kapitel/aufgabeN.tex` | ein Kapitel pro Aufgabe |
| `literatur.bib` | alle Quellen inkl. KI-Tools |
| `bilder/` | Abbildungen (bevorzugt PDF/PNG) |

## Kompilieren

```
latexmk main.tex
```
Ergebnis: `build/main.pdf`. Benötigt pdflatex, biber und biblatex-apa (in TeX Live/MiKTeX enthalten).
In Overleaf: Menü → Compiler „pdfLaTeX“; biber wird automatisch erkannt.

## Regeln für die Gruppe

- **Verweise** immer mit `\label{...}` + `\cref{...}`, nie „Abbildung 3“ von Hand tippen.
  Präfixe: `chap:`, `sec:`, `fig:`, `tab:` plus Kürzel der Aufgabe (z. B. `fig:a1-...`).
- **Bilder:** `\caption` unter dem Bild; fremde Bilder mit `\bildquelle{bibkey}` und Eintrag in `literatur.bib`.
- **Tabellen:** `\caption` über der Tabelle.
- **Internetquellen:** immer `url` **und** `urldate`; Links vor Abgabe noch einmal anklicken.
- **KI/Automatisierung:** an der Stelle mit `\kihinweis{Tool}{Zweck}{bibkey}` markieren,
  das Tool als `@software` in `literatur.bib` eintragen und im Abschnitt „Beiträge“ des Kapitels erneut nennen.
- **Keine Schriftwechsel:** keine `\small`, `\Large`, `\fontfamily` o. Ä. im Text.
- **Ein Satz pro Zeile** – macht Diffs lesbar und vermeidet Merge-Konflikte.

## Git-Workflow

1. `git pull` vor dem Arbeiten.
2. Möglichst nur „eure“ Kapiteldatei bearbeiten.
3. Kleine Commits mit klarer Nachricht, dann `git push`.
4. Optional: Overleaf-Projekt über *Menu → GitHub* mit dem Repository verknüpfen.

## Vor der Abgabe

- [ ] Alle Platzhalter (Namen, Titel, Beispielquellen) ersetzt
- [ ] Keine „??“ im PDF (offene Verweise) und keine Warnungen zu fehlenden Zitaten
- [ ] Alle URLs funktionieren, Abrufdaten aktuell
- [ ] Rechtschreib- und Grammatikprüfung (z. B. LanguageTool / LTeX-Erweiterung in VS Code) + gegenseitiges Korrekturlesen
- [ ] Jedes Kapitel hat einen vollständigen Abschnitt „Beiträge“
