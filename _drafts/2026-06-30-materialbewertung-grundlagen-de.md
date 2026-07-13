---
layout: post
lang: de
title: "Materialbewertung in SAP: Standardpreis und gleitender Durchschnittspreis verständlich erklärt"
description: "Wie SAP den Wert deiner Materialien bestimmt: Standardpreis (S) gegen gleitenden Durchschnittspreis (V), Material- und Buchhaltungsbeleg, das WE/RE-Konto und Preisdifferenzen — in klarer Sprache."
slug: materialbewertung-grundlagen
permalink: /blog/de/materialbewertung-grundlagen/
translation_key: post-materialbewertung
date: 2026-07-07
category: "Finanzen"
keywords: "Materialbewertung, Standardpreis, gleitender Durchschnittspreis, Preissteuerung, WE/RE-Konto, Preisdifferenzen, Bestandswert, SAP Buchhaltung"
reading_time: 8
sources:
  - label: "SAP Help Portal — Inventory Valuation / Materials Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Materialwirtschaft und Bestandsbewertung — allgemeine Grundlagen. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen Standardpreis und gleitendem Durchschnittspreis?"
    a: "Der Standardpreis (S) bleibt in der Regel über das Geschäftsjahr konstant; Abweichungen zum Einkaufspreis laufen auf ein Preisdifferenzen-Konto. Der gleitende Durchschnittspreis (V) wird bei jedem Zugang neu als gewichteter Durchschnitt berechnet und passt sich so laufend an."
  - q: "Wo wird die Preissteuerung eines Materials gepflegt?"
    a: "Im Materialstammsatz in der Sicht „Buchhaltung 1“. Dort steht das Kennzeichen S oder V zusammen mit dem aktuellen Bewertungspreis und dem Gesamtbestandswert."
  - q: "Wozu dient das WE/RE-Verrechnungskonto?"
    a: "Es überbrückt die Lücke zwischen Wareneingang und Rechnungseingang. Beim Wareneingang wird es bebucht, bei der Rechnung wieder ausgeglichen. Ein offener Saldo zeigt, dass entweder eine Rechnung oder eine Lieferung noch fehlt."
  - q: "Warum bekommt ein Material plötzlich einen unerwarteten Bestandswert?"
    a: "Meist wegen einer bewertungsrelevanten Buchung — etwa eines Wareneingangs zu einem stark abweichenden Preis oder einer manuellen Umbewertung. Der Blick in den Materialbeleg und den verknüpften Buchhaltungsbeleg zeigt, was passiert ist."
---

„Warum steht bei dem einen Material ein S und bei dem anderen ein V?“ Sobald wir im Materialstamm die Sicht Buchhaltung 1 öffnen, kommt fast reflexartig diese Frage. Dahinter steckt die Materialbewertung: der Mechanismus, der bei jeder Warenbewegung entscheidet, mit welchem Betrag ein Material zu Buche schlägt. Sie verbindet die operative Bestandsführung mit der Finanzbuchhaltung, und wer diese Grundlogik einmal durchschaut hat, versteht auch einen großen Teil dessen, was SAP im Hintergrund bucht.

## Der Wert deines Lagers, laufend automatisch gepflegt

Die Materialbewertung bestimmt, mit welchem *Wert* ein bestandsführendes Material in der Bilanz erscheint. Bei jeder Warenbewegung, ob Wareneingang, Warenausgang oder Umbuchung, erzeugt SAP einen **Materialbeleg**. Ist der Vorgang bewertungsrelevant, kommt automatisch ein **Buchhaltungsbeleg** dazu, der die Sachkonten bebucht. So bleibt der Lagerwert in der Buchhaltung immer synchron mit dem physischen Bestand, ohne dass jemand von Hand rechnet.

## Materialbeleg und Buchhaltungsbeleg: zwei getrennte Welten

Das wichtigste Konzept zuerst: SAP trennt sauber zwischen **Bestand** und **Wert**.

- Der **Materialbeleg** dokumentiert die *physische* Bewegung: Was wurde wann, wie viel, von wo nach wo bewegt?
- Der **Buchhaltungsbeleg** dokumentiert die *wertmäßige* Auswirkung: Welche Sachkonten werden mit welchen Beträgen bebucht?

Beide Belege entstehen gleichzeitig, sind aber eigenständig. Der Materialbeleg wird über Belegnummer und Belegjahr identifiziert, der Buchhaltungsbeleg über Buchungskreis, Belegnummer und Geschäftsjahr.

### Wann ist eine Warenbewegung bewertungsrelevant?

Bewertungsrelevant ist eine Bewegung immer dann, wenn sich der Bestandswert in der Bilanz ändert — also die Finanzbuchhaltung betroffen ist.

- **Bewertungsrelevant:** ein externer Wareneingang (der Bestand steigt, das Umlaufvermögen wächst), ein Warenausgang an einen Kunden, eine Verschrottung oder eine Verbrauchsbuchung auf eine Kostenstelle.
- **Nicht bewertungsrelevant:** eine reine Umlagerung innerhalb desselben Werks, etwa von einem Lagerort in einen anderen. Der Bestand bleibt im selben Buchungskreis, nur die Lokation ändert sich — die Bilanz merkt davon nichts.

Merksatz: Ändert sich der Bestandswert auf Buchungskreisebene, entsteht ein Buchhaltungsbeleg. Wandert der Bestand nur intern von A nach B, nicht.

### Woher kommt der Buchungskreis?

Der Buchungskreis des Buchhaltungsbelegs wird automatisch aus dem Werk abgeleitet, in dem die Warenbewegung stattfindet. Du musst ihn also nicht angeben — das Werk bestimmt, in welcher rechtlichen Einheit gebucht wird.

## Preissteuerung: Standardpreis (S) oder gleitender Durchschnittspreis (V)?

Im Materialstammsatz, in der Sicht *Buchhaltung 1*, steht ein zentrales Steuerfeld: die **Preissteuerung**. Sie kennt genau zwei Ausprägungen, und die Entscheidung dafür prägt das gesamte Bewertungsverhalten des Materials.

- **S — Standardpreis:** Das Material wird mit einem *festen* Preis bewertet, der in der Regel über das Geschäftsjahr konstant bleibt. Weicht der tatsächliche Einkaufspreis davon ab, landet die Differenz auf einem separaten **Preisdifferenzen-Konto**. Der Bestandswert bewegt sich ausschließlich zum Standardpreis.
- **V — Gleitender Durchschnittspreis:** Der Bewertungspreis wird bei jedem bewertungsrelevanten Zugang *neu* berechnet — als gewichteter Durchschnitt aus altem Bestand und neuem Zugang. Preisdifferenzen entstehen dabei normalerweise nicht, weil der Preis immer dem aktuellen Durchschnitt entspricht.

Welche Steuerung wann sinnvoll ist, ist eine bilanzpolitische Entscheidung. Als Faustregel:

| Preissteuerung | Typischer Einsatz |
| --- | --- |
| **S — Standardpreis** | Halbfertig- und Fertigerzeugnisse aus Eigenproduktion, Materialien mit stabilen Einkaufspreisen |
| **V — Gleitender Durchschnitt** | Rohstoffe und Handelswaren mit stark schwankenden Einkaufspreisen |

Der Standardpreis sorgt für stabile, planbare Kosten in der Produktion; der gleitende Durchschnitt bildet reale Marktschwankungen direkt im Bestandswert ab.

## Ein Zahlenbeispiel mit Standardpreis

Am klarsten wird die Logik an einem durchgerechneten Beispiel. Ausgangssituation im Materialstammsatz:

- **Anfangsbestand:** 100 Stück
- **Gesamtwert:** 200,00 €
- **Standardpreis:** 2,00 € pro Stück

Geplant ist ein Wareneingang von 100 Stück zu einem **Bestellpreis von 2,40 €**, gefolgt von einem Rechnungseingang derselben 100 Stück zu einem **Rechnungspreis von 2,20 €**.

### Schritt 1 — Wareneingang buchen

Nach dem Wareneingang stehen im Materialstammsatz:

- **Bestand:** 200 Stück (100 alt + 100 neu)
- **Gesamtwert:** 400,00 € (200 alt + 200 neu, jeweils zum Standardpreis bewertet)
- **Standardpreis:** unverändert 2,00 €

Der Clou: Das Bestandskonto bewegt sich *nur* zum Standardpreis, nie zum Bestellpreis. Die Buchungen im Buchhaltungsbeleg:

- **Bestandskonto:** +200 € (= 100 Stück × 2,00 € Standardpreis)
- **WE/RE-Verrechnungskonto:** +240 € (= 100 Stück × 2,40 € Bestellpreis)
- **Preisdifferenzen (Aufwand):** +40 € (= Differenz 2,40 € − 2,00 € × 100 Stück)

Weil der Bestellpreis über dem Standardpreis liegt, entsteht ein **Aufwand** aus Preisdifferenzen.

### Schritt 2 — Rechnungseingang buchen

Die Rechnung kommt über 100 Stück zu 2,20 € statt der bestellten 2,40 €. Danach:

- **Bestand:** bleibt 200 Stück (die Rechnung ändert keine Menge)
- **Gesamtwert:** bleibt 400,00 €
- **Standardpreis:** bleibt 2,00 €

Im Buchhaltungsbeleg wird das WE/RE-Konto zum Bestellpreis ausgeglichen, der Kreditor zum Rechnungspreis fortgeschrieben und die Differenz auf das Preisdifferenzen-Konto gebucht:

- **WE/RE-Verrechnungskonto:** −240 € (Ausgleich des Wareneingangs)
- **Kreditorenkonto (Lieferant):** +220 € (= 100 × 2,20 € Rechnungspreis)
- **Preisdifferenzen (Ertrag):** +20 € (= Differenz 2,40 € − 2,20 € × 100 Stück)

Weil der Rechnungspreis unter dem Bestellpreis liegt, entsteht hier ein **Ertrag** aus Preisdifferenzen. Beide Richtungen, Aufwand wie Ertrag, sind völlig normal und hängen nur davon ab, ob der tatsächliche Preis über oder unter der Referenz liegt.

## Das WE/RE-Verrechnungskonto: der zentrale Mittler

Das **WE/RE-Verrechnungskonto** (englisch GR/IR account, von *goods receipt / invoice receipt*) ist eines der wichtigsten Konten in der Bewertung. Seine Aufgabe ist es, die zeitliche Lücke zwischen Wareneingang und Rechnungseingang zu überbrücken:

- Beim **Wareneingang** wird Bestellpreis × Menge dort gebucht.
- Beim **Rechnungseingang** wird derselbe Betrag wieder ausgeglichen.
- Ist die Ware da, aber die Rechnung noch nicht, zeigt der offene Saldo die noch nicht abgerechneten Wareneingänge.
- Ist die Rechnung da, aber die Ware noch nicht, zeigt der Saldo (mit umgekehrtem Vorzeichen) die noch nicht eingegangenen Lieferungen.

Das Konto ist bilanzrelevant und gehört zu jedem Periodenabschluss: Es wird analysiert, um zu klären, welche Posten alt und unverrechnet sind und wo noch etwas fehlt. Ein lange offener WE/RE-Saldo ist ein verlässlicher Hinweis auf einen unvollständigen Prozess.

## Wie der Bestellpreis überhaupt entsteht

Ein häufiges Missverständnis: In der Bestellung wird *nicht* der Bewertungspreis aus dem Materialstammsatz vorgeschlagen. Stattdessen sucht SAP den Preis hierarchisch vom Speziellen zum Allgemeinen. Zuerst sieht das System nach einem Einkaufsinfosatz zur Kombination Lieferant/Material auf der Ebene Einkaufsorganisation/Werk. Wird es dort nicht fündig, sucht es eine Stufe höher auf Ebene der Einkaufsorganisation, und erst wenn auch dort keine Daten liegen, muss der Preis manuell eingegeben werden.

Existiert ein Infosatz, haben gültige Konditionen Vorrang. Fehlen diese oder sind sie abgelaufen, liest das System die Nummer des letzten Einkaufsbelegs aus dem Infosatz und schlägt den Preis aus jenem Beleg vor.

Wenn du den vorgelagerten Schritt vertiefen willst, hilft der Artikel [Was ist eine Bestellanforderung in SAP?](/blog/de/was-ist-eine-bestellanforderung/) beim Einstieg in den Beschaffungsablauf.

## Was das für dich im Alltag bedeutet

Die Preissteuerung und die Konfiguration der Bewertungskonten sind Sache des Customizings und der Buchhaltung, nicht des einzelnen Anwenders. Die *Wirkung* siehst du als Einkäufer oder Disponent aber täglich:

- Wenn du einen Wareneingang buchst, laufen die Buchhaltungsbuchungen automatisch: das System rechnet, du musst nichts tun.
- Wenn eine Rechnung mit Abweichung kommt, siehst du im Rechnungsbeleg die Preisdifferenz, die auf das passende Konto gebucht wird.
- Wenn ein Material einen unerwarteten Bestandswert hat, lohnt der Blick in die Materialbeleg-Übersicht und den verknüpften Buchhaltungsbeleg.
- Wenn ein WE/RE-Saldo lange offen bleibt, deutet das auf eine fehlende Rechnung oder Lieferung hin, ein Klassiker für den Periodenabschluss.

## Häufige Stolpersteine

Am ehesten verwechselt werden Standardpreis (S) und gleitender Durchschnittspreis (V) — und damit auch, was die Preissteuerung bei einer Buchung überhaupt bewirkt. Wer die folgenden Punkte im Kopf behält, umgeht die häufigsten Irrtümer.

- **Bestandskonto mit dem Bestellpreis verwechseln.** Beim Standardpreis bewegt sich das Bestandskonto ausschließlich zum Standardpreis. Jede Abweichung landet auf dem Preisdifferenzen-Konto — nicht im Bestandswert.
- **Preisdifferenzen für einen Fehler halten.** Aufwand oder Ertrag aus Preisdifferenzen sind bei Standardpreis-Steuerung völlig normal. Sie zeigen nur, ob der tatsächliche Preis über oder unter dem Standardpreis lag.
- **Den offenen WE/RE-Saldo ignorieren.** Ein Saldo dort bedeutet fast immer, dass ein Prozess halb fertig ist — Ware ohne Rechnung oder Rechnung ohne Ware.

## Worauf es ankommt

Die Materialbewertung sorgt dafür, dass der Wert deines Lagers in der Buchhaltung jederzeit stimmt. Jede bewertungsrelevante Bewegung erzeugt neben dem Materialbeleg einen Buchhaltungsbeleg. Ob ein Material mit festem **Standardpreis (S)** oder mit **gleitendem Durchschnittspreis (V)** geführt wird, entscheidet, wie Preisabweichungen verbucht werden: beim Standardpreis über ein Preisdifferenzen-Konto, beim gleitenden Durchschnitt direkt im Bewertungspreis. Das WE/RE-Verrechnungskonto hält Wareneingang und Rechnung zusammen. Wer diese drei Bausteine verstanden hat, also Bewertungsrelevanz, Preissteuerung und WE/RE-Konto, durchschaut die Bewertungslogik im gesamten SAP-System.

## Häufige Fragen

### Was ist der Unterschied zwischen Standardpreis und gleitendem Durchschnittspreis?

Der Standardpreis (S) bleibt in der Regel über das Geschäftsjahr konstant; Abweichungen zum Einkaufspreis laufen auf ein Preisdifferenzen-Konto. Der gleitende Durchschnittspreis (V) wird bei jedem Zugang neu als gewichteter Durchschnitt berechnet und passt sich so laufend an.

### Wo wird die Preissteuerung eines Materials gepflegt?

Im Materialstammsatz in der Sicht „Buchhaltung 1“. Dort steht das Kennzeichen S oder V zusammen mit dem aktuellen Bewertungspreis und dem Gesamtbestandswert.

### Wozu dient das WE/RE-Verrechnungskonto?

Es überbrückt die Lücke zwischen Wareneingang und Rechnungseingang. Beim Wareneingang wird es bebucht, bei der Rechnung wieder ausgeglichen. Ein offener Saldo zeigt, dass entweder eine Rechnung oder eine Lieferung noch fehlt.

### Warum bekommt ein Material plötzlich einen unerwarteten Bestandswert?

Meist wegen einer bewertungsrelevanten Buchung — etwa eines Wareneingangs zu einem stark abweichenden Preis oder einer manuellen Umbewertung. Der Blick in den Materialbeleg und den verknüpften Buchhaltungsbeleg zeigt, was passiert ist.
