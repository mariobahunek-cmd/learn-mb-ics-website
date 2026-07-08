---
layout: post
lang: de
title: "Order-to-Cash in SAP: Der Vertriebsprozess Schritt für Schritt"
description: "Order-to-Cash erklärt: vom Kundenauftrag über Lieferung und Warenausgang bis zum Zahlungseingang. So läuft der Vertriebsprozess in SAP S/4HANA — verständlich für Anwender."
slug: order-to-cash-prozess-vertrieb
permalink: /blog/de/order-to-cash-prozess-vertrieb/
translation_key: post-order-to-cash
date: 2026-07-07
category: "Vertrieb"
keywords: "Order-to-Cash, SAP Vertrieb, Auftragsabwicklung, Kundenauftrag, Lieferung, Warenausgang, Faktura, Belegfluss, S/4HANA Sales"
reading_time: 8
sources:
  - label: "SAP Help Portal — Sales (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Sales / Vertrieb — allgemeine Grundlagen zum Order-to-Cash-Prozess. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was bedeutet Order-to-Cash?"
    a: "Order-to-Cash beschreibt den kompletten Vertriebsprozess in SAP — von der Bestellung des Kunden bis zum Zahlungseingang. Sinngemäß heißt der Begriff „vom Auftrag bis zum Geldeingang“."
  - q: "Was ist der Unterschied zwischen Auslieferung und Kundenauftrag?"
    a: "Der Kundenauftrag ist der kaufmännische Vertriebsbeleg mit Kunde, Material, Preis und Termin. Die Auslieferung ist ein eigenständiger Logistikbeleg mit Versandstelle, Lagerort und Warenausgangsdatum — keine bloße Kopie des Auftrags."
  - q: "Warum wird der Warenausgang vor der Rechnung gebucht?"
    a: "Die Rechnung soll nur das fakturieren, was tatsächlich versendet wurde. Deshalb bucht SAP zuerst den Warenausgang (Ware verlässt das Lager) und erstellt erst danach die Faktura. So bleiben Bestand und Buchhaltung konsistent."
  - q: "Was ist der Belegfluss im Vertrieb?"
    a: "Der Belegfluss zeigt, wie die Belege eines Vorgangs zusammenhängen: Kundenauftrag, Auslieferung, Warenausgang, Faktura und Zahlung verweisen aufeinander. Per Klick lässt sich jeder Vorgang bis zum Ursprungsauftrag zurückverfolgen."
---

Wenn ein Kunde etwas bestellt und am Ende das Geld auf dem Konto eingeht, liegt dazwischen ein durchgängiger Ablauf, der in SAP einen festen Namen hat: **Order-to-Cash**, oft auch Auftragsabwicklung oder schlicht Vertriebsprozess genannt. Er ist der Kernprozess im SAP-Vertrieb (Sales). Dieser Artikel geht den kompletten Weg Schritt für Schritt durch — verständlich und aus Anwender-Sicht.

## Kurz gesagt: vom Auftrag bis zum Zahlungseingang

Order-to-Cash (kurz **O2C**) beschreibt den **kompletten Vertriebsprozess** in SAP S/4HANA — von der ersten Bestellung des Kunden bis zum tatsächlichen Geldeingang auf dem Konto. Der Begriff heißt sinngemäß *„vom Auftrag bis zum Zahlungseingang“*, und genau so sollte man ihn denken: als durchgängige Kette, in der jeder Schritt den nächsten anstößt und jeder Beleg auf den vorherigen verweist.

Im Vertrieb ist O2C der Leitprozess schlechthin. Alles andere — Stammdatenpflege, Preisfindung, Verfügbarkeitsprüfung, Reporting — dient am Ende demselben Zweck: diese Kette sauber durchlaufen zu lassen.

## Die sechs Schritte im Überblick

Bevor wir in jeden Schritt eintauchen, hier die feste Reihenfolge:

1. **Kundenauftrag anlegen** (Sales Order)
2. **Auslieferung anlegen** (Delivery)
3. **Kommissionierung** (Waren zusammenstellen)
4. **Warenausgang buchen** (Goods Issue)
5. **Faktura erstellen** (Rechnung / Billing Document)
6. **Zahlungseingang buchen** (Incoming Payment)

Ein Punkt ist dabei besonders wichtig: Der **Warenausgang kommt vor der Fakturierung**, nicht danach. Warum das so ist, sehen wir gleich in Schritt 4.

## Schritt 1: Kundenauftrag anlegen

Alles beginnt mit dem **Kundenauftrag** (englisch *Sales Order*). Der Kunde hat etwas bestellt — telefonisch, per E-Mail, über einen Webshop oder direkt im Vertriebsinnendienst — und der Sachbearbeiter erfasst diesen Auftrag in SAP.

Der Kundenauftrag ist der **erste Beleg** im Prozess und damit der Auslöser für alles, was folgt. Er enthält im Wesentlichen:

- den **Auftraggeber** und gegebenenfalls abweichenden **Warenempfänger**, **Rechnungsempfänger** und **Regulierer**
- das bestellte **Material** mit Menge
- den vereinbarten **Preis** (über die Preisfindung ermittelt)
- das gewünschte **Lieferdatum**
- die **Verkaufsorganisation**, den **Vertriebsweg** und die **Sparte** (zusammen: der Vertriebsbereich)

Beim Anlegen passiert im Hintergrund einiges automatisch: SAP führt die **Verfügbarkeitsprüfung (ATP)** durch, ermittelt über die Preisfindung den Preis und schlägt einen Liefertermin vor.

Hinter dem Begriff „Kunde“ steckt im modernen S/4HANA der **Geschäftspartner (Business Partner)** mit der Rolle „Kunde“. Wenn dieses Konzept noch neu ist, hilft der Beitrag zum [Geschäftspartner-Konzept in S/4HANA](/blog/de/geschaeftspartner-konzept-s4hana/) weiter.

## Schritt 2: Auslieferung anlegen

Sobald der Kundenauftrag steht und die Ware verfügbar ist, entsteht der zweite Beleg: die **Auslieferung** (englisch *Outbound Delivery*). Sie ist der Übergang vom kaufmännischen Vertriebsbeleg in die Logistik.

Die Auslieferung ist **keine bloße Kopie** des Kundenauftrags. Sie ist ein eigenständiger Logistikbeleg, der alle Daten bündelt, die das Lager zum Versenden braucht:

- welches **Material** in welcher **Menge** versendet wird
- aus welchem **Werk** und welchem **Lagerort** die Ware kommt
- an welche **Versandstelle** der Auftrag gegeben wird
- das geplante **Warenausgangsdatum**

Die Auslieferung kann **einzeln** zu einem Kundenauftrag angelegt werden oder in einem **Sammelvorgang** für viele Aufträge gleichzeitig. Im operativen Vertrieb ist der Sammelvorgang der Regelfall. Merke: Mit der Auslieferung wechselt der Prozess vom Vertrieb in die Logistik — ab hier denkt SAP nicht mehr in „Auftrag“, sondern in „Sendung“.

## Schritt 3: Kommissionierung

Bevor irgendetwas das Lager verlässt, muss die Ware **physisch zusammengestellt** werden. Diesen Schritt nennt SAP **Kommissionierung** (englisch *Picking*). Er umfasst alles, was im Lager passiert, damit die Auslieferung versandbereit wird:

- der Lagerist erhält die **Kommissionierliste**
- er entnimmt die Materialien aus den jeweiligen Lagerplätzen
- die **kommissionierte Menge** wird in der Auslieferung erfasst und gegen die **angeforderte Menge** abgeglichen
- bei Bedarf wird die Ware verpackt und auf einen Versandträger (zum Beispiel eine Palette) gesetzt

Nutzt das Unternehmen ein angeschlossenes **Lagerverwaltungssystem (EWM)**, läuft die Kommissionierung dort als eigener Prozess mit Lageraufträgen. Wichtig ist das Grundverständnis: Kommissionierung ist der physische Schritt zwischen Auslieferung und Warenausgang — und sie ist etwas anderes als der Warenausgang. Erst wird kommissioniert, danach gebucht.

## Schritt 4: Warenausgang buchen

Jetzt kommt einer der wichtigsten Schritte: der **Warenausgang** (englisch *Goods Issue*, kurz WA). Mit dem Warenausgang sagst du dem System: *„Die Ware hat das Lager verlassen.“* Diese Buchung löst eine ganze Kette automatisch aus:

- der **Bestand** des Materials wird im System reduziert
- es wird automatisch ein **Materialbeleg** erzeugt (er dokumentiert die mengenmäßige Bewegung)
- es wird automatisch ein **Buchhaltungsbeleg** erzeugt (er dokumentiert die wertmäßige Buchung in der Finanzbuchhaltung)
- auf der Kostenseite werden die **Herstellkosten des Umsatzes** (Cost of Goods Sold) belastet

Genau diese Doppelbuchung — einmal Materialbeleg, einmal Buchhaltungsbeleg — kennt man aus der Materialwirtschaft schon vom Wareneingang. Im Vertrieb passiert das spiegelbildlich, nur in die andere Richtung: Bestand *raus* statt *rein*.

Und hier der zentrale Punkt: **Der Warenausgang muss vor der Fakturierung gebucht werden.** Der Grund ist einfach — die Rechnung soll nur das fakturieren, was tatsächlich versendet wurde. Liefe die Rechnung vor dem Warenausgang, könnte ein Kunde Ware in Rechnung gestellt bekommen, die noch im Lager liegt, oder die Buchhaltungsbelege wären nicht konsistent. Deshalb erzwingt SAP diese Reihenfolge.

## Schritt 5: Faktura erstellen

Erst nach dem Warenausgang wird die **Faktura** (englisch *Invoice* oder *Billing Document*) erstellt. Sie ist der Beleg, mit dem dem Kunden die Leistung in Rechnung gestellt wird. Beim Anlegen passiert Folgendes:

- SAP übernimmt die relevanten Daten aus **Kundenauftrag** und **Auslieferung**
- die **Konditionen** (Preise, Rabatte, Steuern) werden final bestimmt
- es wird ein **Fakturabeleg** erzeugt
- parallel entsteht automatisch ein **Buchhaltungsbeleg**: die *offene Forderung* gegen den Kunden

Die Faktura kann **auftragsbezogen** oder **lieferbezogen** sein. Im klassischen Order-to-Cash mit physischer Ware ist die *lieferbezogene Faktura* der Standard — sie referenziert direkt auf die Auslieferung. Bei reinen Dienstleistungen ohne Lieferschein kommt die *auftragsbezogene Faktura* zum Einsatz. Mit der Buchung der Faktura gibt der Vertrieb den Vorgang an die Finanzbuchhaltung ab; der offene Posten beim Kunden ist die Brücke zwischen beiden Bereichen.

## Schritt 6: Zahlungseingang buchen

Der letzte Schritt ist der **Zahlungseingang** (englisch *Incoming Payment*). Der Kunde bezahlt die Rechnung, und die offene Forderung wird ausgeglichen. Dieser Schritt findet nicht mehr im Vertrieb statt, sondern in der **Finanzbuchhaltung (FI)** — gehört aber trotzdem zum O2C-Prozess. Typischerweise wird dabei:

- der Geldeingang auf dem Bankkonto verbucht
- der **offene Posten** beim Kunden **ausgeglichen**
- gegebenenfalls Skonto, Rundungsdifferenz oder Teilzahlung behandelt

Man muss dafür nicht tief in die FI-Buchungen einsteigen. Es reicht der Merksatz: Vertrieb und Finanzbuchhaltung sind über die integrierte Buchung der Faktura verknüpft, und erst der Zahlungseingang schließt den Order-to-Cash-Kreis vollständig ab.

## Der Belegfluss: wie alles zusammenhängt

Eines der wichtigsten Konzepte im Vertrieb ist der **Belegfluss** (englisch *Document Flow*). Bei jedem Schritt entsteht ein neuer Beleg, der **auf den vorherigen verweist**. Sauber durchlaufen sieht die Kette so aus:

*Kundenauftrag → Auslieferung → Warenausgang (Materialbeleg + Buchhaltungsbeleg) → Faktura → Buchhaltungsbeleg → Zahlungseingang*

In jedem dieser Belege lässt sich der Belegfluss per Klick anzeigen. Damit sieht man auf einen Blick:

- aus welchem Kundenauftrag eine Auslieferung entstanden ist
- welche Faktura zu welcher Lieferung gehört
- ob der Warenausgang schon gebucht wurde
- ob bereits eine Zahlung eingegangen ist

Der Belegfluss garantiert **Nachvollziehbarkeit und Revisionssicherheit**: Jeder Cent, der bei einem Kunden eingeht, lässt sich bis zum ursprünglichen Auftrag zurückverfolgen. Genau das ist im Vertriebsalltag Gold wert.

## Häufige Stolpersteine

- **Warenausgang und Faktura in der Reihenfolge verdrehen.** Erst Warenausgang, dann Faktura — nicht umgekehrt. Nur was das Lager verlassen hat, darf in Rechnung gestellt werden.
- **Kundenauftrag und Auslieferung gleichsetzen.** Die Auslieferung ist kein Klon des Auftrags, sondern ein eigener Logistikbeleg mit Versandstelle, Lagerort und Warenausgangsdatum.
- **Kommissionierung mit Warenausgang verwechseln.** Kommissionierung ist das physische Zusammenstellen, der Warenausgang die Buchung des Verlassens — zwei verschiedene Schritte.
- **Auftrags- und lieferbezogene Faktura vermischen.** Bei physischer Ware ist die Faktura lieferbezogen, bei reinen Dienstleistungen auftragsbezogen.

## Kurz zusammengefasst

Order-to-Cash ist die durchgängige Kette vom Kundenauftrag bis zum Zahlungseingang. Ein Kunde bestellt (Kundenauftrag), das Lager bereitet die Sendung vor (Auslieferung), die Ware wird zusammengestellt (Kommissionierung), der Versand wird gebucht (Warenausgang mit Material- und Buchhaltungsbeleg), dem Kunden wird die Leistung in Rechnung gestellt (Faktura), und am Ende kommt das Geld an (Zahlungseingang in der Finanzbuchhaltung). Wer sich diese Erzählung und den **Belegfluss** als Bild einprägt, versteht den SAP-Vertrieb schon zu einem großen Teil — denn dann erkennt man nicht nur die Begriffe wieder, sondern auch, wie sie zusammenhängen.

## Häufige Fragen

### Was bedeutet Order-to-Cash?

Order-to-Cash beschreibt den kompletten Vertriebsprozess in SAP — von der Bestellung des Kunden bis zum Zahlungseingang. Sinngemäß heißt der Begriff „vom Auftrag bis zum Geldeingang“.

### Was ist der Unterschied zwischen Auslieferung und Kundenauftrag?

Der Kundenauftrag ist der kaufmännische Vertriebsbeleg mit Kunde, Material, Preis und Termin. Die Auslieferung ist ein eigenständiger Logistikbeleg mit Versandstelle, Lagerort und Warenausgangsdatum — keine bloße Kopie des Auftrags.

### Warum wird der Warenausgang vor der Rechnung gebucht?

Die Rechnung soll nur das fakturieren, was tatsächlich versendet wurde. Deshalb bucht SAP zuerst den Warenausgang (Ware verlässt das Lager) und erstellt erst danach die Faktura. So bleiben Bestand und Buchhaltung konsistent.

### Was ist der Belegfluss im Vertrieb?

Der Belegfluss zeigt, wie die Belege eines Vorgangs zusammenhängen: Kundenauftrag, Auslieferung, Warenausgang, Faktura und Zahlung verweisen aufeinander. Per Klick lässt sich jeder Vorgang bis zum Ursprungsauftrag zurückverfolgen.
