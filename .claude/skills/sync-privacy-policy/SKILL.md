---
name: sync-privacy-policy
description: Sync Runway's privacy policy from the app repo (~/cashflow/docs/privacy-policy.md, the source of truth) to the public website repo (~/runway-site/privacy-policy.md), adapting it for Jekyll, and check sibling website pages for privacy claims that are now stale. Use when docs/privacy-policy.md changes in the app repo, when asked to publish/sync the privacy policy to the website, or when the site's privacy policy looks out of date.
---

# Sync the privacy policy to the website

`~/cashflow/docs/privacy-policy.md` is the source of truth. `~/runway-site/privacy-policy.md`
is the public-facing copy, rendered by Jekyll/GitHub Pages. They drift because they're edited
independently in two different repos -- this skill is the repeatable process for bringing the
site back in sync, not just a copy-paste.

Both repos are local, in the same WSL environment, at fixed paths (`~/cashflow`, `~/runway-site`)
-- this works regardless of which repo the current session's working directory is in.

## Steps

1. **Diff before touching anything.** Read both files and understand exactly what changed in
   the app repo's version since the site was last synced -- don't blindly overwrite; know what
   you're porting and why.

2. **Port the content, with two structural adaptations** (these are the only two -- otherwise
   port the app repo's wording verbatim, it's the canonical text):
   - Keep the site's Jekyll front matter (`layout: page`, `title: Privacy Policy`) at the top --
     the app repo's copy doesn't have this, don't drop it.
   - The site's own convention is a clickable contact link:
     `[RunwayFinanceApp@gmail.com](mailto:RunwayFinanceApp@gmail.com)` -- the app repo's copy
     is plain text. Convert it; don't port the plain-text version.
   - Carry the effective date over exactly as written in the app repo -- it's the authoritative
     version.

3. **Check sibling pages for now-stale privacy claims.** This is the part that's easy to skip
   and is exactly why this is a skill and not just a copy command. `~/runway-site/AGENTS.md`
   already states the rule directly (see its "Privacy Principles" section: *"If privacy behavior
   changes in the future, update all relevant pages: privacy-policy.md, index.md, support/help
   documentation"*) -- follow that rule, don't duplicate it here. At minimum, read:
   - `index.md` -- has made blanket privacy claims before (e.g. "No cloud sync." as a flat
     feature bullet) that don't account for opt-in features that *can* involve a user's own
     cloud storage (e.g. Snapshot Sharing's auto-share-to-a-folder option). The fix in that case
     wasn't to delete the claim -- it was to make it accurate: "No cloud sync **required**."
     Same principle applies to any future page/claim: state what's true (nothing forced,
     nothing automatic, nothing without the user choosing it) without overclaiming that
     no optional path exists at all.
   - `about-dev.md` -- same kind of narrative-voice claims, same fix pattern if needed.
   - `support-runway.md`, `get-help.md` -- quick check each time; haven't needed changes yet,
     but a future feature might touch them.

4. **Follow the site's own voice rules while editing anything** (`~/runway-site/AGENTS.md`):
   double-hyphens with spaces on both sides (` -- `) for em-dashes, never a solid em-dash;
   plain language over technical implementation detail; no exaggerated claims.

5. **Report what changed and flag judgment calls.** The front-matter/mailto-link adaptations
   are mechanical -- don't bother mentioning them. Any wording change to a sibling page (step 3)
   is a judgment call, not a mechanical port -- call it out explicitly and explain the
   reasoning, the same way you'd flag a finding in a review, so the user can weigh in on the
   exact phrasing rather than discover it in a diff later.

6. **Never commit automatically**, in either repo, unless explicitly asked. Leave the changes
   staged/unstaged for review, same as any other change.
