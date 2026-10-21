# Glossary

**Anchor** — The name a renderer gives a heading
so links can jump to it (`#a-real-top-heading`).
Invented at render time; differs between
renderers in edge cases.

**ATX heading** — A heading written with `#`
characters at the line start; one per level,
`#` to `######`.

**Autolink** — A GFM extra that turns a bare web
address in the text into a link without bracket
syntax.

**Block** — A unit of structure: a paragraph, a
heading, a list, a code block. Markdown parses
blocks first, inline markup second.

**Code fence** — A code block delimited by three
backticks (or tildes) instead of indentation.
See *info string*.

**Code span** — Inline code: text between single
backticks inside a paragraph. Contents are never
interpreted as markup.

**CommonMark** — The specification that defines
Markdown's constructs precisely, with a public
test suite. The baseline dialect of this guide.

**Dialect / flavour** — A variant of Markdown: a
defined set of core rules plus chosen extras.
GFM, pandoc's Markdown, and each app's private
set are flavours.

**Extension** — An optional feature beyond the
core language — tables, task lists,
strikethrough — that a renderer may include or
not.

**GFM (GitHub Flavoured Markdown)** — CommonMark
plus GitHub's extras: tables, task lists,
strikethrough, autolinks.

**Hard break** — A line break inside a paragraph,
written as two trailing spaces or a trailing
backslash.

**Info string** — The word after an opening code
fence, usually a language name, telling the
renderer how to present the block.

**Inline** — Markup inside a block: emphasis,
links, code spans.

**Loose list** — A list whose items are wrapped
in paragraph tags, rendering with extra space.
Opposite: a *tight* list.

**Reference link** — A link whose address is
supplied by a definition elsewhere in the file:
`[text][label]` plus `[label]: address`.

**Renderer** — The program that reads Markdown
and produces output, usually HTML. The referee
of every rule in this guide.

**Setext heading** — A heading written as text
underlined with `===` (level 1) or `---`
(level 2). The `---` form is the trap in
chapter 4.

**Slug** — Another name for an anchor as derived
from heading text — lowercased, spaces to
hyphens, punctuation dropped.

**Strikethrough** — `~~text~~`, a GFM extra,
rendered as `<del>`.

**Task list** — A GFM list whose items begin
with `[ ]` or `[x]`, rendered as checkboxes.

## Sources

- The CommonMark spec and its test suite:
  spec.commonmark.org
- GitHub's guide to its flavour:
  docs.github.com — "Basic writing and formatting
  syntax"
- Pandoc's manual (the readers used here):
  pandoc.org/MANUAL.html
- Python-Markdown's documentation:
  python-markdown.github.io
