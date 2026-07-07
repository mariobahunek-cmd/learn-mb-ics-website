---
layout: post
lang: en
title: "Order-to-Cash in SAP: The Sales Process Step by Step"
description: "Order-to-cash explained: from sales order through delivery and goods issue to incoming payment. How the sales process works in SAP S/4HANA — in plain language for users."
slug: order-to-cash-process-sales
permalink: /blog/en/order-to-cash-process-sales/
translation_key: post-order-to-cash
date: 2026-07-07
category: "Sales"
keywords: "order-to-cash, SAP sales, order processing, sales order, delivery, goods issue, billing document, document flow, S/4HANA Sales"
reading_time: 9
sources:
  - label: "SAP Help Portal — Sales (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Sales area — general background on the order-to-cash process. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What does order-to-cash mean?"
    a: "Order-to-cash describes the complete sales process in SAP — from the customer's order to the incoming payment. The term literally means “from order to cash in the bank”."
  - q: "What is the difference between a delivery and a sales order?"
    a: "The sales order is the commercial sales document holding the customer, material, price and date. The delivery is a separate logistics document with shipping point, storage location and goods-issue date — not just a copy of the order."
  - q: "Why is goods issue posted before the invoice?"
    a: "The invoice should only bill what was actually shipped. So SAP first posts the goods issue (goods leave the warehouse) and only then creates the billing document, keeping stock and accounting consistent."
  - q: "What is the document flow in sales?"
    a: "The document flow shows how the documents of a process connect: sales order, delivery, goods issue, invoice and payment all reference each other. One click lets you trace any transaction back to the original order."
---

When a customer orders something and, at the end, the money lands in the bank, there is a continuous chain in between — and in SAP it has a fixed name: **order-to-cash**, often also called order processing or simply the sales process. It is the core process in SAP Sales. This article walks through the whole path step by step — in plain language, from a user's point of view.

## In short: from order to cash in the bank

Order-to-cash (**O2C** for short) describes the **complete sales process** in SAP S/4HANA — from the customer's first order to the actual receipt of money in the bank. The term means, roughly, *“from order to cash”*, and that's exactly how to think about it: as a continuous chain in which each step triggers the next and each document references the one before it.

In sales, O2C is the guiding process. Everything else — master data, pricing, availability checks, reporting — ultimately serves the same purpose: running this chain cleanly from start to finish.

## The six steps at a glance

Before we dive into each step, here is the fixed sequence:

1. **Create the sales order**
2. **Create the delivery**
3. **Picking** (assembling the goods)
4. **Post goods issue**
5. **Create the billing document** (invoice)
6. **Post the incoming payment**

One point matters especially: **goods issue comes before billing**, not after. Why that is, we'll see in step 4.

## Step 1: Create the sales order

Everything starts with the **sales order**. The customer has ordered something — by phone, by e-mail, through a web shop or directly via inside sales — and a clerk records that order in SAP.

The sales order is the **first document** in the process and therefore the trigger for everything that follows. In essence, it contains:

- the **sold-to party** and, where different, the **ship-to party**, **bill-to party** and **payer**
- the ordered **material** and its quantity
- the agreed **price** (determined through pricing)
- the requested **delivery date**
- the **sales organization**, **distribution channel** and **division** (together: the sales area)

When the order is created, several things happen automatically in the background: SAP runs the **availability check (ATP)**, determines the price through pricing, and proposes a delivery date.

Behind the word “customer”, modern S/4HANA holds the **business partner** in the role “customer”. If that concept is still new, the article on the [business partner concept in S/4HANA](/blog/en/business-partner-concept-s4hana/) will help.

## Step 2: Create the delivery

Once the sales order is in place and the goods are available, the second document is created: the **outbound delivery**. It is the handover from the commercial sales document into logistics.

The delivery is **not just a copy** of the sales order. It is a separate logistics document that bundles all the data the warehouse needs in order to ship:

- which **material** is shipped in which **quantity**
- from which **plant** and which **storage location** the goods come
- to which **shipping point** the order is assigned
- the planned **goods-issue date**

The delivery can be created **individually** for a single sales order or in a **collective run** for many orders at once. In day-to-day sales, the collective run is the norm. Remember: with the delivery, the process moves from sales into logistics — from here on, SAP no longer thinks in terms of “order” but of “shipment”.

## Step 3: Picking

Before anything leaves the warehouse, the goods have to be **physically assembled**. SAP calls this step **picking**. It covers everything that happens in the warehouse to make the delivery ready to ship:

- the warehouse operator receives the **picking list**
- they take the materials from their respective storage bins
- the **picked quantity** is recorded in the delivery and reconciled against the **requested quantity**
- if needed, the goods are packed and placed on a shipping unit (a pallet, for example)

If the company runs a connected **warehouse management system (EWM)**, picking runs there as its own process with warehouse tasks. What matters is the basic idea: picking is the physical step between delivery and goods issue — and it is not the same thing as goods issue. First you pick, then you post.

## Step 4: Post goods issue

Now comes one of the most important steps: the **goods issue** (GI). With goods issue you tell the system: *“The goods have left the warehouse.”* This posting triggers a whole chain automatically:

- the material's **stock** is reduced in the system
- a **material document** is created automatically (it records the quantity movement)
- an **accounting document** is created automatically (it records the value posting in Finance)
- on the cost side, the **cost of goods sold** is charged

This same double posting — one material document, one accounting document — is familiar from goods receipt in materials management. In sales it happens as a mirror image, just in the other direction: stock *out* instead of *in*.

And here's the central point: **goods issue must be posted before billing.** The reason is simple — the invoice should only bill what was actually shipped. If the invoice ran before goods issue, a customer could be billed for goods still sitting in the warehouse, or the accounting documents would be inconsistent. That's why SAP enforces this sequence.

## Step 5: Create the billing document

Only after goods issue is the **billing document** (invoice) created. It is the document that bills the customer for the goods or service. When it is created, the following happens:

- SAP pulls the relevant data from the **sales order** and the **delivery**
- the **conditions** (prices, discounts, taxes) are finalized
- a **billing document** is created
- in parallel, an **accounting document** is created automatically: the *open receivable* against the customer

The billing document can be **order-related** or **delivery-related**. In classic order-to-cash with physical goods, the *delivery-related* invoice is standard — it references the delivery directly. For pure services without a delivery note, the *order-related* invoice is used. When the billing document is posted, sales hands the transaction over to Finance; the open item on the customer's account is the bridge between the two areas.

## Step 6: Post the incoming payment

The final step is the **incoming payment**. The customer pays the invoice, and the open receivable is cleared. This step no longer happens in sales but in **Finance (FI)** — yet it still belongs to the O2C process. Typically, at this point:

- the incoming money is posted to the bank account
- the **open item** on the customer's account is **cleared**
- any cash discount, rounding difference or partial payment is handled

You don't need to go deep into the FI postings for this. The takeaway is enough: sales and Finance are linked through the integrated posting of the billing document, and only the incoming payment fully closes the order-to-cash loop.

## The document flow: how it all connects

One of the most important concepts in sales is the **document flow**. At each step a new document is created that **references the previous one**. Run cleanly, the chain looks like this:

*Sales order → Delivery → Goods issue (material document + accounting document) → Billing document → Accounting document → Incoming payment*

In every one of these documents you can display the document flow with a single click. At a glance, it shows you:

- which sales order a delivery came from
- which invoice belongs to which delivery
- whether goods issue has already been posted
- whether a payment has already come in

The document flow guarantees **traceability and audit reliability**: every cent that comes in from a customer can be traced back to the original order. In everyday sales, that is worth its weight in gold.

## Common pitfalls

- **Swapping the order of goods issue and billing.** Goods issue first, then billing — not the other way around. Only what has left the warehouse may be invoiced.
- **Treating the sales order and delivery as the same thing.** The delivery is not a clone of the order but a separate logistics document with shipping point, storage location and goods-issue date.
- **Confusing picking with goods issue.** Picking is the physical assembling; goods issue is the posting of the goods leaving — two distinct steps.
- **Mixing up order-related and delivery-related billing.** For physical goods the invoice is delivery-related; for pure services it is order-related.

## In a nutshell

Order-to-cash is the continuous chain from the sales order to the incoming payment. A customer orders (sales order), the warehouse prepares the shipment (delivery), the goods are assembled (picking), the shipment is posted (goods issue with a material and an accounting document), the customer is billed (billing document), and finally the money arrives (incoming payment in Finance). Once you've internalized that story and the **document flow** as a picture, you already understand a large part of SAP sales — because then you don't just recognize the terms, you also see how they fit together.

## Frequently asked questions

### What does order-to-cash mean?

Order-to-cash describes the complete sales process in SAP — from the customer's order to the incoming payment. The term literally means “from order to cash in the bank”.

### What is the difference between a delivery and a sales order?

The sales order is the commercial sales document holding the customer, material, price and date. The delivery is a separate logistics document with shipping point, storage location and goods-issue date — not just a copy of the order.

### Why is goods issue posted before the invoice?

The invoice should only bill what was actually shipped. So SAP first posts the goods issue (goods leave the warehouse) and only then creates the billing document, keeping stock and accounting consistent.

### What is the document flow in sales?

The document flow shows how the documents of a process connect: sales order, delivery, goods issue, invoice and payment all reference each other. One click lets you trace any transaction back to the original order.
