---
layout: post
lang: de
title: "Procure-to-Pay in SAP: der Beschaffungsprozess vom Bedarf bis zur Zahlung"
description: "Procure-to-Pay (P2P) in SAP S/4HANA verständlich erklärt: vom Bedarf über Bestellanforderung, Bestellung und Wareneingang bis zur Rechnungsprüfung und Zahlung."
slug: beschaffungsprozess-procure-to-pay
permalink: /blog/de/beschaffungsprozess-procure-to-pay/
translation_key: post-procure-to-pay
date: 2026-07-07
category: "Einkauf"
keywords: "Procure-to-Pay, P2P, Beschaffungsprozess, SAP MM, Bestellanforderung, Bestellung, Wareneingang, Rechnungsprüfung, dreiseitiger Abgleich, Einkauf"
reading_time: 8
sources:
  - label: "SAP Help Portal — Sourcing and Procurement (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Materials Management / Sourcing and Procurement — allgemeine Grundlagen zum Beschaffungsprozess. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen Bestellanforderung und Bestellung?"
    a: "Die Bestellanforderung ist ein internes Dokument, mit dem eine Abteilung dem Einkauf einen Bedarf meldet. Die Bestellung ist der verbindliche Beleg, der nach außen an den Lieferanten geht. Erst die Bestellung ist rechtlich bindend."
  - q: "Was passiert beim Wareneingang in SAP?"
    a: "Beim Wareneingang zur Bestellung wird die Ware im System vereinnahmt: Der Bestand des Materials erhöht sich, und SAP erzeugt automatisch einen Materialbeleg für die Mengenbewegung und einen Buchhaltungsbeleg für die wertmäßige Buchung."
  - q: "Was ist der dreiseitige Abgleich?"
    a: "Der dreiseitige Abgleich vergleicht Bestellung, Wareneingang und Rechnung in Menge und Preis. Nur wenn die drei Belege zusammenpassen, läuft die Rechnung sauber durch. Bei Abweichungen außerhalb der Toleranz sperrt SAP die Rechnung zur Klärung."
  - q: "Warum bleibt eine Bestellung manchmal offen?"
    a: "Häufige Gründe sind eine noch ausstehende Freigabe, eine gesperrte Rechnung wegen Preis- oder Mengenabweichung oder eine Lieferung, die noch nicht als Wareneingang gebucht wurde. Die Bestellüberwachung zeigt, an welcher Stelle der Prozess hängt."
  - q: "Wo endet der Beschaffungsprozess?"
    a: "Aus Sicht des Einkaufs endet er mit der geprüften Rechnung. Die tatsächliche Zahlung an den Lieferanten findet in der Finanzbuchhaltung (FI) statt, meist über den automatischen Zahllauf. Damit ist der Procure-to-Pay-Kreis geschlossen."
---

Wenn ein Unternehmen etwas beschafft — Rohstoffe für die Produktion, Verbrauchsmaterial fürs Büro oder eine Dienstleistung — durchläuft dieser Vorgang in SAP fast immer denselben Ablauf: **Procure-to-Pay**, kurz **P2P**, oder auf Deutsch der Beschaffungsprozess. Dieser Artikel geht den Weg vom ersten Bedarf bis zur Zahlung Schritt für Schritt durch — mit den Begriffen, die dir im SAP-Einkauf immer wieder begegnen.

## Kurz gesagt: der komplette Weg vom Bedarf zur Zahlung

Procure-to-Pay beschreibt den **kompletten Beschaffungsprozess** in SAP — vom ersten Bedarf im Unternehmen bis zur finalen Zahlung an den Lieferanten. Im Modul **SAP MM (Materials Management)** ist das der Kernprozess: Alles, was du sonst im Einkauf machst, baut auf diesem Ablauf auf.

In der Praxis lässt sich der Beschaffungszyklus als Kette von acht Phasen beschreiben:

1. **Bedarfsermittlung** — manuell oder automatisch über die Bedarfsplanung
2. **Bezugsquellenfindung** — bei wem kaufen wir?
3. **Lieferantenauswahl** — Preise und Konditionen vergleichen
4. **Bestellbearbeitung** — die Bestellung anlegen
5. **Bestellüberwachung** — den Status verfolgen
6. **Wareneingang** — die Ware vereinnahmen
7. **Rechnungsprüfung** — die Lieferantenrechnung abgleichen
8. **Zahlungsabwicklung** — in der Buchhaltung

Klingt viel? Wenn du den Ablauf einmal als logische Geschichte verstanden hast, ergibt sich der Rest fast von selbst. Gehen wir die Phasen einzeln durch.

## Schritt 1: Bedarfsermittlung

Alles startet mit einem **Bedarf**. Irgendwo im Unternehmen wird etwas benötigt. Diesen Bedarf gibt es in zwei Varianten:

- **Manuelle Bedarfsermittlung:** Eine Fachabteilung sieht, dass etwas fehlt, und meldet den Bedarf an den Einkauf.
- **Automatische Bedarfsermittlung über die Bedarfsplanung (MRP):** SAP prüft regelmäßig die Bestände und meldet automatisch, wenn ein Mindestbestand unterschritten wird oder eine Produktion einen Bedarf auslöst.

Die Bedarfsplanung (Material Requirements Planning, kurz MRP) erzeugt bei erkanntem Bedarf automatisch eine Bestellanforderung. So muss niemand von Hand nachhalten, wann welcher Bestand zur Neige geht.

## Bestellanforderung (BANF) anlegen

Nach der Bedarfsermittlung entsteht eine **Bestellanforderung** (kurz **BANF**). Wichtig zu verstehen: Die BANF ist ein **rein internes Dokument**. Sie geht nicht an den Lieferanten, sondern ist eine Bitte der Fachabteilung an den Einkauf: „Bitte beschafft uns Folgendes."

Eine Bestellanforderung enthält typischerweise:

- was beschafft werden soll (Materialnummer oder Beschreibung)
- wie viel davon
- bis wann
- für welchen Zweck (Kostenstelle, Auftrag, Projekt)

Sie kann manuell erfasst werden oder automatisch durch die Bedarfsplanung entstehen. Mehr dazu im Detail: [Was ist eine Bestellanforderung (BANF) in SAP?](/blog/de/was-ist-eine-bestellanforderung/)

## Schritt 2: Bezugsquellenfindung — bei wem kaufen wir?

Sobald die Bestellanforderung da ist, stellt sich die nächste Frage: **Bei welchem Lieferanten kaufen wir?** Die Bezugsquellenfindung ist genau dieser Schritt. SAP bietet dafür mehrere Hilfen:

- **Infosatz:** enthält die Konditionen zwischen einem bestimmten Material und einem bestimmten Lieferanten (zum Beispiel Preis, Lieferzeit)
- **Orderbuch:** regelt, welche Lieferanten überhaupt zugelassen sind und welcher in welchem Zeitraum bevorzugt wird
- **Rahmenverträge (Outline Agreements):** langfristige Vereinbarungen mit einem Lieferanten

Bei den Rahmenverträgen unterscheidet SAP zwei Formen — den Kontrakt und den Lieferplan:

- **Kontrakt:** eine Rahmenvereinbarung über eine Gesamtmenge (**Mengenkontrakt**) oder einen Gesamtwert (**Wertkontrakt**); abgerufen wird flexibel über Kontraktabrufe
- **Lieferplan:** konkrete Liefertermine und -mengen werden über die Zeit verteilt eingeplant und abgerufen (typisch in der Serienfertigung)

## Schritt 3: Lieferantenauswahl und Konditionen vergleichen

Sind mögliche Bezugsquellen ermittelt, geht es um die **finale Lieferantenauswahl**. Hier vergleicht der Einkauf:

- Preise verschiedener Bezugsquellen oder Anfragen
- Lieferzeiten
- Liefer- und Zahlungsbedingungen
- Qualität und bisherige Performance des Lieferanten

Optional greift an dieser Stelle ein **Freigabeverfahren**: Gerade bei größeren Beträgen ist das Mehraugenprinzip Pflicht. Die Anforderung oder Bestellung muss erst freigegeben werden, bevor sie weiterläuft — ein bewusst eingebauter Kontrollschritt.

## Schritt 4: Bestellung erstellen

Jetzt kommt der zentrale Schritt: die **Bestellung** (englisch *Purchase Order*, kurz **PO**). Im Gegensatz zur Bestellanforderung ist die Bestellung ein **externer Beleg**. Sie geht nach außen an den Lieferanten und ist rechtlich verbindlich.

Die Bestellung enthält unter anderem:

- Lieferant
- Material und Menge
- Preis und Konditionen
- Lieferdatum
- Lieferadresse (zum Beispiel ein bestimmtes Werk oder Lager)
- Rechnungsempfänger

Eine Bestellung kann direkt aus einer Bestellanforderung erzeugt werden, aus einem Rahmenvertrag heraus oder komplett manuell entstehen. Die Daten aus der Anforderung — Material, Menge, Werk, Termin — werden dabei übernommen.

## Schritt 5: Bestellüberwachung

Nach dem Versand der Bestellung läuft die **Bestellüberwachung**. Der Einkauf verfolgt:

- ob für eine Bestellposition bereits eine Lieferung eingetroffen ist
- ob bereits eine Rechnung erfasst wurde
- ob ausstehende Lieferungen beim Lieferanten gemahnt werden müssen

Idealerweise schickt der Lieferant zwischendurch eine **Bestellbestätigung** zurück, sodass der Einkauf den vereinbarten Liefertermin im System hinterlegen kann. Bestellbestätigungen sind aber nicht zwingend.

## Schritt 6: Wareneingang

Sobald die Ware physisch im Lager ankommt, kommt der aus Anwendersicht spannendste Schritt: der **Wareneingang**. Die Ware wird in SAP **vereinnahmt** — das heißt, sie wird mengen- und wertmäßig ins System gebucht.

Was passiert beim Buchen?

- Der Bestand des Materials erhöht sich.
- Es wird automatisch ein **Materialbeleg** erzeugt — er dokumentiert die mengenmäßige Bewegung.
- Es wird gleichzeitig ein **Buchhaltungsbeleg** erzeugt — er dokumentiert die wertmäßige Buchung.

Diese Doppelbuchung — einmal Menge (Materialbeleg), einmal Wert (Buchhaltungsbeleg) — ist der Grund, warum ein Wareneingang in SAP in aller Regel nicht „nur" den Lagerbestand verändert, sondern zugleich die Finanzbuchhaltung berührt.

## Schritt 7: Rechnungsprüfung und der dreiseitige Abgleich

Irgendwann kommt die **Rechnung des Lieferanten**. Sie wird in SAP über die logistische Rechnungsprüfung erfasst. Das System macht dabei etwas sehr Wichtiges: den **dreiseitigen Abgleich** (englisch *three-way match*).

Dabei werden drei Belege miteinander verglichen:

| Beleg | Frage |
| --- | --- |
| **Bestellung** | Was war vereinbart? |
| **Wareneingang** | Was wurde tatsächlich geliefert? |
| **Rechnung** | Was berechnet uns der Lieferant? |

Nur wenn diese drei Dokumente in **Menge und Preis übereinstimmen**, läuft die Rechnung sauber durch. Überschreiten die Abweichungen die eingestellten Toleranzen, sperrt SAP die Rechnung automatisch zur Klärung.

Ein Beispiel: Bestellt waren 100 Stück zu 5 Euro, geliefert wurden ebenfalls 100 Stück. Berechnet der Lieferant jetzt aber 6 Euro pro Stück, erkennt SAP die Preisdifferenz und stellt die Rechnung zur Prüfung zurück. Genau dieser Mechanismus macht den dreiseitigen Abgleich zu einem der wichtigsten Kontrollpunkte im Beschaffungsprozess.

## Schritt 8: Zahlungsabwicklung in FI

Ist die Rechnung erfolgreich durch die Prüfung gelaufen, ist die Beschaffung aus MM-Sicht abgeschlossen. Der letzte Schritt findet im Modul **SAP FI (Finance)** statt: die tatsächliche **Zahlung an den Lieferanten**.

In FI wird die offene Verbindlichkeit reguliert — typischerweise über den automatischen Zahllauf oder eine manuelle Zahlung. Damit ist der Procure-to-Pay-Kreis geschlossen. Für das Verständnis reicht es zu wissen:

- Die Zahlung passiert in **FI**, nicht in MM.
- MM und FI sind über die **integrierte Buchung** verknüpft.
- Die Buchhaltungsbelege aus Wareneingang und Rechnungsprüfung sind die Brücke zwischen den beiden Modulen.

## Sonderfälle: nicht jede Beschaffung läuft geradeaus

Neben dem Standard-Beschaffungsprozess gibt es **Sonderbeschaffungsprozesse**, die vom geraden Ablauf abweichen:

- **Umlagerung mit Umlagerungsbestellung** — eine interne Bestellung zwischen zwei Werken desselben Unternehmens. Zwischen Versand und Empfang liegt die Ware im Transitbestand.
- **Lohnbearbeitung** — ein externer Lieferant fertigt mit vom Unternehmen beigestellten Komponenten.
- **Lieferantenkonsignation** — der Lieferant stellt Ware bereit, das Eigentum geht erst bei der Entnahme über.

Welcher Prozess für eine Bestellposition gilt, steuert SAP über den **Positionstyp**. Für den Alltag reicht es zu erkennen, dass es diese Varianten gibt — der Grundablauf Bedarf → Bestellung → Wareneingang → Rechnung bleibt derselbe.

## Häufige Stolpersteine

- **Bestellanforderung und Bestellung verwechseln.** Die Anforderung ist intern, die Bestellung geht nach außen. Wer beim Lieferanten nachfragt, warum „die Bestellung" nicht angekommen ist, sollte zuerst prüfen, ob überhaupt schon eine Bestellung existiert.
- **Fehlende Freigabe übersehen.** Eine nicht freigegebene Anforderung oder Bestellung wird nicht weiterverarbeitet. Ein Blick auf den Freigabestatus spart viel Sucherei.
- **Materialbeleg und Buchhaltungsbeleg vermischen.** Beim Wareneingang entstehen zwei Belege: einer für die Menge, einer für den Wert. Sie hängen zusammen, sind aber nicht dasselbe.
- **Gesperrte Rechnung nicht erkennen.** Weicht die Rechnung in Menge oder Preis über die Toleranz hinaus ab, sperrt SAP sie automatisch. Die Rechnung ist dann erfasst, aber noch nicht zahlungsreif — sie muss erst geklärt werden.

## Kurz zusammengefasst

Procure-to-Pay ist der rote Faden des SAP-Einkaufs: Jemand braucht etwas (Bedarf), meldet das intern (Bestellanforderung), der Einkauf sucht einen Lieferanten (Bezugsquellenfindung), holt bei Bedarf eine Freigabe, schickt eine Bestellung raus, bekommt die Ware (Wareneingang mit Material- und Buchhaltungsbeleg), bekommt die Rechnung, gleicht alles ab (dreiseitiger Abgleich) und bezahlt in FI. Wer diesen Ablauf als zusammenhängende Geschichte versteht, kann fast jede Detailfrage im Einkauf selbst herleiten — statt einzelne Begriffe isoliert auswendig zu lernen.

## Häufige Fragen

### Was ist der Unterschied zwischen Bestellanforderung und Bestellung?

Die Bestellanforderung ist ein internes Dokument, mit dem eine Abteilung dem Einkauf einen Bedarf meldet. Die Bestellung ist der verbindliche Beleg, der nach außen an den Lieferanten geht. Erst die Bestellung ist rechtlich bindend.

### Was passiert beim Wareneingang in SAP?

Beim Wareneingang zur Bestellung wird die Ware im System vereinnahmt: Der Bestand des Materials erhöht sich, und SAP erzeugt automatisch einen Materialbeleg für die Mengenbewegung und einen Buchhaltungsbeleg für die wertmäßige Buchung.

### Was ist der dreiseitige Abgleich?

Der dreiseitige Abgleich vergleicht Bestellung, Wareneingang und Rechnung in Menge und Preis. Nur wenn die drei Belege zusammenpassen, läuft die Rechnung sauber durch. Bei Abweichungen außerhalb der Toleranz sperrt SAP die Rechnung zur Klärung.

### Warum bleibt eine Bestellung manchmal offen?

Häufige Gründe sind eine noch ausstehende Freigabe, eine gesperrte Rechnung wegen Preis- oder Mengenabweichung oder eine Lieferung, die noch nicht als Wareneingang gebucht wurde. Die Bestellüberwachung zeigt, an welcher Stelle der Prozess hängt.

### Wo endet der Beschaffungsprozess?

Aus Sicht des Einkaufs endet er mit der geprüften Rechnung. Die tatsächliche Zahlung an den Lieferanten findet in der Finanzbuchhaltung (FI) statt, meist über den automatischen Zahllauf. Damit ist der Procure-to-Pay-Kreis geschlossen.
