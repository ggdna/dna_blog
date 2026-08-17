# dna_blog

The DNA layer that turns every finished ticket into a blog post.

## Content

- `dna/doc/en/guides/blog-guide.md` — language, naming and content of a
  post
- `dna/doc/templates/blog-template-en.md`,
  `dna/doc/templates/blog-template-de.md` — the post structure in both
  languages

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @tssuite/dna-blog   # TypeScript projects
dart pub add dev:dna_blog    # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run. This
layer sits on top of
[dna_base](https://github.com/ggsuite/dna_base) — everything generic comes
from there, this repo only adds its own topic.

## Development

This repo has `role: "dna"` in `dna/_dna.json`: the `dna/` folder is
authored by hand, never generated. The repo instantiates its own DNA — run
`dart test` after changes; commit first (a file the DNA would overwrite
must not carry uncommitted work).
