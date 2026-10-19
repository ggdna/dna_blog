# dna_blog

English | [Deutsch](README.de.md)

Gives a repo the rules and the template to write a blog post for every
ticket, and a skill that writes it.

## Motivation

A ticket often touches several repos. Without a rule it stays open which
repo writes about the change and what the post may say. The layer makes
every repo of a ticket write its own post before publishing: from its own
view, about its own changes only, filed under `doc/blog/<yyyy>` next to
the code it describes. Each post can be read on its own, without knowing
who builds on the repo.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-blog   # TypeScript projects
dart pub add dev:dna_blog     # Dart projects
helix init
```

`helix init` places a test that instantiates and verifies the DNA on every
test run. It copies the guide to `doc/guides/`, the template to
`doc/templates/` and the skill to `.claude/skills/blog/`.

Type `/blog` in Claude Code before publishing a ticket. The skill reports
whether `doc/blog/<yyyy>` already holds a post for the change, and if not,
writes one to `doc/blog/<yyyy>/<yyyy>-<mm>-<dd>-<title>.md` and names the
file for review.

## Guides

- `dna/doc/guides/blog-guide.md` — which repos of a ticket get a post,
  what a post may contain, where it is filed (`doc/blog/<yyyy>`) and how
  it is written: 60–100 lines, wrapped at 80 characters, mermaid diagrams
  where needed

## Templates

- `dna/doc/templates/blog-template.md` — the structure of an English blog
  post: motivation, strategy, one section per implementation step,
  dependency updates and open points

## Skills

- `/blog` — reports whether the current ticket still needs a post in this
  repo, and writes it; follows the blog guide

## Scope

The layer writes English posts only. Posts in other languages are the job
of [dna_translate](https://github.com/ggdna/dna_translate), which also
ships the German template. The guide links a publish guide and a
translate guide; it follows them only when the repo has them from other
layers.

## Layers

The layer is orthogonal: `dna/_dna.json` lists no parent layers. It
carries only its own topic and is combined with other layers by the
consuming repo or by the umbrella layer of its organization.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file;
  `mustOverride` in `dna/_dna.json` marks it, so every repo that lists
  this layer sets it in its own `dna/_vars.json`
- `dnaMermaidMarkdownBlock` — the fence a mermaid diagram is wrapped in

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.

Edit the files below `dna/`, not their copies in `doc/` and `.claude/`,
which the test overwrites.

## License

MIT — see [LICENSE](LICENSE).
