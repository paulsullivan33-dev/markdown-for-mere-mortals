# Lists

Lists look too simple to have traps. They have
three: numbering that ignores the numbers you
typed, bullet characters that end one list and
start another, and the difference between a
*tight* list and a *loose* one. `examples/lists.md`
contains all three:

```
1. Clear the beds
1. Order the seeds
1. Plant the tomatoes

* One marker style
+ Another marker
- A third

- Outer item
  - Nested item
- Back to the top level
```

## Lazy numbering works

Every ordered item in that fixture is typed `1.`
The rendered list is numbered 1, 2, 3 under
every reader in this guide:

```
$ pandoc -f commonmark -t html examples/lists.md
<ol type="1">
<li>Clear the beds</li>
<li>Order the seeds</li>
<li>Plant the tomatoes</li>
</ol>
```

The numbers in the source are placeholders; the
renderer counts. (The *first* number is real —
a list starting `3.` renders starting at 3 in
CommonMark — a behaviour stated here from the
spec, and worth knowing; the lab fixture does
not exercise it.) Lazy numbering is a gift when
editing: insert an item anywhere, renumber
nothing.

## Changing the bullet changes the list

Under strict CommonMark, the fixture's three
bullet spellings are **three separate lists**:

```
<ul>
<li>One marker style</li>
</ul>
<ul>
<li>Another marker</li>
</ul>
<ul>
<li><p>A third</p></li>
<li><p>Outer item</p>
<ul>
<li>Nested item</li>
</ul></li>
<li><p>Back to the top level</p></li>
</ul>
```

A change of bullet character (`*` → `+` → `-`)
starts a new list. Then the two `-` groups merge
into one — and because the nested item makes
that list *loose*, every item's text is wrapped
in its own `<p>`, which most stylesheets render
with extra air around each item. Same dashes,
visibly different list.

Pandoc's Markdown reads the same bytes as **one
six-item list**, loose throughout:

```
$ pandoc -f markdown -t html examples/lists.md
<ul>
<li><p>One marker style</p></li>
<li><p>Another marker</p></li>
<li><p>A third</p></li>
<li><p>Outer item</p>
<ul>
<li>Nested item</li>
</ul></li>
<li><p>Back to the top level</p></li>
</ul>
```

Neither is buggy. They are different answers to
a question the 2004 page never asked sharply:
where does a list end? CommonMark answers "when
the marker changes"; pandoc's reader is more
forgiving.

Practical rules that survive both:

- Pick **one bullet character per list** and
  keep it; mixing `*`, `+`, and `-` is where the
  split happens.
- Indent nested items to line up under the
  parent item's text (two spaces for a `-`
  parent, as in the fixture) — under-indented
  nesting is the other classic way a list falls
  apart.
- A list that renders with unexpected gaps is
  probably *loose*: something — a nested list,
  a second paragraph in an item — has wrapped
  the items in `<p>` tags.

**Check:** the nested item in both captures sits
inside its parent `<li>`, not beside it. If your
render puts "Nested item" at the top level, the
indent is short — render, don't squint.
