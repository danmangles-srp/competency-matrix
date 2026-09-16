# SRP Behaviour Matrix — Extended Candidates & Cuts

Two parts:
- **Part A** — 20 extended behaviours worth adding, ranked within each group. All are distinct
  from the current `matrix.md` and from the `reviewed-matrix.md` additions. Each is non-obvious,
  observable, and weighted toward the thing that actually makes SRP's work hard: a client in
  another timezone and culture who **cannot see you work**.
- **Part B** — the weakest items in the current list, ranked by what to drop or merge first.

Level tags mark where a behaviour first becomes an expectation (cumulative — Snr does all of it).

---

## Part A — 20 behaviours to add

### Communicating (remote + international)

1. **[Jnr] Writes plain English for non-native readers** — short sentences, no idioms, slang, or
   unexplained abbreviations. The client reads in their second language; clever phrasing costs a
   round-trip. Highest-ROI, most SRP-specific behaviour on this list.
2. **[Jnr] Restates the ask in their own words before building** — confirms understanding *before*
   burning a day. A misread across a timezone gap costs 24h+ to detect and fix.
3. **[Mid] Escalates with a proposed solution, not just a problem** — "here's the issue **and** what
   I suggest we do." Raising a naked problem into another timezone stalls for a full cycle.
4. **[Mid] Keeps a single source of truth** — decisions land in a durable, findable place, not
   buried in DMs or an unminuted call. If two people would answer "what did we decide?" differently, it failed.
5. **[Mid] Communicates uncertainty honestly** — estimates as ranges with a confidence level; says
   "I don't know — I'll find out by X" instead of bluffing. False certainty is expensive to unwind remotely.
6. **[Jnr] Flags own availability early and protects a reliable overlap window** — announces time off
   and PTO well ahead, and guards a predictable daily overlap with the client. Remote team can't see your calendar.

### Engineering

7. **[Jnr] Keeps main deployable / CI green** — never leaves the build red overnight. Across timezones
   a broken build blocks the other side for their whole working day.
8. **[Mid] Reproduces the client's environment and data before claiming "done"** — kills
   "works on my machine," which detonates trust when the client hits it hours later.
9. **[Mid] Adds observability** — logs, metrics, traces — so a production issue is diagnosable
   **remotely**, without shoulder-surfing or a live screen-share at a bad hour.
10. **[Jnr] Handles secrets and credentials safely** — never in code, commits, logs, or chat.
    Non-negotiable discipline; the cheapest place to catch it is at Jnr.
11. **[Jnr] Self-reviews their own diff before requesting review** — reads it as a stranger would.
    Catches the obvious, respects the reviewer's time (who is often asleep when you push).
12. **[Mid] Ships reversibly** — feature flags, dark launches, one-step rollback. When something
    breaks and the author is offline, the client's side needs to undo it without you.
13. **[Jnr] Time-boxes investigations and reports back** — sets a limit on a spike, then surfaces
    findings rather than silently rabbit-holing for a day where nobody can see the stall.

### Deliver value to the client

14. **[Mid] Agrees acceptance criteria before building** — written, client-confirmed "done" up front.
    Prevents the slow, expensive remote argument about whether a thing is finished.
15. **[Mid] Demos working software regularly** — shows, doesn't tell. A running demo builds remote
    trust faster than any status update.
16. **[Mid] Tracks work against estimate/budget and flags overruns early** — the client is spending
    money they can't see being spent; the warning must come before the invoice.
17. **[Snr] Owns the outcome end-to-end** — "done" means the client's result is real in production,
    not "my part merged." Refuses to let work fall down the gap between people.
18. **[Snr] Maintains an explicit top-risks view** — can name the current top 3 risks to the project
    and what's being done about each. Surfaces them before they land.

### Coaching & knowledge

19. **[Snr] Runs blameless retros / post-mortems** — extracts the lesson and the system fix without
    finger-pointing. In a distributed team, blame kills the honesty you need most.
20. **[Mid] Documents knowledge so it outlives them** — runbooks, decision records, the gotchas that
    cost a day. In a remote team you can't tap a shoulder; the doc is the shoulder.

---

## Part B — weakest current items, drop/merge first

Ranked. Reasoning given so it's a coaching conversation, not a deletion.

1. **DROP / fold — `2a` Jnr: "Daily updates a written to-do list."**
   Weakest item in the list. It's hygiene bordering on obvious (violates the matrix's own
   "only non-obvious" rule), and it names a *task*, not an outcome. The value it points at —
   visible progress — is already carried better by `2b` (daily status update) and by the proposed
   async-first behaviour. **Fold into those; don't list separately.**

2. **MERGE — `4e` Jnr: "Follows the release process every time."**
   Heavily overlaps `4d` (no release without QA + approval) and `4f` (builds a fitting release
   process). "Follow the process" is compliance, close to obvious once `4d` exists. **Merge the
   "every time" reliability into `4d`** so one item covers "there is a gate, and it's never skipped."

3. **TRIM / TIER — `4c` "Explain a task in business terms" vs `4a` "Articulate business strategy."**
   Not weak, but redundant with `4a`. They're the same muscle at two levels. Keep both **only if
   tiered explicitly** (4c = this task's business value; 4a = the whole client's strategy);
   otherwise collapse to one laddered behaviour.

4. **REWORD — `3c` "Can articulate the difference between integration, interface, and unit tests."**
   Half of this is a **knowledge check**, not a behaviour — someone can recite the definitions and
   still test badly. Keep the observable half ("can describe the coverage and test methods *in the
   current project*") and drop the recite-the-definitions framing.

### Net effect
Cutting `2a` and merging `4e`/`4c` removes 2–3 low-signal lines. Adding even the top 6 from Part A
(items 1, 2, 7, 10, 14, 17) more than replaces them with higher-signal, remote-specific behaviour —
a shorter, sharper list that's easier to coach against.
