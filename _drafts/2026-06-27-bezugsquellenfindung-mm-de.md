---
layout: post
lang: de
title: "Bezugsquellenfindung in SAP MM: Infosatz, Orderbuch, Kontrakt und Quotierung"
description: "Wie SAP im Einkauf die Bezugsquelle findet: Infosatz, Rahmenverträge, Orderbuch und Quotierung verständlich erklärt — vom Bedarf bis zur Quellenwahl."
slug: bezugsquellenfindung-mm
permalink: /blog/de/bezugsquellenfindung-mm/
translation_key: post-source-determination
date: 2026-07-08
category: "Einkauf"
keywords: "SAP Bezugsquellenfindung, SAP Einkaufsinfosatz, SAP Orderbuch, SAP Kontrakt, SAP Lieferplan, SAP Quotierung, SAP Rahmenvertrag, SAP Bestellanforderung"
reading_time: 10
sources:
  - label: "SAP Help Portal — Bezugsquellenfindung (Materials Management, SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Materials Management / Purchasing — allgemeine Grundlagen zur Bezugsquellenfindung. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist die Bezugsquellenfindung in SAP MM?"
    a: "Die Bezugsquellenfindung ist der Schritt, in dem SAP zu einem Materialbedarf automatisch die passende Bezugsquelle bestimmt — also den Lieferanten oder den Rahmenvertrag, aus dem das Material beschafft wird. Dafür wertet das System vier Werkzeuge aus: Einkaufsinfosatz, Rahmenvertrag, Orderbuch und Quotierung."
  - q: "Was ist der Unterschied zwischen Kontrakt und Lieferplan?"
    a: "Beide sind Rahmenverträge. Ein Kontrakt vereinbart eine Gesamtmenge oder einen Gesamtwert, ruft aber keine konkreten Termine ab — die Lieferungen erfolgen später als einzelne Kontraktabrufe. Ein Lieferplan legt zusätzlich direkt die konkreten Liefertermine und -mengen in Einteilungen fest und dient selbst als Versorgungsbeleg."
  - q: "Wozu dient das Orderbuch?"
    a: "Das Orderbuch legt pro Material und Werk fest, welche Bezugsquellen in welchem Zeitraum zulässig, bevorzugt oder gesperrt sind. Bei Orderbuchpflicht darf ein Material nur über die dort eingetragenen Quellen bezogen werden. Es steuert damit, wer überhaupt liefern darf."
  - q: "Was macht die Quotierung?"
    a: "Die Quotierung verteilt den Bedarf prozentual auf mehrere erlaubte Bezugsquellen, zum Beispiel 60 Prozent an einen und 40 Prozent an einen anderen Lieferanten. Sie ersetzt das Orderbuch nicht, sondern ergänzt es: Das Orderbuch sagt, wer liefern darf, die Quotierung teilt zwischen den Erlaubten auf."
  - q: "Wirkt die Quotierung automatisch?"
    a: "Nein. Sie greift nur, wenn zwei Dinge zusammenkommen: Im Materialstamm ist die Quotierungsverwendung gepflegt, und es existiert eine gültige Quotierungsregel. Fehlt eines von beiden, wird die Quotierung ignoriert."
---

Ein Material wird gebraucht, und jemand muss entscheiden, woher es kommt. In SAP trifft diese Entscheidung zu großen Teilen das System selbst, über die Bezugsquellenfindung. Die meisten, die ich in MM schule, verwechseln zuerst genau hier die Begriffe: Orderbuch, Kontrakt und Lieferplan werden schnell durcheinandergebracht, und die Rolle der Quotierung bleibt oft unklar. Dabei greifen die vier Werkzeuge nach einer nachvollziehbaren Logik ineinander.

## Woher SAP das Material bezieht

Die Bezugsquellenfindung ist der Schritt, in dem SAP zu einem Materialbedarf automatisch die passende Bezugsquelle bestimmt, also den Lieferanten oder den Rahmenvertrag, aus dem beschafft wird. Dafür wertet das System vier Werkzeuge aus: den **Einkaufsinfosatz**, den **Rahmenvertrag** (Kontrakt oder Lieferplan), das **Orderbuch** und die **Quotierung**. Zusammen beantworten sie zwei Fragen: *Wer darf liefern?* und *in welchem Verhältnis?*

## Wie beginnt der Prozess?

Am Anfang steht ein Bedarf. Sobald ein Material benötigt wird, entsteht eine **Bestellanforderung (BANF)**, eine interne Anforderung, die sagt: „Wir brauchen X Stück von Material Y bis Datum Z.“ Eine BANF entsteht auf zwei Wegen:

- **manuell** durch einen Anwender, etwa im Self-Service-Einkauf
- **automatisch** durch die Materialbedarfsplanung (MRP, englisch *Material Requirements Planning*), die den Bedarf aus Beständen, Aufträgen und Prognosen errechnet

Die Bezugsquellenfindung ist der Schritt danach. Sie klärt, aus welcher Quelle die Anforderung gedeckt wird. Vereinfacht ausgedrückt: Das Orderbuch sagt, wer überhaupt liefern darf, die Quotierung sagt, wie aufgeteilt wird, und Kontrakt sowie Infosatz liefern die Konditionen.

## Der Einkaufsinfosatz — die Verbindung Lieferant und Material

Der **Einkaufsinfosatz** ist der Steckbrief einer Beziehung zwischen einem Lieferanten und einem Material. Er hält fest, zu welchen Konditionen ein bestimmter Lieferant ein bestimmtes Material anbietet: Preis, Lieferzeit, Mindestbestellmenge und weitere Einkaufsdaten.

Der Nutzen: Legt ein Einkäufer eine Bestellung an, zieht SAP diese Daten automatisch aus dem Infosatz. Der Preis muss nicht jedes Mal neu eingetippt werden, und es bleibt nachvollziehbar, was in der Vergangenheit galt. Der Infosatz ist damit oft die Grundlage, auf der die anderen Werkzeuge aufsetzen.

## Was ist ein Rahmenvertrag?

Ein **Rahmenvertrag** ist eine längerfristige Vereinbarung mit einem Lieferanten über feste Konditionen, ohne dass jede einzelne Lieferung neu verhandelt wird. SAP kennt zwei Formen: den Kontrakt und den Lieferplan.

### Der Kontrakt

Ein **Kontrakt** vereinbart über einen längeren Zeitraum, typisch ein bis fünf Jahre, eine Gesamtabnahmemenge oder einen Gesamtwert mit einem Lieferanten, aber noch keine konkreten Liefertermine. Die einzelnen Lieferungen werden später als **Kontraktabrufe** angelegt, also Bestellungen mit Bezug zum Kontrakt.

Wie jeder Einkaufsbeleg besteht ein Kontrakt aus einem **Kopf** (Lieferant, Laufzeit, Vertragsart, Kopfkonditionen) und **Positionen** (Material, Gesamtmenge, Preis). Zwei Vertragsarten sind zu unterscheiden:

- **Mengenkontrakt**: Die Gesamtmenge ist fest vereinbart. Beispiel: 10.000 Stück eines Materials zu einem festen Stückpreis, gültig über zwei Jahre. Der Kontrakt gilt als erfüllt, wenn die 10.000 Stück abgerufen sind.
- **Wertkontrakt**: Der Gesamtwert ist fest. Beispiel: ein Gesamtvolumen von 120.000 Euro, frei verteilbar auf mehrere Materialien. Erfüllt ist er, wenn dieser Wert erreicht ist.

Welche Form passt, entscheidet die Geschäftslage: Eine feste Menge spricht für den Mengenkontrakt, ein flexibles Budget über mehrere Materialien für den Wertkontrakt.

Jeder Kontrakt führt automatisch Buch über seine Abrufe: Nummer, Bestelldatum, abgerufene Menge, Bestellwert. So ist jederzeit sichtbar, wie viel schon ausgeschöpft ist.

### Der Lieferplan

Ein **Lieferplan** ist enger getaktet als der Kontrakt. Hier vereinbarst du nicht nur die Gesamtmenge, sondern direkt die konkreten Liefertermine und -mengen in sogenannten **Einteilungen**. Das ist typisch für die Just-in-Time-Beschaffung, etwa in der Automobilindustrie oder der Serienproduktion. Ein Vorteil: Du brauchst keine separaten Bestellungen, denn der Lieferplan selbst ist der Versorgungsbeleg.

## Das Orderbuch — wer darf wann liefern?

Das **Orderbuch** ist das zentrale Steuerwerkzeug. Es legt pro Material und Werk fest, welche Bezugsquellen zu welchem Zeitpunkt zulässig, bevorzugt oder gesperrt sind. Bei jeder automatischen Quellenermittlung, im Einkauf wie in der Bedarfsplanung, schaut das System zuerst hier hinein.

### Die Felder im Orderbuch

Ein Eintrag umfasst unter anderem:

- **Gültigkeit** — der Zeitraum von-bis, in dem die Bezugsquelle zulässig ist
- **Bezugsquelle** — zum Beispiel ein bestimmter Kontrakt oder ein Infosatz eines Lieferanten
- **Fix** — das Kennzeichen für die bevorzugte Bezugsquelle in einem Zeitraum. Ein fixer Eintrag wird bei der automatischen Ermittlung zuerst gewählt.
- **Gesperrt** — die Bezugsquelle darf in diesem Zeitraum nicht verwendet werden
- **Disposition** — die Verwendung in der Bedarfsplanung. Nur so gekennzeichnete Einträge zieht die MRP heran.

### Orderbuchpflicht

Pro Material, oder pauschal pro Werk, lässt sich die **Orderbuchpflicht** setzen. Sie bedeutet: Das Material darf ausschließlich über die im Orderbuch eingetragenen Quellen bezogen werden. Wird eine Bestellung ohne gültigen Orderbucheintrag versucht, meldet das System, dass keine zulässige Bezugsquelle vorliegt. Das ist die häufigste Fehlermeldung überhaupt: Die Bestellung bleibt hängen, und dahinter steckt fast immer eine Orderbuchpflicht ohne passenden Eintrag.

### Wie das Orderbuch gepflegt wird

Gefüllt wird das Orderbuch auf drei Wegen. Der einfachste ist die manuelle Pflege, Eintrag für Eintrag pro Material und Werk. Häufiger übernimmt SAP die Quelle direkt aus einem Rahmenvertrag oder Infosatz, sobald dieser angelegt oder geändert wird. Und für Bestandsmaterial lässt sich das Orderbuch automatisch generieren: Das System trägt alle vorhandenen Bezugsquellen eines Materials in einem Schritt ein, samt Vorschaufunktion zum Simulieren.

## Die Quotierung — wenn mehrere Lieferanten liefern sollen

In der Praxis will man ein Material oft **nicht** nur von einem einzigen Lieferanten beziehen, selbst wenn dieser den besten Preis hat. Typische Gründe:

- **Versorgungssicherheit** — fällt ein Lieferant aus, übernimmt der andere
- **Verhandlungsmacht** — zwei parallele Quellen halten den Preisdruck aufrecht
- **Kapazitätsgrenzen** — ein Lieferant allein deckt nicht den ganzen Bedarf
- **Risikostreuung** — mehrere Länder oder Standorte senken das Klumpenrisiko

Die **Quotierung** (englisch *quota arrangement*) ist das Werkzeug dafür. Sie verteilt den Bedarf prozentual auf mehrere Bezugsquellen.

### Ein einfaches Beispiel

Ein Material soll zu 60 Prozent von Lieferant A und zu 40 Prozent von Lieferant B bezogen werden. Dafür trägt eine Quotierungsregel zwei Einträge mit dem Quotenverhältnis 3 zu 2 (das entspricht 60 zu 40). Bei jeder neuen Anforderung wählt das System automatisch die Quelle, die gemäß der vereinbarten Aufteilung als Nächstes an der Reihe ist.

### Wie SAP entscheidet: der Quotierungsfaktor

Damit die Verteilung aufgeht, berechnet das System pro Bezugsquelle einen **Quotierungsfaktor**:

> Quotierungsfaktor = (bisher bezogene Menge + Quotierungsbasismenge) ÷ Quote

Bei jeder neuen Bestellung gewinnt die Quelle mit dem niedrigsten Faktor. So pendelt sich die tatsächliche Verteilung über die Zeit auf die vereinbarte Quote ein. Über die **Quotierungsbasismenge** lässt sich ein Startwert vorgeben, etwa um einem Lieferanten bewusst einen Vorsprung zu geben und das Verhältnis zu verschieben.

### Die Quotierungsverwendung im Materialstamm

Damit die Quotierung überhaupt greift, muss im Materialstamm (Sicht *Einkauf*) die **Quotierungsverwendung** gepflegt sein. Sie steuert, in welchen Vorgängen die Quotierung wirkt: in der Bestellanforderung, in der Bestellung, in der Bedarfsplanung, bei der Anlieferung eines Lieferplans oder im Produktionsauftrag. Die Werte sind kombinierbar, sodass eine Quotierung etwa gleichzeitig in der Bedarfsplanung und in der manuellen Anforderung greifen kann.

Es gibt außerdem eine **Mindestlosgröße** pro Quotierungseintrag: Liegt der einzelne Bedarf darunter, geht alles an die nächste Quote. Das vermeidet Kleinstbestellungen, die sich nicht lohnen.

### Zwei häufige Missverständnisse

- **„Die Quotierung wirkt automatisch.“** Nur, wenn im Materialstamm die Quotierungsverwendung gepflegt ist *und* eine gültige Quotierungsregel existiert. Ohne beides bleibt sie wirkungslos.
- **Quotierung ersetzt das Orderbuch.** Tut sie nicht. Das Orderbuch sagt, wer überhaupt liefern darf, die Quotierung verteilt nur zwischen den bereits Erlaubten.

## Bestellanforderung und Bezugsquellenfindung im Zusammenspiel

Die Bezugsquellenfindung läuft typischerweise beim Anlegen einer Bestellanforderung. Für Einkäufer gibt es dafür eine erweiterte Erfassung, in der alle Daten auf einem zentralen Bildschirm liegen: Kopfdaten für den gesamten Beleg, eine Positionsübersicht mit Material, Menge, Lieferdatum und Werk sowie ein Positionsdetail für Zusatzangaben. Ein Häkchen aktiviert die automatische Quellenermittlung direkt beim Anlegen der Position.

### Einfach- oder Mehrfachkontierung

Wird ein Material direkt für ein Kontierungsobjekt angefordert, etwa eine Kostenstelle, kommt ein **Kontierungstyp** ins Spiel:

- **Einfachkontierung** — die Kosten gehen vollständig auf ein Objekt, etwa eine einzige Kostenstelle.
- **Mehrfachkontierung** — die Kosten verteilen sich auf mehrere Objekte, entweder mengenmäßig, wertmäßig oder prozentual.

Ein Beispiel: 90 Bürostühle, verteilt auf drei Kostenstellen zu je einem Drittel, ergeben 30 Stühle pro Stelle. Erhöht sich die Gesamtmenge auf 120, passt das System die prozentuale Verteilung automatisch an, also 40 Stühle je Stelle. Diese automatische Anpassung greift aber nur, wenn im Kontierungstyp die prozentuale Aufteilung aktiv gewählt ist; sonst müssen die Mengen manuell gepflegt werden.

### Bearbeitungsstatus und Belegfluss

Der **Bearbeitungsstatus** einer Anforderungsposition zeigt jederzeit, wie weit der Beschaffungsprozess ist, etwa *nicht bestellt*, *bestellt*, *angefragt* oder *in einen Rahmenvertrag umgesetzt*. Über den Belegfluss lassen sich die Folgebelege (Bestellung, Wareneingang, Rechnung) direkt aus der Anforderung heraus verfolgen.

## Was Anwender im Alltag davon merken

Die Bezugsquellenfindung wird nicht täglich konfiguriert. Die zugrunde liegenden Stammdaten, also Infosätze, Kontrakte, Orderbuch und Quotierung, pflegt man meist einmalig oder bei Vertragsänderungen. Im täglichen Ablauf bewegen sich Einkäufer und Disponenten aber ständig in dieser Logik:

- Ein Bedarf entsteht, durch Self-Service oder Bedarfsplanung.
- Die Bezugsquellenfindung läuft, automatisch oder beim Anlegen aktiviert.
- Das System wählt die Quelle: Orderbuch zulässig? Quotierung aktiv? Kontrakt vorhanden? Infosatz als Rückfallebene?
- Die Anforderung wird zur Bestellung, manuell oder automatisch umgesetzt.
- Wareneingang und Rechnung werden über den Status verfolgt.

Im MRP-Lauf geschieht dasselbe automatisch für alle dispositiv geführten Materialien: Das System prüft Orderbuch und Quotierung, wählt die fixe oder dispositionsrelevante Quelle und legt eine Anforderung an, zugeordnet zum passenden Kontrakt oder Infosatz.

## Das Wichtigste

Die Bezugsquellenfindung beantwortet die Frage, woher ein Material kommt, und sie tut es weitgehend automatisch. Vier Werkzeuge greifen dabei ineinander: Der **Einkaufsinfosatz** liefert die Konditionen einer Lieferanten-Material-Beziehung, der **Rahmenvertrag** (Kontrakt oder Lieferplan) bindet längerfristige Vereinbarungen ein, das **Orderbuch** entscheidet, wer überhaupt liefern darf, und die **Quotierung** teilt den Bedarf zwischen mehreren Quellen auf. Wer diese vier Rollen auseinanderhält, versteht schnell, warum SAP im konkreten Fall genau diese eine Quelle vorschlägt.

## Häufige Fragen

### Was ist die Bezugsquellenfindung in SAP MM?

Die Bezugsquellenfindung ist der Schritt, in dem SAP zu einem Materialbedarf automatisch die passende Bezugsquelle bestimmt — also den Lieferanten oder den Rahmenvertrag, aus dem das Material beschafft wird. Dafür wertet das System vier Werkzeuge aus: Einkaufsinfosatz, Rahmenvertrag, Orderbuch und Quotierung.

### Was ist der Unterschied zwischen Kontrakt und Lieferplan?

Beide sind Rahmenverträge. Ein Kontrakt vereinbart eine Gesamtmenge oder einen Gesamtwert, ruft aber keine konkreten Termine ab — die Lieferungen erfolgen später als einzelne Kontraktabrufe. Ein Lieferplan legt zusätzlich direkt die konkreten Liefertermine und -mengen in Einteilungen fest und dient selbst als Versorgungsbeleg.

### Wozu dient das Orderbuch?

Das Orderbuch legt pro Material und Werk fest, welche Bezugsquellen in welchem Zeitraum zulässig, bevorzugt oder gesperrt sind. Bei Orderbuchpflicht darf ein Material nur über die dort eingetragenen Quellen bezogen werden. Es steuert damit, wer überhaupt liefern darf.

### Was macht die Quotierung?

Die Quotierung verteilt den Bedarf prozentual auf mehrere erlaubte Bezugsquellen, zum Beispiel 60 Prozent an einen und 40 Prozent an einen anderen Lieferanten. Sie ersetzt das Orderbuch nicht, sondern ergänzt es: Das Orderbuch sagt, wer liefern darf, die Quotierung teilt zwischen den Erlaubten auf.

### Wirkt die Quotierung automatisch?

Nein. Sie greift nur, wenn zwei Dinge zusammenkommen: Im Materialstamm ist die Quotierungsverwendung gepflegt, und es existiert eine gültige Quotierungsregel. Fehlt eines von beiden, wird die Quotierung ignoriert.
