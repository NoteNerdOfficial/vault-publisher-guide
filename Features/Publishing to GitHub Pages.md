---
updated: 2026-11-06
pinned: 4
tags:
  - feature
  - github
  - publishing
---

# Publishing to GitHub Pages

The build makes a site. This is the part that puts it on the internet.

## How it gets there

Through GitHub's **Git Data API** (blobs, a tree, a commit, a ref) and then
GitHub Pages is pointed at the branch. There is no git binary involved, no
workflow file, and no `workflow` token scope needed.

The *built* site is committed, not your Markdown. See
[[Rendering inside Obsidian]] for why nothing could rebuild it on a server
anyway.

## Settings

**Settings → Vault Publisher**, under the connection section.

### Personal access token

A token with permission to write to one repository. **Connection** checks it
and tells you what it found, which is cheaper than finding out from a failed
publish.

> [!important] Where the token is kept
> It is encrypted through the operating system's keychain, so what sits in the
> vault's `data.json` is ciphertext wherever the platform has somewhere to keep
> a key. The settings screen tells you which storage mode is actually in
> effect. It does not assume the keychain was available.

### Repository, branch, custom domain

| Setting | Notes |
| --- | --- |
| **Repository** | `owner/repo`. In this vault it is the placeholder `your-username/your-site-repo`; replace it with yours. |
| **Branch** | `gh-pages` by default. |
| **Custom domain** | Written to a `CNAME` file in the branch on **every** publish. |
| **GitHub Enterprise** | A different API base, for a GitHub that is not github.com. |

> [!note] Why the domain is rewritten every time
> GitHub Pages reads the domain from a file in the branch, not from the
> repository settings alone. A publish that sent a complete tree without it
> would silently un-set a domain you had configured in the web UI. So once it
> is set here, it is written every time.

> [!warning] Private repositories
> GitHub Pages cannot serve a private repository on a free plan. There is a
> **private** flag so the plugin knows what it is dealing with, but the
> limitation is GitHub's.

## The second publish is small

The first publish uploads everything. After that, the build hashes its
rendered output and compares it against a manifest of what is already
published, so **only what changed is uploaded**.

This is why deterministic ids matter: Obsidian's per-render random ids would
make every page look changed on every build, and the manifest would match
nothing.

Files the build no longer produces are **pruned**: a note you deleted or
un-published does not linger as a page on the live site.

> [!warning] A password costs you this
> Every encrypted build mints a fresh salt and a fresh IV per file, so every
> file differs from the one already published and the manifest matches
> nothing. A locked site therefore uploads in full every time. See
> [[Locking a site behind a password]].

## Publishing

**Publish to GitHub** in the settings panel, or the command **Vault Publisher:
Publish site to GitHub**. Progress is reported in the settings screen rather
than through notices, because a publish renders every note and then talks to
GitHub, which on a large vault is long enough that silence reads as a hang,
and a notice can neither stay put nor show a proportion.

Read the report when it finishes. See [[Choosing what gets published]] for what
it will tell you.

## A link back

**Link to the source repository** puts a **Source repo** link in the site's
bar. It defaults to the repository you publish to, but you can type a
different address: your vault's repository is not necessarily the one the
site lives in. See [[Linking back to the source]].

## Related

- [[Install and first build]]: do this locally first.
- [[Locking a site behind a password]]: if public is not what you want.
- [[Commands and automation]]: publishing without clicking.
