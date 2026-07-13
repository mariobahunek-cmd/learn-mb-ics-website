---
layout: post
lang: en
title: "SAP S/4HANA Embedded Analytics: reporting inside the live system"
description: "What Embedded Analytics in SAP S/4HANA means: real-time reporting via CDS views, analytical Fiori apps and KPI tiles — explained in plain language."
slug: embedded-analytics-in-s4hana
permalink: /blog/en/embedded-analytics-in-s4hana/
translation_key: post-embedded-analytics
date: 2026-07-08
category: "Basics"
keywords: "SAP Embedded Analytics, SAP S/4HANA, CDS views, KPI tiles, analytical Fiori apps, real-time reporting, HANA in-memory, SAP Analytics Cloud"
reading_time: 9
sources:
  - label: "SAP Help Portal — SAP S/4HANA Analytics"
    url: "https://help.sap.com/"
    note: "Analytics / Embedded Analytics area — general background. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is Embedded Analytics in SAP S/4HANA?"
    a: "Embedded Analytics means that reports and evaluations run directly inside the operational SAP S/4HANA system — on the same live data, in real time, without the detour through a separate business intelligence system. This is made possible by the HANA in-memory database together with CDS views as the data model."
  - q: "What are CDS views?"
    a: "CDS views (Core Data Services) are a modeling layer that describes which data from which tables is combined for an evaluation. They are the data foundation for almost all analytical apps and reports in S/4HANA. End users don't build them — that's a job for consultants and developers."
  - q: "How does Embedded Analytics differ from a data warehouse like SAP BW?"
    a: "A data warehouse such as SAP BW extracts data from the ERP and loads it into a second system, usually with a time lag. Embedded Analytics evaluates directly on the original data in S/4HANA, in real time and without replication. For large, cross-source analyses, a data warehouse still makes sense."
  - q: "What is a dynamic tile (KPI tile)?"
    a: "A dynamic tile shows a live figure right on the home screen — for example the number of open purchase orders or the revenue for the month. The value updates automatically, so you can read your situation without ever opening the app."
  - q: "Do I need SAP Analytics Cloud in addition to Embedded Analytics?"
    a: "Not necessarily. Embedded Analytics covers operational evaluations directly in S/4HANA. SAP Analytics Cloud is an optional cloud platform for more advanced tasks such as enterprise-wide dashboards, planning and predictive analytics across several data sources."
---

In SAP S/4HANA, working and analyzing are no longer two separate worlds. Whoever creates a purchase order, posts an invoice or processes a sales order can evaluate the same data in the same system straight away, in real time and without a detour through a separate reporting tool. That is exactly what the term Embedded Analytics stands for.

Whenever we reach this point in a course, the same question comes up: “Don't I have to switch to another tool or over to BW for that?“ The moment it clicks is always the same: the evaluation is already right there, inside the workflow.

## What it's about: reporting inside the running system

Embedded Analytics means that analytical functions are built directly into SAP S/4HANA. You no longer need a separate business intelligence system to produce evaluations. The operational system and the analysis are one and the same: you work on the same live data, in real time, without having to copy the data somewhere first.

That's the big difference from the classic world, where one ERP system ran the processes and a second system delivered the reports.

## How did it work before — and what changed?

In the past you had two separate systems:

- The **ERP system** for the operational processes: purchase orders, sales orders, postings.
- A dedicated **BI system** such as SAP BW (Business Warehouse) for the evaluations.

The data first had to travel between the two. It was extracted, transformed and loaded into BW, often overnight. Only then could you build reports on it. That meant your evaluation showed yesterday's state, not the state right now.

In SAP S/4HANA this detour disappears. The analysis and the operational system are the same system. The purchase order you just posted shows up immediately in the matching evaluation.

## Why does this work? The HANA factor

What made this possible is the **SAP HANA in-memory database**. The name already says the essential part: it keeps the data in main memory (*in memory*) rather than mainly on disk. Calculations therefore run extremely fast, even on large data volumes, and even when you trigger them live on the operational data.

In practice that means:

- Evaluations run on the **original data**, not on copies.
- Reports deliver results in **real time**, not only after an overnight load.
- The effort for **data replication** disappears.
- Users always see the **current state**, not yesterday's.

This real-time character is the heart of the idea. Whenever you read about “evaluation in real time” or “without data replication”, it almost always points to Embedded Analytics.

## What are CDS views?

For evaluations to run directly on the operational data, you need a layer that prepares that data for analysis. This layer is called **CDS views**, short for *Core Data Services*.

Picture CDS views as a **data-model layer**. They build on classic database views and describe which data from which tables is combined for which evaluation, including relationships, calculations and meaningful field names. That makes them the technical foundation for almost all analytical apps and reports in S/4HANA.

For you as a user, the key points are:

- You **don't build CDS views yourself**. That's a job for consultants and developers.
- But you should be able to place the term: it describes **where the numbers come from** that an analytical app shows you.
- They ensure that different apps work on **the same, consistent data foundation**.

## How do you experience Embedded Analytics in the Fiori Launchpad?

The Fiori Launchpad is the home screen in S/4HANA — a set of tiles from which you open apps. Embedded Analytics shows up there in several forms.

### Analytical apps

**Analytical apps** are pure evaluation apps. They give you lists, key figures and visual summaries without your having to open a separate tool. A typical example is an app that shows you at a glance which sales orders are in which state and where things are stuck.

To place them correctly: analytical apps are not operational apps, you don't post anything with them, you evaluate. They access live data directly, without a detour through a BI system, and they sit in the Fiori Launchpad like every other app.

### KPI tiles (dynamic tiles)

A special case is the **KPI tile**, a form of **dynamic tile**. It shows a live figure right on the home screen, without your having to open the app. Typical examples:

- Number of open purchase orders
- Revenue for the current month
- On-time delivery rate as a percentage
- Number of overdue orders

The value updates automatically and always shows the current state. That way you can tell at a glance whether everything is fine or whether you need to step in. By contrast, a **static tile** shows only a title and an icon and simply opens the app when clicked — with no figure of its own.

### Overview pages and cards

A central data-driven app type is the **overview page**. It brings together all the information you need for a task on a single page, matched to your area of work or your role. It's built from several **cards**, each showing something different:

- **Analytical card** — visualizes a key figure graphically, for example the total purchase order value as a chart.
- **List card** — shows a list of relevant records, for example urgent requisitions.
- **Table card** — presents tabular data in columns, for example expenses by period and value.

Alongside it there is the **object page**. It shows all the details for a specific business object, such as a purchase order, a material or a customer, on one page, organized into a header, sections and blocks.

## From the number to the detail: drill-down

Evaluations in S/4HANA are rarely a dead end. The most important movement is the **drill-down**: you start with an aggregated number and work your way down step by step until you see the cause.

Here's an example of the path from top to bottom:

1. Total revenue this quarter
2. Revenue by region
3. Revenue by country
4. Revenue by customer
5. Revenue by individual order

That's how you find out where a deviation comes from, without opening five different reports. A single key figure turns into a whole analytical story.

When you want to look at several angles at once, **multidimensional reports** help. With them you can see, for example, revenue by product, by region and by quarter in a single evaluation, and you can change filters and views whenever you like. This, too, runs directly in the S/4HANA system, in real time, without external tools.

## How do you find the right evaluation?

With all these apps, tiles and reports, one question comes up quickly: which evaluations even exist? That's what the **Query Browser** is for — an app you use to browse the available reports and queries. You can filter by topic, look at previews and launch the right evaluation directly.

The Query Browser is especially useful when you're not sure whether a ready-made evaluation already exists for your question. Very often SAP already ships exactly what you need.

## Where does Embedded Analytics end — and where does SAP Analytics Cloud begin?

Embedded Analytics covers a great many scenarios, but not everything. For more complex requirements, **SAP Analytics Cloud (SAC)** comes into play as well — an optional cloud platform you can connect to S/4HANA. It offers:

- complex, interactive **dashboards**
- **planning functions** such as budgeting and forecasting
- **predictive analytics** with forecasting models
- data integration from **several sources**, not only from S/4HANA

Worth placing clearly: SAP Analytics Cloud is **not a mandatory component**. Embedded Analytics in S/4HANA works without it. SAC is an addition for use cases that go beyond what makes sense directly inside the ERP.

## Embedded Analytics compared with a data warehouse

This is exactly where the most common mix-up happens: Embedded Analytics and a classic **data warehouse** such as SAP BW (Business Warehouse) quickly get thrown into the same pot. Both have their place, but they solve different jobs.

| Aspect | Embedded Analytics | Data warehouse (e.g. SAP BW) |
| --- | --- | --- |
| Where evaluation happens | directly in S/4HANA | in a second system |
| Data basis | original data | copies of the data |
| Freshness | real time, current state | often time-lagged, yesterday's state |
| Data replication | none needed | extraction and load needed |
| Typical purpose | operational evaluations | large, cross-source analyses |

This doesn't mean the data warehouse disappears. For very large, enterprise-wide analyses across many sources, there are still good reasons to use a data warehouse (such as SAP BW/4HANA). But for the typical operational evaluations in an S/4HANA system, you no longer need it.

## A day with Embedded Analytics

To keep this from staying abstract, here's a typical flow:

1. **Log in to the Fiori Launchpad.** Right on the home screen, KPI tiles show the most important live figures for your area.
2. **A tile shows a critical value.** You click it and land in an analytical app with the details.
3. **In the app you use drill-down** to trace which cases are causing the problem.
4. **For a detailed view** you open a multidimensional report and filter by region and quarter.
5. **If you can't find a fitting evaluation**, you use the Query Browser to check what else is available.
6. **All the data is live.** You don't have to reload anything, replicate anything or wait for anything.

Once you understand how these building blocks fit together, you can quickly place even unfamiliar situations correctly.

## The key terms at a glance

- **Embedded Analytics** — evaluation directly in the ERP, without a separate BI system
- **HANA in-memory database** — keeps data in main memory, makes real time possible
- **CDS views** — the data-model layer for evaluations
- **Analytical apps** — pure evaluation apps in the launchpad
- **KPI tiles / dynamic tiles** — live figures right on the home screen
- **Drill-down** — from the aggregated number step by step into the detail
- **Multidimensional reports** — several angles in one analysis
- **Query Browser** — app for browsing the available evaluations
- **SAP Analytics Cloud (SAC)** — optional cloud platform for more advanced BI tasks

## The bottom line

Embedded Analytics is not a technical buzzword but a central concept in SAP S/4HANA: evaluations run directly inside the operational system, in real time, without the detour through a classic data warehouse. This is made possible by the HANA in-memory database together with CDS views as the data foundation. In the Fiori Launchpad you meet it as analytical apps, KPI tiles, overview pages and drill-down. Once you can keep these building blocks apart, it quickly becomes clear why analyzing and working belong together in S/4HANA.

## Frequently asked questions

### What is Embedded Analytics in SAP S/4HANA?

Embedded Analytics means that reports and evaluations run directly inside the operational SAP S/4HANA system — on the same live data, in real time, without the detour through a separate business intelligence system. This is made possible by the HANA in-memory database together with CDS views as the data model.

### What are CDS views?

CDS views (Core Data Services) are a modeling layer that describes which data from which tables is combined for an evaluation. They are the data foundation for almost all analytical apps and reports in S/4HANA. End users don't build them — that's a job for consultants and developers.

### How does Embedded Analytics differ from a data warehouse like SAP BW?

A data warehouse such as SAP BW extracts data from the ERP and loads it into a second system, usually with a time lag. Embedded Analytics evaluates directly on the original data in S/4HANA, in real time and without replication. For large, cross-source analyses, a data warehouse still makes sense.

### What is a dynamic tile (KPI tile)?

A dynamic tile shows a live figure right on the home screen — for example the number of open purchase orders or the revenue for the month. The value updates automatically, so you can read your situation without ever opening the app.

### Do I need SAP Analytics Cloud in addition to Embedded Analytics?

Not necessarily. Embedded Analytics covers operational evaluations directly in S/4HANA. SAP Analytics Cloud is an optional cloud platform for more advanced tasks such as enterprise-wide dashboards, planning and predictive analytics across several data sources.
