---
layout: post
lang: en
title: "Accounts Receivable in SAP S/4HANA explained"
description: "Customer master, invoices, incoming payments, open-item management, dunning and the link to the general ledger: how Accounts Receivable works in SAP S/4HANA."
slug: accounts-receivable-s4hana
permalink: /blog/en/accounts-receivable-s4hana/
translation_key: post-accounts-receivable
date: 2026-07-08
category: "Finance"
keywords: "SAP Accounts Receivable, FI-AR, customer master, business partner, customer invoice, incoming payment, open items, dunning, reconciliation account, S/4HANA Finance"
reading_time: 9
sources:
  - label: "SAP Help Portal — Accounts Receivable (SAP S/4HANA Finance)"
    url: "https://help.sap.com/"
    note: "Finance / Accounts Receivable area — general background. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is Accounts Receivable in SAP?"
    a: "Accounts Receivable (FI-AR) is the sub-ledger that manages all amounts customers owe you. Every transaction with a customer — invoice, credit memo, incoming payment, dunning notice — is posted here and mirrored in the general ledger through a reconciliation account."
  - q: "How is a customer created in SAP S/4HANA?"
    a: "A customer is no longer created as a standalone object but as a business partner with the role “FI customer”. The data splits into general information at client level (address, bank details) and company-specific information at company-code level (account management, payment data, dunning data)."
  - q: "What is a reconciliation account?"
    a: "A reconciliation account is a general-ledger account that automatically receives a matching posting for every entry in the customer sub-ledger. This keeps the total of all customer accounts always equal to the balance of the reconciliation account — the basis for a consistent balance sheet."
  - q: "How does the dunning program work in SAP?"
    a: "The dunning program selects overdue open items, determines the dunning level per account and generates the matching notices. The flow has four steps: maintain parameters, schedule the dunning run, edit the dunning proposal and start the printout."
  - q: "What is an open item in Accounts Receivable?"
    a: "An open item is a posted receivable that has not yet been paid. When the payment arrives, the incoming payment is cleared against the invoice and the item counts as settled. Only unpaid open items are considered in a dunning run."
---

An invoice goes out, the money comes in a few weeks later, the item is cleared, and whoever pays late gets a reminder. Anyone working in accounting with SAP S/4HANA runs through this cycle almost every day. Accounts Receivable is where all of it comes together, and its structure turns out to be surprisingly straightforward once you separate the building blocks that carry it.

## The sub-ledger for customer receivables

Accounts Receivable (**FI-AR**) is the sub-ledger in SAP financial accounting that manages everything your customers owe you. In SAP, a customer is called a **customer account** in the ledger sense, and every transaction with one, whether an invoice, credit memo, incoming payment or dunning notice, is recorded in Accounts Receivable and mirrored in the general ledger through a **reconciliation account**.

The key idea behind it: the sub-ledger keeps the detail customer by customer, and the general ledger keeps the total. The reconciliation account keeps both in step automatically, so the balance sheet is consistent at all times, with no one having to reconcile by hand.

## What does an accountant do in Accounts Receivable?

The daily work revolves around a small set of recurring tasks:

- **Maintain customer master data** — address, payment terms, dunning procedure
- **Post customer invoices** — this is where the receivable is created
- **Enter credit memos** — for example after complaints or returns
- **Record incoming payments** and clear open items
- **Send dunning notices** for overdue receivables
- **Handle special cases** such as down payments, guarantees or value adjustments

However varied these sound, three building blocks keep coming back at the core: the **master record** (who is the customer?), the **document** (what was posted?) and the **dunning notice** (how do I collect what's overdue?). Keep those three apart and you have Accounts Receivable under control.

## The customer in the business partner concept

In SAP S/4HANA, a customer is no longer created as a standalone object but as a **business partner** with the role “FI customer”. This unification arrived with S/4HANA: previously there were separate worlds for customer, vendor (supplier) and business partner. Today the business partner is the central object, and one person or company can carry several roles, for example customer and supplier at the same time.

The fields of a customer master record split across two levels:

### Client level — the general data

**Client level** holds the details that apply across the whole organization, regardless of which legal entity bills the customer:

- **Address** — street, postal code, city, country
- **Tax data**
- **Payment transactions**
- **Bank details** — bank IDs with IBAN

### Company-code level — the company-specific data

A **company code** is the smallest independent legal unit in SAP for which a complete set of accounts is kept, in practice a legal entity that produces its own balance sheet. Company-code level holds the details that apply only to that one entity. These cover account management, where the reconciliation account sits, the payment transactions for that entity, and correspondence, under which the dunning data sits.

**Practical rule:** the entry at company-code level takes precedence over the entry at client level. If bank details are maintained at both levels, the company-code entry wins. Bank master records themselves, by the way, are created at client level and can then be assigned to any customer or supplier — which avoids maintaining the same data twice.

## How is a customer invoice posted?

Like every posting in financial accounting, a customer invoice consists of a **document header** (date, company code, document type) and **line items** (the individual lines). The **document type** controls the number range and the account types allowed. Accounts Receivable uses its own document types, for example one for customer invoices, one for credit memos and one for incoming payments. The system proposes the right type automatically, depending on which app you are using.

An illustrative example: you post an invoice of **220,000 €** to a customer. The invoice contains 200,000 € of goods value plus 20,000 € of output tax (10 % here). That produces:

| Account | Debit | Credit |
| --- | --- | --- |
| Receivables (customer) | 220,000 € | |
| Sales revenue | | 200,000 € |
| Output tax | | 20,000 € |

The receivable from the customer sits on the **debit** side (they owe you money); revenue and tax sit on the **credit** side. Before you post for good, you can **simulate** the entry: SAP shows you the finished result, including the automatically generated tax line, before anything is committed. Only when you post does the system assign a document number.

## How are incoming payments and open items handled?

As soon as an invoice is posted, the receivable becomes an **open item**, a posted receivable that has not yet been paid. When the money arrives, the incoming payment is cleared against the matching invoice. The open item is then settled and no longer appears in any dunning notice.

This **open-item management** is the heart of Accounts Receivable: for each customer you can see at a glance which invoices are still open and which are already cleared. Payments can be assigned manually or, in high volumes, processed through the automatic **payment run**. In a payment run, the system posts, clears open items and feeds the print programs with the data they need. For incoming payments it can, for example, collect by SEPA direct debit, provided a valid direct-debit mandate from the customer is on file.

## When a partner is both customer and supplier

In practice a business partner is sometimes both at once: your customer and your supplier (vendor). If the link is maintained in both master records, the payment run can **offset** the open items of the two accounts.

An illustrative example: you owe the partner 5,000 € (as a supplier) and they owe you 8,000 € (as a customer). Instead of moving both amounts separately, the payment run nets them — you transfer only the 3,000 € difference. That saves payment traffic and makes the relationship easier to read.

## How does the dunning program work?

If a customer doesn't pay by the due date, the question of a reminder arises. The first one can be a friendly nudge; if payment still doesn't come, the tone sharpens. The **dunning program** handles this automatically: it selects overdue open items, determines the **dunning level** per account (how often you have already dunned) and generates the matching notice.

The flow has four steps:

1. **Maintain parameters** — you define how the run works. Parameters from an earlier run can be copied.
2. **Schedule the dunning run** — the system determines accounts, items, dunning levels and everything needed, and saves the result in a **dunning proposal**.
3. **Edit the dunning proposal** — you can change, delete or rebuild the proposal until the result fits.
4. **Start the printout** — the notices are printed or emailed, and the dunning data in master records and documents is updated in one step.

One quirk: even a supplier can be dunned, namely when a credit memo means they exceptionally owe you something.

### The dunning fields in the master record

The main control fields for the dunning program sit in the customer master record on the **Correspondence** tab:

- **Dunning procedure** — a predefined scheme that sets how dunning happens (for example four levels at 14-day intervals)
- **Dunning block** — temporarily excludes a customer from dunning
- **Last dunned** — the date of the last notice the account was included in
- **Dunning level** — the highest level reached; the program sets it automatically
- **Clerk** — whose name appears on the dunning letter

Worth knowing: through the **language** stored in the master record, a notice can be produced in the customer's language, provided a form exists in that language. And if an open item carries a collection method such as direct debit, dunning is usually skipped — the system will collect the money itself anyway.

This control works not only per customer but also **per document**: to take a single invoice out of the dunning run temporarily, you set the dunning block on that document alone, without blocking the whole customer.

## How is Accounts Receivable linked to the general ledger?

This is probably the most important concept in Accounts Receivable: **every posting in the customer sub-ledger is automatically mirrored in the general ledger** — on a special general-ledger account declared as a **reconciliation account**.

Post an invoice of 220,000 € to a customer, and a matching posting of the same amount appears at the same time on the general-ledger account “Trade receivables” — with no manual effort. Which reconciliation account applies is stored in the customer master record (company-code level).

The effect: the **total of all customer accounts** is always equal to the balance of the corresponding reconciliation account in the general ledger. So you can read the overall receivable from the reconciliation account and, in the sub-ledger, see at any time which customers make it up. A reconciliation account, by the way, can't be posted to directly — it only ever moves through the sub-ledger.

## Special G/L transactions — the second layer

Not every transaction with a customer is an ordinary receivable. **Special G/L transactions** are business events tied to the customer but shown separately:

- **Down payments** you receive or grant
- **Guarantees**
- **Down-payment requests**
- **Value adjustments** on doubtful receivables

They run through separate **special G/L accounts** and are reported apart — so a down payment received isn't confused with an open receivable. That keeps it clearly visible what is genuine credit and what is still an outstanding receivable.

## The bottom line

Accounts Receivable is the sub-ledger for all customer receivables. It rests on three building blocks: the **master record** (the customer as a business partner), the **document** (invoice, credit memo, incoming payment) and the **dunning notice** (collecting overdue amounts automatically). The payment run clears open items, the dunning program chases late payers, and the **reconciliation account** keeps the sub-ledger and general ledger in step at all times. Keep those building blocks apart and you'll understand the receivables side of an S/4HANA system quickly and with confidence.

## Frequently asked questions

### What is Accounts Receivable in SAP?

Accounts Receivable (FI-AR) is the sub-ledger that manages all amounts customers owe you. Every transaction with a customer — invoice, credit memo, incoming payment, dunning notice — is posted here and mirrored in the general ledger through a reconciliation account.

### How is a customer created in SAP S/4HANA?

A customer is no longer created as a standalone object but as a business partner with the role “FI customer”. The data splits into general information at client level (address, bank details) and company-specific information at company-code level (account management, payment data, dunning data).

### What is a reconciliation account?

A reconciliation account is a general-ledger account that automatically receives a matching posting for every entry in the customer sub-ledger. This keeps the total of all customer accounts always equal to the balance of the reconciliation account — the basis for a consistent balance sheet.

### How does the dunning program work in SAP?

The dunning program selects overdue open items, determines the dunning level per account and generates the matching notices. The flow has four steps: maintain parameters, schedule the dunning run, edit the dunning proposal and start the printout.

### What is an open item in Accounts Receivable?

An open item is a posted receivable that has not yet been paid. When the payment arrives, the incoming payment is cleared against the invoice and the item counts as settled. Only unpaid open items are considered in a dunning run.
