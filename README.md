# Apollo Engagement — Org Chart

An interactive, clickable org chart of the Apollo engagement, laid out as a
flowchart tree (Apollo root → connector lines → one expandable card per stream)
and styled with the **Turing.com design system** (`design.md`: Poppins, brand
blue `#2e6edf`, dark `#0f0f0f` hero with blue-glow shadow, card shadows).
Everything lives in a single file — `index.html` — no dependencies, no build
step, no server.

## How to use

- **Open it:** double-click `index.html`. All streams start expanded.
- **Apollo hierarchy is intertwined with each workstream:** inside a stream's
  Apollo zone, every stakeholder's reporting chain is drawn above them as a
  connected tree (e.g., CRE shows John Cortese → Jason D'Silva → Atul Singh →
  Nicholas Pollari). **Apollo Leadership** (managers above the stakeholders)
  render as dashed cards with indigo avatars — distinct from the solid
  dark-avatar stakeholder cards — and have their own legend entry in the header. The **"Apollo hierarchy"** header
  button switches to a standalone tree of the full client organization;
  clicking again returns to the streams.
- Clicking anyone in the hierarchy opens their profile panel, which shows
  their **Reporting Line** (clickable chain up to the top) and **Direct
  Reports**, alongside any streams they're attached to.
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
- **Search** (top bar) highlights matching people, opens their streams, dims
  everything else, and **auto-scrolls the canvas to the first match** (after
  2+ characters). Press **Enter** to cycle through all matches — handy for
  people who appear in several streams.
- **Drag** empty canvas space to pan; Esc closes the panel.
- **Mobile friendly:** on phones the header stacks (search gets its own row,
  legend hides), the profile panel opens full-screen, and the canvas pans
  with native touch scrolling in both directions; pinch-zoom works too.
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
  stakeholders: [ { name: "Nikki", level: "L1" } ]
}
```

Stakeholder `level` (L1/L2) is legacy and no longer affects rendering — the
in-stream hierarchy now comes entirely from `APOLLO_REPORTING`.

**3. `APOLLO_REPORTING`** — the client org: `person -> direct manager`
(`null` = top of the visible hierarchy). Drives the reporting tree inside each
stream's Apollo zone, the standalone "Apollo hierarchy" toggle view, and the
"Reporting Line" / "Direct Reports" panel sections. Add a new leader by adding
their PEOPLE entry plus one line here; stream cards widen automatically.

## Sharing

Send `index.html` over Slack or email — it is fully self-contained (Poppins
loads from Google Fonts when online; falls back to Arial offline). To put it
on a URL, drop the file onto any static host.

## Data to collect for full executive polish

- [ ] Profile photos (square headshots → `photos/`)
- [ ] LinkedIn URLs
- [ ] Real titles and one-line bios
- [ ] Tech Leads for Ops — Servstream, ACS, Data Engineering, CRE

## Notes on the source data

- Built from the stream staffing sheet shared on 2026-07-21.
- "Ali" appeared struck through under CoreAI in the source sheet, so he is excluded.
- The stakeholder group (Nikki, Ananya, Kaustubh, Matt, Rajeev) applies to both
  Finance — Quickwins and Ops — Quickwins, per Gaurav's confirmation.
- Apollo hierarchy comes from the client reporting table (2026-07-21).
  **Rajeev Kollara is Apollo Leadership** (not a stream stakeholder): he
  appears in the Quickwins chains above Kaustubh and reports to John Hack.
  Full names adopted for Juan Surgeon, Abdul Goffar, Swapnil Daptardar;
  "Niki"/"Anany" in the table are Nikki/Ananya. Stephen Olano's reporting
  line was not in the table — he shows without a chain until provided.
