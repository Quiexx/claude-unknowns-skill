# claude-unknowns-skill

Two Claude Code skills implementing a "Know your unknowns" workflow — surfacing and reducing unknown-unknowns at each phase of any substantial task (code, documents, business analysis, client work, process design, market research, decisions), not just software engineering.

Adapted and generalized from the "Know your unknowns" methodology (Thariq / Anthropic, Apache-2.0, [github.com/ThariqS/html-effectiveness](https://github.com/ThariqS/html-effectiveness)) — the original is code/engineering-focused; this version rewrites every technique in domain-neutral language and adds a fixed visual design system so output is consistent across sessions.

## Skills

- **`skills/unknowns`** — the workhorse. Eleven techniques (blindspot pass, teach-me, design directions, mock, brainstorm, interview, reference-check, tweakable plan, decision notes, pitch/buy-in doc, completion quiz) split across pre-work, during-work, and post-work. Invoke with a technique name or with nothing and it infers the right one from context. Produces self-contained local `.html` artifacts (no build step, no external dependencies) using the fixed design system in `skills/unknowns/design-system.md`.
- **`skills/unknowns-init`** — a bootstrapper. Run once per project to install a MUST-level "Know your unknowns" workflow section into that project's `CLAUDE.md`, so the pre-work discovery / during-work decision log / pre-finalization quiz steps apply by default instead of relying on the `unknowns` skill being manually invoked every time.

## Install

Copy (or symlink) each skill directory into `~/.claude/skills/`:

```bash
cp -r skills/unknowns skills/unknowns-init ~/.claude/skills/
```

Both skills then become available globally in Claude Code, in any project.

## License

Sample/personal-use code, not maintained as a general-purpose product. See the upstream methodology's license (Apache-2.0) for the ideas this builds on.
