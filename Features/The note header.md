---
updated: 2026-11-08
pinned: 5
tags:
  - feature
  - frontmatter
  - evergreen
---

# The note header

Three frontmatter keys reach a published page. This note has all three set, so
the header at the top of its published version is built from the block above,
which makes this note its own demonstration.

## The three keys

```yaml
---
updated: 2026-11-04
pinned: true
tags:
  - feature
  - frontmatter
  - evergreen
---
```

### `updated`

Dates the note. The key is whatever the **Date property** setting names,
`updated` by default, and it accepts either `2026-11-04` or
`2026-11-04T18:40`.

A note without it falls back to the file's own modified time, which is why a
synced or bulk-edited vault is better off setting it by hand: one careless
sync and every note was "updated" the same afternoon.

The same date orders **Recently updated** on the front page.

### `tags`

Becomes the row of chips under the title. Inline `#tags` in the body count
too. Each chip links to that tag's page on the site, which lists every
published note carrying it.

### `pinned`

Does not appear in the header at all. It puts the note under **Start here**:
a short list held above the file tree in the left panel, and a section on the
generated front page. The key is whatever the **Start here property** setting
names.

Set it to a number rather than `true` to say where the note goes:

```yaml
pinned: 1     # leads
pinned: 2     # second
pinned: 1.5   # between those two, without renumbering either
```

Numbered notes lead in their numbers, then everything left on `true` follows
in title order. `pinned: 0`, and anything that is neither a number nor `true`,
means not pinned.

Five show at once and the rest sit behind a **Show more** that expands in
place, so pin as many as you like. The panel and the front page run the same
sort, so the two cannot disagree about the order.

> [!note] Why not Obsidian's bookmarks?
> They are reached through an internal API, they hold folders and saved
> searches as well as notes, and they can name notes that are *not* being
> published, which would put a private note's title on a public page. That is
> precisely the leak the privacy scan exists to catch, so the plugin does not
> create it on purpose. See [[Choosing what gets published]].

## What else the header shows

A **Links** figure (how many published notes link here, and how many this
note links out to) appears whenever either is more than zero. It is counted
from the links the build actually *resolved*, so a link to an unpublished note
is not in it.

## What the header leaves out

Everything else in the frontmatter, and **removed rather than hidden**: a
published page carries no trace of the keys it was not asked for.

Add `status: draft` or `client: Acme` to a note and nothing appears anywhere in
the output. This matters more than it looks. A vault that decides what is
public in its frontmatter would otherwise publish that decision, which is
exactly backwards.

## Headings, so there is an outline

A note needs sections for the right-hand **On this page** list to have anything
to follow. Every heading on a published page also gets a stable id and a
**Copy link to this section** control, so a heading is an address you can hand
to someone.

The ids are derived from the heading text and are stable across rebuilds, so a
link you sent last month still lands in the right place.

## Related

- [[Pages the build writes for you]]: where the tags and the pins end up.
- [[Choosing what gets published]]: the frontmatter key that decides
  publication, as opposed to these three, which only decorate.
