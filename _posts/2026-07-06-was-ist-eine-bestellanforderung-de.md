---
layout: post
lang: de
title: "Was ist eine Bestellanforderung (BANF) in SAP?"
description: "Die Bestellanforderung ist der erste Schritt im SAP-Einkauf: eine interne Bitte, etwas zu beschaffen. Was sie ist, wie sie entsteht und wie aus ihr eine Bestellung wird — verständlich erklärt."
slug: was-ist-eine-bestellanforderung
permalink: /blog/de/was-ist-eine-bestellanforderung/
translation_key: post-purchase-requisition
date: 2026-07-06
category: "Einkauf"
keywords: "Bestellanforderung, BANF, SAP MM, Einkauf, Beschaffung, Bestellung, Freigabe, Anwender"
reading_time: 6
sources:
  - label: "SAP Help Portal — Sourcing and Procurement (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Bereich Materials Management / Sourcing and Procurement — allgemeine Grundlagen zur Bestellanforderung. Vor produktiver Nutzung immer den aktuellen Stand im Help Portal prüfen."
---

Wenn in einem Unternehmen etwas beschafft werden soll — Material, Ersatzteile, eine Dienstleistung — beginnt der Weg in SAP fast immer an derselben Stelle: mit einer **Bestellanforderung**, kurz BANF. Sie ist einer der Begriffe, die jeder SAP-Anwender im Einkaufsumfeld früher oder später hört. Dieser Artikel erklärt in klarer Sprache, was dahintersteckt.

## Kurz gesagt: eine interne Bitte, etwas zu beschaffen

Eine Bestellanforderung ist ein **internes Dokument**. Mit ihr sagt eine Abteilung im Grunde: „Wir brauchen dieses Material oder diese Leistung — bitte kümmert euch um die Beschaffung." Sie richtet sich also **nach innen**, an den Einkauf, und noch nicht nach außen an einen Lieferanten.

Genau das ist der wichtigste Unterschied, den man am Anfang oft verwechselt:

- Die **Bestellanforderung** ist die interne Anforderung („wir hätten gern").
- Die **Bestellung** ist das verbindliche Dokument, das an den Lieferanten geht („wir bestellen hiermit").

Die Bestellanforderung ist damit der erste Schritt in der Beschaffungskette und noch kein Vertrag mit irgendjemandem.

## Wie eine Bestellanforderung entsteht

Es gibt zwei typische Wege, auf denen eine Bestellanforderung in SAP entsteht.

**1. Manuell angelegt.** Ein Mitarbeiter aus einer Fachabteilung — zum Beispiel aus der Instandhaltung oder dem Lager — erfasst die Anforderung selbst: Was wird gebraucht, wie viel, für welches Werk und bis wann. Das ist der klassische Fall, wenn jemand konkret weiß, dass etwas beschafft werden muss.

**2. Automatisch erzeugt.** Häufig legt SAP die Bestellanforderung selbst an, ohne dass jemand sie tippt. Das passiert typischerweise über die **Bedarfsplanung (MRP)**: Wenn der Bestand eines Materials unter einen definierten Punkt fällt, erkennt das System den Bedarf und schlägt automatisch eine Beschaffung vor — in Form einer Bestellanforderung. Auch andere Prozesse, etwa ein Instandhaltungsauftrag, können automatisch eine BANF auslösen.

In beiden Fällen ist das Ergebnis dasselbe: ein internes Dokument, das dem Einkauf sagt, dass etwas gebraucht wird.

## Vom Bedarf zur Bestellung

Sobald die Bestellanforderung da ist, übernimmt der Einkauf. Vereinfacht läuft es so:

1. **Anforderung sichten.** Der Einkauf prüft die offenen Bestellanforderungen.
2. **Bezugsquelle finden.** Von wem soll beschafft werden? Manchmal ist das bereits hinterlegt (etwa über einen Infosatz oder einen Vertrag), manchmal wählt der Einkauf den Lieferanten aktiv aus.
3. **In eine Bestellung umwandeln.** Aus der Bestellanforderung wird eine echte Bestellung erzeugt. Erst diese geht an den Lieferanten.

Die Daten aus der Anforderung — Material, Menge, Werk, Termin — werden dabei in die Bestellung übernommen. Die Bestellanforderung bleibt als Beleg erhalten und ist mit der Bestellung verknüpft, sodass später nachvollziehbar ist, wo der Bedarf ursprünglich herkam.

## Die Freigabe: warum eine Anforderung „hängen" kann

In vielen Unternehmen darf nicht jede Bestellanforderung sofort zur Bestellung werden. Ab bestimmten Wertgrenzen oder für bestimmte Materialgruppen muss sie erst **freigegeben** werden — das ist eine interne Genehmigung, oft durch eine Führungskraft oder den Kostenstellenverantwortlichen.

Für den Anwender heißt das: Wenn eine Anforderung „nichts tut" und nicht in eine Bestellung übergeht, liegt es häufig daran, dass die Freigabe noch aussteht. Das ist kein Fehler, sondern ein bewusst eingebauter Kontrollschritt.

## Wer im Alltag damit arbeitet

- **Fachabteilungen** (Lager, Instandhaltung, Produktion) lösen Bedarfe aus und legen Anforderungen an.
- **Der Einkauf** wandelt sie in Bestellungen um und wählt Lieferanten.
- **Genehmigende** geben Anforderungen ab bestimmten Grenzen frei.

Für dich als Anwender ist die Bestellanforderung damit oft der Punkt, an dem du mit dem Beschaffungsprozess in Berührung kommst — sei es, weil du selbst eine anlegst, oder weil du wissen willst, warum eine Bestellung noch nicht raus ist.

## Häufige Stolpersteine

- **Bestellanforderung mit Bestellung verwechseln.** Die Anforderung ist intern, die Bestellung geht nach außen. Wer beim Lieferanten nachfragt, warum „die Bestellung" nicht angekommen ist, sollte zuerst prüfen, ob überhaupt schon eine Bestellung existiert — oder ob es noch bei der Anforderung hängt.
- **Fehlende Freigabe übersehen.** Eine nicht freigegebene Anforderung wird nicht weiterverarbeitet. Ein Blick auf den Freigabestatus spart viel Sucherei.
- **Unvollständige Angaben.** Fehlt etwa das Lieferdatum oder ist die Menge unklar, kann der Einkauf die Anforderung nicht sauber umsetzen.

## Kurz zusammengefasst

Die Bestellanforderung ist der **interne Startpunkt** jeder Beschaffung in SAP: eine Bitte an den Einkauf, etwas zu besorgen. Sie kann von Hand oder automatisch entstehen, durchläuft bei Bedarf eine Freigabe und wird am Ende in eine Bestellung umgewandelt, die an den Lieferanten geht. Wer diesen einen Unterschied — intern anfordern gegen extern bestellen — verinnerlicht hat, versteht den Einstieg in den SAP-Einkauf schon zur Hälfte.
