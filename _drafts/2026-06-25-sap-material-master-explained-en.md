---
layout: post
lang: en
title: "The SAP material master explained: views, material type and organisational levels"
description: "What material master data is in SAP, how it is organised into views, and what role material type, plant and storage location play — explained in plain language for users."
slug: sap-material-master-explained
permalink: /blog/en/sap-material-master-explained/
translation_key: post-material-master
date: 2026-07-07
category: "Master Data"
keywords: "material master, master data, SAP MM, views, material type, plant, storage location, SAP S/4HANA, material number"
reading_time: 8
sources:
  - label: "SAP Help Portal — Material Master (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Materials Management area — general background on the material master; always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between master data and transactional data?"
    a: "Master data is permanently maintained, foundational information such as the material master, which processes refer back to again and again. Transactional data is individual events such as orders, deliveries or invoices that build on top of that master data."
  - q: "Why is the material master split into views?"
    a: "Because different departments need different information about the same material. Each view bundles exactly the fields of one area, so purchasing, sales, warehousing and accounting each maintain only what is relevant to them."
  - q: "Can the same material be different in two plants?"
    a: "Yes. Much of the data is plant-specific, such as valuation or planning. The same material number can therefore be valuated or planned differently in plant A than in plant B, even though it is the same material in business terms."
  - q: "Why can't a material be used in a certain process?"
    a: "Often a view is missing. Without the purchasing view you cannot order the material; without the accounting view you cannot post value movements. If a view is missing for a given plant, SAP reports the material as not created there."
---

Anyone working with SAP runs into one term sooner or later that shows up almost everywhere: **material master data**. It is at the heart of nearly every logistics and commercial process in the system. Whether it is purchasing, sales, the warehouse or accounting — without clean material master data, very little runs smoothly in SAP. This article explains, in plain language, what's behind it.

## In short: the central data object for every material

Material master data describes everything a company buys, stores, produces or sells — raw materials, semi-finished goods, finished products, trading goods or services. Each of these materials gets its own **material master record** in the system, with a unique **material number**.

This material number is **unique across the whole client**: it exists only once in the entire system and therefore stands for exactly one specific material. When you create a purchase order, put goods into stock or capture a sales order, SAP always refers back to this material master. If the data there is wrong or incomplete, the whole process stalls. That's why the rule holds: **master data is the foundation for all logistics processes.**

## Master data versus transactional data

SAP distinguishes two broad types of data:

- **Transactional data** is individual events — purchase orders, deliveries, invoices. It is created continuously in day-to-day business.
- **Master data** is the permanently maintained, central information those events refer to.

The material master belongs to master data. It is created cleanly once and then used again and again. That's exactly why it pays to understand it: an error in the master record ripples out into many downstream transactions.

## Structured in views: different data per area

Because the material master is used by many areas, it isn't organised as one single block of data but as **views**. A view contains exactly the data a particular department needs for its work.

This has a clear advantage: each area maintains only what is relevant to it. Purchasing cares about sources of supply and order handling, sales about selling data and delivery terms, accounting about valuation. This separation keeps things clear and responsibilities well defined.

The most important views at a glance:

### Basic data

Basic data is the foundation of every material master. It applies **to the entire company** and holds general information such as the material description, base unit of measure (piece, kilogram, litre and so on), material group, and weights and dimensions. This view must **always** be created — without basic data, the material doesn't exist.

### Purchasing

The purchasing view holds everything relevant to procurement: purchasing group, order unit of measure, goods receipt processing time and control data for purchase orders. Only with this view can the material be ordered at all.

### Sales

The sales views (often split across several sub-areas) contain selling data, shipping conditions, tax classification and the link to plant and sales area. Only then can the material be used in a sales order.

### Storage

The storage views describe how and where the material is stored — storage conditions, temperature requirements, shelf-life data or hazardous-material indicators. They are mainly maintained when the material has special storage requirements.

### Accounting

The accounting view is the bridge to the finance world. It holds the valuation class, the price control (standard price or moving average price) and the current material price. Without this view SAP cannot post any value movements for the material — no inventory valuation, no goods receipt posting and no invoice verification.

### Planning

The planning views control how demand for the material is determined and covered: MRP type, lot-sizing procedure, safety stock, reorder point and planned delivery time. They are the basis for automatic requirements planning — the same logic from which a [purchase requisition](/blog/en/what-is-a-purchase-requisition/) can be created automatically.

## Material type and industry sector: the switches

Before you can even create a material master, you set two central fields: the **material type** and the **industry sector**.

### The material type

The material type determines the fundamental properties of a material. Among other things, it controls which views may be created at all, how the material number is assigned (internally or externally), how the material is valuated and which movement types are allowed.

Typical standard material types include, for example, raw materials (bought, not sold), semi-finished goods (produced internally, not sold directly), finished products (produced internally and sold), as well as trading goods and services. In customising, companies can also define their own material types. Choosing the material type is a decision with weight, because it predetermines many other properties.

### The industry sector

The industry sector field influences which views and fields the material master offers. An “engineering” sector shows different fields than “pharmaceuticals” or “food”, for example. Importantly, the sector is set when the material is first created and **cannot be changed** afterwards. Overlook that and you may face a tedious re-creation.

## How a material master is created

Creating a material follows a fixed logic in SAP. Simplified, it goes like this:

1. **Set the material number and sector.** Unless internal number assignment applies, you enter a unique material number and choose the sector and material type.
2. **Select the views.** SAP shows a list of all available views. You pick exactly the ones you need for your process — for example basic data, purchasing, storage and accounting. Tip: create only the views you actually need; you can add more at any time.
3. **Maintain the organisational levels.** SAP asks for the relevant levels such as plant, storage location or sales area.
4. **Enter the data.** Now you fill in the mandatory fields in each view — material text, unit of measure, valuation class, price control and so on.
5. **Save.** SAP confirms the creation. From now on, the material can be used in the corresponding processes.

Whether you use the classic SAP GUI or a modern Fiori app makes no difference to the result — both write to the same data.

## Organisational levels: client, plant, storage location

Material master data isn't only “global”. Much of the data is tied to **organisational levels** — that is, to the places in the company where the material is actually used.

### Client level

At **client level** sits data that applies to all plants and warehouses: material number, material description, material group, base unit of measure. This data is maintained once and then applies company-wide.

### Plant level

The **plant** is the central organisational unit in logistics — a production site, distribution centre or storage location. At plant level you maintain, for example, inventory management and planning data, the material valuation, the goods receipt processing time and the purchasing group. As a result, the same material can be valuated or planned differently in two plants.

### Storage location level

Within a plant there are one or more **storage locations**. At this level, storage-related data is maintained. When you post stock, it always happens on the combination of plant plus storage location.

This logic is decisive: whenever you create and maintain data, it always matters **for which organisational unit** you are entering it.

## Common pitfalls

- **Confusing views.** Valuation data lives in the accounting view, not in basic data. Look for it in the wrong place and you won't find it.
- **Mixing up plant and client data.** Basic data applies across the client, while many other views are plant-specific. When in doubt, it's worth checking which level a field sits on.
- **Wanting to change the sector later.** The sector is fixed after creation. So it needs to be right from the start.
- **Creating views incompletely.** If the purchasing or accounting view is missing, the material can't be used in that process — SAP then reports it as not created for the plant.
- **Treating the material number as not unique.** It is unique across the client and cannot be assigned twice — not even in different plants.

## In a nutshell

Material master data is the central data object for every material in SAP and the foundation for purchasing, sales, warehousing, planning and accounting. Once you understand how the material master is built from **views**, what role **material type** and **industry sector** play, and how the **organisational levels** client, plant and storage location fit together, you've grasped a large part of the logic that holds the system together. Master data isn't tedious overhead — it's the reason SAP runs smoothly day to day.

## Frequently asked questions

### What is the difference between master data and transactional data?

Master data is permanently maintained, foundational information such as the material master, which processes refer back to again and again. Transactional data is individual events such as orders, deliveries or invoices that build on top of that master data.

### Why is the material master split into views?

Because different departments need different information about the same material. Each view bundles exactly the fields of one area, so purchasing, sales, warehousing and accounting each maintain only what is relevant to them.

### Can the same material be different in two plants?

Yes. Much of the data is plant-specific, such as valuation or planning. The same material number can therefore be valuated or planned differently in plant A than in plant B, even though it is the same material in business terms.

### Why can't a material be used in a certain process?

Often a view is missing. Without the purchasing view you cannot order the material; without the accounting view you cannot post value movements. If a view is missing for a given plant, SAP reports the material as not created there.
