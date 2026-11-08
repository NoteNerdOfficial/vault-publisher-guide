---
updated: 2026-11-08
tags:
  - feature
  - navigation
  - site
---

# Pages the build writes for you

A note becomes a page. But most of what is on the screen was written by the
build rather than by you, and none of it needs configuring.

## The front page

If one of your notes should be the homepage, say so under **Homepage** and
that note is published *at* `index.html` rather than at its own URL, so every
link to it, from wikilinks to backlinks to the tree to the graph, points at
the front page rather than at a second copy of it.

Leave it blank and the build looks for `README.md`, then `index.md`, then
`Home.md`, among the notes being published. Failing all three it writes an
overview of its own, carrying:

- the note count and the tag count
- **Start here**, from your pinned notes, in the order you numbered them
- **Most linked**, ordered by how much of the vault points at each note
- **Recently updated**, by the date property
- **Tags**, as a cloud
- **Browse by folder**

> [!example] This vault
> `Start here.md` is the homepage, set explicitly. Build the preview and it is
> what opens, at `index.html`, with no second copy of it anywhere.

## A page per tag

Every tag in the published set gets its own page listing the notes that carry
it, plus a tag index. The chips in a note's header link to them.

## The browse page

The vault's folder structure, as a tree, for a reader who would rather look
around than search.

## On every note page

**Across the top.** A command bar with search. **Search or jump to…** covers
every published note, and the drop-down offers **Recently updated** before you
have typed anything.

**Down the left.** **Start here** above the vault tree. Your pinned notes sit
at the top of the panel and stay there while the tree scrolls underneath, five
at a time with a **Show more** for the rest. They are not in the search
drop-down as well: one list in two places is one too many, and the drop-down
copy was the one that disappeared the moment you typed. See
[[The note header]] for the key and its ordering.

**Down the right rail**:

| Section | What it is |
| --- | --- |
| **On this page** | The note's outline, from its headings. |
| **About this note** | Word count, reading time, section count, and the date. |
| **Linked from** | Every published note that links here. |
| **Related** | What the note is *near*: notes that share links with it rather than linking to it directly. |
| **Local graph** | The neighbourhood, laid out at build time and emitted as an SVG. No graph library ships to the reader. |

**A Read / Markdown switch.** Markdown mode shows the note's own text, minus
what the rendering hides. It is not a developer's curiosity: the whole promise
of the project is that the vault is the source and the site is a rendering of
it, and a reader who wants to quote a passage or lift a table is better served
by text than by a selection dragged out of styled HTML.

A note has source behind it, so the switch is there. The browse page, the tag
pages and the generated homepage do not, so it is not.

**A theme toggle.** Light and dark are both built, and a reader's choice is
remembered from page to page. Which one a first-time visitor lands in is
**Settings → Appearance → Opens in**, their own system setting by default.
See [[Themes and your own CSS]].

## Links that go nowhere

Wikilinks become relative URLs. A link to a note that is *not* being published
degrades safely rather than producing a dead link. It stays readable as text.
This is what makes a partial publish usable: you can publish a third of a
vault whose notes all link to each other.

## Attachments

The files a page points at are carried and their references rewritten:
images, and for an as-is page the scripts and stylesheets too. See
[[Publishing a built app]].

## Related

- [[The note header]]: the parts of a page you do control.
- [[Themes and your own CSS]]: what all of this looks like.
- [[Known limits]]: excluded folders and attachments.
