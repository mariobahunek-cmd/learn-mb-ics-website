---
layout: post
lang: de
title: "SAP Fiori Launchpad: die Startseite von S/4HANA verständlich erklärt"
description: "Kacheln, Bereiche, Seiten, Suche und Personalisierung: So funktioniert das SAP Fiori Launchpad als moderne Startseite für jeden S/4HANA-Anwender — klar erklärt."
slug: sap-fiori-launchpad-grundlagen
permalink: /blog/de/sap-fiori-launchpad-grundlagen/
translation_key: post-fiori-launchpad
date: 2026-07-07
category: "Grundlagen"
keywords: "SAP Fiori Launchpad, SAP Fiori, S/4HANA Oberfläche, Fiori Kacheln, Bereiche und Seiten, Meine Startseite, Personalisierung, SAP Anwender"
reading_time: 8
sources:
  - label: "SAP Help Portal — SAP Fiori Launchpad (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich SAP Fiori / User Experience — allgemeine Grundlagen zum Launchpad. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Unterschied zwischen SAP Fiori und dem Fiori Launchpad?"
    a: "SAP Fiori ist das gesamte Design- und Bedienkonzept von S/4HANA — also der Stil, in dem die Apps aussehen und funktionieren. Das Fiori Launchpad ist die konkrete Startseite, auf der diese Apps als Kacheln liegen und von der aus du sie öffnest."
  - q: "Warum sieht mein Launchpad anders aus als das meiner Kollegen?"
    a: "Fiori ist rollenbasiert. Jeder Anwender sieht nur die Apps, die zu seiner Rolle gehören. Wer im Einkauf arbeitet, bekommt andere Kacheln als jemand aus der Buchhaltung — plus die eigenen Personalisierungen wie angeheftete Apps oder ein anderes Theme."
  - q: "Was ist der Unterschied zwischen einem Bereich (Space) und einer Seite (Page)?"
    a: "Ein Bereich ist ein großer Abschnitt des Launchpads, meist einem Aufgabengebiet zugeordnet, und funktioniert wie ein Reiter oben. Innerhalb eines Bereichs liegen eine oder mehrere Seiten, auf denen die Apps in Abschnitten mit Überschriften gruppiert sind."
  - q: "Kann ich das Fiori Launchpad selbst anpassen?"
    a: "Ja. Du kannst Apps anheften, Kacheln per Drag-and-Drop umsortieren, eigene Abschnitte anlegen und das Theme wechseln. Diese Personalisierung gilt nur für dich und ändert nichts an dem, was andere Anwender sehen."
  - q: "Muss ich in Fiori noch Transaktionscodes kennen?"
    a: "Für die meiste Arbeit nicht mehr. Die zentrale Suche findet Apps und Geschäftsobjekte über Klartext, etwa „Bestellung anlegen“. Klassische Transaktionen lassen sich in S/4HANA aber weiterhin aufrufen und öffnen sich dann in einem eingebetteten GUI-Fenster."
---

Melde dich an einem SAP-S/4HANA-System an, und du landest fast immer an derselben Stelle: im SAP Fiori Launchpad. Es ist die moderne Startseite jedes Anwenders und ersetzt Schritt für Schritt die klassische, graue SAP GUI. Wenn ich das im Kurs zum ersten Mal zeige, kommt fast reflexhaft die Frage, ob Fiori denn „ein neues Programm“ sei. Ist es nicht: Fiori ist die Oberfläche, durch die dasselbe S/4HANA hindurchscheint, das früher grau und kantig aussah.

## Das Launchpad in einem Satz

Das Fiori Launchpad ist der zentrale Einstiegspunkt in SAP S/4HANA. Stell es dir vor wie den Homescreen deines Smartphones: Du siehst Kacheln, klickst eine an, und die zugehörige App öffnet sich. Im Hintergrund läuft dabei das komplette S/4HANA mit seinen Geschäftsprozessen.

Der wichtigste Gedanke dahinter: Das Launchpad ist **rollenbasiert**. Es zeigt dir nur die Apps, die zu deiner Aufgabe gehören, nicht das gesamte System. Deshalb sieht deine Startseite anders aus als die einer Kollegin aus dem Einkauf oder der Buchhaltung.

## Was ist SAP Fiori überhaupt?

SAP Fiori ist die Benutzeroberfläche, die User Experience, von SAP S/4HANA. Während die alte SAP GUI mit grauen Menüs, Transaktionscodes und dicht gepackten Eingabefeldern arbeitete, sieht Fiori aus wie eine moderne Web-Anwendung: Kacheln auf hellem Hintergrund, klare Schrift, verständliche Symbole und eine durchgängige Suche.

SAP hat Fiori nach fünf Designprinzipien aufgebaut:

- **Rollenbasiert** — jeder Anwender sieht nur die Apps, die zu seiner Rolle gehören
- **Flexibel** — die Oberfläche passt sich verschiedenen Anwendungsfällen und Geräten an (Desktop, Tablet, Smartphone)
- **Einheitlich** — alle Apps folgen demselben Look-and-Feel und fühlen sich an wie aus einem Guss
- **Einfach** — klare Aufgaben, wenige Klicks, kein überfrachtetes Menü
- **Ansprechend** — die Bedienung soll angenehm und intuitiv sein

## Die festen Bereiche des Launchpads

Wenn du das Launchpad geöffnet hast, findest du dich schnell zurecht, sobald du die festen Zonen kennst. Ganz oben sitzt die Kopfzeile, die Shell Bar, mit Logo, Suche, Benachrichtigungen und dem Benutzermenü. Darunter liegt der Hauptbereich mit den eigentlichen Apps, organisiert in Bereichen und Seiten (englisch: Spaces and Pages). Navigiert wird über das Menü oder die Suche.

### Apps und Kacheln

Apps sind die einzelnen Funktionen, die du im Launchpad anklickst. Sie werden dir in zwei Formen präsentiert:

- **Kacheln (Tiles)** — größere, oft farbige Quadrate oder Rechtecke
- **Links** — kompakte Textlinks, ideal für selten genutzte Apps

Beide führen zum selben Ziel: Sie öffnen eine App. Kacheln sind nur auffälliger und können zusätzliche Informationen anzeigen.

### Die zentrale Suche

Ganz oben im Launchpad liegt eine Suchleiste. Dort suchst du nicht nur nach Apps, sondern auch nach Geschäftsobjekten — konkreten Bestellungen, Kunden, Materialien oder Mitarbeitern. Die Suche durchsucht systemweit alles, wofür du berechtigt bist.

Das ist ein großer Vorteil gegenüber der klassischen GUI: Du musst keine Transaktionscodes mehr auswendig können. Tippe „Bestellung anlegen“ oder „Kunde 12345“ ein, und das System bringt dich direkt zum Ziel.

### Benachrichtigungen und Benutzermenü

Rechts oben in der Kopfzeile findest du ein Glockensymbol, das Notification Center. Hier laufen Genehmigungsanfragen, Aufgaben, Erinnerungen und Workflow-Schritte ein. Mit einem Klick springst du aus der Benachrichtigung direkt in die passende App.

Daneben liegt dein Benutzermenü, erkennbar am Profilbild oder an deinen Initialen. Dort findest du persönliche Einstellungen (Sprache, Zeitzone, Theme), Personalisierungsoptionen, Favoriten sowie das Abmelden.

## Welche Kachel-Arten gibt es?

Nicht jede Kachel ist gleich. SAP unterscheidet drei zentrale Arten:

- **Statische Kachel (Static Tile)** — zeigt nur Titel und Symbol. Ein Klick öffnet die App, sonst passiert nichts.
- **Dynamische Kachel (Dynamic Tile)** — zeigt eine aktuelle Kennzahl direkt auf der Kachel, zum Beispiel „Offene Bestellungen: 47“. Du erkennst deine Lage auf einen Blick, ohne die App zu öffnen.
- **News-Kachel (News Tile)** — zeigt aktuelle Nachrichten oder Mitteilungen, oft als rotierender Inhalt. Praktisch für interne Kommunikation oder Newsfeeds.

Dynamische Kacheln sparen Zeit: Du siehst direkt auf dem Launchpad, ob du etwas tun musst. Genau deshalb sind sie in modernen S/4HANA-Systemen beliebt.

## Bereiche und Seiten — wie die Apps organisiert sind

In früheren Fiori-Versionen waren Apps in **Gruppen** (Groups) organisiert. Im Laufe der Zeit hat SAP das System modernisiert. Heute arbeitest du mit **Bereichen** (Spaces) und **Seiten** (Pages).

### Bereiche

Ein Bereich ist ein eigener Abschnitt im Launchpad, der einer Rolle oder einem Aufgabengebiet zugeordnet ist. Du kannst dir Bereiche wie Reiter (Tabs) im oberen Teil vorstellen: etwa „Einkauf“, „Lager“ oder „Mein Arbeitsplatz“. Wer im Einkauf arbeitet, klickt auf den Einkauf-Bereich und sieht nur die dort relevanten Apps.

### Seiten

Innerhalb eines Bereichs gibt es eine oder mehrere Seiten. Eine Seite ist eine inhaltliche Untergliederung: Die Apps sind in Abschnitten mit Überschriften gruppiert — zum Beispiel „Bestellungen“, „Anfragen“ oder „Lieferantenstammdaten“.

### Meine Startseite

Mit dem Theme **SAP Fiori Horizon** ist auch **Meine Startseite** dazugekommen, eine persönliche Startseite, die du selbst gestalten kannst. Sie bündelt typischerweise mehrere Abschnitte:

- **To-Dos** — Aufgaben und Situationen an einem Ort
- **Seiten** — direkt anspringbar, ohne den Umweg über die Bereiche
- **Apps** — kürzlich oder häufig genutzte Apps sowie Favoriten
- **Insights** — analytische Karten und Kennzahlen

So baust du dir deinen persönlichen Schnellzugriff, unabhängig von den vorgegebenen Bereichen.

## Personalisierung: das Launchpad zu deinem machen

Eine der Stärken von Fiori ist die Personalisierung. Du musst die Einrichtung nicht hinnehmen, wie sie kommt. Typischerweise kannst du:

- **Apps anheften** — wichtige Apps auf „Meine Startseite“ oder eigene Seiten legen
- **Reihenfolge ändern** — Kacheln per Drag-and-Drop verschieben
- **Abschnitte anlegen oder umbenennen** — eigene Strukturen aufbauen
- **Theme wechseln** — die Optik des Launchpads ändern

### Themes — die Optik wählen

SAP liefert in S/4HANA mehrere Themes mit. Die zentralen für aktuelle Systeme:

- **SAP Quartz Light** — helles Theme, lange Zeit Standard in S/4HANA
- **SAP Quartz Dark** — dunkles Theme, augenschonend bei langen Arbeitstagen
- **SAP Fiori Horizon** — das neueste Theme mit Signatur-Design und stärkerem Fokus auf die wichtigen Bildschirmbereiche

Das Theme wechselst du im Benutzermenü unter „Einstellungen“ beziehungsweise „Darstellung“.

## Welche App-Typen gibt es?

Nicht jede App macht dasselbe. SAP unterscheidet drei Haupttypen:

- **Transaktionale Apps** — hier führst du Geschäftstransaktionen aus, etwa eine Bestellung anlegen, einen Kunden anlegen oder eine Rechnung freigeben. Das ist die operative Arbeit.
- **Analytische Apps** — Apps für Auswertungen, Kennzahlen und Dashboards. Sie zeigen dir Trends und Berichte, etwa Umsatz nach Region oder offene Posten.
- **Fact-Sheet-Apps** — Übersichts-Apps zu einem konkreten Geschäftsobjekt. Du siehst alle relevanten Informationen zu einem Kunden, einer Bestellung oder einem Material auf einen Blick und navigierst von dort weiter.

Ein typischer Arbeitstag mischt alle drei: Morgens prüfst du in einer analytischen App den Stand, springst von dort in eine Fact-Sheet-App zu einem konkreten Vorgang und öffnest schließlich eine transaktionale App, um etwas zu ändern oder freizugeben.

## Fiori und die klassische SAP GUI im Vergleich

Viele Unternehmen arbeiten noch mit beiden Welten parallel. Die wichtigsten Unterschiede:

| Merkmal | SAP Fiori | SAP GUI |
| --- | --- | --- |
| Optik | webbasiert, modern, farbig | Desktop-basiert, grau, dicht |
| Bedienung | Suche, Kacheln, Klicks | Transaktionscodes und Menüpfade |
| Geräte | Desktop, Tablet, Smartphone | Installation auf dem PC |
| Zielgruppe | Anwender mit klaren Aufgaben | Power-User mit vielen Spezialtransaktionen |
| Zukunft | SAP investiert hier | bleibt für bestimmte Funktionen erhalten |

Aus dem Fiori Launchpad heraus kannst du in S/4HANA übrigens auch klassische GUI-Transaktionen aufrufen — sie öffnen sich dann in einem eingebetteten GUI-Fenster. So kommt jede Funktion durch dieselbe Tür herein.

## Häufige Stolpersteine

Fast immer sind es dieselben Stellen, an denen es hakt: Launchpad, Kachel und App geraten durcheinander, und wer lange mit der alten SAP GUI gearbeitet hat, sucht die vertrauten Menüs dort, wo jetzt Kacheln liegen.

- **Begriffe verwechseln.** Bereich, Seite, Abschnitt, Kachel, App — wer diese durcheinanderbringt, findet sich in Gesprächen schwerer zurecht. Ordne jedem Begriff seine Funktion zu, dann wird das Launchpad schnell klar.
- **Personalisierung mit Berechtigung verwechseln.** Wenn dir eine App fehlt, hilft kein Anheften — sie gehört schlicht nicht zu deiner Rolle. Personalisierung ordnet nur an, was du ohnehin sehen darfst.
- **Nach Transaktionscodes suchen, statt die Suche zu nutzen.** Die zentrale Suche findet Apps und Geschäftsobjekte über Klartext. Wer trotzdem Codes tippt, macht sich die Arbeit unnötig schwer.

## Worauf es ankommt

Das SAP Fiori Launchpad ist die **rollenbasierte Startseite** von S/4HANA: eine Sammlung von Kacheln, die dir genau die Apps zeigt, die zu deiner Aufgabe passen. Du navigierst über Bereiche und Seiten, findest alles über die zentrale Suche und richtest dir mit Personalisierung und Themes deinen eigenen Arbeitsplatz ein. Wer die Bausteine Kachel, Bereich, Seite und App-Typ einmal auseinanderhält, bewegt sich in S/4HANA schnell sicher.

## Häufige Fragen

### Was ist der Unterschied zwischen SAP Fiori und dem Fiori Launchpad?

SAP Fiori ist das gesamte Design- und Bedienkonzept von S/4HANA — also der Stil, in dem die Apps aussehen und funktionieren. Das Fiori Launchpad ist die konkrete Startseite, auf der diese Apps als Kacheln liegen und von der aus du sie öffnest.

### Warum sieht mein Launchpad anders aus als das meiner Kollegen?

Fiori ist rollenbasiert. Jeder Anwender sieht nur die Apps, die zu seiner Rolle gehören. Wer im Einkauf arbeitet, bekommt andere Kacheln als jemand aus der Buchhaltung — plus die eigenen Personalisierungen wie angeheftete Apps oder ein anderes Theme.

### Was ist der Unterschied zwischen einem Bereich (Space) und einer Seite (Page)?

Ein Bereich ist ein großer Abschnitt des Launchpads, meist einem Aufgabengebiet zugeordnet, und funktioniert wie ein Reiter oben. Innerhalb eines Bereichs liegen eine oder mehrere Seiten, auf denen die Apps in Abschnitten mit Überschriften gruppiert sind.

### Kann ich das Fiori Launchpad selbst anpassen?

Ja. Du kannst Apps anheften, Kacheln per Drag-and-Drop umsortieren, eigene Abschnitte anlegen und das Theme wechseln. Diese Personalisierung gilt nur für dich und ändert nichts an dem, was andere Anwender sehen.

### Muss ich in Fiori noch Transaktionscodes kennen?

Für die meiste Arbeit nicht mehr. Die zentrale Suche findet Apps und Geschäftsobjekte über Klartext, etwa „Bestellung anlegen“. Klassische Transaktionen lassen sich in S/4HANA aber weiterhin aufrufen und öffnen sich dann in einem eingebetteten GUI-Fenster.
