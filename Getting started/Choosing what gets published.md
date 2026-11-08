---
updated: 2026-11-06
pinned: 3
tags:
  - guide
  - safety
  - selection
---

# Choosing what gets published

This is the setting that matters most, because it is the only one whose
mistakes are public. Three selectors decide it, of three different shapes,
because a vault that keeps everything in one tree and a vault that is private
by default want different answers.

## Scope: the coarse answer

**One folder**, or **the whole vault**. There is no third option and no
default: the setting starts unchosen and a build refuses until you pick.

Pick one folder if your vault is mostly private and you have a `Published`
folder. Pick the whole vault if the vault *is* the thing you are publishing,
as this one is.

## Excluded folders: the subtraction

**Exclude folders** takes a list of vault paths, one per line, and subtracts
them from whatever the scope took in. Publish the whole vault except
`Journal`, `People` and `Archive`.

No globs. A literal path has exactly one failure mode, a path that is not in
the vault, and the build report names every entry that excluded nothing, so a
typo is reported rather than silently publishing the folder you meant to keep
back.

It applies at every scope, not only to a vault published whole, because a
folder with a private subfolder in it is the same problem one level down. And
it beats the scope where they contradict each other: an entry that contains
the scope publishes nothing, which is what it says.

> [!warning] This is the weakest of the three
> A folder you add to the vault tomorrow is published. The settings screen
> says so. If something must never go out, use the frontmatter flag below,
> and note that **excluded folders do not reach attachments**: an image inside
> an excluded folder that a *published* note embeds is still carried. See
> [[Known limits]].

**This vault uses it.** `Scratch/` is excluded. Build the site and look for
`Scratch/Not published.md`. It is not there, and the report says why.

## A frontmatter flag: the whitelist

**Require a frontmatter flag** names a frontmatter key. With it set, a note is
published only if it carries that key set to `true`:

```yaml
---
publish: true
---
```

This is the one that fails safe. Every note opts in, a note you forget about
stays private, and a new folder changes nothing. It is the setting for notes
that would do real harm if they went out by accident.

The cost is that you have to remember. Leave it off for a vault like this one,
where everything is meant to be public; turn it on for a vault where the
default should be "no".

## Four rules that apply first

Before any selector is consulted:

1. **The build's own output folders are never input.** `_vault-publisher/` and
   `_site-preview/` are excluded, whatever the scope says. Without this, the
   next build selects the last preview and publishes a site inside your site.
2. **Dot-folders are skipped**: the ones Obsidian hides, `.obsidian/`
   included.
3. **Installed dependencies are skipped**: `node_modules` and its two
   cousins. A package's `README.md` is not a note.
4. **Every rendered page is scanned for content from unpublished notes.**

## The privacy scan

A Dataview query reaches across the whole vault, which is a normal and wanted
thing; an index page is exactly that. But it means a published page can
contain a line pulled out of a note that is *not* being published, which is
the failure mode that makes a publisher dangerous rather than merely buggy.

So every rendered page is scanned for it, and the leak is **always reported**,
named by note. What you choose is whether it also stops the build:

- **Refuse to publish if private notes are exposed**: off by default, because
  refusing by default would block the first publish of many ordinary vaults
  with an error the user cannot act on.
- Turn it on for a vault that holds anything genuinely private.

## And one more thing selection does not do

Notes are published as rendered pages, never as Markdown source files, even
inside a folder published whole. The **Markdown** view on a published page
shows a note's text, but what is on the server is the page.

## Related

- [[The note header]]: which frontmatter keys do reach the page.
- [[Publishing a built app]]: `.html` files and whole folders, which are
  selected by different rules.
- [[This vault as a worked example]]: the choices this vault made.
