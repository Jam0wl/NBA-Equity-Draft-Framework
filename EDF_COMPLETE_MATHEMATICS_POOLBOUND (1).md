# EDF -- Vollständige Mathematik (Poolgebunden)

## 1. Basisdefinitionen

Base(t) = 100 − W(t) Equity(t) = 2,1333 × W29(t)

Pool(f) ∈ {Lottery, Playoff}

## 2. Lottery (1--14)

Für Pick p mit Owner f gilt:

Weight(p) = Base(p) + Equity(f), falls Pool(f) = Lottery und p =
base-stärkster Lottery-Pick von f

sonst:

Weight(p) = Base(p)

Tickets(p) = round(10 × Weight(p))

Ziehung ohne Zurücklegen.

## 3. Playoff (15--30)

Score_PO(t) = W(t) + 0,07 × Equity(t), falls Pool(t) = Playoff

sonst:

Score_PO(t) = W(t)

Sortierung absteigend → Pick 15 bis 30.

## 4. Second Round

Unverändert gegenüber bestehendem System.
