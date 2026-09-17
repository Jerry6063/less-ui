# 随充 · 设备伴侣 — PRD summary (v1)

1. **Goal.** Turn a one-off accessory purchase into a registered device the owner can check, match and repair from one mini program, so the manual never has to be opened.
2. **Primary job (new buyer).** Scan the box QR, confirm the device, get warranty on file in under 60 seconds — no receipt, no account form.
3. **Primary job (owner).** Answer two questions fast: "how much is left in my power bank" and "can this charger fast-charge my laptop".
4. **Success metric (north star).** Share of registered devices per unit sold, measured 30 days post-purchase; launch target 35%, from an estimated 8% on the current warranty web form.
5. **Supporting metrics.** Onboarding completion 80%+ from scan to warranty confirmed; support tickets that arrive with device + issue pre-filled 70%+ (today ~15%), cutting first-reply handling time.
6. **Scope cut for v1 — no accessory store.** Compatibility results link out to the existing mall instead of carrying cart and checkout.
7. **Scope cut for v1 — single-user, no sharing.** No family device sharing, no transfer of warranty on resale; both need identity work that does not pay back before launch.
8. **Scope cut for v1 — three chargeable models in the finder.** The compatibility matrix ships hand-curated for top-selling phones and laptops, not an open model database.
9. **Risk — telemetry honesty.** Charge level and live wattage need a Bluetooth link; only Prime-series hardware reports it. Non-smart accessories must degrade to a warranty-and-support card, or the home screen reads as broken.
10. **Risk — compatibility claims are a liability.** A wrong "full speed" verdict becomes a support ticket and a review; every verdict needs a lab-measured wattage and an explicit "third-party proprietary fast charge not supported" line rather than an optimistic guess.
