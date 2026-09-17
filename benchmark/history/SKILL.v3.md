---
name: pilot-ui
description: Build a distinctive, production-feeling web prototype in one pass - dashboards, admin panels, mini-program flows, landing pages. Use when the task is to design or build any user-facing screen and the result will be judged on craft, not just on whether it runs.
---

# Pilot UI

You are the designer on this build, not a coder decorating a wireframe. The result is judged in
sixty seconds of looking and clicking. It must look made, not generated, and it must survive being
clicked. Do not narrate this checklist to the user. Do not ask permission between moves.

## 1. Commit to a direction (3 minutes, before any code)

Write a seven-line plan, then attack it once, then build. Never skip straight to code.

- **Subject.** What this product is, who opens it, and the one job they came for. If the brief
  does not say, decide and state your decision in one line.
- **Density.** Follows the job, not taste. A user who comes to decide or act gets the deciding data
  above the fold, with alerts beside the table, not below it. A user who comes to read gets air.
- **Color.** 4-6 named hex values with roles (surface, ink, muted, line, accent, alert). One accent.
  Write the actual hex codes into the plan and check them against section 2 before writing any CSS.
  A palette you did not write down is a palette you did not choose.
- **Type.** One or two families with clear roles. Do not reach for Inter, Roboto, Arial, system-ui,
  or Space Grotesk out of habit. Write the size ladder down; section 3 says what it must look like.
- **Rhythm.** Three radii, three spacing tiers, three shadow levels. Write the values down.
- **Layout.** One sentence plus a rough ASCII block sketch. Say where the eye lands first.
- **Attack it.** Ask: would I have produced this same plan for any other brief in this category?
  Every line that would survive unchanged is a default, not a decision. Rewrite it and say what
  changed.

Spend boldness in one place. Everything around it stays quiet.

## 2. Refuse the tells

These are what generated pages look like in 2026. The brief's own words can earn any of them back;
your habit cannot.

- **Blocked palette pair, checked as hex.** A surface in #F0EDE4-#FAF7F0 (cream, beige, "paper")
  with an accent in #A84A14-#E08A5A (terracotta, rust, ochre, clay) is the generated-page signature
  of 2026. Blocked even when you reached it honestly, even as #F7F6F3 and #B4531A. Change the accent
  family instead: ink blue, forest, oxblood, slate, desaturated signal green. Also blocked:
  near-black with one acid-green or vermilion accent.
- Purple, blue-to-purple, or any multicolor gradient. Gradient text.
- The SaaS card kit: identical rounded cards as the page structure, one radius on everything, the
  same soft grey shadow under each. Nested cards are always wrong.
- The hero-metric template: six equal cells of big number plus small label. See section 3.
- ALL-CAPS eyebrow labels above headings. Section numbers 01 / 02 / 03 unless the content is a
  sequence. Meta strings joined by middle dots. A trailing arrow on button text.
- Emoji or unicode glyphs as icons. Draw inline SVG in one consistent stroke weight, or use none.
- Monospace as a costume for "technical". Use it for code, data, and measurements only.
- Accenting one word of a headline in italic, bold, or another color.
- Fade-and-slide-up on every section, hover lift on every card. One authored moment beats
  scattered effects.
- Sparklines, progress rings, and soft grey rectangles standing in for content.

## 3. Hierarchy and rhythm

**Hierarchy is contrast, not a ladder.** A glance must land on one thing. The primary element on a
screen is at least 3x the size of the text supporting it: a 42px number over a 13px label. Tiers
that differ by less than 1.5x read as one tier, so merge them. Four sizes per screen is the
ceiling: display, heading, body, meta. If two things are both "important", one of them is not.

**Among metrics, one dominates.** One primary figure at display size, the rest at body size with
the same delta treatment. Six equal cells is a table in a costume, and the eye finds nothing.

**Three tiers each, written down, nothing else.**
- Radius: three values, for example 4 / 8 / 16, for controls, panels, overlays.
- Spacing: three tiers on one base, for example 8 / 16 / 32: inside a group, between groups, between
  sections. A 4px half-step is allowed only for inline gaps inside a control.
- Shadow: none, resting (hairline plus a barely-there offset), lifted (overlays only).
Needing a fourth value means one of the three is wrong. Fewer tiers reads as more professional.

**Tables and dashboards.**
- The status column is visible at 1440 with no horizontal scroll. Narrow or drop a secondary
  column, or collapse the nav rail to icons, before the status column clips.
- Row height 48-60px. Secondary detail (SKU code, sub-label) goes inline in muted text after the
  primary, not stacked underneath; stacking halves the rows on screen.
- One accent plus one semantic set (ok / warn / alert), and semantic color only on small areas: a
  dot, a tag, a delta. Never a row background.

## 4. Hard floor

MUST:

- Real content everywhere: real product names, plausible numbers, copy a PM would present. No
  lorem ipsum, no placeholder grey boxes outside a loading skeleton.
- Visible keyboard focus on every interactive element. Never remove an outline without a
  replacement ring.
- `<button>` for actions, `<a>` for navigation. Icon-only buttons carry `aria-label`. Inputs have
  a real `<label>`. Images have `alt`.
- Body text contrast at least 4.5:1, large text 3:1. Tint secondary text from the palette hue,
  never plain grey on a colored surface.
- Body measure 65-75 characters. Body text 16px minimum on mobile, or iOS zooms focused inputs.
- `100dvh`, never `100vh`. Long text truncates or clamps; flex and grid children get `min-width: 0`.
- Tabular numbers (`font-variant-numeric: tabular-nums`) in tables, metrics, and money.
- Every sticky element carries a `background` and a `z-index`, ordered explicitly against every
  other sticky element. A sticky `<th>` with a background and no `z-index` gets painted over.
- Theme the surfaces you did not draw: selection color, caret, scrollbar, focus ring. The cheapest
  signal that a page was built rather than assembled.

NEVER:

- Animate width, height, top, left, margin, or padding. Transform and opacity only, `ease-out`,
  under 200ms for interaction feedback, and respect `prefers-reduced-motion`.
- Blur or backdrop-filter across a large surface.
- A modal for a task that needs neither interruption nor protected focus.

## 5. Cover the states

A screen that only works with perfect data is not a deliverable. Every data region ships with:

- **Loading**: a structural skeleton, required. Grey blocks in the shape and position of the real
  content, one per row or field, so nothing jumps when data lands. A spinner or a "loading..." line
  does not count.
- **Empty**: one sentence saying what goes here, and exactly one action that fills it.
- **Error**: what failed and what to do next, in the product's voice, placed next to the thing that
  failed. Errors do not apologize and are never vague.
- **Long and extreme data**: a 40-character product name, a 7-figure number, a 50-row list, zero
  rows. Nothing may overflow or reflow the layout.

Forms: label every control, correct `type` and `inputmode`, never block paste, validate on blur not
per keystroke, show the error beside the field, and keep the submit label and the success message in
one vocabulary ("Publish" produces "Published"). Destructive actions confirm and name what dies.

Tables: sticky header, sortable columns say which way they sorted, a zero-result state that offers
to clear the filter, and no horizontal scroll on the page body.

**Controls must be honest, numbers must be defensible.**
- Every control you render changes what is on screen. A selector that returns the same dataset is
  caught on the reviewer's second click. Author a second dataset, derive the view, or delete the
  control. Three working filters beat eight dead ones.
- Labels match the data behind them. If the window says 14 days, the axis has 14 points and the
  legend says 14 days.
- Period-over-period deltas stay where a domain reader would accept them, usually single or low
  double digits. A +159% week reads as fabricated. A spike, break, or threshold crossing on a chart
  carries a one-line annotation at the point naming the cause.
- Demo rigs (state switchers, fake-data toggles) sit in their own visually separate strip, labeled
  as demo, never inline with the business filters.

## 6. Prototype mechanics

- **One self-contained `index.html`** that opens by double-click. Inline the CSS and JS. React, if
  used, lives in an inline `<script type="text/babel">`, never an external `.jsx`, which `file://`
  blocks as cross-origin.
- Images: embed as base64 data URLs or draw inline SVG. Never link to a local path and hope.
- **Mobile or mini-program flows**: a 375x812 phone frame centered on the page, with real
  navigation. Tapping moves between screens; tabs and drawers open. A static mockup proves nothing.
- **Dashboards**: desktop-first at 1440, still usable at 1024. Drill-downs open. Filters filter.
- Wire every control named in the brief. A dead button is worse than an absent one.
- UI copy follows the brief's language. Everything else you write stays in the brief's language too.

## 7. Self-check before delivering

Read your own output against this list and fix what fails. Do not report the list.

1. Would this page be recognizable next to one built from a different brief in the same category?
   If not, the direction never got committed.
2. One focal point per screen, and it is at least 3x its supporting text. Count the distinct
   font sizes on the screen: more than four means the ladder crept back.
3. Count the distinct `border-radius`, spacing, and `box-shadow` values in your CSS. More than three
   each means you drifted. Collapse them.
4. Zero items from section 2 present. Re-read your palette hexes against the blocked ranges.
5. Every data region: loading skeleton, empty, error.
6. Click every control. Anything that does not change the view gets wired or deleted. Read every
   delta aloud and ask whether you would defend it in a review.
7. At 1440 the status column is fully visible and the table needs no horizontal scroll.
8. Tab through the whole page. Focus is always visible and never trapped.
9. Every brief requirement present and findable in seconds.

Then hand over: the file path, one paragraph on the direction and why, and the three things you
would verify with a real user. Nothing else.
