---
layout: post
lang: de
title: "Debitorenbuchhaltung in SAP S/4HANA verständlich erklärt"
description: "Debitorenstammsatz, Rechnung, Zahlungseingang, offene Posten, Mahnwesen und der Draht zum Hauptbuch: wie die Debitorenbuchhaltung in S/4HANA funktioniert."
slug: debitorenbuchhaltung-s4hana
permalink: /blog/de/debitorenbuchhaltung-s4hana/
translation_key: post-accounts-receivable
date: 2026-07-08
category: "Finanzen"
keywords: "SAP Debitorenbuchhaltung, FI-AR, Debitorenstammsatz, Geschäftspartner, Ausgangsrechnung, Zahlungseingang, offene Posten, Mahnprogramm, Abstimmkonto, S/4HANA Finance"
reading_time: 9
sources:
  - label: "SAP Help Portal — Accounts Receivable (SAP S/4HANA Finance)"
    url: "https://help.sap.com/"
    note: "Bereich Finance / Accounts Receivable — allgemeine Grundlagen. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist die Debitorenbuchhaltung in SAP?"
    a: "Die Debitorenbuchhaltung (englisch Accounts Receivable, kurz FI-AR) ist das Nebenbuch, das alle Forderungen gegenüber Kunden verwaltet. Jeder Vorgang mit einem Kunden — Ausgangsrechnung, Gutschrift, Zahlungseingang, Mahnung — wird hier gebucht und gleichzeitig über ein Abstimmkonto im Hauptbuch mitgeführt."
  - q: "Wie wird ein Debitor in SAP S/4HANA angelegt?"
    a: "Ein Debitor wird nicht mehr als eigenes Objekt angelegt, sondern als Geschäftspartner mit der Rolle „FI Debitor“. Die Daten verteilen sich auf allgemeine Angaben auf Mandantenebene (Anschrift, Bankverbindung) und firmenspezifische Angaben auf Buchungskreisebene (Kontoverwaltung, Zahlungsverkehr, Mahndaten)."
  - q: "Was ist ein Abstimmkonto?"
    a: "Ein Abstimmkonto ist ein Sachkonto im Hauptbuch, auf dem jede Buchung des Debitoren-Nebenbuchs automatisch mitgebucht wird. So bleibt der Saldo aller Debitorenkonten immer identisch mit dem Saldo des Abstimmkontos — die Grundlage für eine konsistente Bilanz."
  - q: "Wie funktioniert das Mahnprogramm in SAP?"
    a: "Das Mahnprogramm wählt überfällige offene Posten aus, bestimmt je Konto die Mahnstufe und erzeugt daraus Mahnungen. Der Ablauf hat vier Schritte: Parameter pflegen, Mahnlauf einplanen, Mahnvorschlag bearbeiten und Mahndruck starten."
  - q: "Was ist ein offener Posten in der Debitorenbuchhaltung?"
    a: "Ein offener Posten ist eine gebuchte Forderung, die noch nicht bezahlt ist. Geht die Zahlung ein, wird der Zahlungseingang gegen die Rechnung ausgeglichen und der Posten gilt als erledigt. Nur unbezahlte offene Posten werden im Mahnlauf berücksichtigt."
---

Wer in der Buchhaltung mit SAP S/4HANA arbeitet, hat fast täglich mit Kundenforderungen zu tun: eine Rechnung wird geschrieben, das Geld kommt herein, ein Posten wird ausgeglichen, ein säumiger Kunde bekommt eine Mahnung. Genau diese Vorgänge bündelt die Debitorenbuchhaltung. Dieser Artikel erklärt in klarer Sprache, wie sie aufgebaut ist und wie die einzelnen Bausteine zusammenspielen.

## Kurz gesagt: das Nebenbuch für Kundenforderungen

Die Debitorenbuchhaltung (englisch Accounts Receivable, kurz **FI-AR**) ist das Nebenbuch in der SAP-Finanzbuchhaltung, das alle **Forderungen gegenüber Kunden** verwaltet. Ein Kunde heißt in SAP **Debitor**. Jeder Geschäftsvorfall mit einem Debitor — Ausgangsrechnung, Gutschrift, Zahlungseingang, Mahnung — wird über die Debitorenbuchhaltung abgebildet und gleichzeitig im Hauptbuch über ein **Abstimmkonto** mitgebucht.

Der wichtigste Gedanke dahinter: Das Nebenbuch führt die Details Kunde für Kunde, das Hauptbuch führt die Summe. Beide bleiben durch das Abstimmkonto automatisch im Gleichschritt — daher ist die Bilanz jederzeit konsistent, ohne dass jemand von Hand abstimmen muss.

## Was macht ein Buchhalter in der Debitorenbuchhaltung?

Die tägliche Arbeit dreht sich um wenige, immer wiederkehrende Aufgaben:

- **Debitorenstammdaten pflegen** — Anschrift, Zahlungsbedingungen, Mahnverfahren
- **Ausgangsrechnungen buchen** — die Forderung gegenüber dem Kunden entsteht
- **Gutschriften erfassen** — etwa bei Reklamationen oder Rücksendungen
- **Zahlungseingänge verbuchen** und offene Posten ausgleichen
- **Mahnungen versenden** bei überfälligen Forderungen
- **Sonderfälle** wie Anzahlungen, Bürgschaften oder Wertberichtigungen abbilden

So verschieden diese Aufgaben klingen, im Kern kehren drei Bausteine immer wieder: der **Stammsatz** (wer ist der Kunde?), der **Beleg** (was wurde gebucht?) und die **Mahnung** (wie treibe ich Überfälliges ein?). Wer diese drei auseinanderhält, hat die Debitorenbuchhaltung im Griff.

## Der Debitor im Geschäftspartner-Konzept

In SAP S/4HANA wird ein Debitor nicht mehr als eigenes Objekt angelegt, sondern als **Geschäftspartner mit der Rolle „FI Debitor“**. Diese Vereinheitlichung kam mit S/4HANA: Früher gab es getrennte Welten für Debitor, Kreditor (Lieferant) und Geschäftspartner. Heute ist der Geschäftspartner das zentrale Objekt, und eine Person oder Firma kann mehrere Rollen tragen — zum Beispiel Kunde und Lieferant zugleich.

Die Felder eines Debitorenstammsatzes verteilen sich auf zwei Ebenen:

### Mandantenebene — die allgemeinen Daten

Auf **Mandantenebene** stehen die Angaben, die für das gesamte Unternehmen gelten, unabhängig davon, welche Gesellschaft mit dem Kunden abrechnet:

- **Anschrift** — Straße, Postleitzahl, Ort, Land
- **Steuerdaten**
- **Zahlungsverkehr**
- **Bankverbindung** — Bank-IDs mit IBAN

### Buchungskreisebene — die firmenspezifischen Daten

Ein **Buchungskreis** ist die kleinste rechtlich selbstständige Einheit in SAP, für die eine vollständige Buchhaltung geführt wird — praktisch eine bilanzierende Gesellschaft. Auf **Buchungskreisebene** stehen die Angaben, die nur für diese eine Gesellschaft gelten:

- **Kontoverwaltung** — hier liegt unter anderem das Abstimmkonto
- **Zahlungsverkehr**
- **Korrespondenz** — hier liegen die Mahndaten

**Praxisregel:** Der Eintrag auf Buchungskreisebene hat Vorrang vor dem Eintrag auf Mandantenebene. Ist eine Bankverbindung auf beiden Ebenen gepflegt, gilt die buchungskreisspezifische. Bankstammsätze selbst werden übrigens auf Mandantenebene angelegt und lassen sich anschließend jedem Debitor und Kreditor zuweisen — das erspart Doppelpflege.

## Wie wird eine Ausgangsrechnung gebucht?

Wie alle Buchungen in der Finanzbuchhaltung besteht auch eine Debitorenrechnung aus einem **Belegkopf** (Datum, Buchungskreis, Belegart) und **Belegpositionen** (die einzelnen Zeilen). Die **Belegart** steuert dabei den Nummernkreis und die zulässigen Kontotypen. Typische Belegarten in der Debitorenbuchhaltung sind zum Beispiel eine eigene Art für Debitorenrechnungen, eine für Gutschriften und eine für Zahlungseingänge. Das System schlägt die passende Belegart automatisch vor, je nachdem welche App du gerade nutzt.

Ein illustratives Beispiel: Du buchst eine Rechnung über **220.000 €** an einen Kunden. Die Rechnung enthält 200.000 € Warenwert plus 20.000 € Umsatzsteuer (hier 10 %). Daraus wird:

| Konto | Soll | Haben |
| --- | --- | --- |
| Forderungen (Debitor) | 220.000 € | |
| Umsatzerlöse | | 200.000 € |
| Umsatzsteuer | | 20.000 € |

Die Forderung gegenüber dem Kunden steht im **Soll** (er schuldet dir Geld), Erlöse und Steuer stehen im **Haben**. Bevor du endgültig buchst, kannst du die Buchung **simulieren**: SAP zeigt dir das fertige Ergebnis inklusive der automatisch erzeugten Steuerposition, bevor etwas festgeschrieben wird. Erst mit dem Buchen vergibt das System eine Belegnummer.

## Wie werden Zahlungseingänge und offene Posten behandelt?

Sobald eine Rechnung gebucht ist, gilt die Forderung als **offener Posten** — eine gebuchte Forderung, die noch nicht bezahlt ist. Kommt das Geld herein, wird der **Zahlungseingang** gegen die passende Rechnung ausgeglichen. Der offene Posten ist damit erledigt und taucht in keiner Mahnung mehr auf.

Diese **Offene-Posten-Verwaltung** ist das Herzstück der Debitorenbuchhaltung: Zu jedem Kunden siehst du auf einen Blick, welche Rechnungen noch offen und welche bereits ausgeglichen sind. Zahlungen lassen sich manuell zuordnen oder — bei großen Mengen — über den automatischen **Zahllauf** verarbeiten. Beim Zahllauf bucht das System, gleicht offene Posten aus und versorgt die Druckprogramme mit den nötigen Daten. Für eingehende Zahlungen kann es zum Beispiel per **SEPA-Lastschrift** einziehen, sofern ein gültiges Lastschriftmandat des Kunden vorliegt.

## Debitor und Kreditor in einer Person

In der Praxis ist ein Geschäftspartner manchmal beides zugleich: dein **Kunde** (Debitor) und dein **Lieferant** (Kreditor). Ist die Verknüpfung in beiden Stammsätzen gepflegt, kann der Zahllauf die offenen Posten der beiden Konten **verrechnen**.

Ein illustratives Beispiel: Du schuldest dem Partner 5.000 € (als Lieferant) und er schuldet dir 8.000 € (als Kunde). Statt beide Beträge getrennt zu bewegen, saldiert der Zahllauf — du überweist nur die Differenz von 3.000 €. Das spart Zahlungsverkehr und macht die Beziehung übersichtlicher.

## Wie funktioniert das Mahnprogramm?

Zahlt ein Kunde nicht bis zum Fälligkeitsdatum, stellt sich die Frage nach einer Mahnung. Die erste kann eine freundliche Erinnerung sein; bleibt die Zahlung aus, wird der Ton schärfer. Das **Mahnprogramm** erledigt das automatisch: Es wählt überfällige offene Posten aus, bestimmt je Konto die **Mahnstufe** (also wie oft schon gemahnt wurde) und erzeugt die passende Mahnung.

Der Ablauf hat vier Schritte:

1. **Parameter pflegen** — du legst fest, wie der Lauf arbeitet. Parameter aus einem früheren Lauf lassen sich kopieren.
2. **Mahnlauf einplanen** — das System ermittelt Konten, Posten, Mahnstufen und alle nötigen Daten und sichert das Ergebnis in einem **Mahnvorschlag**.
3. **Mahnvorschlag bearbeiten** — du kannst den Vorschlag ändern, löschen oder neu erstellen, bis das Ergebnis passt.
4. **Mahndruck starten** — die Mahnungen werden gedruckt oder per E-Mail versendet; die Mahndaten in Stammsätzen und Belegen werden in einem Schritt aktualisiert.

Eine Besonderheit: Auch ein **Kreditor** kann gemahnt werden — nämlich dann, wenn er wegen einer Gutschrift ausnahmsweise etwas schuldet.

### Die Mahn-Felder im Stammsatz

Die zentralen Steuerfelder für das Mahnprogramm liegen im Debitorenstammsatz auf der Registerkarte **Korrespondenz**:

- **Mahnverfahren** — ein vordefiniertes Schema, das festlegt, wie gemahnt wird (etwa vier Stufen im Abstand von 14 Tagen)
- **Mahnsperre** — sperrt einen Debitor vorübergehend vom Mahnen
- **Letzte Mahnung** — Datum der letzten Mahnung, in die das Konto einbezogen wurde
- **Mahnstufe** — die höchste erreichte Stufe; das Programm setzt sie automatisch
- **Sachbearbeiter** — dessen Name auf dem Mahnbrief erscheint

Nützlich zu wissen: Über die im Stammsatz hinterlegte **Sprache** kann eine Mahnung in der Sprache des Kunden erstellt werden, sofern ein Formular in dieser Sprache existiert. Und liegt für einen offenen Posten ein Einzugsverfahren wie die Lastschrift vor, unterbleibt in der Regel die Mahnung — denn das System zieht das Geld ohnehin selbst ein.

Diese Steuerung ist nicht nur pauschal je Kunde möglich, sondern auch **je Beleg**: Willst du eine einzelne Rechnung vorübergehend aus dem Mahnlauf nehmen, setzt du die Mahnsperre nur auf diesem Beleg, ohne den ganzen Kunden zu sperren.

## Wie hängt die Debitorenbuchhaltung am Hauptbuch?

Das ist das wohl wichtigste Konzept der Debitorenbuchhaltung: **Jede Buchung im Debitoren-Nebenbuch wird automatisch im Hauptbuch mitgebucht** — auf einem speziellen Sachkonto, das als **Abstimmkonto** deklariert ist.

Buchst du eine Rechnung über 220.000 € auf einen Kunden, entsteht gleichzeitig auf dem Hauptbuch-Sachkonto „Forderungen aus Lieferungen und Leistungen“ eine Buchung in gleicher Höhe — ganz ohne manuelles Zutun. Welches Abstimmkonto gilt, steht im Debitorenstammsatz (Buchungskreisebene).

Der Effekt: Der **Saldo aller Debitorenkonten** ist immer identisch mit dem Saldo des zugehörigen Abstimmkontos im Hauptbuch. Deshalb kannst du dem Abstimmkonto die Gesamtforderung entnehmen und im Nebenbuch jederzeit sehen, aus welchen Kunden sie sich zusammensetzt. Ein Abstimmkonto lässt sich übrigens nicht direkt bebuchen — es wird ausschließlich über das Nebenbuch bewegt.

## Sonderhauptbuchvorgänge — die zweite Ebene

Nicht jeder Vorgang mit einem Kunden ist eine normale Forderung. **Sonderhauptbuchvorgänge** sind Geschäftsvorfälle, die mit dem Debitor verbunden sind, aber getrennt ausgewiesen werden müssen:

- **Anzahlungen**, die du erhältst oder gewährst
- **Bürgschaften**
- **Anzahlungsanforderungen**
- **Wertberichtigungen** auf zweifelhafte Forderungen

Sie laufen über separate **Sonderhauptbuchkonten** und werden im Reporting getrennt gezeigt — damit eine erhaltene Anzahlung nicht mit einer offenen Forderung verwechselt wird. So bleibt klar sichtbar, was echtes Guthaben und was noch offene Forderung ist.

## Kurz zusammengefasst

Die Debitorenbuchhaltung ist das Nebenbuch für alle **Kundenforderungen**. Sie steht auf drei Bausteinen: dem **Stammsatz** (der Debitor als Geschäftspartner), dem **Beleg** (Rechnung, Gutschrift, Zahlungseingang) und der **Mahnung** (das automatische Eintreiben Überfälliger). Der Zahllauf gleicht offene Posten aus, das Mahnprogramm kümmert sich um Säumige, und das **Abstimmkonto** hält Nebenbuch und Hauptbuch jederzeit im Gleichschritt. Wer diese Bausteine auseinanderhält, versteht die Forderungsseite eines S/4HANA-Systems schnell und sicher.

## Häufige Fragen

### Was ist die Debitorenbuchhaltung in SAP?

Die Debitorenbuchhaltung (englisch Accounts Receivable, kurz FI-AR) ist das Nebenbuch, das alle Forderungen gegenüber Kunden verwaltet. Jeder Vorgang mit einem Kunden — Ausgangsrechnung, Gutschrift, Zahlungseingang, Mahnung — wird hier gebucht und gleichzeitig über ein Abstimmkonto im Hauptbuch mitgeführt.

### Wie wird ein Debitor in SAP S/4HANA angelegt?

Ein Debitor wird nicht mehr als eigenes Objekt angelegt, sondern als Geschäftspartner mit der Rolle „FI Debitor“. Die Daten verteilen sich auf allgemeine Angaben auf Mandantenebene (Anschrift, Bankverbindung) und firmenspezifische Angaben auf Buchungskreisebene (Kontoverwaltung, Zahlungsverkehr, Mahndaten).

### Was ist ein Abstimmkonto?

Ein Abstimmkonto ist ein Sachkonto im Hauptbuch, auf dem jede Buchung des Debitoren-Nebenbuchs automatisch mitgebucht wird. So bleibt der Saldo aller Debitorenkonten immer identisch mit dem Saldo des Abstimmkontos — die Grundlage für eine konsistente Bilanz.

### Wie funktioniert das Mahnprogramm in SAP?

Das Mahnprogramm wählt überfällige offene Posten aus, bestimmt je Konto die Mahnstufe und erzeugt daraus Mahnungen. Der Ablauf hat vier Schritte: Parameter pflegen, Mahnlauf einplanen, Mahnvorschlag bearbeiten und Mahndruck starten.

### Was ist ein offener Posten in der Debitorenbuchhaltung?

Ein offener Posten ist eine gebuchte Forderung, die noch nicht bezahlt ist. Geht die Zahlung ein, wird der Zahlungseingang gegen die Rechnung ausgeglichen und der Posten gilt als erledigt. Nur unbezahlte offene Posten werden im Mahnlauf berücksichtigt.
