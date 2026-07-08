---
layout: post
lang: de
title: "Das Hauptbuch in SAP S/4HANA: Finanzbuchhaltung verständlich erklärt"
description: "Sachkonten, Kontenplan, Universal Journal, Belege und Abstimmkonten: So funktioniert das Hauptbuch (FI-GL) in SAP S/4HANA — klar und praxisnah erklärt."
slug: hauptbuch-s4hana-finanzbuchhaltung
permalink: /blog/de/hauptbuch-s4hana-finanzbuchhaltung/
translation_key: post-general-ledger
date: 2026-07-08
category: "Finanzen"
keywords: "SAP Hauptbuch, FI-GL, Finanzbuchhaltung, Sachkonto, Kontenplan, Universal Journal, ACDOCA, Abstimmkonto, Buchungskreis, S/4HANA Finance"
reading_time: 10
sources:
  - label: "SAP Help Portal — Finanzbuchhaltung (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Finance / General Ledger Accounting — allgemeine Grundlagen zum Hauptbuch. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist das Hauptbuch in SAP S/4HANA?"
    a: "Das Hauptbuch (FI-GL) ist die zentrale Komponente des externen Rechnungswesens in SAP S/4HANA. Es zeichnet alle wertrelevanten Geschäftsvorfälle vollständig und abgestimmt auf, sodass jederzeit eine ordnungsmäßige Bilanz und Gewinn- und Verlustrechnung erstellt werden kann."
  - q: "Was ist das Universal Journal?"
    a: "Das Universal Journal ist eine einzige zentrale Tabelle (technisch ACDOCA), in der SAP S/4HANA alle wertrelevanten Buchungen aus Finanzbuchhaltung, Controlling, Anlagenbuchhaltung und Profitcenter-Rechnung gemeinsam ablegt. Dadurch gibt es nur noch eine Datenquelle statt getrennter, ständig abzustimmender Tabellen."
  - q: "Was ist der Unterschied zwischen Kontenplan und Sachkonto?"
    a: "Ein Sachkonto ist eine einzelne Position der Buchhaltung, etwa „Bank Hauptkonto“ oder „Erlöse Inland“. Der Kontenplan ist das geordnete Verzeichnis, das die Definition aller Sachkonten eines Hauptbuchs enthält — im Kern Kontonummer, Kontenbezeichnung und Sachkontoart."
  - q: "Warum kann man nicht direkt auf ein Abstimmkonto buchen?"
    a: "Ein Abstimmkonto verbindet ein Nebenbuch — etwa Debitoren, Kreditoren oder Anlagen — in Echtzeit mit dem Hauptbuch. Es wird ausschließlich automatisch aus dem Nebenbuch fortgeschrieben. Direkte Buchungen darauf sind gesperrt, damit Nebenbuch und Hauptbuch immer übereinstimmen."
  - q: "Auf welcher Ebene wird die Bilanz erstellt?"
    a: "Die gesetzliche Bilanz und die Gewinn- und Verlustrechnung werden auf Ebene des Buchungskreises erstellt. Der Buchungskreis ist die kleinste in sich abgeschlossene Buchhaltungseinheit — meist ein einzelnes rechtlich selbstständiges Unternehmen."
---

Wer die Zahlen eines Unternehmens verstehen will, landet früher oder später beim Hauptbuch. In SAP S/4HANA ist es das Herzstück der Finanzbuchhaltung: Hier laufen alle wertrelevanten Geschäftsvorfälle zusammen, und hier entstehen am Ende Bilanz und Gewinn- und Verlustrechnung. Dieser Artikel erklärt in klarer Sprache, aus welchen Bausteinen das Hauptbuch besteht und wie sie zusammenspielen.

## Kurz gesagt: das Herz der Finanzbuchhaltung

Das Hauptbuch (im Original **FI-GL**, für *General Ledger*) ist die zentrale Komponente des externen Rechnungswesens in SAP S/4HANA. Seine Aufgabe ist klar: die **vollständige und abgestimmte Aufzeichnung aller wertrelevanten Geschäftsvorfälle**, sodass jederzeit eine ordnungsmäßige **Bilanz** und **Gewinn- und Verlustrechnung (GuV)** erstellt werden kann.

Das Hauptbuch ist damit ein vollständiger Nachweis aller Geschäftsvorfälle und zugleich die zentrale Quelle für die Rechnungslegung. Aus ihm leiten sich unter anderem ab:

- Informationen zum einzelnen Konto
- Journale
- Summen- und Saldenlisten
- Bilanz- und GuV-Auswertungen

Jeder Buchungsvorgang in den Nebenbüchern — Debitoren, Kreditoren, Anlagen, Bank — wird automatisch im Hauptbuch mitgebucht. Das ist die berühmte **Echtzeit-Integration** über die Abstimmkonten, zu der weiter unten mehr kommt.

## Was ist das Universal Journal?

Wer früher mit älteren SAP-Systemen gearbeitet hat, kennt eine strukturelle Schwäche: **Finanzbuchhaltung (FI) und Controlling (CO) lagen in getrennten Tabellen.** Das Hauptbuch lebte in den FI-Tabellen, das Controlling in eigenen CO-Tabellen, die Profitcenter-Rechnung wieder woanders. Daten mussten ständig abgeglichen und übergeleitet werden.

Genau diesen Bruch hat SAP mit S/4HANA aufgelöst. Das Stichwort heißt **Universal Journal** — eine einzige zentrale Tabelle (technisch *ACDOCA*), in der **alle wertrelevanten Buchungen aus Finanzbuchhaltung, Controlling, Anlagenbuchhaltung und Profitcenter-Rechnung gemeinsam** abgelegt werden.

Was bedeutet das in der Praxis?

- **Eine einzige Wahrheit:** Es gibt keine Differenzen mehr zwischen FI- und CO-Sicht, weil die Daten aus derselben Tabelle stammen.
- **Auswertungen nach vielen Dimensionen:** Bilanzen pro Profitcenter, Segment oder Geschäftsbereich sind standardmäßig möglich, weil alle Dimensionen direkt am Beleg hängen.
- **Echtzeit-Reporting:** Auswertungen wie Bilanz oder GuV greifen direkt auf das Universal Journal zu — separate Aggregationstabellen entfallen.

Ein sichtbares Beispiel: In SAP S/4HANA können Profitcenter Teil der Finanzbuchhaltung sein. Ihre Informationen werden im Universal Journal abgelegt, und sie fungieren wie Buchungskreise als Dimension für die Rechnungslegung. Das Universal Journal ist damit weit mehr als ein Datenbank-Trick — es ist der Grund, warum FI und CO in S/4HANA zusammenwachsen.

## Sachkonten und Kontenplan

Das Hauptbuch besteht aus **Sachkonten** (englisch *G/L Accounts*). Jedes Sachkonto steht für eine bestimmte Position in der Buchhaltung — zum Beispiel „Bank Hauptkonto“, „Verbindlichkeiten aus Lieferungen und Leistungen“ oder „Erlöse Inland“.

Alle Sachkonten zusammen sind im **Kontenplan** organisiert. Der Kontenplan enthält in geordneter Form die Definition aller Sachkonten eines Hauptbuchs. Diese Definition umfasst im Wesentlichen die **Kontonummer**, die **Kontenbezeichnung** und die **Sachkontoart**.

Ein paar Begriffe, die den Kontenplan greifbar machen:

- **Operativer Kontenplan:** der Kontenplan, der einem Buchungskreis zugeordnet ist und auf den tatsächlich gebucht wird.
- **Kontengruppe:** fasst Konten mit ähnlicher betriebswirtschaftlicher Funktion zusammen (etwa Geldkonten, Aufwandskonten, Ertragskonten). Sie steuert auch die Nummernkreise und legt fest, welche Felder bei der Erfassung Pflicht, optional oder ausgeblendet sind.
- **Sachkontoart:** unterscheidet Konten nach ihrer Rolle — zum Beispiel Bestandskonto, Geldkonto (Bankabstimmkonto), Primärkosten oder Erlöse, Sekundärkosten sowie nicht betriebliche Aufwendungen und Erträge.

Gepflegt und angezeigt werden Sachkonten in S/4HANA über die entsprechende Fiori-App aus dem Bereich Hauptbuch des Launchpads. Über die Kontonummer und die Kontengruppe hängt jedes Sachkonto an genau seinem Platz im Kontenplan.

## Der Buchungskreis als zentrale Bilanzierungseinheit

Das vielleicht wichtigste Organisationselement im Finanzwesen ist der **Buchungskreis**. Ein Buchungskreis ist eine **unabhängige Buchhaltungseinheit und das kleinste Organisationselement, für das eine vollständige, in sich abgeschlossene Buchhaltung** abgebildet werden kann. Ein typisches Beispiel ist ein einzelnes rechtlich selbstständiges Unternehmen innerhalb eines Konzerns.

Ein paar Eckdaten, die den Buchungskreis charakterisieren:

- Er hat einen **vierstelligen, alphanumerischen Schlüssel** (zum Beispiel 1010 oder 1710 in den Beispielmandanten von SAP).
- Jeder Buchungskreis verfügt über genau **eine Hauswährung**. Fremdwährungsbeträge werden automatisch umgerechnet.
- **Das Hauptbuch wird auf Buchungskreisebene geführt.** Das ist die Ebene, auf der gesetzliche Bilanzen und GuVs erstellt werden.
- Bei jeder Transaktion in der Finanzkomponente muss der Buchungskreis angegeben werden.

Das macht den Buchungskreis zum eigentlichen **Bilanzierer**: Wer wissen will, auf welcher Ebene die Bilanz entsteht, findet die Antwort hier.

## Wie läuft eine Belegerfassung ab?

Das tägliche Brot der Buchhaltung ist das **Erfassen von Sachkontenbuchungen**. In SAP S/4HANA gibt es dafür die entsprechende Fiori-App zum Buchen von Hauptbuchbelegen. Ihr Einstiegsbild ist typischerweise in mehrere Bereiche unterteilt:

- **Kopfdaten:** Buchungsdatum, Belegart, Buchungskreis, Periode und Ähnliches. Diese Angaben gelten für den gesamten Beleg.
- **Positionsdaten:** Hier werden die einzelnen Positionen erfasst — pro Zeile ein Sachkonto mit einem Soll- oder Haben-Betrag.
- **Steuerpositionen:** Details zur Steuerberechnung, etwa ob die Steuer automatisch berechnet wird.
- **Vorlagen:** Vorgefertigte Buchungsbelegvorlagen lassen sich hier referenzieren.

Inhaltlich folgt jede Buchung immer demselben Schema:

1. **Belegkopf erfassen** — Datum, Belegart, Buchungskreis.
2. **Positionen erfassen** — mindestens zwei: eine Soll- und eine Habenposition. Das ist das buchhalterische Grundgesetz „Soll an Haben“, jede Buchung muss ausgeglichen sein.
3. **Beleg simulieren oder buchen** — erst hier wird es verbindlich.

Erst beim erfolgreichen Buchen vergibt das System im Hintergrund eine eindeutige **Belegnummer** und schreibt den Beleg ins Universal Journal.

## Belegart und Buchungsschlüssel: die Steuerinstrumente

Zwei Begriffe werden gerne verwechselt: **Belegart** und **Buchungsschlüssel**. Beide steuern die Buchung, aber auf unterschiedlichen Ebenen.

Die **Belegart** steht im **Belegkopf** und unterscheidet die vielen Arten von Buchhaltungsbelegen voneinander. Klassische Standardbelegarten sind zum Beispiel:

- **SA** — Sachkontenbelege
- **DR** — Debitorenrechnungen
- **DG** — Debitorengutschriften
- **DZ** — Debitorenzahlungen
- **KR** — Kreditorenrechnungen
- **KG** — Kreditorengutschriften
- **KZ** — Kreditorenzahlungen

Jede Belegart steuert unter anderem den **Belegnummernkreis** und die zulässigen Kontoarten.

Der **Buchungsschlüssel** sitzt dagegen auf **Positionsebene** — also pro Zeile im Beleg. Er signalisiert dem System drei Dinge:

- welche **Kontoart** verwendet wird (Sachkonto, Debitor, Kreditor, Anlage, Material)
- ob es sich um eine **Soll- oder Habenbuchung** handelt
- welcher **Feldstatus** für die Zusatzangaben gilt

Für reine Hauptbuchbuchungen genügen zwei Buchungsschlüssel: **40** steht für die Sollbuchung auf ein Sachkonto, **50** für die Habenbuchung. In den modernen Fiori-Apps musst du diese Schlüssel nicht mehr selbst eintippen — du wählst einfach die Spalte „Soll“ oder „Haben“, und das System vergibt im Hintergrund 40 oder 50 mitsamt ihren Steuerungsfunktionen. Abgeschafft sind sie also nicht, sie laufen nur unter der Haube weiter.

## Was ist ein Abstimmkonto?

Ein zentrales Konzept, das man wirklich verstanden haben sollte, ist das **Abstimmkonto** (englisch *Reconciliation Account*). Ein Abstimmkonto verbindet ein Nebenbuch in **Echtzeit** mit dem Hauptbuch: Sobald in einem Nebenbuch gebucht wird, erfolgt gleichzeitig eine Buchung auf dem zugehörigen Abstimmkonto im Hauptbuch.

Ein Beispiel macht das greifbar: Ein Buchhalter erfasst eine Kreditorenrechnung in der Kreditorenbuchhaltung. Diese Rechnung wird im **Kreditoren-Stammsatz** (Nebenbuch) sichtbar — und gleichzeitig wird im Hintergrund das hinterlegte Abstimmkonto „Verbindlichkeiten aus Lieferungen und Leistungen“ im Hauptbuch fortgeschrieben. Es gibt also keine Differenz zwischen Nebenbuch und Hauptbuch, sie sind in Echtzeit synchron.

Über Abstimmkonten sind unter anderem folgende Nebenbücher mit dem Hauptbuch verbunden:

- **Kreditorenbuchhaltung** (FI-AP)
- **Debitorenbuchhaltung** (FI-AR)
- **Anlagenbuchhaltung** (FI-AA)

Eine wichtige Konsequenz für die Praxis: **Auf ein Abstimmkonto kann man nicht direkt buchen.** Es wird ausschließlich automatisch über die jeweiligen Nebenbuchbuchungen bedient. Wer versucht, direkt auf das Konto „Forderungen aus Lieferungen und Leistungen“ zu buchen, wird vom System gestoppt — gebucht wird über die Debitorenrechnung im Nebenbuch. So bleibt die Abstimmung zwischen den Büchern jederzeit gewahrt.

## Buchungsperioden und Periodenabschluss

Jede Buchung in SAP ist einer **Buchungsperiode** zugeordnet. Üblicherweise entspricht eine Periode einem Monat des Geschäftsjahres — also zwölf Hauptperioden plus mögliche Sonderperioden für Abschlussbuchungen.

Das System prüft bei jeder Buchung, ob die Zielperiode **geöffnet** ist. Erst wenn eine Periode für eine Belegart und einen Kontotyp freigeschaltet ist, kann gebucht werden. So verhindert SAP, dass nachträglich in bereits abgeschlossene Monate hineingebucht wird.

Am Periodenende fallen typische Abschlussarbeiten an:

- Abgrenzungen buchen (etwa für einen Versicherungsaufwand, der mehrere Perioden betrifft)
- das **WE/RE-Verrechnungskonto** pflegen — das Konto, auf dem Wareneingänge ohne Rechnung und Rechnungen ohne Wareneingang zwischengelagert werden
- ein Belegjournal anlegen
- Bilanz und GuV generieren
- Summen- und Saldenlisten erstellen

Man muss diese Tätigkeiten nicht jeden Tag selbst durchführen — aber es hilft enorm zu wissen, dass es sie gibt und in welcher Reihenfolge sie typischerweise ablaufen.

## Ledger und parallele Rechnungslegung

Viele Unternehmen müssen mehrere Rechnungslegungsvorschriften gleichzeitig erfüllen — zum Beispiel **HGB** für den deutschen Jahresabschluss und **IFRS** für den Konzernabschluss, mitunter zusätzlich **US-GAAP**. SAP S/4HANA bietet dafür zwei Ansätze:

- **Kontenlösung:** Unterschiedliche Wertansätze werden auf unterschiedliche Konten gebucht. Bei der Bilanzerstellung werden über die Bilanz/GuV-Struktur die jeweils passenden Konten ausgewertet.
- **Ledgerlösung:** Mehrere parallele „Hauptbücher“ (Ledger) laufen gleichzeitig. Genau ein Ledger ist das **führende Ledger**, die anderen ergänzen es. Für Neueinführungen wird heute meist die Ledgerlösung empfohlen.

Ein **Ledger** ist dabei nichts anderes als eine vollständige Sicht des Hauptbuchs nach einem bestimmten Regelwerk. Jedes Ledger schreibt seine Werte ebenfalls ins Universal Journal — dadurch bleiben parallele Bewertungen sauber getrennt und trotzdem in einer Datenquelle.

## Ein paar häufige Verständnisfallen

Beim Einstieg ins Hauptbuch tauchen immer wieder dieselben Stolpersteine auf:

- **Buchungskreis und Kostenrechnungskreis verwechseln.** Der Buchungskreis ist die Bilanzierungseinheit (FI). Der Kostenrechnungskreis ist die Organisationseinheit für das Controlling (CO). Ein Kostenrechnungskreis kann mehrere Buchungskreise enthalten — alle mit gleichem operativem Kontenplan.
- **Kontenplan und Bilanz/GuV-Struktur gleichsetzen.** Der Kontenplan listet alle Sachkonten. Die Bilanz/GuV-Struktur ist die hierarchische Anordnung dieser Konten für das Reporting (etwa „Aktiva → Anlagevermögen → Sachanlagen“). Das sind zwei verschiedene Objekte.
- **Direkt auf ein Abstimmkonto buchen wollen.** Geht nicht. Abstimmkonten werden ausschließlich automatisch aus den Nebenbüchern fortgeschrieben.
- **Das Universal Journal als „nur Technik“ abtun.** Es ist der Grund, warum Profitcenter in S/4HANA Teil von FI sind, warum Bilanzen pro Segment möglich sind und warum die FI/CO-Abstimmung entfällt.

## Kurz zusammengefasst

Das Hauptbuch in SAP S/4HANA lässt sich als eine zusammenhängende Geschichte lesen: Ein Unternehmen (Buchungskreis) führt seine Konten (Sachkonten) in einem geordneten Verzeichnis (Kontenplan). Jeder Geschäftsvorfall wird als Beleg erfasst (Belegart) — entweder direkt über eine Hauptbuchbuchung (Buchungsschlüssel 40/50) oder automatisch aus einem Nebenbuch über ein Abstimmkonto. Alles landet in derselben Tabelle (Universal Journal, technisch ACDOCA), aus der am Periodenende Bilanz und GuV entstehen. Wer diese Kette einmal verstanden hat, ordnet die vielen Detailbegriffe der Finanzbuchhaltung mühelos ein.

## Häufige Fragen

### Was ist das Hauptbuch in SAP S/4HANA?

Das Hauptbuch (FI-GL) ist die zentrale Komponente des externen Rechnungswesens in SAP S/4HANA. Es zeichnet alle wertrelevanten Geschäftsvorfälle vollständig und abgestimmt auf, sodass jederzeit eine ordnungsmäßige Bilanz und Gewinn- und Verlustrechnung erstellt werden kann.

### Was ist das Universal Journal?

Das Universal Journal ist eine einzige zentrale Tabelle (technisch ACDOCA), in der SAP S/4HANA alle wertrelevanten Buchungen aus Finanzbuchhaltung, Controlling, Anlagenbuchhaltung und Profitcenter-Rechnung gemeinsam ablegt. Dadurch gibt es nur noch eine Datenquelle statt getrennter, ständig abzustimmender Tabellen.

### Was ist der Unterschied zwischen Kontenplan und Sachkonto?

Ein Sachkonto ist eine einzelne Position der Buchhaltung, etwa „Bank Hauptkonto“ oder „Erlöse Inland“. Der Kontenplan ist das geordnete Verzeichnis, das die Definition aller Sachkonten eines Hauptbuchs enthält — im Kern Kontonummer, Kontenbezeichnung und Sachkontoart.

### Warum kann man nicht direkt auf ein Abstimmkonto buchen?

Ein Abstimmkonto verbindet ein Nebenbuch — etwa Debitoren, Kreditoren oder Anlagen — in Echtzeit mit dem Hauptbuch. Es wird ausschließlich automatisch aus dem Nebenbuch fortgeschrieben. Direkte Buchungen darauf sind gesperrt, damit Nebenbuch und Hauptbuch immer übereinstimmen.

### Auf welcher Ebene wird die Bilanz erstellt?

Die gesetzliche Bilanz und die Gewinn- und Verlustrechnung werden auf Ebene des Buchungskreises erstellt. Der Buchungskreis ist die kleinste in sich abgeschlossene Buchhaltungseinheit — meist ein einzelnes rechtlich selbstständiges Unternehmen.
