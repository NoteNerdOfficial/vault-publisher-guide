---
updated: 2026-11-08
pinned: 2
tags:
  - guide
  - setup
---

# Install and first build

Nothing here touches the internet. The goal is a site on your own disk that
you can click around in, which is also the fastest way to find out whether
your vault publishes the way you expected.

## Install the plugin

**Settings → Community plugins → Browse**, search for **Vault Publisher**,
install it, then enable it. That is the whole of it, and it is the route that
keeps you on the current version.

The listing is at
[community.obsidian.md/plugins/vault-publisher](https://community.obsidian.md/plugins/vault-publisher),
whose **Add to Obsidian** button opens the same screen in the app.

The plugin is desktop-only, because it needs a running Obsidian to render
through, and `isDesktopOnly` in the manifest says so. It requires Obsidian
**1.7.2** or later.

If this vault was handed to you with the plugin already inside it, it is at
`.obsidian/plugins/vault-publisher/` and there is nothing to install. Enable it
under **Settings → Community plugins** if it is not already on.

> [!note] Installing by hand, or building from source
> Neither is the normal route, and neither updates itself afterwards. To put a
> build in place by hand, copy `main.js`, `manifest.json` and `styles.css`
> into `<your-vault>/.obsidian/plugins/vault-publisher/` and reload. To build
> it yourself: `npm install`, then `npm run build`, then
> `npm run deploy <path-to-vault>`. The deploy script takes the vault path as
> an argument, from `VAULT_PUBLISHER_VAULT`, or from a gitignored
> `.vault-path` file, and has no default, because guessing a directory to
> write a plugin into is worse than failing with instructions.

## Fill in the two things that have no default

Open **Settings → Vault Publisher**. Two settings start empty on purpose and a
build refuses to run until both are answered:

| Setting | Why there is no default |
| --- | --- |
| **Site name** | A placeholder would tick the first-run checklist's own box, and you would publish a site called "My Site". |
| **Scope** | Both possible defaults are wrong. A folder name publishes nothing when the folder does not exist; the whole vault publishes every private note you own on the first run. |

Everything else has a default that is safe to leave: no excluded folders, no
frontmatter flag, no folders published whole, the `studio` theme, no custom
stylesheet, no password, no overlay, no tracker, no source link.

That is deliberate across the board: the settings that reach a published page
are all opt-in, so upgrading the plugin never changes what your site contains.

## Build a preview

**Settings → Vault Publisher → Build a preview**, or the command palette:
**Vault Publisher: Build site to preview folder**.

The build writes into `_site-preview/` inside the vault. It reports as it goes,
since rendering a large vault takes long enough that silence reads as a hang,
and it finishes with a report naming:

- how many notes were selected, rendered and written
- every file that was skipped, and the reason
- every excluded-folder entry that excluded nothing
- any content a Dataview query pulled in from a note that is not published
- any reference in an as-is page that resolved to nothing

Read the report. It is where the plugin tells you about the things that look
like success from the outside. A folder you spelled wrong excludes nothing
and says nothing, unless something says it.

## Look at it

**Open the preview** starts a local server and opens the site in your browser.
The server exists only while you are using it: it is a listening socket that
can write inside your vault, so it starts on demand and **Stop serving** ends
it.

You can open `_site-preview/index.html` directly instead, but some things need
a server to work properly. Use the preview button.

## What you should see

The front page, then a page per note. On a note page: a command bar with
search across the top; on the left a **Start here** list above the vault tree;
the note in the middle; and a rail on the right carrying **On this page**,
**About this note**, **Linked from** and **Related**. There is a **Read /
Markdown** switch, and a theme toggle a reader can pin.

If that is what you are looking at, the hard part is done. The rest is
[[Publishing to GitHub Pages|getting it onto the internet]] and deciding what
it should look like.

## Then

- [[Choosing what gets published]]: before you publish anything public.
- [[Pages the build writes for you]]: what is on the screen and where it came
  from.
- [[Publishing to GitHub Pages]]: the online half.
