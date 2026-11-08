---
updated: 2026-11-05
tags:
  - feature
  - commands
  - automation
---

# Commands and automation

## The commands

All seven are in the palette under **Vault Publisher**:

| Command | What it does |
| --- | --- |
| **Build site to preview folder** | Builds into `_site-preview/`. See [[Install and first build]]. |
| **Publish site to GitHub** | Renders, builds and commits. See [[Publishing to GitHub Pages]]. |
| **Open preview in browser** | Starts the local server and opens the site. |
| **Report render timings** | How long each note in the publish scope took to render. |
| **Import review comments** | Turns an exported review into a note in the vault. |
| **Send open review comments to the tracker** | Files every open comment. |
| **Sync review comments with the tracker now** | Pulls and pushes state immediately, ignoring the quiet interval. |

The first three also have buttons in the settings panel.

## Running something on load

The plugin's `data.json` has an `autoRun` key, which runs one thing when the
plugin loads:

| `autoRun` | |
| --- | --- |
| `none` | The default. |
| `build` | Build a preview. |
| `publish` | Publish. |
| `spike` | Report render timings for the publish scope. |
| `diagnose` | Sample one note's render over time. Needs `diagnosePath` beside it. |

**Build** and **publish** are offered in the settings panel as **Run
automatically** / **What to run**. The other two exist so the whole loop can be
driven from a shell during development.

### Why this exists

Obsidian offers no way to invoke a command from outside the app. Clicking
through the UI for every iteration produces measurements nobody can reproduce,
so instead you write `data.json`, touch the build, and the run happens on
reload.

With the [hot-reload](https://github.com/pjeby/hot-reload) community plugin
installed in the vault, deploying a new `main.js` is enough on its own: the
reload fires on the file change and the `autoRun` fires with it.

> [!note] `diagnose` needs to be told which note
> Because the note worth sampling is whichever one is rendering wrongly, and
> nothing can work that out for you. Set `diagnosePath` to its vault path.

## Related

- [[Rendering inside Obsidian]]: what the timing and diagnose runs measure.
- [[Every setting]]: the automation section.
