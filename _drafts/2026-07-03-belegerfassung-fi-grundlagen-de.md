---
layout: post
lang: de
title: "Belegerfassung in SAP FI: So funktioniert das Buchen von Belegen"
description: "Jede Buchung in SAP FI ist am Ende ein Beleg. Was Belegkopf, Belegposition und Belegart bedeuten und was der Unterschied zwischen Buchen, Vorerfassen und Merken ist — klar erklärt."
slug: belegerfassung-fi-grundlagen
permalink: /blog/de/belegerfassung-fi-grundlagen/
translation_key: post-fi-belegerfassung
date: 2026-07-07
category: "Finanzen"
keywords: "SAP FI, Belegerfassung, Beleg buchen, Belegart, Belegkopf, Belegposition, Vorerfassen, Finanzbuchhaltung"
reading_time: 7
sources:
  - label: "SAP Help Portal — Finance (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Finance / Financial Accounting — allgemeine Grundlagen zur Belegerfassung. Vor produktiver Nutzung immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen Belegkopf und Belegposition?"
    a: "Der Belegkopf enthält die allgemeinen Daten, die für den ganzen Beleg gelten — etwa Buchungsdatum, Belegart, Buchungskreis und Währung. Die Belegpositionen sind die einzelnen Buchungszeilen mit Konto und Soll- oder Habenbetrag."
  - q: "Was bedeutet es, einen Beleg zu buchen statt vorzuerfassen?"
    a: "Ein gebuchter Beleg ist endgültig gespeichert, bekommt eine feste Belegnummer und fließt in Bilanz und GuV ein. Ein vorerfasster Beleg ist gespeichert, aber noch nicht bilanzwirksam — er wartet meist auf eine Freigabe."
  - q: "Warum lässt SAP eine Buchung manchmal nicht zu?"
    a: "Häufig liegt es an einer Toleranzgruppe, die pro Mitarbeiter Höchstbeträge festlegt. Übersteigt eine Buchung die Grenze, weist das System sie ab. Das ist eine bewusst eingebaute Kontrolle, kein Fehler."
  - q: "Wozu dient die Belegart?"
    a: "Die Belegart steuert unter anderem, aus welchem Nummernkreis die Belegnummer stammt und welche Kontotypen im Beleg erlaubt sind. Sie ordnet den Geschäftsvorfall ein — etwa als Sachkontenbuchung, Kreditoren- oder Debitorenrechnung."
---

Egal ob Bankbuchung, Eingangsrechnung oder Gutschrift — in der SAP-Finanzbuchhaltung (FI) landet jeder Geschäftsvorfall am Ende in derselben Form: als **Beleg**. Wer versteht, wie ein Beleg aufgebaut ist und wie man ihn erfasst, versteht den Kern der Arbeit in SAP FI. Dieser Artikel erklärt in klarer Sprache, was dahintersteckt.

## Kurz gesagt: der Beleg ist die zentrale Einheit jeder Buchung

Ein **FI-Beleg** ist die Einheit, in der SAP jeden einzelnen Geschäftsvorfall in der Finanzbuchhaltung speichert. Er besteht immer aus zwei Teilen:

- Dem **Belegkopf** — mit allgemeinen Daten wie Buchungsdatum, Belegart, Buchungskreis und Währung.
- Den **Belegpositionen** — den eigentlichen Buchungszeilen mit Konto, Soll- oder Habenbetrag und weiteren Zuordnungen wie Kostenstelle oder Profitcenter.

Eine Regel gilt dabei immer: Jeder Beleg muss ausgeglichen sein, **Soll-Summe = Haben-Summe**. Das ist das Grundprinzip der doppelten Buchführung, und SAP erzwingt es technisch beim Buchen. Ein Beleg, der nicht ausgeglichen ist, lässt sich gar nicht erst buchen.

## Welche Buchungen erfasst man in SAP FI?

In der Finanzbuchhaltung von SAP S/4HANA erfasst man typischerweise diese Arten von Buchungen:

- **Sachkontenbuchungen** — zum Beispiel ein Geldtransfer von der Bank in die Kasse.
- **Debitorenrechnungen** — Ausgangsrechnungen an Kunden.
- **Debitorengutschriften** — Gutschriften an Kunden.
- **Kreditorenrechnungen** — Eingangsrechnungen von Lieferanten.
- **Kreditorengutschriften** — Gutschriften von Lieferanten.

Ein einfaches Beispiel macht das Prinzip greifbar: Werden 5.000 € vom Bankkonto abgehoben und in die Kasse gelegt, entsteht eine Sachkontenbuchung mit zwei Zeilen — Kasse 5.000 € im Soll, Bank 5.000 € im Haben. Soll und Haben sind gleich, der Beleg ist ausgeglichen.

## Wozu dient die Belegart?

Die **Belegart** ist ein zentrales Steuerelement in jedem Beleg. Sie legt fest:

- Aus welchem **Nummernkreis** die Belegnummer gezogen wird.
- Welche **Kontotypen** (Sachkonto, Debitor, Kreditor, Anlage, Material) im Beleg zugelassen sind.
- Ob eine **Belegaufteilung** stattfindet.
- Welche **Felder** in der Erfassung sichtbar oder Pflicht sind.

In der Praxis muss man die Belegart selten von Hand suchen: SAP schlägt je nach Vorgang eine passende Standard-Belegart vor, die man bei Bedarf überschreiben kann. Bei einer Kreditorenrechnung ist das zum Beispiel eine Rechnungs-Belegart, bei einer reinen Hauptbuchbuchung eine Sachkonten-Belegart. Die Belegart ordnet den Vorfall also von Anfang an richtig ein.

## Buchen, Vorerfassen, Merken — drei Wege, einen Beleg zu speichern

Das ist eines der wichtigsten Konzepte im Alltag. Beim Erfassen eines Belegs hast du drei Möglichkeiten, was mit ihm geschehen soll:

- **Buchen** — der Beleg wird endgültig gespeichert, bekommt eine feste Belegnummer und fließt in alle Auswertungen ein (Bilanz, GuV, Saldenliste). Rückgängig geht das nur noch über eine Stornobuchung.
- **Vorerfassen** — der Beleg ist gespeichert und hat eine vorläufige Nummer, fließt aber *noch nicht* in Bilanz und GuV ein. Typischer Einsatz: Ein Sachbearbeiter erfasst, die endgültige Buchung gibt eine zweite Person frei (Vier-Augen-Prinzip).
- **Merken** — der Beleg wird als *gemerkter Beleg* zwischengespeichert, oft noch unvollständig. Das nutzt man, wenn noch Daten fehlen und man später weiterarbeiten will.

Der praktische Kern dahinter: Nur der **gebuchte** Beleg ist bilanzwirksam. Vorerfasste und gemerkte Belege sind zwar gespeichert, tauchen aber nicht in Bilanz oder GuV auf. Erst nach dem Klick auf „Buchen" ist ein Beleg endgültig — bis dahin kannst du alles ändern oder verwerfen.

## Was steht im Belegkopf?

Beim Erfassen eines Belegs füllst du im Belegkopf typischerweise diese Felder:

- **Belegdatum** — bei Eingangsrechnungen das Rechnungsdatum.
- **Buchungsdatum** — das Datum, das die Buchungsperiode bestimmt.
- **Belegart** — ordnet den Vorgang ein (siehe oben).
- **Buchungskreis** — die buchende Organisationseinheit.
- **Währung** — zum Beispiel EUR.
- **Text** — ein frei wählbarer Erläuterungstext.

Bei Kreditoren- oder Debitorenrechnungen kommen Felder wie **Lieferant** beziehungsweise **Kunde**, **Referenz**, **Betrag** und **Steuerkennzeichen** hinzu. Die Positionen darunter enthalten dann die einzelnen Konten mit ihren Soll- und Habenbeträgen.

## Wie ein Beleg entsteht — vom Eintippen bis zur Belegnummer

Ein typischer Ablauf sieht so aus:

1. **Vorgang auswählen** — je nachdem, ob eine Hauptbuchbuchung, eine Eingangs- oder eine Ausgangsrechnung erfasst wird.
2. **Belegkopf füllen** — Belegdatum, Buchungsdatum, Belegart, Buchungskreis, Währung.
3. **Positionen erfassen** — Konto, Soll- oder Habenbetrag und weitere Zuordnungen wie Kostenstelle oder Profitcenter.
4. **Simulieren** — SAP zeigt dir die fertige Buchung mit allen automatisch erzeugten Zeilen (etwa Steuer oder Belegaufteilung), *bevor* du buchst. So siehst du das Ergebnis vorab.
5. **Buchen** — der Beleg wird endgültig gespeichert, das System vergibt eine Belegnummer.
6. **Bestätigung** — SAP meldet, dass der Beleg gesichert wurde, und zeigt die Belegnummer an.

Der Simulieren-Schritt ist im Alltag Gold wert: Er zeigt automatisch erzeugte Positionen wie die Steuerzeile, bevor etwas endgültig ist. So lassen sich Fehler früh erkennen, statt sie später stornieren zu müssen.

## Toleranzgruppen: warum eine Buchung abgelehnt wird

SAP schützt vor versehentlichen oder zu großen Buchungen über sogenannte **Toleranzgruppen**. Pro Mitarbeiter lassen sich damit Grenzen festlegen, zum Beispiel:

- ein **Höchstbetrag pro Beleg**,
- ein **Höchstbetrag pro Position** in Verbindung mit einem Debitoren- oder Kreditorenkonto,
- ein maximaler **Skontoprozentsatz**, den der Mitarbeiter zuweisen darf,
- eine maximale **Toleranz für Zahlungsdifferenzen** (Über- oder Unterzahlung).

Ein Beispiel: Liegt die Grenze pro Beleg bei 500.000 € und versuchst du eine Buchung über 600.000 €, weist SAP sie ab. Das wirkt zunächst wie eine Blockade, ist aber eine eingebaute Sicherheitsschicht — kein Bug, sondern eine bewusste Kontrolle. Ein Kollege mit höherer Berechtigung darf denselben Beleg unter Umständen buchen.

## Wer im Alltag mit der Belegerfassung arbeitet

- **Sachbearbeiter in der Buchhaltung** erfassen laufende Belege — Rechnungen, Bankbuchungen, Umbuchungen.
- **Buchhaltungsleiter oder Prüfende** geben vorerfasste Belege frei und arbeiten mit höheren Toleranzgrenzen.
- **Fachabteilungen** liefern die Grundlagen, etwa Eingangsrechnungen, die dann erfasst werden.

Für dich als Anwender ist die Belegerfassung der Punkt, an dem Geschäftsvorfälle in Zahlen übersetzt werden. Wer den Aufbau eines Belegs und den Unterschied zwischen Buchen, Vorerfassen und Merken verinnerlicht hat, findet sich in SAP FI schnell zurecht.

## Häufige Stolpersteine

- **Vorerfasst mit gebucht verwechseln.** Ein vorerfasster Beleg sieht aus wie gebucht, ist aber nicht bilanzwirksam. Wer einen Betrag in der Bilanz vermisst, sollte prüfen, ob der Beleg wirklich gebucht oder nur vorerfasst wurde.
- **Buchungsdatum und Belegdatum vertauschen.** Das Buchungsdatum bestimmt die Periode. Wird es falsch gesetzt, landet die Buchung im falschen Monat.
- **Toleranzgrenze übersehen.** Wird eine Buchung ohne klaren Grund abgelehnt, lohnt ein Blick auf die eigene Toleranzgruppe, bevor man einen Systemfehler vermutet.
- **Nicht simulieren.** Wer vor dem Buchen nicht simuliert, sieht automatisch erzeugte Positionen wie die Steuerzeile erst hinterher — und muss im Zweifel stornieren.

## Kurz zusammengefasst

Der Beleg ist die zentrale Einheit jeder Buchung in SAP FI: ein **Belegkopf** mit den allgemeinen Daten und **Belegpositionen** mit den einzelnen Buchungszeilen, die in Soll und Haben immer ausgeglichen sein müssen. Die Belegart ordnet den Vorgang ein, und beim Speichern entscheidest du zwischen Buchen, Vorerfassen und Merken — nur das Buchen macht den Beleg endgültig und bilanzwirksam. Wer diesen Aufbau und diese drei Optionen verstanden hat, beherrscht die Grundlagen der Belegerfassung.

## Häufige Fragen

### Was ist der Unterschied zwischen Belegkopf und Belegposition?

Der Belegkopf enthält die allgemeinen Daten, die für den ganzen Beleg gelten — etwa Buchungsdatum, Belegart, Buchungskreis und Währung. Die Belegpositionen sind die einzelnen Buchungszeilen mit Konto und Soll- oder Habenbetrag.

### Was bedeutet es, einen Beleg zu buchen statt vorzuerfassen?

Ein gebuchter Beleg ist endgültig gespeichert, bekommt eine feste Belegnummer und fließt in Bilanz und GuV ein. Ein vorerfasster Beleg ist gespeichert, aber noch nicht bilanzwirksam — er wartet meist auf eine Freigabe.

### Warum lässt SAP eine Buchung manchmal nicht zu?

Häufig liegt es an einer Toleranzgruppe, die pro Mitarbeiter Höchstbeträge festlegt. Übersteigt eine Buchung die Grenze, weist das System sie ab. Das ist eine bewusst eingebaute Kontrolle, kein Fehler.

### Wozu dient die Belegart?

Die Belegart steuert unter anderem, aus welchem Nummernkreis die Belegnummer stammt und welche Kontotypen im Beleg erlaubt sind. Sie ordnet den Geschäftsvorfall ein — etwa als Sachkontenbuchung, Kreditoren- oder Debitorenrechnung.
