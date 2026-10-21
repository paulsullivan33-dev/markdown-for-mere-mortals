# What Markdown Is

Markdown is two things wearing one name.

The first is a **writing format**: a way of
marking up plain text with characters that were
already on the typewriter — `#` for headings,
dashes for lists, `*stars*` for emphasis — so
the raw text stays readable even before anything
formats it. John Gruber published the original
in 2004, with a short syntax page and a Perl
script that turned the text into HTML.

The second thing is a **crowd of renderers**:
the programs that read the format and produce
the page. Every notes app, forum, wiki, chat
client, and documentation generator has one, and
they were mostly written by reading that 2004
syntax page and making their own decisions about
the parts it left vague. Which parts were vague
turns out to matter.

## The flavours you will actually meet

- **Original ("classic") Markdown** — the 2004
  rules as most early renderers understood them.
  No tables, no task lists, and some loose habits
  this guide will point at when they bite.
- **CommonMark** — a specification, written years
  later, that pins down exactly what every
  construct means, with hundreds of test cases.
  When people say a renderer is "standards
  compliant," this is the standard they mean.
- **GFM (GitHub Flavoured Markdown)** —
  CommonMark plus a small set of extras GitHub
  added: tables, task lists, strikethrough, and
  turning bare web addresses into links. It is
  the dialect of README files and issue trackers
  everywhere.
- **An app's own dialect** — whatever your notes
  app, chat client, or wiki does. Usually close
  to GFM, with private differences nobody
  published.

This guide tests the first three properly and
names the fourth honestly as out of lab reach.

## The test beds

Everything here was run through **pandoc
3.1.3**, a document converter that ships with
several Markdown readers — one per flavour — so
a single fixture can be fed through each in
turn:

```
$ pandoc --version
pandoc 3.1.3
Features: -server +lua
Scripting engine: Lua 5.4
```

```
$ pandoc --list-input-formats
...
commonmark
commonmark_x
...
gfm
...
markdown
markdown_github
markdown_mmd
markdown_phpextra
markdown_strict
...
```

Five of those readers do the work in this guide:
`markdown` (pandoc's own, close to the original
with many extras), `commonmark` (strict
CommonMark), `gfm`, `commonmark_x` (CommonMark
plus selected extras), and `markdown_strict` (the
2004 rules, closely kept). A second, unrelated
renderer — **Python-Markdown 3.11.1**, the
`markdown_py` command — checks whether pandoc's
answers are pandoc's alone:

```
$ markdown_py --version
markdown_py 3.11.1
```

Selecting a flavour is one flag. This shape
recurs in every chapter:

```
pandoc -f gfm -t html examples/flavors.md
```

## The rule that explains the rest

> **A Markdown file has no fixed meaning. It has
> the meaning the renderer reading it gives it.**

That is not philosophy; it is Tuesday. Chapter
10 feeds one ordinary newsletter to four
renderers and gets back four different pages —
in one of them the table isn't a table, and in
another the numbered list has been quietly
folded into the bullet list above it. Every
earlier chapter isolates one such disagreement
so you can see it coming.

**Check:** the fixtures live in `examples/`,
and every quoted output in this guide names the
flavour that produced it. If your renderer
disagrees with a capture here, that disagreement
*is* the lesson — find out which flavour you
have before you blame the file.
