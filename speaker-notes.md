---
layout: default
title: Speaker Notes
---

# Speaker Notes

## Stop Typing, Start Orchestrating — RVATech Data & AI Summit 2026

**How to use this document:** Notes are keyed to slide numbers. Each entry tells you what's on screen, what to say, what to do with your hands (screen switches, typing in terminal, advancing fragments), and how to transition to the next slide. Rehearse with the deck open — advance through fragments as you read each note.

**Screen setup:** Chrome with `presentation.html` on one side. Terminal with Claude Code in `mini-crm` on the other. You'll be switching between them starting at Block 2. Have iTerm2 (or your terminal) ready with two tabs for Block 5's Writer/Reviewer demo.

**Pre-flight checklist:**
- [ ] Presentation loaded in Chrome, slide 1 visible
- [ ] Terminal open in `mini-crm`, Claude Code *not yet launched* (you'll launch it live in Block 0)
- [ ] Second terminal tab ready (empty) for Block 5
- [ ] `mini-crm` freshly seeded: `python3 scripts/reset_db.py && python3 scripts/seed.py`
- [ ] Exercise cards URL or file ready to share (drop link in chat/Slack when you reach Block 2)
- [ ] Fallback: if Wi-Fi dies, have pre-run terminal output screenshots in a local folder

**Emoji legend — quick reference:**

| Emoji | Meaning |
|-------|---------|
| ▶️ | Advance fragment / do this next |
| ⏸️ | Pause — let it breathe |
| ⏭️ | Transition to next slide |
| 🌐 | Switch to / you're in Chrome |
| 💻 | Switch to / you're in Terminal |

---

## Slide 1 — Title Slide

**On screen:** Title slide — "Stop Typing, Start Orchestrating"

**Say:** Nothing yet. This is up while people settle in. ⏸️ Let it breathe for 30 seconds.

⏭️ **Transition → Slide 2:** "Alright, let's get started."

---

## Slide 2 — Block 0 Divider: Setup & Orientation

**On screen:** Section divider — "Block 0 · Setup & Orientation · 0:00–0:05"

**Say:** "We've got 70 minutes together. Before we dive in, let's make sure everyone's set up."

⏭️ **Transition → Slide 3:** Advance immediately.

---

## Slide 3 — Quick Check

**On screen:** Fragment list — "Who's used an AI coding tool?" / "Who's used one from a terminal?" / Prerequisites list

**Say + Do:**

- ▶️ [advance fragment] "Quick show of hands — who's used an AI coding tool before? Copilot, Cursor, ChatGPT for code, anything." ⏸️ [pause, scan the room]
- ▶️ [advance fragment] "Okay, now — who's used one from a *terminal*?" ⏸️ [pause — expect fewer hands] "Perfect. That's exactly why we're here."
- ▶️ [advance fragment] "You'll need three things."
- ▶️ [advance fragments for each prereq] "Terminal open. Claude Code installed and authenticated. And the workshop repo cloned — that's `github.com/busse/mini-crm`."

**If people are stuck:** "If you're not set up yet, pull up the setup instructions — I'll drop the link in chat. You can follow along and catch up during the first demo."

⏭️ **Transition → Slide 4:** "Now let me set the frame for the next 70 minutes."

---

## Slide 4 — The Frame for Today

**On screen:** Blockquote — "For the next 70 minutes, you're not writing code. You're directing an agent that writes code." + screenshot placeholder

**Say:** Read the quote aloud, slowly. ⏸️ Let it land. Then: "That's the mindset shift. We're going from typing to orchestrating. And by the end of this session, you'll have practiced the actual skills to do it."

💻 **Switch to terminal.** Launch Claude Code live: type `claude` and hit enter. Let the room see it boot up. "This is Claude Code. It's a terminal-native coding agent from Anthropic. No IDE plugin, no web UI — just your terminal."

🌐 **Switch back to Chrome.**

⏭️ **Transition → Slide 5:** "So why does this matter? Why agentic coding, why now?"

---

## Slide 5 — Block 1 Divider: Why Agentic Coding?

**On screen:** Section divider — "Block 1 · Why Agentic Coding? · 0:05–0:10"

**Say:** Nothing extra. ▶️ Advance.

⏭️ **Transition → Slide 6:** Advance immediately.

---

## Slide 6 — The Shift

**On screen:** Fragment progression — "autocomplete → copilot → agent" + "The bottleneck moved from writing to directing."

**Say + Do:**

- ▶️ [advance] "Three years ago, autocomplete. GitHub Copilot, tab-complete. Helpful, but you were still driving."
- ▶️ [advance] "Then copilot mode. Inline suggestions, chat panels. You're still writing the code, but with a really smart pair programmer."
- ▶️ [advance] "Now — agents. You describe the task. The agent reads files, makes plans, writes code, runs tests, fixes bugs. *You* review and direct."
- ▶️ [advance] "The bottleneck moved. It used to be about how fast you could type. Now it's about how well you can direct."

⏭️ **Transition → Slide 7:** "So what does 'directing well' actually mean? Three skills."

---

## Slide 7 — Three Skills That Matter Now

**On screen:** Numbered list with fragments — decomposition, trust calibration, workflow design

**Say + Do:**

- ▶️ [advance] "One: problem decomposition. Can you break a fuzzy goal into concrete, agent-sized tasks? A task an agent can finish in one conversation?"
- ▶️ [advance] "Two: trust calibration. When do you read every line of agent output, and when do you ship it? How do you give the agent a way to check its own work?"
- ▶️ [advance] "Three: workflow design. How do you chain multiple agent interactions into something that actually ships? Not a one-shot miracle — a repeatable loop."
- ▶️ [advance] "These three skills are the structure for the rest of the workshop. Everything we do maps back to one of them."

⏭️ **Transition → Slide 8:** "And this isn't theoretical. Let me show you the numbers."

---

## Slide 8 — The Numbers

**On screen:** Three stat callouts — 4%, 200%, 100%

**Say + Do:**

- ▶️ [advance] "Four percent of all public GitHub commits are now authored by Claude Code. Predicted to hit twenty percent by end of this year." ⏸️ [pause] "That's not autocomplete suggestions — those are full commits."
- ▶️ [advance] "Anthropic's own engineering org has seen two hundred percent growth in code output per engineer, year over year. Same headcount."
- ▶️ [advance] "And this one's my favorite. Boris Cherny, who leads the Claude Code team at Anthropic — he hasn't manually written a single line of code since November 2025. One hundred percent AI-generated. Zero hand edits." ⏸️ [pause] "He orchestrates. We're going to learn how he does it."

⏭️ **Transition → Slide 9:** "Okay — enough slides. Let's see it work. From here on out, we're in the terminal."

---

## Slide 9 — Block 2 Divider: Codebase Navigation

**On screen:** Section divider — "Block 2 · Demo + Exercise · Codebase Navigation · 0:10–0:20"

**Say:** "Block 2 — your first real interaction with Claude Code. We're going to explore the mini-CRM repo."

💻 **Switch to terminal.** Claude Code should already be running from Block 0.

⏭️ **Transition → Slide 10:** Leave the slide up briefly, then advance. You'll be mostly in the terminal for the next few minutes.

---

## Slide 10 — Your First Conversation

**On screen:** Example prompts + screenshot placeholder

💻 **You should be in the terminal now.** The slide is reference — don't linger on it. Switch to terminal.

**DEMO — Do this live (3 min):**

1. Type: `What does this project do?`
   - Let Claude read files, grep, explore. Narrate the tool-use trace: "Watch — it's reading the README, looking at the directory structure, opening main.py. I didn't tell it which files to look at."

2. Type: `Where is the main entry point?`
   - Quick answer. "It found it. Traced the FastAPI app setup."

3. Type: `Walk me through the request lifecycle for POST /api/deals`
   - This is the impressive one. Claude will follow router → schema → model → database. "Notice: it followed imports across files. It read the router, found the schema, checked the model definition, traced the database call. That's agentic search — glob, grep, read, all driven by the model."

⏭️ **Transition → Slide 11:** 🌐 Switch back to Chrome. "Let's talk about what just happened."

---

## Slide 11 — What Just Happened

**On screen:** Fragment list — chose files, followed imports, synthesized narrative + "You didn't open a single file manually"

**Say + Do:**

- ▶️ [advance] "Claude's agentic search is plain text tools — glob, grep, read — but driven by the model's reasoning. It *chose* which files to open."
- ▶️ [advance] "It followed imports across modules on its own."
- ▶️ [advance] "And it synthesized a narrative answer — not just dumped file contents."
- ▶️ [advance] "You didn't open a single file manually. And you've already got a mental model of the codebase."

⏭️ **Transition → Slide 12:** "Your turn. Seven minutes."

---

## Slide 12 — Exercise: Codebase Navigation

**On screen:** Exercise box — 4 steps, 7 minutes

**Say:** "Same repo, your machines. Four tasks, increasing depth. Warm up with a project summary. Find where auth lives. Then trace what happens when a deal gets created — that one's meaty. And if you finish early, ask Claude to find bugs — there are real ones in there." [smile]

**Drop the exercise cards link now** if you haven't already.

💻 **Switch to terminal** so the audience sees a Claude Code session while they work. You can quietly do the same exercise or prep for the next demo.

**Timer: 7 minutes.** At 6 minutes, give a one-minute warning.

**Debrief (30 sec):** 🌐 Switch back to Chrome briefly. "Quick takeaway — you just explored an entire codebase without opening a file browser. The agent did the reading. That's skill number one: knowing how to ask."

⏭️ **Transition → Slide 13:** "Now let's talk about *how* you ask."

---

## Slide 13 — Block 3 Divider: Prompt Structuring

**On screen:** Section divider — "Block 3 · Demo + Exercise · Prompt Structuring · 0:20–0:30"

**Say:** "Block 3 — this is where the quality of your input starts to matter a lot."

⏭️ **Transition → Slide 14:** Advance.

---

## Slide 14 — Context Engineering, Not Just Prompting

**On screen:** Fragment list — context rot, attention budget, quality in/quality out + source citation

**Say + Do:**

- "You'll hear people say 'prompt engineering.' I want to reframe that. Anthropic's engineering team calls this *context engineering*. Here's why."
- ▶️ [advance] "Context rot. As the token count grows, accuracy drops. The model's ability to attend to the right information diminishes."
- ▶️ [advance] "Think of it as an attention budget — like human working memory. It's finite. Every token you send is spending part of that budget."
- ▶️ [advance] "So the goal isn't just being specific. It's curating the *smallest set of high-signal tokens* that maximize the model's chance of success."

⏭️ **Transition → Slide 15:** "Let me show you what that looks like in practice."

---

## Slide 15 — Vague vs. Structured

**On screen:** Compare boxes — red (vague: "Add a search feature") / green (structured: full spec)

**Say + Do:**

- "Here's the same task, two ways." [point to red box] "'Add a search feature.' That's what most people type."
- ▶️ [advance] [point to green box] "Now look at this one. It specifies the endpoint, the query parameter, the fields to search, the response format, and that we want tests."
- ▶️ [advance] "Let's run both live and compare."

💻 **Switch to terminal.**

**DEMO — Vague vs. Structured (3 min):**

1. `/clear` first. Type the vague prompt: `Add a search feature`
   - Let it run. It'll probably do *something* — but it'll guess at the implementation, maybe search the wrong fields, maybe skip tests.
   - After it finishes (or after ~60 seconds), `Esc` to stop if it's going too long.
   - Scroll through the output briefly. "Look at what it chose to do. Did it search the right fields? Did it add tests? Probably not."

2. **Reset the code before the second run.** Exit Claude Code (`/exit` or Ctrl+C), then:
   ```
   git checkout . && git clean -fd
   ```
   Narrate: "I'm throwing that away. Clean slate. Now let's do it right."
   Re-launch Claude Code: `claude`

3. Type the structured prompt (you can paste it):
   ```
   Add a search endpoint to the API: accepts a query param `q`, searches the `first_name`, `last_name`, and `email` fields in the contacts table, returns paginated JSON matching the existing list endpoint format. Add tests.
   ```
   - This one should produce clean, correct code in one pass.

4. "See the difference? Same task. The structured version gave Claude enough context to get it right the first time. And I didn't have to correct it."

🌐 **Switch back to Chrome.**

⏭️ **Transition → Slide 16:** "There's a pattern for this."

---

## Slide 16 — The DECOMPOSE Pattern

**On screen:** Mnemonic list — D/E/C/O/M + stat callout (2-3x)

**Say:**

"DECOMPOSE. Five letters, five questions to answer before you hit enter."

- "**D** — Define the outcome. What exactly should happen when this is done?"
- "**E** — Existing patterns. What does the codebase already do that Claude should follow?"
- "**C** — Constraints. Edge cases, limits, things to avoid."
- "**O** — Output format. Files, endpoints, schemas — be specific."
- "**M** — Measure of done. How will you know it works? Tests? Manual check?"

▶️ [advance stat callout] "Anthropic's data shows that just adding verification criteria — the M — gives you a two to three X quality improvement in agent output. That's the single highest-leverage thing you can do."

⏭️ **Transition → Slide 17:** "Your turn. Use this pattern."

---

## Slide 17 — Exercise: Prompt Structuring

**On screen:** Exercise box — "favorite contacts" feature, 6 minutes

**Say:** "Add a favorite contacts feature. But here's the rule: write your prompt *before* you send it. Spend two minutes composing it using DECOMPOSE. The exercise card has a scaffold if you want a starting point. Then run it and compare with your neighbor."

💻 **Switch to terminal.** Display your Claude Code session while they work.

**Timer: 6 minutes.** At 5 minutes, one-minute warning.

**Debrief (30 sec):** "How many people got working code on the first pass? [hands] How many needed to refine? [hands] That refinement loop — that's normal. The structured prompt just gets you *closer* on the first try."

⏭️ **Transition → Slide 18:** "Now let's chain this into a full workflow."

---

## Slide 18 — Block 4 Divider: Task Orchestration

**On screen:** Section divider — "Block 4 · Demo + Exercise · Task Orchestration & Iteration · 0:30–0:45"

**Say:** "Block 4 — this is the biggest block. Fifteen minutes. We're going to build a real feature end-to-end."

⏭️ **Transition → Slide 19:** Advance.

---

## Slide 19 — The Orchestration Loop

**On screen:** Fragment chain — Explore → Plan → Implement → Commit

**Say + Do:**

- ▶️ [advance each fragment with a beat]
- "The official Claude Code best practice is a four-step loop."
- "Explore — read the code, understand the landscape. No changes."
- "Plan — ask for an implementation plan. Review it. Adjust it."
- "Implement — let the agent code against the plan."
- "Commit — verify, then commit."
- ▶️ [advance final note] "Not every task needs every step. Small changes, skip the plan. But for anything non-trivial, this loop saves you from bad implementations."

⏭️ **Transition → Slide 20:** "Let me walk through it live."

---

## Slide 20 — Demo: Building a Feature End-to-End

**On screen:** Numbered steps — email notifications on deal stage change

💻 **Switch to terminal.** `/clear` to start fresh.

**DEMO — The Full Loop (5 min):**

1. **Explore:** Type: `Read the deal router and deal service. How do deal stage transitions work?`
   - Narrate: "I'm in exploration mode. I'm not asking it to build anything yet — I'm asking it to *read* for me."

2. **Plan:** Type: `I want to add email notifications when a deal moves to Closed Won. Create a detailed implementation plan — list the files you'll modify and the order of operations. Don't write code yet.`
   - When the plan appears: "Now I'm reviewing the plan like a tech lead. Does this make sense? Are there things it missed?" Scan it out loud. If something's off, correct it.

3. **Implement:** Type: `Go ahead and implement the plan. Run tests after each major change.`
   - Let it run. Narrate key moments: "It's creating the notification module... now updating the deal service... running tests..."
   - **If a test fails** (likely — this is live code): "Great, an error. This is *normal*. Watch what happens."

4. **Debug:** Copy the error, type: `I got this error: [paste]. Fix it.`
   - "I'm feeding the error back. I'm not debugging it myself — I'm giving Claude the context to fix it."

5. **Verify:** Type: `Run the full test suite and show me results.`
   - "Green? Good. That's one full loop: explore, plan, implement, verify."

🌐 **Switch back to Chrome.**

⏭️ **Transition → Slide 21:** "A few tools that make this loop smoother."

---

## Slide 21 — Session Management

**On screen:** Table — /clear, /compact, Esc, Esc+Esc, --resume, /btw

**Say:** "Quick reference — these are the commands you'll use constantly."

- "/clear — nuclear reset. Use between unrelated tasks."
- "/compact — summarizes the conversation to free up context. Use mid-session when things get long."
- "Esc — stops Claude mid-action but keeps your context. Esc twice rewinds to a checkpoint."
- "--resume — picks up where you left off in a previous session. Great for next-day continuations."
- "/btw — side question that doesn't pollute your conversation history. 'Hey, what's the syntax for X?' without derailing your feature work."

⏭️ **Transition → Slide 22:** "And some things to avoid."

---

## Slide 22 — Anti-Patterns

**On screen:** Fragment list — kitchen sink, correcting over and over, trust-then-verify gap

**Say + Do:**

- ▶️ [advance] "The kitchen sink session. You start with 'add a login page,' then 'oh also fix this CSS,' then 'and refactor the database layer.' Don't. /clear between unrelated tasks."
- ▶️ [advance] "Correcting over and over. If Claude gets something wrong twice, don't keep nudging. /clear and write a better prompt. Your second attempt will be better than your fifth correction."
- ▶️ [advance] "The trust-then-verify gap. Claude's output *looks* right. It compiles. It runs. But did it handle the edge case? Always include verification criteria — you are the only feedback loop otherwise."

⏭️ **Transition → Slide 23:** "One more line to anchor this."

---

## Slide 23 — Tech Lead Quote + Exercise

**On screen:** Blockquote + exercise box — choose a task, follow the loop, 10 minutes

**Say:** Read the quote: "You're a tech lead doing code review in real-time, not a developer typing." Then: "Your turn. Ten minutes. Pick one of three features — rate limiting, CSV export, or admin role. Follow the loop: explore, plan, implement, verify. The exercise card has the details. Don't try to do it in one shot — that's the whole point."

💻 **Switch to terminal.** Work on one of the features yourself while they work.

**Timer: 10 minutes.** Give a two-minute warning at 8 minutes.

**Debrief (30 sec):** "How many people used the plan step? [hands] How many skipped straight to implement? [hands to the skippers] How'd that go? [knowing smile] The plan step is annoying until the first time it saves you from a bad implementation."

⏭️ **Transition → Slide 24:** "Now we level up."

---

## Slide 24 — Block 5 Divider: Multi-Agent Patterns

**On screen:** Section divider — "Block 5 · Demo + Exercise · Multi-Agent Patterns · 0:45–1:00"

**Say:** "Block 5 — this is the advanced section. Everything we've done so far is one agent, one conversation. Now we go to *multiple agents working in parallel*."

⏭️ **Transition → Slide 25:** Advance.

---

## Slide 25 — Pattern 1: Writer/Reviewer

**On screen:** Two-column layout — Tab 1 (Writer) / Tab 2 (Reviewer) + fragment about fresh context

💻 **You need two terminal tabs now.** Set them up side by side if possible.

**DEMO — Writer/Reviewer (3 min):**

1. **Tab 1:** Type: `Add a simple rate limiter to the API — limit to 60 requests per minute per user. Use an in-memory counter. Return 429 when exceeded.`
   - Let it run. Don't wait for it to finish if it's slow.

2. **While Tab 1 works**, switch to **Tab 2.** Launch Claude Code: `claude`
   - Type: `Review the recent changes to this repo related to rate limiting. Look at any new middleware or router changes. Check for: edge cases not handled, race conditions, consistency with existing patterns, test coverage gaps.`
   - "Notice: this is a *fresh* Claude session. It has no knowledge of what Tab 1 did. It's reading the code cold — just like a real code reviewer would."

3. When Tab 2 produces findings, copy them. Switch to **Tab 1.** Type: `A code reviewer found these issues: [paste]. Fix them.`

▶️ [advance fragment] "A fresh context produces unbiased review. Claude won't defend code it just wrote — because it didn't write it, as far as this session knows. You're a manager delegating to two developers."

⏭️ **Transition → Slide 26:** "Next pattern — subagents."

---

## Slide 26 — Pattern 2: Subagents

**On screen:** Two-column layout — built-in subagents list + why subagents

**Stay in terminal for this.**

**DEMO — Subagents (2 min):**

Type in your main Claude session: `Use a subagent to research how the existing codebase handles pagination across all routers. Report back the patterns used and whether they're consistent.`

- "Watch — Claude is going to spawn a separate agent. It runs in its own context window. When it's done, it sends a summary back to my main session."
- While the subagent runs: "Three built-in types. Explore uses Haiku — fast, cheap, read-only. Plan is for research in plan mode. General-purpose has full tools."
- When results come back: "My main session stays clean. The subagent did the reading, and I got a concise summary."

⏭️ **Transition → Slide 27:** "And the big one — agent teams."

---

## Slide 27 — Pattern 3: Agent Teams

**On screen:** Architecture description + screenshot placeholder

**Say:** "This is experimental, so I'm going to walk through the concept rather than live demo it."

- "Agent Teams is multiple Claude Code instances coordinating through shared infrastructure."
- "A team lead decomposes the work, spawns teammates, and synthesizes results."
- "Each teammate has its own context window, its own task queue."
- "They communicate through a shared task list — pending, in-progress, completed — and a mailbox for inter-agent messaging."
- "Think of it like a project manager spinning up a small dev team for a sprint."

⏭️ **Transition → Slide 28:** "And this isn't just a concept. It's in production."

---

## Slide 28 — Real-World Examples

**On screen:** Two columns — Code Review stats + C Compiler case study

**Say:**

[point to left column] "Anthropic's Code Review product, launched two weeks ago. When a PR is opened, it dispatches *multiple agents in parallel*. Each agent independently searches for bugs. Then they *cross-verify each other's findings* to filter false positives. Before this: sixteen percent of PRs got substantive review. After: fifty-four percent."

[point to right column] "And the extreme example — sixteen agents tasked with writing a C compiler in Rust. Two thousand Claude Code sessions. Twenty thousand dollars in API costs. The result: a hundred thousand lines of code that can compile the Linux kernel on x86, ARM, and RISC-V."

⏭️ **Transition → Slide 29:** "This next one's fun."

---

## Slide 29 — Boris Cherny's Daily Setup

**On screen:** Fragment list — 5 local sessions, 5-10 web, notifications, slash commands, Opus + thinking

**Say + Do:**

- ▶️ [advance] "Boris Cherny — head of Claude Code — runs five local sessions in iTerm2 tabs."
- ▶️ [advance] "Plus five to ten web sessions on claude.ai. At the same time."
- ▶️ [advance] "He uses system notifications so he gets pinged when a session needs input. He's managing a team."
- ▶️ [advance] "Slash commands for every repeated workflow. /commit-push-pr — he says he runs that 'dozens of times daily.' /simplify for code cleanup. /verify-app for end-to-end tests."
- ▶️ [advance] "And he uses Opus with extended thinking. Slower, but higher quality. Fewer corrections means less time babysitting."

"This is where the workshop title comes from. He's not typing. He's orchestrating."

⏭️ **Transition → Slide 30:** "Your turn — pick a multi-agent pattern."

---

## Slide 30 — Exercise: Multi-Agent Patterns

**On screen:** Exercise box — 3 options, 8 minutes + stretch

**Say:** "Eight minutes. Pick one of three options — the exercise card has full details for each. Option A: Writer/Reviewer, what we just demoed. Option B: use a subagent to research, then implement. Option C: split a feature across two parallel sessions, backend and frontend. If you finish early, the stretch goal is to create a custom subagent definition file."

💻 **Switch to terminal.** Leave both tabs visible if possible.

**Timer: 8 minutes.** Two-minute warning at 6 minutes.

**Debrief (30 sec):** "Who tried the Writer/Reviewer? What surprised you about the review quality from a fresh context? [take one or two responses] That's the core insight — a separate context is more honest than asking the same agent to review its own work."

⏭️ **Transition → Slide 31:** "Let's bring it home."

---

## Slide 31 — Block 6 Divider: Wrap-Up

**On screen:** Section divider — "Block 6 · Wrap-Up & What's Next · 1:00–1:05"

**Say:** "Five minutes to wrap up."

⏭️ **Transition → Slide 32:** Advance.

---

## Slide 32 — The Three Skills, Revisited

**On screen:** Fragment list — decomposition, trust calibration, workflow design, with block references

**Say + Do:**

- ▶️ [advance] "Problem decomposition — Blocks 2 and 3. You learned to break work into clear, scoped requests that give the agent what it needs."
- ▶️ [advance] "Trust calibration — Blocks 3 and 4. You gave the agent verification criteria. You debugged its output. You learned when to trust and when to check."
- ▶️ [advance] "Workflow design — Blocks 4 and 5. You built orchestration loops, used session management, and ran multiple agents in parallel."

"These three skills transfer to *any* agentic tool. Claude Code is what we used today, but the skills are the point."

⏭️ **Transition → Slide 33:** "Where does this go from here?"

---

## Slide 33 — Where This Applies

**On screen:** Fragment list — onboarding, prototyping, code review, legacy migration

**Say + Do:**

- ▶️ [advance] "Onboarding — you saw this in Block 2. Drop into an unfamiliar codebase, have Claude read it for you, build a mental model in five minutes."
- ▶️ [advance] "Rapid prototyping — idea to working proof of concept in a single session."
- ▶️ [advance] "Code review at scale — we just talked about this. Multi-agent review catches things humans miss."
- ▶️ [advance] "Legacy migration — the fan-out pattern. Generate a task list of 2,000 files to migrate, then batch-process them with Claude in non-interactive mode. It's like MapReduce for code changes."

⏭️ **Transition → Slide 34:** "One last thought."

---

## Slide 34 — Closing Slide

**On screen:** Quote — "You're not replacing developers. You're giving every developer a team." + resource links

**Say:** Read the quote. ⏸️ Pause.

"The workshop repo stays live — you can keep practicing against it. The resources below are the ones I leaned on to build this session."

"The context engineering guide is the one I'd read first if you're going deeper. Best practices doc is your daily reference."

"And I'm at cbusse@singlestoneconsulting.com — happy to talk about this stuff anytime."

⏭️ **Transition → Slide 35:** "We've got five minutes for questions."

---

## Slide 35 — Buffer / Q&A

**On screen:** Section divider — "Q&A · 1:05–1:10" + "Pick a task. Let's orchestrate it live."

**Say:** "Questions? Or — even better — give me a task. Something you'd want to build or fix in your own work. We'll orchestrate it live right here."

💻 **Switch to terminal.** Be ready to type whatever the audience suggests.

**If no questions / quiet room:**
- "Okay, here's one I get a lot: 'what about security? Should I be worried about sending my code to an API?' Short answer: Claude Code runs locally. Your code stays on your machine. The prompts go to the API, but the model doesn't train on them. Check the docs for the full privacy model."
- "Another common one: 'how do I convince my team to use this?' My suggestion — don't pitch it. Use it for a week, ship something noticeably faster, and let people ask you how you did it."

**Closing:** "Thanks for spending 70 minutes with me. Go orchestrate." [end]

---

## Recovery Playbook

Things that might go wrong, and how to handle them:

**Wi-Fi dies mid-demo:**
"This is actually the perfect excuse to talk about fallback planning. I've got pre-run output I can show." Switch to your fallback screenshots folder. Continue narrating.

**Claude Code gives a bad answer live:**
Don't hide it. "See that? It got confused. This is why trust calibration matters. Let me /clear and try a better prompt." This is *better* than a perfect demo — it teaches the skill.

**Claude Code is slow (API latency):**
"While it's thinking — this is a good time to mention that Boris uses Opus with extended thinking. Slower per-response, but fewer corrections. The total time to a working feature is often less."

**Someone's Claude Code isn't working:**
"Pair up with your neighbor for now. One person drives, one navigates. That's actually how a lot of teams work — one agent, two humans reviewing."

**You run long on a block:**
Cut the debrief, not the exercise. People learn more from doing than from listening to you summarize. If you're behind by Block 4, shorten the demo and give full exercise time.

**Someone asks about pricing/costs:**
"Claude Code itself is free to install. You pay for API usage — or use it through a Pro or Max subscription. The workshop repo is small enough that today's exercises cost pennies. Boris's daily usage at Anthropic is obviously enterprise-scale."

---

*Last updated: 2026-03-24*
