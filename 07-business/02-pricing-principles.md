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

Because almost everything is cheap to provide, the free tier is generous everywhere except AI usage — AI-assisted drafting is Hold+-only, not metered-then-capped for free users, and is the natural lever that makes Hold+ pay for its own heaviest users rather than an arbitrary collection of paywalled features. (Historical note: an earlier version of this model gave free users a shared monthly AI allowance rather than excluding them from AI entirely — see `08-decisions/04-open-questions.md` for where that's tracked; the reasoning here reflects the current AI-is-Hold+-only state.)

Usage here is episodic rather than habitual (an active quiet-and-reconnect period, then likely zero for weeks), which keeps average AI cost per Hold+ subscriber low even relative to subscription price — see `02-research/...` reasoning on low-capacity, non-daily-use design.

## Suggested model

### Free

- Full Going Quiet / Taking Time / Reconnect / Conversations journey
- Unlimited Circles and contacts — deliberately not a paid differentiator, since Circles cost essentially nothing to provide; worth stating outright as a trust point ("organise as many people as you need, it's free"), not just leaving uncapped by default
- Quiet History, unlimited
- Basic Patterns (see `03-product/04-patterns.md`)
- Unlimited Library/template storage
- Core accessibility and privacy controls — explicitly includes the Accessibility & Display warmth bar (`04-ux-content/04-navigation-architecture.md`), confirmed free-tier 2026-08-20 on accessibility grounds (light sensitivity, photophobia) rather than left ambiguous alongside the Look & Feel settings it sits next to
- No essential safety feature paywalled (see `01-foundation/03-principles.md`)
- **Optional encrypted backup/sync, multi-device use — moved here from Hold+, 2026-08-20.** Covers Hold's own data only (Circles, Library/templates, History, Patterns, settings) so it's available on a second device. Does not sync email/health app connections themselves — those are external OAuth/permission grants (Gmail, Outlook, HealthKit, Health Connect) that each device authenticates to independently; Hold doesn't hold or relay those credentials between devices. See `08-decisions/01-decision-log.md` for the reasoning; `06-privacy-security/04-content-retention.md`'s "Lapsed/dormant Hold+ backup account retention" section is now stale as a result — its scope note ties the whole retention proposal to the backup being a Hold+-only feature, which is no longer true, and needs its own correction pass, flagged separately, not done here

### Hold+

- Unlimited AI-assisted drafting
- **Built:** "Amend with AI" — a light-touch blend, not a from-scratch regenerate. Below the message box on Going Quiet, Reconnect, Taking Time's update, and Personalise/Conversations, an open prompt ("What's going on, if you want to share?") lets the model edit only what new context requires, keeping the rest of what's already in the box. See `04-ux-content/01-core-journeys.md`, "Amend with AI," and `06-privacy-security/02-ai-boundaries.md` for the mechanics.
- **Built:** AI memory, a separate two-layer opt-in — a standing "Remember helpful details" toggle (off by default, set in the Hold+ area, never an in-the-moment prompt), which lets the model quietly note a short detail while amending and offer it back later, during Taking Time or Reconnect, as a dismissible "Use it" / "Don't remember" suggestion. See `docs/03-privacy-model.md` (in `hold-app`) for the full consent/retention model.
- **Not yet built:** the broader "learning writing style, relationship-aware drafting" idea from the original roadmap cluster — see `03-product/05-roadmap.md` for the privacy consideration this still raises; distinct from, and larger than, the two features above
- Richer Patterns (seasonal trends, recurring timing, health-note correlations, longer-term summaries)
- ~~Optional encrypted sync, multi-device use (future) — covers Hold's own data only...~~ **Moved to Free, 2026-08-20 — see "Suggested model: Free" above and `08-decisions/01-decision-log.md`.**

**Deliberately not monetised:** Trusted Contact (`03-product/05-roadmap.md`), if built at all, stays free and separate from the subscription conversation entirely. Charging for a feature that gives one person visibility into another's status — even scoped narrowly to status-only, revocable, opt-in — risks Hold appearing to profit from something adjacent to surveillance. Not worth the trade-off for the revenue it would add.

### One-time purchases, available to everyone

Not gated behind Hold+ — purchasable by free-tier users too, independent of any subscription:

- **Patterns Report** — raw data export is free for everyone, always (see `03-product/04-patterns.md`); the formatted, one-time **Patterns Report** is ~~£2.99~~ **£2.50 standalone, free with an active Hold+ subscription** (corrected 2026-08-20, see "Pricing corrected 2026-08-20" below), available whether or not someone is a Hold+ subscriber — treated as a first-class part of the monetisation strategy, not a minor add-on, since it targets a sharp, high-motivation need that doesn't require an annual commitment. A polished summary of quiet periods, durations and pattern observations — genuinely useful to bring to a GP or clinician appointment if that's what someone needs it for, but not framed as a medical document or restricted to that use; someone might just as easily want it to look back over their own year. **Supersedes, 2026-08-11:** the earlier separate "formatted GP/clinician PDF export" (£3.99) and the separately-logged, unreconciled £2.99 "Patterns Report" are now one product at one price — see "2026-08-11 correction" below and `08-decisions/01-decision-log.md`.

### Notifications/reminders — resolved

Previously listed as a vague "Customisable reminders" Hold+ line with nothing actually specified. **Decided:** basic notification control is free for everyone — this includes the Taking Time reconnect nudge and its user-chosen interval (already decided in `04-ux-content/01-core-journeys.md`), since "no essential safety or accessibility feature should be paywalled" applies here; a wellbeing-adjacent reminder shouldn't be gated. What could reasonably be Hold+ instead is *finer-grained* control — e.g. different reminder timing per Circle, multiple reminder types — not the basic on/off + interval control itself.

## Initial price hypothesis (updated 2026-08-20 — see "Pricing corrected 2026-08-20" below for the current model)

~~**Decision: £17.99/year as the standing annual price; £4.99/3-month as an initial paid trial...**~~ **Superseded 2026-08-20** — see "Pricing corrected 2026-08-20" below for the current figures.

Annual is the recommended, primary option on the paywall; the 3-month intro price is always visible too, never hidden, as the lower-commitment entry point.

A one-tap "Pause subscription" option should exist — no emailing support, no retention flow. This is on-brand: the people most likely to need Hold are also the people most likely to be overwhelmed by a difficult cancellation process.

Avoid a weekly plan. It can feel predatory for a product used during vulnerability.

A lifetime plan should not be offered until ongoing infrastructure and AI costs are understood.

### Pricing philosophy

Hold exists to reduce emotional burden, not create financial burden. Pricing should always remain accessible, transparent and fair — balancing business sustainability against the reality that some users will be experiencing overwhelm, illness or financial difficulty at the exact moment they need the product most.

### Realism and consistency check

- ~~**3-month tier consistency:** £4.99 × 4 = £19.96/year if someone stayed on the 3-month cadence continuously, a modest ~11% premium over the £17.99 annual price for the flexibility of a shorter commitment — within normal range for a shorter-cadence option, not a bait price.~~ **Superseded 2026-08-12** — this math assumed the 3-month option was a permanent, repeatable cadence someone could stay on indefinitely. Under the resolved trial model, it isn't repeatable in that sense: £4.99 is a one-time introductory price for a single 3-month period, after which the subscription converts to an ongoing monthly or yearly price. The relevant consistency check is now against whatever the ongoing monthly price turns out to be, which hasn't been set — see "3-month tier: resolved 2026-08-12" below.
- **Market comparison:** £19.99/year (was £17.99/year, corrected 2026-08-20) is materially cheaper than comparable wellbeing subscriptions (Balance ≈ £49.99/year, Inflow ≈ £20–23/month) and in line with simpler single-purpose apps like Structured (≈ £17.99/year) — realistic for a narrower-scope MVP. **Not re-verified against the new figure** — this comparison was written against the superseded £17.99/year price; the conclusion likely still holds at £19.99/year given the size of the gap to Balance/Inflow, but that's an assumption, not a re-check.
- **Margin reality:** App Store/Google Play commission (typically 15% under the small-business programme, 30% otherwise) applies before any hosting, AI or support costs are counted — model net revenue at roughly 70–85% of gross subscription income, not 100%, when forecasting.
- **Not yet stress-tested:** none of this has been validated against actual willingness-to-pay data. The number is a reasoned hypothesis consistent with the product's stated values, not a tested price.

## Ethical access options

~~**No free trial, deliberately** (see `08-decisions/01-decision-log.md`) — the free tier is already generous enough (full journey, unlimited Circles/History/Library, basic Patterns, and the raw data export available free-tier too) that someone can fully evaluate whether Hold works for them before Hold+ is even relevant. A trial isn't needed to unlock basic access the way it would be for a normally-gated product. **Confirmed 2026-08-11:** this holds unchanged under the correction below — neither the £17.99/year price nor the new £4.99/3-month option carries a trial period or an auto-converting introductory rate.~~

**Superseded 2026-08-12.** The £4.99/3-month option is now a paid introductory trial that auto-converts to an ongoing monthly-or-yearly subscription — see "3-month tier: resolved 2026-08-12" below. Precisely what's still true: there is still no **free** ($0) trial gating basic access — the free tier itself remains the way someone evaluates Hold before paying anything at all, and that reasoning stands unchanged. What's no longer true: the annual price has an adjacent 3-month product that *does* carry a trial-like mechanic and *does* auto-convert, which the struck-through text above explicitly ruled out same-day, before being reversed by direct instruction. **Flagged as needing real attention before build, not just a note:** an auto-converting subscription has real disclosure obligations under this document's own "Pricing and renewal terms must be plain" principle above and under App Store/Play Store subscription guidelines — price after conversion, exact conversion date, and cancellation method all need to be stated clearly at signup, not buried in terms. This copy hasn't been drafted yet.

- One-tap cancellation route
- Scholarship or sponsored access
- Regional pricing where supported
- Gift subscriptions later

## The paywall/upgrade moment

**Built, though without a working purchase flow yet** — no entitlement/billing system exists in the app. The destination is an honest Hold+ info screen (`app/settings/hold-plus.tsx`) built from this document's real content: what's free, what Hold+ would add, the pricing, and the fair-access commitments below, closing with a plain "not open for purchase yet" note. No fake Subscribe button — building one would invent a purchase flow this book doesn't actually specify. **Checked directly against the actual code: `app/settings/hold-plus.tsx` line 30 currently shows `£17.99/year (≈ £1.50/month)` for "Founding" and `£29.99/year (≈ £2.50/month)` for "Standard"** — the Founding Member/Standard split itself was removed by the 2026-08-11 correction below, so this screen is stale against that decision too, not just today's pricing correction. Flagged as needing a code update; not fixed here, since this file documents the app, it doesn't edit it.

Principle: Hold+ should be discoverable, not interruptive. No forced upsell modal blocking the core Going Quiet/Taking Time/Reconnect journey — someone in the middle of going quiet should never hit a paywall.

Two access points reach the info screen, both covered in "Hold+ visibility" in `04-ux-content/04-navigation-architecture.md`:
- The Settings drawer's Hold+ row.
- Contextual surfacing at natural moments — currently the Patterns screen's "More with Hold+" section, an additive invitation shown below the free stats rather than a locked or greyed-out preview (see `03-product/04-patterns.md`). A quiet, dismissible mention where a Free-tier limit is genuinely reached remains a natural future discovery point too, once such a limit exists — AI-assisted drafting itself is no longer an example of this, since it isn't a free-tier feature at all.

**No standing persistent top-bar element.** Considered and dropped — a permanently visible Hold+ badge in the top bar reads as ongoing pressure/visual noise, inconsistent with Hold's "held, not managed" tone, even styled quietly. See `08-decisions/01-decision-log.md`.

No countdown timers, no "you're missing out" framing, no interstitial that appears uninvited during the core journey, and no locked/greyed-out data — someone should never feel Hold is withholding their own information from them.

## 2026-08-11 update: Hold+ margin reasoning, and two new one-time purchases

**Hold+ annual price reaffirmed at £17.99/year** — this is the same figure as the existing Founding Member annual price above, now with real margin math behind it: checked against current Sonnet API pricing ($3/$15 per million tokens, standard rate), even heavy AI usage costs low single-digit pounds per subscriber per year, so margin stays healthy at this price. Deliberately priced well below the wellness-app category (Headspace/Calm ≈ £55–58/yr, Wysa ≈ £80/yr) — a meaningful share of Hold's audience is chronically ill people with unstable income, and pricing near category norms would create a real barrier for exactly the people the app is meant to serve. This was a deliberate choice over raising the price toward category norms, even though margin would comfortably allow it. **Resolved 2026-08-11:** the Founding Member vs. Standard structure and both monthly tiers (£1.99/£2.99) are removed entirely, not merely left unmentioned — see "2026-08-11 correction" below. **Partially revised 2026-08-12:** a monthly cadence returns as an ongoing post-trial option (see "3-month tier: resolved 2026-08-12" below) — but at a price not yet set, distinct from and not a resurrection of the £1.99/£2.99 Founding Member-era figures removed here.

**One-time AI credit pack — new, £2.99.** A fixed number of AI drafts, never expiring, no subscription commitment — a low-friction entry point before asking for the Hold+ subscription. Sits alongside, not instead of, Hold+'s unlimited AI drafting above. Unaffected by the 2026-08-11 correction below — a separate product from the Patterns Report.

**Patterns Report — £2.99.** **Resolved 2026-08-11** (was flagged as a tension with the existing model, not silently overwritten): merged with the £3.99 GP/clinician PDF export into a single product at a single price — see "One-time purchases, available to everyone" above and "2026-08-11 correction" below. Basic Patterns stays free-tier, richer Patterns stays a Hold+ subscription benefit, both unaffected by this merge — only the paid, formatted one-time report changed. **Patterns itself remains not-yet-scoped** (what data it draws from, what it actually shows, whether the existing AI memory data can feed into it) — that part is still open.

## 2026-08-11 correction: Founding Member split removed, GP export merged into Patterns Report, £4.99/3-month tier added

Resolves three items left open above: the Founding Member/Standard pricing table (originally `08-decisions/01-decision-log.md`, 2026-07, "Revise pricing to a Founding Member launch offer"), the £3.99 GP/clinician PDF export figure (same log, 2026-07 and 2026-07-29 entries), and the "not clear whether it replaces, coexists with, or reprices" flag on the £2.99 Patterns Report immediately above. Full record, including which specific prior log rows this supersedes, is in `08-decisions/01-decision-log.md`, 2026-08-11.

- **Pricing structure simplified to one subscription price plus one shorter-cadence option.** £17.99/year is now the only Hold+ *standing* subscription price — no Founding Member vs. Standard distinction, no separate monthly cadence at £1.99 or £2.99. Alongside it, a new **£4.99/3-month** option gives a lower-commitment entry point for people who don't want to pay for a full year up front. ~~No trial and no auto-converting introductory rate on either cadence.~~ **Superseded 2026-08-12 — see "3-month tier: resolved 2026-08-12" below:** the £4.99/3-month option is now specifically a paid trial that auto-converts, not a standalone permanent product. Everything else in this bullet (no Founding Member split, £17.99/year standing annual price) still stands.
- **GP/clinician PDF export and Patterns Report merged into one product.** One paid, one-time purchase — **Patterns Report, £2.99** — replaces both the earlier £3.99 GP/clinician PDF export and the separately-priced £2.99 Patterns Report that had been logged without being reconciled against it. Reframed so it isn't defined by medical use: still genuinely useful to bring to a GP or clinician appointment, but pitched as a general formatted summary of someone's own quiet periods and patterns, not a medical-only document.
- **Free-tier basic Patterns is unaffected.** The free/Hold+ Patterns split described in "Suggested model" above (basic Patterns free, richer Patterns a Hold+ benefit) stands as already documented — this correction only touches the paid one-time report, not the underlying free feature.
- **AI credit pack (£2.99) is unaffected** — a separate product from the Patterns Report, not touched by this correction.

## 3-month tier: resolved 2026-08-12 — trial-converts-to-ongoing is the final decision

**Resolved, per direct instruction.** This section previously recorded an unreconciled conflict between two directions; that conflict is now closed. The **trial** direction is confirmed as final, superseding the 2026-08-11 "permanent parallel tier, no trial" model recorded earlier in this document (struck through in place above, not deleted, so both versions stay visible in the file's history).

**Final decision:** £4.99/3-month is a **paid introductory trial**, not a permanent standalone product. It auto-converts at the end of the 3 months into an ongoing subscription, at the person's choice of **monthly or yearly** billing. £17.99/year remains the standing annual price, both as the direct paywall option and as one of the two post-trial conversion choices.

**Reasoning carried over from the source write-up:** a *permanent* 3-month tier priced proportionally to annual risked people defaulting to repeated short-term "just in case" purchases instead of ever committing annually — cannibalising annual subscriptions. Framing it as a one-time trial avoids that, while still giving a genuinely lower-commitment entry point than a full year up front. This also fits the "episodic capacity drop" audience reframing logged in `07-business/06-business-strategy.md` — someone who only needs Hold for a few months has an honest product to buy, rather than either overcommitting to a year or repeatedly re-buying a short cycle indefinitely.

~~**Not yet specified — a real gap, not an oversight:** the ongoing **monthly** price...~~ **Resolved 2026-08-20 — see "Pricing corrected 2026-08-20" below.** The ongoing monthly price is now set at £3.49/month.

**Also not yet specified:** the exact conversion mechanic — whether someone chooses monthly-or-yearly at the point of starting the 3-month intro (which the intro price would then be attached to, matching how App Store/Play intro pricing is typically configured against a specific underlying plan) or is asked to choose only once it ends. This is a real technical/product decision, not just a copy detail, and needs resolving before build. **Still open** — the 2026-08-20 pricing correction below fixed the figures, not this mechanic.

**Disclosure requirement, not yet drafted:** see "Ethical access options" above — an auto-converting intro price needs clear, plain disclosure of the post-intro price, the conversion date, and how to cancel before it converts, consistent with this document's own "pricing and renewal terms must be plain" principle. No copy exists for this yet.

## Pricing corrected 2026-08-20 — supersedes the £4.99/3-month and £17.99/year figures above

**Confirmed directly by Bethany, 2026-08-20 — no separate source document exists for this correction; logged from direct confirmation, not a prior write-up or commit.** This corrects a real gap, not a new preference: the underlying decision was reportedly made 2026-08-13, but was never actually written into this file, which continued to show the superseded £4.99/£17.99 figures (and explicitly flagged the ongoing monthly price as "not yet specified," which this correction also resolves).

**Current figures, standing model:**
- **£4.50, one-time intro price covering the first 3 months** (was £4.99/3-month).
- **Converts to an ongoing subscription at £3.49/month or £19.99/year**, person's choice (was £17.99/year standing annual price, with the monthly figure previously unset).
- **Patterns Report: £2.50 standalone; free to anyone with an active Hold+ subscription** (was £2.99 standalone, always paid regardless of Hold+ status — this is a new benefit, not just a price cut, and should be reflected in Hold+'s own feature list above, not just here).
- **AI credit pack: £2.99 — unchanged**, not affected by this correction.

**Not resolved by this correction, still open:** the exact conversion mechanic (monthly-or-yearly chosen at intro start vs. at conversion) and the auto-converting-price disclosure copy, both flagged immediately above — this correction fixed the figures themselves, not those two remaining product/legal questions.
