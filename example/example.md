# Example

`dna_blog` is a DNA layer: it ships the blog guide, the blog post template
and the `/blog` skill, no library code. Declare it as a dev dependency and
instantiate it once:

```bash
dart pub add dev:dna_blog    # Dart projects
pnpm add -D @ggdna/dna-blog  # TypeScript projects
gg dna init
gg dna build
```

Then type `/blog` in Claude Code after a ticket: it copies the template to
`doc/blog/<yyyy>/<yyyy>-<mm>-<dd>-<title>.md` and fills it with the changes
of this repo.
