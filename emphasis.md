# Emphasis

Emphasis uses two characters: `*star*` for
italic-shaped emphasis, `_underscore_` as the
alternative, and doubling either (`**bold**`)
for strong. The characters look interchangeable.
In the middle of a word, they are not — and the
flavours part company over it.

The fixture, `examples/emphasis.md`:

```
The word under_score_here stays plain.

The word mid*dle*star emphasises in the middle.

Use *stars* or _underscores_ for emphasis.
```

Under strict CommonMark:

```
$ pandoc -f commonmark -t html examples/emphasis.md
<p>The word under_score_here stays plain.</p>
<p>The word mid<em>dle</em>star emphasises in the middle.</p>
<p>Use <em>stars</em> or <em>underscores</em> for emphasis.</p>
```

Two rules are visible in that one capture:

- **Underscores refuse to work inside a word.**
  `under_score_here` comes out untouched. This
  is a CommonMark rule written on purpose: file
  names and identifiers like `snake_case_names`
  are full of underscores, and a spec that
  italicised their middles would vandalise
  technical writing.
- **Stars work anywhere.** `mid*dle*star`
  emphasises `dle` mid-word, because stars have
  no such protection.

Pandoc's own Markdown agrees with CommonMark on
this fixture, line for line. The original 2004
rules do not — in the strict reader, the
underscore rule disappears:

```
$ pandoc -f markdown_strict -t html examples/emphasis.md
<p>The word under<em>score</em>here stays plain.</p>
```

`under_score_here` comes out with its middle
italicised — the file-name vandalism CommonMark
was written to prevent. If you maintain text
that an older renderer will read, prefer stars
for emphasis and leave underscores to code.

## Getting the character back

A `\` before a punctuation character makes it
literal. From `examples/bits.md`:

```
Type \*not emphasis\* outside backticks.
```

renders as plain text, asterisks and all:

```
<p>Type *not emphasis* outside backticks.</p>
```

The same protection, stronger, comes from
backticks — chapter 8's code spans keep
`*not emphasis*` untouched even inside a
sentence. Between the two, a renderer should
never force you to *mean* a star.

**Check:** write `a_b_c` and `a*b*c` into your
own renderer's playground and see which one
emphasises. That one test tells you whether you
are on CommonMark-era rules or the 2004 ones —
and whether your `snake_case` words are safe.
