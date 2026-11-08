---
updated: 2026-11-05
tags:
  - feature
  - html
  - prototype
---

# Publishing a built app

A vault can hold a built web application, and publishing one is a different
problem from publishing a note. Nothing here renders it; the only question is
which of its files travel, and where they land.

## HTML files publish as-is

With **Publish HTML files as-is** on, an `.html` file in scope publishes byte
for byte, at its own path, with no stylesheet or script of ours added.

It is **off by default**, and that default is the point rather than caution. A
vault scoped to the whole vault is a common setup, and vaults are full of HTML
nobody wrote as a web page: saved articles, a plugin's bundled help, an export
somebody made once. Selection had never looked at anything but Markdown, so
turning this on silently would publish all of it on the next build, and you
would find out from the live site.

> [!example] Try it in this vault
> `Examples/html-as-is/` is a hand-written page with a stylesheet and an SVG
> beside it. Turn the toggle on, build, and it publishes untouched. Read
> [[About the as-is demo]] first.

## The files a page names travel with it

Scripts, stylesheets, images, and the files a *stylesheet* names in turn: a
`@font-face` src, a `background-image`, an `@import`. Those are resolved
against the stylesheet rather than against the page, because that is what a
browser does.

A reference that resolves to nothing is **reported with the file that made
it**, rather than silently dropped.

## A folder can be published whole

Under **Publish folders whole**, name a folder and every file in it is
published, referenced or not.

This exists for code splitting. A lazily loaded chunk is named only inside a
string in minified JavaScript, so no scan will ever find it, and leaving it
behind is not a missing route: in React the dynamic import rejects and the
application unmounts, so one click turns the whole page blank.

> [!important] Point it at `dist` or `build`, not at a project root
> A folder published whole publishes everything in it.

What it changes is **what is found, never what is refused**. Still left out:
excluded folders, hidden files, `node_modules`, and the build's own output.
Notes inside it are still published as rendered pages rather than as Markdown
source. And every file left out is reported with the reason.

There is a **Find a built app** helper that looks for a likely output folder,
so you do not have to go hunting.

## Where it lands

Each folder has a second field saying where it is published to:

| Publish at | Where the application ends up |
| --- | --- |
| *(blank)* | `/proto/app/dist/` (its vault path, the default) |
| `app` | `/app/` |
| `/` | the front page of the site |

A vault path is not an address anybody wants to send to a reviewer, which is
most of the reason this field exists.

The other is that `/` makes an application the site's **front door**: its
`index.html` becomes the homepage, the overview the build would have written
is not written, and a homepage note moves to `/index-note.html`.

That is the one place a note does *not* win a collision, and it loses to an
instruction you typed rather than to another file that happened to be there.
The settings panel names the note that is about to move, and the build report
says it again.

A destination says *where* a folder lands, not *whether* it may be published:
the scope still decides that. Two folders cannot be sent to the same place,
and the panel tells you while it is still cheap to fix.

## Two things that decide whether it works, and neither is ours

### Build with a relative base

```sh
vite build --base=./
ng build --base-href ./
# package.json: "homepage": "."
```

The default is `/`, which resolves to the root of the domain, and a site
published into a folder is not that. The build report names every reference
that does this.

### Publish what the build produced, not the source

`src/index.html` is a shell with no application in it; nothing here compiles
anything. A page with a framework root element and no `<script>` at all is
reported as such.

## The vault as the project

This works: the app at the root with its `src`, its `node_modules` and a
`docs` folder of notes beside them. Scope the site at the whole vault, add
`dist` as a folder published whole, and the notes publish as pages while the
application publishes wherever you point it: at `/dist/` by default, at
`/app/` if you say so, or at the front of the site with the notes behind it.

## Related

- [[About the as-is demo]]: the example in this vault.
- [[Known limits]]: a runtime-computed path, a Vite source page, and a locked
  site's blob URLs.
- [[Choosing what gets published]]: the scope still governs all of this.
