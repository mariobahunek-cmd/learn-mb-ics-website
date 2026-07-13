---
layout: post
lang: de
title: "Lageraufgaben und Lageraufträge in SAP EWM verständlich erklärt"
description: "Lageraufgabe, Lagerauftrag, Lageranforderung: So steuern diese drei Belege in SAP EWM Einlagerung, Kommissionierung und interne Bewegungen — klar erklärt."
slug: ewm-lageraufgaben-und-lagerauftraege
permalink: /blog/de/ewm-lageraufgaben-und-lagerauftraege/
translation_key: post-ewm-warehouse-tasks
date: 2026-07-08
category: "Lager"
keywords: "SAP EWM Lageraufgabe, SAP EWM Lagerauftrag, Lageranforderung, SAP Extended Warehouse Management, Einlagerung, Kommissionierung, Quittierung, Lagerauftragserstellungsregeln"
reading_time: 9
sources:
  - label: "SAP Help Portal — SAP Extended Warehouse Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Extended Warehouse Management — allgemeine Grundlagen zu Lageraufgabe und Lagerauftrag. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen Lageraufgabe und Lagerauftrag?"
    a: "Die Lageraufgabe ist EINE konkrete Bewegung — etwa „bewege Palette X von Lagerplatz A nach Lagerplatz B“. Der Lagerauftrag bündelt mehrere Lageraufgaben zu einem Arbeitspaket, das ein Mitarbeiter in einem Zug abarbeitet. Kurz: die Lageraufgabe ist der einzelne Befehl, der Lagerauftrag die Zusammenstellung mehrerer Befehle."
  - q: "Was ist eine Lageranforderung in SAP EWM?"
    a: "Die Lageranforderung ist der Ausgangsbeleg, der eine Lageraktivität auslöst — beim Wareneingang meist der Anlieferbeleg, beim Warenausgang der Auslieferungsauftrag. Auf ihrer Grundlage werden die eigentlichen Lageraufgaben erzeugt, die dann die physische Bewegung ausführen."
  - q: "Was bedeutet Quittierung einer Lageraufgabe?"
    a: "Quittieren heißt bestätigen. Nachdem die Lageraufgabe ausgeführt ist, meldet der Mitarbeiter zurück, dass das richtige Produkt in der korrekten Menge am richtigen Nachlagerplatz angekommen ist. Erst mit der Quittierung gilt die Bewegung als abgeschlossen und der Bestand wird entsprechend fortgeschrieben."
  - q: "Wozu dienen Lagerauftragserstellungsregeln (LAER)?"
    a: "Die Lagerauftragserstellungsregeln legen im Customizing fest, welche und wie viele Lageraufgaben zu einem Lagerauftrag zusammengefasst werden. Über Filter, Grenzwerte, Sortier- und Konsolidierungsregeln steuern sie so die Arbeitslast und den Weg der Mitarbeiter durch das Lager."
---

Zwei Belege im SAP Extended Warehouse Management (EWM) sorgen bei Einsteigern zuverlässig für Verwechslung: die Lageraufgabe und der Lagerauftrag. Ein Buchstabe Unterschied im Wort, ein großer Unterschied in der Sache. Die Lageraufgabe ist ein einzelner Bewegungsbefehl, der Lagerauftrag ein ganzes Bündel davon. Wer das einmal sauber trennt, durchschaut fast jeden EWM-Lagerprozess. Dahinter steht eine Hierarchie aus drei Stufen: Lageranforderung, Lageraufgabe, Lagerauftrag.

## Worum es geht

In SAP EWM wird jede physische Bewegung (Einlagern, Kommissionieren, Umlagern) von drei Belegen getragen, die aufeinander aufbauen. Die **Lageranforderung** ist der Auslöser (etwa eine Anlieferung). Die **Lageraufgabe** ist der konkrete Befehl an den Lagerarbeiter, was er tun soll. Der **Lagerauftrag** bündelt mehrere Lageraufgaben zu einem Arbeitspaket. Wer diese drei Ebenen auseinanderhält, versteht den Materialfluss im Lager.

## Das große Bild: die Drei-Stufen-Hierarchie

Das Zusammenspiel der drei Belege lässt sich in einer klaren Reihenfolge lesen:

1. **Lageranforderung** — der Ausgangsbeleg, oft eine Anlieferung (Wareneingang) oder ein Auslieferungsauftrag (Warenausgang)
2. **Lageraufgabe** — der konkrete Befehl an den Lagerarbeiter, was er physisch tun soll
3. **Lagerauftrag** — die Bündelung mehrerer Lageraufgaben zu einem Arbeitspaket

Eine Lageranforderung ermöglicht die Verarbeitung von Lageraktivitäten. Diese Aktivitäten werden über Lageraufgaben ausgeführt, die einen Bezug zur zugehörigen Lageranforderung haben. Im Lagerverwaltungsmonitor lassen sich alle Folgebelege einer Lageranforderung anzeigen und überwachen — von der Anforderung bis zur letzten quittierten Bewegung.

## Schritt 1 — Die Lageranforderung

Eine Lageranforderung ist der Ausgangsbeleg für eine Lageraktivität. Typische Aktivitäten, die auf ihr basieren, sind:

- Kommissionierung
- Einlagerung
- Umbuchungen
- lagerinterne Umlagerungen
- Verschrottung

Im Wareneingangsprozess ist die Lageranforderung der **Anlieferbeleg**. Man spricht hier synonym von der Lageranforderung — alle Folgeaktionen im Lager beziehen sich auf diesen einen Beleg.

### Wie kommt die Anlieferung ins EWM?

Die Anlieferung entsteht nicht im luftleeren Raum. Sie beginnt im ERP-System mit einer Bestellung und wandert über eine Vorankündigung ins EWM:

- **ERP:** Bestellung/Auftrag → Anlieferung
- **EWM:** Anlieferungsbenachrichtigung → Anlieferung

Die ERP-Anlieferung wird zunächst als **Anlieferungsbenachrichtigung** ins EWM kopiert — eine Art Vorankündigung: „Diese Ware ist unterwegs.“ Sobald die Ware physisch eintrifft, wird aus der Benachrichtigung der echte **Anlieferbeleg** im EWM.

Ein Detail, das den Kreislauf schließt: **alle Änderungen am Anlieferbeleg werden an das ERP-System zurückgemeldet.** Der abgeschlossene Anlieferbeleg bildet die Grundlage für die Wareneingangsbuchung im ERP. So bleiben Lager und Buchhaltung synchron.

## Schritt 2 — Die Lageraufgabe

Mithilfe von Lageraufgaben werden **Warenbewegungen im Lager ausgeführt**. Das kann eine physische Bewegung sein oder nur eine reine Bestandsänderung im System.

Lageraufgaben werden unter anderem benötigt für:

- Kommissionierung
- Einlagerung
- interne Bewegungen
- Umbuchungen
- Wareneingangsbuchungen
- Warenausgangsbuchungen

### Was ist eine Lageraufgabe konkret?

Die Lageraufgabe ist ein **Beleg, der den Lagerarbeiter über eine konkrete Aufgabe informiert** — zum Beispiel: „Bewege drei Paletten von Produkt Y zu Lagerplatz ABC.“ Sie ist der eigentliche Arbeitsauftrag auf der untersten, ausführbaren Ebene.

In einem Einlagerungs- oder Kommissionierprozess sowie bei Umbuchungen ist die Grundlage für die Lageraufgabe die Lageranforderung. Angelegt wird sie pro Lageranforderungsposition, entweder manuell oder automatisch; die automatische Erzeugung übernimmt das Post Processing Framework (PPF), ein Steuerungsrahmen für nachgelagerte Aktionen. Für spontane Bewegungen im Lager, etwa eine Palette von einem Platz zum anderen, lässt sich eine Lageraufgabe auch ganz ohne Referenzbeleg anlegen.

### Quittierung — der zweite Schritt

Ist die Lageraufgabe ausgeführt, muss sie **quittiert** werden. Quittieren heißt bestätigen: Der Lagerarbeiter meldet zurück, dass das richtige Produkt in der korrekten Menge am richtigen Nachlagerplatz eingegangen ist. Erst damit ist die Bewegung abgeschlossen.

Ob eine Quittierung nötig ist, steuern Einstellungen im Von- und Nachlagertyp. In der Lagerprozessart lässt sich zudem festlegen, dass die Quittierung automatisch schon mit dem Anlegen der Lageraufgabe erfolgt. Sinnvoll ist das bei einfachen, fehlerresistenten Bewegungen, bei denen keine zusätzliche Bestätigung durch einen Menschen nötig ist.

### Produkt- und HU-Lageraufgabe

Es gibt zwei Arten von Lageraufgaben, je nachdem, was bewegt wird:

- **Produkt-Lageraufgabe** — wenn ein Produkt in einem einzigen Schritt vom Wareneingangsplatz zum endgültigen Nachlagerplatz bewegt wird. Sie enthält die nötigen Angaben: Lagerprozessart, Von-Lagerplatz und Nach-Lagerplatz.
- **HU-Lageraufgabe** — für komplexere Bewegungen, bei denen die Ware zum Beispiel an einem Verpackungsarbeitsplatz umgepackt wird, bevor sie ans Ziel geht. „HU“ steht für Handling Unit, also eine verpackte Einheit wie eine Palette oder Kiste. Die HU-Lageraufgabe enthält dieselben Felder wie die Produkt-Lageraufgabe, wird aber für verpackte Ware und mehrstufige Bewegungen verwendet.

## Schritt 3 — Der Lagerauftrag

Jetzt kommt der Begriff, der so oft mit der Lageraufgabe verwechselt wird.

Mehrere Lageraufgaben werden **zu einem Lagerauftrag zusammengefasst**. Der Lagerauftrag ist ein **Arbeitspaket**, das ein Mitarbeiter innerhalb eines bestimmten Zeitraums bearbeitet. Er enthält eine oder mehrere Lageraufgaben oder Inventurpositionen.

Anders gesagt: Die **Lageraufgabe** ist EINE konkrete Bewegung („bewege Palette X von Lagerplatz A nach Lagerplatz B“). Der **Lagerauftrag** bündelt MEHRERE Lageraufgaben zu einer sinnvollen Arbeitsabfolge für einen Mitarbeiter (etwa „bewege diese fünf Paletten in einem Rutsch“). Die Bündelung dient dazu, die Arbeitslast der Lagerressourcen zu steuern.

### Warum ist die Bündelung wichtig?

Lageraufgaben entstehen laufend — immer wenn Produkte ein- oder ausgehen, bewegt oder gezählt werden. Ohne Bündelung müsste ein Mitarbeiter sie einzeln und in beliebiger Reihenfolge abarbeiten. SAP EWM fasst deshalb mehrere Lageraufgaben zu Lageraufträgen zusammen, nach festgelegten Regeln.

Ein anschauliches Beispiel: Bei einer großen Anlieferung mit 50 Paletten würde ein einzelner Lagerarbeiter sonst 50 lose Lageraufgaben vor sich haben. Mit dem Lagerauftrag bündelt SAP EWM etwa zehn Paletten zu einer Einheit, sodass der Mitarbeiter eine sinnvolle, überschaubare Arbeitsmenge erhält und effizient durch das Lager läuft.

## Lagerauftragserstellungsregeln (LAER)

Wie SAP EWM entscheidet, welche Lageraufgaben gebündelt werden, regeln die **Lagerauftragserstellungsregeln** (kurz LAER). Sie werden im Customizing definiert, also in der Systemkonfiguration, die ein Berater einrichtet.

Lageraufträge werden in vier Schritten erstellt:

1. Lageraufgaben werden entsprechend dem **Aktivitätsbereich** zusammengefasst und mit vordefinierten Regeln sortiert. Ein Aktivitätsbereich fasst mehrere Lagerplätze zu einer Arbeitszone zusammen.
2. Pro Aktivitätsbereich werden **eine oder mehrere LAER** definiert.
3. Die LAER werden nacheinander abgearbeitet, bis jede Lageraufgabe einem Lagerauftrag zugewiesen ist. Filter und Grenzwerte greifen je nach Konfiguration.
4. Passt keine Regel, greift eine **von SAP bereitgestellte Standardregel**, damit keine Lageraufgabe übrig bleibt.

### Drei zentrale Steuerelemente

- **Filter und Grenzwerte** — bestimmen, welche und wie viele Lageraufgaben in einem Lagerauftrag gruppiert werden.
- **Sortierregeln** — sobald eine LAER angewendet wird, werden die Lageraufgaben nach der Sortierregel geordnet. Typische Kriterien sind Gang, Säule und Ebene des Lagerplatzes — so läuft der Mitarbeiter einen sinnvollen Weg statt kreuz und quer.
- **Konsolidierungsgruppen** — legen fest, welche Lageraufgaben zusammen verpackt oder verarbeitet werden dürfen.

### Restbearbeitungs- und Standardregeln

Damit eine Lageraufgabe verarbeitet werden kann, muss sie **einem Lagerauftrag zugeordnet sein**. Bleiben nach allen definierten LAER noch Aufgaben übrig, greifen zwei Auffangmechanismen:

- **Restbearbeitungsregeln** — erzeugen Lageraufträge für die verbleibenden Aufgaben, gruppiert pro Aktivitätsbereich, Queue und Konsolidierungsgruppe.
- **Standardregeln** — gruppieren pro Aktivitätsbereich, Queue und Lieferung. Sie greifen, wenn für einen Aktivitätsbereich gar keine eigene LAER definiert wurde.

## Ein Beispiel: der Wareneingangsprozess von Anfang bis Ende

So spielen alle drei Belege in einem vollständigen Wareneingangs-Workflow zusammen:

1. **ERP:** Der Einkauf legt eine Bestellung an.
2. **ERP:** Der Lieferant kündigt die Lieferung an → das ERP erzeugt eine Anlieferung.
3. **EWM:** Die ERP-Anlieferung wird als **Anlieferungsbenachrichtigung** ins EWM kopiert.
4. **EWM:** Bei physischem Wareneingang entsteht der EWM-**Anlieferbeleg** (die Lageranforderung).
5. **EWM:** SAP EWM erzeugt automatisch eine **Lageraufgabe** für die Einlagerung — vom Wareneingangsbereich am Tor zum endgültigen Nachlagerplatz.
6. **EWM:** Mehrere Lageraufgaben werden gemäß LAER zu einem **Lagerauftrag** gebündelt.
7. **Lagermitarbeiter:** bearbeitet den Lagerauftrag, führt die einzelnen Lageraufgaben aus und **quittiert** sie nach Ausführung.
8. **EWM:** Die Wareneingangsbuchung wird ausgelöst — der Bestand wechselt vom Wareneingangs- in den frei verfügbaren Bereich.
9. **ERP:** Die Buchung wird an das ERP zurückgemeldet, Bestand und Buchhaltung werden dort fortgeschrieben.

Der Hintergrund der zwei Bereiche: Solange sich der Bestand im Einlagerungsprozess befindet, gilt er noch als „im Wareneingang“ und ist nicht frei verfügbar. Erst am endgültigen Nachlagerplatz wird er als verfügbar geführt. So erkennt die Bestandsführung sofort, ob eine Menge schon verkaufsbereit ist oder noch im Zulauf steckt.

## Warum ein Lieferavis den Wareneingang erzwingen kann

Beim Anlegen der Bestellung wird festgelegt, ob vom Lieferanten ein Lieferavis (eine Lieferankündigung) erwartet wird. Dazu dient ein **Bestätigungssteuerschlüssel** auf Positionsebene. Er kann auch im Versand-Customizing, im Einkaufsinfosatz oder in den Lieferantenstammdaten vordefiniert sein.

Die praktische Konsequenz: Ist dieser Schlüssel gesetzt, muss zuerst eine Anlieferung angelegt werden, bevor der Wareneingang gebucht werden kann. Ohne Anlieferung lässt das System keinen Wareneingang zu — eine häufige Fehlerquelle in der Praxis, wenn ein Wareneingang scheinbar grundlos blockiert.

## Was Anwender im Alltag konkret tun

Als Lagerist arbeitest du im Tagesgeschäft vor allem mit dem **Lagerauftrag**, deinem Arbeitspaket für die nächste Stunde. Der typische Ablauf am mobilen Scanner:

- **Am Gerät anmelden** — ein Lagerauftrag wird dir zugewiesen.
- **Erste Lageraufgabe** erscheint: „Hole Palette X aus dem Quellbereich, bring sie zum Zielbereich.“
- **Quittieren** — Produkt, Menge und Platz bestätigen.
- **Nächste Lageraufgabe** im selben Lagerauftrag → bis der Auftrag abgeschlossen ist.

Als Disponent oder Lagerleiter arbeitest du eher mit den **Lagerauftragserstellungsregeln** — das ist Konfigurationsarbeit, kein Tagesgeschäft. Aber das Verständnis der LAER-Logik hilft, ungleichmäßige Auslastung oder Engpässe im Lager zu erkennen und gezielt gegenzusteuern.

## Zum Mitnehmen

Drei Belege tragen jede Bewegung in SAP EWM: Die **Lageranforderung** löst eine Aktivität aus, die **Lageraufgabe** ist der einzelne, ausführbare Befehl, und der **Lagerauftrag** bündelt mehrere Lageraufgaben zu einem Arbeitspaket. Die Quittierung schließt jede Bewegung ab, und die Lagerauftragserstellungsregeln steuern, wie klug die Arbeit gebündelt wird. Wer Anforderung, Aufgabe und Auftrag sauber auseinanderhält, versteht den Materialfluss im Lager — vom Tor bis zum Regal.

## Häufige Fragen

### Was ist der Unterschied zwischen Lageraufgabe und Lagerauftrag?

Die Lageraufgabe ist EINE konkrete Bewegung — etwa „bewege Palette X von Lagerplatz A nach Lagerplatz B“. Der Lagerauftrag bündelt mehrere Lageraufgaben zu einem Arbeitspaket, das ein Mitarbeiter in einem Zug abarbeitet. Kurz: die Lageraufgabe ist der einzelne Befehl, der Lagerauftrag die Zusammenstellung mehrerer Befehle.

### Was ist eine Lageranforderung in SAP EWM?

Die Lageranforderung ist der Ausgangsbeleg, der eine Lageraktivität auslöst — beim Wareneingang meist der Anlieferbeleg, beim Warenausgang der Auslieferungsauftrag. Auf ihrer Grundlage werden die eigentlichen Lageraufgaben erzeugt, die dann die physische Bewegung ausführen.

### Was bedeutet Quittierung einer Lageraufgabe?

Quittieren heißt bestätigen. Nachdem die Lageraufgabe ausgeführt ist, meldet der Mitarbeiter zurück, dass das richtige Produkt in der korrekten Menge am richtigen Nachlagerplatz angekommen ist. Erst mit der Quittierung gilt die Bewegung als abgeschlossen und der Bestand wird entsprechend fortgeschrieben.

### Wozu dienen Lagerauftragserstellungsregeln (LAER)?

Die Lagerauftragserstellungsregeln legen im Customizing fest, welche und wie viele Lageraufgaben zu einem Lagerauftrag zusammengefasst werden. Über Filter, Grenzwerte, Sortier- und Konsolidierungsregeln steuern sie so die Arbeitslast und den Weg der Mitarbeiter durch das Lager.
