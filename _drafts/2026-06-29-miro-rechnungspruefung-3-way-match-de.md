---
layout: post
lang: de
title: "Rechnungsprüfung mit MIRO: der 3-Way-Match in SAP MM verständlich erklärt"
description: "3-Way-Match aus Bestellung, Wareneingang und Rechnung: wie die Logistik-Rechnungsprüfung mit MIRO Abweichungen prüft, sperrt und das WE/RE-Konto ausgleicht."
slug: miro-rechnungspruefung-3-way-match
permalink: /blog/de/miro-rechnungspruefung-3-way-match/
translation_key: post-invoice-verification
date: 2026-07-08
category: "Einkauf"
keywords: "SAP MIRO, 3-Way-Match, Logistik-Rechnungsprüfung, WE/RE-Verrechnungskonto, Rechnungssperre, Toleranzen, SAP MM, Wareneingang"
reading_time: 10
sources:
  - label: "SAP Help Portal — Logistics Invoice Verification (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Materialwirtschaft / Logistik-Rechnungsprüfung — allgemeine Grundlagen. Vor produktivem Einsatz immer den aktuellen Stand im Help Portal prüfen."
faq:
  - q: "Was ist der 3-Way-Match in SAP?"
    a: "Der 3-Way-Match ist der Abgleich von drei Belegen: Bestellung, Wareneingang und Lieferantenrechnung. Nur wenn Preis und Menge in allen dreien zusammenpassen, läuft die Rechnung ohne Sperre durch. Das System zieht die Vorschlagswerte automatisch aus Bestellung und Wareneingang."
  - q: "Wozu dient das WE/RE-Verrechnungskonto?"
    a: "Das WE/RE-Verrechnungskonto ist ein Übergangskonto zwischen Materialwirtschaft und Finanzbuchhaltung. Der Wareneingang bucht es im Haben, die Rechnung gleicht es im Soll wieder aus. Steht dort noch ein Saldo, fehlt entweder die Rechnung oder der Wareneingang."
  - q: "Bezahlt die Logistik-Rechnungsprüfung die Rechnung?"
    a: "Nein. Die Logistik-Rechnungsprüfung erfasst, prüft und bucht die Rechnung und erzeugt dabei einen Rechnungs- und einen Buchhaltungsbeleg. Die eigentliche Zahlung und die Verwaltung offener Posten übernimmt die Finanzbuchhaltung (FI)."
  - q: "Was passiert, wenn eine Rechnung außerhalb der Toleranz liegt?"
    a: "Das System bucht die Rechnung trotzdem, setzt aber automatisch eine Zahlungssperre. Die Rechnung ist damit im System sichtbar, darf aber nicht bezahlt werden, bis jemand die Sperre nach Klärung manuell freigibt."
  - q: "Was bedeutet eine gelbe Ampel in MIRO?"
    a: "Grün heißt buchbar, gelb heißt buchbar mit anschließender Zahlungssperre, rot heißt nicht buchbar. Eine gelbe Ampel bei einem Saldo von null bedeutet: rechnerisch stimmt alles, das System sperrt die Rechnung aber wegen einer Abweichung zur Zahlung."
---

Auf deinem Schreibtisch landet eine Lieferantenrechnung. Die Buchhaltung möchte wissen, ob sie zur Auszahlung freigegeben werden kann. Wurde die Ware wirklich angeliefert? Deckt sich der Rechnungspreis mit der Bestellung? Und bleibt am Ende ein Restsaldo auf einem Verrechnungskonto hängen? Genau diese Fragen beantwortet die Logistik-Rechnungsprüfung in SAP MM — mit der Transaktion MIRO und dem 3-Way-Match.

## Kurz gesagt: was der 3-Way-Match leistet

Der 3-Way-Match ist das Grundprinzip der Rechnungsprüfung: Drei Belege — **Bestellung**, **Wareneingang** und **Lieferantenrechnung** — werden miteinander abgeglichen. Nur wenn Preis und Menge in allen dreien zusammenpassen, läuft die Rechnung sauber durch. Das System zieht die Vorschlagswerte automatisch aus Bestellung und Wareneingang; du vergleichst sie nur noch mit der Rechnung deines Lieferanten und buchst.

## Was ist die Logistik-Rechnungsprüfung in SAP MM?

Die Logistik-Rechnungsprüfung ist der dritte und letzte große Schritt im operativen Beschaffungsprozess. Nach dem Anlegen der Bestellung und dem Buchen des Wareneingangs erfasst du hier die eingegangene Lieferantenrechnung, prüfst sie auf *sachliche*, *preisliche* und *rechnerische* Richtigkeit und buchst sie ins System. Dabei entstehen gleichzeitig ein **Rechnungsbeleg** (MM-Beleg) und ein **Buchhaltungsbeleg** (FI-Beleg) — beide eigenständig, aber miteinander verknüpft.

Wichtig ist die saubere Aufgabenteilung: Die Logistik-Rechnungsprüfung kümmert sich ausschließlich um das Prüfen und Buchen. Für die tatsächliche Zahlung und die Verwaltung offener Verbindlichkeiten ist sie **nicht** zuständig — das übernimmt die Finanzbuchhaltung (FI).

In S/4HANA gibt es zwei Wege, eine Rechnung zu erfassen:

- **Die GUI-Transaktion MIRO** („Eingangsrechnung hinzufügen“) — die Einbildtransaktion für die Logistik-Rechnungsprüfung, in der du alle Angaben auf einem Bildschirm erfasst.
- **Die SAP-Fiori-App zum Anlegen einer Lieferantenrechnung** — die moderne Variante im Launchpad, mit identischer Logik im Hintergrund.

Beide Wege führen zum selben Ergebnis: zu einem gebuchten Rechnungsbeleg mit Bezug zu Bestellung und Wareneingang.

## Die drei Belege im 3-Way-Match

Beim 3-Way-Match werden drei Belege verglichen, die aus drei verschiedenen Abteilungen stammen. Jeder liefert seinen eigenen Beitrag zur Prüfung:

| Beleg | Quelle | Was wird geprüft? |
| --- | --- | --- |
| Bestellung | Einkauf | Bestellpreis, bestellte Menge, Lieferant, Steuerkennzeichen, Zahlungsbedingungen |
| Wareneingang | Lager / Wareneingang | gelieferte Menge, Lieferdatum, Lieferscheinnummer, Werk und Lagerort |
| Lieferantenrechnung | Logistik-Rechnungsprüfung | Rechnungspreis, fakturierte Menge, Bruttobetrag, Referenznummer, Rechnungsdatum |

Sind Bestellpreis, Wareneingangswert und Rechnungspreis identisch und stimmen auch die Mengen überein, geht der Saldo in MIRO auf null — die Rechnung ist buchbar. In der Realität gibt es allerdings fast immer kleine Abweichungen. Genau hier setzen Toleranzen und Sperrgründe an, dazu gleich mehr.

## Die Buchung beim Wareneingang: das WE/RE-Verrechnungskonto

Um zu verstehen, was MIRO bucht, musst du zuerst verstehen, was der Wareneingang bucht. Beim bewerteten Wareneingang zu einer Bestellposition für Lagermaterial passiert Folgendes:

- Eine **Sollbuchung** auf dem *Bestandskonto* mit dem Betrag „Wareneingangsmenge × Bewertungspreis“
- Eine **Habenbuchung** auf dem **WE/RE-Verrechnungskonto** mit dem Betrag „Wareneingangsmenge × Bestellpreis“

Das WE/RE-Verrechnungskonto (Wareneingangs-/Rechnungseingangs-Verrechnungskonto) ist das zentrale Bindeglied zwischen Materialwirtschaft und Finanzbuchhaltung. Es ist ein *Übergangskonto*: Ist die Ware angekommen, aber die Rechnung fehlt noch, steht auf diesem Konto ein offener Betrag (Ware erhalten, noch nicht berechnet). Sobald die Rechnung mit MIRO gebucht wird, gleicht das System das WE/RE-Konto wieder aus.

Wird ein Material mit der Preissteuerung *Standardpreis* (S) eingebucht, kann eine Wertdifferenz entstehen. Das folgende Beispiel zeigt eine Wareneingangsbuchung für 25 Stück zu je 88 EUR Bestellpreis bei einem hinterlegten Standardpreis von 110 EUR:

| Sachkonto | Bezeichnung | Soll | Haben |
| --- | --- | --- | --- |
| 3001 | Bestand Handelswaren | 2.750,00 EUR | |
| 4500 | WE/RE-Verrechnungskonto | | 2.200,00 EUR |
| 8001 | Ertrag aus Preisdifferenzen | | 550,00 EUR |

Auf dem Bestandskonto landet der Wert zum Standardpreis (25 × 110 EUR), das WE/RE-Konto bekommt den Bestellpreis (25 × 88 EUR) und die Wertdifferenz wandert auf ein Preisdifferenzenkonto. Anders bei Materialien mit *Gleitendem Durchschnittspreis* (V): Dort fließt die Differenz direkt in das Bestandskonto ein, und der Durchschnittspreis im Materialstamm wird automatisch neu ermittelt. (Die Sachkontonummern hier sind nur beispielhaft — im echten System hängen sie vom jeweiligen Kontenplan ab.)

## Die Buchung der Lieferantenrechnung mit MIRO

Erfasst du jetzt mit MIRO die zugehörige Lieferantenrechnung, kehrt sich die Logik um. Das System zieht den Bestellbezug, schlägt die offene Wareneingangsmenge vor und vergleicht den Rechnungsbetrag mit dem, was beim Wareneingang auf dem WE/RE-Konto stehen geblieben ist.

Die Einbildtransaktion MIRO ist in mehrere Bildbereiche unterteilt:

- **Vorgang** — hier wählst du, ob du eine Rechnung, eine Gutschrift, eine nachträgliche Belastung oder eine nachträgliche Entlastung erfasst.
- **Kopfdaten** — Rechnungsdatum, Referenz (die Rechnungsnummer des Lieferanten), Bruttobetrag, Steuerbetrag mit Steuerkennzeichen, Buchungskreis.
- **Zuordnung / Bestellbezug** — hier verknüpfst du die Rechnung mit Bestellung, Lieferschein oder Frachtbrief.
- **Rechnungspositionen** — die Liste aller vorgeschlagenen Positionen; markierte Zeilen werden gebucht.
- **Lieferantendaten** — Detaildaten zum Rechnungssteller aus dem Kreditorenstammsatz.
- **Saldo mit Ampel** — grün heißt buchbar, gelb heißt buchbar mit Zahlungssperre, rot heißt nicht buchbar.

Beim Buchen passieren drei Dinge gleichzeitig:

1. Das **WE/RE-Verrechnungskonto** wird zum Bestellpreis wieder ausgeglichen (Sollbuchung).
2. Das **Kreditorenkonto** wird zum Rechnungsbetrag brutto im Haben fortgeschrieben.
3. Eventuelle Differenzen zwischen Bestell- und Rechnungspreis werden — je nach Preissteuerung des Materials — auf das Bestandskonto oder auf ein Preisdifferenzenkonto gebucht.

Ein einfaches Buchungsbeispiel für eine Rechnung über 2.618 EUR brutto (25 Stück Material zu je 88 EUR, dazu 180 EUR ungeplante Frachtkosten und 238 EUR Vorsteuer):

| Sachkonto | Bezeichnung | Soll | Haben |
| --- | --- | --- | --- |
| 4500 | WE/RE-Verrechnungskonto | 2.200,00 EUR | |
| 5050 | Bezugsnebenkosten (Fracht) | 180,00 EUR | |
| 1576 | Vorsteuer | 238,00 EUR | |
| 4400 | Kreditor (Lieferantenkonto) | | 2.618,00 EUR |

**Tipp aus der Praxis:** Bevor du *Buchen* drückst, wähle in MIRO immer *Simulieren*. Das System zeigt dir dann genau, welche Konten mit welchen Beträgen bebucht werden. Ist der Saldo dabei nicht null, stimmt etwas nicht — meist mit dem Bruttobetrag, dem Steuerkennzeichen oder einer Positionsmenge.

## Toleranzen und Sperrgründe: wann sperrt das System eine Rechnung?

In der Praxis weicht der Rechnungsbetrag fast immer minimal von Bestellung oder Wareneingang ab — durch Rundungsdifferenzen, Frachtkosten oder Preisänderungen. SAP arbeitet deshalb mit **Toleranzen**, die im Customizing der Logistik-Rechnungsprüfung definiert werden. Liegt eine Abweichung innerhalb der Toleranz, wird die Rechnung normal gebucht. Liegt sie *außerhalb*, bucht das System die Rechnung trotzdem — setzt aber automatisch eine **Rechnungssperre** (die gelbe Ampel im Saldo-Bereich).

Die wichtigsten Prüfungen im Überblick:

| Prüfung | Was wird verglichen? | Typische Sperre |
| --- | --- | --- |
| Preisabweichung | Bestellpreis gegen Rechnungspreis pro Mengeneinheit | preisliche Sperre |
| Mengenabweichung | Rechnungsmenge gegen offene Wareneingangsmenge | mengenmäßige Sperre |
| Termin- / Datumsabweichung | Rechnungsdatum gegen geplantes Lieferdatum | Terminsperre |
| Betragsabweichung | Rechnungssumme einer Position gegen erwarteten Betrag | Betragssperre |

Eine gesperrte Rechnung ist gebucht und damit im System sichtbar — aber die Finanzbuchhaltung darf sie *nicht* zur Zahlung freigeben, solange die Sperre aktiv ist. Geprüft und manuell freigegeben werden gesperrte Rechnungen über die Transaktion MRBR („Gesperrte Rechnungen freigeben“) oder die entsprechende Fiori-App. Erst dann fließt das Geld.

Zusätzlich gibt es **manuelle Sperrgründe**, die ein Sachbearbeiter direkt in MIRO setzen kann — etwa bei sachlichen Klärungsfällen, mangelnder Qualität oder offenen Reklamationen. Auch hier gilt: gebucht ja, gezahlt nein.

## Typische Abweichungen und ihre Lösung

Im Tagesgeschäft begegnen dir immer wieder dieselben Konstellationen. Hier ein Überblick, wie SAP damit umgeht und was du als Anwender tun musst:

- **Rechnungspreis höher als Bestellpreis, innerhalb der Toleranz:** Die Rechnung wird gebucht. Bei Standardpreis-Material landet die Differenz auf einem Preisdifferenzenkonto. Bei gleitendem Durchschnittspreis wird der Materialstamm neu bewertet — der Bestand wird teurer.
- **Rechnungspreis höher als Bestellpreis, außerhalb der Toleranz:** Die Rechnung wird gebucht, aber zur Zahlung gesperrt. Nach Klärung mit dem Lieferanten folgt die Freigabe über MRBR.
- **Rechnungsmenge größer als gelieferte Menge:** eine Mengenabweichung. Entweder ist eine weitere Lieferung unterwegs — oder der Lieferant hat falsch fakturiert. Liegt die Überschreitung über der Toleranz, bleibt die Rechnung gesperrt.
- **Frachtkosten auf der Rechnung, aber nicht in der Bestellung:** in MIRO als *ungeplante Bezugsnebenkosten* erfassen. Das System verteilt sie automatisch auf die Positionen.
- **Rechnung kommt vor dem Wareneingang an:** möglich, aber heikel — der Saldo bleibt offen auf dem WE/RE-Konto. Üblich ist die Reihenfolge erst Wareneingang, dann Rechnung.
- **Nachträgliche Belastung oder Entlastung:** Macht der Lieferant nachträglich eine Preisänderung geltend, erfasst du in MIRO eine „nachträgliche Belastung“ oder „nachträgliche Entlastung“. Eine vollständige Stornorechnung ist dagegen die *Gutschrift*.

Hilfreich ist außerdem die Bestellentwicklung: In jedem Bestellbeleg kannst du sehen, wie viel bereits geliefert und wie viel bereits berechnet wurde. Das ist die schnellste Methode, um die Konsistenz von Wareneingang und Rechnung zu prüfen.

## Kurz zusammengefasst

Die Logistik-Rechnungsprüfung mit MIRO ist das Bindeglied zwischen Einkauf, Lager und Buchhaltung. Sie sorgt dafür, dass ein Unternehmen nur das bezahlt, was tatsächlich bestellt und geliefert wurde — und dass das WE/RE-Verrechnungskonto am Ende wieder auf null steht. Der 3-Way-Match aus Bestellung, Wareneingang und Rechnung ist das Grundprinzip; Toleranzen und Sperrgründe sorgen dafür, dass nur saubere Rechnungen automatisch zur Zahlung gehen. Wer die Aufgabenteilung zwischen MM (prüfen und buchen) und FI (zahlen) sauber trennt und die Buchungslogik rund um das WE/RE-Konto versteht, hat das Thema im Griff.

## Häufige Fragen

### Was ist der 3-Way-Match in SAP?

Der 3-Way-Match ist der Abgleich von drei Belegen: Bestellung, Wareneingang und Lieferantenrechnung. Nur wenn Preis und Menge in allen dreien zusammenpassen, läuft die Rechnung ohne Sperre durch. Das System zieht die Vorschlagswerte automatisch aus Bestellung und Wareneingang.

### Wozu dient das WE/RE-Verrechnungskonto?

Das WE/RE-Verrechnungskonto ist ein Übergangskonto zwischen Materialwirtschaft und Finanzbuchhaltung. Der Wareneingang bucht es im Haben, die Rechnung gleicht es im Soll wieder aus. Steht dort noch ein Saldo, fehlt entweder die Rechnung oder der Wareneingang.

### Bezahlt die Logistik-Rechnungsprüfung die Rechnung?

Nein. Die Logistik-Rechnungsprüfung erfasst, prüft und bucht die Rechnung und erzeugt dabei einen Rechnungs- und einen Buchhaltungsbeleg. Die eigentliche Zahlung und die Verwaltung offener Posten übernimmt die Finanzbuchhaltung (FI).

### Was passiert, wenn eine Rechnung außerhalb der Toleranz liegt?

Das System bucht die Rechnung trotzdem, setzt aber automatisch eine Zahlungssperre. Die Rechnung ist damit im System sichtbar, darf aber nicht bezahlt werden, bis jemand die Sperre nach Klärung manuell freigibt.

### Was bedeutet eine gelbe Ampel in MIRO?

Grün heißt buchbar, gelb heißt buchbar mit anschließender Zahlungssperre, rot heißt nicht buchbar. Eine gelbe Ampel bei einem Saldo von null bedeutet: rechnerisch stimmt alles, das System sperrt die Rechnung aber wegen einer Abweichung zur Zahlung.
