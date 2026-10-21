# Raw HTML

Markdown was born as a front end for HTML, and
it never locked the back door: you may write
actual HTML inside a Markdown file, and the
renderer passes it through. What happens to the
Markdown *between* your HTML tags is where the
flavours split. `examples/raw-html.md` asks the
question twice, two ways:

```
<div class="notice">
Bring your own *gloves* on Saturday.
</div>

<div class="notice">

Bring your own *gloves* on Saturday.

</div>
```

## Strict CommonMark: the blank line is the switch

```
$ pandoc -f commonmark -t html examples/raw-html.md
<div class="notice">
Bring your own *gloves* on Saturday.
</div>

<div class="notice">

<p>Bring your own <em>gloves</em> on Saturday.</p>
</div>
```

In the first block, with no blank lines, the
whole thing is one HTML block: the `*gloves*`
prints with its stars on, unparsed. In the
second, the blank lines end the HTML block, so
the middle line is read as Markdown again and
comes out as a proper paragraph with emphasis.
The div tags pass through untouched either way —
only the *contents'* treatment changes.

Rule of thumb for CommonMark and its kin: **an
HTML block runs until a blank line.** If your
Markdown inside a div renders with its stars
showing, the blank lines are missing, not the
stars wrong.

## Pandoc's Markdown: no switch needed

```
$ pandoc -f markdown -t html examples/raw-html.md
<div class="notice">
<p>Bring your own <em>gloves</em> on Saturday.</p>
</div>
<div class="notice">
<p>Bring your own <em>gloves</em> on Saturday.</p>
</div>
```

Pandoc's own reader parses Markdown inside block
HTML in *both* blocks, blank lines or none. Same
file, same tool, different reader — two answers.
Neither is a bug; they are different design
choices about how deep the Markdown layer goes,
inherited from different ancestors of the
format.

Two cautions that apply everywhere:

- **Not every renderer passes HTML through.**
  Some strip it or escape it, for safety: raw
  HTML in user-submitted text is an injection
  risk, and platforms that take Markdown from
  strangers commonly disable it. That is their
  documented policy where it applies; what your
  platform does is testable in one line — paste
  a `<b>test</b>` and see whether it bolds or
  prints.
- **HTML you write is HTML you maintain.** The
  div in this fixture survives rendering, but no
  Markdown tool will check it for you: an
  unclosed tag fails in the page, not in the
  source.

**Check:** stars showing inside a div? Count
the blank lines first — then ask which reader
you're on.
