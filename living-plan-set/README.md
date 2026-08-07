# Living Plan-Set

A single-file HTML template that works as **both a document and a presentation** — styled like an engineering plan set: title block, sheet numbers, drafting-red stamps, SVG flowcharts, and a revision table that makes every printed copy visibly obsolete.

Built for professionals who deliver knowledge to clients: engineers, architects, consultants, lawyers. One file. No build step. No dependencies except Google Fonts.

## Why

- **One artifact, two modes.** Scrolls like a document; the "Present full screen" button turns each sheet into a slide (swipe on tablet, arrow keys on desktop, ESC to exit).
- **Living, not static.** Host it on your own domain. Edit the file, bump the revision table — every stale printout is superseded by design.
- **You control the deliverable.** Unlisted URL + `noindex` for client work; pull the file and the deliverable ceases to exist. Delete the `noindex` line and it's a public marketing page.
- **LLM-native.** It's plain HTML/CSS/SVG. Describe a change to any AI assistant and paste the result.
<img width="747" height="1408" alt="image" src="https://github.com/user-attachments/assets/a12962c0-2533-4a4e-a71e-3fc152371d25" />

## Quick start

1. Copy `template.html` (full demo of every component) or `example-minimal.html` (bare skeleton).
2. Replace the title-block placeholders (firm, client, doc number, stamp).
3. Duplicate `<section class="sheet">` blocks for each sheet; add a matching row to the INDEX table.
4. Upload to your web host; open in any browser. On iPad: Safari → AirPlay to a TV → tap **Present**.

## Component cheat-sheet

| Component | Markup | Use for |
|---|---|---|
| Sheet | `<section class="sheet" id="x"><div class="sheet-head"><div class="sheet-no">X-01</div><h2>Title</h2></div><div class="body">…</div></section>` | One topic = one sheet = one slide |
| Cards | `div.cards` > `div.card` (+ `bad` red / `go` green) | 3-across stat/option cards |
| Hidden detail | `class="detail"` on any element | Visible in document, hidden in Present mode |
| Takeaway box | `div.bottomline` | Navy "bottom line" per sheet |
| Hard-limit box | `div.redline` | Non-negotiables; use sparingly |
| Figure | `div.fig` > inline `<svg>` + `div.figcap` | Flowcharts, timelines (patterns in D-01) |
| Matrix | `table.matrix` in `div.scroll`, tags `span.tag.yes/.no/.cond` | Comparisons |
| Revisions | `table.rev` | Version control + supersession clause |
| Stamp | `div.stamp` | DRAFT / PRELIMINARY / rotate & recolor |

## Design tokens (edit in `:root`)

| Variable | Default | Role |
|---|---|---|
| `--ink` | `#1F4E79` | Brand navy — headers, sheet numbers |
| `--graphite` | `#26282B` | Line work, body text |
| `--paper` | `#FBFBF9` | Page background (with grid) |
| `--stamp` | `#B3392E` | Drafting red — stamps, warnings, dead ends |
| `--go` | `#2E6E4E` | Viable green — outcomes, milestones |
| `--hold` | `#8A6D1F` | Caution amber — conditional states |

Fonts: **Barlow Condensed** (display/title-block caps), **Source Sans 3** (body), **IBM Plex Mono** (labels, sheet numbers, tables).

## Revision workflow

1. Edit content.
2. Change the title-block `Rev N — Mon YYYY` cell.
3. Mark the old `table.rev` row `SUPERSEDED`; add the new row as `CURRENT`.
4. Update the footer doc string. Save. Done — anyone holding a printout now holds an identified stale copy.

## Client vs. public deployment

| | Client deliverable | Public page |
|---|---|---|
| `<meta name="robots" content="noindex,nofollow">` | keep | delete (add a meta description) |
| URL | unlisted path | indexed path, linked from site |
| Disclaimer band | engagement-specific terms | "general information, not advice" |
| Content | client facts allowed | **strip all client-identifying facts** |

## Disclaimer

This is a formatting template only. All content in the demo files is illustrative placeholder text and is not engineering, legal, or professional advice. You are responsible for the content, disclaimers, and confidentiality of anything you publish with it.

## License

MIT — see `LICENSE`.
