---
layout: post
lang: en
title: "SAP SD Pricing with the Condition Technique explained"
description: "Condition types, access sequences, tables, records and the pricing procedure: how SAP S/4HANA finds the price on a sales order — in plain language."
slug: sd-pricing-condition-technique
permalink: /blog/en/sd-pricing-condition-technique/
translation_key: post-sd-pricing
date: 2026-07-08
category: "Sales"
keywords: "SAP SD pricing, condition technique, condition type, access sequence, condition table, condition record, pricing procedure, S/4HANA Sales"
reading_time: 10
sources:
  - label: "SAP Help Portal — Pricing in Sales (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Sales area — general background on pricing and the condition technique. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the condition technique in SAP SD?"
    a: "The condition technique is the rule set SAP S/4HANA uses to automatically determine prices, discounts, surcharges and taxes in sales. It is made up of five interlocking objects and defines which value is copied into a sales document under which conditions."
  - q: "What is the difference between a condition type and a condition record?"
    a: "The condition type describes what is determined — for example a material price or a customer discount — and is a Customizing setting. The condition record is the concrete value behind it, such as “74 EUR for this material for this customer”, and is maintained as master data in day-to-day work."
  - q: "What is an access sequence for?"
    a: "The access sequence is the search strategy of a condition type. It defines the order in which the system looks for matching condition records — from the most specific access (say customer and material) down to the most general (material only). The first hit wins and ends the search."
  - q: "What is a pricing procedure?"
    a: "The pricing procedure is the ordered list of all condition types a document runs through — from the base-price line through discounts and surcharges to tax, including subtotals. In German it is called “Kalkulationsschema”; both terms mean the same thing."
  - q: "Why does the more specific price win when two prices match?"
    a: "Because the access sequence is sorted from specific to general and the system stops searching at the first hit. A condition record for “customer and material” is checked before the general record for “material” and therefore overrides it automatically — without you switching anything off."
---

When you create a sales order in SAP, a unit price suddenly appears, a discount is deducted automatically, and finally tax is added to the item. What looks like magic is in fact a clearly defined rule set: the condition technique. This article breaks it down into its building blocks and shows, step by step, how the system arrives at a price.

## In short: the rule set behind every price

The condition technique is the mechanism SAP S/4HANA uses in sales to automatically determine which price, which discount, which surcharge and which tax are copied into a sales document. It is made up of five objects that work together. The big advantage: you can make prices and discounts depend on almost any field in the document — the customer, the material group, the sales organization, or a combination of them.

The same logic sits behind more than just pricing. Output (message) determination, revenue account determination and other automatic mechanisms in the system build on it too. Once you understand the condition technique, you understand a whole family of determination mechanisms at once.

## What is the condition technique in SAP SD?

When you create a sales order, SAP does not simply look at a single “price” field in the material master. Instead, a defined search-and-calculation process runs in the background. This process is set up entirely in **Customizing** — the system settings a consultant usually configures — and consists of several interlocking objects.

That flexibility is exactly why the condition technique is so powerful, and why it feels so confusing to newcomers at first. As soon as you know the five building blocks and how they interact, the confusion disappears.

## The five building blocks at a glance

Before we work through an example, it pays to keep the central objects cleanly apart:

- **Condition type** — describes *what* is determined (for example a material price, a customer discount, a freight surcharge). It controls properties such as the condition class (price, discount, surcharge, tax), the allowed scales, the validity period, and whether the value acts at header or item level.
- **Access sequence** — defines the *search strategy*: in what order does the system look for matching values? First “customer and material”, then “price list and material”, then “material” alone? Each access sequence is firmly assigned to a condition type.
- **Condition table** — the specific field combination under which a value is stored (for example the combination of sales organization, distribution channel, customer and material).
- **Condition record** — the actual data record with the real value, such as “for this sales organization, this customer and this material, the unit price is 74 EUR”.
- **Pricing procedure** — the ordered list of all condition types a document runs through, including subtotals, calculation formulas and requirements.

In German the pricing procedure is called “Kalkulationsschema”. Both terms mean the same thing.

## How is a pricing procedure structured?

A pricing procedure is essentially a table of rows. Each row is a condition type, each row has a **step** (the order of processing) and a **counter** (the sorting within a step). Here is what a heavily simplified procedure for sales pricing might look like:

| Step | Condition type | Meaning | Effect |
| --- | --- | --- | --- |
| 10 | Material price | base price | + gross unit price |
| 100 | Customer discount (%) | percentage discount | − discount |
| 110 | Customer/material discount | absolute discount | − discount |
| 200 | Subtotal | net before freight | = net item |
| 300 | Freight surcharge | freight cost | + surcharge |
| 400 | Value-added tax | output tax | + tax on net |
| 900 | Final amount | gross item | = amount payable |

The system processes the procedure **strictly top to bottom**. For each row it checks: “Is there a valid condition record for this condition type for this item?” If yes, it copies the value into the document. If no, the row is skipped — unless the condition type is flagged as mandatory, in which case the document would be incomplete.

Which pricing procedure is used at all is decided by SAP through two keys: the **document pricing procedure** (comes from the sales document type) and the **customer pricing procedure** (comes from the sales-area view of the customer master). From the combination of both keys plus the sales organization, the system determines the right procedure. This step is called procedure determination.

## How do you create a condition record?

To turn the empty pricing procedure into real prices, you need **condition records**. They are master data and are maintained in day-to-day work — classically through a maintenance transaction, and in S/4HANA also through a corresponding Fiori app such as “Set Prices”. The logic behind it: creating, changing and displaying are separate functions.

Imagine you have agreed a quantity-based price scale with a major customer and want to store it so it doesn't have to be entered manually on every order. The path there:

1. **Choose the condition type.** You enter the condition type — for a material price, that is the corresponding price condition type.
2. **Choose the key combination.** SAP asks: “At what level should the price apply?” You pick, for example, “customer and material”, because the price should apply only to this one customer. Behind this choice sits a condition table.
3. **Enter organizational data and key.** Sales organization, distribution channel, customer and material — that is, the fields of the chosen condition table.
4. **Maintain the scale.** Using the scale function you store, say, three price levels: from 1 piece 78 EUR, from 25 pieces 74 EUR, from 250 pieces 68 EUR. That fully captures the quantity discount for your major buyer in the system.
5. **Check validity.** Condition records always have a validity period (from/to). For time-limited promotions you should set this period deliberately.
6. **Save.** The condition record is stored and is immediately available for pricing.

When sales now enters an order for 60 pieces of this material for exactly this customer, SAP automatically applies the unit price of 74 EUR — the middle scale level applies, because 60 lies between 25 and 250 pieces. On the “Conditions” tab of the item, the determination can be traced step by step.

## How does the system search during pricing?

This is perhaps the most important concept. A price condition type usually has an access sequence with *several* accesses — from the most specific to the most general. For example:

| Access | Key fields | Specificity |
| --- | --- | --- |
| 10 | Customer / material | very specific |
| 20 | Price list / currency / material | medium |
| 30 | Material | general |

When processing a condition type, SAP fills the key fields of the first access from the document (customer from the header, material from the item), searches the associated condition table for a valid condition record and — crucially — **stops searching as soon as a hit is found**. Only when an access comes up empty does the system move on to the next access.

This has two practical consequences:

- A specific condition record “customer and material” automatically *overrides* a general record “material only”. You don't have to switch anything off — the order does it.
- The *order of the accesses* within the access sequence is just as critical as the order of the condition types in the pricing procedure. A wrongly sorted access sequence can mean customer discounts or promotional prices never take effect.

## What kinds of conditions are there?

SAP ships numerous condition types as standard. For understanding, it is enough to know the typical categories:

- **Price** — the base price per material, often customer- or price-list-specific and frequently with a quantity scale.
- **Discount** — reduces the price, for example as a percentage customer discount on all items, or an absolute discount for a specific customer-material combination.
- **Surcharge** — increases the price, for example a freight surcharge depending on the item weight.
- **Tax** — the output tax, determined automatically from country plus the tax classification of customer and material.

Three points are important to grasp here:

- The **condition class** (price, discount, surcharge, tax) decides the sign and the posting.
- The **calculation rule** determines whether it is a fixed amount, a percentage, a quantity-based rate or a scale.
- Some condition types may be **overridden manually** — for instance when sales grants a special discount — while others are locked in Customizing. This is set per condition type.

## Master data or Customizing — what goes where?

A common stumbling block is mixing up master data and Customizing. The rule of thumb:

- **Customizing** (set up once by the consultant): condition type, access sequence, condition table and pricing procedure. This is the rule set.
- **Master data** (maintainable in day-to-day work): the condition record. This is the concrete value inside the rule set.

Put differently: the consultant builds the road (Customizing), and the user places the concrete prices on it (master data). Keep those two layers cleanly apart and you immediately see why a new price needs no Customizing — and why a new discount logic very much does.

## Common pitfalls

- **Mixing up the terms.** Condition type, condition record, condition table, access sequence, pricing procedure — these words sound alike. Match each to its “what does it do?” and the confusion clears.
- **Sorting the access sequence wrong.** If the general access comes before the specific one, the specific price never applies. Always sort from specific to general.
- **Assuming every row adds up.** Within one condition type only *one* condition record is applied — the first hit. After that, the system moves to the next row in the procedure.

## In a nutshell

The condition technique looks like a storm of terms at first, but it follows a simple core principle: a pricing procedure is an ordered list of condition types. For each condition type, an access sequence searches one condition table after another for a matching condition record. The first hit wins, then it moves to the next row. Once you internalize this logic, you understand not just pricing in sales, but a whole family of determination mechanisms in SAP.

## Frequently asked questions

### What is the condition technique in SAP SD?

The condition technique is the rule set SAP S/4HANA uses to automatically determine prices, discounts, surcharges and taxes in sales. It is made up of five interlocking objects and defines which value is copied into a sales document under which conditions.

### What is the difference between a condition type and a condition record?

The condition type describes what is determined — for example a material price or a customer discount — and is a Customizing setting. The condition record is the concrete value behind it, such as “74 EUR for this material for this customer”, and is maintained as master data in day-to-day work.

### What is an access sequence for?

The access sequence is the search strategy of a condition type. It defines the order in which the system looks for matching condition records — from the most specific access (say customer and material) down to the most general (material only). The first hit wins and ends the search.

### What is a pricing procedure?

The pricing procedure is the ordered list of all condition types a document runs through — from the base-price line through discounts and surcharges to tax, including subtotals. In German it is called “Kalkulationsschema”; both terms mean the same thing.

### Why does the more specific price win when two prices match?

Because the access sequence is sorted from specific to general and the system stops searching at the first hit. A condition record for “customer and material” is checked before the general record for “material” and therefore overrides it automatically — without you switching anything off.
