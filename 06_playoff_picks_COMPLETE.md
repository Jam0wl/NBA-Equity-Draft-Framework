# Playoff-Picks (15--30)

## Deterministische Vergabe mit gedämpfter Equity

Die Picks 15 bis 30 betreffen ausschließlich die 16 Teams des
Playoff-Pools.\
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

1.  Saison-Siege\
2.  Gedämpfte Equity

Die Teams werden nach diesem Score sortiert.

-   Höchster Score → Pick 15\
-   Niedrigster Score → Pick 30

------------------------------------------------------------------------

# 2. Definition des Playoff-Scores

Der Score für ein Playoff-Team t wird definiert als:

Score_PO(t) = W(t) + λ × Equity(t)

Dabei gilt:

W(t) = Anzahl der Saison-Siege\
Equity(t) = 2,1333 × W29(t)\
λ = 0,07

Damit lautet die vollständige Formel:

Score_PO(t) = W(t) + 0,07 × (2,1333 × W29(t))

------------------------------------------------------------------------

# 3. Kalibrierung der Dämpfung (λ)

Die Wahl von λ = 0,07 basiert auf folgender Zieldefinition:

Ein Unterschied von 10 Final-29-Siegen soll maximal 1,5 Draft-Plätze
verschieben.

Berechnung:

Equity-Differenz bei 10 Final-29-Siegen:

2,1333 × 10 = 21,333

Gedämpfter Effekt:

0,07 × 21,333 ≈ 1,49

Damit führt ein Unterschied von 10 Final-29-Siegen zu einer maximalen
Score-Differenz von etwa 1,5 Punkten.

Da im deterministischen System ein Score-Punkt näherungsweise einem
Draft-Platz entspricht, erfüllt diese Wahl die gewünschte Begrenzung.

------------------------------------------------------------------------

# 4. Maximaler Effekt

Der maximal mögliche Unterschied in den Final 29 beträgt 29 Siege.

Equity-Maximum:

2,1333 × 29 ≈ 61,87

Gedämpfter Effekt:

0,07 × 61,87 ≈ 4,33

Ein außergewöhnlicher Endspurt kann somit maximal etwa vier Draft-Plätze
verschieben.

Die Regular Season bleibt damit strukturell dominierend.

------------------------------------------------------------------------

# 5. Gleichstände

Bei identischem Score_PO wird ein minimaler deterministischer Tiebreaker
angewendet, beispielsweise:

-   Direkter Vergleich\
-   Net Rating\
-   Oder eine feste Team-ID mit minimalem ε-Zuschlag

Dieser Mechanismus dient ausschließlich der Eindeutigkeit und hat keinen
systemischen Einfluss.

------------------------------------------------------------------------

# 6. Warum kein Zufallsverfahren?

Im Playoff-Bereich besteht kein Tanking-Anreiz.

Teams konkurrieren um Playoff-Seeding und Titelchancen.

Ein Zufallsverfahren würde hier keinen strukturellen Vorteil erzeugen,
sondern lediglich Varianz hinzufügen.

EDF verwendet deshalb eine rein leistungsbasierte Sortierung.

------------------------------------------------------------------------

# 7. Systemwirkung

Die gedämpfte Equity bewirkt:

-   Der Endspurt bleibt relevant.
-   Extrem starke Final-29-Leistungen können leichte Verschiebungen
    erzeugen.
-   Die Gesamtbilanz bleibt der dominierende Faktor.
-   Keine radikale Umordnung der Playoff-Hierarchie.

Damit entsteht ein ausgewogenes Verhältnis zwischen Stabilität und
Leistungsanreiz.

------------------------------------------------------------------------

# 8. Zusammenfassung

Lottery (1--14): Zufällige Ziehung mit voller Equity-Wirkung.

Playoffs (15--30): Deterministische Sortierung mit gedämpfter
Equity-Wirkung.

Die Equity bleibt ligaweit eine einheitliche Währung. Lediglich ihre
strukturelle Wirkung wird im Playoff-Bereich kontrolliert begrenzt.
