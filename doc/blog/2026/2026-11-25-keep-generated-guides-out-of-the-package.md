<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Keep generated guides out of the package

## Motivation

- This layer writes `doc/guides/blog-guide.md` and
  `doc/templates/blog-template.md` into every project that uses it
- Both are working material for the developers of that project. They are
  of no use to someone who installs the project's package from pub.dev,
  yet `dart pub publish` uploaded them with every release
- The goal: the layer says itself which of its files stay out of the
  published package, so a project gets this right without extra work

## Strategy

- Ship a `dna/dot-pubignore` that lists the folders this layer writes to
- Rely on the DNA engine to join the ignore files of all layers into one
  `.pubignore` per project, instead of the last layer replacing the
  others
- Keep `dna/` itself in the package: a package used as a layer is read
  from its published `dna/` folder
- Leave `doc/blog/` in the package: the posts describe the changes of the
  package itself

## Implementation 1: dot-pubignore

- `dna/dot-pubignore` lists `/doc/guides/` and `/doc/templates/`
- The `dot-` escape keeps the file in the published layer: `dart pub
  publish` drops every path with a leading dot
- In this repo the engine instantiates it as `.pubignore`, starting with
  the lines of `.gitignore`, followed by the section `# dna_blog`
- `dart pub publish --dry-run` now lists neither `doc/guides/` nor
  `doc/templates/`, while `dna/` is complete and there are no warnings

## Implementation 2: index.jsonc

- The repo gets its `index.jsonc`: summary, domain and the layers that
  use it

## Dependency updates

- helix joins every `*ignore` file across layers: one `# <layer>` section
  per layer, patterns an earlier section already holds are left out
- A root `.pubignore` starts with the project's `.gitignore`, because
  `dart pub publish` reads it instead of the `.gitignore`

## Open Points

- Projects get the `.pubignore` once they use this version of the layer
  and a helix version that joins ignore files
