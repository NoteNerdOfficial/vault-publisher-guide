---
updated: 2026-11-08
tags:
  - feature
  - theme
  - css
---

# Themes and your own CSS

## The five themes

**Settings → Appearance → Style**, with a live specimen beside the dropdown so
you can see a theme before you build with it:

| Theme | What it is for |
| --- | --- |
| **Studio** *(default)* | Product documentation. White paper, near-black type, one confident violet, soft corners. For a vault that documents something other people have to use. |
| **Slate** | Monochrome. Tightly set sans, white panels on grey paper in light and true black in dark. For notes where colour should mean a link and nothing else. |
| **Phosphor** | Terminal, calmed down. Mono headings and a green signal over neutral paper; the green marks links, syntax and callouts, and the page itself has no cast. For a vault full of commands, configuration and output. |
| **Solar** | Low glare. Warm sand and burnt orange in light, a dark that stays warm rather than going blue. For a site read for an hour at a time. |
| **Harbor** | Expressive. Sans headings over a serif body, deep navy and a coral signal, generously rounded. For a vault with a point of view rather than a reference shelf. |

A change applies the next time the site is built. Every theme is built in both
light and dark, and a reader can pin either.

## Which one it opens in

**Settings → Appearance → Opens in** decides what a first-time visitor sees:
their own system setting, which is the default, or light or dark whatever
their machine says.

The two explicit choices are a real override rather than a preference. They
are written into each page at build time, so they hold before the first paint
and with JavaScript switched off, and the stylesheet is built so that pinning
to light still wins on a dark machine.

A reader who works the toggle in the bar beats all of it, on that page and
every page afterwards. Their choice is theirs, and the setting only decides
where they start.

## Why a theme is only a palette

A theme here is a set of custom properties rather than a fork of the
stylesheet. Every rule in the site's CSS is written against `--osp-*` names
that the theme declares, so a sixth look is a palette and a type pairing, not
a second copy of the layout to keep in step with the first.

That is also what makes the escape hatch cheap.

## Your own stylesheet

For the vault that wants one of the five with its own blue: name a CSS file in
the vault under **Appearance → Custom stylesheet**, and its rules are appended
to the end of `assets/site.css` on every build. Redeclaring a token is the
whole of it:

```css
:root {
  --osp-link: #a8431a;
  --osp-font-body: "Iowan Old Style", Georgia, serif;
  --osp-measure: 64ch;
}
```

> [!example] There is one in this vault
> `Examples/site-tokens.css`. Type that path into **Custom stylesheet**, build
> the preview, and the site changes colour. Clear the field to go back.

The file can live in a hidden folder (`.obsidian/snippets/` is a reasonable
place for someone who already writes CSS for Obsidian) because it is read
through the vault adapter rather than the file index.

### Why your override holds in dark mode

The theme's tokens are declared inside a **cascade layer** and your rules are
not, which is what makes that `:root` block work in dark as well as light.

Without the layer, a dark value sits under a selector that outranks a bare
`:root`, so an override written the obvious way worked in light and quietly
stopped working when the reader's system went dark. The layer is the fix, and
it means you do not have to know any of this.

## Two failures that are reported rather than silent

Both would otherwise produce a site that looks exactly like the one before it,
which is the worst kind of failure:

- **A path that is not in the vault** is flagged in the settings panel, and
  lands in the build report's skipped list.
- **A path inside the build's own output folders** is refused before it is
  read. Appended to itself, the stylesheet would double in size on every
  build.

## What does not travel

The stylesheet's own vault path never reaches the output. `assets/site.css` is
published; a banner comment naming the source file would hand every reader of
the site a piece of your folder structure.

## Related

- [[Pages the build writes for you]]: what the CSS is styling.
- [[Every setting]]: the Appearance section in full.
