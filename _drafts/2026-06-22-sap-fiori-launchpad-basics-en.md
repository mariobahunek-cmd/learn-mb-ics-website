---
layout: post
lang: en
title: "SAP Fiori Launchpad: the S/4HANA home screen explained"
description: "Tiles, spaces, pages, search and personalization: how the SAP Fiori Launchpad works as the modern home screen for every S/4HANA user — explained in plain language."
slug: sap-fiori-launchpad-basics
permalink: /blog/en/sap-fiori-launchpad-basics/
translation_key: post-fiori-launchpad
date: 2026-07-07
category: "Basics"
keywords: "SAP Fiori Launchpad, SAP Fiori, S/4HANA interface, Fiori tiles, spaces and pages, My Home, personalization, SAP user"
reading_time: 8
sources:
  - label: "SAP Help Portal — SAP Fiori Launchpad (SAP S/4HANA)"
    url: "https://help.sap.com/"
    note: "SAP Fiori / User Experience area — general background on the launchpad. Always check the current state in the Help Portal before relying on it in production."
faq:
  - q: "What is the difference between SAP Fiori and the Fiori Launchpad?"
    a: "SAP Fiori is the overall design and interaction concept of S/4HANA — the style in which the apps look and behave. The Fiori Launchpad is the actual home screen where those apps sit as tiles and from which you open them."
  - q: "Why does my launchpad look different from my colleagues'?"
    a: "Fiori is role-based. Each user only sees the apps that belong to their role. Someone in purchasing gets different tiles than someone in accounting — plus their own personalization, such as pinned apps or a different theme."
  - q: "What is the difference between a space and a page?"
    a: "A space is a large section of the launchpad, usually tied to an area of work, and it behaves like a tab at the top. Inside a space there are one or more pages, where the apps are grouped into sections with headings."
  - q: "Can I customize the Fiori Launchpad myself?"
    a: "Yes. You can pin apps, reorder tiles by drag and drop, create your own sections and switch the theme. This personalization applies only to you and changes nothing for other users."
  - q: "Do I still need to know transaction codes in Fiori?"
    a: "For most work, no. The central search finds apps and business objects by plain text, such as “create purchase order”. Classic transactions can still be launched in S/4HANA, though, and open in an embedded GUI window."
---

Log in to an SAP S/4HANA system and you land in almost the same place every time: the SAP Fiori Launchpad. It's the modern home screen for every user, and it's steadily replacing the classic grey SAP GUI. When I first show this in class, the almost reflexive question is whether Fiori is “a new program”. It isn't: Fiori is the surface that the same S/4HANA shines through, the system that used to look grey and boxy.

## The launchpad in one sentence

The Fiori Launchpad is the central entry point into SAP S/4HANA. Picture it like the home screen on your phone: you see tiles, click one, and the matching app opens. Behind the scenes, the full S/4HANA system runs with all its business processes.

The key idea behind it: the launchpad is **role-based**. It shows you only the apps that belong to your job, not the entire system. That's why your home screen looks different from a colleague's in purchasing or accounting.

## What is SAP Fiori, anyway?

SAP Fiori is the user interface, the user experience, of SAP S/4HANA. Where the old SAP GUI relied on grey menus, transaction codes and densely packed input fields, Fiori looks like a modern web application: tiles on a light background, clear typography, intuitive icons and one consistent search.

SAP built Fiori around five design principles:

- **Role-based** — each user only sees the apps that belong to their role
- **Adaptive** — the interface adjusts to different use cases and devices (desktop, tablet, smartphone)
- **Coherent** — all apps follow the same look and feel and behave as one consistent whole
- **Simple** — clear tasks, few clicks, no overloaded menus
- **Delightful** — the experience should be pleasant and intuitive to use

## The fixed zones of the launchpad

Once you have the launchpad open, you find your way quickly as soon as you know the fixed zones. At the very top sits the header, the shell bar, with the logo, search, notifications and the user menu. Below it lies the main area with the actual apps, organized into spaces and pages. Navigation runs through the menu or the search.

### Apps and tiles

Apps are the individual functions you click in the launchpad. They're presented in two forms:

- **Tiles** — larger, often colored squares or rectangles
- **Links** — compact text links, ideal for rarely used apps

Both lead to the same outcome: they open an app. Tiles are simply more prominent and can display extra information.

### The central search

At the very top of the launchpad sits a search bar. There you search not only for apps but also for business objects — specific purchase orders, customers, materials or employees. The search scans everything system-wide that you're authorized to see.

That's a big advantage over the classic GUI: you no longer have to memorize transaction codes. Type “create purchase order” or “customer 12345” and the system takes you straight there.

### Notifications and the user menu

At the top right of the header you'll find a bell icon, the notification center. Approval requests, tasks, reminders and workflow steps land here. With one click you jump from a notification straight into the relevant app.

Next to it sits your user menu, recognizable by your profile picture or your initials. There you'll find personal settings (language, time zone, theme), personalization options, favorites and the way to log off.

## What kinds of tiles are there?

Not every tile is the same. SAP distinguishes three main types:

- **Static tile** — shows only a title and an icon. A click opens the app; nothing else happens.
- **Dynamic tile** — shows a live figure right on the tile, for example “Open purchase orders: 47”. You grasp your situation at a glance without opening the app.
- **News tile** — shows current news or announcements, often as rotating content. Handy for internal communication or news feeds.

Dynamic tiles save time: you can tell from the launchpad itself whether something needs your attention. That's exactly why they're popular in modern S/4HANA systems.

## Spaces and pages — how the apps are organized

In earlier Fiori versions, apps were organized into **groups**. Over time, SAP modernized the system. Today you work with **spaces** and **pages**.

### Spaces

A space is its own section of the launchpad, tied to a role or an area of work. Think of spaces as tabs across the top: for example “Purchasing”, “Warehouse” or “My Workplace”. If you work in purchasing, you click the purchasing space and see only the apps relevant there.

### Pages

Within a space there are one or more pages. A page is a further breakdown of the content: the apps are grouped into sections with headings — for example “Purchase orders”, “Requests” or “Supplier master data”.

### My Home

With the **SAP Fiori Horizon** theme, **My Home** was added, a personal home page you can shape yourself. It typically brings together several sections:

- **To-Dos** — tasks and situations in one place
- **Pages** — jump to them directly, without going through the spaces
- **Apps** — recently or frequently used apps, plus favorites
- **Insights** — analytical cards and key figures

That lets you build your own quick access, independent of the spaces set up for you.

## Personalization: making the launchpad your own

One of Fiori's strengths is personalization. You don't have to accept the setup as it comes. Typically you can:

- **Pin apps** — place important apps on “My Home” or your own pages
- **Reorder** — move tiles by drag and drop
- **Create or rename sections** — build your own structure
- **Switch theme** — change how the launchpad looks

### Themes — choosing the look

SAP ships several themes with S/4HANA. The key ones for current systems:

- **SAP Quartz Light** — a light theme, long the standard in S/4HANA
- **SAP Quartz Dark** — a dark theme, easier on the eyes during long working days
- **SAP Fiori Horizon** — the newest theme, with signature design and a stronger focus on the important parts of the screen

You switch the theme in the user menu under “Settings” or “Appearance”.

## What app types are there?

Not every app does the same thing. SAP distinguishes three main types:

- **Transactional apps** — where you carry out business transactions, such as creating a purchase order, creating a customer or releasing an invoice. This is the operational work.
- **Analytical apps** — apps for evaluations, key figures and dashboards. They show you trends and reports, such as revenue by region or open items.
- **Fact sheet apps** — overview apps for a specific business object. You see all the relevant information about a customer, a purchase order or a material at a glance, and navigate onward from there.

A typical working day mixes all three: in the morning you check the state of play in an analytical app, jump from there into a fact sheet app for a specific case, and finally open a transactional app to change or release something.

## Fiori versus the classic SAP GUI

Many companies still run both worlds in parallel. The key differences:

| Aspect | SAP Fiori | SAP GUI |
| --- | --- | --- |
| Look | web-based, modern, colorful | desktop-based, grey, dense |
| Operation | search, tiles, clicks | transaction codes and menu paths |
| Devices | desktop, tablet, smartphone | installed on the PC |
| Audience | users with clearly scoped tasks | power users with many special transactions |
| Direction | where SAP invests | kept for certain functions |

From the Fiori Launchpad, by the way, you can still call classic GUI transactions in S/4HANA — they then open in an embedded GUI window. So every function comes in through the same door.

## Common pitfalls

It's nearly always the same places where people get stuck: launchpad, tile and app blur together, and anyone who spent years in the old SAP GUI keeps looking for the familiar menus where tiles now sit.

- **Mixing up the terms.** Space, page, section, tile, app — confusing these makes conversations harder than they need to be. Match each term to its function and the launchpad quickly falls into place.
- **Confusing personalization with authorization.** If an app is missing, pinning won't help — it simply isn't part of your role. Personalization only rearranges what you're already allowed to see.
- **Hunting for transaction codes instead of using search.** The central search finds apps and business objects by plain text. Typing codes anyway just makes the work harder.

## What it comes down to

The SAP Fiori Launchpad is the **role-based home screen** of S/4HANA: a set of tiles that shows you exactly the apps that fit your job. You navigate through spaces and pages, find everything via the central search, and set up your own workspace with personalization and themes. Once you can tell the building blocks apart, tile, space, page and app type, you move around S/4HANA with confidence.

## Frequently asked questions

### What is the difference between SAP Fiori and the Fiori Launchpad?

SAP Fiori is the overall design and interaction concept of S/4HANA — the style in which the apps look and behave. The Fiori Launchpad is the actual home screen where those apps sit as tiles and from which you open them.

### Why does my launchpad look different from my colleagues'?

Fiori is role-based. Each user only sees the apps that belong to their role. Someone in purchasing gets different tiles than someone in accounting — plus their own personalization, such as pinned apps or a different theme.

### What is the difference between a space and a page?

A space is a large section of the launchpad, usually tied to an area of work, and it behaves like a tab at the top. Inside a space there are one or more pages, where the apps are grouped into sections with headings.

### Can I customize the Fiori Launchpad myself?

Yes. You can pin apps, reorder tiles by drag and drop, create your own sections and switch the theme. This personalization applies only to you and changes nothing for other users.

### Do I still need to know transaction codes in Fiori?

For most work, no. The central search finds apps and business objects by plain text, such as “create purchase order”. Classic transactions can still be launched in S/4HANA, though, and open in an embedded GUI window.
