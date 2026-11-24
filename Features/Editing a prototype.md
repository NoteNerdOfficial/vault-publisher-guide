---
updated: 2026-11-24
pinned: 7
tags:
  - feature
  - edit
  - prototype
---

# Editing a prototype

An HTML page published as-is can be edited in its preview, with tools and a
panel that work like Figma's. What you change is written straight into the
page's file in your vault, so there is no design file to keep in step with
the code: the prototype *is* the design.

![[edit-mode.png]]

*The Team card selected, with the Rectangle tool out. The blue line above
**Start a trial** shows where the rectangle would go, and the Design panel on
the right shows the card's auto layout, sizing, appearance, fill and stroke.*

## What it needs

- **Publish HTML files as-is** on, in **What to publish**.
- **Include comment and edit tools** on, next to **Build a preview**.
- A preview opened from the plugin: **Build a preview**, then **Open the
  preview**. The plugin's local server is what writes the file, so Edit mode
  exists only there. A published site never carries it, even with comments
  switched on for readers.

Edit mode works on the page that is the prototype itself, not on a note that
embeds one. In a note, use **Open full page** on the embed to get there.

> [!example] Try it on this vault
> Build a preview of this vault, open [[See it working]], and use **Open full
> page** on the basket prototype. Press **E**, or click the pencil on the
> notch at the bottom. Every change you make is written into
> `Examples/prototype/basket.html`, and **Undo** takes it back out.

## Selecting

- **Click** a layer to select it. The first click picks the outermost layer
  that is not the size of the whole page, the way Figma picks a frame.
- **Double-click** to go one level inside it, and **Esc** to go back up. On a
  text layer that is already selected, double-click edits its words.
- **Alt-click** selects the deepest layer under the pointer directly.
- **Shift-click** adds a layer to the selection, or takes it away.
- **Right-click** opens a menu with everything the bar and the shortcuts do.

The bar under the page shows the selected layer's path, such as
`main.plans › div.plan`. Click a step in the path to select it.

## The bar

**Edit text**, **Duplicate**, **Hide** and **Delete**, then the insert tools,
then **Undo**, **Redo** and **History**.

- **Drag** a layer to move it. In a row or column it reorders, with a blue
  line showing where it will land. Into an empty frame it goes inside. On a
  grid it can drop into an empty cell.
- **Alt-drag** leaves the original where it is and drops a copy.
- **Drag a handle** on the selection's right or bottom edge, or its corner,
  to resize it.

## Adding layers

| Tool | Key | What it adds |
| --- | --- | --- |
| **Frame** | F | An auto layout frame: a column with 8 px gap and 16 px padding. |
| **Rectangle** | R | A 100 × 100 grey box. |
| **Text** | T | A paragraph, ready to type into. |
| **Image** | ⇧⌘K | An image from the page's own folder, picked from thumbnails with a search. |
| **More** | | A heading, button, link, input, divider or list. |

Pick a tool and the page shows where the layer would land as you move the
pointer: a blue line between two layers, with a dashed outline round the
frame it would go into, or a filled outline round an empty frame. The bar
says it in words, such as "Click to add the button before button.btn, in
form.signup".

- **Click** to add it there.
- **Drag** to give a frame, rectangle or image a size as well.
- **Enter** puts it by the selection instead: inside it if it is a frame,
  after it if not.
- **Esc** puts the tool down. So does picking the same tool again.

Near the edge of a frame, the layer goes beside the frame rather than inside
it, which is how a new card goes between two cards.

Once it is in, the new layer is selected, a text layer is ready to type, and
the panel opens at the section you are likely to want next: **Fill** for a
rectangle or a button, **Auto layout** for a frame, **Text** for text.

**More uses the page's own look.** A heading, button, link or input takes the
classes of one already on the page, and the menu says which, for example
*Button: like "Start a trial"*. A button picks one whose class says
`primary`, `cta`, `main` or `accent` if there is one, so a new button looks
like the page's main button rather than a grey browser default. Because they
are classes and not copied styles, the new layer follows the page's
stylesheet as the old one does.

**Images** come from the page's folder and the folders below it. To use a new
one, put it in that folder in your vault and open the picker again.

> [!note] R is Rectangle in Edit mode
> As in Figma. In View and Comment modes R still opens Review mode, which is
> otherwise a click on the notch.

## The panel

The panel sits beside the page and docks to the left or the right with the
button at its top. It has two tabs.

### Design

For the selected layers, in sections you can fold. The sections you fold stay
folded.

| Section | What is in it |
| --- | --- |
| **Position** | Alignment in its parent, rotation, and **Detach from auto layout** to place a layer freely. A detached layer has **Put back** to return it. |
| **Auto layout** | Direction (down, across, wrap or grid), alignment, gap, padding on each side, columns and rows for a grid, and **Clip content**. **Add auto layout** on a layer without it. |
| **Sizing** | Width and height, each **Fixed**, **Hug contents** or **Fill container**, with **Min and max**. |
| **Appearance** | Opacity, corner radius (one for all corners or each separately) and blend mode. |
| **Text** | Font, weight, size, line height, letter spacing, alignment, case, decoration, truncation and colour. |
| **Fill** | Colours and gradients, and how an image fills its box. |
| **Stroke** | Colour, width and style. |
| **Effects** | Shadows, layer blur and background blur. |
| **State** | Shows the layer as **Hover**, **Pressed** or **Focus**, so the styles for those states can be edited too. |
| **Code** | Where the layer and each rule that styles it are, as a file and a line. |

With nothing selected, the Design tab shows the page instead:

- **Page**: its background, and **Preview at** Full, Tablet or Phone width.
  The narrower widths are still editable.
- **Variables**: the page's colour and size variables (`--name`), editable in
  place.
- **History**: every edit this session, newest first, with **Undo to here**.
  The **History** button on the bar opens it directly.
- **Shortcuts**: the keys below.

### Layers

The page as a tree. Search it, click a row to select the layer, toggle the
eye to hide or show it, and drag a row to reorder. A layer the page's own
script made is marked **Script**: it is not in the file, so it can be
inspected but not moved or deleted.

## Several layers at once

With more than one layer selected, a change in the panel applies to all of
them, and so does every action on the bar. **Shift+A** adds auto layout,
**⌥⌘G** frames the selection in a new auto layout frame, and **⇧⌘G** takes a
frame apart again. **⌥⌘C** and **⌥⌘V** copy one layer's look (fill, stroke,
radius, shadow, text styles) and paste it onto others, without its size or
place. **Select matching layers** in the right-click menu selects every layer
with the same tag and classes.

## Where a change is written

- A value on the layer's own `style` is changed there.
- A value that comes from a stylesheet rule shared with other layers asks
  first: change **this layer** only, or **all** the layers the rule styles.
  The rule is changed in place, in the page or in its linked `.css` file.
- A colour can be picked from the page's variables, from the colours already
  on the page, or made into a new variable with **Create variable**. The
  eyedropper (**I**) picks one from anywhere on the screen, in Chromium-based
  browsers.
- On a page that changes with the window's width, **Applies to** chooses
  between every width and only this width and narrower (`@media`).

An edit changes only the characters it has to, so a diff of the file shows
the change and nothing else, with the file's own indentation and quotes.

## Going to the code

The **Code** section names the file and line where the layer starts, and
where each rule that styles it is. Click a location to copy it, as
`path:line`, or use **Open in** to open the file at that line in your editor.

Which editor is a setting: **Comments and editing → Open code in**. VS Code by
default; also Cursor, Windsurf, Zed, VS Code Insiders and Obsidian. Obsidian
opens the file but not the line. **Custom** takes a link of your own with
placeholders, for any editor that has a link format:

| Placeholder | Becomes |
| --- | --- |
| `{path}` | the file's full path on this computer |
| `{file}` | its path inside the vault |
| `{vault}` | the vault's name |
| `{line}`, `{column}` | where the layer or rule starts |

For example `myeditor://open?path={path}&line={line}`. **Don't show a link**
leaves only the location to copy.

## Undo, History and backups

Every edit can be undone with **⌘Z** and redone with **⇧⌘Z**, or taken back
several at a time with **Undo to here** in History. A move or a group of
changes made at once undoes as one step.

Before the first edit to a file each time the preview server starts, a copy
of the file is kept in the review folder, under `edit-backups/`. It never ends
in `.html`, so it is never published.

## Keyboard shortcuts

On Windows and Linux, read **Ctrl** for ⌘, **Alt** for ⌥ and **Shift** for ⇧.

**Modes**

| Key | Does |
| --- | --- |
| E | Edit mode. |
| V / C | View mode / Comment mode. |
| Esc, with nothing selected | Leaves Edit mode. |
| Hold Space | Use the page as in View mode (open a menu, turn a slide), then let go and edit what it showed. |

**Selecting**

| Key | Does |
| --- | --- |
| Click / Alt-click | Select / select the deepest layer. |
| Shift-click | Add to or take from the selection. |
| Double-click / Enter | Go inside the layer, or edit its words if it is text. |
| Esc / ⇧Enter | Go up to its parent. |
| Tab / ⇧Tab | Next / previous layer beside it. |
| ⌘A | Select every layer beside it. |

**Adding**

| Key | Does |
| --- | --- |
| F / R / T | Frame / rectangle / text tool. |
| ⇧⌘K | Image picker. |
| Enter, with a tool out | Add it by the selection. |
| Esc, with a tool out | Put the tool down. |

**Changing**

| Key | Does |
| --- | --- |
| Enter | Edit the selected text. Enter again to finish, Esc to cancel. |
| ⌘D, or ⌥-drag | Duplicate. |
| ⌘C / ⌘V | Copy / paste layers. |
| ⌥⌘C / ⌥⌘V | Copy / paste properties. |
| Delete or Backspace | Delete. |
| ⇧⌘H | Hide or show. |
| ⇧A | Add auto layout. |
| ⌥⌘G (or ⌘G) / ⇧⌘G | Frame the selection / ungroup. |
| Arrow keys | Reorder it in its row, column or grid. |
| ⌘] / ⌘[ | Bring forward / send backward. |
| Arrow keys, on a detached layer | Nudge 1 px; with ⇧, 10 px. |
| I | Eyedropper. |
| ⌘Z / ⇧⌘Z | Undo / redo. |

**Looking**

| Key | Does |
| --- | --- |
| Hold ⌥ | Measure the distance from the selection to the layer under the pointer. |
| Right-click | Every action, in a menu. |

## Settings

| Setting | Where | What it does |
| --- | --- | --- |
| **Include comment and edit tools** | next to **Build a preview** | Puts the comment layer and Edit mode on the preview. |
| **Publish HTML files as-is** | **What to publish** | Edit mode only appears on these pages. |
| **Open code in** | **Comments and editing → Edit mode** | The editor the Code section opens a file in. |
| **Review folder** | **Comments and editing** | Where `edit-backups/` is kept. |

→ [[Every setting]]

## What it does not do yet

- Gap and padding fields do not offer size variables.
- **Put back** on a detached layer keeps the fixed width it was given.
- The panel floats over the page rather than pushing it aside.
- The eyedropper needs a Chromium-based browser.
- A layer the page's script made, rather than the file, can be styled but
  not moved, retyped or deleted.

→ [[Known limits]]

## Related

- [[Publishing a built app]]: publishing HTML as-is, which Edit mode needs.
- [[Reviewing a built site]]: the comment layer that shares the notch.
- [[About the prototype demo]]: a prototype to try it on.
