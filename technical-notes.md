---
layout: page
title: Technical Notes
---

This page is where I will try to provide specific details about updates to the app.

Most apps summarize an update as "bug fixes and performance improvements." I'd rather tell you what actually changed -- especially anything touching your data, your privacy, or the accuracy of the numbers Runway shows you. If something was found and fixed, it's listed here, not smoothed over.

This isn't a feature tour -- see [the main page](index.md) for what Runway does. This is the record of what changed, release by release, starting with 1.0.0. New entries are added at the top as new versions ship.

---

## 1.0.2 -- September 12, 2026

This release grew out of something I ran into myself: a bill's due date passed before it actually cleared my bank, and Runway had already quietly stopped counting it against my balance -- which briefly made my available cash look higher than it really was. Here's what changed to fix that, and what else came with it.

### New: bills that don't clear on time stay visible

- If a bill, paycheck, or credit card payment's due date passes and you haven't told Runway it was paid or skipped, it now keeps counting against your projected balance instead of quietly assuming it happened. By default it stays held for a few days (configurable in Settings -> Reminders), or you can tell Runway "Still waiting" to hold it indefinitely, or "Dismiss" if you already know it's fine. You can flag "Still waiting" right on the due date itself, before it's even technically overdue -- useful if you're checking that day and it hasn't cleared yet. Dismissing something by mistake is no longer permanent -- Cash Flow History can bring it back. Credit card payments are covered the same way: the first time a payment is found overdue, its estimated amount is locked in so it doesn't keep changing on you, whether the card pays a fixed amount or the full balance each cycle.
- The bills-due reminder now also covers paychecks, and lets you confirm a bill or paycheck right from the reminder itself, the day it's due.

### Data safety

- A full backup now also carries whether you've flagged a bill "still waiting" or dismissed it, and your hold-length setting.
- Restoring a backup now checks the actual values of your saved settings, not just that they're present -- closing two ways a hand-edited or spreadsheet-damaged backup file could previously cause real problems (see below).

### Also fixed

- A corrupted safety-buffer value (most likely from hand-editing or a spreadsheet reformatting a backup file) could make "Safe to spend today" show "$NaN" and silence the below-buffer warning entirely, even for an account that had genuinely dropped below its buffer. Runway now falls back to the default buffer instead of trusting a damaged value.
- A corrupted reminder frequency in an imported backup could hang the app permanently on launch, since reminders rebuild every time the app starts. Damaged values now fall back to their normal setting.

---

## 1.0.1 -- September 5, 2026

The same internal review process that caught issues before 1.0.0 shipped ran again for this release. Here's what's new, and what it found and fixed.

### New: plan around a one-time change

- You can now adjust a single upcoming bill, paycheck, or payment for just that one occurrence -- tap "Adjust…" on the Dashboard or Runway tab. Useful for the one-off: a smaller card payment after an unexpected expense, extra principal on a loan, a signing bonus on one paycheck, a service credit lowering a bill for a month. The recurring amount for every future cycle is untouched -- it resumes automatically the next time around. It also shows up consistently in a What-If scenario, the same way a real paid or skipped bill already does.
- After you confirm a credit card payment or a variable bill (electric, water) as paid, Runway now offers a shortcut to update the number it leaves behind -- the card's new balance, or the bill's amount for next time -- right from that same screen. Runway never changes a balance on its own; this just saves you a trip to go do it yourself.

### Money accuracy

- Fixed a twice-a-month credit card payment being counted twice once you'd already made it. If you marked the first payment paid and then updated the card's balance to reflect that, the app subtracted that same payment again when working out the second one -- which could turn the second payment negative and make your projected balance jump *up* on the day you paid a card. Everything downstream of that payment was wrong for the rest of the forecast.
- Fixed a credit card sitting at a negative balance (say, a refund that landed after you'd already paid the bill) showing up as money coming back into your checking account. The credit still reduces what you owe -- it just no longer looks like income.
- Fixed an already-paid bill or payment silently rewriting its own history. If you updated a card's balance or a bill's amount after marking it paid -- exactly what Runway now invites you to do, above -- the record of what you'd already paid would quietly change to match, instead of staying frozen at what it actually was when you paid it. This showed up on the calendar, the Runway tab, and the home-screen widgets alike; all of them now correctly freeze the figure the moment it's settled.
- Fixed a gap in CSV backup validation: a single corrupted or blank date in an imported file (most likely from opening the export in a spreadsheet and re-saving it) could silently empty your Cash Flow History for every month, with no error or warning that anything had gone wrong. Nothing was ever actually lost -- the underlying data round-tripped correctly the whole time -- but the display broke silently. That kind of row is now rejected at import time with a clear error instead.

### Getting your data in and out

- CSV import (both a full backup and the starter template) now offers a real "Choose file…" option on the installed app, not just pasting the file's contents in by hand.
- Restoring a backup on a new phone already carried your theme, text size, currency, and reminder preferences across -- but they didn't actually take effect until you fully closed and reopened the app. They now apply immediately once the restore finishes.

### Accessibility and readability

- Fixed several places where a larger combined text size (the phone's own accessibility setting plus Runway's own) could crowd content together or clip it: action links running off the edge of the screen in Cash Flow History and on a shared snapshot, button text clipping on the snapshot-import screen and several others, and the Dashboard/Runway calendar's day number, dots, and balance figure overlapping each other on both the in-app calendar and the home-screen widget. The calendar now drops the balance figure at the largest text size to give the date and markers the room they need -- it's still one tap away in that day's own detail view -- and says so on-screen rather than just disappearing silently.
- Columns of dollar figures (account lists, day-by-day balances, Cash Flow History, both account screens) now line their digits up vertically instead of drifting slightly from row to row.

### Also fixed

A representative sample: the amount box shown when marking something paid now rounds to a whole dollar figure instead of occasionally showing something like "$3205.33..."; that same box is bigger and easier to read at larger text sizes; the home-screen List widget now shows what you actually paid when it differs from what was expected, matching the calendar and Runway tab; and a one-time planned adjustment now correctly shows its "(adjusted)" label everywhere it should, including a What-If scenario's results and a shared snapshot.

---

## 1.0.0 -- August 13, 2026

Runway's first public release. Before it went out, every screen, every calculation, and every permission the app requests went through a deliberate internal review -- not just manual testing, but a structured audit built specifically to catch the kind of thing that's easy to miss (a number that's right on one screen and wrong on another, a permission a library asked for that the app never actually uses). Here's what that process, along with regular testing, actually found and fixed before this version shipped.

### Privacy and permissions

- Removed three Android permissions the app had no real use for, all defaults pulled in silently by libraries rather than anything Runway itself needed: microphone access (a side effect of the camera permission used to scan a Snapshot Sharing pairing code), "draw over other apps" (an Expo template default), and fingerprint/biometric hardware access (an unused capability of a notifications library). All three are now explicitly blocked from the shipped app.
- Debug and diagnostic logging is now stripped from release builds entirely. It was never transmitted anywhere and was only readable with direct USB-debugging access to a physical device, but it doesn't belong in a release build regardless -- and one of those messages briefly included a saved What-If scenario's own name, which it no longer does in any build.
- Disclosed two bundled-but-inactive Google components in the privacy policy: Firebase Cloud Messaging (part of the library that schedules local reminders) and Google's ML Kit Play-Services-connected scanning mode (bundled alongside the on-device QR scanner used for Snapshot Sharing pairing). Neither is configured with a project of mine, and neither is ever triggered by anything Runway does -- but a technical inspection of the app would find them present, so the policy now says so.
- Android's automatic cloud backup is disabled specifically for the app's financial data.
- Snapshot Sharing's pairing scanner now checks that a scanned QR code is actually a genuine Runway pairing key of the right size before trusting it, instead of accepting anything shaped like one.
- Premium purchase status now only checks in with Google Play when you actually tap "Unlock Premium" or "Restore purchase" -- not on every app launch.

### Data integrity

- Restoring from a CSV backup and "Start fresh" now complete fully or not at all if interrupted partway through (a phone call, low battery, closing the app) -- never a state where your data is partially wiped.
- Deleting an account gets the same guarantee: it and everything tied to it (linked bills, dangling references from other bills) are removed atomically, or nothing is.
- CSV import now rejects values it can't safely act on -- a malformed date, a corrupted recurring-bill interval -- instead of silently producing a wrong forecast or, in one case I found and fixed before release, freezing the app permanently after your existing data had already been replaced by the import.
- Fixed "Safe to spend today" on the Dashboard: it was computed from your combined balance across every cash account against one global buffer, while every other figure on the same screen (the status headline, the calendar colors, account-specific warnings) is worked out per account. It could show a healthy green number directly beneath a red shortfall warning for the exact same account. It now checks each account against its own buffer, like the rest of the screen.
- Fixed a rounding bug where a twice-a-month credit card set to "pay in full" on both halves could show double the real payment amount in one preview -- the actual forecast and calendar were never affected, only that one summary.
- Fixed a case where a bill could vanish without a trace if its purpose was set in a way that created a second, duplicate payment with no screen to display it on.
- Fixed several cases where deleting or resetting data could leave stale references behind -- an account removed while bills still pointed at it, or a removed account's history records outliving the account itself.

### Accessibility

- Every text color in the app is now checked against the WCAG AA contrast standard -- computed against the actual formula, not judged by eye -- across all four appearance combinations (light/dark, standard/colorblind-friendly). This closed the fourth instance of the same gap found across four separate rounds of testing; the check itself is now automated so a fifth round shouldn't need a fifth audit to catch it.
- Added screen reader support throughout: both home-screen widgets, the app's two largest forms, the calendar's weekday header (previously read letter-by-letter, so Tuesday and Thursday sounded identical), and the calendar's payday/bill-due markers (now distinguished by shape, not just color).
- The OS's "reduce motion" setting is now respected for tab and tutorial transitions, which previously animated regardless.
- Enlarged the tap target on 84 small text links across the app (Update, Edit, Remove, Skip, and similar) that previously responded to taps no larger than the visible text itself.
- Fixed text clipping and overlap when the OS's font-size setting and the app's own text-size setting are both turned up at the same time -- headlines losing words, buttons cut to one letter, fields running off-screen.

### Also fixed

A representative sample, not the complete list: past one-time bills no longer linger in the account list forever; CSV export/import now round-trips paid/skipped status and Cash Flow History's monthly balances correctly; removing your only cash account no longer references an account that doesn't exist; the home-screen widgets now repaint immediately on a theme or currency change instead of waiting up to 30 minutes; and dozens of smaller wording, layout, and edge-case fixes across Accounts, Settings, and the Dashboard.

---

This list isn't exhaustive -- a lot of work goes into creating an app like this, a million small issues pop up and I believe I've caught most of them. I've worked hard to make Runway the best app I can. Every line above corresponds to an actual change, found through either deliberate internal review or regular use. If you find something that isn't behaving the way it's supposed to, [please let me know](get-help.md).
