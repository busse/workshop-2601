# Pre-Presentation Punchlist

**Workshop:** Stop Typing, Start Orchestrating — 2026 RVATech Data & AI Summit
**Date:** March 26, 2026
**Last audited:** March 25, 2026

---

## P0 — Screenshot Placeholders in Slides

The slide deck originally had 5 placeholder boxes. Slides 4, 10, and 20 now have real screenshots. One placeholder remains:

- [x] **Slide 4** (slides.html line 381) — Real screenshot in place. ✓
- [x] **Slide 10** (slides.html line 450) — Real screenshot in place. ✓
- [x] **Slide 20** (slides.html line 585) — Real screenshot in place. ✓
- [ ] **Slide 27** (slides.html line 699) — Agent Teams split-pane view. _Short placeholder, narrow column._
  - Capture: screenshot of two terminal panes running concurrent Claude sessions, or find/create a conceptual diagram

**Decision needed:** Slide 27 might work better as a simple diagram or removed entirely in favor of the live demo. Your call.

---

## P1 — Presenter Prep (Not in repo, but called out in speaker notes)

- [ ] Prepare **fallback screenshots** of successful demo runs in a local folder (speaker-notes.md line 20). If Wi-Fi or the API goes down, you can show these instead of live demos.
- [ ] Run through the **pre-flight checklist** (speaker-notes.md lines 15-20):
  - Presentation loaded in Chrome, slide 1 visible
  - Terminal open in mini-crm, Claude Code NOT yet launched (launch live in Block 0)
  - Second terminal tab ready (empty) for Block 5
  - mini-crm freshly seeded
  - Exercise cards URL ready to share
  - Fallback screenshots prepared

---

## P2 — Stale Open Questions in demo-repo-spec.md

These were written before the repo was built but have since been resolved. Check them off or remove the section (lines 410-416):

- [ ] **Repo hosting** — Resolved: public repo at github.com/busse/mini-crm
- [ ] **License** — Resolved: MIT
- [ ] **Python version floor** — Resolved: 3.11+
- [ ] **Include .claude/commands/?** — Resolved: not included in demo repo

---

## P3 — Minor Polish

- [ ] **Verify QR code on slide 33** — Confirm it renders correctly at https://busse.github.io/workshop-2601/slides/#/33 after latest deploy. Was broken earlier (SVG path issue), fixed with PNG + relative_url.
- [ ] **Event link** — The RVATech event page (https://rvatech.com/rvatech-events/2026-rvatech-data-summit/) doesn't appear on any participant-facing page. Consider adding it to the landing page (index.md) or setup page if you want attendees to be able to find it.
- [ ] **Office hours page** — Review office-hours.md content and campaign banner in the layout. Confirm the donation link (pages.lls.org/voy/va/va26/cbusse) is live and correct.
- [ ] **Nav link for office hours** — The office-hours page exists but isn't in the nav (_includes/nav.html). Decide if it should be — the banner links to it, but there's no nav entry.

---

## Already Verified (No Action Needed)

These areas were audited and found complete:

- All participant-facing text (exercises.md, setup.md, index.md) — no placeholders, no TODOs
- All email addresses consistently `cbusse@singlestoneconsulting.com`
- All repo URLs consistently `github.com/busse/mini-crm`
- Event name consistently "2026 RVATech Data & AI Summit"
- Presenter name consistently "Chris Busse"
- LinkedIn (linkedin.com/in/chrisbusse) on closing slide and footer
- Navigation links all resolve to existing pages
- Exercise cards complete for all 4 blocks with stretch goals
- Speaker notes complete for all 34 slides with demo scripts
- QR code files exist (both SVG and PNG in assets/images/)
- reveal.js CDN links functional
- Jekyll config correct (baseurl, permalink, markdown settings)
