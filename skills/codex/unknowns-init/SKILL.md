---
name: unknowns-init
description: Install the "Know your unknowns" workflow as mandatory rules in the current project's AGENTS.md, so pre-work discovery, mid-work decision logging, and pre-finalization self-checks apply automatically every session — not just when the unknowns skill is manually invoked. Use when the user wants this methodology enforced by default in a specific project, not just available as an occasional tool.
---

# Unknowns Workflow Bootstrapper

A plain skill only runs when Codex decides to invoke it or the user explicitly asks — that's fine for occasional tools, but not for a habit that's supposed to apply by default (e.g. "always keep a decision log during multi-step work"). This skill closes that gap by writing the habit into the project's `AGENTS.md`, which Codex loads as project instructions every session, the same way this user's other project-independent MUST rules work.

This is a **project-scoped** action: run it once per project where the workflow should be mandatory. It does not touch global (`~/.codex`) config.

## Language

Communicate with the user in **Russian** throughout this skill — status updates, what was written to `AGENTS.md`, confirmations, and the final report in step 5. Keep established technical terms in English where that's how the user already uses them (skill names like `unknowns`/`unknowns-init`, file paths, the marker `<!-- unknowns-workflow:v1 -->`, technique names). The installed `AGENTS.md` section itself (the block under "Section to install" below) stays in English, since it is an instruction Codex reads, not user-facing prose.

## Steps

1. Determine the project root: `git rev-parse --show-toplevel` if inside a git repo, otherwise the current working directory.
2. Check for `<root>/AGENTS.md`.
   - **Doesn't exist**: create it containing only the section below.
   - **Exists, contains the marker `<!-- unknowns-workflow:v1 -->`**: already installed — tell the user and stop. Don't duplicate.
   - **Exists, no marker**: append the section below at the end of the file (preserve everything already there).
3. Show the user what was written (the added section, or the new file's content) before finishing.
4. Confirm the `unknowns` skill is installed (`~/.codex/skills/unknowns/SKILL.md`); if it's missing, say so — these two skills are meant to be used together.
5. Report the file path and remind the user this only applies to this project — run `unknowns-init` again in any other project where they want the same enforcement.

## Section to install

```markdown
<!-- unknowns-workflow:v1 -->
## Know Your Unknowns Workflow (MANDATORY)

This project uses the `$unknowns` skill to catch unknown-unknowns while they're still cheap to fix. These steps are MANDATORY — apply them by default without being asked, the same as this project's other MUST rules (testing, security, etc.).

### Before starting unfamiliar or ambiguous work
Before starting any non-trivial task that touches unfamiliar territory or has ambiguous scope:
- Territory unfamiliar (module, domain, client, market, process you haven't worked in) → use `$unknowns` with the `blindspot` technique first.
- Territory familiar but scope/requirements are ambiguous → use `$unknowns` with the `interview` technique first.
- The right shape of the solution is genuinely undetermined → use `$unknowns` with the `directions` or `mock` technique before building the real thing.
- About to adapt or port an existing pattern or precedent → use `$unknowns` with the `reference-check` technique before reproducing it.

Skip only for trivial, fully-understood, single-step changes — and say briefly why you're skipping.

### During multi-step work
For any task spanning multiple steps, files, or sessions: maintain a running log via `$unknowns` with the `decision-notes` technique. Every deviation from the plan gets logged with the conservative choice made and the reasoning. Do not silently improvise without recording it.

### Before finalizing, delivering, or merging
Before declaring non-trivial work done, sending a deliverable, or merging code: use `$unknowns` with the `quiz` technique to self-verify genuine understanding of what was produced. If the result needs sign-off from someone else, also produce the `pitch` technique.
```

## Notes

- This is additive and idempotent — safe to re-run; it will no-op if the marker is already present.
- If the user wants the wording softened to a recommendation instead of a MUST rule, edit the installed section directly (change "MANDATORY" language and the skip condition) rather than re-running this skill.
