# Less UI

**Less is more professional.** A one-pass, tokens-first design skill for coding agents
(Claude Code, Cursor, Codex and anything that reads `SKILL.md`). It makes AI-built prototypes
read as designed rather than generated, and it got *shorter* every time it got better.

1,468 words. No reference files. No Python. Nothing to configure.

## Why another design skill

Most design skills tell the agent what good looks like and then ask it to check its own work.
That produces either a template with a nicer palette, or a rewrite loop where the agent audits,
fails, rewrites, audits again. Less UI was built by running the same brief through five versions of
the skill and measuring wall clock, tokens and a fixed rubric each time. Two things fell out:

- **Constraints declared before building cost 1.5x. The same constraints audited afterwards cost
  4.8x.** So the skill makes the agent write its palette, four type sizes, three radii, three
  spacing steps and two shadows as a `:root` token block before any CSS, and bans literal values
  outside it. The tiers hold by construction; nothing is counted at the end.
- **Only distilled content earns a place.** Every element on screen must answer "what decision
  does this serve?". Robustness lives in the code; the screen shows the story.

## What the agent does with it

1. Writes a six-line plan (subject, density, color as hexes, type, layout, one principle) and
   attacks it once: any line that would survive for a different brief is a default, not a choice.
2. Refuses the 2026 tells, checked as hex ranges, not vibes: cream + terracotta, purple gradients,
   the card kit, six equal metric cells, ALL-CAPS eyebrows, arrows on buttons, emoji icons.
3. Builds hierarchy by contrast: the focal element is at least 3x its supporting text, four sizes
   per screen, one metric dominates.
4. Ships every state (structural skeleton, empty with one action, error with cause and recovery),
   makes every control actually change the view, keeps deltas where a domain reader would accept
   them, and annotates every spike on a chart.
5. For flows: one question per screen, constraints as copy at the point of anxiety, the primary
   action disabled until valid.
6. Self-checks once, fixes once, ships. Hands back the file, the direction, what it cut and why.

## Install

```bash
npx skills add Jerry6063/less-ui
```

Or copy `skills/less-ui/` into `.claude/skills/` (Claude Code), `.cursor/skills/` or
`.agents/skills/`. If skills are not available in your environment, paste `templates/CLAUDE.md`
into the project root instead; it is the same text without frontmatter.

## Use

```
/less-ui  <paste your brief>
```

Works best when the brief names the user, their one job, and the must-have regions. Two briefs of
that shape are in `benchmark/briefs/`.

## Receipts

Every rule in the skill was added because a measured run failed without it. All runs: Claude Opus,
identical brief, one pass, no user in the loop, browser tools barred from the builder, outputs
verified afterwards in a real browser.

| Version | Words | What changed | Time | Tokens | Score /14 |
|---|---|---|---|---|---|
| v1 | 1,219 | first distillation | 300 s | 91 k | 13 |
| v2 | 1,558 | hex blocklist, skeleton required, honest controls, defensible deltas | 334 s | 97 k | 14 |
| v3 | 1,797 | hierarchy 3x, three tiers each, enforced by **counting** | 1,608 s | 212 k | 12 |
| v4 | 1,911 | same rules, enforced by **tokens first**, one-pass check | 516 s | 112 k | 14 |
| v5 | 1,468 | economy + flow rules, whole skill compressed | 538 s* | 109 k | verified |

\* v5 was measured on the second brief (a five-screen mobile flow), not the dashboard.

On the first brief, the same run with other skills: Anthropic `frontend-design` 13/14 in 212 s,
`impeccable` 11/14 in 600 s, `huashu-design` 8/14 in 445 s. Full evidence, including what each
deduction was for, in `benchmark/SCORECARD.md`.

## Demos

Both are single self-contained HTML files produced by the skill in one pass. Open them locally, or
preview without cloning:

- Operations dashboard: [preview](https://htmlpreview.github.io/?https://github.com/Jerry6063/less-ui/blob/main/demos/ops-dashboard/index.html) · [source](demos/ops-dashboard/index.html)
- Device companion mini program: [preview](https://htmlpreview.github.io/?https://github.com/Jerry6063/less-ui/blob/main/demos/device-companion/index.html) · [source](demos/device-companion/index.html)

Data in the demos is fictional. Each folder has the builder's `notes.md` with the plan and the
token block it committed to.

## Layout

```
skills/less-ui/SKILL.md      the skill
templates/CLAUDE.md          same rules as a CLAUDE.md drop-in
benchmark/briefs/            two assessment-style briefs and the rubric
benchmark/SCORECARD.md       every run, every deduction, every lesson
benchmark/history/           v1 to v4 of the skill, for the diff
demos/                       one-pass outputs
```

## Credits

Less UI distills, in its own words, ideas from Anthropic's `frontend-design` skill (the
plan-then-attack process and the list of tells), `ibelick/ui-skills` (MUST/NEVER floor),
`pbakaus/impeccable` (craft floor, states, hardening), `alchaincyf/huashu-design` (single-file
prototype mechanics, phone frame), `Nutlope/hallmark` (the idea of a brief-based test harness) and
Vercel's Web Interface Guidelines. None of their text is reproduced.

## License

MIT
