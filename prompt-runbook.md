---
layout: default
title: Prompt Runbook
---

# Prompt Runbook

## All prompts, one place — ready to copy and paste

Organized by block and slide. Each prompt is in a code block for easy copy. Terminal commands are marked with `$`.

---

## Pre-Flight

```bash
$ python3 scripts/reset_db.py && python3 scripts/seed.py
```

```bash
$ claude
```

**Repo reset (use between demos):**

```bash
$ git checkout . && git clean -fd
```

**Full reset (repo + data):**

```bash
$ git checkout main && git clean -fd && python3 scripts/reset_db.py && python3 scripts/seed.py
```

---

## Block 2 — Codebase Navigation (Slides 10-12)

### Demo (Slide 10)

**Prompt 1 — Project overview:**

```
What does this project do?
```

**Prompt 2 — Entry point:**

```
Where is the main entry point?
```

**Prompt 3 — Request lifecycle (the impressive one):**

```
Walk me through the request lifecycle for POST /api/deals
```

### Exercise prompts (Slide 12)

**1 — Architecture overview:**

```
What does this project do? Give me an overview of the architecture.
```

**2 — Find auth:**

```
Where is authentication implemented? Walk me through how a user logs in.
```

**3 — Trace a request:**

```
What happens when a POST request is made to /api/deals?
```

**4 — Find bugs (stretch):**

```
Are there any obvious bugs or code smells in this codebase?
```

---

## Block 3 — Prompt Structuring (Slides 14-17)

### Demo: Vague vs. Structured (Slide 15)

**Before the vague prompt:**

```
/clear
```

**Vague prompt (the bad one):**

```
Add a search feature
```

**After vague prompt — reset:**

```
/exit
```

```bash
$ git checkout . && git clean -fd
```

```bash
$ claude
```

**Structured prompt (the good one):**

```
Add a search endpoint to the API: accepts a query param `q`, searches the `first_name`, `last_name`, and `email` fields in the contacts table, returns paginated JSON matching the existing list endpoint format. Add tests.
```

### Exercise: Favorite Contacts (Slide 17)

**Full DECOMPOSE prompt (scaffold):**

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

---

## Block 4 — Task Orchestration (Slides 19-23)

### Demo: Email Notifications (Slide 20)

**Before the demo:**

```
/clear
```

**Step 1 — Explore:**

```
Read the deal router and deal service. How do deal stage transitions work?
```

**Step 2 — Plan:**

```
I want to add email notifications when a deal moves to Closed Won. Create a detailed implementation plan — list the files you'll modify and the order of operations. Don't write code yet.
```

**Step 3 — Implement:**

```
Go ahead and implement the plan. Run tests after each major change.
```

**Step 4 — Debug (paste your actual error):**

```
I got this error: [paste]. Fix it.
```

**Step 5 — Verify:**

```
Run the full test suite and show me results.
```

### Exercise: Choose a Feature (Slide 23)

**Explore step (same for all options):**

```
Read the existing contact router and understand how the list endpoint works. Also check how the test suite is set up in tests/conftest.py.
```

**Plan step (fill in your feature):**

```
I want to add [your feature]. Create a detailed implementation plan. List the files you'll create or modify, the changes to each, and the order of operations. Don't write code yet.
```

**Implement step:**

```
Go ahead and implement the plan. Run tests after each major change.
```

**Debug step:**

```
I got this error when running the tests:

[paste the error]

Fix it.
```

**Verify step:**

```
Run the full test suite and show me the results.
```

**Stretch — Create a slash command:**

```bash
$ mkdir -p .claude/commands && cat > .claude/commands/run-tests.md << 'EOF'
Run pytest and report results. If anything fails, fix it and re-run.
EOF
```

---

## Block 5 — Multi-Agent Patterns (Slides 25-30)

### Demo: Writer/Reviewer (Slide 25)

**Tab 1 — Writer:**

```
Add a simple rate limiter to the API — limit to 60 requests per minute per user. Use an in-memory counter. Return 429 when exceeded.
```

**Tab 2 — Reviewer (fresh session):**

```
Review the recent changes to this repo related to rate limiting. Look at any new middleware or router changes. Check for: edge cases not handled, race conditions, consistency with existing patterns, test coverage gaps.
```

**Tab 1 — Feed review back:**

```
A code reviewer found these issues: [paste]. Fix them.
```

### Demo: Subagents (Slide 26)

```
Use a subagent to research how the existing codebase handles pagination across all routers. Report back the patterns used and whether they're consistent.
```

### Exercise Option A — Writer/Reviewer (Slide 30)

**Tab 1 — Writer:**

```
Add a "deal notes" feature: a new endpoint POST /api/deals/{id}/notes that lets users add timestamped notes to a deal. Store in a new notes table. Include GET /api/deals/{id}/notes to list them.
```

**Tab 2 — Reviewer:**

```
Review the recent changes to this codebase related to deal notes. Look at the new model, router, and any tests. Check for:
- Missing input validation
- SQL injection risks
- Consistency with existing patterns
- Edge cases not handled
- Test coverage gaps
```

**Tab 1 — Feed back:**

```
A code reviewer found these issues with your implementation:

[paste review]

Fix them.
```

### Exercise Option B — Subagent Research (Slide 30)

**Research:**

```
Use a subagent to research how the existing codebase handles pagination across all routers. Report back: what pattern is used, is it consistent, and are there any endpoints missing pagination that should have it?
```

**Implement:**

```
Based on the subagent's findings, add pagination to any endpoints that are missing it. Follow the existing pattern exactly.
```

### Exercise Option C — Parallel Build (Slide 30)

**Tab 1 — Backend:**

```
Add a CSV import endpoint: POST /api/contacts/import that accepts a CSV file upload with columns: first_name, last_name, email, phone, company_name. Parse the CSV, create or match companies by name, and create contacts. Return a summary of what was imported. Add tests.
```

**Tab 2 — Frontend:**

```
Add a CSV import page to the frontend. Create a new template at app/templates/import.html that has:
- A file upload form for CSV files
- A preview table showing the first 5 rows before import
- A submit button that POSTs to /api/contacts/import
- A results summary after import completes
Add a link to it from the main navigation.
```

### Stretch — Custom Subagent Definition

```bash
$ mkdir -p .claude/agents && cat > .claude/agents/reviewer.md << 'EOF'
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
EOF
```

**Invoke it:**

```
Use the reviewer agent to review the changes I just made.
```

---

## Quick Reference

| Command | Use when |
|---------|----------|
| `/clear` | Between unrelated tasks |
| `/compact` | Context getting long mid-session |
| `Esc` | Stop Claude mid-action |
| `Esc + Esc` | Rewind to checkpoint |
| `--resume` | Pick up previous session |

---

*Stop Typing, Start Orchestrating — RVATech Data Summit, March 26, 2026*
