# Mathematische Herleitung des Equity Draft Framework (EDF)

Dieses Dokument enthält die vollständige mathematische Definition des
Equity Draft Framework inklusive eines durchgerechneten Beispiels mit
ganzzahligen Lottery-Tickets.

------------------------------------------------------------------------

# 1. Grunddefinitionen

Es gibt 30 Teams. Für jedes Team $t$ gilt:

-   $W(t)$ = Saison-Siege (0--82)
-   $W_{29}(t)$ = Siege in den Final 29 (0--29)

Nach Saisonende werden die Teams nach $W(t)$ sortiert.

-   Die 16 besten Teams bilden den Playoff-Pool.
-   Die 14 restlichen Teams bilden den Lottery-Pool.

------------------------------------------------------------------------

# 2. Base-Funktion

Die strukturelle Ausgangsgewichtung eines Picks wird definiert als:

$$
Base(t) = 100 - W(t)
$$

Damit gilt: - Weniger Saison-Siege → höhere Base - Mehr Saison-Siege →
niedrigere Base

------------------------------------------------------------------------

# 3. Equity-Funktion

Equity entsteht ausschließlich durch Siege in den Final 29.

Kalibrierungsziel: Ein Team mit 40 Siegen und 15 Final-29-Siegen soll 15
% mehr Lottery-Gewicht haben als ein Team mit 20 Siegen und 0
Final-29-Siegen.

Daraus ergibt sich:

$$
Equity(t) = k \cdot W_{29}(t)
$$

mit

$$
k = 2{,}1333
$$

------------------------------------------------------------------------

# 4. Gesamtgewicht

$$
Weight(t) = Base(t) + Equity(t)
$$

Da Lottery-Tickets ganzzahlig sein müssen, skalieren wir das Gewicht mit
Faktor 10:

$$
Tickets(t) = \text{round}(10 \cdot Weight(t))
$$

Damit entstehen ausschließlich ganze Lose.

------------------------------------------------------------------------

# 5. Beispiel-Saison (Lottery-Teams)

Annahme: Alle Teams besitzen ihren eigenen Pick.

  Team        W    W29   Base   Equity   Tickets
  ----------- ---- ----- ------ -------- ---------
  Pistons     18   6     82     12,8     948
  Wizards     20   4     80     8,5      885
  Hornets     22   9     78     19,2     972
  Spurs       24   12    76     25,6     1016
  Blazers     26   10    74     21,3     953
  Grizzlies   28   14    72     29,9     1019
  Jazz        29   8     71     17,1     881
  Raptors     30   13    70     27,7     977
  Nets        32   11    68     23,5     915
  Hawks       34   15    66     32,0     980
  Bulls       35   12    65     25,6     906
  Rockets     36   16    64     34,1     981
  Magic       38   7     62     14,9     769
  Pacers      39   5     61     10,7     717

------------------------------------------------------------------------

# 6. Lottery-Verfahren (Full 1--14 Draw)

Die Ziehung erfolgt ohne Zurücklegen.

Für Pick 1 gilt:

$$
P(t) = \frac{Tickets(t)}{\sum Tickets}
$$

Nach Ziehung wird das Team entfernt und neu normalisiert.

------------------------------------------------------------------------

# 7. Beispielhafte Ziehung

Ein möglicher Ausgang:

1.  Grizzlies\
2.  Spurs\
3.  Hawks\
4.  Rockets\
5.  Hornets\
6.  Raptors\
7.  Pistons\
8.  Blazers\
9.  Nets\
10. Bulls\
11. Wizards\
12. Jazz\
13. Magic\
14. Pacers

------------------------------------------------------------------------

# 8. Nachweis der 15%-Kalibrierung

Team A: - W = 40 - W29 = 15

$$
Base = 60
$$

$$
Equity = 32
$$

$$
Weight = 92
$$

Team B: - W = 20 - W29 = 0

$$
Base = 80
$$

$$
Weight = 80
$$

$$
\frac{92}{80} = 1{,}15
$$

Team A erhält exakt 15 % mehr Gewicht.

------------------------------------------------------------------------

# 9. Best-Pick-Regel (bei Trades)

Besitzt eine Franchise mehrere First-Round-Picks, wird Equity
ausschließlich auf den Pick mit der höchsten Base angewendet.

Formal:

$$
BestPick(f) = \arg\max Base(s(p))
$$

Nur dieser Pick erhält:

$$
Base + Equity
$$

Alle anderen Picks behalten ausschließlich ihre Base.

Equity ist nicht handelbar.
