# Lottery (Picks 1--14)

## Vollständige Ziehung mit poolgebundener Equity

Die gesamte Reihenfolge 1--14 wird ausgelost.

Gewicht eines Picks p:

Weight(p) = Base(p) + Equity(f),

nur wenn:

-   Pool(f) = Lottery
-   p der base-stärkste Lottery-Pick dieser Franchise ist

Andernfalls:

Weight(p) = Base(p)

Tickets:

Tickets(p) = round(10 × Weight(p))

Ziehung erfolgt ohne Zurücklegen, mit Neu-Normalisierung nach jedem
Pick.

Playoff-Franchises dürfen keine Equity in der Lottery anwenden.
