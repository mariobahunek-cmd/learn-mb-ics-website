---
layout: post
lang: de
title: "Kundenstammdaten in SAP S/4HANA — die drei Datenebenen verstehen"
description: "Kundenstammdaten sind die Grundlage jedes Vertriebsprozesses in SAP. Wie das Geschäftspartner-Konzept funktioniert, welche drei Datenebenen es gibt und warum Partnerrollen zählen."
slug: kundenstammdaten-in-sap
permalink: /blog/de/kundenstammdaten-in-sap/
translation_key: post-kundenstammdaten
date: 2026-07-07
category: "Stammdaten"
keywords: "SAP Kundenstammdaten, Geschäftspartner, Vertriebsbereichsdaten, Buchungskreisdaten, Partnerrollen, SAP S/4HANA Sales, Stammdaten pflegen"
reading_time: 8
sources:
  - label: "SAP Help Portal — Sales (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Sales / Business Partner — allgemeine Grundlagen zu Kundenstammdaten und dem Geschäftspartner-Konzept. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen einem Geschäftspartner und einem Kunden in SAP?"
    a: "Der Geschäftspartner ist das übergeordnete Stammdatenobjekt in SAP S/4HANA. „Kunde“ ist eine Rolle, die dieser Geschäftspartner einnehmen kann — genauso wie „FI-Debitor“ oder „Lieferant“. Ein und derselbe Geschäftspartner kann also mehrere Rollen gleichzeitig tragen."
  - q: "Wo werden Kundenstammdaten in SAP gepflegt?"
    a: "Zentral über die Geschäftspartner-Pflege — klassisch mit der Transaktion BP oder über eine passende Fiori-App im SAP Fiori Launchpad. Dort pflegst du allgemeine Daten, Vertriebsbereichsdaten und Buchungskreisdaten an einer Stelle."
  - q: "Warum muss ich Vertriebsbereichsdaten pro Bereich separat pflegen?"
    a: "Weil ein Kunde in verschiedenen Vertriebsbereichen unterschiedlich behandelt werden kann — etwa im Direktverkauf anders als im Großhandel. Willst du einen Kunden in mehreren Vertriebsbereichen einsetzen, brauchst du für jeden Bereich einen eigenen Datensatz."
  - q: "Was passiert, wenn Partnerrollen fehlen?"
    a: "Ohne die notwendigen Partnerrollen — Auftraggeber, Warenempfänger, Rechnungsempfänger, Regulierer — lässt sich oft gar kein Vertriebsbeleg anlegen. Der Prozess bleibt dann stehen, bis die Rollen im Kundenstammsatz ergänzt sind."
---

Ein Kundenauftrag ist in Sekunden angelegt: Adresse, Zahlungsbedingungen und Versandregeln stehen schon da, ohne dass jemand sie eintippt. Woher kommen diese Angaben? Aus den **Kundenstammdaten** — dem Datensatz, auf den fast jeder Schritt im SAP-Vertrieb zugreift, vom Angebot über den Kundenauftrag bis zur Rechnung. Woran die meisten in meinen Kursen hängen bleiben, ist nicht das Pflegen der Felder, sondern der Aufbau dahinter: das Geschäftspartner-Konzept und die drei Datenebenen, die man leicht verwechselt.

## Die zentrale Datenquelle für den Vertrieb

Kundenstammdaten sind ein Stammdatensatz, der alles Wichtige über einen Kunden bündelt: wer er ist, wohin geliefert wird, wie er bezahlt und wie er steuerlich behandelt wird. Wenn du einen Kundenauftrag anlegst, holt sich das System die meisten Angaben automatisch aus diesem Satz. Neu eintippen musst du sie nicht.

Das Besondere in SAP S/4HANA: Kunden werden über das **Geschäftspartner-Konzept** verwaltet. Ein Geschäftspartner ist das übergeordnete Objekt, und „Kunde“ ist eine der Rollen, die er einnehmen kann.

## Woher ein Verkaufsbeleg seine Daten bezieht

Legst du einen Verkaufsbeleg an, füllt SAP viele Felder aus verschiedenen Stammdatenquellen automatisch vor:

- **Geschäftspartner-Stammdaten (Kunde)** — Adresse, Zahlungsbedingungen, Versandkonditionen
- **Materialstammdaten** — Beschreibung, Gewicht, Volumen, Mengeneinheit
- **Kunden-Material-Informationen** — kundenspezifische Materialnummern
- **Konditionsstammdaten** — Preisfindung, Materialpreis, Kundenrabatt
- **Nachrichtenstammdaten** — Versand von Auftragsbestätigungen per E-Mail, EDI oder Fax
- **Steuerungstabellen** — im Customizing gepflegt, steuern, welche Daten vorgeschlagen werden

Die meisten übernommenen Werte sind **Vorschlagswerte**, die du bei Bedarf überschreiben kannst. Auch ein vorhergehender Beleg kann als Vorlage dienen, etwa ein Angebot, aus dem der Kundenauftrag entsteht. Mehr zum Zusammenspiel im Vertrieb findest du im Überblick zum [Order-to-Cash-Prozess](/blog/de/order-to-cash-process-sales/).

## Das Geschäftspartner-Konzept in SAP S/4HANA

In SAP S/4HANA werden Kunden und Lieferanten über **Geschäftspartner-Stammdaten** verwaltet. Damit pflegst du sie *zentral* — anders als im alten SAP ERP, wo Kunde und Lieferant getrennt geführt wurden.

Konkret heißt das: Ein und derselbe Geschäftspartner kann gleichzeitig Kunde, FI-Debitor und sogar Lieferant sein — ohne dass du ihn mehrfach anlegen musst. Das Geschäftspartner-Konzept bündelt alle Stammdaten an einer Stelle und unterscheidet die verschiedenen Geschäftskontexte über Rollen. Wenn du das Konzept vertiefen möchtest, hilft der Artikel zum [Geschäftspartner-Konzept in S/4HANA](/blog/de/geschaeftspartner-konzept-s4hana/).

### Welche Geschäftspartnertypen gibt es?

Beim Anlegen legst du zwingend den **Geschäftspartnertyp** fest. Zur Wahl stehen die Person für eine natürliche Person, die Organisation für ein Unternehmen, eine Abteilung oder einen Verband, und die Gruppe etwa für eine Wohngemeinschaft, ein Ehepaar oder einen Vorstand.

### Wie funktioniert das Rollenkonzept?

Die Verbindung zwischen einem Geschäftspartner und den einzelnen Anwendungen entsteht über ein **Rollenkonzept**. Eine Rolle steht für einen Geschäftskontext, in dem der Partner auftreten kann. Typische Rollen sind:

- **Kunde** — relevant für Verkaufsprozesse
- **FI-Debitor** — relevant für die Buchhaltung
- **Lieferant** — falls derselbe Partner auch beschafft wird

Erst wenn die passenden Rollen gepflegt sind, kannst du den Geschäftspartner sowohl im Vertrieb als Auftraggeber verwenden als auch in der Buchhaltung als Empfänger einer Forderung führen. Gepflegt wird das entweder mit der Transaktion `BP` oder über eine entsprechende Fiori-App im SAP Fiori Launchpad.

## Die drei Datenebenen eines Kundenstammsatzes

Die Daten eines Kunden gliedern sich in drei Ebenen. Diese Hierarchie ist der wichtigste Punkt, den man verstehen sollte — und zugleich der, der am häufigsten durcheinandergebracht wird.

### Ebene 1 — Allgemeine Daten (Mandantenebene)

Allgemeine Daten sind für Vertrieb *und* Buchhaltung relevant. Sie gelten für alle Organisationseinheiten innerhalb eines Mandanten. Dazu gehören:

- **Anschrift** (Straße, Postleitzahl, Ort, Land, Region, Sprache)
- **Bankverbindungen**
- **Kommunikationsdaten** (Telefon, E-Mail)
- **Steuernummern**

### Ebene 2 — Vertriebsbereichsdaten (Rolle „Kunde“)

Vertriebsbereichsdaten sind nur für den Vertrieb relevant. Sie gelten für einen bestimmten **Vertriebsbereich**, und der setzt sich aus drei Komponenten zusammen: der Verkaufsorganisation als verkaufender Einheit, dem Vertriebsweg (etwa Direktverkauf oder Großhandel) und der Sparte, also der Produktsparte.

Wichtig: Willst du einen Kunden in mehreren Vertriebsbereichen einsetzen, musst du die Vertriebsbereichsdaten *für jeden Bereich separat* pflegen. Zur besseren Übersicht sind die Felder auf Registerkarten verteilt, unter anderem:

- **Aufträge** — Bestellverhalten, Kundenschema, Versandbedingungen
- **Versand** — Lieferwerk, Lieferpriorität, Komplettlieferung
- **Fakturierung** — Zahlungsbedingungen, Incoterms, Kontierungsgruppe, Steuerklassifikation
- **Partnerrollen** — Auftraggeber, Warenempfänger, Rechnungsempfänger, Regulierer

### Ebene 3 — Buchungskreisdaten (Rolle „FI-Debitor“)

Buchungskreisdaten sind für die Buchhaltung relevant und gelten für einen bestimmten Buchungskreis. Sie werden häufig von der Buchhaltung selbst gepflegt. Ein zentrales Feld ist das **Abstimmkonto**: Über dieses Sachkonto werden Debitorenbuchungen automatisch im Hauptbuch mitgeschrieben, sodass Nebenbuch und Hauptbuch immer im Einklang bleiben.

## Die vier Standard-Partnerrollen im Vertrieb

Jeder Kundenstammsatz braucht im Vertrieb vier obligatorische Partnerrollen. In den meisten Fällen ist das alles dieselbe Partei, bei Konzernkunden können die Rollen aber aufgeteilt sein:

- **Auftraggeber** — wer den Kundenauftrag erteilt
- **Warenempfänger** — wer die Ware physisch bekommt (kann eine andere Adresse sein, z. B. eine Filiale)
- **Rechnungsempfänger** — wer die Rechnung erhält
- **Regulierer** — wer die Rechnung bezahlt (z. B. eine Konzern-Zentralkasse)

Ein Beispiel aus der Konzernwelt: Auftraggeber ist die Tochtergesellschaft, Warenempfänger eine bestimmte Filiale, Rechnungsempfänger die Konzernverwaltung und Regulierer die zentrale Kasse. Die Trennung dieser Rollen erlaubt es, komplexe Liefer- und Zahlungswege sauber abzubilden.

## Warum Stammdaten in Sichten organisiert sind

SAP-Stammdaten sind in **Sichten** organisiert, die jeweils einer Organisationseinheit zugeordnet sind — Werk, Verkaufsorganisation, Buchungskreis und so weiter. Diese segmentierte Struktur sorgt für Flexibilität und für **Datenintegrität**: Wenn alle relevanten Angaben in einem einzigen Datenobjekt zusammenlaufen, gibt es keine redundanten Kopien. Vertrieb, Einkauf, Bestandsführung, Rechnungsprüfung und Finanzwesen greifen auf dieselben Daten zu — ein zentraler Vorteil gegenüber älteren Systemen mit getrennten Debitoren- und Kreditoren-Welten.

## Was Anwender im Alltag damit tun

Kundenstammdaten zu pflegen ist keine tägliche Aufgabe. Das passiert meist beim Onboarding eines Neukunden oder bei größeren Datenpflege-Aktionen, oft durch Stammdaten-Sachbearbeiter oder die Buchhaltung. Trotzdem profitiert jeder im Vertrieb von sauberen Stammdaten, denn Fehler wirken sich direkt im Prozess aus:

- **Falsche Adresse** → Lieferung geht zurück, es entstehen Kosten
- **Falsche Zahlungsbedingung** → zu großzügiger Skonto, Margenverlust
- **Falsche Steuerklassifikation** → falscher Steuerausweis, Compliance-Risiko
- **Fehlende Partnerrollen** → Beleg lässt sich nicht anlegen, der Prozess steht

Wer im Vertrieb mit SAP arbeitet, sollte deshalb mindestens das Konzept der drei Datenebenen verstehen, auch wenn er selbst selten Stammdaten pflegt.

## Häufige Stolpersteine

Vor allem zwei Dinge sorgen fast garantiert für Verwirrung: die drei Sichten (allgemeine Daten, Buchungskreis- und Vertriebsbereichsdaten) und die vier Partnerrollen, die gern durcheinandergeraten. Um genau diese kreisen die häufigsten Stolpersteine:

- **Die drei Datenebenen verwechseln.** Allgemeine Daten gelten mandantenweit, Vertriebsbereichsdaten nur je Vertriebsbereich, Buchungskreisdaten nur je Buchungskreis. Wer das durcheinanderbringt, sucht Felder an der falschen Stelle.
- **Vertriebsbereichsdaten nur einmal anlegen.** Ein Kunde, der in mehreren Vertriebsbereichen aktiv ist, braucht überall eigene Vertriebsbereichsdaten — sonst lässt er sich dort nicht verwenden.
- **Rollen vergessen.** Ohne die Rolle „Kunde“ gibt es keine Vertriebssicht, ohne „FI-Debitor“ keine Buchhaltungssicht. Fehlt eine Rolle, fehlt der halbe Prozess.

## Worauf es ankommt

Kundenstammdaten sind die zentrale Datenquelle für jeden Vertriebsprozess in SAP. In S/4HANA laufen sie über das Geschäftspartner-Konzept, bei dem „Kunde“ nur eine von mehreren Rollen eines Geschäftspartners ist. Die Daten gliedern sich in drei Ebenen: allgemeine Daten, Vertriebsbereichsdaten und Buchungskreisdaten. Über Partnerrollen werden sie mit den einzelnen Prozessen verknüpft. Wer diese Struktur einmal verinnerlicht hat, versteht, warum ein sauber gepflegter Kundenstamm die halbe Miete für reibungslose Aufträge, Lieferungen und Rechnungen ist.

## Häufige Fragen

### Was ist der Unterschied zwischen einem Geschäftspartner und einem Kunden in SAP?

Der Geschäftspartner ist das übergeordnete Stammdatenobjekt in SAP S/4HANA. „Kunde“ ist eine Rolle, die dieser Geschäftspartner einnehmen kann — genauso wie „FI-Debitor“ oder „Lieferant“. Ein und derselbe Geschäftspartner kann also mehrere Rollen gleichzeitig tragen.

### Wo werden Kundenstammdaten in SAP gepflegt?

Zentral über die Geschäftspartner-Pflege — klassisch mit der Transaktion BP oder über eine passende Fiori-App im SAP Fiori Launchpad. Dort pflegst du allgemeine Daten, Vertriebsbereichsdaten und Buchungskreisdaten an einer Stelle.

### Warum muss ich Vertriebsbereichsdaten pro Bereich separat pflegen?

Weil ein Kunde in verschiedenen Vertriebsbereichen unterschiedlich behandelt werden kann — etwa im Direktverkauf anders als im Großhandel. Willst du einen Kunden in mehreren Vertriebsbereichen einsetzen, brauchst du für jeden Bereich einen eigenen Datensatz.

### Was passiert, wenn Partnerrollen fehlen?

Ohne die notwendigen Partnerrollen — Auftraggeber, Warenempfänger, Rechnungsempfänger, Regulierer — lässt sich oft gar kein Vertriebsbeleg anlegen. Der Prozess bleibt dann stehen, bis die Rollen im Kundenstammsatz ergänzt sind.
