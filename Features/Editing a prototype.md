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
| **Attributes** | The layer's HTML attributes: a link's address, an image's alt text, a field's placeholder, its id and classes. |
| **Code** | Where the layer and each rule that styles it are, as a file and a line, with every value editable. See [[#Going to the code]]. |

With nothing selected, the Design tab shows the page instead:

- **Page**: its background, and **Preview at** Full, Tablet or Phone width.
  The narrower widths are still editable.
- **Variables**: the page's colour and size variables (`--name`), editable in
  place.
- **History**: every edit this session, newest first, with **Undo to here**.
  The **History** button on the bar opens it directly.
- **Changes**: what this session did to each file, as a diff: removed lines
  in red, added lines in green. **Copy** takes one file's changes, **Copy
  all** every file's, in the format `git diff` uses.
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

The **Code** section names the file and line where the layer starts. Under
it are the CSS rules that style the layer, **strongest first**, the way the
browser weighs them, each with its own file and line.

- **A struck-out value loses** to another rule. Hover it to see which:
  *Overridden by .card.big*. A dotted underline means a shorthand that loses
  only in part, such as `padding` when another rule sets `padding-top`. This
  is usually the answer to "why doesn't my change show?"
- **Every value is a field.** Click it, type, and press **Enter** to write
  it into that rule in the file; **Esc** puts it back. Empty it to take the
  property away.
- **Add a property** on a rule's last line, written as `gap: 12px`.
- **On the layer (style)** is the layer's own `style` attribute, and takes
  new properties the same way.
- A rule that styles more than one layer says how many, such as *3 layers*:
  a change there changes all of them.

A value marked `!important`, or one that names a file (`url(...)`), is
shown but not editable: change it in the file. So is a rule in a stylesheet
the page's script made, or one loaded from another site.

Click a location to copy it, as `path:line`, or use **Open in** to open the
file at that line in your editor.

### Which editor

Which editor **Open in** uses is a setting: **Comments and editing → Open
code in**. VS Code by default; also Cursor, Windsurf, Zed, VS Code Insiders
and Obsidian. Obsidian opens the file but not the line. **Custom** takes a
link of your own with placeholders, for any editor that has a link format:

| Placeholder | Becomes |
| --- | --- |
| `{path}` | the file's full path on this computer |
| `{file}` | its path inside the vault |
| `{vault}` | the vault's name |
| `{line}`, `{column}` | where the layer or rule starts |

For example `myeditor://open?path={path}&line={line}`. **Don't show a link**
leaves only the location to copy.

## Describing a change for an AI tool

Some changes are quicker to say than to make: "make this the highlighted
plan", "give it the same look as that button". **Describe** lets you say
them on the page, point at what you mean, and hand them to an AI coding tool
such as Claude Code or Cursor with the code behind each layer.

1. **Select a layer and press `/`**, or click **Describe** on the bar. The
   bar's message line becomes a prompt, starting with that layer as ①.
2. **Type what should change.** To point at another layer, click it on the
   page while you type: it goes into the line as a numbered reference, such
   as ②, and is outlined and numbered on the page. The click points rather
   than selects, at the layer right under the pointer.
3. **Press Enter.** The change joins a stack above the bar, and the prompt
   stays open for the next one. **Esc** closes it. Select another layer and
   press `/` again for a change about that one.

A layer keeps its number everywhere it is mentioned, so "match ②" in one
change and "② bigger" in another are about the same layer.

### The stack

- **Click a change**, or its pencil, to load it back into the bar with its
  words and references. The bar says *Editing change 1*. Change the words,
  take a reference out, or click layers to add one, then press **Enter** to
  save it in place. **Esc** leaves it as it was, and emptying it takes it
  out.
- **×** takes a change out; **Clear** (the bin) takes them all.
- **What's copied** flips the stack to the exact text it hands over: the
  changes in order, then *The layers, by number*, each with its file and
  line, its HTML as the file has it, and the CSS that applies, the rule that
  wins first. It also says the width you were looking at, and a hover or
  pressed state if one was shown.

### Handing it over

- **Copy for AI** (**⌘Enter**) puts the text on the clipboard. Paste it into
  Claude Code, Cursor or any AI tool.
- **Save as note** writes the same text to a note in the vault, in the
  **Change requests** folder by default, named for the page and the day,
  such as `pricing 2026-11-24.md`. Its frontmatter names the page and has
  `status: open`. Tell your AI tool to read the note and make the changes,
  and keep it as a record of what was asked.

Describe never changes the page's files, and it is not part of comments or
review: nothing you describe shows to a reviewer or on a published site.
The stack lasts while the page is open; reloading the page clears it, so
save a note first if you want to keep it.

The **Code** section has **Describe a change** too, for the selected layer.

## Attributes

The **Attributes** section shows the attributes worth having for the kind
of layer it is (`href` and `target` for a link, `src` and `alt` for an
image, `type`, `placeholder` and `required` for a field) and then `id`,
`class`, `title`, `aria-label`, `role`, and any other the layer already has.

- Type a value and press **Enter**. Empty a field to take the attribute
  away, except `alt`, where empty means a decorative image.
- On-off attributes such as `required` and `disabled` are checkboxes.
- **Add** one on the last line, written as `data-plan=pro`.

Event handlers (`onclick` and the like), `style`, which has the Design
sections, and `javascript:` addresses can't be written from here.

## A layer the page's script made

Some layers are not written in the file: the page's JavaScript builds them
when it loads, from a list of strings or from data. The bar says so when you
select one (*Made by the page's script, so it isn't in the file*), and the
Layers tab marks it **Script**.

You can restyle one: colour, size and layout go into a CSS rule for its
class, which changes every layer like it. Moving or deleting it can't be done
from the page, because there is no place in the HTML to write that to.

**Its words often can be changed.** The plugin looks for them in the page's
`<script>` blocks, the `.js` files it loads, and the `.json` files those
scripts fetch, such as `fetch("plans.json")`. When they are written out
once, in a string, **Edit text**, **Enter** and double-click work as on any
other text, and the new words go into that string. Quotes and backticks in
what you type are escaped for you, and **Undo** puts the old words back.

When they can't be changed, **Edit text** is greyed out, and its tooltip, the
bar and the **Code** section say why:

| The reason | What it means | What to do |
| --- | --- | --- |
| *Somewhere else* | The words are not in the page's scripts or the JSON files they fetch: they come from a server, or are worked out in code. | Change them where they come from. |
| *Put together from pieces* | The script builds them from parts, such as `${count} items left`, so there is no one place for the whole sentence. | Change the part you want in the script; **Code** shows where. |
| *In the scripts several times* | The same words are written in more than one place, and which one made this layer can't be told. | **Code** lists each place with its line: pick **Change this one**, or **Change all** when they are in one file. Then edit as usual. |
| *Other layers inside it* | It holds more than words. | Double-click to select the words inside it. |

Angle brackets can't be typed into a script's words from the page, since
many scripts put their strings into the page as HTML.

**Code** shows where the layer probably comes from either way: *Found by its
text* when the words are there, and *Found by its class* when only the class
is, which is usually where the script makes the layer from data. When the
text has a number in it that the script fills in, such as *3 items left*,
Code looks for the words around the number instead.

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

**Describing**

| Key | Does |
| --- | --- |
| / | Describe a change to the selected layer, in the bar. |
| Click, while describing | Point at a layer: it goes in as a number. |
| Enter / Esc | Add the change (or save the one being edited) / close the prompt. |
| ⌘Enter | Copy every change for an AI tool. |

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
| **Change requests folder** | **Comments and editing → Edit mode** | Where Describe saves a change request as a note. |
| **Review folder** | **Comments and editing** | Where `edit-backups/` is kept. |

→ [[Every setting]]

## What it does not do yet

- Gap and padding fields do not offer size variables.
- **Put back** on a detached layer keeps the fixed width it was given.
- The panel floats over the page rather than pushing it aside.
- The eyedropper needs a Chromium-based browser.
- A layer the page's script made, rather than the file, can be styled but
  not moved or deleted. Its words can be changed only when they are written
  out whole in a script, or in a JSON file it fetches.
- A JSON file a script fetches reaches the preview only when its folder is
  published whole (**Publish folders whole**), so a page that loads its
  words that way shows them only then.

→ [[Known limits]]

## Related

- [[Publishing a built app]]: publishing HTML as-is, which Edit mode needs.
- [[Reviewing a built site]]: the comment layer that shares the notch.
- [[About the prototype demo]]: a prototype to try it on.
