---
layout: post
lang: en
title: "The Business Partner in SAP S/4HANA — one master record for customers and suppliers"
description: "The central master data object for customers and suppliers in SAP S/4HANA — what the Business Partner is, its types, roles, and why it replaced old records."
slug: business-partner-concept-s4hana
permalink: /blog/en/business-partner-concept-s4hana/
translation_key: post-geschaeftspartner
date: 2026-07-07
category: "Master Data"
keywords: "SAP Business Partner, SAP S/4HANA, customer, vendor, master data, role concept, transaction BP, end user"
reading_time: 7
sources:
  - label: "SAP Help Portal — Business Partner (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Master Data / Business Partner — general background on the Business Partner. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between a Business Partner and a customer record?"
    a: "The Business Partner is the higher-level master data object — the container for all the data about a partner. The customer (a customer in the finance view) is just a role that this Business Partner can take on. One Business Partner can be both a customer and a vendor at the same time."
  - q: "Where is the Business Partner maintained?"
    a: "In the classic SAP GUI via transaction BP, and in SAP Fiori via the app for managing Business Partner master data. Both paths write to the same tables — you pick whichever fits your working environment."
  - q: "Why was the Business Partner introduced in SAP S/4HANA?"
    a: "Previously there were separate customer and vendor records, which had to be maintained twice for partners with a dual role. The Business Partner consolidates this into a single master record and represents the functions through roles — which reduces redundancy and maintenance effort."
  - q: "Can I change the Business Partner type later?"
    a: "Not easily, by standard. The type — person, organisation or group — is set when you create the record and is fixed afterwards. That's why it pays to clarify up front what you're actually dealing with."
  - q: "What is the difference between general and role-specific data?"
    a: "General data such as address, bank details and communication applies across all roles and is maintained only once. Role-specific data such as payment terms or purchasing conditions applies only within the relevant role."
---

"Isn't a Business Partner just another word for a customer record?" Few concepts make switchers frown as much as the Business Partner — and the question mostly comes from people who spent years working with the old customer and vendor accounts. The short answer is no, but the two are closely linked. The **Business Partner** (Geschäftspartner in German) is the pivot point in SAP S/4HANA: without it there is no sales order, no purchase order and no invoice, no matter whether you work in purchasing, in sales or in accounting.

## What it's really about: one master record for all external partners

In SAP S/4HANA, the Business Partner is the **central master data object** for all of a company's external partners: above all customers and suppliers, but also other people or organisations the company has a business relationship with.

Here's what's special: a Business Partner is created only once. Through a role concept, it can then be used for very different processes, as a customer in sales, as a supplier in purchasing, or as a customer or vendor in accounting. One master record, many functions.

## What came before? Customer and vendor records

Anyone who worked with SAP R/3 or SAP ERP (ECC) knows a different world, the world of separate master records:

- A **customer master record** for customers.
- A **vendor master record** for suppliers.

If a company dealt with the same partner as both a customer and a supplier, it needed *two separate records*. Address, bank details and communication data sat in the system more than once and had to be maintained twice — with all the risks of typos and stale data.

That's exactly what the Business Partner approach resolves. There's now just one master record per partner, and the different functions are represented through roles. In SAP S/4HANA, maintaining a partner through the Business Partner is the intended path; the old, separate maintenance routes for customers and vendors are no longer the standard.

## The three Business Partner types

When you create a Business Partner in the system, the first decision is always: which type is it? SAP distinguishes three fixed types, and you choose exactly one.

### Person

A natural person — a human being with a first and last name. Typical examples: a private customer, an employee or an individual contact. Here you maintain fields such as first name, last name, form of address and, where relevant, date of birth.

### Organisation

A legal entity — a company, an association or another institution. Typical examples: an industrial customer, a wholesale supplier, a public authority. Here you maintain the organisation's name and, as needed, its legal form, industry and tax data.

### Group

A grouping of people or organisations that acts as one shared partner towards the company. Typical examples: a married couple or a joint venture (consortium).

Worth knowing: once chosen, the type can't simply be changed later. That makes the right choice at creation a key step.

## The role concept — the heart of it

Understand the role concept and you've understood the Business Partner. A **role** describes the function in which a Business Partner acts for a particular process. And a single Business Partner can hold several roles at the same time.

Typical roles include, for example:

- **Business Partner (general):** the base role with the core master data such as name, address, communication and tax number. This data applies to every other role.
- **Customer (FI):** the partner acts as a customer in financial accounting — with company-code-specific data such as the reconciliation account and payment terms.
- **Vendor (FI):** the partner acts as a supplier in financial accounting.
- **Customer (Sales):** the partner acts as a customer in sales — with sales-area-specific data such as shipping conditions.
- **Supplier (Purchasing):** the partner acts as a supplier in purchasing — with purchasing-organisation-specific data.
- **Contact person:** the partner is a point of contact.

Picture this example: your company buys office supplies from a firm — and that same firm rents warehouse space from you at the same time. So the partner is a *supplier* and a *customer* at once.

Previously you'd have needed two master records for this. In SAP S/4HANA you create one Business Partner and give it the role "customer" and the role "supplier". Address, bank details and communication sit in the system only once and are used for both roles. That's the core advantage.

## General and role-specific data

For the Business Partner, SAP distinguishes between **general data** (applies across all roles) and **role-specific data** (applies only within a particular function).

**General data** is independent of the role the partner is currently used in:

- **Address:** street, postal code, city, country, and several addresses are possible.
- **Bank details:** IBAN, BIC, bank name, all important for payments.
- **Tax information:** such as the VAT identification number.
- **Communication data:** phone, email and other ways to get in touch.

**Role-specific data** only comes into play once you assign a role to the partner. In the customer role that means shipping and payment terms plus the credit limit, in the supplier role the order currency and the purchasing conditions. And in the FI role it's the reconciliation account and the company-code-related data.

The rule of thumb: general data applies *once for all roles*, role-specific data *only within the relevant role*.

## How to create a Business Partner

In SAP S/4HANA there are two central paths, and both write to the same tables:

- **Classic SAP GUI:** transaction `BP` — the central maintenance screen for all Business Partner roles.
- **SAP Fiori:** an app for managing Business Partner master data, for modern, browser-based maintenance. For finding your way around that interface, see the post on the [basics of the SAP Fiori launchpad](/blog/en/sap-fiori-launchpad-basics/).

A typical flow looks like this:

1. **Open the maintenance tool** — transaction BP or the matching Fiori app.
2. **Choose the type** — person, organisation or group.
3. **Enter general data** — name, address, communication.
4. **Add a role** — depending on the function the partner should act in.
5. **Maintain role-specific data** — such as company code, reconciliation account, payment terms.
6. **Add further roles if needed.**
7. **Save** — the system assigns a Business Partner number.

The charm: you enter the address and bank details only once. Add a second role later and that data is already there; you only maintain the extra fields the new role needs.

## Why the Business Partner is so central

The Business Partner is the foundation many business processes build on. Without it there's no sales order, no purchase order and no incoming invoice. Anyone working in the [procure-to-pay process](/blog/en/procure-to-pay-process/) or in sales runs into it constantly, usually without thinking much about it, because it quietly works in the background as a reliable data core.

## Common pitfalls

This mix-up is especially common: users still think in the old customer-and-vendor terms and trip over the fact that a single Business Partner in S/4HANA can carry several roles at once, so one and the same partner can be both a customer and a supplier.

- **Equating the Business Partner with the customer.** The Business Partner is the container; the customer is just one of its roles. Mix the two up and you'll look for data in the wrong place.
- **Creating a new record for every function.** That used to be the way — today you simply add another role. Duplicate master records are explicitly no longer the approach.
- **Picking the type too hastily.** Person, organisation or group is fixed once the record is created. A moment's thought beforehand saves grief later.
- **Confusing general and role-specific data.** The address is general; the payment terms are role-specific. Knowing the split helps you find fields faster.

## The takeaway

In SAP S/4HANA, the Business Partner is the one master record for all external partners, customers and suppliers alike. It replaces the formerly separate customer and vendor records, comes in the three types person, organisation and group, and is used flexibly through roles. You maintain general data once and role-specific data per role. Internalise that principle — one partner, many roles — and you've grasped a core foundation of SAP S/4HANA.

## Frequently asked questions

### What is the difference between a Business Partner and a customer record?

The Business Partner is the higher-level master data object — the container for all the data about a partner. The customer (a customer in the finance view) is just a role that this Business Partner can take on. One Business Partner can be both a customer and a vendor at the same time.

### Where is the Business Partner maintained?

In the classic SAP GUI via transaction BP, and in SAP Fiori via the app for managing Business Partner master data. Both paths write to the same tables — you pick whichever fits your working environment.

### Why was the Business Partner introduced in SAP S/4HANA?

Previously there were separate customer and vendor records, which had to be maintained twice for partners with a dual role. The Business Partner consolidates this into a single master record and represents the functions through roles — which reduces redundancy and maintenance effort.

### Can I change the Business Partner type later?

Not easily, by standard. The type — person, organisation or group — is set when you create the record and is fixed afterwards. That's why it pays to clarify up front what you're actually dealing with.

### What is the difference between general and role-specific data?

General data such as address, bank details and communication applies across all roles and is maintained only once. Role-specific data such as payment terms or purchasing conditions applies only within the relevant role.
