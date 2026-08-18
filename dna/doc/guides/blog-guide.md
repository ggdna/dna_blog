<!--
@license
Copyright (c) dnaCopyrightHolder

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Blog Guide

## General rules

- For each ticket:
- Create a blog post before publishing
- Follow the [Publish Guide](./publish-guide.md) if it exists

## Choose the language of the prompt

- When the prompt is in English, write a German blog post
- Otherwise write in English

## Copy the template

- Create a year folder `blog/dnaYear` for English posts, if not present
- Create a year folder `blog/de/dnaYear` for German posts, if not present
  (if multi-language-guide.md exists)
- Come up with a summarizing title for the ticket
- Translate the title into English and derive a file name title from it
- Copy `doc/templates/blog-template-de|en.md` to `<yyyy>-<mm>-<dd>-title-en-kebab-case`

## Content

- Follow the structure of the copied template
- Summarize the why, the how as well as the result
- Write simple and understandable
- Summarize the content in 60-100 lines
- Write longer for complex tickets
- Wrap lines at 80 characters
- Embed mermaid diagrams when needed
- Use mermaid dnaMermaidMarkdownBlock markdown blocks

## Translation

- Have a look into the [Multi Language Guide](doc/guides/multi-language-guide.md)
- if a multi-language-guide.md does not exist, do not translate the blogs
