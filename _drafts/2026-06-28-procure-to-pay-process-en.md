---
layout: post
lang: en
title: "Procure-to-Pay in SAP: the procurement process from demand to payment"
description: "Procure-to-Pay (P2P) in SAP S/4HANA explained in plain language: from demand through purchase requisition, order and goods receipt to invoice verification and payment."
slug: procure-to-pay-process
permalink: /blog/en/procure-to-pay-process/
translation_key: post-procure-to-pay
date: 2026-07-07
category: "Purchasing"
keywords: "procure-to-pay, P2P, procurement process, SAP MM, purchase requisition, purchase order, goods receipt, invoice verification, three-way match, purchasing"
reading_time: 8
sources:
  - label: "SAP Help Portal — Sourcing and Procurement (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Materials Management / Sourcing and Procurement — general background on the procurement process. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between a purchase requisition and a purchase order?"
    a: "The purchase requisition is an internal document with which a department tells purchasing about a demand. The purchase order is the binding document that goes outward to the supplier. Only the purchase order is legally binding."
  - q: "What happens during a goods receipt in SAP?"
    a: "During a goods receipt for a purchase order, the goods are received into the system: the stock of the material increases, and SAP automatically creates a material document for the quantity movement and an accounting document for the value posting."
  - q: "What is the three-way match?"
    a: "The three-way match compares the purchase order, the goods receipt and the invoice on quantity and price. Only when all three documents agree does the invoice go through cleanly. If a discrepancy exceeds tolerance, SAP blocks the invoice for clarification."
  - q: "Why does a purchase order sometimes stay open?"
    a: "Common reasons are a release that is still pending, an invoice blocked because of a price or quantity discrepancy, or a delivery that has not yet been posted as a goods receipt. Purchase order monitoring shows where the process is stuck."
  - q: "Where does the procurement process end?"
    a: "From purchasing's point of view it ends with the verified invoice. The actual payment to the supplier takes place in financial accounting (FI), usually through the automatic payment run. That closes the procure-to-pay loop."
---

"Why hasn't my order reached the supplier yet?" — participants ask me that in almost every training session, and just as often there is no purchase order behind it at all, only a purchase requisition. That's exactly where the procurement process begins: with a demand that is first reported internally and only later goes outward as a binding purchase order. In SAP, this whole path from demand to payment is called **Procure-to-Pay**, or **P2P** for short. Let's walk through it from the start, with the terms you keep running into in SAP procurement.

## The big picture: from demand to payment

Procure-to-Pay describes the complete procurement process in SAP, from the first demand in the company to the final payment to the supplier. In the **SAP MM (Materials Management)** module this is the core process: everything else you do in purchasing builds on this flow.

In practice, the procurement cycle can be described as a chain of eight phases:

1. **Determining demand** — manually or automatically via material requirements planning
2. **Finding a source of supply** — who do we buy from?
3. **Selecting the supplier** — comparing prices and terms
4. **Processing the order** — creating the purchase order
5. **Monitoring the order** — tracking the status
6. **Goods receipt** — receiving the goods
7. **Invoice verification** — reconciling the supplier invoice
8. **Payment processing** — in accounting

Sounds like a lot? Once you understand the flow as a logical story, the rest almost falls into place. Let's go through the phases one by one.

## Step 1: Determining demand

Everything starts with a **demand**. Somewhere in the company, something is needed. That demand comes in two flavours:

- **Manual demand:** a specialist department notices something is missing and reports the demand to purchasing.
- **Automatic demand via material requirements planning (MRP):** SAP regularly checks stock levels and reports automatically when a minimum stock is breached or when production triggers a demand.

Material requirements planning (MRP) automatically creates a purchase requisition when it detects a demand. That way, nobody has to track by hand when a given stock is running low.

## Creating the purchase requisition

After the demand has been determined, a **purchase requisition** is created. The key thing to understand: the requisition is a purely internal document. It doesn't go to the supplier — it's a request from the specialist department to purchasing: "Please procure the following for us."

A purchase requisition typically contains:

- what is to be procured (material number or description)
- how much of it
- by when
- for what purpose (cost centre, order, project)

It can be entered manually or created automatically by material requirements planning. For a closer look: [What is a purchase requisition in SAP?](/blog/en/what-is-a-purchase-requisition/)

## Step 2: Finding a source of supply — who do we buy from?

Once the purchase requisition exists, the next question comes up: **which supplier do we buy from?** Finding a source of supply is exactly this step. SAP offers several aids for it:

- **Info record:** holds the terms between a specific material and a specific supplier (for example price, delivery time)
- **Source list:** governs which suppliers are allowed at all, and which one is preferred in a given period
- **Outline agreements:** long-term arrangements with a supplier

For outline agreements, SAP distinguishes two forms — the contract and the scheduling agreement:

- **Contract:** a framework agreement over a total quantity (**quantity contract**) or a total value (**value contract**); it's called off flexibly via contract release orders
- **Scheduling agreement:** specific delivery dates and quantities are scheduled and called off over time (typical in series production)

## Step 3: Selecting the supplier and comparing terms

Once possible sources have been identified, it comes down to the final supplier selection. Here purchasing compares:

- prices from different sources or quotations
- delivery times
- delivery and payment terms
- quality and the supplier's past performance

Optionally, a **release procedure** kicks in at this point: for larger amounts in particular, a four-eyes principle is mandatory. The requisition or order first has to be released before it moves on — a deliberately built-in control step.

## Step 4: Creating the purchase order

Now comes the central step: the **purchase order** (PO for short). Unlike the requisition, the purchase order is an external document. It goes outward to the supplier and is legally binding.

Among other things, the purchase order contains:

- supplier
- material and quantity
- price and terms
- delivery date
- delivery address (for example a specific plant or warehouse)
- invoicing party

A purchase order can be created directly from a purchase requisition, from an outline agreement, or entirely manually. The data from the requisition — material, quantity, plant, date — is carried over in the process.

## Step 5: Monitoring the order

After the purchase order has been sent, **order monitoring** runs. Purchasing keeps an eye on whether a delivery has already arrived for an order item and whether an invoice has already been entered. If a delivery is overdue, it has to be chased with the supplier.

Ideally the supplier sends back an **order confirmation** in the meantime, so purchasing can store the agreed delivery date in the system. Order confirmations aren't mandatory, though.

## Step 6: Goods receipt

Once the goods physically arrive at the warehouse, the most interesting step from a user's point of view arrives: the **goods receipt**. The goods are received into SAP, that is, posted into the system both in quantity and in value.

What happens when you post it? The stock of the material increases, and SAP creates two documents at once: a **material document** that records the quantity movement, and an **accounting document** for the value posting. This double posting is why a goods receipt in SAP, as a rule, doesn't "only" change stock levels but also touches financial accounting.

## Step 7: Invoice verification and the three-way match

At some point the **supplier's invoice** arrives. It's entered in SAP via logistics invoice verification. In doing so, the system does something very important: the **three-way match**.

Three documents are compared with one another:

| Document | Question |
| --- | --- |
| **Purchase order** | What was agreed? |
| **Goods receipt** | What was actually delivered? |
| **Invoice** | What is the supplier charging us? |

Only when these three documents **agree on quantity and price** does the invoice go through cleanly. If the variances exceed the configured tolerances, SAP automatically blocks the invoice for clarification.

An example: 100 pieces at 5 euros were ordered, and 100 pieces were delivered. But if the supplier now charges 6 euros per piece, SAP spots the price difference and holds the invoice back for review. It's exactly this mechanism that makes the three-way match one of the most important control points in the procurement process.

## Step 8: Payment processing in FI

Once the invoice has passed verification, procurement is complete from the MM point of view. The final step takes place in the **SAP FI (Finance)** module: the actual **payment to the supplier**.

In FI the open payable is settled, typically through the automatic payment run or a manual payment. That closes the procure-to-pay loop. To understand the picture, it's enough to know:

- The payment happens in **FI**, not in MM.
- MM and FI are linked through **integrated posting**.
- The accounting documents from the goods receipt and invoice verification are the bridge between the two modules.

## Special cases: not every procurement runs in a straight line

Alongside the standard procurement process, there are **special procurement processes** that deviate from the straight path:

- **Stock transfer with a stock transport order** — an internal order between two plants of the same company. Between dispatch and receipt, the goods sit in stock in transit.
- **Subcontracting** — an external supplier manufactures using components provided by the company.
- **Supplier consignment** — the supplier provides the goods, and ownership only passes on withdrawal.

Which process applies to an order item is controlled by the **item category** in SAP. For everyday work it's enough to recognise that these variants exist — the basic flow of demand → order → goods receipt → invoice stays the same.

## Common pitfalls

Many participants mentally swap the goods receipt and invoice verification — but as a rule the goods come first and the invoice second, and the three-way match kicks in in exactly that order. These are the mix-ups I run into most often:

- **Confusing requisition and order.** The requisition is internal; the order goes outward. If you're asking a supplier why "the order" hasn't arrived, first check whether a purchase order even exists yet.
- **Overlooking a missing release.** A requisition or order that hasn't been released won't be processed further. A glance at the release status saves a lot of searching.
- **Mixing up material document and accounting document.** A goods receipt creates two documents: one for the quantity, one for the value. They belong together, but they aren't the same thing.
- **Not recognising a blocked invoice.** If the invoice deviates on quantity or price beyond tolerance, SAP blocks it automatically. The invoice is then entered but not yet ready for payment — it has to be clarified first.

## What it comes down to

Procure-to-Pay is the thread running through SAP procurement: someone needs something (demand), reports it internally (purchase requisition), purchasing finds a supplier (source of supply), gets a release where needed, sends out a purchase order, receives the goods (goods receipt with a material and an accounting document), receives the invoice, reconciles everything (three-way match), and pays in FI. Once you understand this flow as one connected story, you can work out almost any detail question in purchasing yourself, instead of memorising individual terms in isolation.

## Frequently asked questions

### What is the difference between a purchase requisition and a purchase order?

The purchase requisition is an internal document with which a department tells purchasing about a demand. The purchase order is the binding document that goes outward to the supplier. Only the purchase order is legally binding.

### What happens during a goods receipt in SAP?

During a goods receipt for a purchase order, the goods are received into the system: the stock of the material increases, and SAP automatically creates a material document for the quantity movement and an accounting document for the value posting.

### What is the three-way match?

The three-way match compares the purchase order, the goods receipt and the invoice on quantity and price. Only when all three documents agree does the invoice go through cleanly. If a discrepancy exceeds tolerance, SAP blocks the invoice for clarification.

### Why does a purchase order sometimes stay open?

Common reasons are a release that is still pending, an invoice blocked because of a price or quantity discrepancy, or a delivery that has not yet been posted as a goods receipt. Purchase order monitoring shows where the process is stuck.

### Where does the procurement process end?

From purchasing's point of view it ends with the verified invoice. The actual payment to the supplier takes place in financial accounting (FI), usually through the automatic payment run. That closes the procure-to-pay loop.
