# One File, Four Renderers

Every chapter so far isolated one disagreement.
This one removes the isolation: a single
ordinary document — `examples/newsletter.md`, a
fictional garden club's monthly newsletter with
a table in it — through all four test beds at
once. Nothing in the file is exotic. That is
the point.

## Renderer 1 and 2: pandoc's Markdown and GFM — identical

The lab renders the newsletter under both
readers, saves the outputs, and diffs them:

```
$ diff work/n-pandoc.html work/n-gfm.html
[exit 0]
```

No output, exit 0: on this file, byte-for-byte
the same page — headings with anchors
(`id="riverbend-garden-club-newsletter"`), the
paragraph folded neatly, and the table rendered
as a table, alignment included:

```
<th style="text-align: right;">Beds</th>
```

(the source column separator was `---:`). For
mainstream prose-plus-a-table, the two dialects
most people actually use have converged.

## Renderer 3: strict CommonMark — the table goes

```
$ pandoc -f commonmark -t html examples/newsletter.md
<h1>Riverbend Garden Club Newsletter</h1>
...
<p>| Crop | Beds | Notes | | --- | ---: | --- | | Tomatoes | 4 | Needs
full sun | | Beans | 2 | Climbing variety |</p>
```

Two losses, both already met in earlier
chapters: no heading anchors (a fragment from a
strict reader carries bare tags), and the table
demoted to a paragraph of pipes, exactly as in
chapter 6. The lists, emphasis, and paragraphs
are indistinguishable from the GFM page. Strict
CommonMark is not a worse renderer — it is a
smaller language, and this file uses one word
of a dialect it doesn't speak.

## Renderer 4: Python-Markdown — a different animal

```
$ markdown_py examples/newsletter.md
<h1>Riverbend Garden Club Newsletter</h1>
...
<ul>
<li>Water the seedlings daily</li>
<li>Check the <strong>compost</strong> thermometer</li>
<li>
<p>Return borrowed tools by Friday</p>
</li>
<li>
<p>Clear the beds</p>
</li>
<li>Plant the tomatoes</li>
</ul>
<p>| Crop | Beds | Notes |
| --- | ---: | --- |
| Tomatoes | 4 | Needs full sun |
| Beans | 2 | Climbing variety |</p>
```

Read that list carefully. The fixture has three
bullets, a blank line, then a two-item numbered
list. Python-Markdown's default configuration
**folds the numbered items into the bullet
list** — "Clear the beds" and "Plant the
tomatoes" come out as the fourth and fifth items
of the one `<ul>`, two of its items gone loose
(wrapped in `<p>`) along the way. And
the table prints as literal pipe text (this
renderer keeps tables behind an extension that
is off by default; extensions are its own
configuration world, named here, not explored —
the lab runs it stock, as installed).

The diff against the GFM page is the lab's
loudest transcript line:

```
$ diff work/n-gfm.html work/n-pymd.html
...
[exit 1]
```

Six changed regions for a 30-line newsletter:
anchors, paragraph wrapping, the list merger,
the table. Two renderers, one file, no errors
anywhere — every program did exactly what its
own rules say.

## What to take from this

- **The file is not the document.** The document
  is the file *under a renderer*. Asking "is my
  Markdown right?" without naming the renderer
  is an unfinished question.
- **Convergence is real but partial.** The two
  pandoc readers agree completely here; the
  disagreements arrived with a smaller language
  (strict CommonMark) and a different lineage
  (Python-Markdown).
- **Test in the destination.** A README is read
  by GitHub's renderer, a note by your app's, a
  page here by MkDocs'. Preview where it will
  live — chapter 11 turns the surprises in this
  chapter into a checklist.
