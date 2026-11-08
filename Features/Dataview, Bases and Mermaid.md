---
updated: 2026-11-05
tags:
  - feature
  - dataview
  - bases
  - mermaid
---

# Dataview, Bases and Mermaid

This is the reason the plugin exists, so it is worth being precise about what
survives and what does not.

## What survives

**Dataview** tables, lists and inline queries publish as whatever they
rendered to. The index is given time to load before the build starts, and
Dataview is held still while each page is photographed. Otherwise a query
that refreshes mid-serialization publishes half a table.

**Bases** views are re-emitted as semantic tables and cards rather than
published as the app's own grid markup. That was not the first approach; it
became necessary. Bases renders a virtualized grid whose layout depends on the
app's live measurements, and publishing it directly produced broken layout and
numeric columns that came out blank. Re-emitting fixed both.

**Mermaid** diagrams serialize as the SVG Mermaid drew. The diagram in
[[Rendering inside Obsidian]] is one.

**Code blocks** keep their syntax highlighting, since that is also something
the app did rather than something in the Markdown.

## What does not survive

Interactivity, across the board. A published page is static HTML with one
stylesheet and one script, and the script does navigation, search and theming,
not Dataview.

So:

- **Bases sorting and view switching are gone.** The table you published is
  the view you were looking at.
- **`dataviewjs` buttons do nothing.** And `dataviewjs` is off by default in
  Dataview's own settings; if you turn it on, be aware its *errors* would
  publish verbatim.
- **Collapsed callouts are static** in whichever state they were rendered.

## Three things to know before you rely on this

> [!warning] A long Bases view can publish short
> Bases builds only the rows it is currently showing. A view of any length
> therefore arrives truncated. The gap is now **stated on the published page**,
> which is the honest minimum, and **Refuse to publish a shortened Bases view**
> turns it back into a hard failure. It is off by default because one long base
> otherwise blocked an entire site.

> [!warning] Mermaid publishes light-themed
> Diagrams serialize with resolved colours from Mermaid's default light theme.
> On a dark site they will look wrong until the diagram is re-rendered or the
> colours rewritten. This is open.

> [!warning] Mermaid needs the vault's consent
> Obsidian 1.14 gates diagram rendering per vault. The plugin detects this and
> reports it rather than bypassing it, so if your diagrams publish empty,
> check that the vault has allowed them.

## Try it

- [[Mermaid and code]]: a diagram and a highlighted code block, so you can
  confirm both arrived.
- [[A base, embedded]]: a Bases view, if your Obsidian has Bases.

Build the preview and compare the page against what you see in Obsidian. That
comparison is the whole test.

## Related

- [[Rendering inside Obsidian]]: why any of this works.
- [[Known limits]]: the full list, including these.
