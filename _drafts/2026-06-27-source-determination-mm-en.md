---
layout: post
lang: en
title: "Source determination in SAP MM: info records, source lists, contracts and quotas"
description: "How SAP finds a source of supply in purchasing: info records, outline agreements, the source list and quota arrangements — from demand to the proposal."
slug: source-determination-mm
permalink: /blog/en/source-determination-mm/
translation_key: post-source-determination
date: 2026-07-08
category: "Purchasing"
keywords: "SAP source determination, SAP purchasing info record, SAP source list, SAP contract, SAP scheduling agreement, SAP quota arrangement, SAP outline agreement, SAP purchase requisition"
reading_time: 10
sources:
  - label: "SAP Help Portal — Source Determination (Materials Management, SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Materials Management / Purchasing area — general background on source determination. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is source determination in SAP MM?"
    a: "Source determination is the step in which SAP automatically works out the right source of supply for a material demand — that is, the supplier or the outline agreement the material is procured from. To do this, the system evaluates four tools: the purchasing info record, the outline agreement, the source list and the quota arrangement."
  - q: "What is the difference between a contract and a scheduling agreement?"
    a: "Both are outline agreements. A contract agrees a total quantity or a total value but calls off no fixed dates — deliveries follow later as individual release orders. A scheduling agreement additionally fixes the concrete delivery dates and quantities in schedule lines and serves as the supply document itself."
  - q: "What is the source list for?"
    a: "The source list defines, per material and plant, which sources of supply are allowed, preferred or blocked in a given period. Where source-list requirement is set, a material may only be procured through the sources entered there. It therefore controls who is allowed to supply at all."
  - q: "What does the quota arrangement do?"
    a: "The quota arrangement splits demand by percentage across several permitted sources of supply, for example 60 percent to one supplier and 40 percent to another. It does not replace the source list but complements it: the source list says who may supply, and the quota splits the demand between those permitted."
  - q: "Does the quota arrangement work automatically?"
    a: "No. It only takes effect when two things come together: the quota usage is maintained in the material master, and a valid quota arrangement exists. If either is missing, the quota arrangement is ignored."
---

When a company needs a material, someone has to decide where it comes from. In SAP, the system makes much of that decision itself — through source determination. This article explains, in plain language, which tools work together and how SAP ends up proposing the right source.

## In short: where SAP procures the material from

Source determination is the step in which SAP automatically works out the right source of supply for a material demand — the supplier or the outline agreement it's procured from. To do this, the system evaluates four tools: the **purchasing info record**, the **outline agreement** (contract or scheduling agreement), the **source list** and the **quota arrangement**. Together they answer two questions: *who is allowed to supply?* and *in what proportion?*

## How does the process start?

It all begins with a demand. As soon as a material is needed, a **purchase requisition** is created — an internal request that says: “We need X units of material Y by date Z.” A requisition arises in two ways:

- **manually**, by a user, for instance in self-service purchasing
- **automatically**, through material requirements planning (MRP), which calculates the demand from stock, orders and forecasts

Source determination is the step that follows. It settles which source will cover the requisition. Put simply: the **source list** says who is allowed to supply at all, the **quota arrangement** says how it's split, and the **contract** and **info record** provide the conditions.

## The purchasing info record — the link between supplier and material

The **purchasing info record** is the profile of a relationship between one supplier and one material. It records the conditions under which a specific supplier offers a specific material: price, delivery time, minimum order quantity and further purchasing data.

The benefit: when a buyer creates a purchase order, SAP pulls this data automatically from the info record. The price doesn't have to be typed in each time, and it stays traceable what applied in the past. The info record is therefore often the foundation the other tools build on.

## What is an outline agreement?

An **outline agreement** is a longer-term arrangement with a supplier over fixed conditions, so that each individual delivery isn't negotiated anew. SAP knows two forms: the contract and the scheduling agreement.

### The contract

A **contract** agrees, over a longer period — typically one to five years — a total quantity or a total value with a supplier, but no concrete delivery dates yet. The individual deliveries are created later as **release orders**, that is, purchase orders that reference the contract.

Like every purchasing document, a contract consists of a **header** (supplier, validity period, agreement type, header conditions) and **items** (material, total quantity, price). Two agreement types are worth distinguishing:

- **Quantity contract** — the **total quantity** is fixed. Example: 10,000 units of a material at a fixed unit price, valid over two years. The contract counts as fulfilled once the 10,000 units have been called off.
- **Value contract** — the **total value** is fixed. Example: a total volume of 120,000 euros, freely distributable across several materials. It's fulfilled once that value is reached.

Which form fits depends on the business situation: a fixed quantity argues for a quantity contract, a flexible budget across several materials for a value contract.

Every contract keeps a record of its call-offs automatically — number, order date, quantity called off, order value. So it's visible at any time how much has already been used up.

### The scheduling agreement

A **scheduling agreement** is more tightly timed than the contract. Here you agree not only the total quantity but directly the concrete delivery dates and quantities, in so-called **schedule lines**. This is typical for just-in-time procurement, for instance in the automotive industry or series production. One advantage: you need no separate purchase orders, because the scheduling agreement itself is the supply document.

## The source list — who may supply, and when?

The **source list** is the central steering tool. It defines, per material and plant, which sources of supply are **allowed, preferred or blocked** at a given time. On every automatic source determination — in purchasing as in planning — the system looks here first.

### The fields in the source list

Per entry you maintain, among other things:

- **Validity** — the from-to period in which the source is allowed
- **Source of supply** — for example a specific contract or a supplier's info record
- **Fixed** — the flag for the preferred source in a period. A fixed entry is chosen first during automatic determination.
- **Blocked** — the source may not be used in this period
- **MRP relevance** — its use in requirements planning. Only entries flagged this way are drawn on by MRP.

### Source-list requirement

You can set the **source-list requirement** per material — or across the board per plant. It means: the material may only be procured through the sources entered in the source list. If a purchase order is attempted without a valid source-list entry, the system reports that no allowed source of supply exists. This is a frequent pitfall — usually a source-list requirement without a matching entry is behind it.

### How the source list is maintained

There are three ways to fill the source list:

- **manually**, per material and plant, entry by entry
- **adopted from an outline agreement or info record**, directly when creating or changing the source
- **generated automatically** — the system enters all existing sources of supply for a material in one step, with a preview function for simulating

## The quota arrangement — when several suppliers should deliver

In practice you often want a material **not** just from a single supplier, even when that one offers the best price. Typical reasons:

- **Security of supply** — if one supplier drops out, the other takes over
- **Bargaining power** — two parallel sources keep price pressure alive
- **Capacity limits** — one supplier alone can't cover the whole demand
- **Spreading risk** — several countries or sites reduce concentration risk

The **quota arrangement** is the tool for this. It splits demand **by percentage across several sources of supply**.

### A simple example

A material should be procured **60 percent from supplier A** and **40 percent from supplier B**. You create a quota arrangement with two entries and maintain the quotas in a ratio of **3 to 2** (which equals 60 to 40). On every new demand, the system automatically picks the source that is next in line according to the agreed split.

### How SAP decides: the quota rating

For the split to work out, the system calculates a **quota rating** per source of supply:

> Quota rating = (quantity procured so far + quota base quantity) ÷ quota

On every new order, the source with the **lowest rating** wins. That way the actual distribution settles over time onto the agreed quota. The **quota base quantity** lets you set a starting value — for instance to deliberately give one supplier a head start and shift the ratio.

### Quota usage in the material master

For the quota arrangement to take effect at all, the **quota usage** must be maintained in the material master (the *Purchasing* view). It controls in which operations the quota applies — for example in the purchase requisition, the purchase order, requirements planning, the delivery of a scheduling agreement or the production order. The values can be combined, so a quota can apply in planning and in a manual requisition at the same time.

There is also a **minimum lot size** per quota entry: if a single demand falls below it, the whole amount goes to the next quota. This avoids tiny orders that aren't worth it.

### Two common misunderstandings

- **“The quota arrangement works automatically.”** Only when the quota usage is maintained in the material master *and* a valid quota arrangement exists. Without both, it has no effect.
- **The quota replaces the source list.** It doesn't. The source list says who is allowed to supply at all — the quota only distributes among those already permitted.

## Purchase requisition and source determination in play

Source determination typically runs when a purchase requisition is created. For buyers there's an enhanced entry screen where all the data sits on one central page: header data for the whole document, an item overview with material, quantity, delivery date and plant, and an item detail for additional information. A checkbox activates automatic source determination directly as the item is created.

### Single or multiple account assignment

If a material is requested directly for an account assignment object — say a cost center — you specify an **account assignment category**:

- **Single account assignment** — the costs go entirely to one object, such as a single cost center.
- **Multiple account assignment** — the costs are distributed across several objects, either by quantity, by value or by percentage.

An example: 90 office chairs, distributed across three cost centers at one third each, gives 30 chairs per center. Raise the total quantity to 120 and the system adjusts the percentage split automatically — 40 chairs per center. That automatic adjustment only kicks in, though, when percentage distribution is actively chosen in the account assignment category; otherwise the quantities have to be maintained by hand.

### Processing status and document flow

The **processing status** of a requisition item shows at any time how far the procurement process has come — for instance *not ordered*, *ordered*, *RFQ created* or *converted into an outline agreement*. Through the document flow you can track the follow-on documents — purchase order, goods receipt, invoice — straight from the requisition.

## What users notice in daily work

Source determination isn't configured every day. The underlying master data — info records, contracts, source list, quota arrangement — is usually maintained once, or when agreements change. In the daily flow, though, buyers and planners constantly move within this logic:

- A **demand arises** — through self-service or requirements planning
- **Source determination runs** — automatically or activated on creation
- The **system picks the source** — is the source list allowing it? Is a quota active? Is there a contract? An info record as fallback?
- The **requisition becomes a purchase order** — converted manually or automatically
- **Goods receipt and invoice** are tracked via the status

In the MRP run, the same happens automatically for all materials under planning: the system checks the source list and the quota, picks the fixed or MRP-relevant source, and creates a requisition — assigned to the matching contract or info record.

## In a nutshell

Source determination answers the question of where a material comes from — and it does so largely automatically. Four tools mesh together: the **purchasing info record** supplies the conditions of a supplier-material relationship, the **outline agreement** (contract or scheduling agreement) brings longer-term arrangements into play, the **source list** decides who is allowed to supply at all, and the **quota arrangement** splits the demand across several sources. Once you can keep these four roles apart, it quickly becomes clear why SAP proposes that one particular source in a given case.

## Frequently asked questions

### What is source determination in SAP MM?

Source determination is the step in which SAP automatically works out the right source of supply for a material demand — that is, the supplier or the outline agreement the material is procured from. To do this, the system evaluates four tools: the purchasing info record, the outline agreement, the source list and the quota arrangement.

### What is the difference between a contract and a scheduling agreement?

Both are outline agreements. A contract agrees a total quantity or a total value but calls off no fixed dates — deliveries follow later as individual release orders. A scheduling agreement additionally fixes the concrete delivery dates and quantities in schedule lines and serves as the supply document itself.

### What is the source list for?

The source list defines, per material and plant, which sources of supply are allowed, preferred or blocked in a given period. Where source-list requirement is set, a material may only be procured through the sources entered there. It therefore controls who is allowed to supply at all.

### What does the quota arrangement do?

The quota arrangement splits demand by percentage across several permitted sources of supply, for example 60 percent to one supplier and 40 percent to another. It does not replace the source list but complements it: the source list says who may supply, and the quota splits the demand between those permitted.

### Does the quota arrangement work automatically?

No. It only takes effect when two things come together: the quota usage is maintained in the material master, and a valid quota arrangement exists. If either is missing, the quota arrangement is ignored.
