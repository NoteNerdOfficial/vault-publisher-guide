---
updated: 2026-11-22
tags:
  - feature
  - review
  - overlay
---

# Reviewing a built site

A comment layer over a built site: pins anchored to blocks of a page, a panel
listing every thread, and a way for the comments to come back to you.

It runs over a local preview by default. Shipping it into the published site is
a separate switch, letting a reader of that site *write* rather than only read
is a second, and how their comments reach you is a third.

## Using it

1. **Include a review overlay** on, then **Build a preview**.
2. **Open the preview**: this starts the local server.
3. Switch to comment mode, click a paragraph. It outlines the block and opens a
   draft box with a priority chooser.
4. Type, send. The comment appears in the review panel.

The panel sorts by time or by priority, filters open from resolved, and steps
through a review one comment at a time with **Resolve and next**. An open pin
shows the block it is about, the comment, a reply box, and the issue it was
filed as, if any.

The toolbar can be dragged to any of six places: the top or bottom of the
window, at the left, the centre or the right. It snaps to the nearest and
stays there from page to page, and the panel opens on the side away from it.

## Pins survive a rebuild

A pin remembers where it was dropped **twice**: in document coordinates, and
as a fraction across the block it landed on. So a rebuild that reflows the page
does not scatter the review.

## Reviewing a prototype

A prototype published with **Publish HTML files as-is** gets the same overlay
as a note, and the overlay follows what the app is doing.

> [!example] Try it on the review demo
> `Examples/review-prototype` is a basket prototype in a phone frame, with a
> scrolling list, a bottom sheet, a popup and a second screen.
> [[About the review demo]] walks through each of the behaviours below.

**One toolbar inside a phone or tablet frame.** When a frame page shows the
app in an `<iframe>`, the outer page carries the only toolbar, and pins land
on what is on the screen. A comment remembers which screen of the app it was
left on, the panel names that screen, and opening the comment sends the frame
back to it. The screen has to be published from the same site as the frame,
which it is when the prototype is one folder.

**Pins follow sheets, drawers and popups.** A comment left inside a dialog, a
bottom sheet, a drawer or a popup belongs to it. The pin moves with it as it
slides in, and is shown only while it is open, whether the app hides it,
parks it off-screen or takes it out of the page. The panel says where a
hidden comment is, such as "sheet (closed)". A pin on a row of a scrolling
list stays on that row as the list scrolls.

**Opening a comment brings back what it is about.** Opening a comment whose
sheet or drawer is closed opens it again, and closing the comment closes it.
A popup the prototype removed from the page cannot be opened that way, so the
card offers **Reopen**, which taps the button that opened it the first time.
It is a button rather than automatic because a tap runs the prototype's own
code.

> [!note] What the overlay counts as a popup
> A `<dialog>`; anything with `role="dialog"` (or `alertdialog`, `menu`,
> `listbox`, `tooltip`), `aria-modal="true"` or the `popover` attribute; and
> anything with a class such as `sheet`, `drawer`, `modal`, `popup`,
> `dropdown` or `toast`. Most prototypes already say one of these.

Only comments left from 0.1.9 on record what reopening needs, and a backdrop
the prototype dims separately does not come back with the sheet.

## Settings

The settings are in **Leave a review**, which has two halves: what happens in
your own preview, and what goes out with the published site.

### In your preview

| Setting | What it does |
| --- | --- |
| **Your name** | Shown against the comments you leave in the preview. Optional, and never written into the published site. |
| **Review folder** | Where comments are saved as you leave them, and where a reader's exported file goes. `_vault-publisher/review` by default. |
| **Import review comments** | Turns the review folder into a note in your vault, with a task per comment. |

### On the published site

| Setting | What it does |
| --- | --- |
| **Include in the published site** | Puts the overlay on published pages too. Off by default: it carries the overlay to every reader, which is a decision about the site rather than about how you work. |
| **Let readers write comments** | Off, the published overlay only reads: pins, the panel, import and export. |
| **How readers' comments reach you** | **A file they send you**, or **GitHub issues on** the site's repository. Below. |
| **Address shown when a reader exports** | With **A file they send you**: an email address or a URL, shown to a reader who has comments to return. |
| **Sign-in service (optional)** | With **GitHub issues**: the address of your own sign-in service. Below. |

> [!important] No vault path reaches a reader
> A published page keys its comments on its own URL and never on the vault path
> behind it, so no folder names go out. The preview overlay *does* carry the
> vault path, which is how an imported comment finds its note, and exactly
> why the published overlay is a different code path rather than the
> same one with a flag set to false.

## How readers' comments reach you

### A file they send you

A reader's comments stay in their own browser until they export them. They
send you the file, at the address you gave, and you drop it into the **Review
folder** and run **Import review comments**. Nothing needs setting up, and
nothing leaves the reader's browser except the file they choose to send.

### GitHub issues

Each comment becomes an issue on the repository the site publishes to, and
everyone who opens the site sees every comment as a pin.

1. A reader leaves a comment as usual.
2. The overlay opens GitHub's own **New issue** form, already filled in. The
   reader submits it, signed in to GitHub as themselves. There is no token to
   store and nothing to host.
3. Until the issue appears, the reader's pin shows faded, as posting.
4. Every visitor's overlay reads the repository's issues and draws them
   where they were left. An issue closed on GitHub shows as closed, and the
   card links to the issue, where the replies are.
5. A sync in the plugin brings the issues into your **Review folder**, so the
   preview and the imported review show them too.

> [!example] What a shared issue looks like
> The title is the first line of the comment. The body is the comment, the
> passage it is about, and where it was left, followed by a hidden marker the
> overlay reads the pin back from:
>
> ```markdown
> The delivery price should be shown before this step.
>
> > Choose delivery
>
> ---
> Left on [Basket](https://your-username.github.io/your-site-repo/Examples/review-prototype/screens/basket.html).
>
> <!-- osp-review {"v":1,"id":"…","page":"…","block":"…","priority":"medium"} -->
> ```
>
> The marker is in the body rather than a label because GitHub drops labels
> from a prefilled form unless the poster can triage the repository. Leave it
> in place when editing an issue, or the pin loses its place.

What this needs, without a sign-in service:

- **A public repository**, since visitors read the issues without signing in.
- **A GitHub account** for anyone who posts.
- **An unlocked site.** It is refused for a site locked with a password, whose
  review would otherwise be public.

If the site's repository cannot carry shared comments, **GitHub issues** is
missing from the choice, and the section says why.

Nothing from the vault goes into a shared issue. **Send to GitHub** from the
preview also leaves the note's vault path out of any issue it files on a
public repository.

### Optional sign-in, hosted by you

You can add a small sign-in service of your own: a Cloudflare Worker and a
GitHub App, both under your accounts. Paste its address into **Sign-in
service (optional)** and publish again. Then:

- the first time a reader posts, they can **Sign in with GitHub** or **Use
  GitHub's form**;
- once signed in, they post from the page, with no GitHub tab per comment,
  and **Sign out of GitHub** is in the overlay's menu;
- the repository can be **private**, including on GitHub Enterprise Server,
  and readers sign in to read the comments as well;
- a **locked site** can share comments too, through a private repository.

The service holds the GitHub App's secret and swaps a sign-in code for a
token, which is all it does. Posting and reading go from the reader's browser
to GitHub directly. It keeps nothing, and on Cloudflare's free plan it costs
nothing: it is called when a reader signs in and every eight hours or so
after, far below the free plan's 100,000 requests a day.

The Worker and a step-by-step setup guide are in the plugin's repository, in
`examples/github-signin-worker`. Setting it up takes about ten minutes.

> [!example] The settings, filled in
> | Setting | Value |
> | --- | --- |
> | **Include in the published site** | on |
> | **Let readers write comments** | on |
> | **How readers' comments reach you** | GitHub issues on `your-username/your-site-repo` |
> | **Sign-in service (optional)** | `https://review-signin.your-username.workers.dev` |

### In a company setting

Where Cloudflare is not allowed, or GitHub is a company Enterprise Server:

- **Run the sign-in service yourself.** It uses only standard web APIs, so it
  runs on an internal host as well as on Cloudflare. Point it at the
  Enterprise Server with its `GITHUB_URL` setting and create the GitHub App
  on that server. It must be reachable by reviewers over HTTPS and must
  itself reach GitHub. Reviewers sign in with their company accounts, and the
  repository can stay private.
- **GitHub issues without sign-in.** Nothing to host, but every visitor must
  be able to read the repository's issues without signing in, and most
  company Enterprise Servers allow nothing to be read that way. In practice
  this works only for a public repository on github.com.
- **A file they send you.** No GitHub access at all, so it works behind any
  firewall.

## Getting the comments back

**Import review comments** turns the review into a note in your vault, in the
**Review folder**: your own comments from the preview, files readers sent
you, and shared comments a sync brought in.

The live comments file in that folder is written continuously by the review
server while it runs, so it is treated separately from a `*.json` you drop
there by hand, never renamed out from under the thing writing it.

### Comments link back to the writing, not the HTML

A publish records which note produced which page, in a page map kept in the
vault beside the review file. So an imported comment points at the note you
need to edit rather than at a built page you cannot.

This also solves a smaller problem: naming a page when four of them are called
`index`.

## Filing from a published site

You cannot, which is why the tracker's section is called **Issue tracker
(preview builds only)**. Filing goes through the plugin's own local server, so
the **Send** action exists in a preview opened in a browser and in no
published page: a static host has nothing to file through.

To file a published site's comments, bring them into the vault first, then
file from a preview. Comments shared as GitHub issues come in with a sync;
otherwise a reader exports them and you import them.
See [[Filing comments as issues]].

## Related

- [[About the review demo]]: a prototype to try all of this on.
- [[Filing comments as issues]]: GitHub, Jira, Asana.
- [[Commands and automation]]: the review commands.
