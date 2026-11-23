---
updated: 2026-11-22
tags:
  - feature
  - encryption
  - privacy
---

# Locking a site behind a password

## Why it is encryption and not a login

A site on GitHub Pages is public. A password prompt drawn over a document that
already contains the text protects nothing. `curl` returns it in full, and so
does View Source.

So a password here is not access control. It **encrypts the files at build
time**, and a reader without the password downloads ciphertext.

## What is encrypted

Each page is encrypted **whole**: title, navigation, search payload and all.
Encrypting only the body would be worse than useless: publishing a navigation
tree that lists `Clients/Acme/Q3 Plan` beside an encrypted body gives away the
thing worth keeping.

Attachments are encrypted beside their own names, with `.enc` on the end.

What stays readable, because it has to: the two stylesheets, the site and
overlay scripts, the harvested fonts, `.nojekyll`, `CNAME`, and a shell page
that says a password is needed.

## The crypto

PBKDF2-HMAC-SHA256 at **600,000 iterations**, OWASP's current figure, then
**AES-GCM**. One salt per build, a fresh IV per file, and the iteration count
is carried in every payload, so raising it later does not strand sites already
published.

The derived key is cached in `sessionStorage` for the tab, so following a link
to another page does not ask again.

## How a locked page comes back

It is **reassembled**, not merely decrypted. The page's own files are
encrypted too, so the markup names files that are not on the server. The
reader's browser fetches them, decrypts them, and hands them to the document
as blob URLs.

Order matters: anything the parser must have (scripts, stylesheets, and the
files a stylesheet names) is put in place *before* the document is written,
because a script element whose load has already failed does not try again.
Images are swapped in afterwards, so a page is readable before its pictures
arrive.

That only repairs what is in the page when it is written, so a locked site
also publishes a service worker, `osp-sw.js`, at its root. Once a page has
unlocked, every request it makes for a locked file goes through the worker,
which fetches the encrypted file, decrypts it and answers with the plain one:
a picture a script adds later, a `fetch()` for data, a lazily loaded chunk of
a code-split application. While the worker is in charge the page is written
exactly as published, with no blob URLs.

The worker never stores the key. It asks the page that made the request,
which answers from the tab's `sessionStorage`, so the key still lasts no
longer than the tab. Publishing the site without a password after it was
locked replaces the worker with one that removes itself.

> [!note] Without service workers
> Some private windows, and a site opened from disk, have no service
> workers. There the page falls back to blob URLs, and a code-split
> application or a runtime `fetch()` fails as it used to. Tested in Chromium
> on GitHub Pages; not yet in Safari.

## What it is not

A shared secret. One password for everyone, no revocation short of
republishing with a new one, and anybody who has it can pass it on. If you
need per-reader access with the ability to revoke it, this is not that and
cannot be made into it.

## What it costs

> [!warning] No incremental publishing
> A fresh salt and a fresh IV per file means every encrypted file differs from
> the one already published, so the manifest matches nothing and every publish
> is a full upload. That is the opposite of what incremental publishing exists
> for, and it matters most on exactly the large sites it was written for.

## Where the password lives

**Password for the published site**, in settings. It is stored through the same
keychain the tracker token uses, so what is in `data.json` is ciphertext.

Structurally, it is kept well away from the build's configuration: the build
never sees it at all. Encryption runs over the finished files afterwards. That
is also why **a preview is never locked**: you are reading your own vault.

## Related

- [[Publishing to GitHub Pages]]: the upload this changes.
- [[Choosing what gets published]]: not publishing something is stronger than
  encrypting it.
