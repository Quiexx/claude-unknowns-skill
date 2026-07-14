---
name: unknowns
description: Surface and reduce unknown-unknowns at each phase of any substantial task — code, documents, business analysis, client work, process design, market research, decisions. Produces self-contained local HTML artifacts (cards, comparison grids, mocks, interviews, quizzes) instead of markdown prose, because reacting by clicking is cheaper than writing paragraphs. Use when starting unfamiliar work, when scope is ambiguous, before committing to an approach, mid-way through multi-step work, or before finalizing/delivering something. Invoke as `/unknowns <technique>` or let it infer the right technique from context.
---

# Know Your Unknowns

A working plan/prompt/brief is a map. The actual problem is the territory. The two never match exactly — the gap between them is your unknowns, and it splits into four kinds:

| | Known to you | Unknown to you |
|---|---|---|
| **Explicit / stated** | Known knowns — already in the brief | Known unknowns — gaps you're aware of |
| **Implicit / exists but unstated** | Unknown knowns — real context nobody said out loud (prod reality, an existing convention, a precedent) | Unknown unknowns — risks you don't even know to ask about |

The quadrant that costs the most is the last one, and it is cheapest to find **before** work starts, gets more expensive to find **during** work, and is most expensive to discover **after** something has already shipped, been sent, or been merged. This skill provides eleven techniques split across those three windows.

This skill applies to any domain: a codebase, a client relationship, a market you're entering, a business process you're redesigning, a report you're writing, a decision you're about to make. Do not assume "code" — read the actual task and generalize the technique to it.

## Language

Write all HTML output in **Russian** — headings, body text, prompts, questions, explanations, everything the user reads. Keep established technical terms in English where that's how the user already uses them (skill names like `unknowns`/`unknowns-init`, file paths, code identifiers, framework/library names, and the technique names themselves e.g. "blindspot pass", "tweakable plan" — write these in English inline, but explain them in Russian around them). Don't force-translate proper names or code. When in doubt, prefer Russian prose with English technical nouns embedded, the way a Russian-speaking engineer would actually write.

## Output format

Every technique below produces one self-contained `.html` file — inline CSS/JS, no build step, no external dependencies, opens directly in a browser. Favor interactive elements (checkboxes, toggles, collapsible sections, a "copy this follow-up prompt" button) over prose: the point is that the user reacts by clicking, not by writing paragraphs back.

**Always build the page using `design-system.md`** (in this skill's directory) — it defines the fixed palette, typography, and component patterns (cards, chips, prompt blocks, quiz questions, timelines) that every artifact from this skill should reuse, so output looks like one consistent product across techniques and across sessions rather than a different improvised style each time. Read that file before writing any HTML. Use `artifact-design` skill only for general accessibility/responsiveness fundamentals not already covered there — it does not override the fixed palette/type.

Save the file to `.claude/unknowns/<technique>-<topic-slug>-<YYYYMMDD-HHmm>.html` in the current project (create the directory if it doesn't exist). These are working documents for the person who requested them — never publish them externally (no `Artifact` tool, no sharing) unless explicitly asked.

**Always report the result as a clickable `file://` link**, not just a bare path — convert the saved path to an absolute path and print it as `file:///absolute/path/to/file.html` on its own line, so the user can open it straight from the terminal without retyping it.

## Choosing a technique

If invoked without an argument, infer from context:

- Territory is unfamiliar (a module, a client, a market, a department you haven't worked in) → **blindspot**
- You don't know the domain's vocabulary well enough to even ask good questions → **teach-me**
- The right shape of the solution is genuinely open and words won't settle it faster than seeing options → **directions**
- One direction seems right but its concrete shape needs to be seen before real work starts → **mock**
- The problem is real but no intervention is chosen yet, and there's real material worth grounding a brainstorm in → **brainstorm**
- Scope is ambiguous but bounded, and specific questions would resolve it → **interview**
- About to adapt, port, or reuse an existing pattern or precedent → **reference-check**
- About to write a plan for the work → **tweakable-plan**
- Mid-way through multi-step work → **decision-notes**
- About to present results for approval or buy-in → **pitch**
- About to finalize, send, submit, or merge → **quiz**

## Pre-work techniques (cheapest place to find unknowns)

### 1. Blindspot pass
**When**: stepping into unfamiliar material — an unfamiliar module, a client's business you haven't worked with before, a regulatory area, a market you haven't researched, another team's process.
**Do**: actually read/explore the relevant material first (code, docs, prior correspondence, whatever exists). Then produce a card per blindspot: what the gap is, why it matters concretely (not abstractly), and a copy-pasteable follow-up instruction that closes it. End with all fixes merged into one composite brief the user can hand back to you.
**Prompt pattern to recognize**: "I'm about to work on X but I've never worked in/with Y before — find what I don't know I don't know here."

### 2. Teach-me (concept ladder)
**When**: the user needs enough vocabulary and mental model to ask good questions or evaluate options — not to become an expert.
**Do**: build a short vocabulary ladder (5–8 terms, each building on the last), plus one concrete before/after or worked example the user can manipulate (sliders/toggles/inputs where a parameter is genuinely tunable) to build intuition. End with 2–3 example prompts the user can now write using real vocabulary.

### 3. Design directions
**When**: multiple genuinely different approaches exist and describing them in prose is slower than reacting to them rendered out.
**Do**: render 3–4 divergent options side by side — layouts, outlines, structures, strategies, whatever fits the domain — each with a one-line rationale. Give a lightweight react mechanism per option (keep / drop / take-this-element-from-here) that assembles into a reply the user can submit as-is.

### 4. Mock before you commit
**When**: one direction is likely right but its concrete shape (layout, structure, flow, wording) needs to be seen or clicked through before real work starts on it.
**Do**: build a single disposable artifact with placeholder/fake data, behaving enough like the real thing to react to. Label it explicitly as throwaway — it is not meant to become the real deliverable.

### 5. Brainstorm the intervention
**When**: the problem is real but no intervention is chosen, and there's existing material (code, past reports, data, prior analyses) worth grounding the brainstorm in rather than brainstorming in the abstract.
**Do**: search/read the relevant material, then generate ~10 options plotted on a cheap-and-fast → ambitious-and-slow axis, each grounded in a specific fact from the material (not a generic idea). Give a resonance checkbox per option.
**Prompt pattern to recognize**: "Here's my rough problem: P. Look at [material] and brainstorm ways to address it, from cheapest to most ambitious."

### 6. The interview
**When**: scope is ambiguous in specific, answerable ways.
**Do**: ask ONE question at a time — never dump a list — ordered by how much the answer would change the shape of the work (highest-leverage first). Let each answer inform the next question. End with a decisions table summarizing every answer and a ready-to-use follow-up brief that incorporates them.
**Prompt pattern to recognize**: "Interview me one question at a time about what's still ambiguous in X. Prioritize questions where my answer would change the [architecture / structure / approach]."

### 7. Point at a reference
**When**: about to adapt, port, or reuse an existing pattern or precedent — code in another language, a competitor's playbook, a past client deliverable, an existing SOP — where a literal misread would be expensive.
**Do**: build a semantics map first — matched excerpts or side-by-side comparisons between source and target, explicit gotchas and edge cases — and get confirmation that the source was understood correctly before producing the adapted version. Never skip straight to reproducing the pattern.

### 8. The tweakable plan
**When**: writing any plan — an implementation plan, a project plan, a report outline, a campaign plan.
**Do**: sort the plan by likelihood-of-being-revised, not by execution order. Lead with the decisions the user is most likely to want to change (the domain's high-leverage variables: data model / structure / user-facing choices / positioning). Push the mechanical, low-judgment parts to the bottom, collapsed, since those are trusted to just get done.
**Prompt pattern to recognize**: "Write a plan for X, but lead with what I'm most likely to want to tweak, and bury the mechanical part — I trust you on that."

## During-work technique

### 9. Decision notes
**When**: any task spanning multiple steps, files, or sessions.
**Do**: maintain a running log for the duration of the work. Every time reality forces a deviation from the plan (an edge case, missing data, a conflicting constraint), pick the conservative/safe option, log it under "Deviations" with the reasoning, and keep going without stopping to ask — unless the deviation is high-stakes or irreversible, in which case stop and ask. End with a short "what this changes for next time" summary.
**Prompt pattern to recognize**: "Keep a running notes file as you build X. If you hit something that forces a deviation, pick the conservative option, log it, and keep going."

## Post-work techniques

### 10. The buy-in / pitch doc
**When**: the result needs approval or buy-in from someone who wasn't in the room for the work.
**Do**: lead with the outcome or a demo of the result, not with the process that produced it. Pre-empt the 3–5 objections a skeptical reviewer would actually raise, each answered with evidence. Name exactly who needs to sign off on what.
**If the pitch introduces a multi-part process, framework, or set of options** (e.g. explaining this very skill's techniques, a new workflow, a menu of choices someone needs to actually operate afterward): don't stop at a one-line label per part. Give each part its own breakdown using the `.breakdown` component in `design-system.md` — why it exists, what it produces, how to trigger/use it (the literal invocation), a concrete example, and when it applies. Also include a `.flow-phase`/`.flow-row` decision-flow diagram (design-system.md) that shows, as a scannable sequence of "if this, do that" rows, exactly when to reach for each part — a bullet list of names is not enough for something the reader has to operate later.
**Output shape**: default to a doc-style page (hero → objections → sign-off). If the user asks for a "slide deck", "presentation", "deck", or the pitch is meant to be presented live rather than read async, use the `Slide deck` component in `design-system.md` instead — one idea per slide, keyboard/dot navigation, title slide as the cover.

### 11. The completion quiz
**When**: about to finalize, send, submit, or merge non-trivial work — including your own, not just someone else's.
**Do**: produce a short report on what changed or was produced (context → reasoning → outcome), then a self-check quiz of 4–6 questions that must be answered correctly. Wrong answers should point back to the specific section that answers them, not just mark the answer wrong.
**Prompt pattern to recognize**: "Give me a report on [the change/output] — context, reasoning, what was done — with a quiz at the bottom I must pass before I [merge/send/finalize] it."

## Non-negotiables

- Ground every technique in real material wherever it exists — read the actual code, docs, data, or prior correspondence. Never invent context to fill a template.
- Never skip the reference-check before reproducing a pattern you haven't verified you understood.
- The interview and decision-notes techniques require genuine back-and-forth or genuine logging over time — not a single upfront guess dressed up as either.

This skill was adapted for general-purpose (not just coding) use from the "Know your unknowns" methodology (Thariq / Anthropic, Apache-2.0, github.com/ThariqS/html-effectiveness).
