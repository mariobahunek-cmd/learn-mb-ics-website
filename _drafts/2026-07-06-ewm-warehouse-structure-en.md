---
layout: post
lang: en
title: "SAP EWM warehouse structure: warehouse number, storage type, bin explained"
description: "The SAP EWM warehouse structure in plain language: warehouse number, storage type, storage section, storage bin and activity area, explained clearly."
slug: ewm-warehouse-structure
permalink: /blog/en/ewm-warehouse-structure/
translation_key: post-ewm-warehouse-structure
date: 2026-07-08
category: "Warehouse"
keywords: "SAP EWM warehouse structure, SAP EWM warehouse number, SAP EWM storage type, SAP EWM storage section, SAP EWM storage bin, activity area, Extended Warehouse Management"
reading_time: 9
sources:
  - label: "SAP Help Portal — SAP Extended Warehouse Management (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Extended Warehouse Management area — general background on the warehouse structure. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the warehouse structure in SAP EWM?"
    a: "The warehouse structure in SAP EWM is the hierarchical representation of a real warehouse inside the system. It runs from the top down: the warehouse number stands for the whole warehouse, the storage type for an area within it, the storage section for a group of similar bins, and the storage bin for the individual slot. That way the system always knows where a product physically sits."
  - q: "What is the difference between a storage type and a storage section?"
    a: "A storage type is a physical or logical subdivision of the warehouse, such as a high-rack area, a goods-receipt area or a picking area. A storage section sits one level lower and, within a storage type, groups together several storage bins that share similar properties, for example heavy parts or fast movers."
  - q: "How many characters does a warehouse number have in SAP EWM?"
    a: "The warehouse number in SAP EWM is four characters long. In the classic SAP ERP warehouse, the equivalent field is only three characters. When a warehouse is run through EWM, the ERP warehouse number is flagged as EWM-relevant and linked to the four-character EWM warehouse number."
  - q: "When is an activity area mandatory in SAP EWM?"
    a: "An activity area is optional in general and bundles storage bins for a specific task such as putaway, picking or physical inventory. It is only mandatory for physical inventory — for every other activity you may use one, but you don't have to."
  - q: "Does a user have to create the warehouse structure themselves?"
    a: "No. The warehouse structure is set up once when the warehouse is built, or when it is extended, through Customizing. In day-to-day work, though, every user moves within that structure: for a goods receipt, a warehouse task, a scan or a physical inventory, you always work along the hierarchy of warehouse number, storage type, storage section and storage bin."
---

From the outside, a warehouse looks like one big room full of shelves. For a system like SAP Extended Warehouse Management to manage every product down to the exact spot, that room has to be broken into clear levels. That is what the warehouse structure does: warehouse number, storage type, storage section and storage bin — a hierarchy that runs from “the whole warehouse” all the way to a single slot. This article explains those levels in plain language, with practical examples.

## In short: the map of your warehouse

The warehouse structure in SAP EWM is the hierarchical representation of a real warehouse inside the system. It runs from the top down: the **warehouse number** stands for the whole warehouse, the **storage type** for an area within it, the **storage section** for a group of similar bins, and the **storage bin** for the individual slot. That way the system always knows where a product physically sits — and can tell you where it should go on putaway and where to fetch it on picking.

SAP EWM stands for **Extended Warehouse Management**. It is the software many companies use to run their large, complex warehouses — from the arrival at the door to the shipment out.

## SAP EWM versus the classic SAP WM — the difference up front

If you come from older SAP systems, you may still know **SAP WM (Warehouse Management)**. EWM is not simply an evolution of it, but a product in its own right with its own architecture. They do share one thing: both use a **warehouse number** as the top-level organizational unit.

One visible difference is in the detail. In the classic SAP ERP warehouse, the field for the warehouse number is **three characters** long; in SAP EWM it is **four characters**. When a warehouse is run through EWM, there is no need to build a separate substructure for it in ERP. Instead, the ERP warehouse number is flagged as EWM-relevant and linked to the four-character EWM warehouse number.

## How do ERP and EWM fit together?

Before we step into the EWM-internal levels, it helps to look at the handover from the surrounding ERP system into EWM. Simplified, the chain looks like this:

- **Plant** (in ERP) — the location where goods are produced or stored
- **Storage location** (in ERP) — an inventory-management unit within the plant
- **Warehouse number** (in ERP, 3 characters) — connects into EWM
- **Warehouse number** (in EWM, 4 characters) — where the EWM structure begins

A **plant** is a location where goods are produced (a manufacturing plant) or stored (a distribution center). It belongs to a company code, an organizational unit in finance. **Storage locations** are assigned to a plant and keep track of stock for inventory management.

A storage location on its own holds no physical substructures. Those come into play only through the **warehouse number**. A warehouse number can stand for a single building or for several buildings that together form one warehouse complex.

## Level 1 — the warehouse number: the whole warehouse

The **warehouse number** is the top level of warehouse organization. Underneath it, Customizing stores the organizational and physical properties of the warehouse building. These include, for example:

- **Weight unit** — the unit in which weights are managed
- **Volume unit** — the unit in which volumes are managed
- **Time unit** — the base unit for time figures

Determination schemas for palletization data and packaging specifications also hang off the warehouse number. In practice, a warehouse number usually corresponds to **one building or one distribution center**. If your storage sites are far apart in different cities, it makes sense to give each complex its own warehouse number.

### The supply chain unit (SCU)

Every warehouse number has a unique **supply chain unit (SCU)** — a physical or organizational unit that carries business attributes in the logistics process. The SCU holds important framing information such as **country, region and time zone**. To display all date and time fields, the system falls back on the time zone of this SCU. In practice, the SCU ensures that times in the warehouse are always shown correctly and in relation to the location.

## Level 2 — the storage type: an area within the warehouse

A **storage type** is a physical or logical subdivision of the warehouse complex. It is characterized by its **storage technique, space requirements, organizational form or function** — in short, by what happens in that area. Technically, the storage type is a **four-character code** defined in Customizing.

Every storage type has a **storage type role** that determines what it is for. A regular storage type stores goods; other roles cover the intermediate stops that goods pass through on their way through the warehouse. The main roles at a glance:

- **Regular storage type** — a physical area where products are actually stored
- **Identification point** — where goods are labeled, identified or checked during putaway
- **Pick point** — where goods are checked, labeled or packed during removal
- **Identification and pick point** — both functions in one place
- **Staging area group** — one or more staging areas in the warehouse
- **Work center** — for tasks such as deconsolidation, inspection, packing or value-added services
- **Doors** — specific physical locations, such as the doors on one side of the warehouse
- **Yard** — a yard area adjoining the warehouse
- **Material flow control** — an area with automated conveyor systems
- **Automated warehouse** — a high-rack warehouse with a storage and retrieval machine
- **Production supply** — an area where goods are staged close to the production line

The key settings for putaway, removal and goods-movement control are defined in the Customizing of the storage type. The storage type is therefore the level at which you decide how an area behaves.

## Level 3 — the storage section: bins with similar properties

A **storage section** is an organizational subdivision within a storage type. It groups together storage bins that share similar properties. The system uses this information during **putaway** to decide where an incoming product should best go.

Which criteria define a storage section is entirely up to you. Typical examples:

- **Heavy parts** — bins built to take high weight
- **Bulky parts** — bins with plenty of room
- **Hazardous materials** — bins with special requirements
- **Fast movers** — items with a high turnover, close to the exit
- **Slow movers** — items that are rarely moved

Storage sections are also needed in staging area groups — that is, in the storage types for goods receipt and goods issue. The storage section is thus the link between the broad area (storage type) and the concrete slot (storage bin).

## Level 4 — the storage bin: the individual slot

The **storage bin** is the smallest spatial unit in the warehouse. It states the exact position where a product sits. When the system tells you to “fetch the goods from bin X”, it means a storage bin.

### What a storage bin carries

A storage bin holds a set of attributes that together describe what it can do and where it is:

- **Assignment** — which warehouse number, storage type and storage section it belongs to
- **Capacities** — maximum weight, maximum volume, total capacity
- **Structural coordinates** — aisle, stack, level
- **Geographic coordinates** — X, Y, Z for distance calculation

### The bin coordinate

Because a bin's position is usually derived from a coordinate system, it is called the **bin coordinate**. It can be up to **18 characters** long. For example, the coordinate `01-02-03` stands for aisle 1, stack 2 and level 3.

One principle matters here: the bin coordinate is **unique within a warehouse**. No bin shares its coordinate with another — otherwise the system would not know where the goods really are.

Creating the coordinates runs through Customizing in two steps:

1. **Define the coordinate structure** — that is, set the “encoding” of the bin: which characters stand for aisle, stack, level and any further components
2. **Create templates** — so that storage bin master data can be generated automatically, instead of creating each bin by hand

For the coordinates, you may use any combination of **letters and numbers**.

### Further properties

Every storage bin belongs to exactly one storage type and can be assigned to a storage section. Beyond that, you can set further properties that matter in day-to-day work:

- **Storage bin type** — describes the relative size or the actual measurements
- **Bin access type** — controls which resources may access the bin
- **RF verification field** — when scanning by radio-frequency (RF) device, the check that the correct bin is approached
- **Geo coordinates** — to calculate routes and distances between bins
- **Fire-containment section** — used in reporting for hazardous materials

## The activity area: bundling bins for one task

Alongside the pure spatial hierarchy, there is a second ordering that cuts across it: the **activity area**. Warehouse activities such as putaway, picking and physical inventory are organized in these areas. An activity area consists of one or more assigned storage bins.

What makes it special:

- A storage bin can, depending on the task, be assigned to **several activity areas**
- For sorting, attributes of the bin such as aisle, stack or level serve as criteria — producing a sensible walking order
- Activity areas are **optional in general** — with one exception

That exception is **physical inventory**: there, the activity area is mandatory. For every other activity you may use one, but you don't have to.

## What does a complete warehouse structure look like?

To illustrate, here is an illustrative example — a warehouse with the number `1010` and several storage types that together map the path of goods through the warehouse:

| Storage type | Function | Example sections |
| --- | --- | --- |
| `0010` high-rack | storage | fast movers, slow movers |
| `9010` staging inbound | goods-receipt zone | inbound (GR zone) |
| `8010` deconsolidation | breaking down deliveries | deco |
| `0050` fixed bins | fixed slots | total |
| `8020` packing | packing | pack inbound, work |
| `9020` staging outbound | goods-issue zone | outbound 1, outbound 2 |
| `9050` yard | adjoining yard | inspection, doors |

That is how goods travel from arrival (inbound zone) through storage (high-rack) to shipment (outbound zone) — and every stop is a storage type with its sections and bins.

## What users deal with day to day

The individual warehouse worker does not create the warehouse structure each day. It is set up once when the warehouse is built, or when it is extended, through Customizing. But in day-to-day work, **every user constantly moves within that structure**. Concretely, for example, when you:

- **post a goods receipt** — you choose the target warehouse number, and the system proposes the fitting storage bin based on the storage type and storage section
- **process a warehouse task** — it tells you “from bin A to bin B”
- **run a scan** — you confirm the bin coordinate by RF device
- **carry out a physical inventory** — it is organized by activity areas

In all these cases you move along the chain **warehouse number → storage type → storage section → storage bin**. Once you can keep these four levels apart, you suddenly understand a large part of what happens in the warehouse.

## In a nutshell

The warehouse structure in SAP EWM translates a real warehouse into four clear levels: the **warehouse number** is the whole warehouse, the **storage type** an area within it, the **storage section** a group of similar bins, and the **storage bin** the individual slot with its unique coordinate. Cutting across them, the **activity area** bundles bins for a specific task — mandatory only for physical inventory. Once you know these building blocks, you read every warehouse task, every scan and every putaway like a map.

## Frequently asked questions

### What is the warehouse structure in SAP EWM?

The warehouse structure in SAP EWM is the hierarchical representation of a real warehouse inside the system. It runs from the top down: the warehouse number stands for the whole warehouse, the storage type for an area within it, the storage section for a group of similar bins, and the storage bin for the individual slot. That way the system always knows where a product physically sits.

### What is the difference between a storage type and a storage section?

A storage type is a physical or logical subdivision of the warehouse, such as a high-rack area, a goods-receipt area or a picking area. A storage section sits one level lower and, within a storage type, groups together several storage bins that share similar properties, for example heavy parts or fast movers.

### How many characters does a warehouse number have in SAP EWM?

The warehouse number in SAP EWM is four characters long. In the classic SAP ERP warehouse, the equivalent field is only three characters. When a warehouse is run through EWM, the ERP warehouse number is flagged as EWM-relevant and linked to the four-character EWM warehouse number.

### When is an activity area mandatory in SAP EWM?

An activity area is optional in general and bundles storage bins for a specific task such as putaway, picking or physical inventory. It is only mandatory for physical inventory — for every other activity you may use one, but you don't have to.

### Does a user have to create the warehouse structure themselves?

No. The warehouse structure is set up once when the warehouse is built, or when it is extended, through Customizing. In day-to-day work, though, every user moves within that structure: for a goods receipt, a warehouse task, a scan or a physical inventory, you always work along the hierarchy of warehouse number, storage type, storage section and storage bin.
