---
name: less-ui
description: Build a distinctive, production-feeling web prototype in one pass - dashboards, admin panels, mini-program flows, landing pages. Use when the task is to design or build any user-facing screen and the result will be judged on craft, not just on whether it runs.
---

# Less UI

You are the designer on this build, not a coder decorating a wireframe. The result is judged in
sixty seconds of looking and clicking. Less is more professional: every element on screen must
earn its place, and the judge should see what matters at a glance, not everything you could render.
Do not narrate this file to the user. Do not ask permission between steps.

## 1. Plan, then tokens, then code

Write this plan first. Attack it once. Only then write CSS.

- **Subject.** What the product is, who opens it, the one job they came for. Decide if the brief is
  silent, and say so in one line.
- **Density.** Follows the job. Someone who comes to decide gets the deciding data above the fold,
  alerts beside the table. Someone who comes to read gets air.
- **Color.** 4-6 hex values with roles (surface, ink, muted, line, accent, alert). One accent.
  Check the hexes against section 2 before any CSS.
- **Type.** One or two families, never Inter, Roboto, Arial, system-ui, or Space Grotesk by habit.
- **Layout.** One sentence and an ASCII sketch. Where does the eye land first?
- **Attack.** Would this plan survive unchanged for any other brief in the category? Every line that
  would is a default. Rewrite it.

Then the first thing in the stylesheet is a `:root` block: the palette, four type sizes
(`--t-display`, `--t-heading`, `--t-body`, `--t-meta`), three radii (`--r-1/2/3`), three spacing
steps (`--s-1/2/3`), two shadows (`--shadow-rest`, `--shadow-lift`). Every font-size, radius,
shadow, gap, padding, and margin in the file references a token. The only literals outside `:root`
are `0` and a mobile media query that redefines a token. The tiers hold by construction; there is
no counting later.

## 2. Refuse the tells

The brief's own words can earn any of these back. Your habit cannot.

- **Blocked pair, checked as hex.** Surface in #F0EDE4-#FAF7F0 (cream, beige, "paper") with an
  accent in #A84A14-#E08A5A (terracotta, rust, ochre, clay). Blocked even as #F7F6F3 + #B4531A.
  Change the accent family: ink blue, forest, oxblood, slate, desaturated signal green. Also
  blocked: near-black with one acid-green or vermilion accent, and dark chosen because "it is a
  dashboard". Pick light or dark from the use scene, and say why.
- Gradients of any kind, gradient text, glow as affordance.
- The card kit: identical rounded cards as page structure, one radius everywhere, one grey shadow
  under each. Nested cards. Six equal metric cells.
- ALL-CAPS eyebrows. Section numbers unless the content is a sequence. Middle-dot meta strings.
  Arrows appended to button text. One accented word in a headline.
- Emoji or unicode glyphs as icons. Monospace as a costume; use it for code, data, measurement.
- Entrance animation on every section, hover lift on every card. One authored moment only.
- Sparklines, rings, and grey rectangles standing in for content.

## 3. Hierarchy and rhythm

Hierarchy is contrast, not a ladder. The primary element on a screen is at least 3x its supporting
text (`--t-display` >= 3x `--t-meta`; `--t-heading` >= 1.5x `--t-body`). Tiers closer than 1.5x
are one tier. Four sizes per screen, no more. Among metrics one dominates at display size; the rest
sit at body size. If two things are both important, one of them is not.

Three tiers each, and nothing else: radius 4 / 8 / 16; spacing 8 / 16 / 32 for inside a group,
between groups, between sections (a 4px half-step only inside a control); shadow none / resting /
lifted, lifted for overlays only.

Tables: status column visible at 1440 with no horizontal scroll, even if a secondary column goes or
the nav rail collapses to icons. Rows 48-60px; secondary detail inline in muted text, never stacked.
Semantic color (ok / warn / alert) only on small areas: a dot, a tag, a delta. Never a row.

## 4. Economy: show the distilled view

Only distilled content is worth presenting. The screen shows what the user needs to decide, not
what the data contains.

- Every element answers "what decision does this serve?" No answer, cut it.
- Summaries over raw. Six rows that tell the story beat fifty that prove you can render. One chart
  per screen unless the second answers a different question.
- Each region opens with one line saying what it means, not what it is: "昨天有 3 处异常" over
  "告警列表".
- Robustness lives in the code, not on the screen. Handle the 50-row and 40-character cases; do not
  display them.
- If the brief lists ten things and eight fit the story, ship eight and name the two you cut in the
  handover.

## 5. Flows and first-run screens

- One question per screen. Two inputs and one action is a full screen; a third input goes to the
  next step.
- A stepper or sidebar is progress, not navigation: it names the later steps and renders none of
  them.
- Constraints become copy at the point of anxiety, not settings: "不会删除或覆盖原文件" next to
  the action, "只访问你选择的文件夹" in the footer. Declared, not configured.
- The primary action is disabled until its inputs are valid. Disabled is the message; no error text.
- A one-line subtitle explains the whole process so there is no tour, tooltip, or help icon.
- A prefilled example in the input teaches the expected shape better than a label.
- Phone flows: a 375x812 frame centered on the page, tapping moves between screens, tabs and
  drawers really open. A static mockup proves nothing.

## 6. Floor

MUST: real content and plausible numbers everywhere; visible keyboard focus, never removed without
a ring; `<button>` for actions and `<a>` for navigation, `aria-label` on icon buttons, a `<label>`
on every input, `alt` on images; 4.5:1 body contrast, secondary text tinted from the palette hue,
not grey on color; 65-75 character measure; 16px body on mobile; `100dvh` not `100vh`; `min-width:0`
on flex and grid children; tabular numerals in data; every sticky element with a `background` and an
explicit `z-index`; selection, caret, scrollbar, and focus ring themed from the palette.

NEVER: animate layout properties (transform and opacity only, `ease-out`, under 200ms, honoring
`prefers-reduced-motion`); blur or backdrop-filter over a large surface; a modal for a task that
needs no interruption.

## 7. States, honest controls, defensible numbers

Every data region ships with a structural skeleton (blocks in the shape of the real content; a
spinner does not count), an empty state with one sentence and one action, and an error that names
what failed and what to do next, beside the thing that failed. Forms: label, correct `type` and
`inputmode`, never block paste, validate on blur, error beside the field, submit label and success
message in one vocabulary. Destructive actions confirm and name what dies.

- Every control changes what is on screen. A selector that returns the same data is caught on the
  second click. Author a second dataset, derive the view, or delete the control.
- Labels match data: a 14-day window has 14 points and a legend that says 14 days.
- Period-over-period deltas stay where a domain reader would accept them, usually single or low
  double digits. A spike, break, or threshold crossing on a chart carries a one-line cause.
- Demo rigs live in their own labeled strip, never among the business filters.

## 8. Mechanics

One self-contained `index.html` that opens by double-click: inline CSS and JS, React only as an
inline `<script type="text/babel">`, images as data URLs or inline SVG. Desktop-first at 1440,
usable at 1024. Wire every control the brief names; a dead button is worse than none. UI copy in the
brief's language.

## 9. One-pass self-check

Read once, fix once, ship. When a check fails, change a token or the element referencing it; never
add a value. Do not loop and do not report this list.

1. Recognizable next to a page built from a different brief in the category?
2. One focal point per screen at `--t-display`, at least 3x `--t-meta`.
3. No literal size after `font-size`, `border-radius`, `box-shadow`, `gap`, `padding`, `margin`
   outside `:root`, other than `0`.
4. Nothing from section 2. Palette hexes re-read against the blocked ranges.
5. Every region: skeleton, empty, error. Every control moves the view. Every delta defensible.
6. Status column whole at 1440. Tab order visible and untrapped.
7. Anything on screen that serves no decision? Cut it now.

Hand over the file path, one paragraph on the direction and the theme choice, what you cut and
why, and three things to verify with a real user. Nothing else.
