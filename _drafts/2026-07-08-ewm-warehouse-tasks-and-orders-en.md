---
layout: post
lang: en
title: "SAP EWM warehouse tasks and warehouse orders explained"
description: "Warehouse task, warehouse order, warehouse request: how these three SAP EWM documents drive putaway, picking and internal movements, explained clearly."
slug: ewm-warehouse-tasks-and-orders
permalink: /blog/en/ewm-warehouse-tasks-and-orders/
translation_key: post-ewm-warehouse-tasks
date: 2026-07-08
category: "Warehouse"
keywords: "SAP EWM warehouse task, SAP EWM warehouse order, warehouse request, SAP Extended Warehouse Management, putaway, picking, task confirmation, warehouse order creation rules"
reading_time: 9
sources:
  - label: "SAP Help Portal — SAP Extended Warehouse Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Extended Warehouse Management area — general background on warehouse tasks and warehouse orders. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between a warehouse task and a warehouse order?"
    a: "A warehouse task is ONE concrete movement — for example “move pallet X from bin A to bin B”. A warehouse order bundles several warehouse tasks into one work package that a worker completes in a single pass. In short: the warehouse task is the individual instruction, the warehouse order is the grouping of several instructions."
  - q: "What is a warehouse request in SAP EWM?"
    a: "The warehouse request is the source document that triggers a warehouse activity — usually the inbound delivery for goods receipt, or the outbound delivery order for goods issue. The actual warehouse tasks that carry out the physical movement are created on the basis of the warehouse request."
  - q: "What does confirming a warehouse task mean?"
    a: "Confirming means acknowledging completion. Once the warehouse task has been carried out, the worker reports back that the correct product, in the correct quantity, has arrived at the correct destination bin. Only with confirmation is the movement considered complete and the stock updated accordingly."
  - q: "What are warehouse order creation rules used for?"
    a: "Warehouse order creation rules are defined in Customizing and decide which and how many warehouse tasks are combined into a warehouse order. Through filters, limits, sorting and consolidation, they control the workload and the path each worker takes through the warehouse."
---

Anyone getting to grips with SAP Extended Warehouse Management (EWM) trips over two terms early on that look confusingly alike: **warehouse task** and **warehouse order**. They sound almost identical, yet they are two different documents with clearly separated jobs. Once you understand the difference cleanly, most EWM warehouse processes fall into place. This article walks through the hierarchy *warehouse request → warehouse task → warehouse order* step by step.

## In short: three documents drive every movement in the warehouse

In SAP EWM, every physical movement — putaway, picking, internal transfer — is carried by three documents that build on each other. The **warehouse request** is the trigger (an inbound delivery, for example). The **warehouse task** is the concrete instruction to the worker telling them what to do. The **warehouse order** bundles several warehouse tasks into one work package. Keep these three layers apart and the flow of goods through the warehouse becomes clear.

## The big picture: the three-level hierarchy

The interplay of the three documents reads as a clear sequence:

1. **Warehouse request** — the source document, often an inbound delivery (goods receipt) or an outbound delivery order (goods issue)
2. **Warehouse task** — the concrete instruction to the worker about what to physically do
3. **Warehouse order** — the bundling of several warehouse tasks into one work package

A warehouse request enables warehouse activities to be processed. Those activities are carried out through warehouse tasks that refer back to the corresponding warehouse request. In the warehouse management monitor you can display and track every follow-on document of a warehouse request — from the request all the way to the last confirmed movement.

## Step 1 — The warehouse request

A warehouse request is the source document for a warehouse activity. Typical activities that build on it include:

- **Picking**
- **Putaway**
- **Posting changes**
- **Internal transfers within the warehouse**
- **Scrapping**

In the goods receipt process, the warehouse request is the **inbound delivery document**. The two terms are used interchangeably here — every follow-on action in the warehouse refers back to this one document.

### How does the delivery reach EWM?

The delivery does not appear out of nowhere. It starts in the ERP system with a purchase order and travels into EWM through an advance notice:

- **ERP:** purchase order → inbound delivery
- **EWM:** inbound delivery notification → inbound delivery

The ERP inbound delivery is first copied into EWM as an **inbound delivery notification** — a kind of heads-up: “this stock is on its way.” As soon as the goods physically arrive, the notification becomes the real **inbound delivery document** in EWM.

One detail closes the loop: **any change to the inbound delivery document is reported back to the ERP system.** The completed inbound delivery is the basis for the goods receipt posting in ERP. That keeps the warehouse and accounting in sync.

## Step 2 — The warehouse task

Warehouse tasks are used to **carry out goods movements in the warehouse**. A movement can be physical, or it can be a pure stock change in the system.

Warehouse tasks are needed, among other things, for:

- **Picking**
- **Putaway**
- **Internal movements**
- **Posting changes**
- **Goods receipt postings**
- **Goods issue postings**

### What is a warehouse task, concretely?

A warehouse task is a **document that tells the worker about one concrete task** — for example: “move three pallets of product Y to bin ABC.” It is the actual work instruction at the lowest, executable level.

Key characteristics:

- In a putaway or picking process, and for posting changes, the **basis for the warehouse task is the warehouse request**.
- A warehouse task is created per warehouse request item, **manually or automatically** — the automatic creation is handled by the Post Processing Framework (PPF), a control framework for follow-on actions.
- For spontaneous movements in the warehouse (say, one pallet from one bin to another), a warehouse task can be created **even without a reference document**.

### Confirmation — the second step

Once the warehouse task has been carried out, it must be **confirmed**. Confirming means acknowledging: the worker reports back that the correct product, in the correct quantity, has arrived at the correct destination bin. Only then is the movement complete.

Whether a confirmation is required is controlled by settings on the source and destination storage type. In the warehouse process type you can also specify that confirmation happens **automatically the moment the warehouse task is created** — sensible for simple, low-risk movements where no extra human check is needed.

### Product and HU warehouse tasks

There are two kinds of warehouse task, depending on what is being moved:

- **Product warehouse task** — when a product is moved in a single step from the goods receipt area to the final destination bin. It carries the necessary details: warehouse process type, source bin and destination bin.
- **HU warehouse task** — for more complex movements where the goods are, for example, repacked at a packing station before they reach the destination. “HU” stands for handling unit, meaning a packed unit such as a pallet or box. The HU warehouse task holds the same fields as the product warehouse task but is used for packed goods and multi-step movements.

## Step 3 — The warehouse order

Now comes the term that is so often confused with the warehouse task.

Several warehouse tasks are **combined into one warehouse order**. The warehouse order is a **work package** that a worker processes within a certain period. It contains one or more warehouse tasks or physical inventory items.

Put differently: the **warehouse task** is ONE concrete movement (“move pallet X from bin A to bin B”). The **warehouse order** bundles SEVERAL warehouse tasks into a sensible sequence of work for one worker (“move these five pallets in one go”). The bundling exists to **manage the workload of the warehouse resources**.

### Why does the bundling matter?

Warehouse tasks are created continuously — whenever products come in or go out, are moved or counted. Without bundling, a worker would have to process them one by one, in no particular order. So SAP EWM combines several warehouse tasks into warehouse orders, following defined rules.

A vivid example: with a large inbound delivery of 50 pallets, a single worker would otherwise face 50 loose warehouse tasks. With the warehouse order, SAP EWM bundles, say, **ten pallets into one warehouse order**, so the worker gets a sensible, manageable unit of work and moves efficiently through the warehouse.

## Warehouse order creation rules

How SAP EWM decides which warehouse tasks get bundled is governed by the **warehouse order creation rules**. They are defined in Customizing — the system configuration a consultant sets up.

Warehouse orders are created in four steps:

1. Warehouse tasks are grouped by **activity area** and sorted using predefined rules. An activity area combines several storage bins into one work zone.
2. One or more creation rules are defined per activity area.
3. The rules are worked through in turn until every warehouse task is assigned to a warehouse order. Filters and limits take effect depending on the configuration.
4. If no rule fits, a **standard rule provided by SAP** applies, so that no warehouse task is left over.

### Three central controls

- **Filters and limits** — determine which and how many warehouse tasks are grouped into one warehouse order.
- **Sorting rules** — once a creation rule is applied, the warehouse tasks are ordered by the sorting rule. Typical criteria are aisle, stack and level of the bin — so the worker takes a sensible route instead of crisscrossing the warehouse.
- **Consolidation groups** — define which warehouse tasks may be packed or processed together.

### Subsequent and standard rules

To be processed, a warehouse task must be **assigned to a warehouse order**. If tasks remain after all defined rules have run, two safety nets step in:

- **Subsequent rules** — create warehouse orders for the remaining tasks, grouped per activity area, queue and consolidation group.
- **Standard rules** — group per activity area, queue and delivery. They apply when no creation rule was defined for an activity area at all.

## An example: the goods receipt process from start to finish

Here is how all three documents work together in a complete goods receipt workflow:

1. **ERP:** Purchasing creates a purchase order.
2. **ERP:** The supplier announces the shipment → ERP creates an inbound delivery.
3. **EWM:** The ERP inbound delivery is copied into EWM as an **inbound delivery notification**.
4. **EWM:** On physical goods receipt, the EWM **inbound delivery document** (the warehouse request) is created.
5. **EWM:** SAP EWM automatically creates a **warehouse task** for putaway — from the goods receipt area at the door to the final destination bin.
6. **EWM:** Several warehouse tasks are bundled into one **warehouse order** according to the creation rules.
7. **Warehouse worker:** processes the warehouse order, carries out the individual warehouse tasks and **confirms** them once done.
8. **EWM:** The goods receipt posting is triggered — the stock moves from the goods receipt area into the freely available area.
9. **ERP:** The posting is reported back to ERP, where stock and accounting are updated.

The reason for the two areas: while stock is still in the putaway process, it counts as “in goods receipt” and is not freely available. Only at the final destination bin is it treated as available. This lets inventory management tell at once whether a quantity is ready to sell or still on its way in.

## Why a shipping notification can force the goods receipt

When the purchase order is created, you specify whether a **shipping notification** — a delivery announcement — is expected from the supplier. This is done with a **confirmation control key** at item level. It can also be predefined in shipping Customizing, in the purchasing info record or in the supplier master data.

The practical consequence: **if this key is set, an inbound delivery must be created first before the goods receipt can be posted.** Without an inbound delivery, the system will not allow a goods receipt — a common source of error in practice, when a goods receipt seems to be blocked for no reason.

## What users actually do day to day

As a warehouse worker, your day-to-day revolves mostly around the **warehouse order** — your work package for the next hour. The typical flow at a mobile scanner:

- **Log on to the device** — a warehouse order is assigned to you.
- **The first warehouse task** appears: “fetch pallet X from the source area, take it to the destination area.”
- **Confirm** — verify product, quantity and bin.
- **The next warehouse task** in the same warehouse order → until the order is complete.

As a planner or warehouse manager, you work more with the **warehouse order creation rules** — that's configuration work, not day-to-day operations. But understanding the logic behind the rules helps you spot uneven workload or bottlenecks in the warehouse and steer against them deliberately.

## In a nutshell

Three documents carry every movement in SAP EWM: the **warehouse request** triggers an activity, the **warehouse task** is the individual, executable instruction, and the **warehouse order** bundles several warehouse tasks into one work package. Confirmation closes out each movement, and the warehouse order creation rules control how cleverly the work is bundled. Keep request, task and order cleanly apart, and the flow of goods through the warehouse makes sense — from the door to the shelf.

## Frequently asked questions

### What is the difference between a warehouse task and a warehouse order?

A warehouse task is ONE concrete movement — for example “move pallet X from bin A to bin B”. A warehouse order bundles several warehouse tasks into one work package that a worker completes in a single pass. In short: the warehouse task is the individual instruction, the warehouse order is the grouping of several instructions.

### What is a warehouse request in SAP EWM?

The warehouse request is the source document that triggers a warehouse activity — usually the inbound delivery for goods receipt, or the outbound delivery order for goods issue. The actual warehouse tasks that carry out the physical movement are created on the basis of the warehouse request.

### What does confirming a warehouse task mean?

Confirming means acknowledging completion. Once the warehouse task has been carried out, the worker reports back that the correct product, in the correct quantity, has arrived at the correct destination bin. Only with confirmation is the movement considered complete and the stock updated accordingly.

### What are warehouse order creation rules used for?

Warehouse order creation rules are defined in Customizing and decide which and how many warehouse tasks are combined into a warehouse order. Through filters, limits, sorting and consolidation, they control the workload and the path each worker takes through the warehouse.
