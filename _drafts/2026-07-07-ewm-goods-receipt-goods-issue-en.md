---
layout: post
lang: en
title: "Goods receipt and goods issue in SAP EWM explained"
description: "How goods enter and leave a warehouse in SAP EWM: inbound delivery, putaway, picking, packing and goods issue — walked through step by step from a user's point of view."
slug: ewm-goods-receipt-goods-issue
permalink: /blog/en/ewm-goods-receipt-goods-issue/
translation_key: post-ewm-wareneingang-warenausgang
date: 2026-07-07
category: "Warehouse"
keywords: "SAP EWM, goods receipt, goods issue, Extended Warehouse Management, putaway, picking, warehouse task, warehouse order, inbound delivery"
reading_time: 8
sources:
  - label: "SAP Help Portal — Extended Warehouse Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Extended Warehouse Management area — general background on goods receipt and goods issue. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between a warehouse task and a warehouse order?"
    a: "A warehouse task is a single movement instruction — for example, move product X from bin A to bin B. A warehouse order bundles one or more warehouse tasks into a work package that one employee processes in one go. In short: warehouse task = what to do, warehouse order = which work package."
  - q: "Where is the purchase order created — in ERP or in EWM?"
    a: "The purchase order is created in the ERP system, not in SAP EWM. EWM only takes over once the order becomes an inbound delivery that is passed on to the warehouse."
  - q: "What does confirming a warehouse task mean?"
    a: "By confirming, the warehouse worker acknowledges that the movement was actually carried out — correct product, correct quantity, correct bin. Only after confirmation does the system treat the task as done."
  - q: "Why does a goods receipt sometimes seem to get stuck?"
    a: "Often the related warehouse task has not been confirmed yet, or the goods are still in the goods receipt area and have not been put away to their final bin. Until putaway is complete, the stock counts as not yet fully available."
  - q: "What is a quant in SAP EWM?"
    a: "A quant is the stock of a particular product in a specific storage bin. It is the finest unit EWM uses to track what is where and in what quantity."
---

At its core, every warehouse does the same thing: goods come in, get stored away, are later retrieved, packed and leave again. In SAP Extended Warehouse Management (EWM) these two directions are called **goods receipt** and **goods issue**. Once you understand them as a single connected story, you understand almost the entire day-to-day operation of an EWM warehouse. This article walks through both processes step by step — purely from a user's perspective, without any configuration.

## In short: into the warehouse, out of the warehouse

Goods receipt and goods issue follow the same underlying logic in SAP EWM. It all starts with a **triggering document** from the ERP system — a purchase order for goods receipt, a sales order for goods issue. From that a **warehouse document in EWM** is created (the inbound delivery or the outbound delivery order), and this drives the **physical movement in the warehouse** through warehouse tasks and warehouse orders.

The only difference is the direction:

- **Goods receipt:** movement *into* the warehouse. It starts in the goods receipt area and ends at a storage bin.
- **Goods issue:** movement *out of* the warehouse. It starts at the storage bin and ends in the goods issue area (the staging zone).

Both use the same tools: an inbound delivery or an outbound delivery order, warehouse tasks, warehouse orders and confirmation. Once you understand these terms, you have both directions covered.

## Goods receipt: purchase order, inbound delivery, putaway

The goods receipt process does not begin in EWM but in the **ERP system, with a purchase order**. As soon as the supplier announces the shipment (for example via a shipping notification), an **inbound delivery** is created in ERP.

This ERP inbound delivery is handed over to SAP EWM and becomes the **inbound delivery in EWM** — the actual execution document the warehouse works with. Simplified, the chain looks like this:

1. **Purchase order** in the ERP system
2. **Inbound delivery** in the ERP system (created manually or automatically from the shipping notification)
3. **Inbound delivery notification** in EWM — an intermediate document that newer, embedded EWM variants can skip
4. **Inbound delivery in EWM** — the document the warehouse work hangs on

An important point for understanding: changes made to the EWM inbound delivery are **reported back to ERP**. Once warehouse execution is complete, the document forms the basis for the goods receipt posting in ERP. That keeps the warehouse and ERP inventory in sync.

### Two storage locations in goods receipt

A common pattern: SAP EWM can represent goods receipt across **two storage locations**. As long as the stock is still in the putaway process, it belongs to a goods receipt location. Only once the goods have reached their final bin is the stock moved to the location "available".

The benefit: ERP inventory management already sees the stock, but it stays visible that from a warehouse perspective it is *not yet fully available*. That prevents goods still sitting at the door from being promised elsewhere.

## Where do the goods go? Putaway

Once the inbound delivery exists in EWM, the system has to decide **which storage bin** the goods go to. This is **putaway**.

To do this, the inbound delivery generates a **warehouse task for putaway**. This warehouse task contains the **destination** — storage type, storage section and storage bin. Which bin is proposed is driven by stored rules that take into account, among other things:

- properties of the product (for example batch, serial number or hazardous material)
- the type of packaging (packed or unpacked)
- the activity area in the warehouse

As a user you do not maintain these rules yourself. What matters is the principle: the inbound delivery produces a warehouse task, and that task tells the worker exactly where the goods should go.

## Goods issue: order, picking, packing, shipping

The goods issue process typically starts with a **sales order** in the ERP system (a stock transfer is also possible). The sales order becomes an **outbound delivery** in ERP, and as soon as that concerns an EWM-managed warehouse, it is passed on to EWM:

1. **Sales order** in ERP
2. **Outbound delivery** in ERP
3. **Outbound delivery request** in EWM (intermediate document)
4. **Outbound delivery order** in EWM — the central document for goods issue
5. **Outbound delivery in EWM** at the end, after the goods issue posting

When the outbound delivery order is created, a fair amount happens in the background: among other things, the system determines the storage bin to pick from as well as the door and staging zone. After that, the actual warehouse work can begin.

### Picking

During **picking**, the goods are retrieved from the storage bin and brought to the goods issue area. Here too a **warehouse task** drives the movement — this time for picking. It contains the **source** (storage type and bin) and the **destination** (the staging zone).

For the worker this is a clear work item: "Fetch product X in quantity Y from bin Z and bring it to the staging zone." Once carried out, the task is confirmed.

### Packing

**Packing** can happen at different stages. SAP EWM can work with **packaging specifications** that define how a product is packed — for example how many units go on a pallet. The packed units are tracked as **handling units (HUs)**, so it stays traceable what is inside each package at any time.

### Posting goods issue

Once the goods have been picked and sit in the staging zone, the **goods issue posting** follows. The EWM outbound delivery reports it back to the ERP system, where the matching inventory and financial documents are created automatically. With that, the goods have left the warehouse — physically and in the system.

## Warehouse task versus warehouse order — what's the difference?

These two terms are the ones people mix up most, yet the difference is simple.

### Warehouse task

The warehouse task is **the single movement instruction**. It tells the warehouse worker exactly what to do, for example: "Move three pallets of product Y to bin ABC." Warehouse tasks are needed for, among other things:

- picking
- putaway
- internal movements and stock transfers
- goods receipt and goods issue postings

Once the task has been carried out, it has to be **confirmed**. With confirmation the worker acknowledges: correct product, correct quantity, correct bin.

### Warehouse order

The warehouse order is the next level up: **a work package** that one worker processes within a certain time frame. It contains **one or more warehouse tasks**. So several individual warehouse tasks are bundled into one or more warehouse orders — following rules defined in the background.

As a memory aid: **warehouse task = what to do, warehouse order = which work package.**

## The warehouse structure: warehouse number, storage type, storage bin

To make goods receipt and goods issue work, it helps to look at the structure of an EWM warehouse. It is clearly hierarchical:

- **Warehouse number:** the top organisational unit, in practice usually a building or a distribution centre.
- **Storage type:** a physical or logical subdivision — for example high-rack storage, a goods receipt zone, a goods issue zone or a packing area.
- **Storage section:** a finer subdivision within a storage type (such as "fast movers" versus "slow movers").
- **Storage bin:** the **smallest spatial unit** of the warehouse. This is where the actual stock ends up.

The stock of a product in a storage bin is called a **quant**. It is the unit EWM uses to track what is where and in what quantity.

## Common pitfalls

- **Confusing warehouse task and warehouse order.** The warehouse task is the single instruction; the warehouse order is the larger work package that bundles several tasks.
- **Equating the inbound delivery notification with the inbound delivery.** The notification is the intermediate document in EWM; the inbound delivery in EWM is the actual execution document the work is based on.
- **Forgetting to confirm.** A movement that has been carried out is only done in the system once it has been confirmed.
- **Looking for the purchase order in the wrong system.** The purchase order is created in ERP, not in EWM. EWM only starts at the inbound delivery.
- **Treating ERP and EWM master data as identical.** There is a transfer between the two, but the data models are not the same — the warehouse view in EWM stands on its own.

## In a nutshell

Goods receipt and goods issue are two directions of the same underlying logic in SAP EWM: a document from the ERP system kicks off the process, EWM turns it into a warehouse document, and that document drives the physical movement through warehouse tasks and warehouse orders — into the warehouse for goods receipt, out of it for goods issue. Once you remember both paths as one continuous story — purchase order, inbound delivery, putaway on one side; order, picking, packing, goods issue on the other — you understand the operational heart of an EWM warehouse.

## Frequently asked questions

### What is the difference between a warehouse task and a warehouse order?

A warehouse task is a single movement instruction — for example, move product X from bin A to bin B. A warehouse order bundles one or more warehouse tasks into a work package that one employee processes in one go. In short: warehouse task = what to do, warehouse order = which work package.

### Where is the purchase order created — in ERP or in EWM?

The purchase order is created in the ERP system, not in SAP EWM. EWM only takes over once the order becomes an inbound delivery that is passed on to the warehouse.

### What does confirming a warehouse task mean?

By confirming, the warehouse worker acknowledges that the movement was actually carried out — correct product, correct quantity, correct bin. Only after confirmation does the system treat the task as done.

### Why does a goods receipt sometimes seem to get stuck?

Often the related warehouse task has not been confirmed yet, or the goods are still in the goods receipt area and have not been put away to their final bin. Until putaway is complete, the stock counts as not yet fully available.

### What is a quant in SAP EWM?

A quant is the stock of a particular product in a specific storage bin. It is the finest unit EWM uses to track what is where and in what quantity.
