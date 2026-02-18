# Mathematische Herleitung und formale Definitionen

Dieses Dokument enthält die vollständige mathematische Ausarbeitung des
Equity Draft Framework (EDF).

Hier werden später definiert:

-   Variablen und Notation
-   Definition der Base-Funktion
-   Definition der Equity-Funktion
-   Gewichtungslogik für Lottery-Picks
-   Full 1--14 Draw Verfahren
-   Playoff-Pick-Ordnungsfunktion
-   Nicht-Handelbarkeit der Equity (formale Definition)
-   Kalibrierungsbedingungen (z. B. 15-von-29-Schwelle)
-   Beispielrechnungen
-   Sensitivitätsanalysen

## Mathematische Ausarbeitung des Equity Draft Framework (EDF)

Die folgende Darstellung ist die vollständige formale Systemdefinition des Equity Draft Framework mit Variablen, Regeln, Ableitungen und Rechenbeispielen. Sie folgt der internen Spezifikation aus deinem Master-Log. 

---

### 1. Grundmengen und Notation

Die Liga besteht aus 30 Teams. Jedes Team wird mit (t) bezeichnet.

Für jedes Team (t) werden zwei zentrale Saisonwerte definiert.

Es gilt (W(t)) als die Gesamtzahl der Siege in der regulären Saison. Damit ist (W(t)\in{0,1,\dots,82}).

Es gilt (W_{29}(t)) als die Zahl der Siege in den Final 29. Damit ist (W_{29}(t)\in{0,1,\dots,29}).

Die Final 29 sind als Endfenster der Saison so definiert, dass jedes Team in diesem Fenster genau einmal gegen jedes der anderen 29 Teams spielt. Dadurch wird (W_{29}(t)) zwischen allen Teams direkt vergleichbar.

---

### 2. Pool-Bildung nach Saisonende

Nach Ende der regulären Saison werden alle Teams primär nach (W(t)) absteigend sortiert.

Bei Gleichstand in (W(t)) wird als erster Tiebreaker (W_{29}(t)) verwendet, ebenfalls absteigend.

Es entstehen zwei Pools.

Der Playoff-Pool (P) besteht aus den bestplatzierten 16 Teams.

Der Lottery-Pool (L) besteht aus den verbleibenden 14 Teams.

Damit gilt (|P|=16) und (|L|=14).

---

### 3. Draft-Ausgänge: Grundstruktur

Die Picks 1 bis 14 werden ausschließlich unter den Lottery-Teams vergeben.

Die Picks 15 bis 30 werden ausschließlich unter den Playoff-Teams vergeben.

EDF definiert dabei zwei unterschiedliche Vergabemechanismen.

Für den Lottery-Pool (L) wird die komplette Reihenfolge 1 bis 14 durch ein gewichtetes Ziehen ohne Zurücklegen bestimmt.

Für den Playoff-Pool (P) wird die Reihenfolge 15 bis 30 deterministisch über eine eindeutige Leistungskennzahl bestimmt.

---

### 4. Deterministische Ordnung für Picks 15–30

EDF verlangt, dass innerhalb des Playoff-Pools keine zwei Teams denselben Rang „teilen“ können. Deshalb wird eine streng eindeutige Punktzahl (TP(t)) konstruiert.

Es gilt

[
TP(t)=30\cdot W(t)+W_{29}(t)+\varepsilon(t)
]

Dabei ist (\varepsilon(t)) ein deterministischer, eindeutiger Bruchteil in ((0,1)), der nur dazu dient, absolute Eindeutigkeit zu erzwingen.

Eine einfache Spezifikation ist

[
\varepsilon(t)=\frac{ID(t)}{1000}
]

wobei (ID(t)\in{1,\dots,30}) ein fest zugewiesener Team-Identifier ist.

Die Draftordnung im Playoff-Pool ist dann wie folgt definiert.

Das Team mit dem höchsten (TP(t)) erhält Pick 15.

Das Team mit dem niedrigsten (TP(t)) erhält Pick 30.

Damit ist die Zuordnung deterministisch und kollisionsfrei.

---

### 5. Lottery-Mathematik: Base und Equity

EDF zerlegt die Lottery-Gewichtung in zwei strikt getrennte Komponenten.

Komponente A heißt Base und hängt nur von der Saisonbilanz des Quellteams eines Picks ab. Base ist handelbar, weil sie am Pick-Asset hängt.

Komponente B heißt Equity und hängt nur von der Final-29-Performance einer Franchise ab. Equity ist nicht handelbar, weil sie an die Franchise-Leistung gebunden ist.

---

#### 5.1 Base als Funktion der Saison-Siege

Für ein Quellteam (s) wird die Base so definiert:

[
Base(s)=B_{\max}-m\cdot W(s)
]

Dabei sind (B_{\max}>0) und (m>0) politische Parameter.

Damit gilt automatisch: Je mehr Siege (W(s)), desto kleiner (Base(s)).

Die Parameter müssen so gewählt werden, dass (Base(s)) für alle realistischen (W(s)) positiv bleibt.

---

#### 5.2 Equity als Funktion der Final-29-Siege

Für eine Franchise (f) wird Equity so definiert:

[
Equity(f)=k\cdot W_{29}(f)
]

Dabei ist (k>0) ein politischer Skalierungsparameter.

Damit gilt: Jeder Final-29-Sieg erzeugt exakt (k) Einheiten Equity.

---

### 6. Die zentrale Trade-Regel: Equity ist nicht handelbar

EDF erlaubt Pick-Trading weiterhin vollständig, aber trennt sauber zwischen „Pick-Asset“ und „Leistungs-Asset“.

Ein First-Round-Pick (p) besitzt eine Base, weil er ein Quellteam (s(p)) hat. Diese Base reist mit dem Pick.

Eine Franchise (f) besitzt Equity, weil sie sie erspielt hat. Diese Equity reist niemals mit einem Pick.

Formal wird das so implementiert, dass nach allen Trades zuerst die Equity der Franchise berechnet wird und anschließend nur auf exakt einen Pick angewendet werden darf.

---

#### 6.1 „Best-Pick“-Anwendungsregel

Sei (OwnedFirsts(f)) die Menge aller First-Round-Picks, die Franchise (f) im aktuellen Draft besitzt.

Jeder Pick (p\in OwnedFirsts(f)) hat ein Quellteam (s(p)) und damit eine Base (Base(s(p))).

EDF definiert den besten Pick einer Franchise über die Base-Stärke ohne Equity:

[
BestPick(f)=\arg\max_{p\in OwnedFirsts(f)} Base(s(p))
]

Das bedeutet: Der „beste Pick“ ist derjenige mit der höchsten Base, bevor Equity addiert wird.

---

#### 6.2 Gewicht eines Picks nach EDF

Für jeden Pick (p), der Franchise (f) gehört, gilt das Lottery-Gewicht (Weight(p)):

Wenn (p=BestPick(f)), dann gilt

[
Weight(p)=Base(s(p))+Equity(f)
]

Wenn (p\neq BestPick(f)), dann gilt

[
Weight(p)=Base(s(p))
]

Damit wird Equity exakt einmal pro Franchise angewendet, unabhängig davon, wie viele Picks diese Franchise besitzt.

Das ist der Mechanismus, der verhindert, dass man Equity „kauft“ oder über mehrere Picks verteilt.

---

### 7. Ziehungsprozedur: Full 1–14 Draw ohne Zurücklegen

Sei (PicksInLottery) die Menge der 14 Lottery-Picks (nach Trades) mit jeweils definiertem (Weight(p)).

Die Ziehung erzeugt eine vollständige Reihenfolge der Picks 1 bis 14.

Für Pick 1 wird ein Pick (p) zufällig gewählt mit Wahrscheinlichkeit

[
\Pr(p \text{ wird Pick 1})=\frac{Weight(p)}{\sum_{q\in PicksInLottery} Weight(q)}
]

Der gezogene Pick wird aus der Menge entfernt.

Für Pick 2 wird erneut aus den verbleibenden Picks gezogen, wieder proportional zu den verbleibenden Gewichten.

Das wird fortgesetzt, bis alle 14 Positionen vergeben sind.

Mathematisch ist das ein gewichtetes Sampling ohne Zurücklegen mit Renormalisierung nach jedem Ziehschritt.

---

### 8. Kalibrierungsbedingung: die „15 von 29“-Schwelle

EDF enthält eine explizite Designanforderung zur Parameterkalibrierung.

Die Anforderung lautet: Das beste Team innerhalb des Lottery-Pools, also das „14.-schlechteste“ Team, soll ein sehr schlechtes Team in der Gesamtgewichtung überholen können, wenn es in den Final 29 stark performt, konkret mit 15 Siegen.

Formal wird das als Ungleichung formuliert.

Team (A) sei das beste Lottery-Team mit Saison-Siegen (W_A) und Final-29-Siegen (W_{29,A}=15).

Team (B) sei ein 20-Siege-Team, also (W_B=20). Für eine konservative Vergleichsrechnung wird (W_{29,B}=0) gesetzt.

Die Bedingung lautet

[
Base(A)+15k>Base(B)
]

Mit (Base(x)=B_{\max}-m\cdot W(x)) ergibt sich

[
(B_{\max}-mW_A)+15k>(B_{\max}-m\cdot 20)
]

(B_{\max}) kürzt sich heraus:

[
-mW_A+15k>-20m
]

Umformen liefert

[
15k>m\cdot(W_A-20)
]

Das ist die zentrale Kalibrierungsformel: Sie sagt direkt, wie groß (k) im Verhältnis zu (m) sein muss, abhängig vom plausiblen Wert (W_A).

---

#### 8.1 Beispielrechnung

Ein plausibler konservativer Wert für das beste Lottery-Team liegt im Bereich Mitte 30 Siege. Setze beispielhaft (W_A=35).

Dann gilt

[
15k>m\cdot(35-20)=15m
]

Damit folgt

[
k>m
]

Eine „saubere“ Parameterauswahl ist beispielsweise

[
k=1.2m
]

Dann ist die Schwelle strikt erfüllt.

Die Aussage dahinter ist absichtlich klar: Ein Final-29-Sieg soll mindestens so viel „wert“ sein wie der Base-Vorteil, den man durch zusätzliche Saison-Niederlagen generieren würde.

---

### 9. Größenordnung: Warum Base nicht dominieren darf

EDF verfolgt die Absicht, dass Final-29-Performance nicht zur Rundungsnote wird.

Eine praktische Vergleichslogik lautet: Die Spannweite der Base über den Lottery-Bereich soll in derselben Größenordnung liegen wie die Spannweite realistischer Equity-Werte.

Wenn Lottery-Teams über die Saison typischerweise zwischen etwa 14 und 35 Siege haben, dann beträgt die Base-Spannweite

[
Base(14)-Base(35)=m\cdot(35-14)=21m
]

Wenn Final-29-Siege bei Lottery-Teams realistisch etwa zwischen 5 und 18 liegen, dann beträgt die Equity-Spannweite

[
k\cdot(18-5)=13k
]

Wählt man (k) ungefähr in der Größenordnung von (m), dann wird Equity zu einem echten, spürbaren Steuerungshebel und nicht zu einem kosmetischen Add-on.

---

### 10. Formale Ein-Satz-Zusammenfassung der Trade-Compliance

Ein First-Round-Pick-Asset (p) besteht aus (Base(s(p))) und ist handelbar.

Die Equity einer Franchise (f) ist (Equity(f)=k\cdot W_{29}(f)), ist nicht handelbar und darf nur auf den base-stärksten First-Round-Pick angewendet werden, den (f) aktuell besitzt.

Jede Implementierung, die Equity mit einem Pick über Ownership-Grenzen hinweg überträgt, ist nicht EDF-konform. 

---

Wenn du willst, setze ich dir daraus jetzt direkt eine publikationsfertige Version für `08_mathematics.md`, mit konsistenten Definitionen, Beispielzahlen (mit frei wählbaren Parametern (B_{\max}, m, k)) und einem vollständig ausgeschriebenen Mini-Lottery-Beispiel mit drei Teams, damit Leser das Ziehen ohne Zurücklegen intuitiv nachvollziehen können.

