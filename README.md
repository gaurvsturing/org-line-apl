# Apollo Engagement — Org Chart

An interactive, clickable org chart of the Apollo engagement, laid out as a
flowchart tree (Apollo root → connector lines → one expandable card per stream)
and styled with the **Turing.com design system** (`design.md`: Poppins, brand
blue `#2e6edf`, dark `#0f0f0f` hero with blue-glow shadow, card shadows).
Everything lives in a single file — `index.html` — no dependencies, no build
step, no server.

## How to use

- **Open it:** double-click `index.html`. All streams start expanded.
- **Click a stream card** to collapse/expand it in place. Inside, the hierarchy
  reads top-down like a reporting line: the **Apollo · Client Stakeholders**
  zone (light blue) sits on top, a connector line drops into the
  **Turing · Delivery Team** zone (white), which shows the **Tech Lead** first
  and then a line down to the **Team Members**. People appear as mini profile
  cards (avatar, name, title, role chip).
- **Click the Apollo root node** to expand/collapse all streams; the header
  also has Expand all / Collapse all buttons.
- **Click any person** to open the profile side panel: photo, title, role
  chips, bio, a LinkedIn button, and every stream they belong to. Clicking a
  stream row in the panel jumps to and opens that stream on the canvas.
- **Search** (top bar) highlights matching people, opens their streams, and
  dims everything else.
- **Drag** empty canvas space to pan; Esc closes the panel.
- The Turing logo (header) and Apollo Global Management logo (root node) are
  embedded as base64 data URIs from `../BFSI Web App/turing-logo.jpg` and
  `../BFSI Web App/Apollo-logo.png` — the file stays fully self-contained.
  To swap a logo, re-run a base64 replace or ask Claude.

## How to update the data

Open `index.html` and find the two data blocks at the top of the `<script>`:

**1. `PEOPLE`** — one entry per person. Fill in as you collect details:

```js
"Riya": {
  title: "Tech Lead",                          // shown under the name
  bio: "10+ yrs in fintech platforms…",        // blank = auto-generated from role
  linkedin: "https://linkedin.com/in/riya…",   // blank = greyed-out button
  photo: "photos/riya.jpg"                     // blank = initials avatar
},
```

Put photo files in a `photos/` folder next to `index.html` (square images look best).

**2. `STREAMS`** — who sits where:

```js
{
  name: "Finance — Quickwins",
  accent: "#2e6edf",                   // small dot + panel accent color
  members: [ { name: "Pradeep", role: "PM" }, { name: "Vaibhav" } ],
  techLeads: ["Riya"],                 // can be []
  stakeholders: [ { name: "Nikki", level: "L1" } ]  // level optional
}
```

## Sharing

Send `index.html` over Slack or email — it is fully self-contained (Poppins
loads from Google Fonts when online; falls back to Arial offline). To put it
on a URL, drop the file onto any static host.

## Data to collect for full executive polish

- [ ] Profile photos (square headshots → `photos/`)
- [ ] LinkedIn URLs
- [ ] Real titles and one-line bios
- [ ] Confirm L1/L2 stakeholder definitions and Ops — Quick Wins stakeholder coverage
- [ ] Tech Leads for Ops — Servstream, ACS, Data Engineering, CRE

## Notes on the source data

- Built from the stream staffing sheet shared on 2026-07-21.
- "Ali" appeared struck through under CoreAI in the source sheet, so he is excluded.
- The L1/L2 stakeholder list (Nikki/Ananya/Kaustubh, Matt/Rajeev) is assigned to
  Finance — Quickwins only; move entries in `STREAMS` if it should span more.
