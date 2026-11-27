<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Scope blog posts to their repo

## Motivation

- A ticket often touches several repos. Until now the guide asked for one
  post "for each ticket" and left open which repo writes it and what it
  may say.
- A repo is a building block: many parents can use it. A post that
  explains a change by naming one of its users carries knowledge the repo
  must not have, and it is wrong from the view of every other user.
- The goal: every post can be read on its own, next to the code it
  describes, without knowing who builds on top of it.

## Strategy

- One post per repo, written by every repo of a ticket that has the
  blog guide
- A post describes the changes of its own repo only
- Updated dependencies get their own section: only what changed in them
  and matters for this repo
- Users of the repo are never mentioned
- Tickets and plans are referenced only within the own organization
- Posts move from `blog/<yyyy>` to `doc/blog/<yyyy>`, next to the rest of
  the documentation

## Implementation 1: The blog guide

- New section "Know which repos get a post": every repo of the ticket
  with this guide writes its own post before publishing
- New section "Keep the post to this repo" with the scope rules above
- The copy target is now a full path:
  `doc/blog/<yyyy>/<yyyy>-<mm>-<dd>-<title>.md`; before, the year folder
  and the `.md` extension were missing
- The link to the translate guide is relative to the guide's own folder,
  so it resolves in every consuming repo

## Implementation 2: Template and skill

- The motivation asks "why and what for, from the view of this repo"
  instead of "for whom" — the old wording invited naming users
- A new optional section "Dependency updates" sits before "Open Points";
  it is left out when no dependency was updated
- `/blog` now looks only at the commits of this repo in the ticket and
  checks `doc/blog/<yyyy>` for an existing post
- `/blog` copies the english template; other languages follow the
  translate guide

## Implementation 3: The year variable is gone

- `dnaYear` froze the year at instantiation time: a repo instantiated in
  2026 kept filing posts under `2026` in the following years
- The guide now names the folder `doc/blog/<yyyy>`, the year of the post
- Consumers that set `dnaYear` in their own `dna/_vars.json` can drop it

## Open Points

- Existing posts under `blog/<yyyy>` stay where they are until a consumer
  takes the new version; move them to `doc/blog/<yyyy>` then
- Whether a post follows the scope rules is not checked automatically
