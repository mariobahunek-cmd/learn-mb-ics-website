---
layout: post
lang: en
title: "Invoice verification with MIRO: the 3-way match in SAP MM explained"
description: "The 3-way match of purchase order, goods receipt and invoice: how MIRO checks variances, blocks payment and clears the GR/IR account in SAP MM."
slug: miro-invoice-verification-3-way-match
permalink: /blog/en/miro-invoice-verification-3-way-match/
translation_key: post-invoice-verification
date: 2026-07-08
category: "Purchasing"
keywords: "SAP MIRO, 3-way match, logistics invoice verification, GR/IR clearing account, invoice block, tolerances, SAP MM, goods receipt"
reading_time: 10
sources:
  - label: "SAP Help Portal — Logistics Invoice Verification (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Materials Management / Logistics Invoice Verification area — general background. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the 3-way match in SAP?"
    a: "The 3-way match is the comparison of three documents: the purchase order, the goods receipt and the supplier invoice. Only when price and quantity line up across all three does the invoice go through without a block. The system pulls the proposed values automatically from the purchase order and the goods receipt."
  - q: "What is the GR/IR clearing account for?"
    a: "The GR/IR clearing account is a transit account between materials management and financial accounting. The goods receipt credits it, and the invoice debits it again to clear it. If a balance remains, either the invoice or the goods receipt is still missing."
  - q: "Does logistics invoice verification pay the invoice?"
    a: "No. Logistics invoice verification records, checks and posts the invoice, creating an invoice document and an accounting document in the process. The actual payment and the management of open items are handled by financial accounting (FI)."
  - q: "What happens when an invoice falls outside tolerance?"
    a: "The system still posts the invoice but automatically sets a payment block. The invoice is then visible in the system but must not be paid until someone reviews the reason and manually releases the block."
  - q: "What does a yellow traffic light in MIRO mean?"
    a: "Green means the invoice can be posted, yellow means it can be posted but with a payment block, and red means it cannot be posted. A yellow light with a balance of zero means the figures add up, but the system will block the invoice for payment because of a variance."
---

A supplier invoice lands on your desk. Accounting wants to know whether it can be released for payment. Were the goods actually delivered? Does the invoice price match the purchase order? And will a balance be left sitting on a clearing account at the end? These are exactly the questions logistics invoice verification answers in SAP MM — using the MIRO transaction and the 3-way match.

## In short: what the 3-way match does

The 3-way match is the core principle of invoice verification: three documents — the **purchase order**, the **goods receipt** and the **supplier invoice** — are compared against one another. Only when price and quantity line up across all three does the invoice go through cleanly. The system pulls the proposed values automatically from the purchase order and the goods receipt; you simply compare them with your supplier's invoice and post.

## What is logistics invoice verification in SAP MM?

Logistics invoice verification is the third and final major step in the operational procurement process. After creating the purchase order and posting the goods receipt, this is where you record the incoming supplier invoice, check it for *content*, *price* and *arithmetic* accuracy, and post it to the system. Doing so creates an **invoice document** (an MM document) and an **accounting document** (an FI document) at the same time — both independent, yet linked to each other.

The clean division of labor matters here: logistics invoice verification only checks and posts. It is **not** responsible for the actual payment or for managing open payables — that falls to financial accounting (FI).

In S/4HANA there are two ways to record an invoice:

- **The MIRO transaction** (“Enter incoming invoice”) — the single-screen transaction for logistics invoice verification, where you capture every entry on one screen.
- **The SAP Fiori app for creating a supplier invoice** — the modern variant in the launchpad, with identical logic behind the scenes.

Both routes lead to the same result: a posted invoice document referencing the purchase order and the goods receipt.

## The three documents in the 3-way match

The 3-way match compares three documents that come from three different departments. Each contributes its own part to the check:

| Document | Source | What is checked? |
| --- | --- | --- |
| Purchase order | Purchasing | order price, ordered quantity, supplier, tax code, payment terms |
| Goods receipt | Warehouse / receiving | delivered quantity, delivery date, delivery note number, plant and storage location |
| Supplier invoice | Logistics invoice verification | invoice price, invoiced quantity, gross amount, reference number, invoice date |

When the order price, the goods receipt value and the invoice price are identical, and the quantities match too, the balance in MIRO drops to zero — the invoice can be posted. In reality, though, there are almost always small variances. That is exactly where tolerances and blocking reasons come in, more on which shortly.

## The goods receipt posting: the GR/IR clearing account

To understand what MIRO posts, you first have to understand what the goods receipt posts. For a valuated goods receipt against a purchase order item for stock material, the following happens:

- A **debit** to the *stock account* for the amount “goods receipt quantity × valuation price”
- A **credit** to the **GR/IR clearing account** for the amount “goods receipt quantity × order price”

The GR/IR clearing account (goods-receipt / invoice-receipt clearing account) is the central link between materials management and financial accounting. It is a *transit account*: when the goods have arrived but the invoice is still missing, this account carries an open amount (goods received, not yet invoiced). As soon as the invoice is posted with MIRO, the system clears the GR/IR account again.

When a material is received under the *standard price* control (S), a value difference can arise. The example below shows a goods receipt posting for 25 units at 88 EUR order price each, with a standard price of 110 EUR held in the material master:

| G/L account | Description | Debit | Credit |
| --- | --- | --- | --- |
| 3001 | Inventory — trading goods | 2,750.00 EUR | |
| 4500 | GR/IR clearing account | | 2,200.00 EUR |
| 8001 | Gain from price differences | | 550.00 EUR |

The stock account is valued at the standard price (25 × 110 EUR), the GR/IR account receives the order price (25 × 88 EUR), and the value difference goes to a price-difference account. It works differently for materials under the *moving average price* (V): there the difference flows straight into the stock account, and the average price in the material master is recalculated automatically. (The G/L account numbers here are illustrative only — in a real system they depend on the chart of accounts in use.)

## Posting the supplier invoice with MIRO

When you now record the matching supplier invoice with MIRO, the logic reverses. The system pulls in the purchase order reference, proposes the open goods receipt quantity, and compares the invoice amount with what was left on the GR/IR account after the goods receipt.

The single-screen MIRO transaction is divided into several areas:

- **Transaction** — here you choose whether you are recording an invoice, a credit memo, a subsequent debit or a subsequent credit.
- **Header data** — invoice date, reference (the supplier's invoice number), gross amount, tax amount with tax code, company code.
- **Assignment / PO reference** — here you link the invoice to a purchase order, delivery note or bill of lading.
- **Invoice items** — the list of all proposed items; the flagged lines are the ones that get posted.
- **Supplier data** — details about the invoicing party from the supplier master record (maintained via the business partner in S/4HANA).
- **Balance with traffic light** — green means it can be posted, yellow means it can be posted with a payment block, red means it cannot be posted.

Three things happen at once when you post:

1. The **GR/IR clearing account** is cleared again at the order price (a debit).
2. The **supplier account** is credited with the gross invoice amount.
3. Any differences between the order price and the invoice price are posted — depending on the material's price control — either to the stock account or to a price-difference account.

A simple posting example for an invoice of 2,618 EUR gross (25 units of material at 88 EUR each, plus 180 EUR of unplanned freight and 238 EUR of input tax):

| G/L account | Description | Debit | Credit |
| --- | --- | --- | --- |
| 4500 | GR/IR clearing account | 2,200.00 EUR | |
| 5050 | Delivery costs (freight) | 180.00 EUR | |
| 1576 | Input tax | 238.00 EUR | |
| 4400 | Supplier account | | 2,618.00 EUR |

**A tip from practice:** before you hit *Post*, always choose *Simulate* in MIRO. The system then shows you exactly which accounts will be posted with which amounts. If the balance isn't zero, something is off — usually the gross amount, the tax code or an item quantity.

## Tolerances and blocking reasons: when does the system block an invoice?

In practice, the invoice amount almost always differs a little from the purchase order or the goods receipt — through rounding differences, freight costs or price changes. SAP therefore works with **tolerances**, defined in the Customizing for logistics invoice verification. If a variance stays within tolerance, the invoice posts normally. If it lands *outside*, the system posts the invoice anyway — but automatically sets an **invoice block** (the yellow traffic light in the balance area).

The most important checks at a glance:

| Check | What is compared? | Typical block |
| --- | --- | --- |
| Price variance | order price against invoice price per unit | price block |
| Quantity variance | invoiced quantity against open goods receipt quantity | quantity block |
| Date / schedule variance | invoice date against planned delivery date | date block |
| Amount variance | an item's invoice total against the expected amount | amount block |

A blocked invoice is posted and therefore visible in the system — but financial accounting must *not* release it for payment while the block is active. Blocked invoices are reviewed and manually released through the MRBR transaction (“Release blocked invoices”) or the corresponding Fiori app. Only then does the money flow.

On top of that, there are **manual blocking reasons** that a clerk can set directly in MIRO — for example in cases needing clarification, quality issues or open complaints. The same rule applies: posted yes, paid no.

## Common variances and how to resolve them

Day to day, the same situations keep coming up. Here is an overview of how SAP handles them and what you, as a user, need to do:

- **Invoice price higher than the order price, within tolerance:** The invoice is posted. For standard-price material, the difference lands on a price-difference account. For moving average price, the material master is revalued — the stock becomes more expensive.
- **Invoice price higher than the order price, outside tolerance:** The invoice is posted but blocked for payment. After clarifying with the supplier, it is released via MRBR.
- **Invoiced quantity greater than the delivered quantity:** a quantity variance. Either another delivery is on its way — or the supplier billed incorrectly. If the overage exceeds tolerance, the invoice stays blocked.
- **Freight costs on the invoice, but not in the purchase order:** record them in MIRO as *unplanned delivery costs*. How they are posted depends on Customizing — the system either distributes them across the invoice items (and thus to stock or price differences) or posts them to a separate G/L account, as in the posting example above on account 5050.
- **Invoice arrives before the goods receipt:** possible, but risky — the balance stays open on the GR/IR account. The usual order is goods receipt first, invoice second.
- **Subsequent debit or credit:** If the supplier later claims a pure price change, you record a “subsequent debit” or “subsequent credit” in MIRO. Distinct from that is the *credit memo* (a separate transaction type in MIRO): it represents an actual supplier credit — for example for a returned delivery — and reduces both quantity and value. Cancelling an already posted invoice document, in turn, is a different operation (invoice reversal, transaction MR8M) and not a credit memo you enter yourself.

The purchase order history is also useful: in every purchase order you can see how much has already been delivered and how much has already been invoiced. It's the quickest way to check the consistency of goods receipt and invoice.

## In a nutshell

Logistics invoice verification with MIRO is the link between purchasing, the warehouse and accounting. It makes sure a company only pays for what was actually ordered and delivered — and that the GR/IR clearing account ends up back at zero. The 3-way match of purchase order, goods receipt and invoice is the core principle; tolerances and blocking reasons ensure that only clean invoices go through to payment automatically. Once you keep the division of labor between MM (checking and posting) and FI (paying) clear, and understand the posting logic around the GR/IR account, you have the topic under control.

## Frequently asked questions

### What is the 3-way match in SAP?

The 3-way match is the comparison of three documents: the purchase order, the goods receipt and the supplier invoice. Only when price and quantity line up across all three does the invoice go through without a block. The system pulls the proposed values automatically from the purchase order and the goods receipt.

### What is the GR/IR clearing account for?

The GR/IR clearing account is a transit account between materials management and financial accounting. The goods receipt credits it, and the invoice debits it again to clear it. If a balance remains, either the invoice or the goods receipt is still missing.

### Does logistics invoice verification pay the invoice?

No. Logistics invoice verification records, checks and posts the invoice, creating an invoice document and an accounting document in the process. The actual payment and the management of open items are handled by financial accounting (FI).

### What happens when an invoice falls outside tolerance?

The system still posts the invoice but automatically sets a payment block. The invoice is then visible in the system but must not be paid until someone reviews the reason and manually releases the block.

### What does a yellow traffic light in MIRO mean?

Green means the invoice can be posted, yellow means it can be posted but with a payment block, and red means it cannot be posted. A yellow light with a balance of zero means the figures add up, but the system will block the invoice for payment because of a variance.
