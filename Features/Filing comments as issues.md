---
updated: 2026-11-06
tags:
  - feature
  - review
  - tracker
---

# Filing comments as issues

An open review comment can become an issue in **GitHub**, **Jira** or
**Asana**, and be kept in step with it afterwards.

It is off unless you turn it on, and that is the whole of the design: a
provider of **none** means no command does anything, no action appears in the
overlay, and no request is ever made. A review that stays in the vault is the
normal case and should cost nothing.

## Setting it up

**File comments as issues** picks the provider. Then:

### GitHub

| Setting | |
| --- | --- |
| **Repository owner** | Blank means the repository the site publishes to. |
| **Repository** | Likewise. |

GitHub needs no separate token: it files with the one the publish already
uses, since it is the same kind of credential for the same account and usually
the same repository. The other two providers have nothing to borrow, so they
ask, and their credential is encrypted through the OS keychain like the
publish token.

### Jira

| Setting | |
| --- | --- |
| **Jira site** | Where the API is, context path included. |
| **How you sign in** | Which Jira this is, which decides both the credential and the API. |
| **Project key** | e.g. `ENG`. |
| **Issue type** | Blank means `Task`. |
| **Atlassian account email** | On Cloud. |
| **Username** | With basic auth on a Jira you run yourself. |
| **Browser address** | Optional: where a *person* opens Jira, if the API is somewhere else. |

### Asana

| Setting | |
| --- | --- |
| **Project** | The project gid tasks are created in. |
| **Workspace** | Optional. |

### Labels

**Labels** is a comma-separated list every filed issue carries. `review` by
default, so the issues this creates are findable as a group.

## Filing

Per comment, from the pin in the overlay, or **Send every open comment** for
the lot. There is also the command **Vault Publisher: Send open review
comments to the tracker**.

## Keeping the two in step

**Keep the two in step** is on whenever a tracker is configured at all, on the
grounds that a tracker you bothered to set up is one you want to be right.
With it on:

- a comment resolved here closes its issue
- a comment deleted here closes its issue
- an issue finished there resolves its comment

Off leaves all of that to the command and the button, and changes nothing
else: filing is a separate action either way.

**Sync now** does it immediately, as does the command **Vault Publisher: Sync
review comments with the tracker now**.

> [!note] Automatic sync is rate-limited, on purpose
> An automatic sync stays quiet for a minute afterwards. A preview page that
> loads, pulls and saves within a second is three triggers for one person
> opening one page, and the tracker should not be asked the same question
> three times. The command and the button ignore the interval: asking
> explicitly means now.

## Related

- [[Reviewing a built site]]: where the comments come from, and why filing
  only works from a preview.
