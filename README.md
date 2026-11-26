# dna_blog

The DNA layer that says how a ticket becomes a blog post.

## Guides

- `dna/doc/en/guides/blog-guide.md` — which repos of a ticket get a post,
  what a post may contain, where it is filed
  (`pm/<lang>/<yyyy>-Q<n>/blog`)

Every file of `dna/doc/en/` also ships in German and Farsi, with the
same name:

- `dna/doc/de/guides/`
- `dna/doc/de/templates/`
- `dna/doc/fa/guides/`
- `dna/doc/fa/templates/`

## Templates

- `dna/doc/en/templates/blog-template.md` — the structure of an english blog
  post

## Skills

- `/blog` — reports whether the current ticket still needs a post, and
  writes it

## Publishing

`dna/dot-pubignore` keeps `/doc/*/guides/` and `/doc/*/templates/` out of the
package `dart pub publish` uploads. helix joins it with the ignore files of the
other layers into the project's `.pubignore`.

## Layers

Orthogonal: this layer carries only its own topic and is combined with
other layers by the consuming repo. Posts in other languages are the job
of [dna_translate](https://github.com/ggdna/dna_translate), which also
ships the german template.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file
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
