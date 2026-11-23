---
updated: 2026-11-22
tags:
  - example
  - review
  - prototype
---

# About the review demo

A small shopping-basket prototype drawn inside a phone frame, for trying out
the review overlay on something more like an app than a page. Everything it
does is something a real prototype does: a list that scrolls on its own, a
bottom sheet that slides up, a popup that is built when asked for and thrown
away when answered, and a second screen.

> [!important] Two switches first
> **Settings → Vault Publisher → Publish HTML files as-is**, so the prototype
> is built at all, and **Include a review overlay**. Then **Build a preview**
> and **Open the preview**, and go to `Examples/review-prototype/index.html`.

## What is in the folder

| File | What it is |
| --- | --- |
| `index.html` | The phone frame. The app is shown in an `<iframe>` inside it. |
| `screens/basket.html` | The first screen: the list, the **Choose delivery** sheet and the **Remove** popup. |
| `screens/done.html` | The second screen, reached with **Pay now**. |
| `screens/app.css` | Both screens' styles. |

## Things to try

### One toolbar, not two

The frame page and the screen inside it are both HTML pages, so both get the
overlay. Only the outer one shows it: the screen's overlay sees that it is
inside a reviewed page and stands down. Pins are still dropped on the
screen's own buttons and rows.

### A comment remembers its screen

1. Comment on the **Order placed** heading on the second screen.
2. Tap **Back to the basket**.
3. Open the comment from the review panel. The frame goes back to the second
   screen and the pin is on the heading. The panel names the screen the
   comment belongs to.

### Pins on a scrolling list stay on their row

Comment on **Desk lamp**, then scroll the list. The pin scrolls with the row,
and disappears when the row leaves the list's own window, even though the
page itself never scrolled.

### Pins follow the sheet

1. Tap **Choose delivery** and comment on **Next day**.
2. Tap the list to close the sheet. The pin slides away with it and is
   hidden while the sheet is closed. In the panel, the comment says the
   sheet is closed.
3. Open the comment from the panel. The sheet comes back up, as it was, and
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

## On the published site

With **Leave a review → Include in the published site** on, the same overlay
goes out with the prototype, and a reader can leave comments on it if **Let
readers write comments** is on too. How their comments reach you is the last
choice in that section. → [[Reviewing a built site]]

## Related

- [[Reviewing a built site]]
- [[Publishing a built app]]
- [[About the as-is demo]]: the other as-is example, about which files travel
  with a page.
