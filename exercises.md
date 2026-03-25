---
layout: default
title: Exercise Cards
---

# Exercise Cards

## Stop Typing, Start Orchestrating — RVATech Data Summit 2026

Each card is self-contained. You have `mini-crm` cloned and running locally with Claude Code open in the repo directory.

**Repo:** `github.com/busse/mini-crm` — Python/FastAPI/SQLite CRM
**Reset anytime:** `git checkout main && git clean -fd && python3 scripts/reset_db.py && python3 scripts/seed.py`
(Windows: use `python` instead of `python3`)

---

## Exercise 1 — Codebase Navigation

**Block 2 · 7 minutes**

### The task

Use Claude Code to explore `mini-crm` without opening a single file yourself. You're a new developer who just got dropped into this codebase — let the agent do the reading.

### Steps

1. **Warm-up:** Ask Claude Code to summarize the project structure.
   ```
   What does this project do? Give me an overview of the architecture.
   ```

2. **Directed exploration:** Find where authentication is handled.
   ```
   Where is authentication implemented? Walk me through how a user logs in.
   ```

3. **Go deeper:** Trace a request lifecycle.
   ```
   What happens when a POST request is made to /api/deals?
   ```

4. **Stretch:** Ask Claude to find problems.
   ```
   Are there any obvious bugs or code smells in this codebase?
   ```

### What "done" looks like

You should have a mental model of the project: what the models are, how routers are organized, where auth lives, and how the frontend talks to the API — all without opening a file browser.

### Things to notice

- Watch the tool-use trace. Claude uses `glob`, `grep`, and `read` — plain text tools driven by the model. No special IDE indexing.
- On the stretch question, Claude should find real issues: missing input validation on contacts, N+1 queries in deals, inconsistent error handling. These are intentional.

---

## Exercise 2 — Prompt Structuring

**Block 3 · 6 minutes**

### The task

Add a "favorite contacts" feature to the CRM. But before you send anything to Claude Code, write a structured prompt using the **DECOMPOSE** pattern from the demo.

### The DECOMPOSE pattern

| Letter | Question to answer |
|--------|--------------------|
| **D**efine the outcome | What exactly should this feature do? |
| **E**xisting patterns | What conventions does the codebase already follow? |
| **C**onstraints | Any edge cases, limits, or things to avoid? |
| **O**utput format | What files, endpoints, schemas should be produced? |
| **M**easure of done | How will you know it works? (tests, manual check, etc.) |

### Steps

1. **Write your prompt first.** Don't send it yet. Spend 2 minutes composing a structured prompt that covers DECOMPOSE. Here's a starting scaffold:

   ```
   Add a "favorite contacts" feature to the CRM.

   Outcome: Users can mark contacts as favorites and filter by favorites.

   Existing patterns:
   - Follow the router/schema/model pattern in app/routers/, app/schemas/, app/models/
   - Use the same pagination pattern as GET /api/contacts
   - Authentication is required (use the get_current_user dependency)

   Constraints:
   - Favorites are per-user (each user has their own favorites)
   - A contact can only be favorited once per user (no duplicates)
   - Use a join table, not a boolean on the contact model

   Output:
   - New model: UserFavorite (user_id, contact_id)
   - New endpoints: POST /api/contacts/{id}/favorite, DELETE /api/contacts/{id}/favorite, GET /api/contacts/favorites
   - Updated schema for contact list response (include is_favorited field)

   Done when:
   - All new endpoints return correct responses
   - Tests pass (add tests in tests/test_contacts.py or a new test file)
   - Existing tests still pass
   ```

2. **Send it to Claude Code** and watch the output.

3. **Compare with a neighbor** — whose prompt produced more complete, correct code? What was different about the prompts?

### Stretch

If Claude got something wrong, refine your prompt and re-run. Use `/clear` first so it starts fresh. See how the improved prompt changes the output.

### What "done" looks like

You have working favorite-contacts endpoints with tests. More importantly, you experienced how prompt structure directly controls output quality.

---

## Exercise 3 — Task Orchestration

**Block 4 · 10 minutes**

### The task

Build a feature end-to-end using the **Explore → Plan → Implement → Verify** loop. This is *not* a one-shot prompt exercise — the goal is to practice the iterative workflow.

### Choose your feature

Pick **one** of the following. All are designed to be completable in 10 minutes with the orchestration loop.

**Option A — CSV export for contacts**
Add a `GET /api/contacts/export` endpoint that returns all contacts as a CSV download. Include company name as a joined field.

**Option B — Rate limiting**
Add rate limiting middleware to the API. Limit to 60 requests per minute per user. Return `429 Too Many Requests` when exceeded.

**Option C — Admin role**
Add an `is_admin` flag to the user model. Create a middleware or dependency that restricts certain endpoints (e.g., `DELETE /api/contacts/{id}`) to admin users only.

### Steps

1. **Explore** — Start in Plan Mode or just ask questions. Don't write code yet.
   ```
   Read the existing contact router and understand how the list endpoint works.
   Also check how the test suite is set up in tests/conftest.py.
   ```

2. **Plan** — Ask Claude to plan before implementing.
   ```
   I want to add [your feature]. Create a detailed implementation plan.
   List the files you'll create or modify, the changes to each, and the order
   of operations. Don't write code yet.
   ```
   Review the plan. If something looks off, tell Claude to adjust.

3. **Implement** — Give the go-ahead.
   ```
   Go ahead and implement the plan. Run tests after each major change.
   ```

4. **Debug** — When (not if) something fails, paste the error back.
   ```
   I got this error when running the tests:

   [paste the error]

   Fix it.
   ```

5. **Verify** — Confirm everything works.
   ```
   Run the full test suite and show me the results.
   ```

### Stretch

- Use `/compact` mid-session if your context is getting long.
- Try creating a slash command: save a reusable prompt to `.claude/commands/run-tests.md` with content like `Run pytest and report results. If anything fails, fix it and re-run.`

### What "done" looks like

A working feature with passing tests, built through multiple turns of the orchestration loop rather than a single prompt. You should have used at least 3 of the 4 loop steps (Explore, Plan, Implement, Verify).

### Things to notice

- The Plan step saves you from bad implementations. Reviewing a plan is faster than reviewing code.
- Feeding errors back is the most common interaction pattern — get comfortable with it.
- If you find yourself correcting Claude more than twice on the same issue, `/clear` and write a better prompt.

---

## Exercise 4 — Multi-Agent Patterns

**Block 5 · 8 minutes · Choose one option**

These exercises require opening multiple terminal tabs or windows with Claude Code, or using subagent features. Pick the pattern that interests you most.

---

### Option A — Writer / Reviewer

Two Claude Code sessions: one writes, one reviews.

**Setup:** Open two terminal tabs. Both should be in the `mini-crm` directory.

1. **Tab 1 (Writer):** Ask Claude to implement a feature.
   ```
   Add a "deal notes" feature: a new endpoint POST /api/deals/{id}/notes
   that lets users add timestamped notes to a deal. Store in a new notes
   table. Include GET /api/deals/{id}/notes to list them.
   ```
   Let it finish.

2. **Tab 2 (Reviewer):** In a fresh session, ask Claude to review what Tab 1 just wrote.
   ```
   Review the recent changes to this codebase related to deal notes.
   Look at the new model, router, and any tests. Check for:
   - Missing input validation
   - SQL injection risks
   - Consistency with existing patterns
   - Edge cases not handled
   - Test coverage gaps
   ```

3. **Feed back:** Copy the review findings and paste them into Tab 1.
   ```
   A code reviewer found these issues with your implementation:

   [paste review]

   Fix them.
   ```

**Why this works:** A fresh context gives unbiased review. Claude won't defend code it just wrote.

---

### Option B — Subagent Research

Use a subagent to investigate, then implement based on findings.

1. **Research phase:** Ask Claude to dispatch a subagent for investigation.
   ```
   Use a subagent to research how the existing codebase handles
   pagination across all routers. Report back: what pattern is used,
   is it consistent, and are there any endpoints missing pagination
   that should have it?
   ```

2. **Review the findings.** The subagent runs in its own context and returns a summary to your main session.

3. **Implement:** Based on the research, fix any inconsistencies.
   ```
   Based on the subagent's findings, add pagination to any endpoints
   that are missing it. Follow the existing pattern exactly.
   ```

**Why this works:** The subagent uses a smaller model (Haiku) for fast, read-only research. Your main session stays clean and focused on implementation.

---

### Option C — Parallel Build

Split a feature across two sessions: one for backend, one for frontend.

**Setup:** Open two terminal tabs, both in `mini-crm`.

1. **Tab 1 (Backend):**
   ```
   Add a CSV import endpoint: POST /api/contacts/import that accepts
   a CSV file upload with columns: first_name, last_name, email, phone,
   company_name. Parse the CSV, create or match companies by name,
   and create contacts. Return a summary of what was imported.
   Add tests.
   ```

2. **Tab 2 (Frontend):**
   ```
   Add a CSV import page to the frontend. Create a new template at
   app/templates/import.html that has:
   - A file upload form for CSV files
   - A preview table showing the first 5 rows before import
   - A submit button that POSTs to /api/contacts/import
   - A results summary after import completes
   Add a link to it from the main navigation.
   ```

3. **Integrate:** Once both are done, test the full flow together.

**Why this works:** Backend and frontend are independent enough to build in parallel. This mirrors how real teams work — and it's how Boris Cherny runs 5+ sessions daily.

---

### Stretch (any option)

Create a custom subagent definition. Save this to `.claude/agents/reviewer.md`:

```markdown
# Code Reviewer Agent

You are a code reviewer for a Python/FastAPI application.

## Focus areas
- Input validation and error handling
- SQL query efficiency (watch for N+1 queries)
- Consistency with existing patterns
- Test coverage

## Rules
- Be specific: reference file names and line numbers
- Prioritize: critical → important → nice-to-have
- Don't suggest stylistic changes unless they affect readability
```

Then invoke it: *"Use the reviewer agent to review the changes I just made."*

---

## Quick Reference

| Block | Exercise | Duration | Key skill |
|-------|----------|----------|-----------|
| 2 | Codebase Navigation | 7 min | Letting the agent read for you |
| 3 | Prompt Structuring | 6 min | DECOMPOSE pattern, structured prompts |
| 4 | Task Orchestration | 10 min | Explore → Plan → Implement → Verify loop |
| 5 | Multi-Agent Patterns | 8 min | Parallel sessions, subagents, Writer/Reviewer |

**Session management cheat sheet:**

| Command | What it does |
|---------|--------------|
| `/clear` | Reset context between tasks |
| `/compact` | Summarize conversation to free context |
| `Esc` | Stop Claude mid-action |
| `Esc + Esc` | Rewind to previous checkpoint |
| `--resume` | Pick up a previous conversation |

**Repo reset:** `git checkout main && git clean -fd && python3 scripts/reset_db.py && python3 scripts/seed.py`

---

*Stop Typing, Start Orchestrating — RVATech Data Summit, March 26, 2026*
