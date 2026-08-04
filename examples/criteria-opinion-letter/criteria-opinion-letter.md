# Criteria-and-Opinion Letter

**File:** [`criteria-opinion-letter.html`](criteria-opinion-letter.html) — open it in a browser, no install.

Worked example: a letter stating the engineering criteria that define a
stand-alone (off-grid) solar-powered lighting system, and an opinion that
anything meeting them falls in that class.

Every other module in this repo computes something. This one has no engine and
no numbers to verify. It is here because the framework is useful for documents
as well as calculations, and the document case has its own set of problems:
page fit, figures that print, and language that survives a client asking you to
soften it.

---

## The structure is the reusable part

| Section | Does what |
|---|---|
| 1 · Purpose | Says why the letter exists, in language a stranger can follow |
| 2 · Qualifying Criteria | Numbered conditions an item must meet |
| 3 · Opinion | "Anything meeting Section 2 is X" — bound to §2, not to a product |
| 4 · Basis and Limitations | What you did not do, and whose decision each remaining question is |
| Exhibit A | A figure showing one arrangement that qualifies |

That shape fits any letter asking an engineer what category something falls in
rather than whether a specific item passes a check — equipment classification,
code-path applicability, material equivalency, and so on. Swap the criteria and
the figure; the skeleton holds.

## Criteria letter vs. certification

A **certification** says *this product is X*. It obliges you to have examined
that product.

A **criteria letter** says *anything meeting these conditions is X*. It obliges
only that the criteria be sound.

The second lets you answer a classification question without reviewing,
endorsing, or disclosing any particular product — frequently what is actually
being asked, and a much smaller thing to put a seal on. It also lets a client
who is protective of their design get a useful document without handing over a
parts list.

That distinction only survives if the letter keeps its side of the bargain, so
the tool defends it rather than trusting you to remember at 11pm:

- **Name scan** — warns when an owner, requester, manufacturer or product name
  appears anywhere in the inputs. Populate `FLAGGED` with the names your letter
  must not contain.
- **Title check** — warns when the title looks like it names a company, because
  a title asserting *Company X's products qualify* contradicts §4 and is the
  first thing an opposing expert will pull on.
- **Financial/tax scope prompt** — reminds you to state that such
  determinations are not yours, if anyone downstream will be making one.

Please do not delete these when adapting the file.

## Four sketch archetypes

The figure offers four arrangements, sharing one small SVG helper set (`SVG`):

| Archetype | Shows |
|---|---|
| `pole_top` | Module above, battery on the shaft, luminaire on an arm |
| `bollard` | Low path light: module as cap, battery in the base |
| `remote` | Ground-mounted array, equipment enclosure, separate luminaire pole |
| `blocks` | Pure schematic — no physical form depicted at all |

They exist to make the same point the letter makes in words: criteria define a
class, not one product, and several arrangements satisfy them equally. Reach
for `blocks` when even an outline drawing would suggest a particular
manufacturer's product.

Adding one: write a `draw*()` returning `SVG.frame(W, H, body)` and register it
in `ARCHETYPES` with a `label` and a `caption`.

## Document-module features worth stealing

- **Auto-fit.** A US-Letter sheet is 1056 CSS px. Each page carries
  `min-height: 11in`, so content that overruns is *silently clipped* at print
  time. `autofit()` measures the laid-out pages and steps `--doc-size` down
  until they genuinely fit, then reports the size it landed on and warns if it
  could not. Type is sized in `em` throughout so one variable scales everything.
- **Print-exact pages.** `@page { size: 8.5in 11in; margin: 0 }` with in-flow
  flex footers. Print with **Margins: None** and **Scale: 100 %** — "Fit to
  page" is what makes output look shrunken and off-centre.
- **Three layouts.** Two-page letter + Exhibit A (default), two-page with the
  figure inline, or a one-page letter at roughly 9 pt.
- **Save/load inputs** as JSON, same convention as the calc modules, including
  the AI-provenance banner on files tagged `"source": "ai"`.

## Before using this on real work

- §4 as written is the minimum its author was willing to seal. It is not legal
  advice, and it is not tuned to your jurisdiction or your insurer. Have your
  own limitations reviewed — and expect a client to ask you to shorten them.
  A letter with no limitations section is a weaker document, not a stronger
  one; unqualified engineering opinions are read with more suspicion, not less.
- The financial/tax scope sentence is **off by default** here on purpose. Write
  your own if your matter needs one.
- The **DRAFT — UNVERIFIED** watermark defaults **on**. Leave it on until you
  have read every sentence and are prepared to seal what it says.
- Nothing in this file has been reviewed by anyone. You are the engineer of
  record. The tool is not, and neither is the AI that helped write it.
