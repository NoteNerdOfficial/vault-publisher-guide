---
updated: 2026-11-07
tags:
  - example
  - bases
---

# A base, embedded

A Bases view, embedded in a note, published as a semantic table.

> [!note] This one needs Bases
> Bases ships with recent Obsidian versions. If your Obsidian does not have
> it, the embed below will not render and the published page will say so rather
> than publishing a blank space. Everything else in this vault works without
> it.

## The view

`Notes.base` filters this vault down to the notes tagged `#feature` and shows
each one's name, its tags and its `updated` date, so the table below is built
from the same frontmatter [[The note header]] describes.

![[Notes.base]]

## What happened to it on the way out

The app renders Bases as a **virtualized grid** whose layout depends on live
measurements. Published directly, that produced broken layout and numeric
columns that came out blank.

So the build does not publish the grid. It reads the view and **re-emits it**
as its own table, or cards, depending on the view type. That fixed the layout
and recovered the values.

What it cost: sorting and view switching. The table you are reading is the view
as it was when the page was built.

> [!warning] Check the row count
> Bases builds only the rows it is currently showing, so a long view can
> publish short. The published page states the gap when there is one. Turn on
> **Refuse to publish a shortened Bases view** to make it a hard failure
> instead. → [[Known limits]]

## Related

- [[Dataview, Bases and Mermaid]]
- [[Mermaid and code]]
