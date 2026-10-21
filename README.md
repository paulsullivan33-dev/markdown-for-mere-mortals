# Markdown for Mere Mortals

**Markdown** is the plain-text format half the
world writes in without knowing its name: README
files, forum posts, notes apps, chat messages,
documentation sites. You type `#` for a heading,
`*stars*` for emphasis, dashes for a list, and a
*renderer* — a program that reads the text —
turns it into a formatted page.

Here is the part the cheatsheets leave out:
**there is no single Markdown.** There is the
original 2004 flavour, the **CommonMark** spec
that tried to pin the language down, **GitHub
Flavoured Markdown** (GFM), and the private
dialect inside every app on your phone. They
agree on the basics and disagree, sometimes
silently, on tables, task lists, line breaks,
and which characters are allowed to emphasise
the middle of a word. The same file can come out
as a tidy table in one place and a paragraph full
of pipe characters in another. This guide shows
you the disagreements, with the receipts.

Every behaviour in this guide was run for real
through **pandoc 3.1.3** — using its `markdown`,
`commonmark`, `gfm`, `commonmark_x`, and
`markdown_strict` readers as five test beds —
and cross-checked against a second, unrelated
renderer, **Python-Markdown 3.11.1**, so every
output can be reproduced: the `---` that turned
into a heading instead of a rule, the numbered
list a renderer folded into the bullets above
it, the table that strict CommonMark declined
to see.

## What this guide covers

- [**What Markdown is**](what-markdown-is.md) —
  a text format plus a crowd of renderers; the
  flavours this guide tests, and the one rule
  that explains the rest: the renderer is the
  referee
- [**Paragraphs and line breaks**](paragraphs-and-breaks.md) —
  why pressing Enter once does nothing, the
  two-space break, the backslash break, and the
  flavour where the backslash stops working
- [**Emphasis**](emphasis.md) — stars versus
  underscores, the middle-of-a-word rule that
  CommonMark keeps and the original flavour
  breaks, and the backslash escape
- [**Headings and anchors**](headings-and-anchors.md) —
  `#` headings, setext headings, the `---` trap,
  and the anchor names renderers invent — plus
  the ones this guide can't test for you
- [**Lists**](lists.md) — lazy numbering that
  works, bullet characters that split one list
  into three under CommonMark, nesting, and
  loose versus tight
- [**Tables, task lists, and strikethrough**](tables-tasks-and-strikethrough.md) —
  the GFM extras, what strict CommonMark makes
  of them (a paragraph of pipes), the flavour
  that takes the table but not the checkboxes,
  and the escaped pipe
- [**Links and images**](links-and-images.md) —
  inline and reference links, the definition
  that vanishes, the missing reference that
  stays literal, bare addresses, and the image
  one renderer wraps in a figure
- [**Code**](code.md) — code spans that protect
  their contents, indented blocks, fenced
  blocks, and what the language name on a fence
  actually buys you
- [**Raw HTML**](raw-html.md) — HTML inside
  Markdown, the blank line that switches
  parsing back on, and one renderer that never
  switched it off
- [**One file, four renderers**](one-file-four-renderers.md) —
  a garden club newsletter through every test
  bed at once, diffs included
- [**When it renders wrong**](when-it-renders-wrong.md) —
  the symptom list: what you see, what caused
  it, what to change

## What it doesn't cover

Any one app's dialect in depth — GitHub's live
renderer, Obsidian, chat apps, and the rest are
named where their flavours matter, but their
behaviour is documented-only here, because it
can't be run from this guide's lab (chapter 4
says which parts, and why). Turning Markdown
into Word files, ebooks, PDFs, and slides is
the series' *Pandoc for Mere Mortals*; this
guide renders to HTML only, because HTML is
where flavour differences are easiest to see.
Formal grammar — the CommonMark spec's parsing
algorithm — is linked from the glossary, not
reproduced.

## How to use this guide

Read chapters 1–4 in order; they install the
model (a file plus a referee) and the four traps
that cause most real-world surprises. After
that, chapters stand alone — go to the table,
list, or link that just rendered wrong. Every
chapter works from a file in `examples/`, and
the commands are collected in
`examples/commands.txt`, so you can repeat any
capture yourself: in Markdown, the file is never
the whole story — check what your renderer
makes of it before you ship it.
