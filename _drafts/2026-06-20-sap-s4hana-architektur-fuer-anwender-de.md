---
layout: post
lang: de
title: "SAP S/4HANA Architektur einfach erklärt für Anwender"
description: "SAP S/4HANA besteht aus drei Schichten: der In-Memory-Datenbank HANA, dem ERP selbst und der Fiori-Oberfläche. Was das für dich als Anwender bedeutet — verständlich erklärt."
slug: sap-s4hana-architektur-fuer-anwender
permalink: /blog/de/sap-s4hana-architektur-fuer-anwender/
translation_key: post-s4hana-architektur
date: 2026-07-07
category: "Grundlagen"
keywords: "SAP S/4HANA Architektur, SAP HANA, In-Memory-Datenbank, SAP Fiori, Cloud ERP, SAP BTP, RISE with SAP, SAP für Anwender"
reading_time: 7
sources:
  - label: "SAP Help Portal — SAP S/4HANA"
    url: "https://help.sap.com/"
    note: "Allgemeine Grundlagen zur S/4HANA-Architektur. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen SAP HANA und SAP S/4HANA?"
    a: "SAP HANA ist die In-Memory-Datenbank, die im Hintergrund läuft und die Daten hält. SAP S/4HANA ist das ERP-System mit den Geschäftsanwendungen, das auf dieser Datenbank aufsetzt. Kurz: HANA ist das Fundament, S/4HANA das Gebäude darauf."
  - q: "Was bedeutet das „4“ in S/4HANA?"
    a: "Das „4“ steht für die vierte Generation der SAP-Geschäftssoftware — nach R/2, R/3 und SAP ERP. Der Zusatz „HANA“ zeigt, dass diese Generation ausschließlich auf der SAP-HANA-Datenbank läuft."
  - q: "Muss ich als Anwender die Architektur überhaupt kennen?"
    a: "Bedienen kannst du SAP auch ohne dieses Wissen. Aber wer die drei Schichten versteht, kann besser einordnen, warum Auswertungen plötzlich in Echtzeit da sind, warum die Oberfläche wie eine App aussieht und wo im System welche Aufgabe erledigt wird."
  - q: "Ist SAP BTP dasselbe wie SAP HANA?"
    a: "Nein. SAP HANA ist die Datenbank direkt unter S/4HANA. SAP BTP (Business Technology Platform) ist eine übergeordnete Plattform, auf der App-Entwicklung, Integration, Datenanalyse und KI-Funktionen gebündelt werden — sie verbindet SAP-Anwendungen mit anderen Systemen."
  - q: "Was ist der Unterschied zwischen Cloud- und On-Premise-Betrieb?"
    a: "Bei der Cloud betreibt SAP (oder ein Partner) das System in einem Rechenzentrum, du greifst über das Netz darauf zu. Bei On-Premise läuft das System auf den eigenen Servern des Unternehmens, das dann auch Wartung und Updates selbst verantwortet."
---

„S/4HANA“ hört man im SAP-Umfeld ständig — auf Folien, in Projektmeetings, im Kursraum. Für viele klingt das nach Technik, nach Servern, nach etwas, das nur die IT verstehen muss. Dabei lässt sich die Architektur von SAP S/4HANA erstaunlich klar erklären, auch ohne eine Zeile Code. Dieser Artikel zeigt dir in einfacher Sprache, wie das System aufgebaut ist und was das für dich als Anwender im Alltag bedeutet.

## Kurz gesagt: ein Haus mit drei Stockwerken

Am einfachsten stellst du dir SAP S/4HANA als **Gebäude mit drei Stockwerken** vor:

- **Unten** liegt die Datenbank **SAP HANA** — das Fundament, das alle Daten hält.
- **In der Mitte** liegt das eigentliche **ERP-System S/4HANA** — die Geschäftsanwendung, mit der du arbeitest.
- **Oben** liegt die Benutzeroberfläche **SAP Fiori** — das, was du auf dem Bildschirm siehst und bedienst.

Wer diese drei Schichten einmal auseinanderhält, versteht sofort, warum die Begriffe manchmal durcheinandergehen: HANA, S/4HANA und Fiori sind nicht dasselbe, sondern bauen aufeinander auf.

## SAP S/4HANA in einem Satz

SAP S/4HANA ist die **aktuelle Generation der SAP-Geschäftsanwendungen** — der Nachfolger der früheren Systeme SAP R/3 und SAP ERP. Drei Dinge machen es technisch besonders:

- Die **In-Memory-Plattform SAP HANA** als Datenbank-Grundlage.
- Eine **vereinfachte, einheitliche Datenstruktur** mit deutlich weniger Tabellen als früher.
- Die **moderne Benutzeroberfläche SAP Fiori**.

## Schicht 1 — SAP HANA: die In-Memory-Datenbank

SAP HANA ist eine **In-Memory-Datenbank**. Das heißt: Die Daten liegen nicht wie bei klassischen Datenbanken vor allem auf der Festplatte, sondern werden im Hauptspeicher (Arbeitsspeicher, RAM) gehalten. Und Zugriffe auf den Arbeitsspeicher sind um ein Vielfaches schneller als Zugriffe auf eine Festplatte.

Für dich als Anwender ist vor allem ein Punkt wichtig: HANA kann **Transaktionen und Auswertungen im selben System** verarbeiten. Früher brauchte man dafür meist zwei getrennte Welten — ein System für das Tagesgeschäft (Buchungen, Bestellungen) und ein separates Data Warehouse für Auswertungen. Diese wurden oft nur nachts aktualisiert.

Weil HANA beides gleichzeitig kann, sind **Auswertungen in Echtzeit** möglich. Du siehst Kennzahlen auf dem Stand von jetzt, nicht auf dem Stand der letzten Nacht.

## Schicht 2 — SAP S/4HANA: das ERP-System

Auf HANA setzt die eigentliche Geschäftsanwendung auf: **SAP S/4HANA**. Das ist das ERP-System, mit dem im Unternehmen täglich gearbeitet wird — Bestellungen anlegen, Aufträge erfassen, Rechnungen buchen, Lager verwalten.

Das System deckt die typischen Geschäftsbereiche ab:

- **Kernprozesse** wie Herstellen, Verkaufen, Liefern und Finanzen.
- **Unterstützende Prozesse** wie Einkaufen, Service, Instandhaltung und Personal.

Das ist die Ebene, auf der die fachliche Arbeit passiert — etwa im Einkauf, im Vertrieb, in der Lagerwirtschaft oder im Rechnungswesen. Ein guter Einstieg in einen dieser Prozesse ist der [Beschaffungsprozess Procure-to-Pay](/blog/de/beschaffungsprozess-procure-to-pay/).

## Schicht 3 — SAP Fiori: die Benutzeroberfläche

SAP Fiori ist **kein einzelnes Programm**, sondern ein Designkonzept — eine Sammlung von Gestaltungsregeln dafür, wie SAP-Software aussehen und sich bedienen soll: einheitlich, aufgeräumt und auf verschiedenen Geräten nutzbar. Als Anwender bekommst du damit unter anderem:

- **Das SAP Fiori Launchpad** als zentralen Einstieg — vergleichbar mit einer App-Übersicht für deine SAP-Aufgaben.
- **Rollenbasierte Bereiche**, in denen du nur die Apps siehst, die für deine Aufgabe relevant sind. Mehr dazu in den [Grundlagen zum SAP Fiori Launchpad](/blog/de/sap-fiori-launchpad-grundlagen/).
- **Kennzahlen-Kacheln**, die wichtige Werte sofort anzeigen, ohne dass du erst eine Auswertung starten musst.
- **Auswertungen direkt im Arbeitsablauf** (Embedded Analytics), sodass du vom Überblick mit wenigen Klicks in die Details springen kannst.

Das Ziel dahinter: weniger Klicks, weniger Bildschirmwechsel, eine Oberfläche, die auf jedem Gerät gleich aussieht.

## Wo passt SAP BTP hinein?

Neben HANA gibt es noch die **SAP Business Technology Platform (BTP)**. Ein häufiges Missverständnis: BTP ist **nicht** SAP HANA. BTP ist eine übergeordnete Plattform, die alles rund um S/4HANA bündelt — App-Entwicklung, Integration, Datenanalyse und intelligente Technologien wie KI und maschinelles Lernen.

Vereinfacht gesagt ist BTP die **Verbindungsschicht**: Sie sorgt dafür, dass SAP S/4HANA mit ergänzenden SAP-Lösungen und mit Systemen anderer Anbieter zusammenspielt. Als Anwender musst du nicht jeden Bereich von BTP kennen — es reicht zu wissen, dass hier Erweiterungen, Automatisierungen und Anbindungen entstehen.

## Cloud, On-Premise oder Hybrid?

SAP S/4HANA gibt es in mehreren Betriebsvarianten. Der Unterschied liegt vor allem darin, **wer das System betreibt und wie stark es angepasst werden kann**:

- **Cloud, Public Edition** — ein weitgehend vorkonfiguriertes Cloud-ERP mit Standardprozessen, das regelmäßig automatisch aktualisiert wird. Oft die Wahl mittelständischer Unternehmen.
- **Cloud, Private Edition** — ein Cloud-ERP mit mehr Spielraum für individuelle Anpassungen. Häufig bei großen Unternehmen im Einsatz.
- **On-Premise** — das System läuft auf den eigenen Servern des Unternehmens. Maximale Anpassbarkeit, aber Betrieb, Wartung und Updates liegen im Haus.

Rund um die Einführung hörst du oft zwei Namen: **GROW with SAP** richtet sich an Unternehmen, die die Cloud Public Edition zügig einführen wollen, und **RISE with SAP** an Unternehmen, die ihr bestehendes ERP in Richtung Cloud modernisieren.

## Warum heißt es eigentlich „S/4HANA“?

Ein kurzer Blick auf die Geschichte macht den Namen verständlich:

| Jahr | System | Kennzeichen |
|------|--------|-------------|
| 1979 | SAP R/2 | Standardsoftware für Großrechner |
| 1992 | SAP R/3 | Drei-Ebenen-Architektur, grafische Oberfläche |
| 2004 | SAP ERP | serviceorientiert, auf SAP NetWeaver aufbauend |
| 2015 | SAP S/4HANA | Neuentwicklung, optimiert für In-Memory, Fiori-Oberfläche |

Das **„4“** steht für die **vierte Generation** der SAP-Geschäftssoftware (nach R/2, R/3 und SAP ERP). Das **„HANA“** zeigt, dass diese Generation ausschließlich auf der SAP-HANA-Datenbank läuft — anders als ältere Versionen, die auch auf Datenbanken anderer Anbieter liefen.

## Was du als Anwender konkret davon hast

Du musst nicht programmieren können, um von dieser Architektur zu profitieren. Drei Vorteile spürst du im Alltag am deutlichsten:

- **Echtzeit-Auswertungen** — keine Wartezeit auf nächtliche Läufe mehr, weil Tagesgeschäft und Auswertung im selben System liegen.
- **Einfachere Bedienung** — durch Fiori weniger Klicks, weniger Bildschirmwechsel und Nutzung auf verschiedenen Geräten.
- **Kennzahlen im Arbeitsablauf** — wichtige Werte sind direkt dort sichtbar, wo du arbeitest, nicht nur in einem separaten Berichtswerkzeug.

## Häufige Stolpersteine

- **HANA und S/4HANA verwechseln.** HANA ist die Datenbank im Untergeschoss, S/4HANA die Anwendung darüber. Wer beides gleichsetzt, wundert sich später über Begriffe, die nicht zusammenpassen.
- **BTP für die Datenbank halten.** BTP ist die Plattform drumherum, nicht die Datenbank unter S/4HANA. Das ist eine der häufigsten Verwechslungen.
- **Fiori für „ein Programm“ halten.** Fiori ist ein Designkonzept mit vielen einzelnen Apps, kein einzelnes Werkzeug, das man startet.

## Kurz zusammengefasst

SAP S/4HANA ist ein **Gebäude aus drei Schichten**: die In-Memory-Datenbank **HANA** als Fundament, das **ERP-System S/4HANA** als Anwendung darauf und die **Fiori-Oberfläche** als das, was du siehst und bedienst. Dazu kommt die Plattform **BTP** als Verbindungsschicht nach außen. Wer diesen Aufbau einmal verstanden hat, ordnet fast jeden S/4HANA-Begriff mühelos ein — und weiß, warum moderne SAP-Systeme schneller, aufgeräumter und näher am Echtzeit-Geschehen sind als ihre Vorgänger.

## Häufige Fragen

### Was ist der Unterschied zwischen SAP HANA und SAP S/4HANA?

SAP HANA ist die In-Memory-Datenbank, die im Hintergrund läuft und die Daten hält. SAP S/4HANA ist das ERP-System mit den Geschäftsanwendungen, das auf dieser Datenbank aufsetzt. Kurz: HANA ist das Fundament, S/4HANA das Gebäude darauf.

### Was bedeutet das „4“ in S/4HANA?

Das „4“ steht für die vierte Generation der SAP-Geschäftssoftware — nach R/2, R/3 und SAP ERP. Der Zusatz „HANA“ zeigt, dass diese Generation ausschließlich auf der SAP-HANA-Datenbank läuft.

### Muss ich als Anwender die Architektur überhaupt kennen?

Bedienen kannst du SAP auch ohne dieses Wissen. Aber wer die drei Schichten versteht, kann besser einordnen, warum Auswertungen plötzlich in Echtzeit da sind, warum die Oberfläche wie eine App aussieht und wo im System welche Aufgabe erledigt wird.

### Ist SAP BTP dasselbe wie SAP HANA?

Nein. SAP HANA ist die Datenbank direkt unter S/4HANA. SAP BTP (Business Technology Platform) ist eine übergeordnete Plattform, auf der App-Entwicklung, Integration, Datenanalyse und KI-Funktionen gebündelt werden — sie verbindet SAP-Anwendungen mit anderen Systemen.

### Was ist der Unterschied zwischen Cloud- und On-Premise-Betrieb?

Bei der Cloud betreibt SAP (oder ein Partner) das System in einem Rechenzentrum, du greifst über das Netz darauf zu. Bei On-Premise läuft das System auf den eigenen Servern des Unternehmens, das dann auch Wartung und Updates selbst verantwortet.
