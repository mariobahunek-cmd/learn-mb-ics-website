---
layout: post
lang: en
title: "The General Ledger in SAP S/4HANA: financial accounting explained"
description: "G/L accounts, chart of accounts, the Universal Journal and reconciliation accounts: how the General Ledger (FI-GL) works in SAP S/4HANA, in plain language."
slug: general-ledger-s4hana-finance
permalink: /blog/en/general-ledger-s4hana-finance/
translation_key: post-general-ledger
date: 2026-07-08
category: "Finance"
keywords: "SAP General Ledger, FI-GL, financial accounting, G/L account, chart of accounts, Universal Journal, ACDOCA, reconciliation account, company code, S/4HANA Finance"
reading_time: 10
sources:
  - label: "SAP Help Portal — Financial Accounting (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Finance / General Ledger Accounting area — general background on the General Ledger. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the General Ledger in SAP S/4HANA?"
    a: "The General Ledger (FI-GL) is the central component of external accounting in SAP S/4HANA. It records every value-relevant business transaction completely and in a reconciled way, so that a proper balance sheet and profit-and-loss statement can be produced at any time."
  - q: "What is the Universal Journal?"
    a: "The Universal Journal is a single central table (technically ACDOCA) in which SAP S/4HANA stores all value-relevant postings from Financial Accounting, Controlling, Asset Accounting and Profit Center Accounting together. As a result there is only one source of data instead of separate tables that constantly have to be reconciled."
  - q: "What is the difference between a chart of accounts and a G/L account?"
    a: "A G/L account is a single position in the books, such as “bank main account” or “domestic revenue”. The chart of accounts is the ordered directory that holds the definition of all G/L accounts in a ledger — essentially the account number, the account name and the account type."
  - q: "Why can't you post directly to a reconciliation account?"
    a: "A reconciliation account links a sub-ledger — such as customers, vendors or assets — to the General Ledger in real time. It is updated automatically from the sub-ledger only. Direct postings to it are blocked so that the sub-ledger and the General Ledger always match."
  - q: "At what level is the balance sheet produced?"
    a: "The statutory balance sheet and the profit-and-loss statement are produced at company code level. The company code is the smallest self-contained accounting unit — usually a single legally independent company."
---

If you want to understand the numbers behind a business, sooner or later you arrive at the General Ledger. In SAP S/4HANA it is the heart of financial accounting: it's where every value-relevant business transaction comes together, and where the balance sheet and profit-and-loss statement ultimately take shape. This article explains, in plain language, what the General Ledger is built from and how the pieces fit together.

## In short: the heart of financial accounting

The General Ledger (**FI-GL** for short) is the central component of external accounting in SAP S/4HANA. Its job is clear: to record **every value-relevant business transaction completely and in a reconciled way**, so that a proper **balance sheet** and **profit-and-loss statement (P&L)** can be produced at any time.

The General Ledger is therefore both a complete record of all business transactions and the central source for financial reporting. From it you can derive, among other things:

- information about an individual account
- journals
- totals and balance lists
- balance sheet and P&L evaluations

Every posting in the sub-ledgers — accounts receivable, accounts payable, assets, bank — is automatically posted to the General Ledger as well. This is the well-known **real-time integration** through reconciliation accounts, which we'll come back to below.

## What is the Universal Journal?

Anyone who worked with older SAP systems knows a structural weakness: **Financial Accounting (FI) and Controlling (CO) lived in separate tables.** The General Ledger sat in the FI tables, Controlling in its own CO tables, Profit Center Accounting somewhere else again. Data constantly had to be matched up and transferred between them.

SAP resolved exactly this break with S/4HANA. The keyword is the **Universal Journal** — a single central table (technically *ACDOCA*) in which **all value-relevant postings from Financial Accounting, Controlling, Asset Accounting and Profit Center Accounting** are stored together.

What does that mean in practice?

- **A single source of truth:** there are no longer any differences between the FI and CO views, because the data comes from the same table.
- **Analysis across many dimensions:** balance sheets by profit center, segment or business area are possible out of the box, because every dimension is attached directly to the document.
- **Real-time reporting:** evaluations such as the balance sheet or P&L read straight from the Universal Journal — separate aggregation tables are no longer needed.

A visible example: in SAP S/4HANA, profit centers can be part of financial accounting. Their information is stored in the Universal Journal, and — like company codes — they act as a dimension for financial reporting. The Universal Journal is thus far more than a database trick; it's the reason FI and CO grow together in S/4HANA.

## G/L accounts and the chart of accounts

The General Ledger is made up of **G/L accounts** (general ledger accounts). Each G/L account represents a specific position in the books — for example “bank main account”, “trade payables” or “domestic revenue”.

All G/L accounts together are organized in the **chart of accounts**. The chart of accounts holds, in an ordered form, the definition of all G/L accounts in a ledger. That definition essentially covers the **account number**, the **account name** and the **account type**.

A few terms make the chart of accounts more tangible:

- **Operating chart of accounts:** the chart of accounts assigned to a company code and actually used for postings.
- **Account group:** bundles accounts with a similar business function (such as cash accounts, expense accounts, revenue accounts). It also controls number ranges and defines which fields are required, optional or hidden during entry.
- **Account type:** distinguishes accounts by their role — for example balance sheet account, cash account (bank reconciliation account), primary costs or revenue, secondary costs, and non-operating expenses and income.

G/L accounts are maintained and displayed in S/4HANA through the corresponding Fiori app in the General Ledger area of the launchpad. Through its account number and account group, every G/L account sits in exactly its place in the chart of accounts.

## The company code as the central accounting unit

Perhaps the most important organizational element in finance is the **company code**. A company code is an **independent accounting unit and the smallest organizational element for which a complete, self-contained set of books** can be modeled. A typical example is a single legally independent company within a group.

A few defining facts about the company code:

- It has a **four-character, alphanumeric key** (for example 1010 or 1710 in SAP's sample clients).
- Each company code has exactly **one local currency**. Foreign-currency amounts are converted automatically.
- **The General Ledger is kept at company code level.** This is the level at which statutory balance sheets and P&L statements are produced.
- Every transaction in the finance component requires a company code.

That makes the company code the actual **reporting entity**: if you want to know at what level the balance sheet is produced, the answer is here.

## How does document entry work?

The bread and butter of accounting is **entering G/L postings**. In SAP S/4HANA there's a dedicated Fiori app for posting General Ledger documents. Its entry screen is typically split into several areas:

- **Header data:** posting date, document type, company code, period and the like. These entries apply to the whole document.
- **Line item data:** here you enter the individual line items — one G/L account per line, with a debit or credit amount.
- **Tax items:** details of the tax calculation, such as whether tax is calculated automatically.
- **Templates:** ready-made posting document templates can be referenced here.

In terms of content, every posting always follows the same pattern:

1. **Enter the document header** — date, document type, company code.
2. **Enter the line items** — at least two: one debit and one credit item. This is the accounting golden rule of “debit to credit”; every posting must balance.
3. **Simulate or post the document** — only here does it become binding.

Only on a successful posting does the system assign a unique **document number** in the background and write the document to the Universal Journal.

## Document type and posting key: the control instruments

Two terms are easily confused: **document type** and **posting key**. Both steer the posting, but at different levels.

The **document type** sits in the **document header** and distinguishes the many kinds of accounting documents from one another. Classic standard document types include:

- **SA** — G/L account documents
- **DR** — customer invoices
- **DG** — customer credit memos
- **DZ** — customer payments
- **KR** — vendor invoices
- **KG** — vendor credit memos
- **KZ** — vendor payments

Among other things, each document type controls the **document number range** and the permitted account types.

The **posting key**, by contrast, sits at **line item level** — that is, per line in the document. It signals three things to the system:

- which **account type** is used (G/L account, customer, vendor, asset, material)
- whether it is a **debit or a credit** posting
- which **field status** applies to the additional entries

For pure General Ledger postings, two posting keys are enough: **40** stands for a debit posting to a G/L account and **50** for a credit posting. In the modern Fiori apps you no longer type these keys yourself — you simply pick the “debit” or “credit” column, and the system assigns 40 or 50 behind the scenes, along with their control functions. So they haven't been abolished; they just keep running under the hood.

## What is a reconciliation account?

One central concept worth truly understanding is the **reconciliation account**. A reconciliation account links a sub-ledger to the General Ledger in **real time**: the moment a posting is made in a sub-ledger, a posting is made simultaneously to the matching reconciliation account in the General Ledger.

An example makes it tangible: an accountant enters a vendor invoice in accounts payable. That invoice becomes visible in the **vendor master record** (the sub-ledger) — and at the same time, in the background, the assigned reconciliation account “trade payables” is updated in the General Ledger. There is therefore no difference between the sub-ledger and the General Ledger; they are in sync in real time.

The following sub-ledgers, among others, are connected to the General Ledger through reconciliation accounts:

- **Accounts payable** (FI-AP)
- **Accounts receivable** (FI-AR)
- **Asset accounting** (FI-AA)

An important practical consequence: **you cannot post directly to a reconciliation account.** It is served exclusively and automatically through the respective sub-ledger postings. If you try to post directly to the “trade receivables” account, the system stops you — you post through the customer invoice in the sub-ledger instead. That's how the reconciliation between the books stays intact at all times.

## Posting periods and period-end closing

Every posting in SAP is assigned to a **posting period**. Usually a period corresponds to one month of the fiscal year — so twelve regular periods plus possible special periods for closing entries.

On every posting, the system checks whether the target period is **open**. Only once a period has been opened for a document type and an account type can you post to it. This is how SAP prevents postings from slipping retroactively into months that are already closed.

At period-end, a set of typical closing tasks comes up:

- posting accruals and deferrals (for example an insurance expense that spans several periods)
- maintaining the **GR/IR clearing account** — the account where goods received without an invoice and invoices without goods received are held temporarily
- creating a document journal
- generating the balance sheet and P&L
- creating totals and balance lists

You don't have to carry out these tasks yourself every day — but it helps enormously to know they exist and in what order they typically run.

## Ledgers and parallel accounting

Many companies have to comply with several accounting standards at once — for example local GAAP for the statutory annual accounts and **IFRS** for the group accounts, and sometimes **US-GAAP** on top. SAP S/4HANA offers two approaches for this:

- **Accounts approach:** different valuations are posted to different accounts. When the statements are produced, the balance sheet / P&L structure evaluates the appropriate accounts for each standard.
- **Ledger approach:** several parallel “general ledgers” (ledgers) run at the same time. Exactly one ledger is the **leading ledger**, and the others complement it. For new implementations, the ledger approach is usually recommended today.

A **ledger** here is simply a complete view of the General Ledger under a particular set of rules. Each ledger also writes its values into the Universal Journal — which keeps parallel valuations cleanly separated while still living in a single source of data.

## A few common points of confusion

When getting started with the General Ledger, the same stumbling blocks come up again and again:

- **Mixing up company code and controlling area.** The company code is the reporting entity (FI). The controlling area is the organizational unit for Controlling (CO). A controlling area can contain several company codes — all sharing the same operating chart of accounts.
- **Equating the chart of accounts with the balance sheet / P&L structure.** The chart of accounts lists all G/L accounts. The balance sheet / P&L structure is the hierarchical arrangement of those accounts for reporting (such as “Assets → Fixed assets → Property, plant and equipment”). These are two different objects.
- **Trying to post directly to a reconciliation account.** It can't be done. Reconciliation accounts are updated exclusively and automatically from the sub-ledgers.
- **Dismissing the Universal Journal as “just technology”.** It's the reason profit centers are part of FI in S/4HANA, why balance sheets by segment are possible, and why FI/CO reconciliation is no longer needed.

## In a nutshell

The General Ledger in SAP S/4HANA reads as a single connected story: a business (the company code) keeps its accounts (G/L accounts) in an ordered directory (the chart of accounts). Every business transaction is captured as a document (document type) — either directly through a General Ledger posting (posting keys 40/50) or automatically from a sub-ledger through a reconciliation account. It all lands in the same table (the Universal Journal, technically ACDOCA), from which the balance sheet and P&L emerge at period-end. Once you grasp that chain, the many detailed terms of financial accounting fall into place with ease.

## Frequently asked questions

### What is the General Ledger in SAP S/4HANA?

The General Ledger (FI-GL) is the central component of external accounting in SAP S/4HANA. It records every value-relevant business transaction completely and in a reconciled way, so that a proper balance sheet and profit-and-loss statement can be produced at any time.

### What is the Universal Journal?

The Universal Journal is a single central table (technically ACDOCA) in which SAP S/4HANA stores all value-relevant postings from Financial Accounting, Controlling, Asset Accounting and Profit Center Accounting together. As a result there is only one source of data instead of separate tables that constantly have to be reconciled.

### What is the difference between a chart of accounts and a G/L account?

A G/L account is a single position in the books, such as “bank main account” or “domestic revenue”. The chart of accounts is the ordered directory that holds the definition of all G/L accounts in a ledger — essentially the account number, the account name and the account type.

### Why can't you post directly to a reconciliation account?

A reconciliation account links a sub-ledger — such as customers, vendors or assets — to the General Ledger in real time. It is updated automatically from the sub-ledger only. Direct postings to it are blocked so that the sub-ledger and the General Ledger always match.

### At what level is the balance sheet produced?

The statutory balance sheet and the profit-and-loss statement are produced at company code level. The company code is the smallest self-contained accounting unit — usually a single legally independent company.
