---
layout: post
lang: en
title: "Material valuation in SAP: standard price vs. moving average price, explained"
description: "How SAP decides what your inventory is worth: standard price (S) versus moving average price (V), the material and accounting documents, the GR/IR account and price differences — in plain language."
slug: material-valuation-basics
permalink: /blog/en/material-valuation-basics/
translation_key: post-materialbewertung
date: 2026-07-07
category: "Finance"
keywords: "material valuation, standard price, moving average price, price control, GR/IR account, price differences, inventory value, SAP finance"
reading_time: 9
sources:
  - label: "SAP Help Portal — Inventory Valuation / Materials Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Materials Management and inventory valuation — general background. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between standard price and moving average price?"
    a: "The standard price (S) stays constant through the fiscal year; any deviation from the purchase price posts to a price-difference account. The moving average price (V) is recalculated as a weighted average with every receipt, so it adjusts continuously."
  - q: "Where is a material's price control maintained?"
    a: "In the material master, on the Accounting 1 view. That is where the S or V indicator sits, together with the current valuation price and the total stock value."
  - q: "What is the GR/IR clearing account for?"
    a: "It bridges the gap between goods receipt and invoice receipt. The goods receipt posts to it and the invoice clears it again. An open balance signals that either an invoice or a delivery is still missing."
  - q: "Why does a material suddenly show an unexpected stock value?"
    a: "Usually because of a valuation-relevant posting — for example a goods receipt at a very different price, or a manual revaluation. Looking at the material document and the linked accounting document shows what happened."
---

Every company that keeps goods in stock has to carry that inventory at a value on its balance sheet. In SAP this is handled by **material valuation** — the mechanism that decides, on every stock movement, what amount a material contributes. It ties the operational world of inventory management to financial accounting, and once you understand the basic logic you can see through a large part of what SAP is posting behind the scenes.

## In short: the value of your stock, kept up to date automatically

**Material valuation** determines the *value* at which a stock-managed material appears on the balance sheet. Every stock movement — goods receipt, goods issue, transfer posting — produces a **material document**. If the transaction is valuation-relevant, SAP automatically adds an **accounting document** that posts to the general ledger accounts. That way the inventory value in accounting always stays in sync with the physical stock, without anyone doing the maths by hand.

## Material document and accounting document: two separate worlds

The most important concept first: SAP cleanly separates **stock** from **value**.

- The **material document** records the *physical* movement: what was moved, when, how much, and from where to where?
- The **accounting document** records the *financial* impact: which general ledger accounts are posted, and with which amounts?

Both documents are created at the same time but are independent. The material document is identified by its number and year; the accounting document by company code, document number and fiscal year.

### When is a stock movement valuation-relevant?

A movement is valuation-relevant whenever the stock value on the balance sheet changes — that is, whenever financial accounting is affected.

- **Valuation-relevant:** every external goods receipt (stock goes up, current assets grow), a goods issue to a customer, a scrapping, or a consumption posting to a cost centre.
- **Not valuation-relevant:** a pure transfer within the same plant, for example from one storage location to another. The stock stays in the same company code, only the location changes — the balance sheet doesn't notice.

Rule of thumb: if the stock value changes at company-code level, an accounting document is created. If the stock only moves internally from A to B, it isn't.

### Where does the company code come from?

The company code of the accounting document is **derived automatically from the plant** in which the stock movement takes place. You don't enter it — the plant determines which legal entity the posting lands in.

## Price control: standard price (S) or moving average price (V)?

In the material master, on the *Accounting 1* view, sits a key control field: **price control**. It has exactly two settings, and the choice shapes the entire valuation behaviour of the material.

- **S — standard price:** the material is valued at a *fixed* price that stays constant through the fiscal year. When the actual purchase price deviates from it, the difference posts to a separate **price-difference account**. The stock account only ever moves at the standard price.
- **V — moving average price:** the valuation price is *recalculated* on every valuation-relevant receipt — as a weighted average of the old stock and the new receipt. Price differences normally don't arise, because the price always matches the current average.

Which setting makes sense when is a matter of accounting policy. As a rule of thumb:

| Price control | Typical use |
| --- | --- |
| **S — standard price** | Semi-finished and finished goods from in-house production, materials with stable purchase prices |
| **V — moving average** | Raw materials and trading goods with strongly fluctuating purchase prices |

The standard price gives stable, predictable costs in production; the moving average reflects real market fluctuations directly in the stock value.

## A worked example with the standard price

The logic is clearest with a fully worked example. Starting position in the material master:

- **Opening stock:** 100 pieces
- **Total value:** EUR 200.00
- **Standard price:** EUR 2.00 per piece

The plan: a goods receipt of 100 pieces at an **order price of EUR 2.40**, followed by an invoice receipt for the same 100 pieces at an **invoice price of EUR 2.20**.

### Step 1 — post the goods receipt

After the goods receipt, the material master shows:

- **Stock:** 200 pieces (100 old + 100 new)
- **Total value:** EUR 400.00 (200 old + 200 new, each valued at the standard price)
- **Standard price:** unchanged at EUR 2.00

The key point: the stock account only moves at the standard price, never at the order price. The postings in the accounting document:

- **Stock account:** +EUR 200 (= 100 pieces × EUR 2.00 standard price)
- **GR/IR clearing account:** +EUR 240 (= 100 pieces × EUR 2.40 order price)
- **Price differences (expense):** +EUR 40 (= difference EUR 2.40 − EUR 2.00 × 100 pieces)

Because the order price is above the standard price, the price difference is booked as an **expense**.

### Step 2 — post the invoice receipt

The invoice arrives for 100 pieces at EUR 2.20 instead of the ordered EUR 2.40. Afterwards:

- **Stock:** stays 200 pieces (the invoice changes no quantity)
- **Total value:** stays EUR 400.00
- **Standard price:** stays EUR 2.00

In the accounting document the GR/IR account is cleared at the order price, the vendor account is updated at the invoice price, and the difference posts to the price-difference account:

- **GR/IR clearing account:** −EUR 240 (clearing the goods receipt)
- **Vendor account:** +EUR 220 (= 100 × EUR 2.20 invoice price)
- **Price differences (income):** +EUR 20 (= difference EUR 2.40 − EUR 2.20 × 100 pieces)

Because the invoice price is below the order price, this time the price difference is booked as **income**. Both directions — expense and income — are entirely normal and depend only on whether the actual price sits above or below the reference.

## The GR/IR clearing account: the central go-between

The **GR/IR clearing account** (goods receipt / invoice receipt) is one of the most important accounts in valuation. Its job is to bridge the timing gap between goods receipt and invoice receipt:

- On the **goods receipt**, order price × quantity is posted to it.
- On the **invoice receipt**, the same amount is cleared again.
- If the goods are here but the invoice isn't, the open balance shows the **goods received but not yet invoiced**.
- If the invoice is here but the goods aren't, the balance (with the opposite sign) shows the **deliveries not yet received**.

The account is balance-sheet-relevant and belongs to every period-end close: it is analysed to work out which items are old and uncleared and where something is still missing. A GR/IR balance that stays open for a long time is a reliable sign of an incomplete process.

## How the order price is determined in the first place

A common misconception: the purchase order does *not* propose the valuation price from the material master. Instead SAP searches for the price hierarchically, **from the specific to the general**:

1. First it looks for a **purchasing info record** for the vendor/material combination at purchasing-organisation/plant level.
2. If nothing is found there, it searches at purchasing-organisation level.
3. If there is no data at that level either, the price has to be entered manually.

If an info record exists, **valid conditions** take priority. If those are missing or expired, the system reads the number of the last purchasing document from the info record and proposes the price from that document.

If you want to look at the upstream step, [What is a purchase requisition in SAP?](/blog/en/what-is-a-purchase-requisition/) is a good starting point into the procurement flow.

## What this means for you day to day

Price control and the configuration of the valuation accounts are the job of customising and accounting — not of the individual user. But you see the *effect* every day as a buyer or planner:

- When you **post a goods receipt**, the accounting postings run automatically — the system does the maths, you do nothing.
- When an **invoice with a deviation** comes in, you see the price difference in the invoice document, posted to the appropriate account.
- When a material shows an **unexpected stock value**, it's worth looking at the material document overview and the linked accounting document.
- When a **GR/IR balance** stays open for a long time, it points to a missing invoice or delivery — a classic for the period-end close.

## Common pitfalls

- **Confusing the stock account with the order price.** With the standard price, the stock account only ever moves at the standard price. Any deviation lands on the price-difference account — not in the stock value.
- **Mistaking price differences for an error.** Expense or income from price differences is entirely normal under standard-price control. It only shows whether the actual price was above or below the standard price.
- **Ignoring the open GR/IR balance.** A balance there almost always means a process is half finished — goods without an invoice, or an invoice without goods.

## In a nutshell

Material valuation keeps the **value of your stock** correct in accounting at all times. Every valuation-relevant movement creates an accounting document alongside the material document. Whether a material runs on a fixed **standard price (S)** or a **moving average price (V)** decides how price deviations are booked — under the standard price via a price-difference account, under the moving average directly in the valuation price. The GR/IR clearing account keeps goods receipt and invoice tied together. Once you've grasped those three building blocks — valuation relevance, price control and the GR/IR account — the valuation logic across the whole SAP system falls into place.

## Frequently asked questions

### What is the difference between standard price and moving average price?

The standard price (S) stays constant through the fiscal year; any deviation from the purchase price posts to a price-difference account. The moving average price (V) is recalculated as a weighted average with every receipt, so it adjusts continuously.

### Where is a material's price control maintained?

In the material master, on the Accounting 1 view. That is where the S or V indicator sits, together with the current valuation price and the total stock value.

### What is the GR/IR clearing account for?

It bridges the gap between goods receipt and invoice receipt. The goods receipt posts to it and the invoice clears it again. An open balance signals that either an invoice or a delivery is still missing.

### Why does a material suddenly show an unexpected stock value?

Usually because of a valuation-relevant posting — for example a goods receipt at a very different price, or a manual revaluation. Looking at the material document and the linked accounting document shows what happened.
