# Runway Site Development Guidelines

You are not building a finance app. You are helping explain and present a privacy-focused indie app to real people.

## Purpose

This repository contains the website for the Runway app.

The website exists to:
- Explain what Runway does.
- Help users understand the app's privacy-first approach.
- Provide support resources.
- Provide release notes and feature information.
- Encourage downloads and feedback.

The website is not the app itself. Do not add app functionality, business logic, or product behavior here.

The goal of this site is to explain the app to humans.

## Product Context

Runway is a privacy-focused cash flow forecasting app.

It was made by a single indie developer.

The core user question is:

> "Do I have enough cash available to cover my upcoming bills and obligations?"

Runway helps users answer this by forecasting future cash balances based on:
- current account balances,
- known upcoming income,
- recurring bills and obligations.

Runway intentionally avoids becoming a full budgeting platform. Do not describe it as:
- a budgeting app,
- a transaction tracker,
- a spending categorization tool,
- a net worth tracker.

## Content Philosophy

The website should communicate:

- Simplicity: Runway is designed to answer one important question clearly.
- Privacy: User financial data stays on the user's device.
- Transparency: Users should understand how Runway works.
- Trust: The site should feel like a thoughtful independent project, not a faceless financial service.

Avoid:
- exaggerated marketing claims,
- vague "AI-powered finance revolution" language,
- claims that imply bank-level services,
- unnecessary complexity.

Prefer:
- clear explanations,
- plain language,
- concise descriptions,
- honest limitations.

## Privacy Principles

Privacy is a core part of Runway's identity.

Do not add content that suggests:
- user accounts are required,
- financial data is uploaded to servers,
- user information is sold or shared,
- analytics or tracking are present unless explicitly added.

`privacy-policy.md`'s content is not authored here -- it's mirrored from the app repo (`~/cashflow/docs/privacy-policy.md`), which is the source of truth. Use the `sync-privacy-policy` skill to pull an update rather than editing this page's substance directly (formatting/voice fixes that don't change what's disclosed are fine to make here directly).

If privacy behavior changes in the future, update all relevant pages:
- privacy-policy.md
- index.md
- support/help documentation

## Website Structure

Important pages include:

- `index.md` - Main landing page
- `privacy-policy.md` - Privacy policy
- `support-runway.md` - Support development page
- `request-a-feature.md` - Feature feedback
- `get-help.md` - User support

Coming _eventually_:

- `WHATSNEW.md` - User-facing release notes
- `CHANGELOG.md` - Internal development notes

In any case, Keep user-facing content separate from internal development notes.


## Feature Accuracy

Never invent Runway features, capabilities, integrations, or supported platforms.

Before describing a feature:
- verify it exists in the app,
- use existing product documentation,
- avoid promising future functionality unless clearly labeled as planned.


## Writing Style

The website should be:

- Friendly
- Professional
- Approachable
- Written for normal users, not developers

Prefer:
- "Your data stays on your device."
- "See your projected cash balance."
- "Know what bills are coming up."

Avoid:
- technical implementation details unless they help users.


## Em-dashes

I use a lot of em-dashes in my natural writing, but because I'm a human being typing on a physical keyboard I need to use double-hyphens (--) instead. And because I value aesthetics over strict grammar rules, I always surround them with spaces (so, " -- "). Never, ever use a solid em-dash, and never, ever leave it tight against the words on either side.


## Design Guidelines

The website should be clean and simple.

Prioritize:
- readability,
- mobile-friendly layouts,
- clear navigation,
- screenshots and visual examples,
- consistent Runway branding.

Avoid:
- unnecessary animations,
- clutter,
- overly complex layouts,
- generic startup aesthetics.

## Accessibility

Accessibility matters.

Ensure:
- sufficient color contrast,
- readable font sizes,
- meaningful image alt text,
- clear link text,
- mobile-friendly layouts.

## Changes

Before making significant website changes:
- Preserve existing links.
- Avoid breaking GitHub Pages/Jekyll builds.
- Keep Markdown simple when possible.
- Verify that pages render correctly.

When adding new features or sections:
- Consider whether users will understand why it exists.
- Prefer fewer, clearer pages over many small pages.


## Help Test link should expire

Right now, the app is in beta, but when that changes, we need to stop adding people to the beta test.

The "Want to help test Runway? Email me and I'll add you to the beta." link should be removed as soon as the site migrates to a public release.


## A real person made this

I'm an indie developer; I want to lean into that. A real person made this. That person is Bob Larson (Robert Larson, if we're being a little formal). I live in St. Paul, Minnesota. 

If people have questions, comments, feedback, or ideas? -- they can email me at RunwayFinanceApp@gmail.com