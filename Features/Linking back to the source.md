---
updated: 2026-11-04
tags:
  - feature
  - github
---

# Linking back to the source

A small feature with one useful subtlety.

**Link to the source repository** puts a **Source repo** link in the published
site's bar. It is off by default, because a link in the bar is a decision about
the published site and not one to make on somebody's behalf.

**Repository address** is where it points. Leave it blank and it falls back to
the repository the site publishes to, which is the right guess once you have
asked for the link at all, and no guess at all before that.

## Why you might type something else

The repository the *site* lives in is not necessarily the repository the
*vault* lives in. A common arrangement is notes in one repository and a
`gh-pages` branch of another, and a reader following "Source repo" wants the
notes.

## How it reaches the build

Resolved before the build starts. Three questions (is the link on, what was
typed, and what should it fall back to) are settled into one answer: either
there is an address to put in the bar, or there is not.

The build is never handed your publish target or your API host, so it could
not work this out for itself even if it wanted to. That is deliberate: what
the build receives is the answer, not the question.

## Related

- [[Publishing to GitHub Pages]]: the repository this defaults to.
- [[Pages the build writes for you]]: the bar the link appears in.
