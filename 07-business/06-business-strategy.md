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

Hold isn't video- or media-heavy, so infrastructure costs should stay comparatively low relative to user count. AI drafting cost is the main variable to watch as usage scales — this is part of why Free-tier AI replies are capped rather than unlimited (see `02-pricing-principles.md`).

## Revenue scenarios

Illustrative only, not a forecast — net of Apple/Google commission (typically 15% under the small-business programme, 30% otherwise), before hosting/AI/support costs.

| Scenario | Paying users | Approx. monthly recurring revenue (gross) |
|---|---|---|
| Conservative | 100 | ~£250–330 |
| Modest early traction | 500 | ~£1,300–1,650 |
| Good first year | 1,000 | ~£2,600–3,300 |
| Strong | 2,000 | ~£5,200–6,600 |

Treat 100–300 paying users in the first year as a genuinely good outcome, not a disappointing one — it's real evidence people will pay for the problem Hold solves, and a much healthier bar to plan against than assuming thousands of subscribers early.

## Marketing approach

Education and trust-building before paid acquisition, not the other way round.

1. **Immediately:** secure app name, domain, social handles.
2. **1–2 weeks out:** landing page with email sign-up, logo, simple brand identity, "coming soon."
3. **3–4 weeks out:** regular content — why Hold exists, design decisions, accessibility choices, development stories (without identifying anyone), never framed as a hard sell.
4. **2 weeks before launch:** open a waitlist, invite beta testers from relevant communities.
5. **Launch week:** Product Hunt, LinkedIn, Instagram, Threads, relevant subreddits (where research/self-promotion rules permit), TikTok as an experiment.

If paid ads are used at all, start small (£150–300/month) to learn before scaling spend — don't lead with advertising budget.

**Positioning note:** market Hold as diagnosis-agnostic. Early adopters are likely to come from PMDD, ADHD, chronic illness and mental health communities because those groups often experience the underlying problem first-hand, but the product is for anyone whose capacity to communicate is temporarily reduced — burnout, grief, caring responsibilities, or general overwhelm included. Narrowing the brand to one diagnosis would undersell the actual addressable audience.

## IP and company structure

- **"Hold" as a name has a known UK trademark conflict** (Hold Platform Ltd, Malta-registered fintech, holds Class 9 software marks) — needs proper trademark clearance, or a rename, before committing further branding spend. Alternatives already explored: Vouch, Constant, Tend, Harbour, Amity.
- **Own everything through a company, not personally** — code, branding, trademark, domain, website. Makes things far cleaner if developers or investors get involved later.
- **Copyright exists automatically** on code, design, and copy as it's created — no UK registration needed.
- **A patent is not recommended.** Software patents are slow, expensive, and unlikely to protect the actual value here, which comes from brand, design judgement, trust and execution rather than a patentable mechanism.
- **Developer agreements** (if anyone else is ever brought on to build) should explicitly assign all created IP to the company.

## Revenue idea, now resolved: one-time export purchase

**Resolved:** two tiers, not one. Raw data export (a plain CSV/text list of quiet periods and durations) is free for everyone, always — charging for someone's own raw data would sit uncomfortably against data portability norms and wasn't worth the reputational risk for what it would add in revenue. The paid one-time purchase is specifically the **formatted GP/clinician PDF report** — quiet periods, durations, and pattern observations laid out and summarised — priced at **£3.99**, reflecting that it's the formatting and analysis work being sold, not the underlying data. Originally considered at £5.99–6.99 before this distinction was made explicit; £3.99 fits better now that what's being sold is clearly a service, not data access.

Captures revenue at the single highest-motivation moment a free user is likely to have (advocating for themselves medically) without forcing a subscription decision someone may only need once or twice a year.

## Revenue realism check

The ARR scenarios discussed earlier in this repository's history (roughly £5k conservative to £2M exceptional, depending on downloads and conversion) were reasoned before the free tier was this fully specified. Worth revisiting that lens now: the free tier turned out generous — unlimited History, unlimited templates, a shared monthly AI allowance, and now basic Patterns too — which is the right call for trust and word-of-mouth, but likely means a **lower conversion rate than a typical freemium app**, since fewer free users will hit a hard wall that forces the upgrade decision. Conversion is more likely to come from genuinely heavy users (frequent quiet periods, many Circles) and from specific high-value moments (the export feature above) than from volume caps doing the selling.

None of this changes the underlying case for the product — the problem is real, differentiated, and under-served by existing "wellness" or "productivity" framing — but the honest expectation should lean toward the conservative-to-modest end of the earlier scenarios unless and until real usage data says otherwise. Treat the ARR figures elsewhere in this repository as directional hypotheses, not commitments.

## Legal and compliance (cross-reference)

This overlaps with the outstanding legal work already tracked for Hold: privacy policy, GDPR/DPIA, terms of service (liability, not medical/crisis advice), data processing agreements, and — per `06-privacy-security/03-safeguarding.md` — solicitor and/or clinical safety consultant sign-off on the safeguarding trigger logic specifically. None of the business strategy above should proceed to real users ahead of that review.
