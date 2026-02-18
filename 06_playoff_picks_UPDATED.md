
# Playoff-Picks (15--30)

## Deterministische Vergabe mit gedämpfter Equity

Die Picks 15 bis 30 betreffen ausschließlich die 16 Teams des
Playoff-Pools.
Im Equity Draft Framework (EDF) werden diese Picks nicht zufällig
vergeben, sondern deterministisch berechnet.

Ziel dieses Moduls ist es, die Regular Season weiterhin als dominanten
Leistungsindikator zu erhalten, gleichzeitig jedoch dem Saisonendspurt
eine kontrollierte, messbare Bedeutung zu geben.

------------------------------------------------------------------------

# 1. Grundprinzip

Nach Abschluss der regulären Saison werden die 16 besten Teams in den
Playoff-Pool eingeordnet.

Für diese Teams wird kein Lottery-Verfahren angewendet.

Stattdessen wird ein Score berechnet, der aus zwei Komponenten besteht:

1.  Saison-Siege
2.  Gedämpfte Equity

Die Teams werden nach diesem Score sortiert.

-   Höchster Score → Pick 15
-   Niedrigster Score → Pick 30

------------------------------------------------------------------------

# 2. Definition des Playoff-Scores

Der Score für ein Playoff-Team t wird definiert als:

Score_PO(t) = W(t) + λ × Equity(t)

Dabei gilt:

W(t) = Anzahl der Saison-Siege
Equity(t) = 2,1333 × W29(t)
λ = 0,07

Damit lautet die vollständige Formel:

Score_PO(t) = W(t) + 0,07 × (2,1333 × W29(t))

------------------------------------------------------------------------

# 3. Poolbindung der Equity

Equity wirkt im Playoff-Bereich ausschließlich für Franchises,
die die Saison im Playoff-Pool beendet haben.

Eine Franchise, die die Saison im Lottery-Pool beendet hat,
kann ihre Equity nicht zur Verbesserung eines Playoff-Picks einsetzen –
selbst dann nicht, wenn sie durch Trades einen Playoff-Pick besitzt.

Diese Regel verhindert poolübergreifende Arbitrage.

------------------------------------------------------------------------

# 4. Kalibrierung der Dämpfung (λ)

Ein Unterschied von 10 Final-29-Siegen soll maximal 1,5 Draft-Plätze
verschieben.

2,1333 × 10 = 21,333
0,07 × 21,333 ≈ 1,49

------------------------------------------------------------------------

# 5. Maximaler Effekt

0,07 × (2,1333 × 29) ≈ 4,33

Ein außergewöhnlicher Endspurt kann somit maximal etwa vier Draft-Plätze
verschieben.

------------------------------------------------------------------------

# 6. Gleichstände

Bei identischem Score_PO wird ein minimaler deterministischer Tiebreaker
angewendet (z. B. feste Team-ID oder Net Rating).

------------------------------------------------------------------------

# 7. Zusammenfassung

Lottery (1--14): Zufällige Ziehung mit voller Equity-Wirkung
nur für Lottery-Franchises.

Playoffs (15--30): Deterministische Sortierung mit gedämpfter
Equity-Wirkung nur für Playoff-Franchises.
