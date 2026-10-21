# Writing Criteria

Every guide in this repo is written to the same
standard. If you're adding or editing a guide —
human or AI — hold it to these.

1. **Plain words, real ideas.** Simple language,
   never dumbed-down concepts. Explain jargon on
   first use; collect terms in the glossary.
2. **No hype.** No marketing adjectives, no
   "revolutionary," no promises about what
   something will do for the reader.
3. **Honest about limits.** Say what the thing
   *can't* do. State uncertainty instead of
   smoothing it over. Validation notes include
   what remains unverified.
4. **No invented numbers.** Benchmarks, defaults,
   and specs are either measured or qualified with
   "depends on your setup." If it wasn't tested,
   say so.
5. **Checkable.** Commands are meant to be run,
   with "Check:" blocks showing what success looks
   like. Sources are linked, not asserted.
6. **Respect the reader's setup.** Call out
   Windows/Mac/Linux differences. Don't assume a
   GPU, a budget, or prior experience.
7. **Safety isn't skipped.** Real risks get
   stated plainly, not buried.
8. **Scoped.** Each guide says what it covers and
   points elsewhere for the rest. No guide
   pretends to be the whole subject.
9. **Structure over prose.** Tables, before/after
   examples, symptom → fix. Scannable beats essay.

## Verification notes for this guide

Standard 3 and 4 applied to this guide,
specifically. The renderers under discussion are
**pandoc 3.1.3** (readers `markdown`,
`commonmark`, `gfm`, `commonmark_x`, and
`markdown_strict`, HTML writer) and
**Python-Markdown 3.11.1** (`markdown_py`, stock
configuration), both run on the build machine.
Every quoted output is a capture from one of
those two programs. Working transcripts are kept
with the build (`markdown-lab/transcripts/`,
twelve files, `t01`–`t12`, produced by the
harness `markdown-lab/run-lab.sh`; the two diffs
in `t11` are echoed and run by
`markdown-lab/render-compare.sh`).

**The lab.** Fixtures are the files in
`examples/` — a fictional garden club's
newsletter and small purpose-built specimens
(line breaks, emphasis, headings, lists, links,
raw HTML, code, inline bits, a pipe-escape
table) — invented for this guide, kept pristine
in the lab, and rendered read-only: no capture
in the guide comes from a file the lab modified.
Byte-level details the chapters depend on (two
trailing spaces; a trailing backslash) are
proven in `t01`/`t02` with `cat -A` rather than
asserted.

**Verified by running, per chapter:**

- *Ch. 1:* `pandoc --version` (3.1.3);
  `markdown_py --version` (3.11.1);
  `pandoc --list-input-formats` showing the five
  readers used, quoted as an excerpt.
- *Ch. 2:* the three-line paragraph folding to
  one `<p>` under `commonmark` (and identically
  under `markdown`); the blockquote's two lines
  folding the same way (`t12`); two trailing
  spaces and a trailing backslash each producing
  `<br />` under `markdown` and `commonmark`;
  under `markdown_strict` the spaces still
  breaking while the backslash prints literally
  and the lines fold.
- *Ch. 3:* intraword `_` left plain and
  intraword `*` emphasising under `commonmark`
  and `markdown`; `markdown_strict` emphasising
  the underscore word's middle
  (`under<em>score</em>here`); the `\*` escape
  printing literally (`t12`).
- *Ch. 4:* `---` directly under a paragraph
  rendering as `<h2>` with no `<hr>` anywhere;
  the `===` setext H1; closing ATX hashes
  stripped; pandoc heading ids
  (`a-paragraph-about-the-spring-fair` and
  friends) **identical** under `markdown` and
  `gfm`; the `--toc` list nesting the
  second-level heading under the H1 and leaving
  the opening H2 at top level.
- *Ch. 5:* a list typed `1.` three times
  rendering as items 1–3 under both pandoc
  readers; `commonmark` splitting the `*`/`+`/`-`
  bullets into three separate `<ul>`s and merging
  the two `-` groups into one loose list
  (`<p>`-wrapped items), where `markdown` reads
  one six-item loose list; nesting landing
  inside the parent `<li>` both ways.
- *Ch. 6:* under `gfm`, task-list checkboxes
  (`checked=""` on the done item), `<del>` for
  `~~…~~`, a real `<table>`, and the bare
  `www.example.org` autolinked; under strict
  `commonmark`, all four absent — the table as
  one paragraph of pipes; under `commonmark_x`,
  table and strikethrough present, task list and
  autolink absent; pandoc `markdown` matching
  `gfm` on the fixture. The escaped pipe
  (`t07`): `A\|B` yielding one cell reading
  `A|B` under `gfm`.
- *Ch. 7:* the reference link resolving with its
  `title` attribute, the definition line
  producing no output, and the undefined
  reference printing byte-for-byte literally —
  identical under `commonmark` and `markdown`;
  the image as a bare `<img>` in a `<p>` under
  `commonmark`, and wrapped in
  `<figure>`/`<figcaption>` under `markdown`.
- *Ch. 8:* code spans protecting `*not emphasis*`
  verbatim (`t12`); the indented block and the
  language-less fence both rendering as plain
  `<pre><code>`; the `python` fence rendering
  as a `sourceCode` block with the language as
  its class and keyword highlighting spans in
  the body; `commonmark` and `markdown`
  identical on the whole fixture.
- *Ch. 9:* under `commonmark`, Markdown inside
  the un-blank-lined `<div>` left raw (stars
  printed) and parsed after blank lines; under
  pandoc `markdown`, parsed in both blocks.
- *Ch. 10:* the newsletter under four renderers
  — `markdown` vs `gfm` proven identical by a
  `diff` that exits 0 with no output;
  `commonmark` losing the anchors and the table;
  `markdown_py` losing the table (stock
  configuration, extensions off), producing no
  anchors, and folding the two numbered items
  into the bullet list as items four and five,
  two items loose; the `gfm`–`markdown_py` diff
  exiting 1 with six changed regions.

**One claim is stated from the spec, not the
lab,** and chapter 5 labels it in place: an
ordered list's *first* number is honoured as its
start in CommonMark. The fixture exercises lazy
numbering only; the start-number behaviour is
CommonMark spec text, quoted as such.

**Capture hygiene (declared trims):**
chapter 4 quotes the body lines and the TOC
list from the `--standalone` pages rather than
the full documents — the transcripts carry the
pages entire, stylesheet and all, and the
chapter says the blocks are excerpts. Chapter
6 shortens two table captures with a marked
`...`. Chapter 8 quotes the opening of the
highlighted code block and describes the
highlight spans rather than reprinting the full
span markup; `t10` carries it entire. The
`[exit N]` lines in transcripts are the
harness's annotations, and the two diff exit
codes (0 and 1) are the evidence, quoted as
such. No output line was altered.

**Documented-only (not run), and why:**

- *GitHub's live renderer and heading slugger.*
  It runs only on GitHub's servers; no local
  copy exists to capture. Chapter 4 names the
  documentation's description (lowercase,
  punctuation removed, spaces to hyphens) as
  documentation, and advises copying anchors
  from the rendered page for the edge cases —
  duplicate headings, non-ASCII text, leading
  numbers — where implementations diverge.
- *App dialects.* Obsidian, VS Code's preview,
  chat clients, wikis, and MkDocs' own renderer
  each implement a private flavour. They are
  named as a category; none is characterised
  beyond what the four test beds demonstrate,
  because none could be run in this lab.
- *Python-Markdown's extensions.* The renderer
  was run stock, as installed
  (`markdown_py fixtures/newsletter.md`). Its
  extension system — which includes a tables
  extension — is named in chapter 10 and not
  exercised; the guide's claims are about the
  default configuration only.
- *The remaining pandoc readers*
  (`markdown_github`, `markdown_mmd`,
  `markdown_phpextra`) — listed in chapter 1
  from `--list-input-formats`, not sampled.
- *Rendering to anything but HTML.* Word,
  ebook, PDF, and slide outputs belong to the
  series' Pandoc guide; they are not claimed
  here, and flavour behaviour in those writers
  is not asserted.

Specimen discipline, for the record: every name,
club, and value in the fixtures is invented for
the guide; no real organisation, system, or
person appears. The lab ran entirely on local
files, with no network, service, or account.
