---
layout: post
lang: en
title: "Customer master data in SAP S/4HANA — understanding the three data levels"
description: "Customer master data is the foundation of every sales process in SAP. How the business partner concept works, what the three data levels are, and why partner functions matter."
slug: customer-master-data-in-sap
permalink: /blog/en/customer-master-data-in-sap/
translation_key: post-kundenstammdaten
date: 2026-07-07
category: "Master Data"
keywords: "SAP customer master data, business partner, sales area data, company code data, partner functions, SAP S/4HANA Sales, master data maintenance"
reading_time: 8
sources:
  - label: "SAP Help Portal — Sales (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Sales / Business Partner area — general background on customer master data and the business partner concept. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between a business partner and a customer in SAP?"
    a: "The business partner is the overarching master data object in SAP S/4HANA. “Customer” is a role that this business partner can take on — just like “FI customer” or “supplier”. So one and the same business partner can hold several roles at once."
  - q: "Where is customer master data maintained in SAP?"
    a: "Centrally, through business partner maintenance — classically with transaction BP or via a suitable Fiori app in the SAP Fiori Launchpad. There you maintain general data, sales area data and company code data all in one place."
  - q: "Why do I have to maintain sales area data separately per area?"
    a: "Because a customer can be handled differently in different sales areas — for example differently in direct sales than in wholesale. If you want to use a customer in several sales areas, you need a dedicated data set for each one."
  - q: "What happens if partner functions are missing?"
    a: "Without the required partner functions — sold-to party, ship-to party, bill-to party and payer — you often cannot create a sales document at all. The process then stalls until the functions are added to the customer master record."
---

Whether it's a quotation, a sales order or an invoice — almost every step in SAP sales draws on the same record: the **customer master data**. It's the foundation from which documents pull their addresses, payment terms and shipping rules. This article explains, in plain language, how customer master data is structured in SAP S/4HANA and why the business partner concept behind it matters so much.

## In short: the central data source for sales

Customer master data is a **master record** that bundles everything important about a customer: who they are, where goods are delivered, how they pay and how they are treated for tax. When you create a sales order, the system pulls most of the details from this record automatically — you don't have to re-enter them every time.

What's special in SAP S/4HANA is that customers are managed through the **business partner concept**. A business partner is the overarching object, and “customer” is one of the roles it can take on.

## Where a sales document gets its data

When you create a sales document, SAP pre-fills many fields automatically from several master data sources:

- **Business partner master data (customer)** — address, payment terms, shipping conditions
- **Material master data** — description, weight, volume, unit of measure
- **Customer-material information** — customer-specific material numbers
- **Condition master data** — pricing, material price, customer discount
- **Output master data** — sending order confirmations by email, EDI or fax
- **Control tables** — maintained in Customizing, they govern which data is proposed

Most of the values carried over are **default values** that you can overwrite when needed. A **preceding document** can also serve as a template — for example a quotation from which the sales order is created. For how these pieces fit together in sales, see the overview of the [order-to-cash process](/blog/en/order-to-cash-process-sales/).

## The business partner concept in SAP S/4HANA

In SAP S/4HANA, customers and suppliers are managed through **business partner master data**. This lets you maintain them *centrally* — unlike in classic SAP ERP, where customer and supplier were kept separately.

In practice this means: one and the same business partner can be a customer, an FI customer and even a supplier at the same time — without you having to create them multiple times. The business partner concept bundles all master data in one place and distinguishes the different business contexts through roles. If you want to go deeper on the concept, the article on the [business partner concept in S/4HANA](/blog/en/business-partner-concept-s4hana/) helps.

### What business partner categories are there?

When creating a business partner, you must choose a **business partner category**:

- **Person** — a natural person
- **Organization** — a company, a department, an association
- **Group** — for example a shared household, a married couple, a board

### How does the role concept work?

The link between a business partner and the individual applications is established through a **role concept**. A role represents a business context in which the partner can appear. Typical roles are:

- **Customer** — relevant for sales processes
- **FI customer** — relevant for accounting
- **Supplier** — if the same partner is also procured from

Only once the appropriate roles are maintained can you use the business partner both in sales, as a sold-to party, and in accounting, as the recipient of a receivable. Maintenance happens either with transaction `BP` or through a corresponding Fiori app in the SAP Fiori Launchpad.

## The three data levels of a customer master record

A customer's data is organized into three levels. This hierarchy is the most important thing to understand — and also the one most often mixed up.

### Level 1 — general data (client level)

General data is relevant for both sales *and* accounting. It applies to all organizational units within a client. It includes:

- **Address** (street, postal code, city, country, region, language)
- **Bank details**
- **Communication data** (phone, email)
- **Tax numbers**

### Level 2 — sales area data (role “customer”)

Sales area data is relevant only for sales. It applies to a specific **sales area**, which is made up of three components:

- **Sales organization** — the selling unit
- **Distribution channel** — for example direct sales or wholesale
- **Division** — the product division

Important: if you want to use a customer in several sales areas, you have to maintain the sales area data *separately for each area*. To keep things manageable, the fields are spread across tabs, among them:

- **Sales** — ordering behavior, customer pricing procedure, shipping conditions
- **Shipping** — delivering plant, delivery priority, complete delivery
- **Billing** — payment terms, Incoterms, account assignment group, tax classification
- **Partner functions** — sold-to party, ship-to party, bill-to party, payer

### Level 3 — company code data (role “FI customer”)

Company code data is relevant for accounting and applies to a specific company code. It is often maintained by accounting itself. A key field is the **reconciliation account**: through this general ledger account, customer postings are automatically recorded in the general ledger, so that the subledger and the general ledger always stay in sync.

## The four standard partner functions in sales

Every customer master record needs four mandatory partner functions in sales. In most cases these are all the same party — but for corporate customers the roles can be split:

- **Sold-to party** — who places the sales order
- **Ship-to party** — who physically receives the goods (can be a different address, e.g. a branch)
- **Bill-to party** — who receives the invoice
- **Payer** — who pays the invoice (e.g. a central corporate treasury)

An example from the corporate world: the sold-to party is the subsidiary, the ship-to party a specific branch, the bill-to party the corporate administration and the payer the central treasury. Separating these functions makes it possible to map complex delivery and payment paths cleanly.

## Why master data is organized into views

SAP master data is organized into **views**, each assigned to an organizational unit — plant, sales organization, company code and so on. This segmented structure provides flexibility and **data integrity**: when all relevant details converge in a single data object, there are no redundant copies. Sales, purchasing, inventory management, invoice verification and finance all access the same data — a core advantage over older systems with separate customer and vendor worlds.

## What users actually do with it

Maintaining customer master data is **not a daily task** — it usually happens when onboarding a new customer or during larger data maintenance campaigns, often by master data clerks or accounting. Even so, everyone in sales benefits from clean master data, because mistakes show up directly in the process:

- **Wrong address** → the delivery comes back, costs arise
- **Wrong payment term** → an overly generous cash discount, margin loss
- **Wrong tax classification** → incorrect tax reporting, a compliance risk
- **Missing partner functions** → the document can't be created, the process stalls

Anyone working in sales with SAP should therefore at least understand the concept of the three data levels — even if they rarely maintain master data themselves.

## Common pitfalls

- **Confusing the three data levels.** General data applies across the whole client, sales area data only per sales area, company code data only per company code. Mix them up and you'll look for fields in the wrong place.
- **Creating sales area data only once.** A customer active in several sales areas needs its own sales area data everywhere — otherwise it can't be used there.
- **Forgetting roles.** Without the “customer” role there is no sales view, without “FI customer” no accounting view. Miss a role and you miss half the process.

## In a nutshell

Customer master data is the **central data source** for every sales process in SAP. In S/4HANA it runs through the business partner concept, where “customer” is just one of several roles a business partner can hold. The data is organized into three levels — general data, sales area data and company code data — and linked to the individual processes through partner functions. Once you've internalized this structure, you understand why a well-maintained customer master is half the battle for smooth orders, deliveries and invoices.

## Frequently asked questions

### What is the difference between a business partner and a customer in SAP?

The business partner is the overarching master data object in SAP S/4HANA. “Customer” is a role that this business partner can take on — just like “FI customer” or “supplier”. So one and the same business partner can hold several roles at once.

### Where is customer master data maintained in SAP?

Centrally, through business partner maintenance — classically with transaction BP or via a suitable Fiori app in the SAP Fiori Launchpad. There you maintain general data, sales area data and company code data all in one place.

### Why do I have to maintain sales area data separately per area?

Because a customer can be handled differently in different sales areas — for example differently in direct sales than in wholesale. If you want to use a customer in several sales areas, you need a dedicated data set for each one.

### What happens if partner functions are missing?

Without the required partner functions — sold-to party, ship-to party, bill-to party and payer — you often cannot create a sales document at all. The process then stalls until the functions are added to the customer master record.
