---
layout: default
title: Approach & Sources
---

# Workshop Approach & Source Material

## Reference Guide for: *Stop Typing, Start Orchestrating*

This document captures the citable sources, key concepts, and practitioner-backed methods that underpin the workshop content. It serves as the detailed reference layer — use it for speaker notes, slide annotations, and exercise design. The [run-of-show](run-of-show.md) cross-references sections here by tag (e.g., `→ Approach §2A`).

*Last updated: 2026-03-11*

---

## Table of Contents

1. [Key Sources](#1-key-sources)
2. [Core Concepts & Frameworks](#2-core-concepts--frameworks)
3. [Boris Cherny's Personal Workflow](#3-boris-chernys-personal-workflow)
4. [Claude Code Best Practices (Official)](#4-claude-code-best-practices-official)
5. [Multi-Agent Patterns](#5-multi-agent-patterns)
6. [Context Engineering](#6-context-engineering)
7. [Notable Data Points](#7-notable-data-points)
8. [Workshop Narrative Thread](#8-workshop-narrative-thread)

---

## 1. Key Sources

### Primary (Anthropic Official)

| Tag | Source | URL | Date | Notes |
|-----|--------|-----|------|-------|
| **SRC-BP** | "Best Practices for Claude Code" — Claude Code Docs | https://code.claude.com/docs/en/best-practices | Ongoing | Official best practices guide; canonical reference for prompting, verification, CLAUDE.md, subagents, and scaling |
| **SRC-CE** | "Effective Context Engineering for AI Agents" — Anthropic Engineering Blog | https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents | 2025-09-29 | Framework for managing context as a finite resource; introduces compaction, sub-agent architectures, just-in-time retrieval |
| **SRC-AT** | "Agent Teams" — Claude Code Docs | https://code.claude.com/docs/en/agent-teams | Ongoing | Official docs for experimental multi-agent coordination with shared task lists and inter-agent messaging |
| **SRC-SA** | "Create Custom Subagents" — Claude Code Docs | https://code.claude.com/docs/en/sub-agents | Ongoing | Official docs for subagent configuration, patterns, and use cases |
| **SRC-CR** | "Code Review for Claude Code" — Claude Blog | https://claude.com/blog/code-review | 2026-03-09 | Multi-agent PR review system; dispatches parallel agents that cross-verify findings |
| **SRC-CC** | "Building a C Compiler with Agent Teams" — Anthropic Engineering | https://www.anthropic.com/engineering/building-c-compiler | 2026 | Case study: 16-agent team, ~2000 sessions, 100K-line Rust C compiler |
| **SRC-HT** | "How Anthropic Teams Use Claude Code" — Anthropic Blog | https://www.anthropic.com/news/how-anthropic-teams-use-claude-code | 2026 | Internal usage patterns across engineering, PM, design, and data science teams |

### Secondary (Boris Cherny Workflow & Interviews)

| Tag | Source | URL | Date | Notes |
|-----|--------|-----|------|-------|
| **SRC-BW** | "How Boris Uses Claude Code" — howborisusesclaudecode.com | https://howborisusesclaudecode.com | 2026-01 | Boris's personal workflow post; parallel sessions, slash commands, subagents, CLAUDE.md |
| **SRC-BC-X** | Boris Cherny's X/Threads posts on workflow | https://www.threads.com/@boris_cherny/post/DTBVlMIkpcm | 2026-01 | Original viral thread on his setup |
| **SRC-PE** | "Building Claude Code with Boris Cherny" — The Pragmatic Engineer | https://newsletter.pragmaticengineer.com/p/building-claude-code-with-boris-cherny | 2026 | Deep-dive interview with Gergely Orosz |
| **SRC-LN** | "Head of Claude Code: What Happens After Coding Is Solved" — Lenny's Newsletter | https://www.lennysnewsletter.com/p/head-of-claude-code-what-happens | 2026 | Product/strategy perspective on the shift from typing to orchestrating |
| **SRC-FT** | "Claude Code Gives Anthropic Its Viral Moment" — Fortune | https://fortune.com/2026/01/24/anthropic-boris-cherny-claude-code-non-coders-software-engineers/ | 2026-01-24 | Broader industry framing |

---

## 2. Core Concepts & Frameworks

### §2A — The Three Skills of Agentic Coding

**Used in:** Block 1 (Why Agentic Coding?)

The workshop is organized around three meta-skills that define effective agentic coding:

1. **Problem Decomposition** — Breaking work into agent-sized tasks. The official best practices guide (SRC-BP) frames this as "Explore first, then plan, then code" — a four-phase workflow: Explore → Plan → Implement → Commit. Boris Cherny demonstrates this in practice by having agents plan before implementing, and using subagents to handle discrete phases (SRC-BW).

2. **Trust Calibration** — Knowing when agent output is reliable and when it needs verification. The single highest-leverage practice per Anthropic's docs (SRC-BP) is giving the agent a way to verify its own work: tests, screenshots, expected outputs. Without clear success criteria, "you become the only feedback loop, and every mistake requires your attention." The Code Review product (SRC-CR) extends this principle to multi-agent cross-verification.

3. **Workflow Design** — Chaining agent steps into reliable pipelines. This ranges from single-session orchestration loops (Plan → Implement → Test → Fix) to multi-agent patterns like parallel sessions, Writer/Reviewer, and full Agent Teams (SRC-AT).

### §2B — Context Engineering (Not Just Prompt Engineering)

**Used in:** Block 3 (Prompt Structuring)

Anthropic's engineering team explicitly frames context engineering as the evolution beyond prompt engineering (SRC-CE). Key principles:

- **Context as finite resource:** Models experience "context rot" — diminishing accuracy as token count increases. LLMs have a limited "attention budget" analogous to human working memory.
- **Goal:** Find the smallest set of high-signal tokens that maximize the likelihood of the desired outcome.
- **Right Altitude Principle:** Balance between hardcoded brittle logic (too specific) and vague guidance (too abstract).
- **Just-in-time retrieval:** Maintain lightweight identifiers (file paths, queries) instead of pre-loading all data; let agents dynamically fetch what they need.

The practical implication for the workshop: the difference between a vague prompt and a structured prompt isn't just about being "more specific" — it's about engineering the right context so the model can do its best work.

### §2C — The Explore → Plan → Implement → Commit Loop

**Used in:** Block 4 (Task Orchestration)

The official best practices (SRC-BP) define a four-phase workflow:

1. **Explore** — Enter Plan Mode. Read files. Understand the landscape. No changes.
2. **Plan** — Ask for a detailed implementation plan. Review and edit it. Press Ctrl+G to open the plan in your editor.
3. **Implement** — Switch to Normal Mode. Let the agent code against the plan. Include verification: "run the test suite and fix any failures."
4. **Commit** — "Commit with a descriptive message and open a PR."

**When to skip planning:** For small, well-defined changes — "if you could describe the diff in one sentence, skip the plan." Planning adds overhead and should be reserved for uncertain approaches, multi-file changes, or unfamiliar code.

### §2D — Verification as Highest-Leverage Practice

**Used in:** Blocks 3 and 4

From the official best practices (SRC-BP):

> "Claude performs dramatically better when it can verify its own work."

Three verification strategies from the docs:

| Strategy | Before | After |
|----------|--------|-------|
| Provide verification criteria | "implement a function that validates email addresses" | "write a validateEmail function. example test cases: user@example.com is true, invalid is false, user@.com is false. run the tests after implementing" |
| Verify UI changes visually | "make the dashboard look better" | "[paste screenshot] implement this design. take a screenshot of the result and compare it to the original" |
| Address root causes | "the build is failing" | "the build fails with this error: [paste error]. fix it and verify the build succeeds. address the root cause, don't suppress the error" |

Giving Claude a 2-3x quality improvement through verification is perhaps the single most important point for workshop attendees to internalize.

---

## 3. Boris Cherny's Personal Workflow

**Used in:** Blocks 1, 4, and 5 (as practitioner credibility)

### §3A — Parallel Session Setup

Boris runs many sessions in parallel (SRC-BW, SRC-BC-X):
- **5 local sessions** in iTerm2 terminal tabs
- **5-10 web sessions** on claude.ai, handing off between local/web/mobile using `/teleport`
- Uses **iTerm2 system notifications** to get alerted when a session needs input
- All coding done with **Opus with extended thinking** — slower but higher quality, fewer corrections needed

### §3B — Slash Commands as Inner-Loop Automation

Boris uses slash commands for every repeated workflow (SRC-BC-X):
- Commands live in `.claude/commands/` and are checked into git
- Example: `/commit-push-pr` — invoked "dozens of times daily"
- Other examples: `/simplify` (code simplification subagent), `/verify-app` (end-to-end test runner)
- Reduces repeated prompting and makes workflows shareable with the team

### §3C — CLAUDE.md as Team Memory

Each team at Anthropic maintains a CLAUDE.md in git (SRC-BW, SRC-HT):
- Documents past mistakes so Claude can learn and avoid repeating them
- Captures style conventions, design guidelines, PR templates, build commands
- Treated like code: reviewed when things go wrong, pruned regularly
- Official guidance (SRC-BP): "For each line, ask: 'Would removing this cause Claude to make mistakes?' If not, cut it."

### §3D — Subagents for Phased Workflows

Boris deploys specialized subagents for different development phases (SRC-BW):
- **Code simplifier** — runs after main implementation to clean up architecture
- **Verify-app agent** — runs end-to-end tests before shipping
- Key principle: subagents run in their own context window, keeping the main conversation clean

### §3E — Team Philosophy

- **Underfund projects intentionally** — one great engineer + unlimited tokens ships faster because they're forced to leverage AI maximally (SRC-PE)
- 100% of Boris's code has been written by AI since November 2025 — zero manual edits (SRC-BW)
- Everyone on the Claude Code team codes: PMs, designers, finance, data scientists. 50%+ overlap between engineering, product, and design roles (SRC-FT)

---

## 4. Claude Code Best Practices (Official)

**Used in:** Blocks 2, 3, and 4

### §4A — CLAUDE.md Authoring

From the official best practices (SRC-BP):

**Include:**
- Bash commands Claude can't guess
- Code style rules that differ from defaults
- Testing instructions and preferred test runners
- Repository etiquette (branch naming, PR conventions)
- Architectural decisions specific to the project
- Developer environment quirks (required env vars)
- Common gotchas or non-obvious behaviors

**Exclude:**
- Anything Claude can figure out by reading code
- Standard language conventions Claude already knows
- Detailed API documentation (link to docs instead)
- Information that changes frequently
- Long explanations or tutorials
- File-by-file descriptions of the codebase
- Self-evident practices like "write clean code"

Run `/init` to generate a starter CLAUDE.md based on current project structure.

### §4B — Providing Specific Context in Prompts

Four strategies from the docs (SRC-BP):

1. **Scope the task** — Specify which file, what scenario, testing preferences
2. **Point to sources** — Direct Claude to the source that can answer a question (e.g., "look through git history")
3. **Reference existing patterns** — Point Claude to patterns in your codebase (e.g., "HotDogWidget.php is a good example")
4. **Describe the symptom** — Provide the symptom, likely location, and what "fixed" looks like

### §4C — Rich Input Methods

- `@` references to include files directly
- Paste images (screenshots, mockups) directly into prompts
- Give URLs for documentation and API references
- Pipe data: `cat error.log | claude`
- Tell Claude to fetch its own context using Bash, MCP, or file reads

### §4D — Session Management Anti-Patterns

From the "Avoid Common Failure Patterns" section (SRC-BP):

1. **The kitchen sink session** — Mixing unrelated tasks in one session. Fix: `/clear` between tasks.
2. **Correcting over and over** — After two failed corrections, `/clear` and write a better initial prompt.
3. **The over-specified CLAUDE.md** — Too long, Claude ignores half of it. Fix: ruthlessly prune.
4. **The trust-then-verify gap** — Plausible output without edge case handling. Fix: always provide verification.
5. **The infinite exploration** — Unscoped investigation fills context. Fix: scope narrowly or use subagents.

### §4E — Session Commands Quick Reference

| Command | Purpose |
|---------|---------|
| `/clear` | Reset context between unrelated tasks |
| `/compact` | Summarize conversation to free context |
| `/compact <focus>` | Summarize with specific focus (e.g., "Focus on the API changes") |
| `/rewind` or `Esc+Esc` | Restore conversation/code to a previous checkpoint |
| `/init` | Generate starter CLAUDE.md |
| `/btw` | Side question that doesn't enter conversation history |
| `Esc` | Stop Claude mid-action (context preserved) |
| `--continue` | Resume most recent conversation |
| `--resume` | Select from recent conversations |

---

## 5. Multi-Agent Patterns

**Used in:** Block 5

### §5A — Subagents (Single Session)

From the official docs (SRC-SA):

Subagents run in their own context window with custom system prompts, specific tool access, and independent permissions. Key properties:
- **Preserve context** — exploration stays out of main conversation
- **Enforce constraints** — limit which tools a subagent can use
- **Control costs** — route tasks to faster, cheaper models (e.g., Haiku for exploration)
- **Cannot spawn other subagents** — single level of delegation only

Built-in subagents:
- **Explore** (Haiku) — read-only codebase search and analysis
- **Plan** — read-only research for plan mode
- **General-purpose** — multi-step tasks requiring both exploration and action

Common patterns:
- **Isolate high-volume operations** — "Use a subagent to run the test suite and report only the failing tests"
- **Parallel research** — "Research the auth, database, and API modules in parallel using separate subagents"
- **Chained subagents** — "Use the code-reviewer subagent to find performance issues, then use the optimizer subagent to fix them"

### §5B — Agent Teams (Multi-Session)

From the official docs (SRC-AT):

Agent Teams coordinate multiple Claude Code instances with:
- A **team lead** that creates the team, spawns teammates, coordinates work
- **Teammates** that work independently in their own context windows
- A **shared task list** with pending/in-progress/completed states and dependency tracking
- A **mailbox** for inter-agent messaging

Best use cases:
- Research and review (parallel investigation)
- New modules/features (each teammate owns a separate piece)
- Debugging with competing hypotheses
- Cross-layer coordination (frontend, backend, tests)

Key guidance:
- Start with **3-5 teammates** for most workflows
- Aim for **5-6 tasks per teammate**
- Teammates **do not inherit** the lead's conversation history
- Use **split-pane mode** (tmux/iTerm2) for visibility, or **in-process mode** (Shift+Down to cycle)

### §5C — Writer/Reviewer Pattern

From the official best practices (SRC-BP):

| Session A (Writer) | Session B (Reviewer) |
|---|---|
| "Implement a rate limiter for our API endpoints" | |
| | "Review the rate limiter implementation in @src/middleware/rateLimiter.ts. Look for edge cases, race conditions, and consistency with our existing middleware patterns." |
| "Here's the review feedback: [Session B output]. Address these issues." | |

A fresh context improves code review since Claude won't be biased toward code it just wrote.

### §5D — Fan-Out Pattern

From the official best practices (SRC-BP):

For large migrations or batch operations:
1. Have Claude generate a task list (e.g., "list all 2,000 Python files that need migrating")
2. Loop through with non-interactive mode: `claude -p "Migrate $file..." --allowedTools "Edit,Bash(git commit *)"`
3. Test on 2-3 files, refine prompt, then run at scale

### §5E — Code Review as Multi-Agent System (Production Example)

Anthropic's Code Review product (SRC-CR), launched March 9, 2026:
- Dispatches **multiple AI agents in parallel** when a PR is opened
- Agents independently search for bugs, then **cross-verify each other's findings** to filter false positives
- Remaining issues are **ranked by severity**
- Before implementation: 16% of PRs got substantive review comments. After: 54%
- Typical cost: $15-$25 per review; ~20 minute completion time

### §5F — C Compiler Case Study (Agent Teams at Scale)

From Anthropic Engineering (SRC-CC):
- **16 agents** tasked with writing a Rust-based C compiler from scratch
- ~**2,000 Claude Code sessions**, ~$20,000 in API costs
- Produced **100,000 lines** of code
- Result: a compiler capable of building the Linux kernel on x86, ARM, and RISC-V

---

## 6. Context Engineering

**Used in:** Blocks 3 and 4 (deeper theory for speaker notes)

### §6A — Core Principles

From Anthropic's context engineering guide (SRC-CE):

- **Context rot** — model accuracy diminishes as token count increases
- **Attention budget** — analogous to human working memory; finite and precious
- **n² pairwise relationships** — transformer architecture means focus stretches thin as context grows
- **Progressive capability matching** — smarter models require less prescriptive engineering; "do the simplest thing that works"

### §6B — Long-Horizon Task Techniques

Three strategies from (SRC-CE) for tasks that exceed a single context window:

1. **Compaction** — Summarize conversation contents nearing limits. Preserve: architectural decisions, unresolved issues, implementation details. Discard: redundant tool outputs.
2. **Structured note-taking** — Agents persist external notes (NOTES.md, to-do lists) outside context windows for later retrieval. Enables progress tracking and long-horizon coherence.
3. **Sub-agent architectures** — Specialized agents handle focused tasks with clean context windows; each returns condensed summaries (1,000-2,000 tokens). Main agent synthesizes.

### §6C — Tool Design Principles

From (SRC-CE):
- Tools should be self-contained, error-robust, and unambiguous in purpose
- Overlapping or bloated tool sets confuse agents about selection logic
- "If a human engineer can't definitively say which tool to use, an AI agent can't do better"

---

## 7. Notable Data Points

**For slides, speaker notes, and credibility building:**

| Stat | Source |
|------|--------|
| 4% of all public GitHub commits authored by Claude Code; predicted to hit 20% by end of 2026 | SRC-BW, SRC-FT |
| 100% of Boris Cherny's code written by AI since November 2025 (zero manual edits) | SRC-BW |
| Code output per Anthropic engineer has grown 200% in the last year | SRC-CR |
| Before Code Review: 16% of PRs got substantive comments. After: 54% | SRC-CR |
| C compiler case study: 16 agents, ~2K sessions, $20K, 100K lines of code | SRC-CC |
| Verification gives 2-3x quality improvement on agent output | SRC-BW |
| Boris runs 5 local + 5-10 web Claude sessions in parallel daily | SRC-BW, SRC-BC-X |
| Everyone on the Claude Code team codes — PMs, designers, finance, data scientists | SRC-FT |

---

## 8. Workshop Narrative Thread

**The through-line tying all blocks together:**

> **You're not replacing developers. You're giving every developer a team.**

1. **Block 1 (Why):** The shift from typing to orchestrating. Three skills: decompose, calibrate trust, design workflows. (§2A)
2. **Block 2 (Navigate):** Your first interaction with the "team." Ask questions like you'd ask a senior engineer. The agent reads files, greps, follows imports. (§4B, §4C)
3. **Block 3 (Prompt):** Context engineering, not prompt engineering. The quality of your input determines the quality of the agent's output. Structured prompts, verification criteria, CLAUDE.md. (§2B, §2D, §4A)
4. **Block 4 (Orchestrate):** The Explore → Plan → Implement → Commit loop. Plan mode, course correction, checkpoint/rewind. Session management as a skill. (§2C, §4D, §4E)
5. **Block 5 (Multi-Agent):** Scale from one agent to a team. Subagents, parallel sessions, Writer/Reviewer, Agent Teams. Production example: Code Review. (§5A–§5F)
6. **Block 6 (Wrap-Up):** Anchor the three skills. Real-world applications. Resources. (§2A)

---

*This document is the reference layer. For timing and flow, see [Run of Show](run-of-show.md).*
