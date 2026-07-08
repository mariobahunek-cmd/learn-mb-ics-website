---
layout: post
lang: de
title: "SAP S/4HANA Embedded Analytics: Auswertungen direkt im Live-System"
description: "Was Embedded Analytics in SAP S/4HANA bedeutet: Reporting in Echtzeit über CDS Views, analytische Fiori-Apps und KPI-Kacheln — klar und praxisnah erklärt."
slug: embedded-analytics-in-s4hana
permalink: /blog/de/embedded-analytics-in-s4hana/
translation_key: post-embedded-analytics
date: 2026-07-08
category: "Grundlagen"
keywords: "SAP Embedded Analytics, SAP S/4HANA, CDS Views, KPI Tiles, analytische Fiori-Apps, Echtzeit-Reporting, HANA In-Memory, SAP Analytics Cloud"
reading_time: 9
sources:
  - label: "SAP Help Portal — SAP S/4HANA Analytics"
    url: "https://help.sap.com/"
    note: "Bereich Analytics / Embedded Analytics — allgemeine Grundlagen. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist Embedded Analytics in SAP S/4HANA?"
    a: "Embedded Analytics bedeutet, dass Auswertungen und Reports direkt im operativen SAP-S/4HANA-System laufen — auf denselben Live-Daten, in Echtzeit, ohne den Umweg über ein separates Business-Intelligence-System. Möglich macht das die HANA In-Memory-Datenbank zusammen mit CDS Views als Datenmodell."
  - q: "Was sind CDS Views?"
    a: "CDS Views (Core Data Services) sind eine Modellierungsschicht, die beschreibt, welche Daten aus welchen Tabellen für eine Auswertung zusammengeführt werden. Sie sind das Datenfundament für nahezu alle analytischen Apps und Reports in S/4HANA. Anwender müssen sie nicht selbst bauen — das ist Aufgabe von Beratern und Entwicklern."
  - q: "Worin unterscheidet sich Embedded Analytics von einem Data Warehouse wie SAP BW?"
    a: "Ein Data Warehouse wie SAP BW extrahiert Daten aus dem ERP und lädt sie in ein zweites System, meist zeitversetzt. Embedded Analytics wertet direkt auf den Originaldaten im S/4HANA aus, in Echtzeit und ohne Replikation. Für große, quellenübergreifende Analysen bleibt ein Data Warehouse trotzdem sinnvoll."
  - q: "Was ist eine dynamische Kachel (KPI Tile)?"
    a: "Eine dynamische Kachel zeigt eine Live-Kennzahl direkt auf der Startseite an — etwa die Anzahl offener Bestellungen oder den Umsatz des Monats. Der Wert aktualisiert sich automatisch, sodass du deine Lage erkennst, ohne die App überhaupt zu öffnen."
  - q: "Brauche ich die SAP Analytics Cloud zusätzlich zu Embedded Analytics?"
    a: "Nicht zwingend. Embedded Analytics deckt operative Auswertungen direkt in S/4HANA ab. Die SAP Analytics Cloud ist eine optionale Cloud-Plattform für weitergehende Aufgaben wie unternehmensweite Dashboards, Planung und Predictive Analytics über mehrere Datenquellen hinweg."
---

Auswerten und arbeiten sind in SAP S/4HANA nicht mehr zwei getrennte Welten. Wer eine Bestellung anlegt, eine Rechnung bucht oder einen Auftrag bearbeitet, kann dieselben Daten im selben System sofort auswerten — in Echtzeit, ohne Umweg über ein separates Reporting-Tool. Genau dafür steht der Begriff Embedded Analytics. Dieser Artikel erklärt in klarer Sprache, was dahintersteckt und wie die einzelnen Bausteine zusammenspielen.

## Kurz gesagt: Reporting direkt im laufenden System

Embedded Analytics bedeutet, dass analytische Funktionen fest in SAP S/4HANA integriert sind. Du brauchst kein separates Business-Intelligence-System mehr, um Auswertungen zu erstellen. Operatives System und Analyse sind eins: Du arbeitest auf denselben Live-Daten, in Echtzeit, ohne dass Daten vorher irgendwohin kopiert werden müssen.

Das ist der große Unterschied zur klassischen Welt, in der ein ERP-System die Prozesse abwickelte und ein zweites System die Berichte lieferte.

## Wie war das früher — und was hat sich geändert?

Früher hattest du zwei getrennte Systeme:

- Das **ERP-System** für die operativen Prozesse: Bestellungen, Aufträge, Buchungen.
- Ein eigenes **BI-System** wie SAP BW (Business Warehouse) für die Auswertungen.

Zwischen beiden mussten die Daten erst wandern. Sie wurden aus dem ERP **extrahiert, transformiert und ins BW geladen** — oft über Nacht. Erst danach konntest du Reports darauf bauen. Das bedeutete: Deine Auswertung zeigte den Stand von gestern, nicht den von jetzt.

In SAP S/4HANA fällt dieser Umweg weg. **Analyse und operatives System sind dasselbe System.** Die Bestellung, die du gerade gebucht hast, taucht sofort in der passenden Auswertung auf.

## Warum funktioniert das? Der HANA-Faktor

Möglich gemacht hat das die **SAP HANA In-Memory-Datenbank**. Der Name sagt schon das Wesentliche: Sie hält die Daten im Arbeitsspeicher (englisch *in memory*) statt hauptsächlich auf der Festplatte. Berechnungen laufen dadurch extrem schnell — auch auf großen Datenmengen und selbst dann, wenn du sie live auf den operativen Daten anstößt.

Praktisch bedeutet das:

- Auswertungen laufen auf den **Originaldaten**, nicht auf Kopien.
- Reports liefern Ergebnisse in **Echtzeit**, nicht erst nach einem nächtlichen Ladelauf.
- Der Aufwand für **Datenreplikation** entfällt.
- Anwender sehen immer den **aktuellen Stand**, nicht den von gestern.

Dieser Echtzeit-Charakter ist der Kern der Idee. Wenn irgendwo von „Auswertung in Echtzeit“ oder „ohne Datenreplikation“ die Rede ist, geht es fast immer um Embedded Analytics.

## Was sind CDS Views?

Damit Auswertungen direkt auf den operativen Daten funktionieren, braucht es eine Schicht, die diese Daten für die Analyse aufbereitet. Diese Schicht heißt **CDS Views**, kurz für *Core Data Services*.

Stell dir CDS Views als **Datenmodell-Schicht** vor. Sie bauen auf den klassischen Datenbank-Views auf und beschreiben, welche Daten aus welchen Tabellen für welche Auswertung zusammengeführt werden — inklusive Beziehungen, Berechnungen und aussagekräftiger Feldnamen. Sie sind damit das technische Fundament für nahezu alle analytischen Apps und Reports in S/4HANA.

Für dich als Anwender ist wichtig:

- CDS Views **musst du nicht selbst bauen**. Das ist Aufgabe von Beratern und Entwicklern.
- Du solltest den Begriff aber einordnen können: Er beschreibt, **woher die Zahlen kommen**, die dir eine analytische App anzeigt.
- Sie sorgen dafür, dass unterschiedliche Apps auf **derselben, konsistenten Datengrundlage** arbeiten.

## Wie erlebt man Embedded Analytics im Fiori Launchpad?

Das Fiori Launchpad ist die Startseite in S/4HANA — eine Sammlung von Kacheln, über die du Apps öffnest. Embedded Analytics begegnet dir dort in mehreren Formen.

### Analytische Apps

**Analytische Apps** sind reine Auswertungs-Apps. Sie liefern dir Listen, Kennzahlen und visuelle Aufbereitungen, ohne dass du ein separates Tool öffnen musst. Ein typisches Beispiel ist eine App, die dir auf einen Blick zeigt, welche Aufträge in welchem Zustand sind und wo es hakt.

Wichtig zur Einordnung:

- Analytische Apps sind **keine operativen Apps** — du buchst damit nichts, du wertest aus.
- Sie greifen direkt auf **Live-Daten** zu, ohne Umweg über ein BI-System.
- Sie liegen wie alle anderen Apps im **Fiori Launchpad**.

### KPI-Kacheln (dynamische Kacheln)

Eine Besonderheit sind **KPI-Kacheln**, eine Form der **dynamischen Kacheln** (Dynamic Tiles). Sie zeigen eine Live-Kennzahl direkt auf der Startseite an, ohne dass du die App öffnen musst. Typische Beispiele:

- Anzahl offener Bestellungen
- Umsatz im aktuellen Monat
- Liefertermintreue in Prozent
- Anzahl überfälliger Aufträge

Der Wert aktualisiert sich automatisch und zeigt immer den aktuellen Stand. So erkennst du auf einen Blick, ob alles im grünen Bereich ist oder ob du eingreifen musst. Zum Vergleich: Eine **statische Kachel** zeigt nur Titel und Symbol und öffnet beim Klick einfach die App — ohne eigene Kennzahl.

### Übersichtsseiten und Karten

Ein zentraler datengetriebener App-Typ ist die **Übersichtsseite** (Overview Page). Sie bündelt alle Informationen, die du für eine Aufgabe brauchst, auf einer einzigen Seite — passend zu deinem Aufgabengebiet oder deiner Rolle. Aufgebaut ist sie aus mehreren **Karten** (Cards), die jeweils etwas anderes zeigen:

- **Analysekarte** — visualisiert eine Kennzahl grafisch, etwa den gesamten Bestellwert als Diagramm.
- **Listenkarte** — zeigt eine Liste relevanter Datensätze, etwa dringende Anforderungen.
- **Tabellenkarte** — präsentiert tabellarische Daten mit Spalten, etwa Ausgaben nach Periode und Wert.

Ergänzend gibt es die **Objektseite** (Object Page). Sie zeigt alle Details zu einem konkreten Geschäftsobjekt — etwa einer Bestellung, einem Material oder einem Kunden — auf einer Seite, gegliedert in Kopfbereich, Abschnitte und Blöcke.

## Von der Kennzahl zum Detail: Drill-Down

Auswertungen in S/4HANA sind selten eine Sackgasse. Der wichtigste Bewegungsablauf heißt **Drill-Down**: Du beginnst mit einer aggregierten Zahl und arbeitest dich schrittweise nach unten, bis du die Ursache siehst.

Ein Beispiel für den Weg von oben nach unten:

1. Gesamtumsatz dieses Quartal
2. Umsatz nach Region
3. Umsatz nach Land
4. Umsatz nach Kunde
5. Umsatz nach einzelnem Auftrag

So findest du heraus, woher eine Abweichung stammt, ohne fünf verschiedene Reports zu öffnen. Aus einer einzigen Kennzahl wird eine ganze Analyse-Geschichte.

Wenn du mehrere Blickwinkel gleichzeitig betrachten willst, helfen **mehrdimensionale Auswertungen** (Multidimensional Reports). Damit siehst du zum Beispiel den Umsatz nach Produkt, nach Region und nach Quartal in einer einzigen Auswertung — und kannst Filter und Sichten jederzeit ändern. Auch das läuft direkt im S/4HANA-System, in Echtzeit, ohne externe Tools.

## Wie findet man die passende Auswertung?

Bei all den Apps, Kacheln und Reports stellt sich schnell die Frage: Welche Auswertungen gibt es überhaupt? Dafür gibt es den **Query Browser** — eine App, mit der du verfügbare Reports und Abfragen (Queries) durchsuchst. Du kannst nach Themen filtern, dir Vorschauen ansehen und die passende Auswertung direkt starten.

Der Query Browser ist besonders dann nützlich, wenn du nicht weißt, ob es für deine Frage schon eine fertige Auswertung gibt. Oft liefert SAP genau das, was du brauchst, bereits mit.

## Wo hört Embedded Analytics auf — und wo beginnt die SAP Analytics Cloud?

Embedded Analytics deckt sehr viele Szenarien ab, aber nicht alles. Für komplexere Anforderungen kommt zusätzlich die **SAP Analytics Cloud (SAC)** ins Spiel — eine optionale Cloud-Plattform, die du mit S/4HANA verbinden kannst. Sie bietet:

- komplexe, interaktive **Dashboards**
- **Planungsfunktionen** wie Budgetierung und Forecasting
- **Predictive Analytics** mit vorhersagenden Modellen
- Datenintegration aus **mehreren Quellen**, nicht nur aus S/4HANA

Wichtig zur Einordnung: Die SAP Analytics Cloud ist **kein Pflichtbestandteil**. Embedded Analytics in S/4HANA funktioniert auch ohne sie. Die SAC ist eine Ergänzung für Anwendungsfälle, die über das hinausgehen, was direkt im ERP sinnvoll ist.

## Embedded Analytics im Vergleich zum Data Warehouse

Eine häufige Verständnisfrage dreht sich um den Unterschied zwischen Embedded Analytics und einem klassischen **Data Warehouse** wie SAP BW (Business Warehouse). Beide haben ihre Berechtigung — sie lösen unterschiedliche Aufgaben.

| Merkmal | Embedded Analytics | Data Warehouse (z. B. SAP BW) |
| --- | --- | --- |
| Ort der Auswertung | direkt im S/4HANA | in einem zweiten System |
| Datengrundlage | Originaldaten | Datenkopien |
| Aktualität | Echtzeit, aktueller Stand | oft zeitversetzt, Stand von gestern |
| Datenreplikation | keine nötig | Extraktion und Ladelauf nötig |
| Typischer Zweck | operative Auswertungen | große, quellenübergreifende Analysen |

Das heißt nicht, dass das Data Warehouse verschwindet. Für sehr große, unternehmensweite Analysen über viele Quellen hinweg gibt es weiterhin gute Gründe, ein Data Warehouse (etwa SAP BW/4HANA) zu nutzen. Für die typischen operativen Auswertungen in einem S/4HANA-System brauchst du es aber nicht mehr.

## Ein Tag mit Embedded Analytics

Damit das nicht abstrakt bleibt, hier ein typischer Ablauf:

1. **Anmeldung im Fiori Launchpad.** Schon auf der Startseite zeigen KPI-Kacheln die wichtigsten Live-Kennzahlen für deinen Bereich.
2. **Eine Kachel zeigt einen kritischen Wert.** Du klickst sie an und landest in einer analytischen App mit den Details.
3. **In der App nutzt du Drill-Down**, um nachzuvollziehen, welche Vorgänge das Problem verursachen.
4. **Für eine Detailsicht** öffnest du eine mehrdimensionale Auswertung und filterst nach Region und Quartal.
5. **Findest du keine passende Auswertung**, nutzt du den Query Browser, um zu prüfen, was sonst verfügbar ist.
6. **Alle Daten sind live.** Du musst nichts neu laden, nichts replizieren, nichts abwarten.

Wenn du verstehst, wie diese Bausteine zusammenspielen, ordnest du auch unbekannte Situationen schnell richtig ein.

## Die wichtigsten Begriffe auf einen Blick

- **Embedded Analytics** — Auswertung direkt im ERP, ohne separates BI-System
- **HANA In-Memory-Datenbank** — hält Daten im Arbeitsspeicher, macht Echtzeit möglich
- **CDS Views** — die Datenmodell-Schicht für Auswertungen
- **Analytische Apps** — reine Auswertungs-Apps im Launchpad
- **KPI-Kacheln / dynamische Kacheln** — Live-Kennzahlen direkt auf der Startseite
- **Drill-Down** — von der aggregierten Zahl schrittweise ins Detail
- **Mehrdimensionale Auswertungen** — mehrere Blickwinkel in einer Analyse
- **Query Browser** — App zum Durchsuchen verfügbarer Auswertungen
- **SAP Analytics Cloud (SAC)** — optionale Cloud-Plattform für weitergehende BI-Aufgaben

## Kurz zusammengefasst

Embedded Analytics ist kein technisches Buzzword, sondern ein zentrales Konzept in SAP S/4HANA: Auswertungen laufen direkt im operativen System, in Echtzeit, ohne den Umweg über ein klassisches Data Warehouse. Möglich macht das die HANA In-Memory-Datenbank zusammen mit CDS Views als Datenfundament. Im Fiori Launchpad begegnet dir das Ganze als analytische Apps, KPI-Kacheln, Übersichtsseiten und Drill-Down. Wer diese Bausteine einmal auseinanderhält, versteht schnell, warum Auswerten und Arbeiten in S/4HANA zusammengehören.

## Häufige Fragen

### Was ist Embedded Analytics in SAP S/4HANA?

Embedded Analytics bedeutet, dass Auswertungen und Reports direkt im operativen SAP-S/4HANA-System laufen — auf denselben Live-Daten, in Echtzeit, ohne den Umweg über ein separates Business-Intelligence-System. Möglich macht das die HANA In-Memory-Datenbank zusammen mit CDS Views als Datenmodell.

### Was sind CDS Views?

CDS Views (Core Data Services) sind eine Modellierungsschicht, die beschreibt, welche Daten aus welchen Tabellen für eine Auswertung zusammengeführt werden. Sie sind das Datenfundament für nahezu alle analytischen Apps und Reports in S/4HANA. Anwender müssen sie nicht selbst bauen — das ist Aufgabe von Beratern und Entwicklern.

### Worin unterscheidet sich Embedded Analytics von einem Data Warehouse wie SAP BW?

Ein Data Warehouse wie SAP BW extrahiert Daten aus dem ERP und lädt sie in ein zweites System, meist zeitversetzt. Embedded Analytics wertet direkt auf den Originaldaten im S/4HANA aus, in Echtzeit und ohne Replikation. Für große, quellenübergreifende Analysen bleibt ein Data Warehouse trotzdem sinnvoll.

### Was ist eine dynamische Kachel (KPI Tile)?

Eine dynamische Kachel zeigt eine Live-Kennzahl direkt auf der Startseite an — etwa die Anzahl offener Bestellungen oder den Umsatz des Monats. Der Wert aktualisiert sich automatisch, sodass du deine Lage erkennst, ohne die App überhaupt zu öffnen.

### Brauche ich die SAP Analytics Cloud zusätzlich zu Embedded Analytics?

Nicht zwingend. Embedded Analytics deckt operative Auswertungen direkt in S/4HANA ab. Die SAP Analytics Cloud ist eine optionale Cloud-Plattform für weitergehende Aufgaben wie unternehmensweite Dashboards, Planung und Predictive Analytics über mehrere Datenquellen hinweg.
