---
updated: 2026-11-24
tags:
  - example
  - review
  - prototype
---

# About the prototype demo

A small shopping-basket prototype, embedded in [[See it working]]. It is one
HTML page that changes shape with its width, and it does the things real
prototypes do that make reviewing them hard: a list that scrolls on its own,
delivery options that slide in, and a popup that is built when asked for and
thrown away when answered.

> [!important] One switch first
> **Settings → Vault Publisher → Include comment and edit tools**, to try the
> review steps below. Then **Build a preview**, **Open the preview**, and go
> to [[See it working]]. **Publish HTML files as-is**, which the prototype
> also needs, is already on in this vault.

## What is in the folder

| File | What it is |
| --- | --- |
| `basket.html` | The prototype: the list, the summary, the delivery options and the **Remove** popup. |
| `basket.css` | Its styles, including the three layouts. |
| `About the prototype demo.md` | This note. Published as an ordinary page. |

## Three widths

The embed in [[See it working]] is written `![[prototype/basket.html|375x700]]`,
so it starts at phone width. The buttons above it change the width:

| Button | Width | What the basket does |
| --- | --- | --- |
| **Phone** | 375 px | One column. **Choose delivery** opens a bottom sheet. |
| **Tablet** | 768 px | A summary panel beside the list. Delivery opens as a drawer from the right. |
| **Desktop** | 1280 px | The same, with more room, scaled down to fit the column. The bar says by how much. |
| **Fit** | the column | Whatever width the article is. |

**Open full page** opens the prototype on its own, at your window's width.

## Reviewing it

With the review overlay on, the note has one toolbar, and comments are
dropped on the prototype inside the frame.

### Pins on a scrolling list stay on their row

Comment on **Desk lamp**, then scroll the list. The pin scrolls with the
row, and disappears when the row leaves the list's own window, even though
the page itself never scrolled.

### Pins follow the sheet

1. Tap **Choose delivery** and comment on **Next day**.
2. Tap the list to close it. The pin slides away with the sheet and is
   hidden while it is closed. In the panel, the comment is marked
   "delivery (closed)", named after the sheet's `id`.
3. Open the comment from the panel. The sheet comes back as it was, and
   closing the comment closes it again.

### Reopen a popup

1. Tap **Remove** on any row and comment on **Keep it**.
2. Tap **Keep it**. The prototype removes the popup from the page entirely,
   so there is nothing left to show.
3. Open the comment from the panel. The card offers **Reopen**, which taps
   the **Remove** button you used the first time and brings the popup back.

It is a button, not automatic, because a tap runs the prototype's own code.
Here that only rebuilds the popup, but in another prototype it might change
something.

## Editing it

Use **Open full page** on the embed, then press **E**. Try selecting a row
and pressing **⇧A** for auto layout, or **More → Button** to add a button in
the prototype's own style. Every change is written into `basket.html`, and
**Undo** takes it back. → [[Editing a prototype]]

## On the published site

With **Comments and editing → Include in the published site** on, the overlay goes
out with the site, and readers can leave comments on the prototype too if
**Let readers write comments** is on. → [[Reviewing a built site]]

## Related

- [[See it working]]: where the prototype is embedded.
- [[Editing a prototype]]: changing it from the preview.
- [[Reviewing a built site]]
- [[Publishing a built app]]: embeds, and publishing whole applications.
- [[About the as-is demo]]: which files travel with a page.
