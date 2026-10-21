# Links and Images

Links are core Markdown — every flavour in this
guide renders them — and they still manage three
surprises: a definition that produces no output,
a reference that silently doesn't, and a web
address that links itself in one flavour and not
another. `examples/links.md`:

```
Read the [planting guide][guide] before April.

An [undefined reference][missing] stays literal.

An inline [link](https://example.org/guide) works too.

[guide]: https://example.org/planting "Planting Guide"
```

## Two ways to write a link

The **inline** form carries its address with it:
`[link](https://example.org/guide)`. The
**reference** form names the address —
`[planting guide][guide]` — and a *definition*
elsewhere in the file supplies it, with an
optional quoted title. Both render, identically
under CommonMark and pandoc's Markdown:

```
$ pandoc -f commonmark -t html examples/links.md
<p>Read the <a href="https://example.org/planting"
title="Planting Guide">planting guide</a> before April.</p>
<p>An [undefined reference][missing] stays literal.</p>
<p>An inline <a href="https://example.org/guide">link</a> works too.</p>
```

Three facts in that capture:

- The definition line at the bottom of the file
  **produces no output at all**. It is not a
  footnote; it is plumbing, and it vanishes.
- The title becomes the link's `title` attribute
  — the hover text.
- The **missing reference stays byte-for-byte
  literal**, brackets and all, with no error.
  Reference links fail silently by design: a
  typo in the label, or a definition deleted in
  an edit, leaves prose that *looks* like a link
  in your source and isn't one on the page.

Reference style earns its keep when the same
address recurs or the address is long enough to
wreck the paragraph's readability in source
form. Inline style earns its keep by failing
visibly — a broken inline link is broken in the
source too.

## Addresses that link themselves

A bare `www.example.org` in the text is not a
link in core Markdown. GFM links it anyway
(chapter 6's capture): `<a href="http://www.example.org">`.
Strict CommonMark leaves it plain. Whether an
autolink is a convenience or an ambush depends
on whether you meant it — if a filename or a
version string in your text ever turns blue
unexpectedly, an autolinking flavour is why.

## Images

An image is a link with a `!` in front:
`![alt text](file)`. The alt text — the words
for screen readers and broken-image boxes —
goes in the brackets. From `examples/bits.md`,
strict CommonMark:

```
<p><img src="shed.png" alt="The tool shed in spring" /></p>
```

Pandoc's own Markdown reader gives the same
standalone image an upgrade:

```
<figure>
<img src="shed.png" alt="The tool shed in spring" />
<figcaption aria-hidden="true">The tool shed in spring</figcaption>
</figure>
```

A `<figure>` with the alt text reused as a
caption — nicer pages, and a real divergence if
you are diffing two renders and wondering where
the extra markup came from. Neither capture
proves anything about the image itself, of
course: Markdown points at the file, and whether
`shed.png` exists is the filesystem's business,
not the renderer's.

**Check:** click every reference link in the
rendered page, not the source. The failures are
silent, literal, and bracket-shaped.
