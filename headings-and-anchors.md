# Headings and Anchors

Headings come in two spellings. The common one,
**ATX**, is hashes at the line start — one `#`
per level, optionally repeated at the end as
decoration. The older one, **setext**, underlines
the text: `===` for level one, `---` for level
two. The setext spelling is where this chapter's
trap lives.

`examples/headings.md`, in full:

```
A paragraph about the spring fair
---

# A real top heading

## A second-level heading ##

Setext Heading One
==================

Some closing text.
```

## The `---` trap

The writer of that fixture probably meant the
`---` as a horizontal rule — a dividing line
under the first paragraph. There is no paragraph
there any more:

```
$ pandoc -f commonmark -t html examples/headings.md
<h2>A paragraph about the spring fair</h2>
<h1>A real top heading</h1>
<h2>A second-level heading</h2>
<h1>Setext Heading One</h1>
<p>Some closing text.</p>
```

A `---` line **directly under text** is a setext
underline, and it wins over the rule reading —
in CommonMark, in GFM, in pandoc's Markdown;
every capture in this guide agrees. A horizontal
rule is what you get from `---` with a blank line
above it, standing on its own between paragraphs.
The closing `#`s on the second-level heading are
stripped, as the capture shows, and the
`===`-underlined text is a level-one heading,
not a paragraph with ambitions.

## Anchors: the names headings get

Render a page as a complete document and the
headings acquire `id` attributes — the anchor
names that `#links` jump to. Pandoc's Markdown
and its GFM reader invent them identically on
this fixture:

```
<h2 id="a-paragraph-about-the-spring-fair">A paragraph about the spring
fair</h2>
<h1 id="a-real-top-heading">A real top heading</h1>
<h2 id="a-second-level-heading">A second-level heading</h2>
<h1 id="setext-heading-one">Setext Heading One</h1>
```

Lowercase, spaces to hyphens, punctuation
dropped. With `--toc`, those same names become
the table-of-contents targets — and the TOC
shows one more mechanical truth: it nests by
heading level, so the level-two heading this
file *opens* with sits at the top of the list,
outside the level-one section that follows it:

```
<li><a href="#a-paragraph-about-the-spring-fair"
id="toc-a-paragraph-about-the-spring-fair">A paragraph about the spring
fair</a></li>
<li><a href="#a-real-top-heading" id="toc-a-real-top-heading">A real top
heading</a>
<ul>
<li><a href="#a-second-level-heading" id="toc-a-second-level-heading">A
second-level heading</a></li>
</ul></li>
```

Start a document with an H2 and your contents
list starts mid-air. (These two blocks are
excerpts from the standalone pages; the lab
transcripts carry the full captures.)

Strict CommonMark, as a fragment, invents no
anchors at all — the first capture above has
bare `<h2>` tags. Anchors are a renderer
*feature*, not part of the text format.

## What this guide can't test for you

**GitHub's own slugger is documented-only
here.** GitHub generates its heading anchors
with its own code, on its own servers; there is
no copy of it in this lab, and the rule this
series lives by is that unrun behaviour is
labelled, not asserted. GitHub's documentation
describes anchors as lowercased, punctuation
removed, spaces replaced with hyphens — close
to what pandoc produced above — and the edge
cases where renderers differ (duplicate
headings, non-ASCII letters, leading numbers)
are exactly the cases where "close" stops being
good enough. If a link must land on a GitHub
heading, click the anchor GitHub itself offers
on the rendered page and copy that, rather than
deriving it by hand from anyone's rules,
including the ones in this chapter.

**Check:** before you link to `#some-heading`,
confirm the name against the rendered page you
are linking *to* — not against the algorithm
you remember.
