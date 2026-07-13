---
layout: post
lang: en
title: "Document entry in SAP FI: how posting a document works"
description: "Every posting in SAP FI ends up as a document. What the document header, line items and document type mean — and the difference between posting, parking and holding a document — explained clearly."
slug: fi-document-entry-basics
permalink: /blog/en/fi-document-entry-basics/
translation_key: post-fi-belegerfassung
date: 2026-07-07
category: "Finance"
keywords: "SAP FI, document entry, post document, document type, document header, line item, park document, financial accounting"
reading_time: 8
sources:
  - label: "SAP Help Portal — Finance (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "Finance / Financial Accounting — general background on document entry. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between a document header and a line item?"
    a: "The document header holds the general data that applies to the whole document — such as posting date, document type, company code and currency. The line items are the individual posting lines, each with an account and a debit or credit amount."
  - q: "What does it mean to post a document instead of parking it?"
    a: "A posted document is saved for good, gets a fixed document number and flows into the balance sheet and P&L. A parked document is saved but not yet reflected in the financials — it usually waits for approval."
  - q: "Why does SAP sometimes refuse to let me post?"
    a: "It's often down to a tolerance group, which sets maximum amounts per user. If a posting exceeds the limit, the system rejects it. That's a deliberate control, not an error."
  - q: "What is the document type for?"
    a: "The document type controls things like which number range the document number comes from and which account types are allowed in the document. It classifies the transaction — for example as a G/L posting, a vendor invoice or a customer invoice."
---

In SAP Financial Accounting, no business transaction gets around one thing: in the end, everything becomes a **document**. Whether cash moves from the bank into petty cash, a supplier invoice arrives or a customer receives a credit memo: technically the same data structure is created every time. Once you've understood how it's built, you'll find your way around the whole FI module quickly.

## The document as the basic unit

An **FI document** is the unit in which SAP stores each individual business transaction in financial accounting. It always consists of two parts:

- The **document header** — general data such as the posting date, document type, company code and currency.
- The **line items** — the actual posting lines, each with an account, a debit or credit amount, and further assignments such as cost centre or profit centre.

One rule always holds: every document must be balanced, total debits = total credits. That's the basic principle of double-entry bookkeeping, and SAP enforces it technically when you post. A document that isn't balanced can't be posted at all.

## Which postings do you enter in SAP FI?

In SAP S/4HANA financial accounting you typically enter these kinds of postings:

- **G/L account postings** — for example a transfer of cash from the bank to petty cash.
- **Customer invoices** — outgoing invoices to customers.
- **Customer credit memos** — credit memos to customers.
- **Vendor invoices** — incoming invoices from suppliers.
- **Vendor credit memos** — credit memos from suppliers.

A simple example makes the principle tangible: if 5,000 EUR is withdrawn from the bank account and put into petty cash, that becomes a G/L posting with two lines: petty cash 5,000 EUR on the debit side, bank 5,000 EUR on the credit side. Debits and credits match, so the document is balanced.

## What is the document type for?

The **document type** is a central control element in every document. It determines:

- Which **number range** the document number is drawn from.
- Which **account types** (G/L, customer, vendor, asset, material) are allowed in the document.
- Whether **document splitting** takes place.
- Whether individual header fields such as reference or header text are mandatory.

Whether an individual field in the line items is visible or mandatory, by contrast, isn't decided by the document type but mainly by the field status group on the G/L account together with the posting key. In practice you rarely have to hunt for the document type by hand: depending on the transaction, SAP proposes a suitable default type, which you can override if needed. For a vendor invoice that's an invoice document type, for a pure G/L posting a G/L document type. So the document type classifies the transaction correctly from the start.

## Posting, parking, holding — three ways to save a document

This is one of the most important concepts in day-to-day work. When you enter a document, you have three options for what should happen to it:

- **Post** — the document is saved for good, gets a fixed document number and flows into every evaluation (balance sheet, P&L, balance list). Reversing it now means posting a reversal.
- **Park** — the document is saved and has a preliminary number, but does *not yet* flow into the balance sheet and P&L. A typical use: a clerk enters it, and a second person approves the final posting (four-eyes principle).
- **Hold** — the document is set aside as a *held document*, often still incomplete. You use this when data is still missing and you want to continue later.

The practical core: only the posted document affects the financials. Parked and held documents are saved, but they don't show up in the balance sheet or P&L. A document is only final once you click "Post"; until then you can change or discard anything.

## What's in the document header?

When you enter a document, you typically fill these header fields:

- **Document date** — for incoming invoices, the invoice date.
- **Posting date** — the date that determines the posting period.
- **Document type** — classifies the transaction (see above).
- **Company code** — the posting organisational unit.
- **Currency** — for example EUR.
- **Text** — a free-form explanatory text.

For vendor or customer invoices, fields such as **supplier** or **customer**, **reference**, **amount** and **tax code** come on top. The line items below then contain the individual accounts with their debit and credit amounts.

## How a document is created — from typing to document number

A typical flow looks like this:

1. **Choose the transaction** — depending on whether you're entering a G/L posting, an incoming or an outgoing invoice.
2. **Fill the header** — document date, posting date, document type, company code, currency.
3. **Enter the line items** — account, debit or credit amount, and further assignments such as cost centre or profit centre.
4. **Simulate** — SAP shows you the finished posting with all automatically generated lines (such as tax or document splitting) *before* you post. So you see the result in advance.
5. **Post** — the document is saved for good and the system assigns a document number.
6. **Confirmation** — SAP reports that the document was saved and shows the document number.

The simulate step is worth its weight in gold day to day: it reveals automatically generated items like the tax line before anything is final. That lets you catch mistakes early, rather than having to reverse them later.

## Tolerance groups: why a posting gets rejected

SAP protects against accidental or oversized postings through so-called **tolerance groups**. For each user, they can set limits, for example:

- a **maximum amount per document**,
- a **maximum amount per line item** in connection with a customer or vendor account,
- a maximum **cash discount percentage** the user may grant,
- a maximum **tolerance for payment differences** (over- or underpayment).

An example: if the limit per document is 500,000 EUR and you try to post 600,000 EUR, SAP rejects it. It feels like a block at first, but it's a built-in safety layer — not a bug, but a deliberate control. A colleague with higher authorisation may be able to post the very same document.

## Who works with document entry day to day

Most of the work falls to the accounting clerks: they enter the ongoing documents, meaning invoices, bank postings and reclassifications. Accounting managers or reviewers come in wherever parked documents need to be released, and they work with higher tolerance limits. The underlying basis, in turn, often comes from the specialist departments, for instance as incoming invoices that are then posted.

For you as a user, document entry is the point where business transactions get translated into figures. Once you've internalised how a document is built and the difference between posting, parking and holding, you'll find your way around SAP FI quickly.

## Common pitfalls

- **Confusing parked with posted.** A parked document looks posted but doesn't affect the financials. If you're missing an amount in the balance sheet, check whether the document was really posted or only parked.
- **Swapping posting date and document date.** The posting date determines the period. Set it wrong and the posting lands in the wrong month.
- **Overlooking a tolerance limit.** If a posting is rejected for no obvious reason, check your own tolerance group before suspecting a system fault.
- **Not simulating.** If you don't simulate before posting, you only see automatically generated items like the tax line afterwards — and may have to reverse.

## What matters most

The document is the central unit of every posting in SAP FI: a **header** with the general data and **line items** with the individual posting lines, which must always balance in debit and credit. The document type classifies the transaction, and when you save you choose between posting, parking and holding — only posting makes the document final and part of the financials. Once you've grasped this structure and these three options, you've got the basics of document entry down.

## Frequently asked questions

### What is the difference between a document header and a line item?

The document header holds the general data that applies to the whole document — such as posting date, document type, company code and currency. The line items are the individual posting lines, each with an account and a debit or credit amount.

### What does it mean to post a document instead of parking it?

A posted document is saved for good, gets a fixed document number and flows into the balance sheet and P&L. A parked document is saved but not yet reflected in the financials — it usually waits for approval.

### Why does SAP sometimes refuse to let me post?

It's often down to a tolerance group, which sets maximum amounts per user. If a posting exceeds the limit, the system rejects it. That's a deliberate control, not an error.

### What is the document type for?

The document type controls things like which number range the document number comes from and which account types are allowed in the document. It classifies the transaction — for example as a G/L posting, a vendor invoice or a customer invoice.
