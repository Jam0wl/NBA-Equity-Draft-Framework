# Equity Draft Framework (EDF)

# Vollständige mathematische Spezifikation

Dieses Dokument enthält die vollständige formale Definition des Equity
Draft Framework (EDF), einschließlich:

-   Definition der Base-Funktion
-   Definition der Equity-Funktion
-   Lottery-Gewichtung
-   Best-Pick-Regel (Nicht-Handelbarkeit der Equity)
-   Gedämpfte Equity im Playoff-Bereich
-   Deterministische Vergabe der Picks 15--30
-   Klarstellung zur Second Round

------------------------------------------------------------------------

# 1. Grundnotation

Es gibt 30 Teams.

Für jedes Team $t$ gilt:

-   $W(t)$ = Anzahl Saison-Siege (0--82)
-   $W_{29}(t)$ = Siege in den Final 29 (0--29)

Nach Saisonende:

-   Top 16 Teams → Playoff-Pool
-   Bottom 14 Teams → Lottery-Pool

------------------------------------------------------------------------

# 2. Base-Funktion (strukturelles Gewicht)

Die Base eines Picks wird definiert als:

$$
Base(t) = 100 - W(t)
$$

Eigenschaften:

-   Weniger Saison-Siege → höhere Base
-   Mehr Saison-Siege → niedrigere Base
-   Base ist an den Pick gebunden und vollständig handelbar

------------------------------------------------------------------------

# 3. Equity-Funktion (einheitliche Währung)

Equity entsteht ausschließlich durch Siege in den Final 29.

Kalibriert wurde:

Ein Team mit 40 Siegen und 15 Final-29-Siegen soll 15 % mehr
Lottery-Gewicht haben als ein Team mit 20 Siegen und 0 Final-29-Siegen.

Daraus folgt:

$$
Equity(t) = 2{,}1333 \cdot W_{29}(t)
$$

Equity ist:

-   Nicht handelbar
-   Nicht übertragbar
-   Ausschließlich an die erspielende Franchise gebunden

------------------------------------------------------------------------

# 4. Lottery-Bereich (Picks 1--14)

Für Lottery-Teams gilt:

$$
Weight(t) = Base(t) + Equity(t)
$$

Zur Erzeugung ganzzahliger Lose:

$$
Tickets(t) = \text{round}(10 \cdot Weight(t))
$$

Die Ziehung erfolgt als gewichtetes Sampling ohne Zurücklegen.

Für Pick 1:

$$
P(t) = \frac{Tickets(t)}{\sum Tickets}
$$

Nach jeder Ziehung wird neu normalisiert, bis alle 14 Picks vergeben
sind.

------------------------------------------------------------------------

# 5. Best-Pick-Regel bei mehreren First-Round-Picks

Besitzt eine Franchise mehrere First-Round-Picks:

$$
BestPick(f) = \arg\max Base(s(p))
$$

Nur dieser Pick erhält:

$$
Base + Equity
$$

Alle weiteren Picks behalten ausschließlich ihre Base.

Equity wird exakt einmal pro Franchise angewendet.

------------------------------------------------------------------------

# 6. Playoff-Bereich (Picks 15--30)

Für Playoff-Teams wird kein Zufallsverfahren verwendet.

Die Reihenfolge ist deterministisch.

Zunächst wird ein gedämpfter Score definiert:

$$
Score_{PO}(t) = W(t) + \lambda \cdot Equity(t)
$$

Kalibrierungsziel:

Ein Unterschied von 10 Final-29-Siegen soll maximal 1,5 Plätze
verschieben.

Da:

$$
Equity-Differenz = 2{,}1333 \cdot 10 = 21{,}333
$$

muss gelten:

$$
\lambda \cdot 21{,}333 \le 1{,}5
$$

Daraus folgt:

$$
\lambda = 0{,}07
$$

Finale Definition:

$$
Score_{PO}(t) = W(t) + 0{,}07 \cdot Equity(t)
$$

Sortierung:

-   Höchster Score → Pick 15
-   Niedrigster Score → Pick 30

Maximaler Effekt über 29 Spiele:

$$
0{,}07 \cdot (2{,}1333 \cdot 29) \approx 4{,}33
$$

Das entspricht maximal ca. 4,33 Draft-Plätzen.

------------------------------------------------------------------------

# 7. Second Round (Picks 31--60)

Die Second Round bleibt unverändert.

Sie folgt vollständig der bestehenden NBA-Logik.

EDF greift ausschließlich in die Struktur der First Round ein.

------------------------------------------------------------------------

# 8. Systemzusammenfassung

Lottery (1--14): Zufällige Ziehung basierend auf Base + voller Equity.

Playoffs (15--30): Deterministische Sortierung basierend auf Wins +
gedämpfter Equity.

Second Round: Unverändert.

Equity ist ligaweit eine einzige Währung. Base ist handelbar. Equity ist
nicht handelbar.


------------------------------------------------------------------------

# 9. Strikte Poolbindung der Equity-Anwendung (Formale Ergänzung)

Die Anwendung der Equity unterliegt einer strukturellen Poolbindung.

Definition:

Sei Pool(t) ∈ {Lottery, Playoff} die Saison-Pool-Zugehörigkeit eines Teams t.

## 9.1 Poolbindung im Lottery-Bereich

Für Picks 1–14 gilt formal:

Weight(t) = Base(t) + Equity(t),

nur falls Pool(t) = Lottery.

Falls Pool(t) = Playoff, gilt:

Weight(t) = Base(t)

auch dann, wenn die betreffende Franchise durch Trades einen
Lottery-Pick besitzt.

Damit kann eine Playoff-Franchise ihre Equity nicht zur Verstärkung eines
Lottery-Picks einsetzen.

## 9.2 Poolbindung im Playoff-Bereich

Für Picks 15–30 gilt:

Score_PO(t) = W(t) + 0,07 · Equity(t),

nur falls Pool(t) = Playoff.

Falls Pool(t) = Lottery, gilt:

Score_PO(t) = W(t)

auch dann, wenn die betreffende Franchise durch Trades einen
Playoff-Pick besitzt.

Damit kann eine Lottery-Franchise ihre Equity nicht zur Verbesserung
eines Playoff-Picks einsetzen.

## 9.3 Best-Pick-Regel unter Poolbindung

Die Definition

BestPick(f) = argmax Base(s(p))

gilt ausschließlich innerhalb des Pools, in dem Franchise f die Saison
beendet hat.

Equity wird pro Franchise exakt einmal angewendet und nur auf einen Pick
im eigenen Pool.

Besitzt eine Franchise keinen Pick in ihrem Saison-Pool, verfällt die
Equity für diesen Draftjahrgang.

------------------------------------------------------------------------

Diese Ergänzung ändert keine mathematische Kernfunktion, sondern
präzisiert die zulässige Anwendungsmenge der Equity.
