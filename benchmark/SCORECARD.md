# Run 1 results - brief 01 "跨境电商运营面板"

All four ran under identical exam conditions on 2026-09-16: one pass, no user in the loop,
browser and screenshot tools barred from the builder, single self-contained `index.html`.
Verification (screenshots at 1440 and 1024, drawer clicks, DOM probes) was done afterwards
by the orchestrator, not by the builders.

## Cost

| Skill | Wall clock | Agent tokens | Tool calls | Output | Skill text in context |
|---|---|---|---|---|---|
| frontend-design | **212 s** | 79 k | 5 | 30.5 KB / 575 lines | 9 KB, no refs |
| less-ui (distilled) | 300 s | 91 k | 8 | 43.3 KB / 713 lines | 7 KB, no refs |
| huashu-design | 445 s | 136 k | 13 | 54.7 KB / 1045 lines | 65 KB + 679 KB refs available |
| impeccable | **600 s** | 150 k | 29 | 59.8 KB / 1105 lines | 12 KB + 411 KB refs available |

## Scores (0-2 each, 14 max)

| # | Criterion | frontend-design | impeccable | huashu-design | less-ui |
|---|---|:--:|:--:|:--:|:--:|
| 1 | Structural distinctness | 2 | 2 | 2 | 2 |
| 2 | Hierarchy, 60-second read | 2 | 2 | 1 | 2 |
| 3 | AI tells absent | 2 | 1 | 0 | 1 |
| 4 | States (loading/empty/error) | 1 | 2 | 2 | 2 |
| 5 | Interaction fidelity | 2 | 2 | 1 | 2 |
| 6 | Business realism | 2 | 2 | 1 | 2 |
| 7 | Time and token cost | 2 | 0 | 1 | 2 |
| | **Total** | **13** | **11** | **8** | **13** |

## Evidence behind the deductions

**frontend-design** - row 4. Only 3 skeleton-class elements; several regions swap to a text
"loading" line rather than a structural skeleton. Everything else clean: cool steel palette,
zero uppercase eyebrows, zero arrow-in-button, zero emoji glyphs, row click opens a drawer whose
SKU matches the row.

**impeccable** - row 3. The alert panel renders two large decorative grey illustrations that stand
in for content, which is the category its own craft-floor bans. Row 7. 600 s, of which the builder
attributes ~40% to skill scaffolding: `new-work.md` is 52 KB and must be read before any decision,
`concept-seed` refuses to run without a PRODUCT.md, then a six-block direction contract, then
DESIGN.md at finish, then 8 runs of its `detect` script (4 of them on one tracking complaint).
Best states of the four: a real skeleton-to-content transition on load, 19 skeleton elements.

**huashu-design** - row 3. Six `text-transform:uppercase` rules, two arrow-suffixed buttons, and
`Inter` as the first sans in the stack. Row 2. The table's sticky `thead` has a background but no
`z-index`, so the first body row paints over the column headers while scrolling; visible at both
1440 and 1024. Row 5 and 6. Five of seven drill buttons carry `data-sku="DEFAULT"`, so clicking
Amazon DE opens a drawer titled "AMAZON DE" whose body describes a Shopee PH speaker. Row 7. The
mandatory three-direction gate cost 4-5 of the 7.4 minutes and is unsatisfiable without a user.

**less-ui** - row 3. Its own banned combination: `--surface:#F7F6F3` with `--accent:#B4531A`, which
is the cream-plus-terracotta tell the skill's own section 2 names first. Everything else on that
list held: no uppercase, no arrows, no emoji, no gradient text. Strongest wiring of the four - all
seven SKU buttons carry distinct real the assessment part numbers and the drawer content matches.

## What to fix in less-ui before run 2

1. The refuse-list is read as prose, not as a check. Move the cream/terracotta pair into a literal
   hex blocklist and require the plan to state its palette hexes before building.
2. Add "structural skeleton" as a MUST under states; the word alone produced 11 elements here
   against impeccable's 19.
3. Add a sticky-header `z-index` rule; two of four builds got table layering wrong.

## Reproduce

```bash
cd /Users/jerryhao/Dailywork/anker-ai-pilot-prep/skills-eval
scripts/only.sh less-ui
```

---

# Run 2 - less-ui v2, same brief, same conditions

Skill grew from 1219 to 1558 words (7.4 KB to 9.4 KB) to carry five new rules. v1 preserved at
`.claude/skills/less-ui/SKILL.v1.md`.

| | v1 | v2 | frontend-design | impeccable | huashu |
|---|:--:|:--:|:--:|:--:|:--:|
| Wall clock | 300 s | 334 s | 212 s | 600 s | 445 s |
| Agent tokens | 91 k | 97 k | 79 k | 150 k | 136 k |
| **Score** | **13** | **14** | 13 | 11 | 8 |

## Did each fix land

| Fix | v1 | v2 |
|---|---|---|
| Hex blocklist for the cream+terracotta pair | violated: `#F7F6F3` + `#B4531A` | clean: surface `#EEF2F5`, accent `#14557A` ink blue |
| Structural skeleton required | 11 skeleton elements, partly text "loading" | 85 skeleton elements laid out as the real page |
| Sticky header needs `z-index` | absent | `thead th` `z-index:4`, topbar `z-index:30`, no overlap |
| Controls must drive data | 7/14/28-day selector returned one dataset | 14-day switch moves the axis from 9-09..9-15 to 9-02..9-15 and recomputes every metric; the SKU drawer follows the same window |
| Deltas must be defensible | +159.5% and +149.4% week over week | +1.2%, +1.1%, +4.9%, -3.5%, -7.1% |

Two behaviors appeared that were not asked for and are worth keeping: the zero-result state cascades
from the table into the chart with its own copy and a reset action, and the error state names a
cause and a recovery ("网关返回 503 ... 30 秒后可重试") instead of a generic failure line.

Cost of the fixes: +34 seconds and +6 k tokens against v1, still less than half of impeccable.

---

# Runs 3 and 4 - less-ui v3 and v4, same brief, same conditions

v3 added the author's two rules (hierarchy by contrast with a 3x primary/secondary ratio; three tiers each
of radius, spacing, shadow) plus density, status-column, row-height, demo-strip and chart-annotation
rules, and enforced them with COUNTING checks in the self-check. v4 kept every rule but moved the
enforcement to the front: the plan is written as a `:root` token block before any CSS, every size
references a token, and the self-check is one pass with a grep for literals instead of a count.

| | v2 | v3 (count-and-fix) | v4 (tokens-first) |
|---|:--:|:--:|:--:|
| Wall clock | 334 s | 1608 s | 516 s |
| Agent tokens | 97 k | 212 k | 112 k |
| Build / revise passes | 1 + fixes | 2 full builds + 3 revisions | 1 + 1 self-check, 1 fix |
| Distinct font sizes | 12 | 6 (4 + 2 mobile) | 4 tokens, 0 literals |
| Radius / shadow values | 3 / 1 | 3 / 2 | 3 / 2 |
| Literal px outside :root (size props) | 103 | 66 | 0 |
| Skeleton elements in loading state | 85 | 21 | 70 |
| Status column visible at 1440 | clipped | yes | yes |
| Rubric score | 14 | 12 (time row 0) | 14 |

## What v4 verified in the browser

- 14-day switch: chart axis goes from 7 to 14 points, legend reads "近 14 天 · 14 个数据点", the SKU
  drawer's trend follows the same window. The headline stays on 昨日营收, which is the correct
  semantics for a yesterday figure.
- Channel filter to Shopee: headline recomputes from $631,500 to $138,100, table drops from 9 rows to 6.
- Row click opens a drawer whose SKU matches the row (A1652, the assessment 737 Power Bank).
- Empty state cascades with its own copy and a "清除全部筛选" action. Loading state renders 70
  structural skeleton blocks. Demo controls sit in a labeled strip above the business filters.
- Chart spike on 09-12 carries an annotation naming the cause (site subsidy, ad budget +42%).
- One dominant figure at 48px over 12px meta (4x); four supporting KPIs in a strip at body size.

## Judgment calls to review, not defects

- v4 chose a dark theme. Nothing in the skill blocks dark with a blue accent, but "dark because it is
  a dashboard" is a category default. For a 9 a.m. office use scene, light is the more defensible
  answer. If the exam brief is silent, say the choice out loud in the handover paragraph.
- v4 deleted a date-range picker rather than ship it dead. The brief never asked for one, so this is
  the rule working, but in an exam the deletion should be mentioned in the handover.

## Lesson for the skill

Rules that are enforced by counting at the end cost a rewrite loop (v3: 4.8x the time of v2).
The same rules enforced by construction at the start (tokens first, literals banned) cost 1.5x and
held perfectly. Write constraints as things to declare before building, never as things to audit
after.

---

# Run 5 - less-ui v5 on brief 02 "设备伴侣小程序"

v5 = v4 rules + an Economy section (only distilled content is worth presenting; every element must
serve a decision; robustness in code, not on screen) + a Flows section drawn from the 办妥 app
(one question per screen, stepper is progress not navigation, constraints as copy at the point of
anxiety, CTA disabled until valid, subtitle explains the process, prefilled example teaches the
input). The whole skill was compressed from 1911 to 1468 words while adding those two sections.

| | v5 on brief 02 |
|---|---|
| Wall clock | 538 s |
| Agent tokens | 109 k |
| Build | 1 pass + 1 self-check, 4 fixes |
| Output | 44.6 KB single file + PRD.md (10 lines) |
| Type tokens / literals outside :root | 4 / 0 |
| Radii / uppercase / middle-dots / arrow buttons / emoji | 3 / 0 / 0 / 0 / 0 |

## Verified in the browser

- 375x812 phone frame centered; tab bar 设备 / 兼容 / 售后 on the three top-level screens.
- Onboarding: the 识别设备 button is disabled with an empty serial and enables when one is typed.
  Three taps land on the home screen. Constraint copy sits under the input: "只读取设备型号与出厂
  日期，不会开启定位或通讯录权限".
- Home: one 48px focal (68%), a one-line meaning headline ("3 件设备都还在保，Nano II 的两年期还剩
  41 天"), two secondary devices inline, one contextual tip with one action. Skeleton replay renders
  10 structural blocks.
- Zero-device empty state: one sentence, one action ("扫码添加设备"), reassurance in the copy
  ("1 分钟拿到电子保修，不用留发票").
- Device detail: headline states meaning ("三个口正在用掉 45W，还剩两小时出头"), per-port live
  status, firmware entry renders an error with cause and recovery, retry opens the update sheet
  with a changelog and "约 3 分钟，其间别拔线；不会清除充电记录和保修登记".
- Compatibility finder: picking MacBook Pro 14" M4 rewrites the focal to 96W and the verdict rows
  (两件满速 / 一件受限 65W), plus a cable line with a concrete reason (3A cable caps at 60W) and one
  mall link. No chart, no ring.
- Support: submit disabled until an issue and a device are chosen; response time rendered as copy
  ("工作日 2 小时内有人回你，当前排队 7 单"); existing ticket shown as a timeline; constraint under
  the button ("提交后不会自动换零件，客服确认方案后你再决定").
- Demo rig lives outside the phone in its own labeled strip.

## Economy rule in action

The builder cut a separate registration screen (same taps as onboarding), a spec-sheet page (folded
into the finder), a sixth tab for ticket status (it is the tail of support), and every chart or
ring (nothing on these screens is a trend), and named each cut in the handover. Screens carry one
focal each; the compatibility screen answers one question ("能不能快充") with three verdict rows.

## Judgment calls

- Dark again, this time with a stated reason (checking a power bank in bed or on a train; every
  focal element is a measurement). Defensible, but two dark builds in a row is worth watching.
- PRD.md is written in English while the UI is zh-CN; the brief did not specify, and the exam
  deliverable should follow the exam's language.
