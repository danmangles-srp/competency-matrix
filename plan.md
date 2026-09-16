# Plan — SRP Skill Tree (career-coaching web app)

## What it is
A one-page web app that renders the `reviewed-matrix.md` behaviours as a **Skyrim-style skill
tree**. Leaders use it live in 1:1 career-coaching sessions: see where a managee sits on each
behaviour, mark progress, and capture notes — one constellation per category.

## Principles
- **Super simple.** Single self-contained `index.html`. No build, no server, no dependencies,
  no accounts. Double-click to open.
- **Data mirrors `reviewed-matrix.md`** — 4 categories, Jnr/Mid/Snr levels, behaviour + signal + example.
- **Per-managee state in `localStorage`.** No backend.
- **Coaching-first.** Every node shows the coaching example + signal; leader sets state + writes notes.

## Mapping (matrix → game)
| Matrix | Skill tree |
|---|---|
| Category (Coaching, Communicating, Engineering, Deliver Value) | Constellation (a column of stars) |
| Behaviour | Perk node (a star) |
| Level Jnr → Mid → Snr (cumulative) | Tier, bottom → top of the constellation |
| Coaching progress | Node state: **Locked** → **Training** → **Mastered** |

State ↔ coaching ladder: Locked = not started · Training = do-help / help-do · Mastered = watch-do done.

## Milestones & tickets

**Status:** M1–M3 (v1) built in `index.html` — usable now. M4–M5 pending.

### M1 — Foundation  *(v1 — ✅ done)*
- **T1.1** Transcribe `reviewed-matrix.md` into a JS data array: `{id, category, level, title, behaviour, signal, example, isNew}`. **AC:** all 29 nodes present; every node has an example.
- **T1.2** `index.html` skeleton — header (title + managee bar), tree canvas, detail panel. **AC:** opens offline, zero console errors.
- **T1.3** Skyrim theme shell — dark starfield bg, carved-serif headings, gold/cyan palette, CSS variables. **AC:** reads as a night-sky skill screen. (Always dark; no light mode needed.)

### M2 — Skill-tree render  *(v1 — ✅ done)*
- **T2.1** Render 4 constellations as columns; nodes placed by tier (Jnr bottom → Snr top). **AC:** all nodes visible, grouped and labelled per category.
- **T2.2** Constellation connectors — SVG trunk + branch lines linking the stars, recomputed on resize. **AC:** lines sit behind stars and track them on window resize.
- **T2.3** Node visual states (Locked / Training / Mastered) — glow + colour. **AC:** three states distinguishable at a glance.
- **T2.4** Hover + selected states. **AC:** hover glows; selected star is ringed.

### M3 — Coaching interaction  *(v1 — ✅ done)*
- **T3.1** Detail panel — level badge, behaviour, signal, example. **AC:** click a star → panel shows its content.
- **T3.2** State controls — Lock / Train / Master buttons. **AC:** click updates the star immediately.
- **T3.3** Per-node coaching notes textarea. **AC:** notes survive reload.
- **T3.4** Managee selector — add / switch managee; state + notes keyed per managee. **AC:** switching shows that person's progress; no bleed between people.
- **T3.5** Progress summary — % mastered overall and per constellation. **AC:** updates live as states change.

> **v1 = M1–M3.** Shippable, usable in a real session.

### M4 — Session polish  *(v2)*
- **T4.1** "Next steps" — surface the lowest-tier not-yet-mastered stars as suggested talking points.
- **T4.2** Session summary — printable view (managee, date, states, notes).
- **T4.3** Legend + 20-second help.
- **T4.4** Responsive to laptop/tablet widths.

### M5 — Share  *(stretch)*
- **T5.1** Export / import a managee as JSON (move between machines).
- **T5.2** Publish as a private Claude Artifact for team leaders.
- **T5.3** Reset-managee and delete-managee controls.

## Out of scope (v1)
No backend, no auth, no multi-user sync, no in-app editing of the matrix (data is code). Tier
locking is **not** enforced — a leader can set any state, because coaching isn't strictly linear.

## Open questions
- Enforce tier locking (can't Master a Snr node until its Mid tier is Mastered), or leave free? **Default: free.**
- Fold the 20 `extended.md` behaviours in later as a toggleable expanded tree?
