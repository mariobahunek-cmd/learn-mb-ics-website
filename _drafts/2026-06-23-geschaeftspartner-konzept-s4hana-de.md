---
layout: post
lang: de
title: "Der Geschäftspartner in SAP S/4HANA — ein Stammsatz für Kunden und Lieferanten"
description: "Der Geschäftspartner ist in SAP S/4HANA das zentrale Stammdatenobjekt für Kunden und Lieferanten: Typen, Rollen und warum er Debitor und Kreditor ablöst."
slug: geschaeftspartner-konzept-s4hana
permalink: /blog/de/geschaeftspartner-konzept-s4hana/
translation_key: post-geschaeftspartner
date: 2026-07-07
category: "Stammdaten"
keywords: "SAP Geschäftspartner, Business Partner, SAP S/4HANA, Debitor, Kreditor, Stammdaten, Rollenkonzept, Anwender"
reading_time: 7
sources:
  - label: "SAP Help Portal — Business Partner (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Stammdaten / Business Partner — allgemeine Grundlagen zum Geschäftspartner. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen Geschäftspartner und Debitor?"
    a: "Der Geschäftspartner ist das übergeordnete Stammdatenobjekt — der „Container“ für alle Daten zu einem Partner. Der Debitor (ein Kunde in der Finanzsicht) ist nur eine Rolle, die dieser Geschäftspartner einnehmen kann. Ein Geschäftspartner kann gleichzeitig Debitor und Kreditor sein."
  - q: "Wo wird der Geschäftspartner gepflegt?"
    a: "In der klassischen SAP GUI über die Transaktion BP, in SAP Fiori über die App zur Verwaltung von Geschäftspartnerstammdaten. Beide Wege schreiben in dieselben Tabellen — du wählst, was zu deinem Arbeitsumfeld passt."
  - q: "Warum wurde der Geschäftspartner in SAP S/4HANA eingeführt?"
    a: "Früher gab es getrennte Debitoren- und Kreditorenstammsätze, die bei Partnern mit Doppelrolle doppelt gepflegt werden mussten. Der Geschäftspartner fasst das zu einem einzigen Stammsatz zusammen und bildet die Funktionen über Rollen ab — das reduziert Redundanz und Pflegeaufwand."
  - q: "Kann ich den Geschäftspartner-Typ nachträglich ändern?"
    a: "Im Standard nicht einfach so. Der Typ — Person, Organisation oder Gruppe — wird beim Anlegen festgelegt und ist danach fest. Deshalb lohnt es sich, vorher zu klären, was tatsächlich vorliegt."
  - q: "Was ist der Unterschied zwischen allgemeinen und rollenspezifischen Daten?"
    a: "Allgemeine Daten wie Adresse, Bankverbindung und Kommunikation gelten rollenübergreifend und werden nur einmal gepflegt. Rollenspezifische Daten wie Zahlungsbedingungen oder Einkaufskonditionen gelten nur in der jeweiligen Rolle."
---

Sobald ein Unternehmen mit SAP S/4HANA arbeitet, taucht ein Begriff früher oder später überall auf: der **Geschäftspartner**, im Englischen *Business Partner*. Egal ob im Einkauf, im Vertrieb oder in der Buchhaltung — ohne Geschäftspartner läuft kein Kundenauftrag, keine Bestellung und keine Rechnung. Dieser Artikel erklärt in klarer Sprache, was dahintersteckt.

## Kurz gesagt: ein Stammsatz für alle externen Partner

Der Geschäftspartner ist in SAP S/4HANA das **zentrale Stammdatenobjekt für alle externen Partner eines Unternehmens** — vor allem Kunden und Lieferanten, aber auch andere Personen oder Organisationen, mit denen das Unternehmen in einer Geschäftsbeziehung steht.

Das Besondere: Ein Geschäftspartner wird **nur ein einziges Mal angelegt**. Über ein Rollenkonzept lässt er sich anschließend für ganz unterschiedliche Prozesse verwenden — als Kunde im Vertrieb, als Lieferant im Einkauf oder als Debitor beziehungsweise Kreditor in der Buchhaltung. Ein Stammsatz, viele Funktionen.

## Was war vorher? Debitor und Kreditor

Wer früher mit SAP R/3 oder SAP ERP (ECC) gearbeitet hat, kennt eine andere Welt — die der getrennten Stammsätze:

- Ein **Debitorenstammsatz** für Kunden.
- Ein **Kreditorenstammsatz** für Lieferanten.

Wenn ein Unternehmen denselben Partner gleichzeitig als Kunde und als Lieferant führte, brauchte es *zwei separate Stammsätze*. Adresse, Bankverbindung und Kommunikationsdaten standen mehrfach im System und mussten doppelt gepflegt werden — mit allen Risiken für Tippfehler und veraltete Daten.

Genau das löst der Geschäftspartner-Ansatz auf. Es gibt nur noch **einen Stammsatz pro Partner**, und die unterschiedlichen Funktionen werden über Rollen abgebildet. In SAP S/4HANA ist die Pflege über den Geschäftspartner der vorgesehene Weg — die alten, getrennten Pflegewege für Debitoren und Kreditoren sind nicht mehr der Standard.

## Die drei Geschäftspartner-Typen

Wenn du im System einen Geschäftspartner anlegst, ist die erste Entscheidung immer: **Welcher Typ liegt vor?** SAP unterscheidet drei feste Typen, und du entscheidest dich für genau einen.

### Person

Eine natürliche Person — ein Mensch mit Vor- und Nachnamen. Typische Beispiele: ein Privatkunde, ein Mitarbeiter oder ein einzelner Ansprechpartner. Hier pflegst du Felder wie Vorname, Nachname, Anrede und gegebenenfalls Geburtsdatum.

### Organisation

Eine juristische Person — ein Unternehmen, ein Verein oder eine andere Institution. Typische Beispiele: ein Industriekunde, ein Großhandelslieferant, eine Behörde. Hier pflegst du den Namen der Organisation und je nach Bedarf Rechtsform, Branche und steuerliche Daten.

### Gruppe

Ein Zusammenschluss von Personen oder Organisationen, der für das Unternehmen als ein gemeinsamer Partner auftritt. Typische Beispiele: eine Ehegemeinschaft oder eine Arbeitsgemeinschaft (ARGE).

Wichtig zu wissen: Der einmal gewählte Typ lässt sich später nicht mehr beliebig ändern. Deshalb ist die richtige Auswahl beim Anlegen ein zentraler Schritt.

## Das Rollenkonzept — das Herzstück

Wer das Rollenkonzept versteht, hat den Geschäftspartner verstanden. Eine **Rolle** beschreibt, in welcher Funktion ein Geschäftspartner für einen bestimmten Prozess auftritt. Und ein einziger Geschäftspartner kann **mehrere Rollen gleichzeitig** haben.

Typische Rollen sind zum Beispiel:

- **Geschäftspartner allgemein:** die Grundrolle mit den zentralen Stammdaten wie Name, Adresse, Kommunikation und Steuernummer. Diese Daten gelten für alle weiteren Rollen.
- **Debitor (FI):** der Partner agiert als Kunde in der Finanzbuchhaltung — mit buchungskreis-spezifischen Daten wie Abstimmkonto und Zahlungsbedingungen.
- **Kreditor (FI):** der Partner agiert als Lieferant in der Finanzbuchhaltung.
- **Kunde (Vertrieb):** der Partner agiert als Kunde im Vertrieb — mit vertriebsbereichs-spezifischen Daten wie Versandbedingungen.
- **Lieferant (Einkauf):** der Partner agiert als Lieferant im Einkauf — mit einkaufsorganisations-spezifischen Daten.
- **Ansprechpartner:** der Partner ist eine Kontaktperson.

Stell dir folgendes Beispiel vor: Dein Unternehmen kauft Büromaterial bei einer Firma ein — und dieselbe Firma mietet gleichzeitig Lagerräume bei dir. Der Partner ist also gleichzeitig *Lieferant* und *Kunde*.

Früher hättest du dafür zwei Stammsätze gebraucht. In SAP S/4HANA legst du **einen Geschäftspartner** an und gibst ihm die Rolle „Kunde“ und die Rolle „Lieferant“. Adresse, Bankverbindung und Kommunikation stehen nur einmal im System und werden für beide Rollen genutzt. Genau das ist der zentrale Vorteil.

## Allgemeine und rollenspezifische Daten

Beim Geschäftspartner unterscheidet SAP zwischen **allgemeinen Daten** (gelten rollenübergreifend) und **rollenspezifischen Daten** (gelten nur in einer bestimmten Funktion).

**Allgemeine Daten** sind unabhängig davon, in welcher Rolle der Partner gerade verwendet wird:

- **Adresse:** Straße, Postleitzahl, Ort, Land — auch mehrere Adressen sind möglich.
- **Bankverbindung:** IBAN, BIC, Bankname — wichtig für Zahlungen.
- **Steuerinformationen:** etwa die Umsatzsteuer-Identifikationsnummer.
- **Kommunikationsdaten:** Telefon, E-Mail und weitere Kontaktwege.

**Rollenspezifische Daten** kommen hinzu, sobald du dem Partner eine Rolle zuweist:

- **In der Rolle Kunde:** Versand- und Zahlungsbedingungen, Kreditlimit.
- **In der Rolle Lieferant:** Bestellwährung, Einkaufskonditionen.
- **In der FI-Rolle:** Abstimmkonto und buchungskreis-bezogene Daten.

Die Faustregel: Allgemeine Daten gelten *einmal für alle Rollen*, rollenspezifische Daten *nur in der jeweiligen Rolle*.

## Wie man einen Geschäftspartner anlegt

In SAP S/4HANA gibt es zwei zentrale Wege, beide schreiben in dieselben Tabellen:

- **Klassische SAP GUI:** die Transaktion `BP` — die zentrale Pflegemaske für alle Geschäftspartner-Rollen.
- **SAP Fiori:** eine App zur Verwaltung der Geschäftspartnerstammdaten für die moderne, browserbasierte Pflege. Wie du dich in dieser Oberfläche zurechtfindest, zeigt der Beitrag zu den [Grundlagen des SAP Fiori Launchpads](/blog/de/sap-fiori-launchpad-grundlagen/).

Ein typischer Ablauf sieht so aus:

1. **Pflege-Werkzeug öffnen** — Transaktion BP oder die passende Fiori-App.
2. **Typ wählen** — Person, Organisation oder Gruppe.
3. **Allgemeine Daten erfassen** — Name, Adresse, Kommunikation.
4. **Rolle hinzufügen** — je nachdem, in welcher Funktion der Partner auftreten soll.
5. **Rollenspezifische Daten pflegen** — etwa Buchungskreis, Abstimmkonto, Zahlungsbedingungen.
6. **Bei Bedarf weitere Rollen ergänzen.**
7. **Speichern** — das System vergibt eine Geschäftspartnernummer.

Der Charme: Adresse und Bankverbindung erfasst du **nur einmal**. Ergänzt du später eine zweite Rolle, sind diese Daten dort automatisch vorhanden — du pflegst nur noch die Felder, die zusätzlich gebraucht werden.

## Warum der Geschäftspartner so zentral ist

Der Geschäftspartner ist das Fundament, auf dem viele Geschäftsprozesse aufsetzen. Ohne ihn gibt es keinen Kundenauftrag, keine Bestellung und keine Eingangsrechnung. Wer im [Beschaffungsprozess (Procure-to-Pay)](/blog/de/beschaffungsprozess-procure-to-pay/) oder im Vertrieb arbeitet, begegnet ihm ständig — meist ohne groß darüber nachzudenken, denn er läuft im Hintergrund als verlässlicher Datenkern mit.

## Häufige Stolpersteine

- **Geschäftspartner mit Debitor gleichsetzen.** Der Geschäftspartner ist der Container, der Debitor nur eine seiner Rollen. Wer beides verwechselt, sucht Daten an der falschen Stelle.
- **Für jede Funktion einen neuen Stammsatz anlegen.** Das war früher so — heute ergänzt du einfach eine weitere Rolle. Doppelte Stammsätze sind ausdrücklich nicht mehr das Vorgehen.
- **Den Typ voreilig wählen.** Person, Organisation oder Gruppe steht nach dem Anlegen fest. Ein Moment Überlegung vorher erspart später Ärger.
- **Allgemeine und rollenspezifische Daten verwechseln.** Die Adresse ist allgemein, die Zahlungsbedingungen sind rollenspezifisch. Wer die Trennung kennt, findet Felder schneller.

## Kurz zusammengefasst

Der Geschäftspartner ist in SAP S/4HANA **der eine Stammsatz für alle externen Partner** — Kunden wie Lieferanten. Er ersetzt die früher getrennten Debitoren- und Kreditorenstammsätze, gibt es in den drei Typen Person, Organisation und Gruppe und wird über Rollen flexibel eingesetzt. Allgemeine Daten pflegst du nur einmal, rollenspezifische Daten pro Rolle. Wer dieses Prinzip — ein Partner, viele Rollen — verinnerlicht hat, versteht ein zentrales Fundament von SAP S/4HANA.

## Häufige Fragen

### Was ist der Unterschied zwischen Geschäftspartner und Debitor?

Der Geschäftspartner ist das übergeordnete Stammdatenobjekt — der „Container“ für alle Daten zu einem Partner. Der Debitor (ein Kunde in der Finanzsicht) ist nur eine Rolle, die dieser Geschäftspartner einnehmen kann. Ein Geschäftspartner kann gleichzeitig Debitor und Kreditor sein.

### Wo wird der Geschäftspartner gepflegt?

In der klassischen SAP GUI über die Transaktion BP, in SAP Fiori über die App zur Verwaltung von Geschäftspartnerstammdaten. Beide Wege schreiben in dieselben Tabellen — du wählst, was zu deinem Arbeitsumfeld passt.

### Warum wurde der Geschäftspartner in SAP S/4HANA eingeführt?

Früher gab es getrennte Debitoren- und Kreditorenstammsätze, die bei Partnern mit Doppelrolle doppelt gepflegt werden mussten. Der Geschäftspartner fasst das zu einem einzigen Stammsatz zusammen und bildet die Funktionen über Rollen ab — das reduziert Redundanz und Pflegeaufwand.

### Kann ich den Geschäftspartner-Typ nachträglich ändern?

Im Standard nicht einfach so. Der Typ — Person, Organisation oder Gruppe — wird beim Anlegen festgelegt und ist danach fest. Deshalb lohnt es sich, vorher zu klären, was tatsächlich vorliegt.

### Was ist der Unterschied zwischen allgemeinen und rollenspezifischen Daten?

Allgemeine Daten wie Adresse, Bankverbindung und Kommunikation gelten rollenübergreifend und werden nur einmal gepflegt. Rollenspezifische Daten wie Zahlungsbedingungen oder Einkaufskonditionen gelten nur in der jeweiligen Rolle.
