---
updated: 2026-11-08
tags:
  - reference
  - settings
---

# Every setting

The settings screen, in the order it appears. Each row says what the default is
and links to the note that explains it.

## Actions

Not settings, but they sit at the top because they are what you came for.

| | |
| --- | --- |
| **Build a preview** | Builds into `_site-preview/`. |
| **Include a review overlay** | Off. Preview-only. → [[Reviewing a built site]] |
| **Open the preview** / **Stop serving** | The local server, started on demand. |
| **Publish to GitHub** | → [[Publishing to GitHub Pages]] |

## Connection

| Setting | Default | |
| --- | --- | --- |
| **Personal access token** | empty | Encrypted via the OS keychain. |
| **Connection** | — | Checks the token and reports what it found. |
| **Repository** | empty | `owner/repo`. |
| **Branch** | `gh-pages` | |
| **Custom domain** | empty | Written to `CNAME` on every publish. |
| **GitHub Enterprise** | off | A different API base. |

→ [[Publishing to GitHub Pages]]

## Content

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
| **Publish folders whole** | empty | Each with a **Publish at** destination. |
| **Find a built app** | — | Looks for a likely output folder. |

→ [[Choosing what gets published]]

## Appearance

| Setting | Default | |
| --- | --- | --- |
| **Style** | `Studio` | Five themes, with a live specimen. Applies on the next build. |
| **Opens in** | the visitor's system | Or pin the site to light or dark. A reader can still switch. |
| **Custom stylesheet** | empty | A vault path, appended to `assets/site.css`. |

→ [[Themes and your own CSS]]

## Source link

| Setting | Default | |
| --- | --- | --- |
| **Link to the source repository** | off | |
| **Repository address** | empty | Blank falls back to the publish target. |

→ [[Linking back to the source]]

## Password

| Setting | Default | |
| --- | --- | --- |
| **Password for the published site** | empty | Encrypts the build. Never applied to a preview. |

→ [[Locking a site behind a password]]

## Review

| Setting | Default | |
| --- | --- | --- |
| **Your name** | empty | Prefills the comment author. |
| **Include in the published site** | off | Ships the overlay to readers. |
| **Let readers write comments** | off | Nested under the above. |
| **Where to send a review** | empty | An email address or URL, shown to readers. |
| **Review folder** | `_vault-publisher/review` | |
| **Import review comments** | — | |

→ [[Reviewing a built site]]

## Trackers

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

## Automation

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
