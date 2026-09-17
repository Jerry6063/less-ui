# Brief 02 - Device companion mini program

Mirrors the "mini-program design" task family used in timed AI-collaboration assessments. Paste the whole brief as the first message.

## Context
You are the software PM for a charging-accessories brand. Domestic users buy a GaN charger or a
power bank and never open the manual. Design a WeChat-style mini program that becomes the
"companion" for the devices they own.

## Users and jobs
- New buyer: register the device, learn what it can charge, get warranty confirmed.
- Existing user: check power-bank charge level, find a compatible cable, file a support ticket.

## Screens (clickable flow, 5 screens)
1. Home: my devices, warranty status, one contextual tip.
2. Device detail: live charge level, output ports and their wattage, firmware update entry.
3. Compatibility finder: pick a phone or laptop model, see which owned charger can fast-charge it.
4. Support: choose issue, attach photo, expected response time, ticket status timeline.
5. Onboarding: first launch, scan the QR on the box, confirm device, done.

## Constraints
- One self-contained `index.html`, phone frame 375x812 centered on the page, tap navigation between screens.
- Realistic product names, prices and copy. Empty state for a user with zero devices.
- UI language: zh-CN, to mirror exam conditions.
- After the prototype, write a 10-line PRD summary: goal, success metric, scope cut for v1, risks.
