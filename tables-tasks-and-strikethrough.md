# Tables, Task Lists, and Strikethrough

Everything in this chapter is an **extra** —
features GitHub added on top of CommonMark and
the world copied. None of them exist in strict
CommonMark, and watching strict CommonMark meet
them is the fastest way to learn what "flavour"
really costs. One fixture, `examples/flavors.md`:

```
## Spring tasks

- [x] Order seeds
- [ ] Sharpen the shears
- [ ] Book the hall

Old price ~~five pounds~~ now four pounds.

| Crop | Beds |
| --- | --- |
| Peas | 3 |
| Kale | 2 |

Visit www.example.org for the full list.
```

## Under GFM: everything works

```
$ pandoc -f gfm -t html examples/flavors.md
<h2 id="spring-tasks">Spring tasks</h2>
<ul class="task-list">
<li><label><input type="checkbox" checked="" />Order seeds</label></li>
<li><label><input type="checkbox" />Sharpen the shears</label></li>
<li><label><input type="checkbox" />Book the hall</label></li>
</ul>
<p>Old price <del>five pounds</del> now four pounds.</p>
<table>
...
<tr class="odd">
<td>Peas</td>
<td>3</td>
</tr>
...
</table>
<p>Visit <a href="http://www.example.org">www.example.org</a> for the
full list.</p>
```

Four extras, four behaviours: `- [x]` and
`- [ ]` become real checkboxes (an ordinary list
whose items start with those brackets), `~~…~~`
becomes `<del>`, the pipe block becomes a
`<table>`, and the bare `www.` address becomes a
link. A table, for reference, is a header row, a
separator row of dashes (colons in the separator
set column alignment, as the `:---:` family in
chapter 10's newsletter shows with `---:`), and
one line per row.

## Under strict CommonMark: a paragraph of pipes

```
$ pandoc -f commonmark -t html examples/flavors.md
<h2>Spring tasks</h2>
<ul>
<li>[x] Order seeds</li>
<li>[ ] Sharpen the shears</li>
<li>[ ] Book the hall</li>
</ul>
<p>Old price ~~five pounds~~ now four pounds.</p>
<p>| Crop | Beds | | --- | --- | | Peas | 3 | | Kale | 2 |</p>
<p>Visit www.example.org for the full list.</p>
```

Nothing failed; the features simply aren't in
the language this reader speaks. The checkboxes
are bracketed text in an ordinary list. The
strikethrough markers print. The table collapses
into a single paragraph of pipe characters —
which, in a rendered page, is what your readers
see: the table's contents, scrambled into prose.
The bare address stays unlinked. If a page of
yours ever renders like that last-but-one line,
you are looking at a table that met a renderer
without the table extension; the file is not
broken.

## The middle flavour

Pandoc's `commonmark_x` reader takes *some*
extras. On this fixture it renders the table and
the strikethrough, but the task list stays
bracketed text and the bare address stays bare:

```
$ pandoc -f commonmark_x -t html examples/flavors.md
...
<p>Old price <del>five pounds</del> now four pounds.</p>
<table>
```

"Mostly GFM" is a real category, and the only way
to know which extras a given renderer includes
is to test the ones you use. Pandoc's own
`markdown` reader, on this fixture, matches GFM
line for line.

## The escaped pipe

A table cell that needs a literal `|` in it
escapes it: `\|`. From `examples/pipe-table.md`:

```
| Item | Code |
| --- | --- |
| Gate key | A\|B |
```

Under GFM the escape keeps the row at two cells,
and the backslash disappears:

```
<td>Gate key</td>
<td>A|B</td>
```

Leave the backslash out and the row has three
cells in a two-column table — the classic cause
of a table whose last column silently drops or
shifts. Under strict CommonMark the same file is
again a paragraph of pipes; the escape is a GFM
rule for a GFM feature.

**Check:** count your table's cells in the
*rendered* page when a row looks wrong. The
separator row defines the truth; every row must
match it, escapes included.
