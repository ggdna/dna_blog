# dna_blog

The DNA layer that says how a ticket becomes a blog post.

## Guides

- `dna/doc/guides/blog-guide.md` — when a post is due, where it is filed
  and what it contains

## Templates

- `dna/doc/templates/blog-template.md` — the structure of an english blog
  post

## Skills

- `/blog` — reports whether the current ticket still needs a post, and
  writes it

## Layers

Orthogonal: this layer carries only its own topic and is combined with
other layers by the consuming repo. Posts in other languages are the job
of [dna_translate](https://github.com/ggdna/dna_translate), which also
ships the german template.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file
- `dnaYear` — the year folder posts are filed under
- `dnaMermaidMarkdownBlock` — the fence a mermaid diagram is wrapped in

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-blog   # TypeScript projects
dart pub add dev:dna_blog         # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
