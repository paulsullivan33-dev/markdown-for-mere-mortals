# Paragraphs and Line Breaks

The first surprise in Markdown happens to almost
everyone in the first five minutes: you press
Enter at the end of a line, and the rendered
page runs the lines together anyway.

## A single Enter is not a break

A paragraph ends at a **blank line**. A lone
newline inside a paragraph is treated as a
space. From `examples/lines.md`:

```
Roses are red
violets are blue
this sentence runs onto the next line.
```

Both strict CommonMark and pandoc's Markdown
fold the three lines into one paragraph:

```
$ pandoc -f commonmark -t html examples/lines.md
<p>Roses are red violets are blue this sentence runs onto the next
line.</p>
```

(The renderer's line *wrapping* in that output
is cosmetic — the HTML is one `<p>` with no
break inside it.) This is deliberate: it lets
you wrap your source at any width without
changing the result. The price is that a
poem, an address, or a signature block typed
one line per line comes out as a single run-on
paragraph.

Quoted text behaves the same way inside a
blockquote — from `examples/bits.md`, the
two-line quote folds to one paragraph:

```
> Many hands make light work,
> especially in April.
```

```
<blockquote>
<p>Many hands make light work, especially in April.</p>
</blockquote>
```

## The two deliberate breaks

When you do want a break inside a paragraph,
Markdown gives you two spellings. You can see
both — and the invisible spaces one of them
depends on — with `cat -A`, where `$` marks each
line end (from `examples/hard-breaks.md`):

```
$ cat -A examples/hard-breaks.md
First line with two trailing spaces  $
second line after the break.$
$
Backslash break here\$
next line again.$
```

1. **Two trailing spaces** before the Enter.
   Fragile — editors love to strip trailing
   spaces, and you cannot see them — but
   universal.
2. **A backslash** at the end of the line.
   Visible in the source, and the spelling this
   guide recommends for that reason.

Both produce a real `<br />` under CommonMark
and under pandoc's Markdown:

```
$ pandoc -f commonmark -t html examples/hard-breaks.md
<p>First line with two trailing spaces<br />
second line after the break.</p>
<p>Backslash break here<br />
next line again.</p>
```

## Where the backslash stops working

The backslash break is a CommonMark-era
refinement; the original 2004 rules know only
the two-space form. In the strictest reader:

```
$ pandoc -f markdown_strict -t html examples/hard-breaks.md
<p>First line with two trailing spaces<br />
second line after the break.</p>
<p>Backslash break here\ next line again.</p>
```

The two spaces still break; the backslash is
printed as a literal `\` and the lines fold.
Modern renderers you are likely to meet —
anything CommonMark- or GFM-based — take the
backslash. A renderer built on the oldest rules
may not.

**Check:** if a break matters, do not trust
your eyes on the source file. Render it and
look for the `<br />`. And if a line ends with
two spaces you *didn't* put there, you now know
why the paragraph broke early.
