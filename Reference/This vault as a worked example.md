---
updated: 2026-11-08
tags:
  - reference
  - meta
---

# This vault as a worked example

The vault you are reading is configured to publish itself. This note says how,
and why each choice is the one it is, so you can copy the parts that fit your
vault and change the parts that do not.

## The configuration

From `.obsidian/plugins/vault-publisher/data.json`:

| Setting | Value here | Why |
| --- | --- | --- |
| **Site name** | `Vault Publisher — Guide` | Required; no default exists. |
| **Scope** | the whole vault | This vault *is* the thing being published. |
| **Exclude folders** | `Scratch` | So you can see an exclusion happen. |
| **Require a frontmatter flag** | off | Everything here is meant to be public, so the whitelist would be ceremony. |
| **Homepage** | `Start here.md` | Set explicitly rather than relying on the `README.md` → `index.md` → `Home.md` fallback. |
| **Date property** | `updated` | The default. Every note sets it. |
| **Start here property** | `pinned` | The default. Five notes set it, numbered `1`–`5`, so the panel reads in the order [[Start here]] recommends rather than alphabetically. |
| **Style** | `Studio` | The default, and it is a documentation theme. |
| **Opens in** | the visitor's system | The default. A guide should look like the machine reading it. |
| **Custom stylesheet** | empty | `Examples/site-tokens.css` is there to try. |
| **Publish HTML files as-is** | off | The default, so the as-is example demonstrates the toggle rather than hiding it. |
| **Publish folders whole** | empty | Nothing here is a built application. |
| **Password** | empty | A guide nobody can read is not a guide. |
| **Review overlay** | off | Turn it on to try it. |
| **Tracker** | `none` | |
| **Repository** | `your-username/your-site-repo` | **A placeholder.** Replace it. |
| **Branch** | `gh-pages` | The default. |
| **Token** | empty | Yours to add. Nothing of anyone else's ships in a shared vault. |

## What to expect when you build it

A preview build of this vault should give you:

- **A front page** that is `Start here.md`, at `index.html`.
- **A page per note**, each with a header built from its frontmatter, an
  outline in the right rail, and backlinks. The notes here link to each other
  heavily, so **Linked from** and **Related** both have something to show.
- **Tag pages** for `guide`, `feature`, `reference`, `setup`, `safety`,
  `rendering`, `theme`, `github` and the rest.
- **A browse tree** with `Getting started`, `Features`, `Reference` and
  `Examples` in it, and **no `Scratch`**.
- **A Start here list** above that tree, reading `Start here`, `Install and
  first build`, `Choosing what gets published`, `Publishing to GitHub Pages`,
  `The note header`: the numbers, not the alphabet.
- **A Mermaid diagram** on [[Rendering inside Obsidian]], if your vault has
  allowed diagrams.
- **A build report** naming `Scratch/Not published.md` among what it left out.

That last one is the thing to actually check. An exclusion that works and an
exclusion that silently did nothing look identical from the outside, which is
why the report names what it skipped.

## Things deliberately left for you to turn on

Each of these is one toggle away, and each demonstrates a different feature:

1. **Custom stylesheet** → `Examples/site-tokens.css`.
   → [[Themes and your own CSS]]
2. **Publish HTML files as-is** → publishes `Examples/html-as-is/`.
   → [[About the as-is demo]]
3. **Include a review overlay** → comment on your own build.
   → [[Reviewing a built site]]
4. **Require a frontmatter flag** → set it to `publish` and watch the site
   empty out, because no note here carries that key. That is the whitelist
   failing safe, which is the behaviour you want from it.
   → [[Choosing what gets published]]

## What is not in this vault

No real repository name, no token, no email address, no absolute filesystem
path, and no name of anybody's vault. Where a path, repository or target was
needed it is a neutral placeholder, because a vault that gets shared publishes
everything in it the moment it is handed over.

Which is, more or less, the lesson this whole plugin is built around.
