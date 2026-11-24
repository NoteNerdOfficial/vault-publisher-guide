---
updated: 2026-11-24
tags:
  - reference
  - settings
---

# Every setting

The settings screen, in the order it appears. Each row says what the default is
and links to the note that explains it.

## Preview and publish

Not settings, but they sit at the top because they are what you came for.

| | |
| --- | --- |
| **Build a preview** | Builds into `_site-preview/`. |
| **Include comment and edit tools** | Off. Puts the comment layer and Edit mode on the preview. → [[Reviewing a built site]], [[Editing a prototype]] |
| **Open the preview** / **Stop serving** | The local server, started on demand. |
| **Publish to GitHub** | → [[Publishing to GitHub Pages]] |

## What to publish

| Setting | Default | |
| --- | --- | --- |
| **Site name** | **unset** | No default on purpose. |
| **Scope** | **unchosen** | Whole vault or one folder. No default on purpose. |
| **Folder** | — | Shown when the scope is a folder. |
| **Require a frontmatter flag** | off | The whitelist. Fails safe. |
| **Publish HTML files as-is** | off | → [[Publishing a built app]] |
| **Homepage** | empty | Falls back to `README.md`, `index.md`, `Home.md`, then a generated overview. |
| **Date property** | `updated` | → [[The note header]] |
| **Start here property** | `pinned` | `true` to list a note, or a number to place it. → [[The note header]] |
| **Refuse to publish if private notes are exposed** | off | The leak is reported either way. |
| **Refuse to publish a shortened Bases view** | off | The gap is stated on the page either way. |
| **Exclude folders** | empty | One vault path per line. No globs. |

→ [[Choosing what gets published]]

## Angular, React and other built apps

| Setting | Default | |
| --- | --- | --- |
| **Publish folders whole** | empty | Each with a **Publish at** destination. |
| **Find a built app** | — | Looks for a likely output folder. |

→ [[Publishing a built app]]

## Appearance

| Setting | Default | |
| --- | --- | --- |
| **Style** | `Studio` | Five themes, with a live specimen. Applies on the next build. |
| **Opens in** | the visitor's system | Or pin the site to light or dark. A reader can still switch. |
| **Custom stylesheet** | empty | A vault path, appended to `assets/site.css`. |
| **Link to the source repository** | off | |
| **Repository address** | empty | Blank falls back to the publish target. |

→ [[Themes and your own CSS]], and [[Linking back to the source]] for the last two.

## GitHub

| Setting | Default | |
| --- | --- | --- |
| **Personal access token** | empty | Encrypted via the OS keychain. |
| **Connection** | — | Checks the token and reports what it found. |
| **Repository** | empty | `owner/repo`. |
| **Branch** | `gh-pages` | |
| **Custom domain** | empty | Written to `CNAME` on every publish. |
| **GitHub Enterprise** | off | A different API base. |

→ [[Publishing to GitHub Pages]]

## Password

| Setting | Default | |
| --- | --- | --- |
| **Password for the published site** | empty | Encrypts the build. Never applied to a preview. |

→ [[Locking a site behind a password]]

## Comments and editing

Three parts, under their own headings.

**Comments in your preview**

| Setting | Default | |
| --- | --- | --- |
| **Your name** | empty | Shown against your comments in the preview. Never written into the published site. |
| **Review folder** | `_vault-publisher/review` | |
| **Reopen sheets and popups automatically** | off | Repeats the taps that opened a comment's sheet. Applies to the published site too. |
| **Import review comments** | — | |

**Edit mode**

| Setting | Default | |
| --- | --- | --- |
| **Open code in** | VS Code | Or Cursor, Windsurf, Zed, VS Code Insiders, Obsidian, **Custom…** or **Don't show a link**. → [[Editing a prototype]] |
| **Custom link** | empty | With **Custom…**: a link with `{path}`, `{file}`, `{vault}`, `{line}` and `{column}`. |
| **Change requests folder** | `Change requests` | Where Edit mode's **Describe** saves a change request as a note. → [[Editing a prototype#Describing a change for an AI tool]] |

**Comments on the published site**

| Setting | Default | |
| --- | --- | --- |
| **Include in the published site** | off | Ships the overlay to readers. Everything below is hidden while it is off. |
| **Let readers write comments** | off | |
| **How readers' comments reach you** | a file they send you | Or GitHub issues on the site's repository, when that repository can carry them. |
| **Address shown when a reader exports** | empty | With a file. An email address or URL, shown to readers. |
| **Sign-in service (optional)** | empty | With GitHub issues. Your own sign-in service's address. |

→ [[Reviewing a built site]]

## Issue tracker (preview builds only)

| Setting | Default | |
| --- | --- | --- |
| **File comments as issues** | `none` | GitHub, Jira or Asana. |
| **Labels** | `review` | Comma-separated. |
| **Send every open comment** | — | |
| **Keep the two in step** | on | Does nothing while the provider is `none`. |
| **Sync now** | — | Ignores the quiet interval. |
| GitHub: **Repository owner**, **Repository** | empty | Blank means the publish target. |
| Jira: **Jira site**, **How you sign in**, **Project key**, **Issue type**, **Atlassian account email**, **Username**, **Browser address** | — | `Issue type` blank means `Task`. |
| Asana: **Project**, **Workspace** | empty | Workspace optional. |

→ [[Filing comments as issues]]

## On startup

| Setting | Default | |
| --- | --- | --- |
| **Run automatically** | off | |
| **What to run** | — | A preview build or a publish. |

`spike` and `diagnose` are set in `data.json` rather than here.
→ [[Commands and automation]]

## Also on the screen

- **Related plugins**: a list of the plugins whose output this one preserves.
- **Remove the previous plugin folder**: appears only once, and only if you
  used the plugin under its old id. The plugin shipped during development as
  `site-publisher-spike`; the first run under `vault-publisher` imports the old
  settings and offers to delete the folder they came from.

## Where settings are stored

`<vault>/.obsidian/plugins/vault-publisher/data.json`. The two credentials and
the site password are ciphertext in there wherever the OS has a keychain to
hold a key; everything else is plain JSON you can read and edit.

→ [[This vault as a worked example]] for the one in this vault.
