---
layout: page
title: Technical Notes
---

This page is where we get specific.

Most apps summarize an update as "bug fixes and performance improvements." We'd rather tell you what actually changed -- especially anything touching your data, your privacy, or the accuracy of the numbers Runway shows you. If something was found and fixed, it's listed here, not smoothed over.

This isn't a feature tour -- see [the main page](index.md) for what Runway does. This is the record of what changed, release by release, starting with 1.0.0. New entries are added at the top as new versions ship.

---

## 1.0.0 -- August 13, 2026

Runway's first public release. Before it went out, every screen, every calculation, and every permission the app requests went through a deliberate internal review -- not just manual testing, but a structured audit built specifically to catch the kind of thing that's easy to miss (a number that's right on one screen and wrong on another, a permission a library asked for that the app never actually uses). Here's what that process, along with regular testing, actually found and fixed before this version shipped.

### Privacy and permissions

- Removed three Android permissions the app had no real use for, all defaults pulled in silently by libraries rather than anything Runway itself needed: microphone access (a side effect of the camera permission used to scan a Snapshot Sharing pairing code), "draw over other apps" (an Expo template default), and fingerprint/biometric hardware access (an unused capability of a notifications library). All three are now explicitly blocked from the shipped app.
- Debug and diagnostic logging is now stripped from release builds entirely. It was never transmitted anywhere and was only readable with direct USB-debugging access to a physical device, but it doesn't belong in a release build regardless -- and one of those messages briefly included a saved What-If scenario's own name, which it no longer does in any build.
- Disclosed two bundled-but-inactive Google components in the privacy policy: Firebase Cloud Messaging (part of the library that schedules local reminders) and Google's ML Kit Play-Services-connected scanning mode (bundled alongside the on-device QR scanner used for Snapshot Sharing pairing). Neither is configured with a project of ours, and neither is ever triggered by anything Runway does -- but a technical inspection of the app would find them present, so the policy now says so.
- Android's automatic cloud backup is disabled specifically for the app's financial data.
- Snapshot Sharing's pairing scanner now checks that a scanned QR code is actually a genuine Runway pairing key of the right size before trusting it, instead of accepting anything shaped like one.
- Premium purchase status now only checks in with Google Play when you actually tap "Unlock Premium" or "Restore purchase" -- not on every app launch.

### Data integrity

- Restoring from a CSV backup and "Start fresh" now complete fully or not at all if interrupted partway through (a phone call, low battery, closing the app) -- never a state where your data is partially wiped.
- Deleting an account gets the same guarantee: it and everything tied to it (linked bills, dangling references from other bills) are removed atomically, or nothing is.
- CSV import now rejects values it can't safely act on -- a malformed date, a corrupted recurring-bill interval -- instead of silently producing a wrong forecast or, in one case we found and fixed before release, freezing the app permanently after your existing data had already been replaced by the import.
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

This list isn't exhaustive -- it's real. Every line above corresponds to an actual change, found through either deliberate internal review or regular use, not a category we thought we should mention. If you find something that isn't behaving the way it's described here, [we want to know](get-help.md).
