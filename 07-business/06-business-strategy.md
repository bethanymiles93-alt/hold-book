# Business strategy

This is business-operations material, not product/UX decisions — kept separate from `02-pricing-principles.md` on purpose so pricing philosophy stays focused on what the user pays and why, while this file covers what it costs to build and run Hold, and how it might grow.

## Pre-launch costs (rough, one-off)

| Item | Approx. cost |
|---|---|
| Company registration | £50 |
| Domain | £10–20/year |
| UK trademark (one class) | ~£170 |
| Apple Developer account | ~£79/year |
| Google Play developer account | ~£20 one-off |
| Landing page | £20–100/year |

Budget roughly **£400–700** to get everything registered and live, before ongoing running costs.

## Running costs (approximate, will vary with actual usage)

| Users | Approx. monthly cost |
|---|---|
| 100 | £30–70 |
| 500 | £80–180 |
| 1,000 | £150–300 |

Hold isn't video- or media-heavy, so infrastructure costs should stay comparatively low relative to user count. AI drafting cost is the main variable to watch as usage scales — this is part of why AI drafting is gated behind Hold+ entirely, with no free-tier allowance, rather than offered free and capped (see `02-pricing-principles.md`).

## Revenue scenarios

Illustrative only, not a forecast — net of Apple/Google commission (typically 15% under the small-business programme, 30% otherwise), before hosting/AI/support costs.

| Scenario | Paying users | Approx. monthly recurring revenue (gross) |
|---|---|---|
| Conservative | 100 | ~£250–330 |
| Modest early traction | 500 | ~£1,300–1,650 |
| Good first year | 1,000 | ~£2,600–3,300 |
| Strong | 2,000 | ~£5,200–6,600 |

Treat 100–300 paying users in the first year as a genuinely good outcome, not a disappointing one — it's real evidence people will pay for the problem Hold solves, and a much healthier bar to plan against than assuming thousands of subscribers early.

**Two one-time IAP lines** (full pricing reasoning in `02-pricing-principles.md`): an AI credit pack (£2.99, non-expiring, no subscription) as a low-friction entry point ahead of the Hold+ subscription decision; the Patterns Report (£2.99) — now the single merged product superseding the earlier separate £3.99 GP/clinician PDF export and the previously-unreconciled £2.99 Patterns Report price, see `08-decisions/01-decision-log.md`, 2026-08-11 correction. Patterns itself isn't yet scoped, so treat this as a logged price only, not a revenue line to model yet.

**3-month tier as an initial trial, not a permanent parallel tier — directional decision from a 2026-08-11 session, confirmed final 2026-08-12.** Full detail and the final resolved structure live in `07-business/02-pricing-principles.md` ("3-month tier: resolved 2026-08-12") — that document is the source of truth, this is a pointer, not a duplicate. Summary: £4.99/3-month functions as a paid introductory trial that auto-converts to an ongoing monthly-or-yearly subscription, rather than a standalone product someone could stay on indefinitely — reasoning being that a permanent proportionally-priced 3-month tier risked people defaulting to repeated short-term purchases instead of ever committing annually, cannibalising annual subscriptions. This is documented as the final *decision*, not yet reflected in any actual implementation — no billing/entitlement system exists in the app at all yet (see "Legal and compliance" below and `hold-plus.tsx`'s own "not open for purchase yet" state), and the ongoing monthly price this converts to hasn't been set. Revenue modelling above doesn't yet account for trial-to-paid conversion rates, since there's no usage data to model it against.

## Marketing approach

Education and trust-building before paid acquisition, not the other way round.

1. **Immediately:** secure app name, domain, social handles.
2. **1–2 weeks out:** landing page with email sign-up, logo, simple brand identity, "coming soon."
3. **3–4 weeks out:** regular content — why Hold exists, design decisions, accessibility choices, development stories (without identifying anyone), never framed as a hard sell.
4. **2 weeks before launch:** open a waitlist, invite beta testers from relevant communities.
5. **Launch week:** Product Hunt, LinkedIn, Instagram, Threads, relevant subreddits (where research/self-promotion rules permit), TikTok as an experiment.

If paid ads are used at all, start small (£150–300/month) to learn before scaling spend — don't lead with advertising budget.

**Positioning note:** market Hold as diagnosis-agnostic. Early adopters are likely to come from PMDD, ADHD, chronic illness and mental health communities because those groups often experience the underlying problem first-hand, but the product is for anyone whose capacity to communicate is temporarily reduced — burnout, grief, caring responsibilities, or general overwhelm included. Narrowing the brand to one diagnosis would undersell the actual addressable audience.

### Audience reframing: episodic capacity drop, not diagnosis — logged 2026-08-12

**Elaborates the positioning note above, doesn't contradict it — significant enough to warrant its own subsection, since it affects messaging and growth strategy directly, not just an internal note.**

**The trigger:** discussing a family member with a relevant condition (chronic fatigue) who doesn't obviously fit Hold's target user despite having "the" diagnosis, since she works full-time and communicates well — exposing that "has condition X" is the wrong targeting frame entirely.

**Reframed audience: episodic capacity drop, not any specific diagnosis.** Groups discussed as strong fits: burnout (occupational or caregiver), depression (episodic more than chronic/well-managed), grief (especially acute/early), Long Covid/ME/CFS/autoimmune flares specifically (distinct from well-managed chronic illness), postpartum, neurodivergent burnout/shutdown, and acute crisis periods generally (job loss, breakup, new diagnosis). Neurodivergent burnout was flagged as a plausible strong fit for the existing community-outreach growth strategy above, given active, organised online communities in that space.

**Why this is treated as a genuine repositioning worth carrying into growth strategy and messaging, not just an interesting aside:** "episodic capacity drop" both more accurately describes who Hold already serves (matches the Going Quiet-as-a-state, not Going Quiet-as-a-label design already established elsewhere in this book) and is a more defensible, non-exclusionary positioning than any single diagnosis. Worth reflecting in future landing-page copy, community-outreach targeting, and the marketing-approach timeline above, not just recorded here as background.

## IP and company structure

- **"Hold" as a name has a known UK trademark conflict** (Hold Platform Ltd, Malta-registered fintech, holds Class 9 software marks) — needs proper trademark clearance, or a rename, before committing further branding spend. Alternatives already explored: Vouch, Constant, Tend, Harbour, Amity.
- **Own everything through a company, not personally** — code, branding, trademark, domain, website. Makes things far cleaner if developers or investors get involved later.
- **Copyright exists automatically** on code, design, and copy as it's created — no UK registration needed.
- **A patent is not recommended.** Software patents are slow, expensive, and unlikely to protect the actual value here, which comes from brand, design judgement, trust and execution rather than a patentable mechanism.
- **Developer agreements** (if anyone else is ever brought on to build) should explicitly assign all created IP to the company.

## Revenue idea, now resolved: one-time export purchase

**Resolved, updated 2026-08-11.** Two tiers, not one. Raw data export (a plain CSV/text list of quiet periods and durations) is free for everyone, always — charging for someone's own raw data would sit uncomfortably against data portability norms and wasn't worth the reputational risk for what it would add in revenue. The paid one-time purchase is the **Patterns Report** — quiet periods, durations, and pattern observations laid out and summarised — priced at **£2.99**. This merges what were previously two separately-priced, unreconciled products (a £3.99 "formatted GP/clinician PDF report" and a separately-logged £2.99 "Patterns Report") into one, and drops the medical-only framing: still genuinely useful to bring to a GP or clinician appointment, but pitched as a general summary of someone's own patterns, not a document defined by that one use case. See `08-decisions/01-decision-log.md`, 2026-08-11 correction.

Captures revenue at a genuinely high-motivation moment — wanting a clear look at one's own quiet periods and patterns, whether for a medical appointment or just for oneself — without forcing a subscription decision someone may only need once or twice a year.

## Revenue realism check

The ARR scenarios discussed earlier in this repository's history (roughly £5k conservative to £2M exceptional, depending on downloads and conversion) were reasoned before the free tier was this fully specified, and before AI drafting moved fully behind Hold+. Worth revisiting that lens now, with two forces pulling in different directions rather than one clear signal:

**Toward higher conversion:** AI drafting was likely the single most-differentiated feature free users experienced. With it now fully paywalled, the free tier presents a harder, clearer wall than the "generous, low-pressure" free tier this document originally reasoned about — someone who wants AI help has no free path to it at all, which is a stronger conversion trigger than any volume cap.

**Against higher conversion:** the same move reduces what free users get day-to-day, which cuts against the trust-and-word-of-mouth case this document also makes — free tier without AI is a less compelling thing to use regularly or recommend, which could shrink the pool of people who ever get far enough to consider paying.

Which force dominates isn't resolvable from reasoning alone, and this document shouldn't pretend otherwise — it depends on real usage data this project doesn't have yet (how much people actually wanted AI vs. the rest of the free tier, how much referral was ever driven by it). Until that data exists, the honest expectation stays where it was: lean toward the conservative-to-modest end of the scenarios above, not toward a rosier read just because the wall got harder in one specific place.

None of this changes the underlying case for the product — the problem is real, differentiated, and under-served by existing "wellness" or "productivity" framing — but the honest expectation should continue leaning conservative-to-modest unless and until real usage data says otherwise. Treat the ARR figures elsewhere in this repository as directional hypotheses, not commitments.

## Legal and compliance (cross-reference)

This overlaps with the outstanding legal work already tracked for Hold: privacy policy, GDPR/DPIA, terms of service (liability, not medical/crisis advice), data processing agreements, and — per `06-privacy-security/03-safeguarding.md` — solicitor and/or clinical safety consultant sign-off on the safeguarding trigger logic specifically. None of the business strategy above should proceed to real users ahead of that review.

**Extended 2026-08-28** with a full international compliance research thread — `06-privacy-security/06-aadc-compliance-review.md` (UK Children's Code), `09-research/international-data-protection-applicability.md`, `09-research/global-architecture-scan-pass1.md`, and `09-research/ai-act-and-remaining-compliance.md`. The last of these carries a consolidated, priority-ordered list of the items that actually need solicitor time (EU AI Act high-risk classification, Online Safety Act/DSA-equivalent scope, GDPR Article 27 EU representative, medical device classification) — everything else surfaced in that research is either a confirmed non-issue, low-cost business setup, or an already-logged future spec item, not something adding to this list.

## MVP status check — verified against the codebase 2026-08-12, supersedes the earlier snapshot

A prior session write-up included a same-day-to-day-old MVP status snapshot, explicitly self-flagged as unverified. This section replaces it with findings checked directly against `hold-app`'s actual code (file/directory presence, not just recent commit messages), current as of 2026-08-12 — re-verify before relying on it for planning further out than that, the same caveat the snapshot it replaces carried.

**Core journey (Going Quiet, Taking Time, Reconnect, Conversations/Library) — built and under active iteration.** `app/create/` (people.tsx, done.tsx) and `app/return/` (reconnect.tsx, update.tsx, transition.tsx, done.tsx) exist; `app/(tabs)/library.tsx` covers Conversations/Library, `app/(tabs)/history.tsx` and `index.tsx` cover History and Home. Recent commit history (last ~15 commits) shows substantial, active rework of Going Quiet's send model, Reconnect's completion flow, and Conversations' per-person reply structure — consistent with "done/mostly done but still moving," not finished-and-static.

**Circles — built.** `circleService.ts`, `AdaptiveCircleChip.tsx`, `SelectionCircle.tsx`, and a dedicated `app/settings/circle/` management screen all exist.

**Settings drawer — built, but materially less complete than the prior snapshot claimed.** `SettingsDrawer.tsx` exists and is wired up, but only **5 of 12** rows are functional: Your Circles, Our Mission, Research, Hold+, Privacy Policy, Feedback, Share Hold, and Delete my data. **Notifications, Language, Connected Accounts, and Terms are explicit `ComingLaterRow` placeholders in the code itself** — tagged "Coming later" in the UI, not silently missing. **There is no Accessibility row and no Personalise row in the drawer at all** — the prior snapshot's claim of "reordered Settings drawer with new Accessibility, Personalise, and Language rows" does not match the current code; Language exists only as a "Coming later" stub, and Accessibility/Personalise as settings rows don't exist (a `PersonaliseAccordion.tsx` component exists, but it's part of the Conversations/Library reply flow, not a settings screen). **Target design confirmed 2026-08-12:** a single merged "Accessibility & Display" row/page, not separate Accessibility and Personalise rows — see `04-ux-content/04-navigation-architecture.md`, "Accessibility & Display page," for the full spec. Still not built.

**AI/infrastructure — built.** `worker/src/` (prompts.ts, index.ts, rateLimit.ts, safeguarding.ts) and the client-side AI services (draftService.ts, messageDraftService.ts, aiMemoryService.ts, aiProxyClient.ts) all exist, consistent with the AI-amend and safeguarding-classifier work documented elsewhere in this book.

**Phase 4 (AI drafting quality/personalisation polish) — not started.** Checked `worker/src/prompts.ts` and `draftService.ts` directly for the anti-AI-phrasing instruction and the 2–3-template style-reference injection logged as planned in `06-privacy-security/02-ai-boundaries.md` — neither exists in the current prompts or draft-generation code.

**Phase 6 (accessibility audit) — not run.** No audit artifacts, results, or dedicated accessibility-testing files found anywhere in the repository, consistent with `02-research/04-accessibility.md` correctly marking this as a planned, not-yet-run audit.

**Phase 7 (widget, moon-cycle overlay) — not started.** No widget-related directory, file, or dependency exists anywhere in the project (checked file names and `package.json`). No moon-cycle-overlay component or reference found either.

**Phase 8 (transition screen, Reconnect landing moment, citation markers) — partially built, matching what was already directly verified earlier this session:** the Transition and Reconnect-landing screens themselves exist and run the original (not the drafted-replacement) copy; no citation-marker mechanism or anchored Research page exists. See `04-ux-content/04-navigation-architecture.md`'s "Transition screen" section for the fuller detail — not re-verified again here, since it was checked directly against the same two files (`app/create/done.tsx`, `app/return/transition.tsx`) earlier in this session.

**Phase 9 (hold-book content updates) — this book itself is the evidence.** Substantial hold-book content work has happened this session and the ones before it; separately, none of what Phase 9 documents (research batch, shame-language elevation, content-depth guidance, safeguarding framework, etc.) implies anything was built in `hold-app` — book content and app code are tracked independently throughout this section.

**Phase 10 (Hold+ monetisation — IAP, paywall, Restore Purchases, receipt validation) — entirely unstarted, confirmed.** No IAP library (e.g. `react-native-iap`), StoreKit integration, receipt-validation code, or purchase-flow logic found anywhere in the codebase or `package.json`. `app/settings/hold-plus.tsx` exists only as the honest "not open for purchase yet" info screen already documented in `07-business/02-pricing-principles.md` — this remains a hard blocker for any paid App Store launch, exactly as the superseded snapshot flagged.
