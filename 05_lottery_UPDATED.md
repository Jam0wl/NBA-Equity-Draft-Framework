
# Lottery

## Vollständige Ziehungsmechanik der Picks 1--14

Die Lottery ist der Mechanismus, über den im Equity Draft Framework
(EDF) die Draft-Picks 1 bis 14 vergeben werden. Sie betrifft
ausschließlich die Teams des Lottery-Pools, also die 14 Mannschaften mit
den schlechtesten Saisonbilanzen.

EDF verändert die klassische NBA-Lottery in zwei zentralen Punkten:

1.  Die vollständige Reihenfolge 1--14 wird ausgelost.
2.  Die Ziehungsgewichte bestehen aus Base + voller Equity.

------------------------------------------------------------------------

# 1. Grundstruktur der Lottery

Nach Abschluss der regulären Saison werden die 14 schlechtesten Teams in
den Lottery-Pool eingeordnet.

Jeder im Lottery-Pool befindliche First-Round-Pick erhält ein
Ziehungsgewicht.

Die Ziehung erfolgt:

-   Gewichtet
-   Ohne Zurücklegen
-   Mit vollständiger Neu-Normalisierung nach jeder gezogenen Position

Damit entsteht eine vollständige zufällige Reihenfolge der Picks 1 bis
14.

------------------------------------------------------------------------

# 2. Zusammensetzung des Ziehungsgewichts

Das Ziehungsgewicht eines Picks besteht aus zwei Komponenten:

1.  Base (strukturelle Ausgleichskomponente)
2.  Equity (leistungsbasierte End-of-Season-Komponente)

Formal:

Weight = Base + Equity

## Poolbindung der Equity

Equity darf in der Lottery ausschließlich von Franchises angewendet
werden, die die Saison im Lottery-Pool beendet haben.

Das bedeutet:

-   Beendet eine Franchise die Saison im Lottery-Pool, kann sie ihre
    Equity auf genau einen Lottery-Pick anwenden (Best-Pick-Regel).

-   Beendet eine Franchise die Saison im Playoff-Pool, kann sie ihre
    Equity in der Lottery nicht einsetzen – selbst wenn sie durch Trades
    Lottery-Picks besitzt.

Damit wird verhindert, dass starke Teams ihre End-of-Season-Leistung zur
Verstärkung von Lottery-Picks nutzen können.

Zur praktischen Umsetzung in ganzzahligen Losen wird das Gewicht mit
einem konstanten Faktor skaliert:

Tickets = round(10 × Weight)

Die Multiplikation mit 10 dient ausschließlich der Ganzzahligkeit und
verändert die relativen Wahrscheinlichkeiten nicht.

------------------------------------------------------------------------

# 3. Ablauf der Ziehung

Die Ziehung erfolgt sequentiell von Pick 1 bis Pick 14.

Für Pick 1 gilt:

Die Wahrscheinlichkeit eines Picks p ergibt sich aus:

Tickets(p) geteilt durch die Summe aller Tickets im Lottery-Pool.

Nach Vergabe von Pick 1 wird der gezogene Pick aus dem Pool entfernt.

Für Pick 2 werden die verbleibenden Tickets neu aufsummiert.

Die Wahrscheinlichkeiten werden neu berechnet.

Dieser Prozess wird fortgeführt, bis alle 14 Positionen vergeben sind.

Dieses Verfahren wird als gewichtetes Sampling ohne Zurücklegen
bezeichnet.

------------------------------------------------------------------------

# 4. Unterschiede zum bisherigen NBA-System

Im bestehenden NBA-System werden nur die ersten vier Picks gelost.
Danach erfolgt eine Rücksortierung nach Bilanz.

EDF hingegen lost die gesamte Reihenfolge 1--14 vollständig aus.

Das bedeutet:

-   Es gibt keine garantierte Minimalposition.
-   Es gibt keine automatische Rücksortierung nach Saisonbilanz.
-   Jede Position ist Ergebnis eines Wahrscheinlichkeitsverfahrens.

Damit wird die strukturelle Sicherheit extremer Niederlagen reduziert.

------------------------------------------------------------------------

# 5. Wirkung der Equity in der Lottery

Equity wirkt im Lottery-Bereich ohne Dämpfung.

Sie steht jedoch ausschließlich Franchises des Lottery-Pools zur
Verfügung.

Ein Team kann seine Ziehungswahrscheinlichkeit nur durch Siege im
Endfenster erhöhen.

Zusätzliche Niederlagen außerhalb der Final 29 erzeugen keinen
proportionalen strategischen Vorteil.

Damit verschiebt sich die Rationalität vom gezielten Verlieren hin zur
aktiven Leistungsoptimierung im Saisonendspurt.

------------------------------------------------------------------------

# 6. Best-Pick-Regel innerhalb der Lottery

Besitzt eine Franchise mehrere First-Round-Picks im Lottery-Pool, wird
Equity nur auf den Pick mit der höchsten Base angewendet – sofern diese
Franchise dem Lottery-Pool angehört.

Das bedeutet:

-   Equity verstärkt genau einen Pick pro Franchise.
-   Equity kann nicht verteilt oder gestapelt werden.
-   Playoff-Franchises erhalten keinen Equity-Effekt in der Lottery.

Diese Regel verhindert, dass Teams mehrere Picks gleichzeitig künstlich
verstärken oder poolübergreifend Vorteile erzeugen.

------------------------------------------------------------------------

# 7. Transparenz und Nachvollziehbarkeit

Das Lottery-System im EDF ist vollständig transparent und mathematisch
nachvollziehbar.

Für jede Ziehungsrunde können öffentlich gemacht werden:

-   Base
-   Equity
-   Tickets
-   Gesamtticketzahl
-   Einzelwahrscheinlichkeiten

Damit wird die Draft-Lottery nicht nur fairer, sondern auch
verständlicher.

------------------------------------------------------------------------

# 8. Systemlogische Bedeutung

Die Lottery ist im EDF kein isolierter Zufallsmechanismus.

Sie ist das Zusammenspiel von strukturellem Ausgleich (Base) und
leistungsbasierter Belohnung (Equity).

Durch die vollständige Auslosung 1--14 wird die Sicherheit extremer
Niederlagen reduziert, während durch die starke Equity-Komponente
sportliche Leistung am Saisonende direkt belohnt wird.

Die Poolbindung stellt sicher, dass diese Belohnung nur dort wirkt, wo
sie strukturell vorgesehen ist.
