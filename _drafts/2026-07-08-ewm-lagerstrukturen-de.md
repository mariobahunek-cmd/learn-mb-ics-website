---
layout: post
lang: de
title: "Lagerstrukturen in SAP EWM: Lagernummer, Lagertyp, Lagerplatz erklärt"
description: "Die SAP-EWM-Lagerstruktur klar erklärt: Lagernummer, Lagertyp, Lagerbereich, Lagerplatz und Aktivitätsbereich — die Hierarchie eines Lagers verständlich."
slug: ewm-lagerstrukturen
permalink: /blog/de/ewm-lagerstrukturen/
translation_key: post-ewm-warehouse-structure
date: 2026-07-08
category: "Lager"
keywords: "SAP EWM Lagerstruktur, SAP EWM Lagernummer, SAP EWM Lagertyp, SAP EWM Lagerbereich, SAP EWM Lagerplatz, Aktivitätsbereich, Extended Warehouse Management"
reading_time: 9
sources:
  - label: "SAP Help Portal — SAP Extended Warehouse Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Extended Warehouse Management — allgemeine Grundlagen zur Lagerstruktur. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist die Lagerstruktur in SAP EWM?"
    a: "Die Lagerstruktur in SAP EWM ist die hierarchische Abbildung eines realen Lagers im System. Sie geht von oben nach unten: Die Lagernummer steht für das gesamte Lager, der Lagertyp für einen Bereich darin, der Lagerbereich für eine Gruppe ähnlicher Plätze und der Lagerplatz für den einzelnen Stellplatz. So weiß das System jederzeit, wo eine Ware physisch liegt."
  - q: "Was ist der Unterschied zwischen Lagertyp und Lagerbereich?"
    a: "Ein Lagertyp ist eine physische oder logische Unterteilung des Lagers, etwa ein Hochregal, ein Wareneingangsbereich oder ein Kommissionierbereich. Ein Lagerbereich liegt eine Ebene tiefer und fasst innerhalb eines Lagertyps mehrere Lagerplätze mit ähnlichen Eigenschaften zusammen, zum Beispiel schwere Teile oder Schnelldreher."
  - q: "Wie viele Zeichen hat eine Lagernummer in SAP EWM?"
    a: "Die Lagernummer in SAP EWM ist vierstellig. Im klassischen SAP-ERP-Lager ist das entsprechende Feld dagegen nur dreistellig. Wird ein Lager über EWM geführt, wird die ERP-Lagernummer als EWM-relevant markiert und mit der vierstelligen EWM-Lagernummer verbunden."
  - q: "Wann ist ein Aktivitätsbereich in SAP EWM Pflicht?"
    a: "Ein Aktivitätsbereich ist grundsätzlich optional und bündelt Lagerplätze für eine bestimmte Tätigkeit wie Einlagern, Kommissionieren oder Inventur. Verpflichtend ist er nur für die Inventur — für alle anderen Aktivitäten kannst du ihn nutzen, musst es aber nicht."
  - q: "Muss ein Anwender die Lagerstruktur selbst anlegen?"
    a: "Nein. Die Lagerstruktur wird einmalig beim Aufbau des Lagers oder bei Erweiterungen über das Customizing eingerichtet. Im Tagesgeschäft bewegt sich jeder Anwender aber in dieser Struktur: Bei Wareneingang, Lageraufgabe, Scan oder Inventur arbeitest du immer entlang der Hierarchie Lagernummer, Lagertyp, Lagerbereich, Lagerplatz."
---

Ein Lager wirkt von außen wie ein einziger großer Raum voller Regale. Damit ein System wie SAP Extended Warehouse Management jede Ware punktgenau verwalten kann, muss dieser Raum aber in klare Ebenen zerlegt sein. Genau das leistet die Lagerstruktur: Lagernummer, Lagertyp, Lagerbereich und Lagerplatz — eine Hierarchie, die von „das ganze Lager“ bis zum einzelnen Stellplatz reicht. Dieser Artikel erklärt die Ebenen in klarer Sprache, mit praktischen Beispielen.

## Kurz gesagt: die Landkarte deines Lagers

Die Lagerstruktur in SAP EWM ist die hierarchische Abbildung eines realen Lagers im System. Sie geht von oben nach unten: Die **Lagernummer** steht für das gesamte Lager, der **Lagertyp** für einen Bereich darin, der **Lagerbereich** für eine Gruppe ähnlicher Plätze und der **Lagerplatz** für den einzelnen Stellplatz. So weiß das System jederzeit, wo eine Ware physisch liegt — und kann dir sagen, wohin sie beim Einlagern soll und wo sie beim Kommissionieren zu holen ist.

SAP EWM steht für **Extended Warehouse Management**, also die erweiterte Lagerverwaltung. Es ist die Software, mit der viele Unternehmen ihre großen, komplexen Lager steuern — von der Anlieferung am Tor bis zum Versand.

## SAP EWM und das klassische SAP WM — der Unterschied vorweg

Wer aus älteren SAP-Systemen kommt, kennt vielleicht noch **SAP WM (Warehouse Management)**. EWM ist keine bloße Weiterentwicklung davon, sondern ein eigenständiges Produkt mit eigener Architektur. Eine Gemeinsamkeit gibt es aber: Beide verwenden eine **Lagernummer** als oberste Organisationseinheit.

Ein sichtbarer Unterschied steckt im Detail. Im klassischen SAP-ERP-Lager ist das Feld für die Lagernummer **drei Zeichen** lang, in SAP EWM dagegen **vier Zeichen**. Wird ein Lager über EWM geführt, muss im ERP keine eigene Unterstruktur dafür gebaut werden. Stattdessen wird die ERP-Lagernummer als EWM-relevant markiert und mit der vierstelligen EWM-Lagernummer verbunden.

## Wie hängen ERP und EWM zusammen?

Bevor wir in die EWM-internen Ebenen einsteigen, lohnt der Blick auf den Übergang vom umgebenden ERP-System ins EWM. Vereinfacht sieht die Kette so aus:

- **Werk** (im ERP) — der Ort, an dem produziert oder gelagert wird
- **Lagerort** (im ERP) — eine Bestandsführungs-Einheit innerhalb des Werks
- **Lagernummer** (im ERP, 3 Zeichen) — verbindet ins EWM
- **Lagernummer** (in EWM, 4 Zeichen) — hier beginnt die EWM-Struktur

Ein **Werk** ist ein Ort, an dem Waren produziert (Fertigungswerk) oder gelagert werden (Distributionszentrum). Es gehört zu einem Buchungskreis, also einer Organisationseinheit im Finanzwesen. **Lagerorte** werden einem Werk zugeordnet und behalten den Bestand für die Bestandsführung im Blick.

Ein Lagerort selbst enthält keine physischen Unterstrukturen. Die kommen erst über die **Lagernummer** ins Spiel. Eine Lagernummer kann für ein einzelnes Gebäude stehen oder für mehrere Gebäude, die zusammen einen Lagerkomplex bilden.

## Ebene 1 — die Lagernummer: das ganze Lager

Die **Lagernummer** ist die oberste Ebene der Lagerorganisation. Unter ihr werden im Customizing die organisatorischen und physischen Eigenschaften des Lagergebäudes hinterlegt. Dazu gehören zum Beispiel:

- **Gewichtseinheit** — in welcher Einheit Gewichte geführt werden
- **Volumeneinheit** — in welcher Einheit Volumina geführt werden
- **Zeiteinheit** — die Basiseinheit für Zeitangaben

Auch Findungsschemata für Palettierungsdaten und Packspezifikationen hängen an der Lagernummer. In der Praxis entspricht eine Lagernummer meist **einem Gebäude oder einem Distributionszentrum**. Liegen deine Lagerstätten in verschiedenen Städten weit auseinander, bekommt jeder Komplex sinnvollerweise eine eigene Lagernummer.

### Die Supply-Chain-Unit (SCU)

Zu jeder Lagernummer gehört eine eindeutige **Supply-Chain-Unit (SCU)** — eine physische oder organisatorische Einheit, die im Logistikprozess mit betriebswirtschaftlichen Eigenschaften versehen ist. Die SCU trägt wichtige Rahmeninformationen wie **Land, Region und Zeitzone**. Für die Anzeige aller Datums- und Uhrzeitfelder greift das System auf die Zeitzone dieser SCU zurück. Praktisch heißt das: Die SCU sorgt dafür, dass Zeiten im Lager immer korrekt und ortsbezogen dargestellt werden.

## Ebene 2 — der Lagertyp: ein Bereich im Lager

Ein **Lagertyp** ist eine physische oder logische Unterteilung des Lagerkomplexes. Charakterisiert wird er durch die **Lagertechnik, den Platzbedarf, die Organisationsform oder die Funktion** — kurz: durch das, was in diesem Bereich passiert. Technisch ist der Lagertyp ein **vierstelliger Code**, der im Customizing definiert wird.

Jeder Lagertyp hat eine **Lagertyprolle**, die festlegt, wofür er da ist. Ein regulärer Lagertyp lagert Ware; andere Rollen decken die Zwischenstationen ab, die Ware auf ihrem Weg durch das Lager durchläuft. Die wichtigsten Rollen im Überblick:

- **Regulärer Lagertyp** — ein physischer Bereich, in dem Produkte tatsächlich gelagert werden
- **Identifikationspunkt** — hier wird Ware beim Einlagern etikettiert, identifiziert oder geprüft
- **Kommissionierpunkt** — hier wird Ware beim Auslagern geprüft, etikettiert oder verpackt
- **Identifikations- und Kommissionierpunkt** — beide Funktionen an einem Ort
- **Bereitstellungszonengruppe** — eine oder mehrere Bereitstellungszonen im Lager
- **Arbeitsplatz** — für Tätigkeiten wie Dekonsolidierung, Prüfung, Verpackung oder Zusatzleistungen
- **Tore** — bestimmte physische Standorte, etwa die Tore an einer Lagerseite
- **Yard** — ein an das Lager angrenzender Hof-Bereich
- **Fördertechnik** — Bereich mit automatisierten Förderanlagen
- **Automatisiertes Lager** — ein Hochregallager mit Regalbediengerät
- **Produktionsversorgung** — Bereich, in dem Ware nahe der Produktionslinie bereitgestellt wird

Die wesentlichen Einstellungen für Einlagerung, Auslagerung und Warenbewegungssteuerung werden im Customizing des Lagertyps festgelegt. Der Lagertyp ist damit die Ebene, auf der du entscheidest, wie ein Bereich funktioniert.

## Ebene 3 — der Lagerbereich: Plätze mit ähnlichen Eigenschaften

Ein **Lagerbereich** ist eine organisatorische Unterteilung innerhalb eines Lagertyps. Er fasst Lagerplätze zusammen, die ähnliche Eigenschaften teilen. Das System nutzt diese Information beim **Einlagern**, um zu entscheiden, wo eine eingehende Ware am besten hinkommt.

Welche Kriterien einen Lagerbereich bilden, ist frei wählbar. Typische Beispiele:

- **Schwere Teile** — Plätze, die für hohes Gewicht ausgelegt sind
- **Sperrige Teile** — Plätze mit viel Raum
- **Gefahrstoffe** — Plätze mit besonderen Auflagen
- **Schnelldreher** — Artikel mit hoher Umschlagshäufigkeit, nah am Ausgang
- **Langsamdreher** — Artikel, die selten bewegt werden

Lagerbereiche werden außerdem in Bereitstellungszonengruppen gebraucht — also in den Lagertypen für Wareneingang und Warenausgang. Der Lagerbereich ist damit das Bindeglied zwischen dem groben Bereich (Lagertyp) und dem konkreten Stellplatz (Lagerplatz).

## Ebene 4 — der Lagerplatz: der einzelne Stellplatz

Der **Lagerplatz** ist die kleinste Raumeinheit im Lager. Er gibt die genaue Position an, an der ein Produkt liegt. Wenn dir das System sagt „hol die Ware von Platz X“, dann meint es einen Lagerplatz.

### Was zu einem Lagerplatz gehört

Ein Lagerplatz trägt eine Reihe von Merkmalen, die zusammen beschreiben, was er kann und wo er liegt:

- **Zuordnung** — zu welcher Lagernummer, welchem Lagertyp und Lagerbereich er gehört
- **Kapazitäten** — maximales Gewicht, maximales Volumen, Gesamtkapazität
- **Strukturelle Koordinaten** — Gang, Säule, Ebene
- **Geografische Koordinaten** — X, Y, Z zur Entfernungsberechnung

### Die Platzkoordinate

Weil sich die Position eines Lagerplatzes meist aus einem Koordinatensystem ableitet, heißt sie **Platzkoordinate**. Sie kann bis zu **18 Zeichen** lang sein. Ein Beispiel: Die Koordinate `01-02-03` steht für Gang 1, Säule 2 und Ebene 3.

Wichtig ist ein Grundsatz: Die Platzkoordinate ist **innerhalb eines Lagers eindeutig**. Kein Platz teilt sich seine Koordinate mit einem anderen — sonst wüsste das System nicht, wo die Ware wirklich liegt.

Das Anlegen der Koordinaten läuft im Customizing in zwei Schritten:

1. **Koordinatenstruktur definieren** — also die „Kodierung“ des Platzes festlegen: welche Zeichen für Gang, Säule, Ebene und weitere Komponenten stehen
2. **Vorlagen erstellen** — mit denen sich die Lagerplatz-Stammdaten automatisch erzeugen lassen, statt jeden Platz von Hand anzulegen

Für die Koordinaten kannst du jede Kombination aus **Buchstaben und Zahlen** verwenden.

### Weitere Eigenschaften

Jeder Lagerplatz gehört zu genau einem Lagertyp und kann einem Lagerbereich zugeordnet sein. Darüber hinaus lassen sich weitere Eigenschaften festlegen, die im Tagesgeschäft eine Rolle spielen:

- **Lagerplatztyp** — beschreibt die relative Größe oder die tatsächlichen Maße
- **Platzzugriffstyp** — steuert, welche Ressourcen auf den Platz zugreifen dürfen
- **RF-Verifikationsfeld** — beim Scannen per Funkgerät (RF) die Kontrolle, dass der richtige Platz angefahren wird
- **Geokoordinaten** — zur Berechnung von Wegen und Entfernungen zwischen Plätzen
- **Brandabschnitt** — im Berichtswesen für Gefahrstoffe genutzt

## Der Aktivitätsbereich: Plätze für eine Tätigkeit bündeln

Neben der reinen Raumhierarchie gibt es eine zweite, quer dazu liegende Ordnung: den **Aktivitätsbereich**. Lageraktivitäten wie Einlagern, Kommissionieren und Inventur werden in solchen Bereichen organisiert. Ein Aktivitätsbereich besteht aus einem oder mehreren zugeordneten Lagerplätzen.

Das Besondere daran:

- Ein Lagerplatz kann je nach Tätigkeit **mehreren Aktivitätsbereichen** zugeordnet sein
- Für die Sortierung dienen Merkmale des Lagerplatzes wie Gang, Säule oder Ebene als Kriterien — so entsteht eine sinnvolle Laufreihenfolge
- Aktivitätsbereiche sind **grundsätzlich optional** — mit einer Ausnahme

Diese Ausnahme ist die **Inventur**: Dort ist der Aktivitätsbereich Pflicht. Für alle anderen Aktivitäten kannst du ihn nutzen, musst es aber nicht.

## Wie sieht eine komplette Lagerstruktur aus?

Zur Veranschaulichung ein illustratives Beispiel — ein Lager mit der Lagernummer `1010` und mehreren Lagertypen, die zusammen den Weg der Ware durch das Lager abbilden:

| Lagertyp | Funktion | Beispiel-Bereiche |
| --- | --- | --- |
| `0010` Hochregal | Lagerung | Schnelldreher, Langsamdreher |
| `9010` Bereitstellung Eingang | Wareneingangszone | Eingang (GR-Zone) |
| `8010` Dekonsolidierung | Auflösen von Anlieferungen | Deko |
| `0050` Festplätze | feste Stellplätze | gesamt |
| `8020` Verpackung | Packen | Pack-Eingang, Arbeit |
| `9020` Bereitstellung Ausgang | Warenausgangszone | Ausgang 1, Ausgang 2 |
| `9050` Yard | angrenzender Hof | Prüfung, Tore |

So bewegt sich eine Ware von der Anlieferung (Eingangszone) über die Lagerung (Hochregal) bis zum Versand (Ausgangszone) — und jede Station ist ein Lagertyp mit seinen Bereichen und Plätzen.

## Was Anwender im Alltag mit der Struktur zu tun haben

Die Lagerstruktur legt nicht der einzelne Lagerist täglich an. Sie wird einmalig beim Aufbau des Lagers oder bei Erweiterungen über das Customizing eingerichtet. Im Tagesgeschäft aber bewegt sich **jeder Anwender ständig in dieser Struktur**. Konkret zum Beispiel, wenn du:

- **einen Wareneingang verbuchst** — du wählst die Ziel-Lagernummer, und das System schlägt anhand von Lagertyp und Lagerbereich den passenden Lagerplatz vor
- **eine Lageraufgabe bearbeitest** — sie sagt dir „von Lagerplatz A nach Lagerplatz B“
- **einen Scan durchführst** — du bestätigst per RF die Platzkoordinate
- **eine Inventur machst** — sie ist nach Aktivitätsbereichen organisiert

In all diesen Fällen bewegst du dich entlang der Kette **Lagernummer → Lagertyp → Lagerbereich → Lagerplatz**. Wer diese vier Ebenen einmal sauber auseinanderhält, versteht auf einen Schlag einen großen Teil dessen, was im Lager passiert.

## Kurz zusammengefasst

Die Lagerstruktur in SAP EWM übersetzt ein reales Lager in vier klare Ebenen: Die **Lagernummer** ist das gesamte Lager, der **Lagertyp** ein Bereich darin, der **Lagerbereich** eine Gruppe ähnlicher Plätze und der **Lagerplatz** der einzelne Stellplatz mit seiner eindeutigen Koordinate. Quer dazu bündelt der **Aktivitätsbereich** Plätze für eine bestimmte Tätigkeit — Pflicht nur bei der Inventur. Wer diese Bausteine kennt, liest jede Lageraufgabe, jeden Scan und jede Einlagerung wie eine Landkarte.

## Häufige Fragen

### Was ist die Lagerstruktur in SAP EWM?

Die Lagerstruktur in SAP EWM ist die hierarchische Abbildung eines realen Lagers im System. Sie geht von oben nach unten: Die Lagernummer steht für das gesamte Lager, der Lagertyp für einen Bereich darin, der Lagerbereich für eine Gruppe ähnlicher Plätze und der Lagerplatz für den einzelnen Stellplatz. So weiß das System jederzeit, wo eine Ware physisch liegt.

### Was ist der Unterschied zwischen Lagertyp und Lagerbereich?

Ein Lagertyp ist eine physische oder logische Unterteilung des Lagers, etwa ein Hochregal, ein Wareneingangsbereich oder ein Kommissionierbereich. Ein Lagerbereich liegt eine Ebene tiefer und fasst innerhalb eines Lagertyps mehrere Lagerplätze mit ähnlichen Eigenschaften zusammen, zum Beispiel schwere Teile oder Schnelldreher.

### Wie viele Zeichen hat eine Lagernummer in SAP EWM?

Die Lagernummer in SAP EWM ist vierstellig. Im klassischen SAP-ERP-Lager ist das entsprechende Feld dagegen nur dreistellig. Wird ein Lager über EWM geführt, wird die ERP-Lagernummer als EWM-relevant markiert und mit der vierstelligen EWM-Lagernummer verbunden.

### Wann ist ein Aktivitätsbereich in SAP EWM Pflicht?

Ein Aktivitätsbereich ist grundsätzlich optional und bündelt Lagerplätze für eine bestimmte Tätigkeit wie Einlagern, Kommissionieren oder Inventur. Verpflichtend ist er nur für die Inventur — für alle anderen Aktivitäten kannst du ihn nutzen, musst es aber nicht.

### Muss ein Anwender die Lagerstruktur selbst anlegen?

Nein. Die Lagerstruktur wird einmalig beim Aufbau des Lagers oder bei Erweiterungen über das Customizing eingerichtet. Im Tagesgeschäft bewegt sich jeder Anwender aber in dieser Struktur: Bei Wareneingang, Lageraufgabe, Scan oder Inventur arbeitest du immer entlang der Hierarchie Lagernummer, Lagertyp, Lagerbereich, Lagerplatz.
