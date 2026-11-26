<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# File blog posts per language and quarter

## Motivation

- Posts lived in `doc/blog/<yyyy>` or, in a PM repo, in
  `doc/<yyyy>-Q<n>/blog`: two rules for one thing
- German posts needed their own template in another layer
- Goal: one place for every post, in every language of a repo

## Strategy

- File every post in `pm/<lang>/<yyyy>-Q<n>/blog`
- Write the leading language first, then translate
- Ship guide and template in English, German and Farsi

## Blog guide

- Posts go into the quarter folder of the day the ticket is finished
- The template is copied from `doc/<lang>/templates/blog-template.md`
- New section "Other languages": languages come from `dnaLanguages`,
  translations keep the file name
- The `/blog` skill checks `pm/<lang>/<yyyy>-Q<n>/blog` of the leading
  language

## Translations

- Guide and template moved to `dna/doc/en/`
- German and Farsi copies in `dna/doc/de/` and `dna/doc/fa/`, with
  English anchors on translated headings
- German posts now use `doc/de/templates/blog-template.md` of this layer

## Publishing

- `dna/dot-pubignore` and `.pubignore` exclude `/doc/*/guides/` and
  `/doc/*/templates/` for every language
- `.pubignore` now also carries the entries of `.gitignore`

## Open Points

- Posts in the old folders are not moved by this layer
