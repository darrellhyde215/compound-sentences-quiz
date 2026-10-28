# Clause & Effect

A single-file browser study game for **compound sentences** — the three ways to join
two independent clauses: coordinating conjunctions (FANBOYS), adverbial conjunctions
(HOTSHOTCAT), and a semicolon.

Open `index.html` in any browser. No install, no network, no build step.

- **Pick your content** — study one section or all of them. The choice is remembered on
  the device, and a URL hash preselects a section (`index.html#fanboys`).
- **Play** — 59 questions: multiple choice, true/false, pick-every-right-answer,
  type-ins, and click-the-punctuation. Points, streak bonus, a second pass over
  whatever was missed, and a per-section score breakdown when more than one is picked.
- **Study guide** — every rule and example on one scrollable page.
- Keyboard: `1`–`9` to pick, `Enter` to check / advance. Light + dark theme.

The four sections:

| id | section | what it drills |
| --- | --- | --- |
| `rules` | The 3 Ways | what a compound sentence is, what an IC is, which punctuation goes with which method |
| `fanboys` | FANBOYS | the seven coordinating conjunctions and the comma-before rule |
| `hotshotcat` | HOTSHOTCAT | the ten adverbial conjunctions and the semicolon-before/comma-after rule |
| `practice` | Spot & Fix | the two practice sets — is it compound, and how do you fix it |

Answers follow the slide deck's own answer keys.

## Adding questions later

Everything lives in `index.html`, in the `DECKS` array near the bottom. One entry per
section: `id` (also the URL hash), `chip` (picker label), `title`, `bank`, `study`.
Adding another section means appending another deck — no logic changes.

- `bank` — the questions. `n` is the slide it came from, and `type` is one of:
  - `mc` — `opts: [...]`, `a: <index of the right one>`
  - `tf` — `a: true | false`
  - `multi` — `opts: [...]`, `a: [indexes of every right one]` (all must be picked)
  - `type` — `accept: ["answer"]`, optional `hint`; matching ignores case and punctuation
  - `spot` — `tokens: [...]`, `a: [indexes]`; the sentence renders as clickable chips and
    the student clicks the punctuation and conjunction that join the clauses
  - every item needs a `why`, shown after answering
- `study` — the study-guide view: sections of `[term, definition]`, with an optional third
  element `[...]` that renders as chips.

Option order is shuffled at runtime, so write `a` against the order in `opts`.
`spot` tokens are **not** shuffled — they render in order, so `a` is a position in the
sentence.

## Testing

`test/drive.html` plays the whole game in a headless browser and checks every grade,
including a deliberate wrong answer of each type to prove misses are caught. It also
validates every answer key against its own options before playing. The command is in a
comment at the top of that file. Any `FAIL` line in the output is real.

It must be run from a `file://` URL — a cross-origin https page blocks iframe access, so
it cannot test the live site. To check a deploy instead, `curl` the Pages URL and compare
its SHA to the local `index.html`.

---

Built from a classroom slide deck, *Compound Sentences PD Notes*. The lesson, examples and
practice sentences belong to their author and are used here for personal study only.
Not affiliated with or endorsed by the author.
