# Ephemeral Engineering

**Disposable calculators. Permanent deliverables.**

An open framework for building single-file, HTML-based engineering tools where **the calculation interface *is* the client deliverable.** Type your inputs on the left, watch the sealed-ready report render on the right, hit Print → PDF. One file. No Excel, no Word, no Mathcad, no subscriptions.

---

> ## ⚠️ ⚠️ ⚠️  READ THIS BEFORE YOU USE ANYTHING IN THIS REPO  ⚠️ ⚠️ ⚠️
>
> ### 🛑 THIS FRAMEWORK GENERATES CODE. CODE CAN BE WRONG. 🛑
>
> **Every tool built with this framework — whether written by you or by an AI — is
> UNVERIFIED until a licensed engineer checks every formula, every unit, every code
> reference, and every boundary condition BY HAND.**
>
> - ❌ **DO NOT** use this for anything you cannot independently verify.
> - ❌ **DO NOT** use this for complex analysis (FEA, dynamic, geotech, seismic systems, anything with coupled behavior). That's what validated commercial software is for.
> - ❌ **DO NOT** seal output from a tool you haven't personally verified against a hand calc or a known-good reference.
> - ✅ **DO** use it for small, simple, *palatable* calculations where your experience, judgement, and gut will immediately tell you if a number is wrong: a simple beam, a footing, a wind pressure, a fastener check.
> - ✅ **DO** run the full [VERIFICATION.md](VERIFICATION.md) checklist on every new tool and every revision.
>
> **You are the engineer of record. The AI is not. The framework is not. The HTML file is not.**
>
> The bet this framework makes is on the *trajectory*: today, frontier AI writes 95%-right engineering code and you supply the last 5% with rigorous verification. In five years, as AI reliability approaches flawless, the engineers who already work in an input-to-deliverable, AI-first workflow will be years ahead. Learn the framework now, on problems small enough to verify — so the habit of verification is built in before the stakes get bigger.
>
> Full terms: [DISCLAIMER.md](DISCLAIMER.md)

---

## The idea in one paragraph

Small structural calcs today take five apps: compute in Excel or Mathcad, sketch in CAD, write the letter in Word, assemble in Bluebeam, save the PDF. Every hand-off between apps is a chance to transcribe a number wrong. **ephemeral-eng collapses that into one artifact**: a single self-contained HTML file with an input panel on the left and a paginated, branded, code-referenced engineering report on the right. The report re-renders live as you type. Change the beam size, watch the PASS/FAIL flip. When it passes, the thing on your screen is already the deliverable — print it to PDF and you're done. And because an AI can write one of these files in minutes from a plain-English description, the calculator itself becomes *ephemeral*: cheap enough to generate per-project, per-condition, per-client — and reusable when you want it to be.

[docs/EphemeralSample.jpeg]

## What's the actual product here?

**Not the calculators. The mindset.** This repo gives you:

| Piece | What it is |
|---|---|
| [`template/ephemeral-template.html`](template/ephemeral-template.html) | A complete, working starter tool (simply-supported beam check) with every convention baked in — including the branding module: drag-drop your logo, type your firm name, pick your brand color, and the whole deliverable re-skins live. Open it in a browser right now — no install, no build step. |
| [`skill/ephemeral-eng/SKILL.md`](skill/ephemeral-eng/SKILL.md) | An AI skill file. Drop it into Claude (Skills), Claude Code, Codex, Cursor, or any agent, and say *"build me a spread footing calc using my ephemeral-eng skill."* The AI follows the conventions and hands you a consistent, deliverable-first tool. |
| [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) | The anatomy: the two-panel layout, the render loop, the print stylesheet, the class vocabulary, and *why* each piece exists. |
| [`VERIFICATION.md`](VERIFICATION.md) | The non-negotiable checklist you run before any tool touches real work. |
| [`examples/`](examples/README.md) | A second working example — an ASCE 7-22 door/window C&C wind calc whose engine is verified against its source repo's documented test cases — plus links to full production modules (fence, pergola, canopy, glass railing…) living in their own repos. This repo is the framework; modules are satellites. |

## Quick start (60 seconds)

1. Download [`template/ephemeral-template.html`](template/ephemeral-template.html).
2. Double-click it. It opens in your browser — that's the whole install.
3. Change the span. Watch the moment diagram, the DCRs, and the PASS/FAIL badges update live.
4. Hit **Print / Save PDF**. The input panel disappears; what prints is a paginated, letter-sized engineering report.
5. Hit **Save inputs (.json)** — that file is your whole project state. Try **Load inputs** with [`examples/sample-inputs-ai.json`](examples/sample-inputs-ai.json) to see how AI-pre-filled projects arrive (flagged for verification).
6. Open the file in a text editor (or hand it to an AI with the skill file) and swap in your own calculation.

## Why HTML? (the pitch to skeptics)

- **Zero dependencies.** One `.html` file runs on any machine with a browser, forever. No licenses, no cloud, no "please update to continue."
- **The UI is the deliverable.** Branding, colors, live SVG diagrams, tables, drag-and-drop photo exhibits — all print-perfect via one `@media print` stylesheet.
- **Instant iteration.** It behaves like engineering software: model different sizes, get instant yes/no. But you built it in an afternoon (or the AI built it in five minutes).
- **AI-native.** A single text file is the ideal medium for an LLM to write, read, review, and revise. Your whole tool fits in one context window — which also makes *verifying* it tractable.
- **Version-controlled engineering.** It's a text file. `git diff` your calculator between Rev A and Rev B and see exactly which formula changed. Try that with a spreadsheet.
- **Portable project state.** Every tool saves/loads its inputs as a small JSON file — archive it with the job, re-load it next revision, or have an AI pre-generate it from the architect's email so you review instead of type. (AI-generated files are flagged and the tool nags you to verify every value.)

## Scope: where this belongs (and where it doesn't)

**Good fit** — single-family residential and light commercial checks: beams, columns, footings, headers, wall bracing, wind pressures (ASCE 7 components & cladding), fastener/anchor checks, guardrails, canopies, evaluation letters.

**Bad fit** — anything where you can't eyeball the answer: FEA, nonlinear analysis, dynamic/seismic response, complex load paths, progressive collapse, anything life-safety-critical beyond your ability to hand-verify. Use validated commercial software and keep your gut in the loop.

## The workflow

```
┌─────────────┐    ┌──────────────────┐    ┌──────────────────┐    ┌─────────────┐
│  Describe    │ →  │  AI builds tool   │ →  │  YOU verify       │ →  │  Use forever │
│  the calc    │    │  from SKILL.md    │    │  (VERIFICATION.md)│    │  or dispose  │
│  in English  │    │  conventions      │    │  hand-calc check  │    │  and rebuild │
└─────────────┘    └──────────────────┘    └──────────────────┘    └─────────────┘
```

## Roadmap

- [ ] More seed modules (footing, header, uplift strap, anchor bolt)
- [ ] Brand-token generator (paste a logo + two hex colors → themed template)
- [ ] A `verify/` harness: paired hand-calc PDFs for each module's test cases
- [ ] Community module registry

## Contributing

PRs welcome — but every calculation module PR **must** ship with a worked verification example (hand calc or textbook reference) or it will not be merged. That's the culture here.

## License

MIT — see [LICENSE](LICENSE). The MIT license's warranty disclaimer is not a formality in this repo; it is the entire point. See [DISCLAIMER.md](DISCLAIMER.md).
