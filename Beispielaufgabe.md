# Beispielaufgabe

### Fabrik hat 7 Produkte für welche folgende Maschinen Verwendet werden:

- 4 Schleifer
- 2 Vertikale Bohrer
- 3 horizontale Bohrer
- 1 Fräse
- 1 Hobel

**Gewinn: Preis - Materialkosten**

**Maschinen: Arbeitszeit (in h)**

|            | Prod1 | Prod2 | Prod3 | Prod4 | Prod5 | Prod7 | Prod7
|-----------:|:-----|:------|:------|:------|:------|:------|:------|
Gewinn | 10 | 6 | 8 | 4 | 11 | 9 | 3 |
Schleifen | 0.5 | 0.7 | - | - | 0.3 | 0.2 | 0.5 |
vertikal bohren | 0.1 | 0.2 | - | 0.3 | - | 0.6 | - |
horizontal bohren | 0.2 | - | 0.8 | - | - | - | 0.6 |
Fräsen | 0.05 | 0.03 | - | 0.07 | 0.1 | - | 0.08 |
hobeln | - | - | 0.01 | - | 0.05 | - | 0.05 |

### Aber: Maschinen müssen gewartet werden!

| Monat | Maschine |
|------:|---------:|
| Jan | 1 Schleifer |
| Feb | 2 h. Bohrer|
| Mär | 1 Fräse |
| Apr | 1 v. Bohrer|
| Mai | 1 Schleifer + 1 v. Bohrer |
| Jun | 1 h. Bohrer |


### Limits für Verkauf pro Monat:

| Monat | Prod1 | Prod2 | Prod3 | Prod4 | Prod5 | Prod7 | Prod7
|-----------:|:-----|:------|:------|:------|:------|:------|:------|
Jan | 500 | 1000 | 300 | 300 | 800 | 200 | 100 |
Feb | 600 | 500 | 200 | 0 | 400 | 300 | 150  |
Mär | 300 | 600 | 0 | 0 | 500 | 400 | 100 |
Apr | 200 | 300 | 400 | 500 | 200 | 0 | 100 |
Mai | 0| 100 | 500 | 100 | 1000 | 300 | 0 |
Jun | 500 | 500 | 100 | 300 | 1100 | 500 | 60 |


### Lagerung: 

- 100 Einheiten pro Produkt
- Kosten: 0.50 €
- Januar: Lager leer
- Juni: 50 Einheiten

### Arbeit: 
    
- 6 Tage / Woche, 2 * 8h Schicht
- 24 Arbeitstage / Monat

## Wie soll der Produktionsplan aussehen?

# Mathematische modellierung

### Sets

$T$ = Zeitdauer(Monate) -> $T_0$ = 1. Monat, $T_e$ = letzter 

$P$ = Produkte

$M$ = Maschinen


### Parameter

- Für jedes Produkt $p \in P$ und Maschine $m \in M$ ist die Zeit $f_{p,m}$ gegeben, in der das Produkt in der Maschine bearbeitet wird
- Für jeden Monat $t \in T$ und jedes Produkt $p \in P$ gibt es ein Limit $l_{t,p}$, wie oft es Verkauft werden kann
- Für jedes Produkt $p \in P$ gibt es einen Profit $k_p$
- Für jeden Monat $t \in T$ und jede Maschine $m \in M$ gibt es eine Anzahl an verfügbaren Maschinen $q_{t,m}$
- Jede Maschine arbeitet $h$ Stunden im Monat
- Es können $z$ Einheiten von jedem Produkt für die Kosten $r$ pro Monat gelagert werden 



### Variablen

Für jeden Monat $t$ und Produkt $p$ werden folgende nichtnegative Variablen eingeführt: $b_{t,p} , u_{t,p} , s_{t,p}$.

- $b_{t,p}$ beschreibt die Produktionsanzahl eines Produkts pro Monat
- $u_{t,p}$ beschreibt die Verkaufsanzahl eines Produktes pro Monat
- $s_{t,p}$ beschreibt die Lageranzahl eines Produktes pro Monat



### Objective funktion

**Objective/ Ziel: Maximaler Profit**

$max \sum_\limits{t\in T} \sum_\limits{p\in P} (k_p * u_{t,p} - r * s_{t,p})$

### Constraints


$s_{t-q,p} + b_{t,p} = u_{t,p} + s_{t,p} \forall t \in T \ t_0, \forall p \in P$

$b_{t_0,p} = u_{t_0,p} + s_{t_0,p} \forall p \in P$

"Balance Constraints": Es können nur so viele Produkte gekauft($u_{t,p}$) und eingelagert($s_{t,p}$) werden, wie im Vorherigen Monat gelagert($s_{t-q,p}$) waren und in diesem Monat produziert($b_{t,p}$) wurden.


$s_{t_e,p} = z \forall p \in P$

"Endstore Constraints": Am Ende des letzten Monats muss das Lageranzahl($s_{t_e,p}$) für jedes Produkt dem maximalen Lagerplatz($z$) entsprechen  


$s_{t,p} \leq z \forall p \in P, \forall t \in T$

"Store Capacity Constraints": Es es können nich mehr Produkte eingelagert werden($s_{t,p}$), als es Lagerplatz($z$) gibt.


$ \sum_\limits{p\in P} f_{p,m} * b_{t,p} \leq h * q_{t,m} \forall t \in T, \forall m \in M$

"Capacity Constraints": Die Zeit in der alle Produkte an den jeweiligen Maschinen produziert werden muss kleiner sein als die Gesamtarbeitszeit($h$) aller verfügbaren Maschinen($q_{t,m}$)


```python

```
