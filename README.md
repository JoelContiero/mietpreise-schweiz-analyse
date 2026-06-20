# Entwicklung der Wohnungsmieten in der Schweiz

Eine Datenanalyse mit Python und Power BI auf Basis offener Daten des Bundesamts für Statistik (BFS).

## Leitfrage

> **Wie stark sind die Wohnungsmieten in der Schweiz in den letzten 10–15 Jahren gestiegen — und hielt das mit der Lohn- und Teuerungsentwicklung Schritt?**

Als Folgeanalyse (Teil 2):

> **Welche Kantone/Regionen sind beim Mietanstieg Spitzenreiter, welche Nachzügler — und wo steht der Kanton Zürich?**

## Einfach erklärt (für alle)

**Worum geht es?** Mieten steigen – das spürt jede:r. Dieses Projekt prüft mit offiziellen Zahlen zwei Dinge: *Steigen die Mieten schneller als die Löhne?* und *In welchen Kantonen ist es am extremsten?*

**Die kurze Antwort auf Frage 1:** Die Mieten sind im letzten Jahrzehnt gestiegen (rund +8 % zwischen 2010 und 2020) – aber die Löhne sind ungefähr gleich schnell mitgewachsen. Weil die allgemeinen Preise (die Teuerung) in dieser Zeit kaum stiegen, blieb am Ende des Monats real etwa gleich viel übrig. **Wichtig:** Diese Zahlen reichen nur bis 2020. Der starke Mietsprung ab 2022 ist hier noch nicht enthalten.

**Die kurze Antwort auf Frage 2:** Es gibt ein klares Stadt-Land- bzw. Zentrums-Gefälle. Am teuersten wohnt man in Zug, **Zürich** und Genf, am günstigsten im Jura. Und die teuren Kantone wurden tendenziell noch teurer: Zürich gehört sowohl beim Preis-*Niveau* als auch beim *Anstieg* (2012–2024) zu den Top 3.

**Kurz erklärt – die wichtigsten Begriffe:**

| Begriff | Was es bedeutet |
|---|---|
| **Nominallohn** | Der Lohn in Franken, wie er auf dem Lohnzettel steht – ohne Berücksichtigung der Preise. |
| **Reallohn** | Der Lohn umgerechnet auf die *Kaufkraft*: Wie viel man sich davon wirklich leisten kann. Steigt der Reallohn, sind die Löhne schneller gewachsen als die Preise. |
| **Teuerung / Inflation** | Wie stark die Preise allgemein steigen (gemessen am Landesindex der Konsumentenpreise, LIK). |
| **Mietpreisindex** | Eine Messzahl, die zeigt, wie sich die Mieten über die Zeit verändern – nicht der Preis in Franken, sondern relativ zu einem Startjahr (hier Dezember 2015 = 100). |
| **Index (z. B. 2010 = 100)** | Ein Trick, um Dinge mit unterschiedlichen Einheiten vergleichbar zu machen: Man setzt ein Jahr auf 100 und misst alles andere daran. Bei 108 ist der Wert 8 % höher als im Startjahr. |
| **Fr./m²** | Monatsmiete pro Quadratmeter. So lassen sich grosse und kleine Wohnungen fair vergleichen. |

## Erste Ergebnisse (Frage 1)

![Mieten, Löhne und Teuerung im Vergleich](figures/mieten_vs_loehne.png)

- **Mieten 2010–2020: rund +8 %** — ein spürbarer, aber moderater Anstieg.
- Die Mieten stiegen **leicht schneller als die Nominallöhne** (+8,2 % vs. +7,2 %).
- **Trotzdem kein realer Kaufkraftverlust:** Die Reallöhne legten am stärksten zu (+8,7 %), weil die Teuerung im Jahrzehnt sehr tief war. Die Löhne hielten also mit den Mieten Schritt.

> Datenstand bis 2020 (Grenze der Lohnreihe). Der starke Miet-/Preisanstieg ab 2022 ist noch nicht enthalten.

## Ergebnisse Frage 2: Mieten nach Kanton

**Niveau 2024 — wo steht Zürich?**

![Mieten nach Kanton 2024](figures/miete_kanton_ranking_2024.png)

- Teuerste Kantone: **Zug, Zürich, Genf** (~21 Fr./m²); günstigste: **Jura, Neuenburg, Appenzell A.Rh.**
- **Zürich liegt auf Rang 2 von 26** und rund 20 % über dem Schweizer Schnitt (17,8 Fr./m²).
- Kleine Wohnungen kosten pro m² am meisten (siehe Heatmap im Notebook).

**Entwicklung 2012–2024 — wer ist am stärksten gestiegen?**

![Anstieg nach Kanton](figures/miete_kanton_anstieg.png)

- Schweizweit stiegen die Mieten pro m² um **rund +12 %**.
- Am stärksten: **Glarus (+19,5 %), Basel-Stadt (+16,6 %), Zürich (+15,1 %)**; am wenigsten Appenzell A.Rh. (+6,9 %).
- **Zürich ist sowohl im Niveau (Rang 2) als auch beim Anstieg (Rang 3) vorne** — teure Kantone wurden tendenziell noch teurer.

> Datengrundlage: BFS-Strukturerhebung, durchschnittliche Nettomiete pro m². Die Jahres-Zeitreihe 2012–2022 stammt aus einer mehrblättrigen BFS-Tabelle, 2024 aus der aktuellen Einzeltabelle (2023 ist in den offenen Daten nicht enthalten).

## Vorgehen

1. **Daten beschaffen** — offene Datensätze von [opendata.swiss](https://opendata.swiss) / BFS
2. **Aufbereiten** — Bereinigung und Strukturierung mit Python/pandas (`notebooks/01_datenaufbereitung.ipynb`)
3. **Analysieren** — explorative Auswertung und Visualisierung (`notebooks/02_analyse.ipynb`)
4. **Präsentieren** — interaktives Dashboard in Power BI (`powerbi/`)

## Datenquellen

| Datensatz | Quelle | Verwendung |
|---|---|---|
| Mietpreisindex (Entwicklung der Mietpreise für Wohnungen, Jahresdurchschnitte) | BFS – LIK | Frage 1: Mietentwicklung über die Zeit |
| Nominallöhne, Konsumentenpreise und Reallöhne | BFS | Frage 1: Vergleich Löhne ↔ Teuerung (enthält Lohn- *und* Preisentwicklung in einer Datei) |
| Durchschnittlicher Mietpreis pro m² nach Zimmerzahl und Kanton (2012–2022 + 2024) | BFS – Strukturerhebung | Frage 2: Mieten nach Kanton, Niveau und Anstieg |

> Hinweis: Der Mietpreisindex ist ein Teilindex des LIK (Basis Dez. 2015 = 100), wodurch sich Miete und Teuerung direkt vergleichen lassen.

## Projektstruktur

```
data/
  raw/          Rohdaten, unverändert wie heruntergeladen
  processed/    bereinigte, analysefertige Daten
notebooks/      Jupyter Notebooks (Aufbereitung + Analyse)
powerbi/        Power-BI-Datei (.pbix) und Dashboard-Screenshots
```

## Verwendete Werkzeuge

Python (pandas, matplotlib, seaborn), Jupyter, Power BI Desktop.

---

*Lernprojekt — entwickelt mit Unterstützung von Claude Code.*
