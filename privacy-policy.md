---
layout: page
title: Privacy Policy
---

**Effective date: August 7, 2026**

Runway is a cash-flow forecasting app. This policy is short because the honest answer to "what do you do with my data?" is: nothing. We never see it.

## The one-sentence version

Your financial data is stored only on your device, is never transmitted to us or anyone else, and the only way it ever leaves your phone is if you export it yourself.

## What we collect

Nothing. We have nothing to collect because your financial data never comes to us.

- **No account.** There is no sign-up, no email, no password, and no user ID. We have no way to know who you are.
- **No servers of ours.** Runway has no backend. Your balances, bills, income, and settings are stored in a local database on your device and nowhere else.
- **No analytics or tracking.** The app does not collect or use your data for analytics or advertising, contains no crash reporters that phone home, and does not perform telemetry of any kind. The on-device QR-code scanner you use to pair for Snapshot Sharing is powered by Google's ML Kit, decoding the code entirely on your device -- nothing about the scan is ever sent anywhere. The same camera library also bundles a second, Google-Play-Services-connected scanning mode that Runway's code never calls. Separately, the library we use to schedule your local reminders bundles Firebase Cloud Messaging, Google's push-notification service, which Runway never uses -- reminders are scheduled entirely on-device, and nothing is ever registered with Google for it. Neither the unused scanning mode nor Firebase Messaging is configured with a Google project of ours.
- **No bank access.** Runway never connects to your bank. Every number in the app is one you typed in yourself.

## Where your data lives

All of your data is kept in a local database on your device. It is deliberately excluded from Android's cloud backup, so it is never copied into your Google account backup. If you delete the app, the data is gone.

Because of this, **the CSV export is your only backup**. Exports are created only when you choose to do so. You can export everything from Settings → Your data at any time. What you do with that file -- save it, share it, import it on another phone -- is entirely your choice and happens through your device's own share and file features, not through any service of ours.

## Snapshot Sharing

Runway lets you optionally share a read-only snapshot of your runway with someone else -- a spouse or household partner, for example. Nothing is shared unless you set it up yourself, in one of two ways:

- **A one-time share.** Tap "Share a snapshot now" and Runway builds a fresh encrypted file and hands it to your phone's own share sheet -- you choose where that one file goes.
- **An ongoing, automatic share.** Pick a folder once, and choose to have Runway keep a snapshot file there updated automatically -- rewritten every time your data changes, with no further taps, until you turn it off in Settings → Share a snapshot. **If that folder is synced by a cloud service you use (Google Drive, for example), the updated file reaches that service automatically, every time it's rewritten.** Runway itself still doesn't connect to any cloud service to make this work (see below) -- but choosing a cloud-synced folder as your destination means your own cloud provider does, continuously, for as long as this is turned on. Turning it off stops future writes; it doesn't delete a copy already sitting in that folder.
- **Encrypted before it ever leaves your device**, either way -- using a key exchanged once between your device and the recipient's, via a QR code you scan together. Runway has no way to read the file, and neither can anyone else without that key.
- **No server, no account, and no cloud service of ours.** Runway does not operate, and does not connect to, any file-sharing or cloud storage service -- for either sharing method, the destination is always somewhere you chose yourself.
- **What's included:** your current accounts, bills, income, and any What-If scenarios you've saved -- the same information your own runway is built from. There's no selective or redacted option; a shared snapshot includes everything that feeds your own forecast.
- **Revocable, going forward only.** You can re-pair at any time to stop future shares -- one-time or ongoing -- from being readable with an old key. Because there's no server, Runway can't reach into a device or a cloud folder that already has a copy and make it forget -- anything already shared stays viewable there as a frozen copy from that point on.

This is the kind of feature the "What we will never do" section below promised to disclose before it shipped -- here it is.

## Reminders

If you turn on reminders (they are off by default), they are scheduled locally on your device. No notification service, no push servers, and nothing about your bills or balances is sent anywhere to make them work.

## Network connections the app makes

- **Automatic, on launch:** Runway may check for updates to its own application code so that bug fixes can reach you between store releases. This check contacts the update service (operated by Expo, the framework Runway is built on) and involves standard technical request information -- app version, platform, and the like. **Runway does not send any of your financial data as part of these requests.**
- **Only when you tap "Unlock Premium" or "Restore purchase" (Settings → Premium):** Runway contacts Google Play Billing to process the purchase or check whether you've already bought it -- the same way any Google Play in-app purchase works. This never happens automatically or in the background; it only happens when you take that specific action, and no financial data of yours is part of it -- only your Google Play purchase record for this app.

App installs and updates through Google Play are additionally covered by Google's own policies.

## What we will never do

- We will never upload, sync, back up, or otherwise copy your financial data off your device.
- We will never sell or share data we do not have.
- If a future feature ever needs to move any of your data anywhere (for example, an optional bank-sync integration), it will be strictly opt-in, clearly explained before anything happens, and this policy will be updated first.

## Children

Runway does not collect personal information from anyone, including children.

## Changes to this policy

If this policy changes, the new version will be published at the same location as this one, with an updated effective date. Since the app collects nothing, changes would realistically only ever describe new optional features.

## Contact

Questions about this policy: [RunwayFinanceApp@gmail.com](mailto:RunwayFinanceApp@gmail.com)
