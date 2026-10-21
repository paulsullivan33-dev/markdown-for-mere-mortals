# When It Renders Wrong

Every entry here is a trap this guide sprang in
the lab, restated as a symptom. Read down the
left column until one matches your page.

| What you see | What happened | Fix |
| --- | --- | --- |
| Lines run together into one paragraph | Single newlines are spaces in Markdown (ch. 2) | Blank line between paragraphs; two trailing spaces or a trailing `\` for a break inside one |
| A paragraph becomes a heading; the dividing line vanishes | `---` directly under text is a setext H2 underline (ch. 4) | Put a blank line above the `---` so it stands alone as a rule |
| A table prints as a paragraph of pipe characters | The renderer has no table extension — strict CommonMark, or Python-Markdown stock (ch. 6, 10) | Use a GFM-capable renderer, or accept prose and rewrite the table as a list |
| One row of a table is short a cell, or the last column shifts | An unescaped `|` inside a cell (ch. 6) | Write it as `\|` |
| `- [ ]` prints as literal brackets | Task lists are a GFM extra this renderer doesn't include — even `commonmark_x` declined them (ch. 6) | Render with GFM, or drop the brackets |
| Bullet list splits into several lists, or gains odd spacing | Bullet character changed mid-list (CommonMark starts a new list), or the list went loose (ch. 5) | One bullet character per list; expect `<p>`-wrapped items once a list is loose |
| Numbered list merges into the bullets above it | Renderer-specific list handling — captured from Python-Markdown (ch. 10) | Test in the destination renderer; a blank line alone did not save this one |
| `snake_case` words come out with italics in the middle | An original-rules renderer: underscores emphasise intraword there (ch. 3) | Prefer `*stars*` for emphasis in text old renderers will read |
| Emphasis works with stars but not underscores in a word | CommonMark's underscore protection — working as designed (ch. 3) | Use stars mid-word, or leave the underscores to code |
| A "link" prints with its brackets showing | A reference link whose definition is missing or mislabelled (ch. 7) | Find or fix the `[label]:` definition; failures are silent |
| Stars print literally inside a `<div>` | The HTML block hasn't ended — no blank line (CommonMark), or the platform strips/parses HTML its own way (ch. 9) | Blank lines around the Markdown inside HTML blocks |
| An image gains a caption you didn't write | The renderer wraps standalone images in `<figure>` and reuses the alt text — pandoc's Markdown does (ch. 7) | Expected behaviour there; put the image inline in a paragraph if the figure is unwanted |
| Code renders as a normal paragraph, backticks showing | A fence is short a backtick, or trailing text follows the opening fence (ch. 8) | Three clean backticks to open, three to close |
| A `#heading-link` you wrote by hand goes nowhere | Anchor names are invented per renderer, and the live slugger's edge cases are its own (ch. 4) | Copy the anchor from the rendered page itself |

Two habits sit underneath the whole table:

1. **Name the renderer before you debug the
   file.** Half of these rows are not file bugs
   at all; they are dialect differences, and no
   edit to the file fixes a feature the renderer
   doesn't have.
2. **Render small.** One fixture line at a
   time, like the lab did — `pandoc -f <flavour>
   -t html` on a five-line file answers in a
   second what an hour of squinting at the full
   page won't.

**Check:** the one test that separates most of
this table's rows: take the failing lines alone
into a scratch file and render under `-f gfm`
and `-f commonmark`. If the outputs differ, you
have a dialect issue; if they agree and it's
still wrong, you have a file issue.
