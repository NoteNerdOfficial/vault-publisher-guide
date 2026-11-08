---
updated: 2026-11-07
tags:
  - reference
  - limits
---

# Known limits

Stated plainly, because every one of these is a thing you would otherwise
discover from a live site.

## Scale is unproven

A clean vault builds 7 notes in about 1,700ms. Seven notes is not five
hundred, and a long publish session may degrade its own environment, which is
why the build watches for that and reports it. This is the open question, and
the next thing to test.

## Interactivity does not survive

Bases sorting and view switching, `dataviewjs` buttons, collapsed callouts:
all static once published. → [[Dataview, Bases and Mermaid]]

## A long Bases view can publish short

Bases renders only the rows it is currently showing, so a long view arrives
truncated. The page states the gap, and **Refuse to publish a shortened Bases
view** turns it into a failure. The guard that compares emitted rows against
the count Bases reports is written but **not yet exercised against a large
base**.

## Mermaid

- **Light-themed.** Diagrams serialize with resolved colours from Mermaid's
  default light theme, so a dark site needs a re-render or a colour rewrite.
- **Needs vault consent.** Obsidian 1.14 gates diagrams per vault. The plugin
  detects this rather than bypassing it.

## `dataviewjs` is off by default

In Dataview's own settings. If you enable it, note that its errors would
publish verbatim.

## Excluded folders do not reach attachments or HTML companions

The exclusion list is applied when notes and `.html` pages are selected. But an
image inside an excluded folder that a **published** note embeds is still
carried, and still published under its vault path at `assets/files/…`. The same
goes for a file an as-is HTML page references.

> [!warning] For anything that must not go out, use the frontmatter flag
> → [[Choosing what gets published]]

## A locked site cannot publish incrementally

Every build mints a fresh salt and a fresh IV per file, so every encrypted file
differs from the one already published and the manifest matches nothing. A
password costs a full upload on every publish, the opposite of what
incremental publishing exists for, and it matters most on exactly the large
sites it was written for.

## A locked site cannot serve a code-split application

An as-is build in a locked site runs from a blob URL, and a module that
`import()`s another chunk resolves that import against its own URL, which a
blob URL does not have. Single-bundle output works.
→ [[Locking a site behind a password]]

## An application that computes a path at runtime still breaks

Publishing a folder whole carries every file, but `fetch('/api/' + id)` is
asking for a server and a static host has none. Nothing here can fix that.

## A Vite source `index.html` is not reported as an empty shell

The warning fires on a framework root element with no `<script>` anywhere, and
Vite's source page *does* have one. It points at `/src/main.tsx`, which is
TypeScript no browser will run. It is still reported, by the rule about
references resolved from the root of the server, but the message is about the
base rather than about the page being unbuildable.

Angular's source `index.html` has no script tag and is caught correctly.
→ [[Publishing a built app]]

## Structural, not bugs

These are consequences of the design rather than things to be fixed:

- **Publishing happens only from a running desktop Obsidian.** No server can
  rebuild the site. → [[Rendering inside Obsidian]]
- **There is no GitHub Actions workflow**, and will not be.
- **Filing an issue works only from a preview.** A static host has nothing to
  file through. → [[Reviewing a built site]]
- **A password is a shared secret**, not access control. No revocation short of
  republishing.
