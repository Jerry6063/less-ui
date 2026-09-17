# notes.md — run 02, device companion mini program (less-ui)

## Files read
- /Users/jerryhao/Dailywork/anker-ai-pilot-prep/skills-eval/.claude/skills/less-ui/SKILL.md (in full)
- /Users/jerryhao/Dailywork/anker-ai-pilot-prep/skills-eval/briefs/02-device-mini-program.md
- Nothing else. No other skill dir, no SKILL.v1-v4, no other run dir, no browser/preview tool.

## `:root` token block (verbatim)

```css
:root{
  /* palette: night-side instrument. deep blue-slate ground, one desaturated teal accent */
  --surface:#131A23;
  --raise:#1B2430;
  --sunk:#0E141B;
  --ink:#EDF3FA;
  --muted:#93A7BE;
  --line:#2B3746;
  --accent:#4FB3A4;
  --warn:#D9A442;
  --alert:#E4685F;

  --t-display:48px;
  --t-heading:24px;
  --t-body:16px;
  --t-meta:12px;

  --r-1:4px;
  --r-2:8px;
  --r-3:16px;

  --s-0:4px;
  --s-1:8px;
  --s-2:16px;
  --s-3:32px;

  --shadow-rest:0 1px 0 #2B3746;
  --shadow-lift:0 18px 44px rgba(7,11,16,.72);

  --font:"PingFang SC","Hiragino Sans GB","Heiti SC","Microsoft YaHei",sans-serif;
  --font-num:"SF Mono","JetBrains Mono",ui-monospace,Menlo,monospace;
}
```

## Direction and theme choice
Night-side instrument, not a store. The scene the brief describes — someone checking a power
bank in bed, on a train, in a bag at 23:00 — is a dark scene, and the screen's job is to report a
measurement (percent left, watts per port, watts achievable). So: dark blue-slate ground (#131A23,
deliberately blue rather than near-black), one desaturated teal accent (#4FB3A4) that reads as
"current flowing", amber and coral reserved for warranty-expiring and failure. The blocked
cream+terracotta pair and the near-black+acid-green pair were both checked as hex and avoided.
Type is PingFang SC (the native CJK face a WeChat mini program actually renders in — not a habit
default) with a mono face used only where it is legitimate: measured numerals (68, 45W, 96W,
timestamps). The one authored moment is the charge bar filling on entry; nothing else animates.

## Screens and wired navigation paths (6 sections, the brief's 5 screens)
1. `s-onboard` — 3 steps in one screen: scan (viewfinder is a real button that simulates a hit and
   prefills the SN) / manual SN entry, confirm device + purchase date, warranty registered.
2. `s-home` — skeleton -> real, or skeleton -> zero-device empty state.
3. `s-detail` — per-device, opened from any of the three home rows with different data each.
4. `s-compat` — three chargeable models, each produces a different verdict set.
5. `s-support` — issue chips, device select, photo attach, submit.
6. `s-ticket` — timeline (existing ticket, and the one you just filed).

Wired paths: scan-frame tap -> step 2; SN input (>=6 chars) enables "识别设备" -> step 2 -> step 3
-> home (also seeds a non-empty home). Home hero and both rows -> detail with their own title,
percent, lede and bar target. Detail back -> home. Detail firmware: error state -> 重试 -> update
row -> drawer (real bottom-sheet with scrim, Esc-free but click-scrim and cancel both close) ->
现在更新 rewrites the detail lede. Detail -> 报修 -> support. Empty home -> 扫码添加设备 ->
onboarding. Tab bar 设备 / 兼容 / 售后 on all three top-level screens, tab highlight follows pushed
screens. Compat: each of 3 model chips rewrites the focal wattage, its color, the verdict line, the
three per-charger rows and the cable advice; 去商城看这根线 only appears for the model that needs a
5A cable and turns into a confirmation. Support: issue chip + device select gate the submit button
(disabled is the message); select validates on blur with the error beside the field; photo attach
adds a real inline-SVG thumbnail; submit builds a new ticket timeline from the actual selections.
Existing ticket row -> its own timeline. Demo rig (labeled, outside the phone, never among product
controls): jump to any screen, toggle the zero-device state, replay the home skeleton.

## What I cut from the brief and why
- **Device registration as a separate screen from onboarding.** The brief lists "register the
  device" as a new-buyer job and onboarding as screen 5; they are the same three taps, so
  registration lives only in onboarding rather than being duplicated as a home action.
- **"Learn what it can charge" as a manual/spec page.** Folded into the compatibility finder — the
  honest version of that job is "will it fast-charge *my* laptop", not a spec sheet.
- **Ticket status as a sixth tab.** It is the tail of the support flow, so it is a pushed screen off
  support, not navigation.
- **Expected response time as a field/setting.** Rendered as one line of copy at the point of
  anxiety (above the submit button), plus the photo-retention line next to the attach control.
- **Any charts, rings or sparklines.** Nothing on these screens is a trend; a single 4px bar carries
  the only continuous quantity there is.

## Build passes and self-check fixes
Two passes total: write the file once, then the one-pass self-check (read once, fix once, ship).
Fixes made in that single pass:
1. Middle-dot meta strings (a section-2 tell) — replaced all " · " separators with natural
   punctuation, and updated the one JS `split()` that depended on the separator.
2. The scan viewfinder was decorative, so onboarding could dead-end for anyone who did not type an
   SN. Made it a real `<button>` that simulates a successful scan and advances.
3. "不是这台，重新扫 / 确认并登记" was two actions in one label — cut to "确认并登记保修".
4. The compatibility screen had no focal element at `--t-display` (self-check item 2). Added the
   answer number — the best achievable wattage — with a subtitle naming which charger it is, and
   colored it amber rather than accent when nothing reaches full speed, so the focal number cannot
   imply a good answer when the answer is bad.
No second review cycle, no rewrite.

## What the skill cost time
- The "every padding/margin/gap/font-size/radius references a token" rule is the expensive one: it
  has to be obeyed while writing, not after, and it forced a few awkward values (a 4px half-step
  token just for control interiors) rather than reaching for the obvious number.
- The 1.5x tier rule collides with the 16px-body-on-mobile floor: `--t-body:16px` and `--t-meta` can
  only be 1.33x apart unless meta drops to ~10.7px and becomes unreadable. Kept 16/12 and separated
  the tiers by color and weight instead. Worth a skill edit.
- The section-2 ban list is worth re-reading before writing rather than after: the middle-dot fix
  touched ~20 strings that would have been written differently the first time.
- Two perl substitutions missed (comment-rule dash count, then a CSS block that silently did not
  insert) and needed verification greps — self-inflicted, but a reminder that "fix once" still needs
  one confirmation read of the fix itself.
