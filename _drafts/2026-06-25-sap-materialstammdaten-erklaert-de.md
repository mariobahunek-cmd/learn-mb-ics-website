---
layout: post
lang: de
title: "Materialstammdaten in SAP einfach erklärt: Sichten, Materialart und Organisationsebenen"
description: "Was Materialstammdaten in SAP sind, wie sie in Sichten aufgebaut sind und welche Rolle Materialart, Werk und Lagerort spielen — verständlich für Anwender erklärt."
slug: sap-materialstammdaten-erklaert
permalink: /blog/de/sap-materialstammdaten-erklaert/
translation_key: post-material-master
date: 2026-07-07
category: "Stammdaten"
keywords: "Materialstammdaten, Material Master, SAP MM, Sichten, Materialart, Werk, Lagerort, Stammdaten, SAP S/4HANA"
reading_time: 7
sources:
  - label: "SAP Help Portal — Material Master (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Materials Management — allgemeine Grundlagen zum Materialstamm; vor produktivem Einsatz aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen Stammdaten und Bewegungsdaten?"
    a: "Stammdaten sind dauerhaft gepflegte Basisinformationen wie der Materialstamm, auf die sich Prozesse immer wieder beziehen. Bewegungsdaten sind einzelne Vorgänge wie Bestellungen, Lieferungen oder Rechnungen, die auf diesen Stammdaten aufsetzen."
  - q: "Warum ist der Materialstamm in Sichten aufgeteilt?"
    a: "Weil verschiedene Fachbereiche unterschiedliche Informationen zum selben Material brauchen. Jede Sicht bündelt genau die Felder eines Bereichs, sodass Einkauf, Vertrieb, Lager und Buchhaltung nur das pflegen, was für sie relevant ist."
  - q: "Kann dasselbe Material in zwei Werken unterschiedlich sein?"
    a: "Ja. Viele Daten sind werkspezifisch, etwa Bewertung oder Disposition. Dieselbe Materialnummer kann daher in Werk A anders bewertet oder anders disponiert werden als in Werk B, obwohl es fachlich dasselbe Material ist."
  - q: "Warum lässt sich ein Material in einem Prozess nicht verwenden?"
    a: "Häufig fehlt die passende Sicht. Ohne Einkaufssicht kannst du das Material nicht bestellen, ohne Buchhaltungssicht keine Wertbewegungen buchen. Fehlt eine Sicht für das jeweilige Werk, meldet SAP das Material dort als nicht angelegt."
---

Wer mit SAP arbeitet, stößt früher oder später auf einen Begriff, der praktisch überall auftaucht: die **Materialstammdaten**. Sie sind das Herzstück fast aller logistischen und kaufmännischen Abläufe im System. Ob Einkauf, Vertrieb, Lager oder Buchhaltung — ohne saubere Materialstammdaten läuft in SAP wenig rund. Dieser Artikel erklärt in klarer Sprache, was dahintersteckt.

## Kurz gesagt: das zentrale Datenobjekt für jedes Material

Materialstammdaten beschreiben alles, was ein Unternehmen einkauft, lagert, produziert oder verkauft — Rohstoffe, Halbfabrikate, Fertigerzeugnisse, Handelsware oder Dienstleistungen. Jedes dieser Materialien bekommt im System einen eigenen **Materialstammsatz** mit einer eindeutigen **Materialnummer**.

Diese Materialnummer ist **mandantenweit eindeutig**: Sie existiert im gesamten System nur einmal und steht damit für genau ein bestimmtes Material. Wenn du eine Bestellung anlegst, eine Ware einlagerst oder einen Kundenauftrag erfasst, greift SAP immer auf diesen Materialstamm zurück. Sind die Daten dort fehlerhaft oder unvollständig, klemmt der ganze Prozess. Deshalb gilt: **Stammdaten sind die Basis für alle Logistikprozesse.**

## Stammdaten gegen Bewegungsdaten

In SAP unterscheidet man zwei große Datentypen:

- **Bewegungsdaten** sind einzelne Vorgänge — Bestellungen, Lieferungen, Rechnungen. Sie entstehen laufend im Tagesgeschäft.
- **Stammdaten** sind die dauerhaft gepflegten, zentralen Informationen, auf die sich diese Vorgänge beziehen.

Der Materialstamm gehört zu den Stammdaten. Er wird einmal sauber angelegt und dann immer wieder verwendet. Genau deshalb lohnt es sich, ihn zu verstehen: Ein Fehler im Stammsatz wirkt sich auf viele nachgelagerte Vorgänge aus.

## Aufbau in Sichten: pro Bereich andere Daten

Weil der Materialstamm von vielen Bereichen genutzt wird, ist er nicht in einem einzigen Datenblock organisiert, sondern in **Sichten** (englisch *Views*). Eine Sicht enthält genau die Daten, die ein bestimmter Fachbereich für seine Arbeit braucht.

Das hat einen klaren Vorteil: Jeder Bereich pflegt nur das, was für ihn relevant ist. Der Einkauf interessiert sich für Bezugsquellen und Bestellabwicklung, der Vertrieb für Verkaufsdaten und Lieferbedingungen, die Buchhaltung für die Bewertung. Diese Trennung sorgt für Übersicht und klare Zuständigkeiten.

Die wichtigsten Sichten im Überblick:

### Grunddaten

Die Grunddaten sind die Basis jedes Materialstamms. Sie gelten **für das gesamte Unternehmen** und enthalten allgemeine Informationen wie Materialkurztext, Basismengeneinheit (etwa Stück, Kilogramm, Liter), Warengruppe sowie Gewichte und Abmessungen. Diese Sicht muss **immer** angelegt werden — ohne Grunddaten existiert kein Material.

### Einkauf

In der Einkaufssicht steht alles, was für den Beschaffungsprozess relevant ist: Einkäufergruppe, Bestellmengeneinheit, Wareneingangsbearbeitungszeit und Steuerungsdaten für Bestellungen. Erst mit dieser Sicht lässt sich das Material überhaupt bestellen.

### Vertrieb

Die Vertriebssichten (oft in mehreren Teilbereichen) enthalten Verkaufsdaten, Versandbedingungen, Steuerklassifikation sowie den Bezug zu Werk und Vertriebsbereich. Erst damit kann das Material in einem Kundenauftrag verwendet werden.

### Lagerung

Die Lagersichten beschreiben, wie und wo das Material gelagert wird — Lagerbedingungen, Temperaturanforderungen, Haltbarkeitsdaten oder Gefahrgutkennzeichen. Sie werden vor allem dann gepflegt, wenn das Material besondere Anforderungen an die Lagerung stellt.

### Buchhaltung

Die Buchhaltungssicht ist das Bindeglied zur Finanzwelt. Hier stehen Bewertungsklasse, Preissteuerung (Standardpreis oder gleitender Durchschnittspreis) und der aktuelle Materialpreis. Ohne diese Sicht kann SAP keine Wertbewegungen für das Material verbuchen — also keine Bestandsbewertung, keine Wareneingangsbuchung und keine Rechnungsprüfung.

### Disposition

Die Dispositionssichten steuern, wie Bedarfe für das Material ermittelt und gedeckt werden: Dispositionsmerkmal, Losgrößenverfahren, Sicherheitsbestand, Meldebestand und Planlieferzeit. Sie sind die Grundlage für die automatische Bedarfsplanung — dieselbe Logik, aus der auch eine [Bestellanforderung](/blog/de/was-ist-eine-bestellanforderung/) automatisch entstehen kann.

## Materialart und Branche: die Weichensteller

Bevor du überhaupt einen Materialstamm anlegen kannst, legst du zwei zentrale Felder fest: die **Materialart** und die **Branche**.

### Die Materialart

Die Materialart bestimmt die grundlegenden Eigenschaften eines Materials. Sie steuert unter anderem, welche Sichten überhaupt angelegt werden dürfen, wie die Materialnummer vergeben wird (intern oder extern), wie das Material bewertet wird und ob Bestände nur mengen- oder auch wertmäßig fortgeschrieben werden (Mengen- und Wertfortschreibung).

Typische Materialarten im SAP-Standard sind zum Beispiel Rohstoffe (wird eingekauft, nicht verkauft), Halbfabrikate (intern produziert, nicht direkt verkauft), Fertigerzeugnisse (intern produziert und verkauft) sowie Handelsware und Dienstleistungen. Im Customizing können Unternehmen zusätzlich eigene Materialarten definieren. Die Wahl der Materialart ist eine Entscheidung mit Tragweite, weil sie viele weitere Eigenschaften vorbestimmt.

### Die Branche

Das Branchenfeld beeinflusst, welche Sichten und Felder im Materialstamm angeboten werden. Eine Branche „Maschinenbau“ zeigt zum Beispiel andere Felder als „Pharma“ oder „Lebensmittel“. Wichtig: Die Branche wird beim erstmaligen Anlegen festgelegt und lässt sich später **nicht mehr ändern**. Wer das übersieht, steht im Zweifel vor einer mühsamen Neuanlage.

## So entsteht ein Materialstamm

Das Anlegen eines Materials folgt in SAP einer festen Logik. Vereinfacht läuft es so:

1. **Materialnummer und Branche festlegen.** Sofern keine interne Nummernvergabe greift, trägst du eine eindeutige Materialnummer ein und wählst Branche und Materialart.
2. **Sichten auswählen.** SAP zeigt eine Liste aller verfügbaren Sichten. Du wählst genau die aus, die du für deinen Prozess brauchst — etwa Grunddaten, Einkauf, Lagerung und Buchhaltung. Tipp: Lege nur die Sichten an, die du wirklich benötigst; weitere kannst du jederzeit ergänzen.
3. **Organisationsebenen pflegen.** SAP fragt nach den passenden Ebenen wie Werk, Lagerort oder Vertriebsbereich.
4. **Daten erfassen.** Jetzt füllst du die Pflichtfelder in jeder Sicht aus — Materialtext, Mengeneinheit, Bewertungsklasse, Preissteuerung und so weiter.
5. **Speichern.** SAP bestätigt die Anlage. Ab sofort kann das Material in den entsprechenden Prozessen verwendet werden.

Ob du dabei die klassische SAP GUI oder eine moderne Fiori-App nutzt, spielt für das Ergebnis keine Rolle — beide Wege schreiben in dieselben Daten.

## Organisationsebenen: Mandant, Werk, Lagerort

Materialstammdaten gibt es nicht nur „global“. Viele Daten sind an **Organisationsebenen** gebunden — also an die Stellen im Unternehmen, an denen das Material tatsächlich verwendet wird.

### Mandantenebene

Auf **Mandantenebene** liegen Daten, die für alle Werke und Lager gelten: Materialnummer, Materialkurztext, Warengruppe, Basismengeneinheit. Diese Daten werden einmal gepflegt und gelten dann unternehmensweit.

### Werksebene

Das **Werk** ist die zentrale Organisationseinheit in der Logistik — Produktionsstätte, Distributionszentrum oder Lagerstandort. Auf Werksebene werden zum Beispiel Bestandsführungs- und Dispositionsdaten, die Materialbewertung, die Bearbeitungszeit für den Wareneingang und die Einkäufergruppe gepflegt. Dadurch kann dasselbe Material in zwei Werken unterschiedlich bewertet oder unterschiedlich disponiert werden.

### Lagerortebene

Innerhalb eines Werks gibt es einen oder mehrere **Lagerorte**. Auf dieser Ebene werden lagerbezogene Daten gepflegt. Wenn du Bestände buchst, geschieht das immer auf der Kombination Werk plus Lagerort.

Diese Logik ist entscheidend: Beim Anlegen und Pflegen ist immer wichtig, **für welche Organisationseinheit** du gerade Daten erfasst.

## Häufige Stolpersteine

- **Sichten verwechseln.** Bewertungsdaten stehen in der Buchhaltungssicht, nicht in den Grunddaten. Wer sie an der falschen Stelle sucht, findet sie nicht.
- **Werks- und Mandantendaten vermischen.** Grunddaten gelten mandantenweit, viele andere Sichten sind werkspezifisch. Es lohnt sich, im Zweifel zu prüfen, auf welcher Ebene ein Feld liegt.
- **Branche nachträglich ändern wollen.** Die Branche ist nach der Anlage fix. Deshalb sollte sie von Anfang an stimmen.
- **Sichten unvollständig anlegen.** Fehlt die Einkaufs- oder Buchhaltungssicht, lässt sich das Material im jeweiligen Prozess nicht nutzen — SAP meldet es dann für das Werk als nicht angelegt.
- **Materialnummer als nicht eindeutig ansehen.** Sie ist mandantenweit eindeutig und kann nicht zweimal vergeben werden — auch nicht in verschiedenen Werken.

## Kurz zusammengefasst

Materialstammdaten sind das zentrale Datenobjekt für jedes Material in SAP und die Grundlage für Einkauf, Vertrieb, Lager, Disposition und Buchhaltung. Wer versteht, wie der Materialstamm in **Sichten** aufgebaut ist, welche Rolle **Materialart** und **Branche** spielen und wie die **Organisationsebenen** Mandant, Werk und Lagerort zusammenhängen, hat einen großen Teil der Logik verstanden, die das System zusammenhält. Stammdaten sind kein lästiges Beiwerk — sie sind der Grund, warum SAP im Alltag rund läuft.

## Häufige Fragen

### Was ist der Unterschied zwischen Stammdaten und Bewegungsdaten?

Stammdaten sind dauerhaft gepflegte Basisinformationen wie der Materialstamm, auf die sich Prozesse immer wieder beziehen. Bewegungsdaten sind einzelne Vorgänge wie Bestellungen, Lieferungen oder Rechnungen, die auf diesen Stammdaten aufsetzen.

### Warum ist der Materialstamm in Sichten aufgeteilt?

Weil verschiedene Fachbereiche unterschiedliche Informationen zum selben Material brauchen. Jede Sicht bündelt genau die Felder eines Bereichs, sodass Einkauf, Vertrieb, Lager und Buchhaltung nur das pflegen, was für sie relevant ist.

### Kann dasselbe Material in zwei Werken unterschiedlich sein?

Ja. Viele Daten sind werkspezifisch, etwa Bewertung oder Disposition. Dieselbe Materialnummer kann daher in Werk A anders bewertet oder anders disponiert werden als in Werk B, obwohl es fachlich dasselbe Material ist.

### Warum lässt sich ein Material in einem Prozess nicht verwenden?

Häufig fehlt die passende Sicht. Ohne Einkaufssicht kannst du das Material nicht bestellen, ohne Buchhaltungssicht keine Wertbewegungen buchen. Fehlt eine Sicht für das jeweilige Werk, meldet SAP das Material dort als nicht angelegt.
