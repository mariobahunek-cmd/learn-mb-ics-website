---
layout: post
lang: de
title: "SAP S/4HANA vs. SAP ECC: was sich für Anwender geändert hat"
description: "Universal Journal, Geschäftspartner, Fiori, vereinfachtes Datenmodell: die wichtigsten Unterschiede zwischen SAP ECC und S/4HANA — für Anwender klar erklärt."
slug: s4hana-vs-ecc-fuer-anwender
permalink: /blog/de/s4hana-vs-ecc-fuer-anwender/
translation_key: post-s4hana-vs-ecc
date: 2026-07-08
category: "Grundlagen"
keywords: "S/4HANA vs ECC, SAP S/4HANA Unterschiede, Universal Journal, ACDOCA, Geschäftspartner, Business Partner, SAP Fiori, vereinfachtes Datenmodell, SAP Anwender"
reading_time: 10
sources:
  - label: "SAP Help Portal — SAP S/4HANA"
    url: "https://help.sap.com/"
    note: "Bereich SAP S/4HANA — allgemeine Grundlagen zu Datenmodell, Geschäftspartner und Oberfläche. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der Hauptunterschied zwischen SAP ECC und SAP S/4HANA?"
    a: "SAP ECC lief auf klassischen relationalen Datenbanken und trennte operative Daten von Auswertungen. S/4HANA läuft ausschließlich auf der In-Memory-Datenbank SAP HANA, nutzt ein vereinfachtes Datenmodell mit weniger Tabellen und bringt Auswertungen direkt ins operative System zurück."
  - q: "Was ist das Universal Journal in S/4HANA?"
    a: "Das Universal Journal ist ein einziges, gemeinsames Journal (technisch die Tabelle ACDOCA), in das Finanzbuchhaltung und Controlling parallel schreiben. Statt vieler getrennter Tabellen und späterer Abstimmung liegen alle rechnungswesenrelevanten Buchungen an einer Stelle."
  - q: "Gibt es in S/4HANA noch Debitoren und Kreditoren?"
    a: "Die Begriffe existieren weiter, aber nur noch als Rollen eines zentralen Geschäftspartners. Kunden- und Lieferantendaten werden nicht mehr als getrennte Stammsätze gepflegt, sondern über Rollen an einem Geschäftspartner abgebildet."
  - q: "Muss ich in S/4HANA noch die alte SAP GUI benutzen?"
    a: "Die klassische SAP GUI bleibt für Power-User und Spezialtransaktionen erhalten, ist aber nicht mehr der Standard-Einstieg. Standard ist das rollenbasierte SAP Fiori Launchpad; klassische Transaktionen lassen sich von dort weiterhin aufrufen."
  - q: "Bleiben meine bekannten Organisationsstrukturen in S/4HANA gleich?"
    a: "Ja. Buchungskreise, Werke, Kostenstellen und Sachkonten bleiben als Strukturen bestehen. Geändert hat sich vor allem die Architektur darunter: ein vereinfachtes Datenmodell, eine integrierte Plattform und eine moderne Oberfläche."
---

„Bleibt eigentlich irgendwas, wie es war?“ Diese Frage kommt in fast jeder Umstellungsrunde. Die ehrliche Antwort: Fachlich buchst du weiter Rechnungen, legst Bestellungen an und bearbeitest Kundenaufträge wie bisher. Was sich ändert, sitzt eine Ebene tiefer, im Datenmodell, in den Stammdaten und an der Oberfläche. „Muss ich jetzt alles komplett neu lernen?“ — so fragen Teilnehmer oft. Die größte Sorge, dass jetzt alles anders wird, trifft den Alltag kaum, sondern die Architektur darunter. Genau die Begriffe, die dabei neu auftauchen, sortieren wir hier ein: Universal Journal, Geschäftspartner, Embedded Analytics, Fiori Launchpad.

## Gleiche Prozesse, neue Architektur

SAP S/4HANA ist der Nachfolger von SAP ECC (dem alten „SAP ERP“). Fachlich machst du dieselben Dinge: Bestellungen anlegen, Rechnungen buchen, Kundenaufträge bearbeiten. Was sich ändert, ist die Architektur darunter: S/4HANA läuft ausschließlich auf der In-Memory-Datenbank SAP HANA, nutzt ein deutlich **vereinfachtes Datenmodell** und bringt eine moderne, rollenbasierte Oberfläche mit. Für dich als Anwender heißt das: weniger doppelte Datenhaltung, Echtzeit-Auswertungen und ein aufgeräumter Zugang zu deinen Aufgaben.

## Warum überhaupt der Schritt von ECC auf S/4HANA?

SAP ECC (ERP Central Component) lief jahrzehntelang auf klassischen relationalen Datenbanken wie Oracle, DB2 oder SQL Server. Daten wurden zeilenorientiert gespeichert, und Auswertungen holte man sich meist aus separaten Reporting-Systemen wie SAP BW — sonst wäre das Tagesgeschäft zu langsam geworden. Doppelte Datenhaltung, Aggregationstabellen und nächtliche Batch-Läufe gehörten zum Alltag.

SAP S/4HANA bricht damit: Die Suite läuft nur noch auf SAP HANA, einer In-Memory-Datenbank. Daten liegen spaltenorientiert im Hauptspeicher, und Summen werden zur Laufzeit berechnet, statt redundant gespeichert zu werden. Aus Anwendersicht bedeutet das Echtzeitprozesse, Analyse und Tagesgeschäft aus derselben Datenquelle, weniger Redundanz und schlankere Tabellen.

Die wichtigsten Effekte für Anwender im Überblick:

- Eine Datenquelle für Transaktion und Auswertung: kein ständiger Wechsel zwischen operativem System und Data Warehouse für Standardberichte
- Vereinfachtes Datenmodell mit weniger Tabellen, weniger Belegen und kürzeren Schreibwegen
- Moderne Oberfläche über SAP Fiori, rollenbasiert, browserfähig und mobil nutzbar
- Eingebettete Auswertungen direkt im operativen System
- Vorkonfigurierte Best Practices, die branchenspezifisch mitgeliefert werden

Diese Vereinfachung, auf Englisch oft „Simplification“ genannt, ist der rote Faden hinter allen Detailänderungen, die wir uns jetzt anschauen.

## Universal Journal: das neue Herz des Rechnungswesens

Wer in einem ECC-System schon einmal eine Buchung nachvollzogen hat, kennt das Problem: Die Finanzbuchhaltung (FI) bucht in ihre Tabellen, das Controlling (CO) in andere, die Anlagenbuchhaltung pflegt eigene Belege, das Material-Ledger noch andere. Abgleich, Abstimmung, periodische Verrechnung — und am Ende passt das Reporting trotzdem nur fast.

S/4HANA löst das mit dem **Universal Journal** (technisch die Tabelle ACDOCA, kurz für „Accounting Document Actual“). Die Kernidee: *ein einziges, umfassendes Journal* für alle rechnungswesenrelevanten Buchungen. Externe Finanzbuchhaltung (FI) und internes Rechnungswesen (CO) schreiben in dieselbe Tabelle und teilen sich dieselben Sachkonten.

Damit verschwindet die alte, harte Trennung zwischen FI-Konten und CO-Kostenarten. Der Kontenplan enthält jetzt sowohl klassische Sachkonten als auch Sachkonten vom Typ *Kosten*. Bei der Anlage eines Sachkontos legt man über die Sachkontoart fest, welcher Typ vorliegt — etwa Primärkosten/Erlöse, Sekundärkosten, ein Bestandskonto oder ein Geldkonto.

Was heißt das konkret für den Anwender?

- Ein Buchungsbeleg enthält in einem Schritt FI- und CO-Informationen — kein nachträglicher Abgleich mehr.
- Aus Bilanz und GuV ist ein Drill-Down bis zum Originalbeleg möglich (etwa bis zur Bestellung oder Lieferantenrechnung).
- Berichte auf Profitcenter-, Segment- oder Geschäftsbereichsebene laufen ohne separates Profit-Center-Ledger.
- Reale Buchungen erfolgen auf die Kostenstelle (oder einen anderen Kontierungsempfänger), statistische Buchungen laufen parallel ans Profitcenter.

Das Universal Journal ist mit Abstand der wichtigste Unterschied im Rechnungswesen.

## Geschäftspartner statt getrennter Kunden- und Lieferantenstämme

In SAP ECC musste man für jeden Geschäftspartner zwei Stammsätze pflegen: einen **Kundenstamm** für die Vertriebsseite und einen **Lieferantenstamm** für die Einkaufsseite. War ein Partner gleichzeitig Kunde und Lieferant (im B2B häufig der Fall), wurde vieles doppelt gepflegt: Adresse, Bankverbindung, Kommunikationsdaten. Inkonsistenzen waren vorprogrammiert.

S/4HANA macht den **Geschäftspartner**-Ansatz (Business Partner, BP) verpflichtend. Der Geschäftspartner ist das zentrale Stammdatenobjekt — Kunden- und Lieferantendaten werden über Rollen abgebildet, nicht mehr über getrennte Stammsätze.

So sieht die Struktur in der Praxis aus:

| Ebene | Beispielinhalt |
| --- | --- |
| Allgemeine Daten (Mandantenebene) | Name, Anschrift, Kommunikation, Geschäftspartnerkategorie |
| Rolle „FI-Debitor“ | Buchungskreis-spezifisch: Abstimmkonto, Zahlungsbedingungen, Zahlwege |
| Rolle „Kunde“ (Vertrieb) | Vertriebsbereichsdaten: Auftragswährung, Lieferbedingungen |
| Rolle „FI-Kreditor“ | Buchungskreis-spezifisch: Abstimmkonto, Zahlwege |
| Rolle „Lieferant“ (Einkauf) | Einkaufsorganisations-Daten |

Drei Geschäftspartnerkategorien sind möglich: **Person**, **Gruppe** (etwa ein Ehepaar oder eine Wohngemeinschaft) und **Organisation** (eine juristische Person, Abteilung oder ein Verband).

Wichtig zu verstehen: Debitor und Kreditor existieren in S/4HANA als Begriffe weiterhin — aber nur noch als *Rollen* eines Geschäftspartners, nicht mehr als eigenständige Stammsätze. Wer die Adresse einmal am Geschäftspartner pflegt, hat sie für alle Rollen konsistent.

## SAP Fiori: die neue Anwender-Oberfläche

Die klassische SAP GUI mit ihrem Easy-Access-Menü und Transaktionscodes hat in S/4HANA nicht ausgedient, ist aber nicht mehr der primäre Einstieg. An ihre Stelle tritt das **SAP Fiori Launchpad** — eine rollenbasierte Web-Oberfläche mit Kacheln, zentraler Suche und persönlicher Startseite.

Der Unterschied ist mehr als kosmetisch. Eine GUI-Transaktion zeigt typischerweise viele Felder und Reiter gleichzeitig; eine Fiori-App ist dagegen auf eine konkrete Aufgabe zugeschnitten — eine Bestellung freigeben, einen Kundenauftrag anlegen, offene Posten prüfen. Die typischen Vorteile:

- Effizienteres Arbeiten, weil relevante Apps und Informationen ohne Umwege erreichbar sind
- Schnellere Entscheidungen dank Hinweisen, die direkt auf der Startseite einlaufen
- Bessere Akzeptanz im Tagesgeschäft durch ein einheitliches, mobiltaugliches Design
- Rollenbasierter Zugriff, sodass jeder nur die Kacheln sieht, die zu seiner Tätigkeit passen

Dabei gibt es drei wichtige App-Typen:

1. **Transaktionale Apps**: operative Vorgänge wie Anlegen, Ändern, Buchen
2. **Fact-Sheet-Apps**: kontextbezogene Detailansicht eines Objekts (Bestellung, Material, Geschäftspartner)
3. **Analytische Apps**: Kennzahl-Kacheln mit Echtzeitdaten und Drill-Down ins Belegdetail

Die alte SAP GUI bleibt für Power-User und administrative Transaktionen verfügbar. Der Standard-Einstieg in S/4HANA ist aber das Fiori Launchpad.

## Embedded Analytics: Echtzeit-Auswertungen im System

In der ECC-Welt war Reporting ein eigenes Universum: Daten wurden per Extraktor nach SAP BW geladen, dort modelliert und aggregiert und über eigene Werkzeuge bereitgestellt. Aktuelle Zahlen gab es frühestens nach dem Nachtlauf.

S/4HANA bringt mit **Embedded Analytics** das operative Reporting direkt ins Transaktionssystem zurück. Möglich wird das durch zwei Bausteine:

- Das **virtuelle Datenmodell (VDM)** — eine semantische Schicht aus sogenannten CDS-Views, die fertig aufbereitete Blickwinkel auf das Universal Journal und weitere Tabellen liefert, ohne die Daten zu kopieren.
- Die In-Memory-Geschwindigkeit von SAP HANA, die Summenbildung erst zur Laufzeit erlaubt.

Für Endanwender sind dabei vor allem drei Werkzeuge relevant. Der Abfrage-Browser (Query Browser) listet die verfügbaren CDS-Views auf, sodass Anwender ohne IT eigene Auswertungen starten. Analytische Fiori-Apps liefern vorgefertigte Auswertungs-Kacheln direkt im Launchpad. Und die SAP Smart Business Cockpits bündeln Kennzahl-Dashboards für Führungskräfte.

Wichtig fürs Verständnis: Embedded Analytics ersetzt nicht das klassische Data Warehouse für strategisches Reporting über viele Jahre und Quellsysteme hinweg. Für operative Echtzeitauswertungen ist es aber das neue Standardwerkzeug.

## SAP Activate: die neue Einführungsmethodik

Ein kurzer Blick über den Tellerrand, mehr zum Einordnen als für den Alltag: Auch die Methodik, mit der SAP-Projekte umgesetzt werden, hat sich geändert. Als Anwender führst du kein Migrationsprojekt selbst durch, aber die Begriffe tauchen in Projektmeetings auf. Die früher übliche ASAP-Methodik ist durch **SAP Activate** abgelöst, ein Framework aus drei Säulen:

1. **SAP Best Practices**: sofort einsatzfähige, branchenspezifisch optimierte Geschäftsprozesse, die bereits vorkonfiguriert im System liegen
2. **Methodik**: eine modulare Roadmap mit klar abgegrenzten Phasen
3. **Geführte Konfiguration**: Werkzeuge, die Best Practices im Kundensystem aktivieren

Die Phasen der SAP-Activate-Roadmap:

| Phase | Was passiert? |
| --- | --- |
| Erkunden (Discover) | Testversion ausprobieren, erste Erfahrung in vorkonfigurierten Szenarien sammeln |
| Vorbereiten (Prepare) | Projekt aufsetzen, eigene Szenarien einrichten, Beispiele aus Best Practices nutzen |
| Kennenlernen (Explore) | Fit/Gap-Analyse — wie muss das System an Kundenanforderungen angepasst werden? |
| Umsetzen (Realize) | Konfiguration, Datenmigration, Erweiterungen und Integration |
| Bereitstellen (Deploy) | Vorbereitung auf den Produktivstart, Anwenderschulungen |
| Ausführen (Run) | Laufender Betrieb, Überwachung, kontinuierliche Optimierung |

SAP Activate unterstützt drei Übergangsszenarien: **Neue Implementierung** (Greenfield), **Systemkonvertierung** (Brownfield, also der ECC-Umstieg ohne Reimplementierung) und **Transformation der Landschaft** (etwa die Konsolidierung mehrerer Altsysteme). Wichtig: Eine Systemkonvertierung ist *kein Upgrade* — es findet ein Wechsel von einem SAP-Produkt (ECC) auf ein anderes (S/4HANA) statt.

## Weitere Änderungen im Schnellüberblick

Neben den großen Themen gibt es einige kleinere, aber praktisch relevante Detailunterschiede:

| Bereich | SAP ECC | SAP S/4HANA |
| --- | --- | --- |
| Datenbank | verschiedene Datenbanken (Oracle, DB2, MaxDB, MSSQL) | ausschließlich SAP HANA (In-Memory) |
| Hauptbuch | viele getrennte Tabellen | Universal Journal (ACDOCA) |
| Kunde / Lieferant | separate Stammsätze | Geschäftspartner mit Rollen |
| Material | Materialnummer, bis 18 Stellen | Produktstammdaten, bis 40 Stellen |
| Oberfläche | SAP GUI als Standard | Fiori Launchpad als Standard |
| Reporting | vorwiegend SAP BW | Embedded Analytics plus BW für Strategie |
| Materialplanung | klassischer MRP-Lauf | MRP Live (auf HANA) |
| Betriebsmodell | primär On-Premise | Cloud- und On-Premise-Varianten |

Hinzu kommen die Cloud-Angebote **RISE with SAP** (Modernisierung großer Bestandskunden) und **GROW with SAP** (für mittelständische Neukunden), beides sind Lizenz- und Service-Pakete, die die Cloud-Einführung beschleunigen sollen. Für den Überblick reicht es, beide Begriffe einordnen zu können.

## Häufige Stolpersteine

- **ECC-Reflexe mitnehmen.** Wer gewohnt ist, Kunde und Lieferant getrennt zu pflegen oder für jede Auswertung ins Data Warehouse zu wechseln, arbeitet in S/4HANA umständlicher als nötig. Der Geschäftspartner und die eingebetteten Auswertungen sind die neuen Standardwege.
- **Systemkonvertierung mit Upgrade verwechseln.** Besonders oft geraten Greenfield und Brownfield durcheinander. Der Brownfield-Umstieg ist ein Produktwechsel von ECC auf S/4HANA, kein reines Release-Upgrade, auch wenn historische Daten und Customizing weitgehend erhalten bleiben.
- **Fiori für reine Kosmetik halten.** Die neue Oberfläche ändert nicht nur die Optik, sondern den Zuschnitt der Arbeit: aufgabenbezogene Apps statt großer Sammel-Transaktionen.

## Worauf es ankommt

SAP S/4HANA ist keine kosmetische Modernisierung von SAP ECC. Die zentralen Konzepte, also Universal Journal, Geschäftspartner, Fiori als Standard-Oberfläche, Embedded Analytics und SAP Activate als Einführungsmethodik, verändern die Art, wie Anwender mit dem System arbeiten.

Die gute Nachricht: Vieles, was du aus ECC kennst, wirkt in S/4HANA weiterhin im Hintergrund. Buchungskreise, Werke, Kostenstellen und Sachkonten sind dieselben geblieben. Geändert hat sich vor allem die *Architektur darunter* — ein vereinfachtes Datenmodell, eine integrierte Plattform und eine moderne Oberfläche. Wer diesen Perspektivwechsel einmal verinnerlicht hat, findet sich in S/4HANA schnell zurecht.

## Häufige Fragen

### Was ist der Hauptunterschied zwischen SAP ECC und SAP S/4HANA?

SAP ECC lief auf klassischen relationalen Datenbanken und trennte operative Daten von Auswertungen. S/4HANA läuft ausschließlich auf der In-Memory-Datenbank SAP HANA, nutzt ein vereinfachtes Datenmodell mit weniger Tabellen und bringt Auswertungen direkt ins operative System zurück.

### Was ist das Universal Journal in S/4HANA?

Das Universal Journal ist ein einziges, gemeinsames Journal (technisch die Tabelle ACDOCA), in das Finanzbuchhaltung und Controlling parallel schreiben. Statt vieler getrennter Tabellen und späterer Abstimmung liegen alle rechnungswesenrelevanten Buchungen an einer Stelle.

### Gibt es in S/4HANA noch Debitoren und Kreditoren?

Die Begriffe existieren weiter, aber nur noch als Rollen eines zentralen Geschäftspartners. Kunden- und Lieferantendaten werden nicht mehr als getrennte Stammsätze gepflegt, sondern über Rollen an einem Geschäftspartner abgebildet.

### Muss ich in S/4HANA noch die alte SAP GUI benutzen?

Die klassische SAP GUI bleibt für Power-User und Spezialtransaktionen erhalten, ist aber nicht mehr der Standard-Einstieg. Standard ist das rollenbasierte SAP Fiori Launchpad; klassische Transaktionen lassen sich von dort weiterhin aufrufen.

### Bleiben meine bekannten Organisationsstrukturen in S/4HANA gleich?

Ja. Buchungskreise, Werke, Kostenstellen und Sachkonten bleiben als Strukturen bestehen. Geändert hat sich vor allem die Architektur darunter: ein vereinfachtes Datenmodell, eine integrierte Plattform und eine moderne Oberfläche.
