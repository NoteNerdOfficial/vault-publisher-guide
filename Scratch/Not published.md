---
updated: 2026-11-07
tags:
  - scratch
---

# This note is not published

If you are reading this on a built site, something is wrong.

`Scratch` is listed under **Exclude folders** in this vault's settings, so this
note is subtracted from the publish scope before anything else happens, even
though the scope is the whole vault and this note is an ordinary note with
ordinary frontmatter.

## How to check

Build the preview and read the build report. It names what it skipped and why,
and this file should be in that list. Then look for it on the site: there
should be no page for it, no entry in the browse tree, and no `scratch` tag
page.

Links to it from published notes degrade safely rather than producing a dead
link, which is what makes a partial publish usable at all.

## Why this folder exists

Because an exclusion that works and an exclusion that silently did nothing look
identical from the outside. The report naming what it left out is the only
difference, which is why it does.

Try it the other way too: remove `Scratch` from **Exclude folders**, rebuild,
and this note appears. Put it back.

## And the thing to remember

Excluded folders are the weakest of the three selectors. A folder you add to
the vault tomorrow is published, and an attachment in here that a *published*
note embeds is still carried out. For anything that must not go out, use the
frontmatter flag instead.

See **Choosing what gets published** in the published vault, which this note
cannot link to with a wikilink without putting a link to an unpublished note on
a published page, which is, itself, the thing worth knowing.
