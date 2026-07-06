---
layout: post
lang: en
title: "What is a purchase requisition in SAP?"
description: "The purchase requisition is the first step in SAP procurement: an internal request to buy something. What it is, how it's created, and how it turns into a purchase order — explained in plain language."
slug: what-is-a-purchase-requisition
permalink: /blog/en/what-is-a-purchase-requisition/
translation_key: post-purchase-requisition
date: 2026-07-06
category: "Purchasing"
keywords: "purchase requisition, SAP MM, procurement, purchase order, release strategy, end user, Sourcing and Procurement"
reading_time: 6
sources:
  - label: "SAP Help Portal — Sourcing and Procurement (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Materials Management / Sourcing and Procurement — general background on the purchase requisition. Always check the current state in the Help Portal before relying on it in production."
---

When a company needs to buy something — material, spare parts, a service — the journey in SAP almost always starts in the same place: with a **purchase requisition**. It's one of those terms every SAP user in a procurement context hears sooner or later. This article explains, in plain language, what's behind it.

## In short: an internal request to buy something

A purchase requisition is an **internal document**. With it, a department is essentially saying: "We need this material or service — please take care of procuring it." So it points **inward**, to the purchasing team, and not yet outward to a supplier.

That's the most important distinction, and the one people mix up at the start:

- The **purchase requisition** is the internal request ("we'd like to have").
- The **purchase order** is the binding document that goes to the supplier ("we hereby order").

The purchase requisition is therefore the first step in the procurement chain, and not yet a contract with anyone.

## How a purchase requisition is created

There are two typical ways a purchase requisition comes into being in SAP.

**1. Created manually.** Someone in a specialist department — say maintenance or the warehouse — enters the request themselves: what's needed, how much, for which plant and by when. This is the classic case when someone knows concretely that something has to be bought.

**2. Created automatically.** Often SAP creates the purchase requisition itself, without anyone typing it. This typically happens through **material requirements planning (MRP)**: when the stock of a material drops below a defined point, the system recognises the demand and automatically proposes procurement — in the form of a purchase requisition. Other processes, such as a maintenance order, can also trigger a requisition automatically.

In both cases the result is the same: an internal document telling purchasing that something is needed.

## From demand to purchase order

Once the purchase requisition exists, purchasing takes over. Simplified, it goes like this:

1. **Review the request.** Purchasing looks at the open purchase requisitions.
2. **Find a source of supply.** Who should it be bought from? Sometimes this is already stored (for example via an info record or a contract), sometimes purchasing actively selects the supplier.
3. **Convert it into a purchase order.** The purchase requisition is turned into an actual purchase order. Only this order goes to the supplier.

The data from the requisition — material, quantity, plant, date — is carried over into the purchase order. The purchase requisition is kept as a document and linked to the purchase order, so it stays traceable where the demand originally came from.

## The release: why a requisition can "get stuck"

In many companies, not every purchase requisition can become a purchase order right away. Above certain value limits, or for certain material groups, it first has to be **released** — that's an internal approval, often by a manager or the person responsible for the cost centre.

For the user this means: if a requisition "does nothing" and never turns into a purchase order, it's often because the release is still pending. That's not a fault — it's a deliberate control step.

## Who works with it day to day

- **Specialist departments** (warehouse, maintenance, production) trigger demand and create requisitions.
- **Purchasing** converts them into purchase orders and selects suppliers.
- **Approvers** release requisitions above certain limits.

For you as a user, the purchase requisition is often the point where you come into contact with the procurement process — whether because you create one yourself, or because you want to know why a purchase order hasn't gone out yet.

## Common pitfalls

- **Confusing requisition with order.** The requisition is internal; the order goes outward. If you're asking a supplier why "the order" hasn't arrived, first check whether a purchase order even exists yet — or whether it's still stuck at the requisition stage.
- **Overlooking a missing release.** A requisition that hasn't been released won't be processed further. A glance at the release status saves a lot of searching.
- **Incomplete details.** If the delivery date is missing or the quantity is unclear, purchasing can't process the requisition cleanly.

## In a nutshell

The purchase requisition is the **internal starting point** of every procurement in SAP: a request to purchasing to source something. It can be created by hand or automatically, goes through a release when needed, and is finally converted into a purchase order that goes to the supplier. Once you've internalised that one distinction — requesting internally versus ordering externally — you already understand half of what getting started in SAP procurement is about.
