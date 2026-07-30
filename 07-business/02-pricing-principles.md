# Pricing principles

## Objective

Create a sustainable product without exploiting people during illness, grief or reduced capacity.

## Principles

- A useful free experience must exist.
- No essential safety or accessibility feature should be paywalled.
- Pricing and renewal terms must be plain.
- Cancellation and pausing should be easy.
- Do not use emotional urgency to sell.
- Do not make users pay merely to retrieve or delete their own content.
- Consider regional pricing and an access programme.
- Test willingness to pay before finalising price.

## Cost model — what actually costs money

This is the reasoning the free/paid split below is built on, not a separate consideration:

- **Near-zero marginal cost:** SMS/share-sheet sending (native OS composer, not a paid API), Circles and contact storage, Quiet History, basic Patterns (simple arithmetic on stored dates), Library/template storage, Email out-of-office (low-cost official APIs).
- **Real, usage-scaling cost:** AI-assisted drafting (Going Quiet, Reassurance, Reconnect and Conversations "AI Help," and any narrative Patterns text).

Because almost everything is cheap to provide, the free tier should be generous everywhere except AI usage — that's the one feature genuinely worth metering, and the natural lever that makes Hold+ pay for its own heaviest users rather than an arbitrary collection of paywalled features.

**AI allowance is one shared monthly pool**, not separate quotas per screen — simpler to understand ("you have 15 AI-assisted drafts this month") and simpler to control cost against than fragmenting it across Going Quiet/Reassurance/Reconnect/Conversations individually.

Usage here is episodic rather than habitual (an active quiet-and-reconnect period, then likely zero for weeks), which keeps average cost per free user low even with a cap that feels generous in the moment — see `02-research/...` reasoning on low-capacity, non-daily-use design.

## Suggested model

### Free

- Full Going Quiet / Taking Time / Reconnect / Conversations journey
- Unlimited Circles and contacts — deliberately not a paid differentiator, since Circles cost essentially nothing to provide; worth stating outright as a trust point ("organise as many people as you need, it's free"), not just leaving uncapped by default
- Quiet History, unlimited
- Basic Patterns (see `03-product/04-patterns.md`)
- Unlimited Library/template storage
- A generous shared monthly AI-assisted drafting allowance (exact number to be set once real usage data exists — see `08-decisions/04-open-questions.md`; treat 10–20/month as the working assumption until tested)
- Core accessibility and privacy controls
- No essential safety feature paywalled (see `01-foundation/03-principles.md`)

### Hold+

- Unlimited AI-assisted drafting
- **Built:** "Amend with AI" — a light-touch blend, not a from-scratch regenerate. Below the message box on Going Quiet, Reconnect, Taking Time's update, and Personalise/Conversations, an open prompt ("What's going on, if you want to share?") lets the model edit only what new context requires, keeping the rest of what's already in the box. See `04-ux-content/01-core-journeys.md`, "Amend with AI," and `06-privacy-security/02-ai-boundaries.md` for the mechanics.
- **Built:** AI memory, a separate two-layer opt-in — a standing "Remember helpful details" toggle (off by default, set in the Hold+ area, never an in-the-moment prompt), which lets the model quietly note a short detail while amending and offer it back later, during Taking Time or Reconnect, as a dismissible "Use it" / "Don't remember" suggestion. See `docs/03-privacy-model.md` (in `hold-app`) for the full consent/retention model.
- **Not yet built:** the broader "learning writing style, relationship-aware drafting" idea from the original roadmap cluster — see `03-product/05-roadmap.md` for the privacy consideration this still raises; distinct from, and larger than, the two features above
- Richer Patterns (seasonal trends, recurring timing, health-note correlations, longer-term summaries)
- Optional encrypted sync, multi-device use (future) — covers Hold's own data only (Circles, Library/templates, History, Patterns, settings) so it's available on a second device. Does not sync email/health app connections themselves — those are external OAuth/permission grants (Gmail, Outlook, HealthKit, Health Connect) that each device authenticates to independently; Hold doesn't hold or relay those credentials between devices.

**Deliberately not monetised:** Trusted Contact (`03-product/05-roadmap.md`), if built at all, stays free and separate from the subscription conversation entirely. Charging for a feature that gives one person visibility into another's status — even scoped narrowly to status-only, revocable, opt-in — risks Hold appearing to profit from something adjacent to surveillance. Not worth the trade-off for the revenue it would add.

### One-time purchases, available to everyone

Not gated behind Hold+ — purchasable by free-tier users too, independent of any subscription:

- **Formatted GP/clinician PDF export** — raw data export is free for everyone, always (see `03-product/04-patterns.md`); the formatted PDF report is £3.99 as a one-time, non-subscription purchase, available whether or not someone is a Hold+ subscriber — treated as a first-class part of the monetisation strategy, not a minor add-on, since it targets a sharp, high-motivation need that doesn't require an annual commitment. Was previously listed under the Hold+ feature list above, which wrongly implied it was subscription-gated; moved here to make the distinction explicit.

### Notifications/reminders — resolved

Previously listed as a vague "Customisable reminders" Hold+ line with nothing actually specified. **Decided:** basic notification control is free for everyone — this includes the Taking Time reconnect nudge and its user-chosen interval (already decided in `04-ux-content/01-core-journeys.md`), since "no essential safety or accessibility feature should be paywalled" applies here; a wellbeing-adjacent reminder shouldn't be gated. What could reasonably be Hold+ instead is *finer-grained* control — e.g. different reminder timing per Circle, multiple reminder types — not the basic on/off + interval control itself.

## Initial price hypothesis (updated)

**Decision:** launch with a Founding Member offer, not the earlier £2.99–£3.99 / £19.99–£24.99 range.

| | Founding Member (launch) | Standard (later) |
|---|---|---|
| Annual | £17.99/year (≈ £1.50/month) | £29.99/year (≈ £2.50/month) |
| Monthly | £1.99/month | £2.99/month |

Founding Members keep their annual price for as long as their subscription stays active — a reward for early supporters, not a time-limited discount that expires on them.

Annual is the recommended, primary option on the paywall; monthly is always visible too, never hidden, for people who can't commit to an annual payment up front. Show the annual price with its monthly-equivalent underneath (e.g. "£17.99/year (≈ £1.50/month)").

A one-tap "Pause subscription" option should exist — no emailing support, no retention flow. This is on-brand: the people most likely to need Hold are also the people most likely to be overwhelmed by a difficult cancellation process.

Avoid a weekly plan. It can feel predatory for a product used during vulnerability.

A lifetime plan should not be offered until ongoing infrastructure and AI costs are understood.

### Pricing philosophy

Hold exists to reduce emotional burden, not create financial burden. Pricing should always remain accessible, transparent and fair — balancing business sustainability against the reality that some users will be experiencing overwhelm, illness or financial difficulty at the exact moment they need the product most.

### Realism and consistency check

- **Internal consistency:** £1.99/month × 12 = £23.88 against £17.99/year is a ~25% annual saving; £2.99/month × 12 = £35.88 against £29.99/year is a ~16.5% saving. Both are within the normal range for a monthly-vs-annual incentive (SaaS convention is roughly 20–40%) — consistent, not contradictory.
- **Market comparison:** £17.99–£29.99/year is materially cheaper than comparable wellbeing subscriptions (Balance ≈ £49.99/year, Inflow ≈ £20–23/month) and in line with simpler single-purpose apps like Structured (≈ £17.99/year) — realistic for a narrower-scope MVP, with room to raise the standard price later once Patterns/Insights, exports and integrations exist to justify it.
- **Margin reality:** App Store/Google Play commission (typically 15% under the small-business programme, 30% otherwise) applies before any hosting, AI or support costs are counted — model net revenue at roughly 70–85% of gross subscription income, not 100%, when forecasting.
- **Not yet stress-tested:** none of this has been validated against actual willingness-to-pay data. The number is a reasoned hypothesis consistent with the product's stated values, not a tested price.

## Ethical access options

**No free trial, deliberately** (see `08-decisions/01-decision-log.md`) — the free tier is already generous enough (full journey, unlimited Circles/History/Library, basic Patterns, a shared AI allowance, and the GP/clinician PDF export available free-tier too) that someone can fully evaluate whether Hold works for them before Hold+ is even relevant. A trial isn't needed to unlock basic access the way it would be for a normally-gated product.

- One-tap cancellation route
- Scholarship or sponsored access
- Regional pricing where supported
- Gift subscriptions later

## The paywall/upgrade moment

**Built, though without a working purchase flow yet** — no entitlement/billing system exists in the app. The destination is an honest Hold+ info screen (`app/settings/hold-plus.tsx`) built from this document's real content: what's free, what Hold+ would add, the Founding Member pricing table, and the fair-access commitments below, closing with a plain "not open for purchase yet" note. No fake Subscribe button — building one would invent a purchase flow this book doesn't actually specify.

Principle: Hold+ should be discoverable, not interruptive. No forced upsell modal blocking the core Going Quiet/Taking Time/Reconnect journey — someone in the middle of going quiet should never hit a paywall.

Two access points reach the info screen, both covered in "Hold+ visibility" in `04-ux-content/04-navigation-architecture.md`:
- The Settings drawer's Hold+ row.
- Contextual surfacing at natural moments — currently the Patterns screen's "More with Hold+" section, an additive invitation shown below the free stats rather than a locked or greyed-out preview (see `03-product/04-patterns.md`). A quiet, dismissible mention where a Free-tier limit is genuinely reached (e.g. the AI reply allowance for the month) remains a natural future discovery point too, once that limit exists.

**No standing persistent top-bar element.** Considered and dropped — a permanently visible Hold+ badge in the top bar reads as ongoing pressure/visual noise, inconsistent with Hold's "held, not managed" tone, even styled quietly. See `08-decisions/01-decision-log.md`.

No countdown timers, no "you're missing out" framing, no interstitial that appears uninvited during the core journey, and no locked/greyed-out data — someone should never feel Hold is withholding their own information from them.
