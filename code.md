# Code

Code is where Markdown stops interpreting, and
that is precisely its value: inside code, the
characters that mean things everywhere else —
stars, hashes, brackets — are inert.
`examples/code.md` holds the three forms:

````
Run the gate check first:

    python3 check_gate.py --beds 4

Then the fenced version:

```python
def water(beds):
    return beds * 2
```

And a fence with no language:

```
plain output here
```
````

## Code spans: backticks inside a sentence

One pair of backticks makes a **code span**. From
`examples/bits.md`:

```
<p>The command is <code>water --beds 4</code> in the shed book, and
<code>*not emphasis*</code> inside backticks.</p>
```

The second span is the point: `*not emphasis*`
inside backticks stays starred text, where the
same characters outside would emphasise (and a
backslash escape, chapter 3, is needed). Spans
are for commands, filenames, and short fragments
inside prose.

## Indented blocks

Four spaces at the line start make an **indented
code block** — the oldest form, inherited from
the 2004 rules:

```
<p>Run the gate check first:</p>
<pre><code>python3 check_gate.py --beds 4</code></pre>
```

Plain `<pre><code>`, nothing more. Its weakness
is social: in an editor, four leading spaces are
easy to mistake for list indentation, and the
block can't start a paragraph without a blank
line before it.

## Fenced blocks, and what the language name buys

Three backticks open a **fenced block**; the
word after them — the **info string**, usually
a language name — is information *for the
renderer*:

```
<div class="sourceCode" id="cb2"><pre
class="sourceCode python"><code class="sourceCode python">…
```

The `python` fence comes back wrapped as source
code *labelled* python, and pandoc's HTML output
goes further: the code inside is syntax-
highlighted, token by token, in `<span>`
elements (the full capture, in the lab
transcript, shows `def` and `return` wrapped as
keyword spans). The fence with no info string
gets the same plain treatment as the indented
block:

```
<pre><code>plain output here</code></pre>
```

So the info string changes nothing about the
*text* — the code is identical either way — and
everything about the presentation: a class to
style by, and highlighting where the renderer
offers it. (What other renderers do with the
info string varies by their own feature lists;
the captured behaviour here is pandoc's HTML
writer.) Fenced blocks also win on ergonomics:
no indent to miscount, and a block can hold
lines that themselves start with spaces.

CommonMark and pandoc's Markdown produced
identical output on this whole fixture — code,
at least, the flavours agree on.

**Check:** if a code block renders as a paragraph
with the backticks showing, the fence is short a
backtick or the opening fence has trailing text
the renderer didn't accept. Render a minimal
three-line fence and work back up.
