---
layout: post
lang: de
title: "Wareneingang und Warenausgang in SAP EWM verständlich erklärt"
description: "Wie Waren in SAP EWM ins Lager kommen und es wieder verlassen: Anlieferung, Einlagerung, Kommissionierung, Verpacken und Warenausgang — Schritt für Schritt aus Anwendersicht."
slug: ewm-wareneingang-warenausgang
permalink: /blog/de/ewm-wareneingang-warenausgang/
translation_key: post-ewm-wareneingang-warenausgang
date: 2026-07-07
category: "Lager"
keywords: "SAP EWM, Wareneingang, Warenausgang, Extended Warehouse Management, Einlagerung, Kommissionierung, Lageraufgabe, Lagerauftrag, Anlieferung"
reading_time: 8
sources:
  - label: "SAP Help Portal — Extended Warehouse Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Extended Warehouse Management — allgemeine Grundlagen zu Wareneingang und Warenausgang. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen einer Lageraufgabe und einem Lagerauftrag?"
    a: "Die Lageraufgabe ist der einzelne Bewegungsbefehl — zum Beispiel „bringe Produkt X vom Platz A nach Platz B“. Der Lagerauftrag bündelt eine oder mehrere Lageraufgaben zu einem Arbeitspaket, das ein Mitarbeiter am Stück abarbeitet. Kurz: Lageraufgabe = was tun, Lagerauftrag = welches Arbeitspaket."
  - q: "Wo wird die Bestellung angelegt — in ERP oder in EWM?"
    a: "Die Bestellung entsteht im ERP-System, nicht in SAP EWM. EWM übernimmt den Prozess erst, wenn daraus eine Anlieferung wird und diese ins Lager weitergereicht wird."
  - q: "Was bedeutet Quittieren einer Lageraufgabe?"
    a: "Mit dem Quittieren bestätigt der Lagermitarbeiter, dass die Bewegung tatsächlich ausgeführt wurde — richtiges Produkt, korrekte Menge, richtiger Lagerplatz. Erst nach der Quittierung gilt die Aufgabe im System als erledigt."
  - q: "Warum bleibt ein Wareneingang manchmal „hängen“?"
    a: "Häufig ist die zugehörige Lageraufgabe noch nicht quittiert, oder die Ware liegt noch im Wareneingangsbereich und wurde noch nicht auf den endgültigen Lagerplatz eingelagert. Solange die Einlagerung nicht abgeschlossen ist, gilt der Bestand als noch nicht voll verfügbar."
  - q: "Was ist ein Quant in SAP EWM?"
    a: "Als Quant bezeichnet man den Bestand einer bestimmten Ware auf einem konkreten Lagerplatz. Es ist die feinste Einheit, mit der EWM verfolgt, was wo und in welcher Menge liegt."
---

In jedem Lager passiert im Kern immer dasselbe: Waren kommen rein, werden verstaut, später wieder herausgeholt, verpackt und verlassen das Lager. In SAP Extended Warehouse Management (EWM) heißen diese beiden Richtungen **Wareneingang** und **Warenausgang**. Wer sie einmal als zusammenhängende Geschichte verstanden hat, versteht damit fast das ganze operative Tagesgeschäft eines EWM-Lagers. Dieser Artikel geht beide Prozesse Schritt für Schritt durch — rein aus Anwendersicht, ohne Customizing.

## Kurz gesagt: rein ins Lager, raus aus dem Lager

Wareneingang und Warenausgang folgen in SAP EWM derselben Grundlogik. Am Anfang steht ein **auslösender Beleg** aus dem ERP-System — eine Bestellung beim Wareneingang, ein Kundenauftrag beim Warenausgang. Daraus entsteht ein **Lagerbeleg in EWM** (die Anlieferung oder der Auslieferungsauftrag), und dieser steuert die **physische Bewegung im Lager** über Lageraufgaben und Lageraufträge.

Der Unterschied ist nur die Richtung:

- **Wareneingang:** Bewegung *in* das Lager hinein. Start ist der Wareneingangsbereich, Ziel ist ein Lagerplatz.
- **Warenausgang:** Bewegung *aus* dem Lager heraus. Start ist der Lagerplatz, Ziel ist der Warenausgangsbereich (die Bereitstellungszone).

Beide arbeiten mit denselben Werkzeugen: Anlieferung beziehungsweise Auslieferungsauftrag, Lageraufgabe, Lagerauftrag und Quittierung. Wer diese Begriffe einmal verstanden hat, deckt damit beide Richtungen ab.

## Der Wareneingang: Bestellung, Anlieferung, Einlagerung

Der Wareneingangsprozess beginnt nicht in EWM, sondern im **ERP-System mit einer Bestellung**. Sobald der Lieferant seine Lieferung ankündigt (zum Beispiel per Lieferavis), entsteht daraus eine **Anlieferung** im ERP.

Diese ERP-Anlieferung wird an SAP EWM übergeben und dort zur **Anlieferung in EWM** — dem eigentlichen Ausführungsbeleg, mit dem im Lager gearbeitet wird. Vereinfacht läuft die Kette so:

1. **Bestellung** im ERP-System
2. **Anlieferung** im ERP-System (manuell oder automatisch über das Lieferavis)
3. **Anlieferungsbenachrichtigung** in EWM — ein Zwischenbeleg, der in neueren, eingebetteten EWM-Varianten auch übersprungen werden kann
4. **Anlieferung in EWM** — der Beleg, an dem die Lagerarbeit hängt

Wichtig für das Verständnis: Änderungen am EWM-Anlieferbeleg werden **zurück an ERP gemeldet**. Ist die Ausführung im Lager abgeschlossen, bildet der Beleg die Basis für die Wareneingangsmeldung im ERP. So bleiben Lager und ERP-Bestandsführung synchron.

### Zwei Lagerorte im Wareneingang

Ein typisches Muster: SAP EWM kann den Wareneingang über **zwei Lagerorte** abbilden. Solange sich der Bestand noch im Einlagerungsprozess befindet, ist er einem Wareneingangs-Lagerort zugeordnet. Erst wenn die Ware am endgültigen Lagerplatz angekommen ist, wird sie auf den Lagerort „verfügbar" umgebucht.

Der Vorteil: Die ERP-Bestandsführung sieht den Bestand zwar bereits, macht aber sichtbar, dass er aus Lagersicht *noch nicht voll verfügbar* ist. Das verhindert, dass Ware verplant wird, die physisch noch am Tor steht.

## Wohin mit der Ware? Die Einlagerung (Putaway)

Sobald die Anlieferung in EWM steht, muss das System entscheiden, **auf welchen Lagerplatz** die Ware kommt. Das ist die **Einlagerung**, oft mit dem englischen Begriff *Putaway* bezeichnet.

Dazu erzeugt die Anlieferung eine **Lageraufgabe für die Einlagerung**. Diese Lageraufgabe enthält das **Ziel** — also Lagertyp, Lagerbereich und Lagerplatz. Welcher Platz vorgeschlagen wird, steuert das System über hinterlegte Regeln, die unter anderem Folgendes berücksichtigen:

- Eigenschaften des Produkts (zum Beispiel Charge, Serialnummer oder Gefahrgut)
- Art der Verpackung (verpackt oder unverpackt)
- den Aktivitätsbereich im Lager

Als Anwender musst du diese Regeln nicht selbst pflegen. Wichtig ist das Prinzip: Aus der Anlieferung entsteht eine Lageraufgabe, und diese sagt dem Mitarbeiter genau, wohin die Ware soll.

## Der Warenausgang: Auftrag, Kommissionieren, Verpacken, Versand

Der Warenausgangsprozess startet typischerweise mit einem **Kundenauftrag** im ERP-System (auch eine Umlagerung ist möglich). Aus dem Kundenauftrag wird eine **Auslieferung** im ERP, und sobald diese ein EWM-geführtes Lager betrifft, wird sie an EWM weitergereicht:

1. **Kundenauftrag** im ERP
2. **Auslieferung** im ERP
3. **Auslieferungsanforderung** in EWM (Zwischenbeleg)
4. **Auslieferungsauftrag** in EWM — der zentrale Beleg für den Warenausgang
5. **Auslieferung in EWM** am Ende, nach der Warenausgangsbuchung

Beim Anlegen des Auslieferungsauftrags läuft im Hintergrund einiges ab: Das System ermittelt unter anderem den passenden Lagerplatz, aus dem entnommen wird, sowie Tor und Bereitstellungszone. Danach kann die eigentliche Arbeit im Lager beginnen.

### Kommissionieren (Picking)

Beim **Kommissionieren** wird die Ware vom Lagerplatz geholt und in den Warenausgangsbereich gebracht. Auch hier steuert eine **Lageraufgabe** die Bewegung — diesmal für die Kommissionierung. Sie enthält die **Quelle** (Lagertyp und Lagerplatz) und das **Ziel** (die Bereitstellungszone).

Für den Mitarbeiter ist das ein klares Arbeitspaket: „Hole Produkt X in Menge Y vom Lagerplatz Z und bringe es in die Bereitstellungszone." Nach der Ausführung wird die Aufgabe quittiert.

### Verpacken (Packing)

Das **Verpacken** kann auf verschiedenen Stufen erfolgen. SAP EWM kann dabei mit **Packspezifikationen** arbeiten, die festlegen, wie ein Produkt verpackt wird — etwa wie viele Einheiten auf eine Palette gehören. Die verpackten Einheiten werden als **Handling Units (HU)** geführt, sodass jederzeit nachvollziehbar bleibt, was sich in welchem Packstück befindet.

### Warenausgang buchen

Sobald die Ware kommissioniert ist und in der Bereitstellungszone steht, folgt die **Warenausgangsbuchung**. Die EWM-Auslieferung meldet diese zurück ans ERP-System, wo automatisch die passenden Bestands- und Finanzbelege entstehen. Damit ist die Ware das Lager verlassen — physisch wie systemseitig.

## Lageraufgabe und Lagerauftrag — was ist der Unterschied?

Diese beiden Begriffe werden am häufigsten verwechselt, dabei ist der Unterschied simpel.

### Lageraufgabe (Warehouse Task)

Die Lageraufgabe ist **der einzelne Bewegungsbefehl**. Sie sagt dem Lagerarbeiter, was konkret zu tun ist, zum Beispiel: „Bewege drei Paletten von Produkt Y zu Lagerplatz ABC." Lageraufgaben braucht es unter anderem für:

- Kommissionierung
- Einlagerung
- interne Bewegungen und Umbuchungen
- Wareneingangs- und Warenausgangsbuchungen

Ist die Aufgabe ausgeführt, muss sie **quittiert** werden. Mit der Quittierung bestätigt der Mitarbeiter: richtiges Produkt, korrekte Menge, richtiger Platz.

### Lagerauftrag (Warehouse Order)

Der Lagerauftrag ist die nächsthöhere Ebene: **ein Arbeitspaket**, das ein Mitarbeiter innerhalb eines bestimmten Zeitraums bearbeitet. Er enthält **eine oder mehrere Lageraufgaben**. Mehrere Einzel-Lageraufgaben werden also zu einem oder mehreren Lageraufträgen gebündelt — nach Regeln, die im Hintergrund definiert sind.

Als Merksatz: **Lageraufgabe = was tun. Lagerauftrag = welches Arbeitspaket.**

## Die Lagerstruktur: Lagernummer, Lagertyp, Lagerplatz

Damit Wareneingang und Warenausgang funktionieren, hilft ein Blick auf die Struktur eines EWM-Lagers. Sie ist klar hierarchisch aufgebaut:

- **Lagernummer:** die oberste Organisationseinheit, in der Praxis meist ein Gebäude oder ein Distributionszentrum.
- **Lagertyp:** eine physische oder logische Unterteilung — zum Beispiel Hochregal, Wareneingangszone, Warenausgangszone oder Verpackungsbereich.
- **Lagerbereich:** eine feinere Untergliederung innerhalb eines Lagertyps (etwa „schnelldrehend" gegen „langsamdrehend").
- **Lagerplatz:** die **kleinste räumliche Einheit** des Lagers. Hier liegt am Ende der konkrete Bestand.

Der Bestand einer Ware auf einem Lagerplatz wird **Quant** genannt. Das ist die Einheit, mit der EWM verfolgt, was wo und in welcher Menge liegt.

## Häufige Stolpersteine

- **Lageraufgabe und Lagerauftrag verwechseln.** Die Lageraufgabe ist der einzelne Befehl, der Lagerauftrag das größere Arbeitspaket, das mehrere Aufgaben bündelt.
- **Anlieferungsbenachrichtigung mit Anlieferung gleichsetzen.** Die Benachrichtigung ist der Zwischenbeleg in EWM; die Anlieferung in EWM ist der eigentliche Ausführungsbeleg, mit dem gearbeitet wird.
- **Quittierung vergessen.** Eine ausgeführte Bewegung ist erst dann im System erledigt, wenn sie quittiert wurde.
- **Bestellung im falschen System suchen.** Die Bestellung wird im ERP angelegt, nicht in EWM. EWM beginnt erst bei der Anlieferung.
- **ERP- und EWM-Stammdaten gleichsetzen.** Zwischen beiden gibt es eine Übertragung, aber die Datenmodelle sind nicht identisch — der Lagerbezug in EWM ist eigenständig.

## Kurz zusammengefasst

Wareneingang und Warenausgang sind in SAP EWM zwei Richtungen derselben Grundlogik: Ein Beleg aus dem ERP-System stößt den Prozess an, in EWM entsteht daraus ein Lagerbeleg, und dieser steuert über Lageraufgaben und Lageraufträge die physische Bewegung — hinein ins Lager beim Wareneingang, hinaus beim Warenausgang. Wer sich diese beiden Wege als durchgehende Geschichte merkt — Bestellung, Anlieferung, Einlagerung auf der einen Seite; Auftrag, Kommissionieren, Verpacken, Warenausgang auf der anderen — versteht den operativen Kern eines EWM-Lagers.

## Häufige Fragen

### Was ist der Unterschied zwischen einer Lageraufgabe und einem Lagerauftrag?

Die Lageraufgabe ist der einzelne Bewegungsbefehl — zum Beispiel „bringe Produkt X vom Platz A nach Platz B“. Der Lagerauftrag bündelt eine oder mehrere Lageraufgaben zu einem Arbeitspaket, das ein Mitarbeiter am Stück abarbeitet. Kurz: Lageraufgabe = was tun, Lagerauftrag = welches Arbeitspaket.

### Wo wird die Bestellung angelegt — in ERP oder in EWM?

Die Bestellung entsteht im ERP-System, nicht in SAP EWM. EWM übernimmt den Prozess erst, wenn daraus eine Anlieferung wird und diese ins Lager weitergereicht wird.

### Was bedeutet Quittieren einer Lageraufgabe?

Mit dem Quittieren bestätigt der Lagermitarbeiter, dass die Bewegung tatsächlich ausgeführt wurde — richtiges Produkt, korrekte Menge, richtiger Lagerplatz. Erst nach der Quittierung gilt die Aufgabe im System als erledigt.

### Warum bleibt ein Wareneingang manchmal „hängen“?

Häufig ist die zugehörige Lageraufgabe noch nicht quittiert, oder die Ware liegt noch im Wareneingangsbereich und wurde noch nicht auf den endgültigen Lagerplatz eingelagert. Solange die Einlagerung nicht abgeschlossen ist, gilt der Bestand als noch nicht voll verfügbar.

### Was ist ein Quant in SAP EWM?

Als Quant bezeichnet man den Bestand einer bestimmten Ware auf einem konkreten Lagerplatz. Es ist die feinste Einheit, mit der EWM verfolgt, was wo und in welcher Menge liegt.
