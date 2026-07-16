# Architecture — Anatomy of an ephemeral-eng Tool

Every tool is **one HTML file** with the same skeleton. This document explains each piece and why it exists. Read alongside [`template/ephemeral-template.html`](../template/ephemeral-template.html), which implements all of it in ~600 commented lines.

## The one-screen mental model

```
┌────────────────────────┬──────────────────────────────────────┐
│  .form-panel (sticky)  │  .preview-panel                       │
│                        │   ┌──────────────────────────────┐    │
│  live-result  ← instant│   │ .diagram-card (screen only)  │    │
│  warn-banner  ← guard  │   │  live SVG of the thing       │    │
│                        │   └──────────────────────────────┘    │
│  <fieldset> Project    │   ┌──────────────────────────────┐    │
│  <fieldset> Geometry   │   │ .report-page  8.5 × 11 in    │    │
│  <fieldset> Section    │   │  THE DELIVERABLE             │    │
│  <fieldset> Criteria   │   │  (as it will print)          │    │
│  <fieldset> Exhibits   │   └──────────────────────────────┘    │
│  <fieldset> Options    │   ┌──────────────────────────────┐    │
│                        │   │ .report-page …               │    │
│  [Print/PDF] [Reset]   │   └──────────────────────────────┘    │
└────────────────────────┴──────────────────────────────────────┘
         @media print: left column vanishes → pages become the PDF
```

The entire framework is that diagram plus one loop:

```
input event → gather() → validate() → compute*() → render():
                                          ├─ live-result (instant DCRs)
                                          ├─ drawDiagram() (SVG)
                                          └─ buildReport() (the pages)
```

Every input fires `render()`. There is no "Calculate" button — the state of the screen is always the state of the answer. That's what makes it feel like engineering software instead of a form.

## Why each design decision

**Single file.** Portability (email it, archive it, open in 10 years), AI-friendliness (the whole tool fits in one context window — for both writing *and reviewing*), and honest versioning (`git diff` shows exactly what changed between Rev A and Rev B, formula included).

**Pure-function calc engine, no DOM.** `computeBeam(inp) → r` touches nothing on the page. This makes the engineering logic (a) testable in isolation — extract it and run it in Node against hand values, (b) reviewable as a contiguous block with units commented per line, and (c) safely editable without touching layout. This separation is the single most important convention: **the math never lives in the HTML.**

**Template-literal report.** `buildReport(d, r)` returns the pages as strings. Rebuilding the whole report on every keystroke sounds wasteful and is completely fine at this scale — and it guarantees the report can never be stale relative to the inputs. No two-way binding framework needed, which is the point: zero dependencies means nothing rots.

**Print CSS is the "export" feature.** `@media print` hides the form panel and diagram, strips shadows, and hard-sizes pages to 8.5×11 with `page-break-after:always`. `print-color-adjust:exact` keeps branding colors. The browser's own Print → Save as PDF is the entire output pipeline — battle-tested, universal, free.

**Substituted-numbers calc steps.** `.calc-step` blocks show `M = wL²/8 = 100 × 12²/8 = 1,800 lb·ft`, with the governing code section floated right (`.ref`). This exists for one reason: a plan reviewer (or the engineer of record, or a future you) must be able to check the printed report with a pencil, without ever opening the tool.

**`esc()` on all user text, `num()` on all numbers.** Project names contain ampersands; unescaped input breaks pages silently. `num()` centralizes precision and thousands separators so the report is typographically consistent.

**Brand tokens in one place.** All identity lives in the `:root` variables + the `FIRM` object. Re-branding a tool for a different firm is a 15-line edit that cannot affect the engineering.

**The draft watermark.** Default ON. It's the framework's cultural artifact: an unverified tool should *look* unverified. Turning it off is a deliberate act you take after completing [VERIFICATION.md](../VERIFICATION.md).

## The class vocabulary

Consistent names are what let an AI (or a colleague) open any tool in the family and immediately know where things are:

| Class | Role |
|---|---|
| `.form-panel` / `.preview-panel` | The two columns |
| `.field`, `.row-2`, `.row-3`, `.hint` | Input layout & unit hints |
| `.live-result`, `.warn-banner` | Instant feedback / input guards |
| `.report-page` | One printed US-Letter page |
| `.kv-table` (`lbl / sym / eq / val / unit`) | Inputs & properties tables |
| `.calc-step` (+ `.label`, `.ref`) | One worked calculation line with code citation |
| `.calc-table`, `.status-cell.pass/.fail`, `tr.compliance-*` | Summary table with DCR & PASS/FAIL |
| `.conclusion-box`, `.signature-block`, `.stamp-placeholder` | Closing block |
| `.img-frame`, `.file-drop` | Drag-and-drop photo exhibits |
| `.page-footer`, `.watermark`, `.version-badge` | Chrome & status |
| `.no-print` | Screen-only elements |

## Two families, one skeleton

- **Calculator/report** (this template): report pages are calc-first.
- **Letter generator**: page 1 is prose letterhead (purpose & scope → numbered findings → conditions of acceptance → conclusion), calculations move to an appendix exhibit, drag-drop images become numbered exhibits with cover pages. Identical slots, identical loop.

## State serialization (input JSON)

The report is regenerated from inputs, so **the inputs are the entire project state** — and the framework makes that state portable. Every tool ships `serializeInputs()` / `exportJSON()` / `importJSON()`:

- **Save inputs (.json)** walks every `id="f_*"` element (plus dropped logo/exhibit images) into a self-describing file with a `_meta` block (framework, tool name, tool version, timestamp, source).
- **Load inputs** restores that state, with guardrails: files from a *different tool* or *different version* trigger a review warning; unknown keys are skipped silently (so old files load into newer tool versions gracefully).
- **AI pre-generation:** because the schema is just the tool's input ids, an AI can read plan notes or an architect's email and emit the JSON directly. Such files must carry `"_meta.source": "ai"`, which makes the tool display a persistent *verify every value* banner until the engineer manually edits an input. Pre-filled ≠ verified — the chrome enforces the distinction.

This is the second half of the "ephemeral" thesis: the calculator can be disposable because the project state outlives it. Archive the JSON with the job; regenerate or upgrade the tool freely.

## Testing the engine outside the browser

Because the engine is pure, this works in any tool with Node:

```bash
node -e "
const fs=require('fs');
const html=fs.readFileSync('mytool.html','utf8');
eval(html.match(/function computeBeam[\s\S]*?\n}/)[0]);
console.log(computeBeam({L:12,w:100,b:1.5,d:9.25,Fb:1200,Fv:180,E:1.6e6,deflDen:240}));
"
```

Compare the output against your hand calc — that's checklist item A2 in [VERIFICATION.md](../VERIFICATION.md), automated.
