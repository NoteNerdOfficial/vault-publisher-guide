---
updated: 2026-11-24
pinned: 1
tags:
  - guide
  - start
---

# Vault Publisher, documented in a vault it can publish

This vault is the documentation for the **Vault Publisher** plugin, and it is
also a working example of the plugin's output. Every note here is written to
be published: the frontmatter is filled in, the folders are arranged the way
the settings expect, and one folder is deliberately left out so you can watch
the exclusion happen.

So there are two ways to read it. You can read it here in Obsidian, or you can
build it into a site and read that, which is the only way to see what the
pages this plugin writes actually look like.

> [!tip] Read the site, not just the vault
> Open **Settings → Vault Publisher → Build a preview**, then **Open the
> preview**. Everything described in these notes is on the screen in front of
> you within a minute, including the parts no note wrote: the front page, the
> tag pages, the browse tree and the rail down the right of each page.

## What the plugin does

It renders every note through Obsidian's own renderer, waits for the slow
asynchronous parts to settle, serializes the result, and assembles the output
into a static website: one stylesheet, one script, light and dark both built.
Then it commits that site to a GitHub repository through the Git Data API and
points GitHub Pages at the branch.

It renders inside the app, rather than converting Markdown the way every
other publisher does, because Dataview, Datacore, Bases and Mermaid output
only exists inside a running Obsidian. See [[Rendering inside Obsidian]].
That one decision explains most of the design, and most of the limits.

## Start here

1. [[Install and first build]]: getting from a fresh vault to a site you can
   look at, without touching GitHub.
2. [[Choosing what gets published]]: the three selectors, which one fails
   safe, and the scan that catches a private note leaking through a query.
3. [[Publishing to GitHub Pages]]: the token, the repository, the branch, and
   what gets uploaded on the second publish.

## Every feature

**Building the site**

- [[Rendering inside Obsidian]]: the renderer, the settle logic, and knowing
  when a page is finished.
- [[Choosing what gets published]]: scope, excluded folders, the frontmatter
  flag, and the four rules that apply before any of them.
- [[The note header]]: the three frontmatter keys a page's header is built
  from, and everything the page leaves out.
- [[Pages the build writes for you]]: the front page, tag pages, the browse
  tree, backlinks, the outline and the local graph.
- [[Dataview, Bases and Mermaid]]: what survives the trip, and what stops
  being interactive.

**Making it yours**

- [[Themes and your own CSS]]: the five themes, the `--osp-*` tokens, and a
  stylesheet of your own on the end.
- [[Linking back to the source]]: a link in the site's bar to the repository
  the vault came from.

**Getting it online**

- [[Publishing to GitHub Pages]]: tokens, repositories, branches, custom
  domains, GitHub Enterprise, and incremental publishing.
- [[Locking a site behind a password]]: real encryption rather than a prompt,
  and what it costs you.
- [[Publishing a built app]]: HTML published as-is, folders published whole,
  and sending a prototype to the front page of the site.

**Reviewing it**

- [[Reviewing a built site]]: the comment overlay, pins that follow a
  prototype's sheets and screens, and getting readers' comments back, as a
  file or as GitHub issues everyone can see.
- [[Filing comments as issues]]: GitHub, Jira or Asana, and keeping the two
  in step.

**Editing it**

- [[Editing a prototype]]: change a prototype from its preview with
  Figma-style tools, a Design panel and keyboard shortcuts, written straight
  into its file.

**Driving it**

- [[Commands and automation]]: the seven commands, and running one on load.

## Reference

- [[Every setting]]: the whole settings screen, section by section.
- [[Known limits]]: what does not work yet, stated plainly.
- [[This vault as a worked example]]: how this vault is configured, and why
  each choice is the way it is.

## Examples you can build

- [[See it working]]: a prototype with phone, tablet and desktop widths,
  diagrams, a Bases view, a Dataview query and highlighted code, on one page.
- [[About the as-is demo]]: a hand-written web page published byte for byte.
- [[About the prototype demo]]: the prototype on that page, and how to
  review it.
- `Scratch/`: a folder that is **not** published, and the build report says
  so. See [[Choosing what gets published]].
