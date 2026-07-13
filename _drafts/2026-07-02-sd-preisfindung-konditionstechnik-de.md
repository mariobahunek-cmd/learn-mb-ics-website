---
layout: post
lang: de
title: "SAP SD Preisfindung mit der Konditionstechnik verständlich erklärt"
description: "Konditionsart, Zugriffsfolge, Konditionstabelle, Konditionssatz, Kalkulationsschema: So findet SAP S/4HANA im Kundenauftrag den Preis — klar erklärt."
slug: sd-preisfindung-konditionstechnik
permalink: /blog/de/sd-preisfindung-konditionstechnik/
translation_key: post-sd-pricing
date: 2026-07-08
category: "Vertrieb"
keywords: "SAP SD Preisfindung, Konditionstechnik, Konditionsart, Zugriffsfolge, Konditionstabelle, Konditionssatz, Kalkulationsschema, S/4HANA Sales"
reading_time: 10
sources:
  - label: "SAP Help Portal — Pricing in Sales (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Sales / Vertrieb — allgemeine Grundlagen zur Preisfindung und Konditionstechnik. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist die Konditionstechnik in SAP SD?"
    a: "Die Konditionstechnik ist das Regelwerk, mit dem SAP S/4HANA im Vertrieb automatisch Preise, Rabatte, Zuschläge und Steuern ermittelt. Sie besteht aus fünf zusammenspielenden Objekten und legt fest, welcher Wert unter welchen Bedingungen in einen Verkaufsbeleg übernommen wird."
  - q: "Was ist der Unterschied zwischen Konditionsart und Konditionssatz?"
    a: "Die Konditionsart beschreibt, was ermittelt wird — etwa ein Materialpreis oder ein Kundenrabatt — und ist eine Einstellung im Customizing. Der Konditionssatz ist der konkrete Wert dazu, zum Beispiel „74 EUR für dieses Material bei diesem Kunden“, und wird als Stammdatum im Tagesgeschäft gepflegt."
  - q: "Wozu dient die Zugriffsfolge?"
    a: "Die Zugriffsfolge ist die Suchstrategie einer Konditionsart. Sie legt fest, in welcher Reihenfolge das System nach passenden Konditionssätzen sucht — vom spezifischsten Zugriff (etwa Kunde und Material) bis zum allgemeinsten (nur Material). Der erste Treffer gewinnt und beendet die Suche."
  - q: "Was ist ein Kalkulationsschema?"
    a: "Das Kalkulationsschema ist die geordnete Liste aller Konditionsarten, die ein Beleg durchläuft — von der Basispreis-Zeile über Rabatte und Zuschläge bis zur Steuer, inklusive Zwischensummen. Im Englischen heißt es „pricing procedure“; beide Begriffe meinen dasselbe."
  - q: "Warum gewinnt bei zwei passenden Preisen der spezifischere?"
    a: "Weil die Zugriffsfolge vom Spezifischen zum Allgemeinen sortiert ist und das System die Suche beim ersten Treffer abbricht. Ein Konditionssatz für „Kunde und Material“ wird vor dem allgemeinen Satz für „Material“ geprüft und übersteuert ihn deshalb automatisch — ohne dass man etwas abschalten muss."
---

Legst du in SAP einen Kundenauftrag an, erscheint plötzlich ein Stückpreis, ein Rabatt wird automatisch abgezogen und am Ende landet noch die Mehrwertsteuer in der Position. Was wie Magie aussieht, ist in Wahrheit ein klar definiertes Regelwerk: die Konditionstechnik. Hand aufs Herz: Bei der Konditionstechnik stutzen die meisten zuerst und fragen, woher das System den Preis eigentlich nimmt. Die Antwort steckt in fünf Objekten, die ineinandergreifen.

## Worum es im Kern geht

Die Konditionstechnik ist der Mechanismus, mit dem SAP S/4HANA im Vertrieb automatisch ermittelt, welcher Preis, welcher Rabatt, welcher Zuschlag und welche Steuer in einen Verkaufsbeleg übernommen werden. Sie besteht aus fünf Objekten, die ineinandergreifen. Der große Vorteil: Du kannst Preise und Rabatte von fast jedem Belegfeld abhängig machen: vom Kunden, der Materialgruppe, der Verkaufsorganisation oder einer Kombination daraus.

Dieselbe Logik steckt nicht nur hinter der Preisfindung. Auch die Nachrichtenfindung, die Erlöskontenfindung und weitere Automatismen im System bauen darauf auf. Wer die Konditionstechnik einmal verstanden hat, versteht damit viele Findungsmechanismen auf einen Schlag.

## Was ist die Konditionstechnik in SAP SD?

Beim Anlegen eines Kundenauftrags schaut SAP nicht einfach in ein Feld „Preis“ im Materialstamm. Stattdessen läuft im Hintergrund ein definierter Such- und Berechnungsprozess ab. Dieser Prozess wird vollständig im Customizing eingerichtet, also in den Systemeinstellungen, die normalerweise ein Berater vornimmt, und besteht aus mehreren verzahnten Objekten.

Genau diese Flexibilität ist der Grund, warum die Konditionstechnik so mächtig und für Einsteiger zunächst so verwirrend ist. Sobald du die fünf Bausteine und ihr Zusammenspiel kennst, verschwindet die Verwirrung.

## Die fünf Bausteine im Überblick

Bevor wir ein Beispiel rechnen, lohnt es sich, die zentralen Objekte einmal sauber auseinanderzuhalten:

- **Konditionsart** — beschreibt, *was* ermittelt wird (zum Beispiel ein Materialpreis, ein Kundenrabatt, ein Frachtzuschlag). Sie steuert Eigenschaften wie die Konditionsklasse (Preis, Abschlag, Zuschlag, Steuer), zulässige Staffeln, den Gültigkeitszeitraum und ob der Wert auf Kopf- oder Positionsebene wirkt.
- **Zugriffsfolge** — definiert die *Suchstrategie*: In welcher Reihenfolge sucht das System nach passenden Werten? Erst „Kunde und Material“, dann „Preisliste und Material“, dann „Material“ allein? Jede Zugriffsfolge ist einer Konditionsart fest zugeordnet.
- **Konditionstabelle** — die konkrete Feldkombination, unter der ein Wert gespeichert wird (zum Beispiel die Kombination aus Verkaufsorganisation, Vertriebsweg, Kunde und Material).
- **Konditionssatz** — der eigentliche Datensatz mit dem tatsächlichen Wert, etwa „Für diese Verkaufsorganisation, diesen Kunden und dieses Material gilt ein Stückpreis von 74 EUR“.
- **Kalkulationsschema** — die geordnete Liste aller Konditionsarten, die ein Beleg durchläuft, inklusive Zwischensummen, Berechnungsformeln und Bedingungen.

Im Englischen heißt das Kalkulationsschema „pricing procedure“. Beide Begriffe bedeuten dasselbe. Manchmal liest man auch „Konditionsschema“; auch das meint dasselbe Objekt.

## Wie ist ein Kalkulationsschema aufgebaut?

Ein Kalkulationsschema ist im Kern eine Tabelle mit Zeilen. Jede Zeile ist eine Konditionsart, jede Zeile hat eine **Stufe** (die Reihenfolge der Abarbeitung) und einen **Zähler** (die Sortierung innerhalb einer Stufe). So könnte ein stark vereinfachtes Schema für die Preisfindung im Vertrieb aussehen:

| Stufe | Konditionsart | Bedeutung | Wirkung |
| --- | --- | --- | --- |
| 10 | Materialpreis | Basispreis | + Brutto-Stückpreis |
| 100 | Kundenrabatt (%) | prozentualer Abschlag | − Abschlag |
| 110 | Kunden-/Materialrabatt | absoluter Abschlag | − Abschlag |
| 200 | Zwischensumme | Netto vor Fracht | = Netto-Position |
| 300 | Frachtzuschlag | Frachtkosten | + Zuschlag |
| 400 | Mehrwertsteuer | Ausgangssteuer | + Steuer auf Netto |
| 900 | Endbetrag | Brutto-Position | = zu zahlender Betrag |

Das System arbeitet das Schema strikt von oben nach unten ab. Für jede Zeile prüft es: „Gibt es zu dieser Konditionsart einen gültigen Konditionssatz für diese Position?“ Wenn ja, übernimmt es den Wert in den Beleg. Wenn nein, wird die Zeile übersprungen, es sei denn, die Konditionsart ist als Mussbedingung markiert; dann bliebe der Beleg unvollständig.

Welches Kalkulationsschema überhaupt zum Einsatz kommt, entscheidet SAP über zwei Schlüssel: das **Belegschema** (kommt aus der Verkaufsbelegart) und das **Kundenschema** (kommt aus dem Verkaufsbereichsbild des Kundenstamms). Aus der Kombination beider Schlüssel plus der Verkaufsorganisation ermittelt das System das passende Schema. Diesen Schritt nennt man Schemafindung.

## Wie legt man einen Konditionssatz an?

Damit aus dem leeren Kalkulationsschema echte Preise werden, brauchst du Konditionssätze. Sie sind Stammdaten und werden im Tagesgeschäft gepflegt — klassisch über eine Pflegetransaktion, in S/4HANA auch über eine entsprechende Fiori-App wie „Preise festlegen“. Die Logik dahinter: Anlegen, Ändern und Anzeigen sind getrennte Funktionen.

Stell dir vor, du hast mit einem Großkunden eine mengenabhängige Preisstaffel vereinbart und willst sie so hinterlegen, dass sie nicht bei jedem Auftrag manuell erfasst werden muss. Der Weg dorthin:

1. **Konditionsart wählen.** Du gibst die Konditionsart ein — für einen Materialpreis ist das die entsprechende Preis-Konditionsart.
2. **Schlüsselkombination wählen.** SAP fragt: „Auf welcher Ebene soll der Preis gelten?“ Du wählst zum Beispiel „Kunde und Material“, weil der Preis nur für diesen einen Kunden gelten soll. Hinter dieser Auswahl steckt eine Konditionstabelle.
3. **Organisationsdaten und Schlüssel eingeben.** Verkaufsorganisation, Vertriebsweg, Kunde und Material — also die Felder der gewählten Konditionstabelle.
4. **Staffel pflegen.** Über die Staffel-Funktion hinterlegst du beispielsweise drei Preisstufen: ab 1 Stück 78 EUR, ab 25 Stück 74 EUR, ab 250 Stück 68 EUR. Damit ist der Mengenrabatt für deinen Großabnehmer vollständig im System abgebildet.
5. **Gültigkeit prüfen.** Konditionssätze haben immer einen Gültigkeitszeitraum (von/bis). Bei zeitlich befristeten Aktionen solltest du diesen Zeitraum bewusst anpassen.
6. **Sichern.** Der Konditionssatz wird gespeichert und steht ab sofort für die Preisfindung bereit.

Erfasst der Vertrieb jetzt einen Auftrag über 60 Stück dieses Materials für genau diesen Kunden, zieht SAP automatisch den Stückpreis von 74 EUR — die mittlere Staffelstufe greift, weil 60 zwischen 25 und 250 Stück liegt. Auf der Registerkarte „Konditionen“ der Position lässt sich die Ermittlung Schritt für Schritt nachvollziehen.

## Wie sucht das System bei der Preisfindung?

Hier steckt das vielleicht wichtigste Konzept. Eine Preis-Konditionsart hat in der Regel eine Zugriffsfolge mit *mehreren* Zugriffen, vom spezifischsten zum allgemeinsten. Zum Beispiel:

| Zugriff | Schlüsselfelder | Spezifität |
| --- | --- | --- |
| 10 | Kunde / Material | sehr spezifisch |
| 20 | Preisliste / Währung / Material | mittel |
| 30 | Material | allgemein |

Beim Durchlauf einer Konditionsart füllt SAP die Schlüsselfelder des ersten Zugriffs aus dem Beleg (Kunde aus dem Kopf, Material aus der Position) und sucht in der zugehörigen Konditionstabelle nach einem gültigen Konditionssatz. Sobald ein Treffer gefunden wurde, bricht die Suche ab. Genau das ist der entscheidende Punkt. Erst wenn ein Zugriff leer ausgeht, wandert das System zum nächsten Zugriff.

Das hat zwei praktische Konsequenzen:

- Ein spezifischer Konditionssatz „Kunde und Material“ *übersteuert* automatisch einen allgemeinen Satz „nur Material“. Du musst nichts abschalten, die Reihenfolge erledigt das.
- Die *Reihenfolge der Zugriffe* innerhalb der Zugriffsfolge ist genauso kritisch wie die Reihenfolge der Konditionsarten im Kalkulationsschema. Eine falsch sortierte Zugriffsfolge kann dazu führen, dass Kundenrabatte oder Aktionspreise nie greifen.

## Welche Arten von Konditionen gibt es?

SAP liefert im Standard zahlreiche Konditionsarten aus. Für das Verständnis reicht es, die typischen Kategorien zu kennen:

- **Preis** — der Basispreis pro Material, häufig kunden- oder preislistenspezifisch und oft mit Mengenstaffel.
- **Abschlag (Rabatt)** — mindert den Preis, etwa als prozentualer Kundenrabatt auf alle Positionen oder als absoluter Rabatt für eine bestimmte Kunde-Material-Kombination.
- **Zuschlag** — erhöht den Preis, zum Beispiel ein Frachtzuschlag in Abhängigkeit vom Positionsgewicht.
- **Steuer** — die Ausgangssteuer, automatisch ermittelt über Land sowie die Steuerklassifikation von Kunde und Material.

Dabei lohnt es sich, drei Dinge auseinanderzuhalten. Die Konditionsklasse (Preis, Abschlag, Zuschlag, Steuer) entscheidet über Vorzeichen und Verbuchung. Die Rechenregel bestimmt, ob ein fester Betrag, ein Prozentwert, ein Mengensatz oder eine Staffel dahintersteckt. Und ob sich eine Konditionsart manuell überschreiben lässt, etwa wenn der Vertrieb einen Sonderrabatt einräumt, oder ob sie im Customizing gesperrt ist, wird pro Konditionsart hinterlegt.

## Stammdaten oder Customizing — was gehört wohin?

Ein häufiger Stolperstein ist die Verwechslung von Stammdaten und Customizing. Die Faustregel:

- **Customizing** (einmal vom Berater eingerichtet): Konditionsart, Zugriffsfolge, Konditionstabelle und Kalkulationsschema. Das ist das Regelwerk.
- **Stammdaten** (im Tagesgeschäft pflegbar): der Konditionssatz. Das ist der konkrete Wert innerhalb des Regelwerks.

Anders gesagt: Der Berater baut die Straße (Customizing), der Anwender legt die konkreten Preise darauf ab (Stammdaten). Wer diese beiden Ebenen sauber trennt, versteht sofort, warum ein neuer Preis kein Customizing braucht, eine neue Rabattlogik aber sehr wohl.

## Häufige Stolpersteine

Regelmäßig bringen Teilnehmer manuell erfasste und automatisch gefundene Konditionen durcheinander. Drei Stellen führen dabei besonders oft in die Irre:

- **Begriffe verwechseln.** Konditionsart, Konditionssatz, Konditionstabelle, Zugriffsfolge, Kalkulationsschema — diese Wörter klingen ähnlich. Ordne jedem sein „Was macht es?“ zu, dann verschwindet die Verwirrung.
- **Zugriffsfolge falsch sortieren.** Steht der allgemeine Zugriff vor dem spezifischen, greift der spezifische Preis nie. Immer vom Spezifischen zum Allgemeinen sortieren.
- **Denken, jede Zeile summiert sich.** Innerhalb einer Konditionsart wird nur *ein* Konditionssatz angezogen — der erste Treffer. Danach geht es zur nächsten Zeile im Schema.

## Worauf es ankommt

Die Konditionstechnik wirkt beim ersten Lesen wie ein Begriffsgewitter, folgt aber einem einfachen Grundprinzip: Ein Kalkulationsschema ist eine geordnete Liste von Konditionsarten. Für jede Konditionsart sucht eine Zugriffsfolge nacheinander in mehreren Konditionstabellen nach einem passenden Konditionssatz. Der erste Treffer gewinnt, dann geht es zur nächsten Zeile. Wer diese Logik einmal verinnerlicht hat, versteht nicht nur die Preisfindung im Vertrieb, sondern gleich eine ganze Familie von Findungsmechanismen in SAP.

## Häufige Fragen

### Was ist die Konditionstechnik in SAP SD?

Die Konditionstechnik ist das Regelwerk, mit dem SAP S/4HANA im Vertrieb automatisch Preise, Rabatte, Zuschläge und Steuern ermittelt. Sie besteht aus fünf zusammenspielenden Objekten und legt fest, welcher Wert unter welchen Bedingungen in einen Verkaufsbeleg übernommen wird.

### Was ist der Unterschied zwischen Konditionsart und Konditionssatz?

Die Konditionsart beschreibt, was ermittelt wird — etwa ein Materialpreis oder ein Kundenrabatt — und ist eine Einstellung im Customizing. Der Konditionssatz ist der konkrete Wert dazu, zum Beispiel „74 EUR für dieses Material bei diesem Kunden“, und wird als Stammdatum im Tagesgeschäft gepflegt.

### Wozu dient die Zugriffsfolge?

Die Zugriffsfolge ist die Suchstrategie einer Konditionsart. Sie legt fest, in welcher Reihenfolge das System nach passenden Konditionssätzen sucht — vom spezifischsten Zugriff (etwa Kunde und Material) bis zum allgemeinsten (nur Material). Der erste Treffer gewinnt und beendet die Suche.

### Was ist ein Kalkulationsschema?

Das Kalkulationsschema ist die geordnete Liste aller Konditionsarten, die ein Beleg durchläuft — von der Basispreis-Zeile über Rabatte und Zuschläge bis zur Steuer, inklusive Zwischensummen. Im Englischen heißt es „pricing procedure“; beide Begriffe meinen dasselbe.

### Warum gewinnt bei zwei passenden Preisen der spezifischere?

Weil die Zugriffsfolge vom Spezifischen zum Allgemeinen sortiert ist und das System die Suche beim ersten Treffer abbricht. Ein Konditionssatz für „Kunde und Material“ wird vor dem allgemeinen Satz für „Material“ geprüft und übersteuert ihn deshalb automatisch — ohne dass man etwas abschalten muss.
