---
layout: default
title: Run of Show
---

# Stop Typing, Start Orchestrating
## An Agentic Coding Workshop with Claude Code
### Run-of-Show Outline — 70 Minutes

**Event:** 2026 RVATech Data & AI Summit | **Date:** March 26, 2026 | **Presenter:** Chris Busse

**Format:** Single-track, live code-along. Advanced multi-agent exercises are stretch goals woven into later blocks.

**Companion doc:** [Approach & Sources](approach.md) — detailed source material, citable references, and speaker-note depth. Cross-referenced below as `→ Approach §X`.

---

## Block 0 — Setup & Orientation (5 min) `[0:00–0:05]`

**Goal:** Everyone has Claude Code open and ready.

- Quick mic check: "Who's used an AI coding tool before? Who's used it from a terminal?"
- Confirm prerequisites: terminal open, Claude Code installed, API key or login working
- If anyone's stuck on setup → point to pre-work doc (troubleshooting steps)
- Set the frame: *"For the next 70 minutes, you're not writing code. You're directing an agent that writes code."*

**On screen:** Terminal with Claude Code ready, workshop repo URL displayed

---

## Block 1 — Why Agentic Coding? (5 min) `[0:05–0:10]`

**Goal:** Establish mental model — coding as orchestration, not typing. `→ Approach §2A, §3E, §7`

- The shift: autocomplete → copilot → agent. What changed?
- Key insight: the bottleneck moved from *writing* to *directing*
- Three skills that matter now:
  1. Problem decomposition (breaking work into agent-sized tasks)
  2. Trust calibration (knowing when to verify vs. ship)
  3. Workflow design (chaining agent steps into reliable pipelines)
- *"This workshop is about building those three skills."*
- Credibility data points: 4% of GitHub commits now from Claude Code; Boris Cherny has written 100% of his code via AI since Nov 2025; Anthropic engineering output up 200% `→ Approach §7`

**No slides after this block** — everything moves to live terminal.

---

## Block 2 — Codebase Navigation (10 min) `[0:10–0:20]`

**Goal:** Use Claude Code to explore and understand an unfamiliar codebase. `→ Approach §4B, §4C`

### Demo (3 min)
- Clone/open the workshop demo repo
- Show Claude Code's first interaction: *"What does this project do?"*
- Follow up: *"Where is the main entry point?"* → *"Walk me through the request lifecycle"*
- Highlight: Claude reads files, greps, follows imports — show the tool-use trace
- Note: Claude Code's "agentic search" is plain glob and grep, driven by the model — and it beats specialized tools `→ Approach §3A`

### Exercise (7 min)
Attendees explore the same repo on their own machines:

1. **Warm-up:** Ask Claude Code to summarize the project structure
2. **Directed exploration:** Find where authentication is handled
3. **Go deeper:** *"What happens when a POST request is made to /api/deals?"*
4. **Stretch:** *"Are there any obvious bugs or code smells?"*

**Debrief callout (30 sec):** *"Notice you didn't open a single file manually. The agent did the reading for you."*

---

## Block 3 — Prompt Structuring (10 min) `[0:20–0:30]`

**Goal:** Learn how prompt shape affects agent output quality. Frame as *context engineering*, not just prompting. `→ Approach §2B, §2D, §4A, §4B, §6A`

### Demo (4 min)
Show the difference between vague and structured prompts on the same task:

| Vague | Structured |
|---|---|
| *"Add a search feature"* | *"Add a search endpoint to the API: accepts a query param `q`, searches the `title` and `description` fields in the items table, returns paginated JSON matching the existing list endpoint format. Add tests."* |

- Run both live. Show how the structured version produces shippable code in one pass.
- Frame the "why": Context engineering — you're curating the smallest set of high-signal tokens to maximize the model's chance of success `→ Approach §2B`
- Introduce the **DECOMPOSE** pattern:
  - **D**efine the outcome
  - **E**xisting patterns to follow
  - **C**onstraints and edge cases
  - **O**utput format expected
  - **M**easure of done (tests, types, etc.)
- Key stat: verification criteria alone give a 2-3x quality improvement on agent output `→ Approach §2D, §7`

### Exercise (6 min)
Attendees practice structured prompting:

1. **Task:** Add a "favorite contacts" feature (details on exercise card)
2. Write a structured prompt using DECOMPOSE before sending it
3. Run it through Claude Code
4. Compare output with a neighbor — whose prompt produced more complete code?

**Stretch:** Refine the prompt based on what Claude got wrong, re-run, see the improvement.

---

## Block 4 — Task Orchestration & Iteration (15 min) `[0:30–0:45]`

**Goal:** Chain multiple agent interactions into a complete workflow. Debug and iterate on agent output. `→ Approach §2C, §3B, §3C, §4D, §4E`

### Demo (5 min)
Build a small feature end-to-end using the official **Explore → Plan → Implement → Commit** loop `→ Approach §2C`:

1. **Explore (Plan Mode):** *"Read /src/notifications and understand how we handle email. Also check the existing event system."*
2. **Plan:** *"I want to add email notifications when an item is created. Create a detailed implementation plan — don't write code yet."* → Review → adjust with Ctrl+G → approve
3. **Implement:** *"Go ahead and implement the plan. Run tests after each major change."*
4. **Debug:** Intentionally hit an error → *"I got this error when running the tests: [paste]. Fix it."*
5. **Verify:** *"Run the tests and show me the results."*

- Show session management: `/clear`, `/compact`, `Esc` to stop, `Esc+Esc` to rewind `→ Approach §4E`
- Highlight anti-patterns: the kitchen sink session, correcting over and over `→ Approach §4D`
- Key lesson: *"You're a tech lead doing code review in real-time, not a developer typing."*

### Exercise (10 min)
Attendees build a feature using the orchestration loop:

1. **Task:** Choose from exercise card (e.g., add rate limiting, add CSV export, add admin role)
2. Follow the loop:
   - Explore in Plan Mode first
   - Ask Claude Code to plan
   - Review and refine the plan
   - Have it implement with verification
   - Feed errors back and iterate
3. Goal: get to a working implementation through the loop, not in one shot

**Stretch:** Use `/compact` to manage context, or create a slash command for a repeated step `→ Approach §3B`

---

## Block 5 — Multi-Agent Patterns (15 min) `[0:45–1:00]`

**Goal:** Introduce parallel and coordinated agent workflows for those ready to level up. `→ Approach §5A–§5F`

### Demo (7 min)

**Pattern 1 — Parallel sessions with Writer/Reviewer (3 min)** `→ Approach §5C`
- Open two terminal tabs with Claude Code
- Tab 1 (Writer): *"Implement a rate limiter for our API endpoints"*
- Tab 2 (Reviewer): *"Review the rate limiter implementation in @src/middleware/rateLimiter.ts. Look for edge cases, race conditions, and consistency with our existing middleware patterns."*
- Feed review back to Tab 1 — show how a fresh context produces unbiased review
- Key insight: *"You're a manager delegating to two developers simultaneously."*
- Boris Cherny runs 5 local + 5-10 web sessions daily using this approach `→ Approach §3A`

**Pattern 2 — Subagents for isolated work (2 min)** `→ Approach §5A`
- *"Use a subagent to research how the existing codebase handles file uploads. Report back the patterns used."*
- Show how the subagent runs in its own context, keeps the main session clean
- Built-in subagents: Explore (Haiku, read-only), Plan, General-purpose

**Pattern 3 — Agent Teams (2 min, brief demo/walkthrough)** `→ Approach §5B, §5E, §5F`
- Show the concept: team lead + teammates + shared task list + mailbox
- Reference the production example: Anthropic's Code Review system dispatches parallel agents that cross-verify findings `→ Approach §5E`
- Reference the extreme example: 16-agent team that built a 100K-line C compiler `→ Approach §5F`

### Exercise (8 min)
Attendees try one multi-agent pattern:

1. **Option A (Writer/Reviewer):** Write a feature in one session, review it in a fresh session, feed review back
2. **Option B (Subagent):** Use a subagent to investigate a question, then implement based on findings
3. **Option C (Parallel):** Split a feature across two Claude Code sessions — one does backend, one does frontend

**Stretch:** Set up a custom subagent definition in `.claude/agents/` with a focused system prompt and limited tool access `→ Approach §5A`

---

## Block 6 — Wrap-Up & What's Next (5 min) `[1:00–1:05]`

**Goal:** Anchor the mental model, point to next steps. `→ Approach §2A, §8`

- Recap the three skills: decomposition, trust calibration, workflow design
- Real-world applications:
  - Onboarding onto unfamiliar codebases
  - Rapid prototyping / proof of concepts
  - Code review and refactoring at scale (Code Review product as example)
  - Legacy code migration (fan-out pattern) `→ Approach §5D`
- Resources to share:
  - Claude Code docs: https://code.claude.com/docs
  - Best practices guide: https://code.claude.com/docs/en/best-practices
  - Context engineering guide: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
  - Workshop repo (stays live for practice)
  - Chris Busse's contact info
- *"You're not replacing developers. You're giving every developer a team."*

---

## Buffer / Q&A (5 min) `[1:05–1:10]`

- Open Q&A
- Live request: audience picks a task, Chris Busse orchestrates it live
- Overflow for any exercise block that ran long

---

## Timing Summary

| Block | Topic | Duration | Cumulative | Key Approach Refs |
|-------|-------|----------|------------|-------------------|
| 0 | Setup & Orientation | 5 min | 0:05 | — |
| 1 | Why Agentic Coding? | 5 min | 0:10 | §2A, §3E, §7 |
| 2 | Codebase Navigation | 10 min | 0:20 | §4B, §4C |
| 3 | Prompt Structuring | 10 min | 0:30 | §2B, §2D, §4A, §6A |
| 4 | Task Orchestration & Iteration | 15 min | 0:45 | §2C, §3B, §3C, §4D, §4E |
| 5 | Multi-Agent Patterns | 15 min | 1:00 | §5A–§5F |
| 6 | Wrap-Up | 5 min | 1:05 | §2A, §5D, §8 |
| — | Buffer / Q&A | 5 min | 1:10 | — |

---

## Open Questions & Decisions

- [ ] **Demo repo:** Build a purpose-built starter repo or use an existing OSS project? (Leaning toward purpose-built for controlled complexity)
- [ ] **Pre-work:** What setup instructions do attendees need before the session? (Claude Code install, API key, repo clone)
- [ ] **Exercise cards:** Design printed/digital cards with task descriptions so attendees can self-serve during exercise blocks?
- [ ] **Fallback plan:** If Wi-Fi fails or API is slow, have a pre-recorded demo video or local model fallback?
- [ ] **DECOMPOSE mnemonic:** Keep as-is or refine? (Currently missing P, O, S, E expansions — intentionally truncated to 5 letters)
- [ ] **Agent Teams demo:** Live demo or walkthrough-only? (Experimental feature, may be complex for a live setting)

---

*Last updated: 2026-03-11*
