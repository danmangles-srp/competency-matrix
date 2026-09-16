# SRP Engineer Behaviour Matrix — Reviewed

This is a list of behaviours we expect SRP engineers who deliver projects to remote
international clients to follow. We only write down the **non-obvious** ones — the
obvious basics (show up, be polite, ship working code) are assumed.

**How to read this**
- Levels are **cumulative**: a Snr is expected to do the Jnr and Mid behaviours too. A
  level tag marks where a behaviour typically *first* becomes an expectation, not a ceiling.
- **Remote + international is the hard part.** Most non-obvious behaviours below exist
  because the client is in another timezone and another culture and *cannot see you work*.
  Trust is built through written evidence, not presence.
- For coaching, each behaviour should be **observable** — you can point at evidence and say
  "yes, they do this" or "not yet." Where a behaviour was vague, a `Signal:` line names what
  to look for in a session. Each behaviour also carries a concrete `Example:` — what it
  actually looks like on a live remote engagement.

Change tags: **[NEW]** proposed addition · **[SHARPENED]** existing item made observable ·
untagged items are unchanged from the original.

---

## 1. Coaching

- **a. Snr:** Can move a junior through the ladder — *do-watch → do-help → help-do → watch-do* — for a specific skill.
  - **[SHARPENED]** Names which rung the junior is on *for that skill*, and moves them up on **evidence of competence, not elapsed time**.
  - Signal: can tell you, per skill, where each junior currently sits and what would move them up a rung.
  - Example: "Maria has built the auth module twice with me watching; she's ready for help-do on payments. I told her: 'You drive the payments integration, I'm on hand.'"
- **b. Snr:** Asks coaching questions to help juniors think through a problem, rather than handing them the answer.
  - Signal: the junior does most of the talking; the senior resists solving it for them.
  - Example: junior asks "should I put a queue here?" — senior replies "what happens if two requests hit this at the same moment?" instead of "yes, use a queue."
- **c. [NEW] Mid:** Coaches peers and juniors on a specific skill they've mastered. Coaching starts before Snr — it's how the pipeline is built.
  - Example: a Mid who owns the client's deploy runs a 20-minute screen-share teaching a Jnr the rollback steps, instead of quietly doing every deploy themselves.
- **d. [NEW] Snr:** Gives feedback **fast and specific** — close to the event, aimed at behaviour not personality, with the impact named (e.g. Situation–Behaviour–Impact).
  - Example: right after the call — "in the client call you cut across Ken twice while he was answering (behaviour); it made us look disorganised to them (impact). Let's let each other finish."
- **e. [NEW] Snr:** Lets juniors **struggle productively** — doesn't rescue at the first sign of difficulty; can tell the difference between stuck-and-learning and stuck-and-stalled.
  - Example: a junior is 40 minutes into a tricky bug and making progress; instead of taking the keyboard you ask "what have you ruled out so far?" and give them another 20 minutes.

## 2. Communicating

*(Remote + async is the theme of this whole section.)*

- **a. Jnr:** Keeps a **written, visible to-do list**, updated daily.
  - Example: Priya's list lives on the shared board, updated by end of her day — "3 done, 1 blocked (waiting on client API key), 2 queued for tomorrow."
- **b. Mid:** Sends team and client a daily written status update — **we update BEFORE the client has to ask.**
  - Example: at 17:00 her time — before the client's morning — she posts "Today: shipped checkout validation, started the refund flow. Tomorrow: finish refunds. Risk: refund spec ambiguous, need a decision (below)."
- **c. Mid:** Gives the client **"A or B" options** for key decisions, in both written and verbal form.
  - **[SHARPENED]** Includes a **recommendation and the reason** — "A or B; I recommend A because…" — not a naked choice offloaded onto the client. A bare A/B still dumps the thinking on them; the recommendation is the senior move.
  - Example: "Search: (A) Postgres full-text — free, ships this week, weaker ranking; (B) Elasticsearch — better results, +2 weeks, ~$40/mo. I recommend A now and revisiting B only if users complain about relevance."
- **d. [NEW] Jnr:** Surfaces **blockers and bad news early** — raises the problem the moment it's known, not at the deadline. A remote client can't see that you're stuck.
  - Example: two hours in, she hits a permissions wall and posts straight away — "Blocked: no write access to the staging DB. Can someone grant it? I'm on the UI meanwhile." — not buried in the 17:00 update.
- **e. [NEW] Mid:** Writes **async-first and timezone-aware** — assumes the reader is asleep. One message carries enough context to act on without a follow-up round-trip. This is *the* remote-delivery skill.
  - Example: instead of "can you clarify the refund rules?" she writes "Refund rules unclear in 2 cases: (1) partial refund after 30 days — allow? (2) store credit vs card? My assumption: allow-1, card-2. Confirm or correct." — answerable in one reply while she sleeps.
- **f. [NEW] Mid:** **Closes the loop** after verbal calls — a short written summary of decisions and next steps, same day. If it isn't written down, it didn't happen.
  - Example: after a 30-minute call she posts that day — "Decisions: refunds capped at 60 days; Ken owns the customer copy. Next: I build the 60-day rule; client sends copy by Thu."
- **g. [NEW] Snr:** **Manages up and manages expectations** — flags risk, slippage, and trade-offs to client stakeholders *before* they become surprises.
  - Example: three days out she tells the sponsor "the integration is ~2 days behind because their API changed. Options: slip the demo to Friday, or demo without live payments. I recommend Friday." — before they spot the slip.

## 3. Engineering

- **a. Mid:** Keeps the project **AI harness** up to date.
  - **[SHARPENED]** "AI harness" = the context and config that let AI tools work well on this codebase (e.g. `CLAUDE.md`, agent/prompt setup, harness scripts). Assessable when defined this way.
  - Example: after adding a new payments service, the Mid updates `CLAUDE.md` and the agent prompts so the next AI-assisted PR knows the service exists and follows its conventions — no stale context left to mislead the tool.
- **b. Jnr:** Uses AI to produce **< 1000-line PRs** that are validated and tested.
  - **[SHARPENED]** Each PR is **single-purpose and reviewable in one sitting**.
  - Example: refunds ship as three ~300-line PRs (rule engine, API, UI), each with tests — not one 1,500-line PR no reviewer in another timezone can get through in a sitting.
- **c. Jnr:** Can articulate the difference between **integration, interface, and unit tests**, and describe the test coverage and methods used in the current project.
  - Example: in a coaching session the Jnr says "we unit-test the rule engine, interface-test the payment adapter against a stub, have two integration tests through the real API, and the UI is uncovered — that's our current gap."
- **d. Mid:** Adds or updates a test **every time a bug is discovered** — the bug can't silently return.
  - Example: a user hits a crash on an empty cart; before fixing, the Mid writes a failing test `checkout_empty_cart_returns_400`, then fixes until it passes.
- **e. [NEW] Jnr:** Writes PR descriptions and commit messages that explain **why, not just what** — the reviewer and the future reader shouldn't have to reverse-engineer intent.
  - Example: PR title "Cap refunds at 60 days"; body — "Client decision 2026-08-20 (link). Used a config value not a hard-coded 60 so ops can change it without a deploy." — not "fix refund logic."
- **f. [NEW] Mid:** **Debugs systematically** — reproduce, isolate, fix, prove with a test — rather than guessing and poking.
  - Example: prod throws 500s; the Mid reproduces from the failing request locally, bisects to a null timezone field, adds a test, then fixes — instead of redeploying random changes hoping one sticks.
- **g. [NEW] Mid:** Reviews others' PRs with **specific, actionable feedback**.
  - Example: "Line 42 — this N+1 query will hammer the client's 50k-row orders table; eager-load here (example)." — not "looks good" or "I'd have done this differently."
- **h. [NEW] Snr:** Makes architectural decisions **deliberately and records them** (what, why, alternatives rejected); treats tech debt as a conscious trade-off, not an accident.
  - Example: choosing events over REST for the new service, the Snr writes a one-page ADR: the decision, why events, what REST would have cost, and the debt taken on (no schema registry yet — revisit in Q4).

## 4. Deliver value to the client

- **a. Snr:** Can articulate the client's **business strategy** — knows the revenue and profit goals for the next year and how they connect to the current system.
  - Example: "The client makes their margin on repeat orders; their goal is +20% revenue this year, and our checkout-speed work feeds their reorder rate directly — that's why it's priority one."
- **b. Mid:** Defines and maintains **SMART milestones**.
  - Example: "Refunds live in production, client-approved, by Sep 15" — specific, measurable, dated — not "work on refunds."
- **c. Mid:** Can explain a task or milestone in **business/project terms**, not just technical ones.
  - Example: asked why the caching task matters, the Mid says "it cuts page load from 4s to under 1s, and the client's own data ties that to a ~7% drop in cart abandonment" — not "it makes it faster."
- **d. Jnr:** Ensures **no work is released without internal QA and client approval**.
  - Example: the Jnr finishes the refund flow but doesn't push to prod until QA signs off *and* the client clicks "approved" in the ticket — even with the deadline that afternoon.
- **e. Jnr:** Follows the release process **every time**.
  - Example: every release runs the same checklist — QA pass → client approval → tag → staging → smoke test → prod — never skipping staging because "it's only a small change."
- **f. Mid:** Builds an effective release process that **fits the client and project** needs.
  - Example: for a client with no CI, the Mid sets up a lightweight release — PR checklist, one-click staging deploy, and a client approval step in *their* tool — fitting their maturity, not a heavyweight process they'll route around.
- **g. [NEW] Snr:** **Pushes back on low-value work** — protects scope and the client's budget; can say "that's not worth building yet, and here's why."
  - Example: client asks for a custom analytics dashboard; the Snr replies "that's ~2 weeks. Your quarter goal is checkout speed and this doesn't move it — suggest we park it. Here's the reasoning."
- **h. [NEW] Mid → Snr:** Spots and proposes **value the client didn't ask for** — surfaces opportunities and risks in the system, not just closes tickets. The difference between an order-taker and a partner.
  - Example: unprompted, the Mid flags "your biggest table has no index on `customer_id`; at current growth it'll crawl at ~100k rows, roughly 3 months out. Cheap to fix now."
- **i. [NEW] Jnr:** Knows **who the end users are** and what they're trying to do — can name the user and the job-to-be-done for the feature in hand.
  - Example: asked who uses the refund screen, the Jnr says "the client's support agents, under time pressure on live chat — so it needs to be two clicks, not a long form."

---

## Review notes (the non-trivial reasoning)

1. **The remote/international context was the biggest gap.** The original section 2 covered
   status updates well but missed the behaviours that actually break remote delivery:
   early blockers (2d), async-first writing (2e), closing the loop after calls (2f), and
   managing up (2g). These deserve the most weight in coaching because they're invisible
   until they fail.

2. **Coaching shouldn't be Snr-only (1c).** Having Mids coach juniors on narrow, mastered
   skills is realistic and is how you scale the coaching pipeline. Worth deciding as policy.

3. **The single most coachable upgrade is naming the ladder rung (1a).** "What rung is
   Priya on for writing tests, and what moves her up?" is a concrete coaching conversation;
   "can they coach" is not.

4. **"A or B" needs a recommendation (2c).** A naked A/B choice still offloads the decision
   work onto the client. The senior behaviour is A/B *plus* a reasoned recommendation.

5. **Engineering was strong on AI-assisted output but light on ownership.** Added the gap
   between "writes code with AI" and "owns a system": explain-why in PRs (3e), systematic
   debugging (3f), reviewing others' work (3g), and deliberate architecture/tech-debt (3h).

6. **Value delivery was all compliance, no initiative.** The original items are about doing
   the process right (good). Added the partner behaviours: push back on low-value work (4g)
   and proactively propose value (4h), grounded by end-user awareness at Jnr (4i).

7. **Prefer observable signals over task descriptions.** A few originals describe tasks
   ("keeps a to-do list") rather than outcomes. For coaching, the assessable question is
   "what do you *see*?" — hence the `Signal:` and `Example:` lines.

### Open questions for you
- **3a level:** Is keeping the AI harness current really a *Mid* behaviour, or should
  *using* it be a Jnr habit while a Mid *owns* it? (Suggest splitting.)
- Do you want an explicit **"assumed basics"** line at the top of each section, so coaches
  are reminded what's deliberately *not* listed?
- Should levels stay 3-tier (Jnr/Mid/Snr), or is there a **Lead/Principal** tier above Snr
  that some of these (2g, 3h, 4a, 4g) actually point at?
