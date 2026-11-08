---
updated: 2026-11-06
tags:
  - feature
  - review
  - overlay
---

# Reviewing a built site

A comment layer over a built site: pins anchored to blocks of a page, a panel
listing every thread, and an export the reviewer sends back.

It runs over a local preview by default. Shipping it into the published site is
a separate switch, and letting a reader of that site *write* rather than only
read is a third.

## Using it

1. **Include a review overlay** on, then **Build a preview**.
2. **Open the preview**: this starts the local server.
3. Switch to comment mode, click a paragraph. It outlines the block and opens a
   draft box with a priority chooser.
4. Type, send. The comment appears in the review panel.

The panel sorts by time or by priority, filters open from resolved, and steps
through a review one comment at a time with **Resolve and next**. An open pin
shows the block it is about, the comment, a reply box, and the issue it was
filed as, if any.

**Your name** prefills the comment author.

## Pins survive a rebuild

A pin remembers where it was dropped **twice**: in document coordinates, and
as a fraction across the block it landed on. So a rebuild that reflows the page
does not scatter the review.

## Getting the comments back

The reviewer exports; you run **Import review comments** and the review becomes
a note in your vault, in the **Review folder**
(`_vault-publisher/review` by default).

The live comments file in that folder is written continuously by the review
server while it runs, so it is treated separately from a `*.json` you drop
there by hand, never renamed out from under the thing writing it.

### Comments link back to the writing, not the HTML

A publish records which note produced which page, in a page map kept in the
vault beside the review file. So an imported comment points at the note you
need to edit rather than at a built page you cannot.

This also solves a smaller problem: naming a page when four of them are called
`index`.

## Shipping it to the published site

Two toggles, nested, because they are two decisions:

| Setting | What it does |
| --- | --- |
| **Include in the published site** | Puts the overlay on published pages too. Off by default: it carries the bundle to every reader of the site, which is a decision about the site rather than about how you work. |
| **Let readers write comments** | Off, and nested under the above. With it off the published overlay is a *reader*: pins, the panel, import and export, and nothing that writes. |
| **Where to send a review** | An email address or a URL shown to a reader who has comments to return. Typed in rather than borrowed from your GitHub settings, because that address was given for a different purpose. |

> [!important] No vault path reaches a reader
> A published page keys its comments on its own URL and never on the vault path
> behind it, so no folder names go out. The preview overlay *does* carry the
> vault path, which is how an imported comment finds its note, and exactly
> why the published overlay is a different code path rather than the
> same one with a flag set to false.

## Filing from a published site

You cannot. Filing goes through the plugin's own local server, so the **Send**
action exists in a preview opened in a browser and in no published page: a
static host has nothing to file through.

Reviewing a published site therefore means: export the comments, import them,
and file from a preview. See [[Filing comments as issues]].

## Related

- [[Filing comments as issues]]: GitHub, Jira, Asana.
- [[Commands and automation]]: the review commands.
