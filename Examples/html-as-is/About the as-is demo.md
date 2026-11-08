---
updated: 2026-11-05
tags:
  - example
  - html
---

# About the as-is demo

This folder is a hand-written web page, published byte for byte. It is an
ordinary note explaining a folder of files that is *not* a note. Read it
first.

> [!important] It will not publish until you turn the toggle on
> **Settings → Vault Publisher → Publish HTML files as-is**. It is off by
> default for a good reason: vaults are full of HTML nobody wrote as a web
> page, and turning this on silently would publish all of it.

## What is in the folder

| File | Why it gets published |
| --- | --- |
| `index.html` | It is an `.html` file in scope, and the toggle is on. |
| `styles.css` | `index.html` names it in a `<link>`. |
| `art/panel.svg` | `index.html` names it in an `<img>`. |
| `art/texture.svg` | **Nothing in the page names it.** `styles.css` does, as a `background-image`. |
| `About the as-is demo.md` | This note. Published as a rendered page, like any other note. |

That fourth row is the point of the demo. A reference inside a stylesheet is
resolved **against the stylesheet** rather than against the page that linked to
it, because that is what a browser does. Get that wrong and the texture is
missing with nothing to say why.

The same applies to a `@font-face` src and an `@import`.

## Keep the folder together

The feature is that a page and the files it references stay next to each other.
Move `art/` and the page is published with a reference to a file that is not
there, which is reported, with the file that made the reference, but is still
a page with a hole in it.

## What the page does not get

No stylesheet of the plugin's, no script of the plugin's, no command bar, no
vault tree, no outline rail, no theme toggle. Nothing rendered it, so there is
nothing to decorate. It lands at its own path with its own markup.

Compare it against this note, which is published next to it and gets all of
that.

## Where it lands

At its vault path: `/Examples/html-as-is/index.html`.

For a built application you would usually want it somewhere better, which is
what **Publish folders whole** and its **Publish at** field are for, including
sending it to `/` and making it the front door of the site.

→ [[Publishing a built app]]

## Related

- [[Publishing a built app]]: the whole feature, including whole folders.
- [[Choosing what gets published]]: the scope still decides whether these
  files are candidates at all.
