# ICO Age Appropriate Design Code (AADC / Children's Code) — compliance review

**Status: internal working assessment, pending solicitor review. Not formal legal sign-off — do not treat this document alone as proof of compliance.**

## Scope and approach

**Resolved 2026-08-28** (correcting this document's earlier framing, which described the minimum age as an open gap — closed, see `08-decisions/01-decision-log.md`, 2026-08-27, and `08-decisions/04-open-questions.md`'s now-closed "Hold's minimum age is currently undefined" entry): Hold will not set a minimum age or age gate. No minimum age, universal highest-protection standard applied instead of age verification. This is settled policy, not an open question — the rest of this document should be read against that settled position throughout, particularly Standards 3 and 6 below.

This is not an improvised workaround — it is the ICO's own recognised alternative to age assurance. The Code's Standard 3 (Age appropriate application) requires a service to either establish user age with a level of certainty proportionate to risk, *or* apply the Code's full standard of protection to all users without distinguishing by age. Hold has deliberately chosen the second route. That choice only actually satisfies Standard 3, however, if the other fourteen standards are genuinely met at the "child" protection level for everyone — which is what the rest of this document checks, standard by standard.

For each standard below: **Likely already met** (existing feature/decision that satisfies it), **Needs light confirmation/documentation** (no build change, but something to confirm or write down before this can be called done), **Not applicable** (with why), or **Genuinely uncertain** (flagged rather than guessed at).

## The 15 standards

### 1. Best interests of the child

**Likely already met.** Hold has no children's-product-specific "best interests" test, but the README's "Hold Test" (a feature must reduce guilt/emotional effort, preserve or repair connection, increase trust, preserve user choice, work at very low capacity, collect only genuinely necessary data, be explicable in plain language, and survive having engagement metrics removed) functions as a best-interests gate applied to *every* user, not a lesser bar for children specifically. Supporting decisions: no diagnosis requirement (`01-foundation/01-mission-and-vision.md`, `01-foundation/04-founder-insights.md`), no guilt-inducing patterns anywhere in the product (`08-decisions/02-ideas-not-to-build.md`), and the explicit "adult-only scope boundary" note (`08-decisions/04-open-questions.md`, 2026-08-11) which at least records that a youth/family variant was deliberately not built rather than overlooked.

### 2. Data protection impact assessments (DPIAs)

**Needs light confirmation/documentation — but flag that a real DPIA, not just this document, is the actual deliverable.** `06-privacy-security/01-privacy-by-design.md` already states the principle ("Complete a DPIA where processing is likely to create high risk"), and a DPIA is already logged as outstanding in `06-privacy-security/03-safeguarding.md`'s "Legal and clinical review" section (tied to the safeguarding detection layer specifically). No DPIA has actually been completed yet. **What needs confirming:** when that DPIA is done, it needs to explicitly cover the Children's Code angle — i.e. that Hold processes free-text data capable of revealing sensitive information, from a user base that may include under-18s, without age verification — not just the safeguarding-trigger content it was originally scoped around.

### 3. Age appropriate application

**Resolved — likely already met, via the chosen alternative route.** The no-minimum-age decision (see "Scope and approach" above) is settled, not provisional: Hold applies Code-level protection to all users rather than running age assurance, which is the ICO-sanctioned alternative for this standard. This status remains conditional on the other fourteen standards actually holding for everyone, not just asserted.

### 4. Transparency

**Needs light confirmation/documentation.** Hold's voice principles already favour short, plain, non-clinical language everywhere (`04-ux-content/02-voice-and-language.md`), and a plain-language privacy summary line was added to `06-privacy-security/01-privacy-by-design.md` (`08-decisions/01-decision-log.md`, 2026-07, row 41: "Hold doesn't read WhatsApp, texts or emails..."). This is a good starting register for "concise, prominent, and in clear language suited to the age of the child." **What needs confirming:** the actual Privacy Policy and Terms of Use documents don't appear to be drafted as customer-facing text anywhere in this book yet — only the underlying principles are. When drafted with the solicitor, they should be checked against a "would a child understand this" bar specifically, not just against general plain-English practice, and should exist as an actually-simple version, not only a legally-complete one.

### 5. Detrimental use of data

**Likely already met.** No behavioural advertising or use of message content for advertising (`06-privacy-security/01-privacy-by-design.md`). No engagement-maximising manipulation: no streaks, no badges/counts, no re-engagement notifications, no habit-loop notification pattern (explicitly rejected, `08-decisions/02-ideas-not-to-build.md`), no AI-inferred mood/health labelling, no congrats/praise for basic communication (rejected on guilt-spiral grounds, `01-decision-log.md`, 2026-08-19). This is one of the strongest matches in the whole review — detrimental engagement patterns are already a named category of things Hold refuses to build, for reasons that predate this review.

### 6. Policies and community standards

**Resolved — likely already met.** Previously flagged as blocked on the undefined minimum age; that gap is now closed (see "Scope and approach" above and `08-decisions/01-decision-log.md`, 2026-08-27). There is no minimum age to fail to uphold, and no age gate whose enforcement could drift out of sync with published policy — the settled position (no age floor, Code-level protection applied to everyone) is itself simple to state consistently in the Terms of Use once drafted. Hold also has no user-generated public content or community feed (explicitly rejected, `08-decisions/02-ideas-not-to-build.md`), so the moderation-of-community-content half of this standard was always moot. **One remaining light task:** once Terms of Use are drafted with the solicitor, confirm the "no minimum age" position is stated there in the same plain terms as here, so published policy and actual behaviour match from day one rather than needing reconciliation later.

### 7. Default settings

**Likely already met.** On-device-only storage by default, no account required for the core app, no data upload by default (`06-privacy-security/01-privacy-by-design.md`), optional backup/sync is opt-in and now free-tier but still off by default, AI-assisted drafting is Hold+-gated and never runs without the user invoking it, and the safeguarding banner/resources appear regardless of tier or settings. This is close to as "high privacy by default" as a consumer app gets without breaking its own core function.

### 8. Data minimisation

**Likely already met.** No full address-book upload by default (`06-privacy-security/01-privacy-by-design.md`); Patterns explicitly records only timing/duration/frequency and optional user-added tags, and is a hard privacy boundary against ever measuring message count, conversation length, or content (`01-decision-log.md`, 2026-07); AI boundaries explicitly forbid inferring relationship facts, sender identity, or health/mood the user hasn't stated (`06-privacy-security/02-ai-boundaries.md`; `08-decisions/02-ideas-not-to-build.md`, "AI-inferred sender guessing," "AI-inferred health/mood labelling").

### 9. Data sharing

**Needs light confirmation/documentation.** No evidence anywhere in this book of third-party data sharing, ad-tech integration, or data-broker use — consistent with the whole privacy-by-design posture. **What needs confirming:** `06-privacy-security/01-privacy-by-design.md` states the principle "Maintain a record of processors and data flows," but no such record actually exists yet as a document. This should be a short, factual list — Cloudflare Workers (AI proxy hosting), Anthropic (drafting/classifier API), Apple/Google (Sign in with Apple/Google, App Store/Play billing, push notifications) — not a new privacy control, just writing down what already exists.

### 10. Geolocation

**Not applicable, in the sense the standard targets device location tracking (GPS/precise location) — Hold has none.** The region/language setup screen (`06-privacy-security/03-safeguarding.md`, "Region and language detection") deliberately avoids this: it uses App Store storefront country or device locale as a *pre-filled, user-confirmed* default, explicitly "no location permission or server-side storage involved," changeable in Settings at any time. Worth keeping this distinction available for a reviewer, since it sits close enough to geolocation to be worth explicitly ruling out rather than silently assuming.

### 11. Parental controls

**Not applicable.** This standard governs services *that provide* parental monitoring tools — it obliges transparency about monitoring where such a feature exists, it doesn't require building one. Hold has no parental-control or child-monitoring feature, and is designed for adults managing their own communication capacity (`08-decisions/04-open-questions.md`, "Adult-only scope boundary — youth/family variant out of scope, not forgotten"). **One thing flagged for the solicitor rather than assumed:** the proposed future Trusted Contact concept (`08-decisions/04-open-questions.md`, scoped in `01-decision-log.md`) is opt-in *self*-disclosure by the account holder to someone they choose, not a parent-of-a-minor monitoring feature — structurally different from what Standard 11 addresses — but worth a specific confirmation from a reviewer if and when it's ever built, rather than assumed clear by analogy alone.

### 12. Profiling

**Likely already met.** No profiling of the user for third-party purposes exists or is planned. Patterns is user-facing self-observation, not covert profiling, and explicitly never infers a health/mood label the user hasn't stated (`08-decisions/02-ideas-not-to-build.md`). The one feature with any profiling-adjacent shape — AI memory (Hold+, `06-privacy-security/02-ai-boundaries.md`) — is opt-in, off by default, both-layers-must-consent, and explicitly barred from capturing psychological/emotional state, which is consistent with this standard's "off by default unless a compelling, child's-best-interest reason" test, not just a nearby analogy.

### 13. Nudge techniques

**Likely already met.** This is one of the most extensively pre-documented standards in the whole review, because Hold's own philosophy already independently arrived at most of it: no forced upsell blocking the core journey, no blurred/locked Hold+ previews (rejected specifically for reading as "you can't see your own data," `08-decisions/02-ideas-not-to-build.md`), a one-tap pause-subscription option, permission-over-pressure as a stated voice principle throughout (`04-ux-content/02-voice-and-language.md`), and no essential safety or accessibility feature ever paywalled (`07-business/02-pricing-principles.md`).

### 14. Connected toys and devices (IoT)

**Not applicable.** Hold is a phone app, not a toy or IoT device — nothing in the product touches this standard.

### 15. Online tools (data rights)

**Needs light confirmation/documentation.** "Delete my data" already exists and genuinely wipes content (Circles, History, templates, drafts, reply/AI state — `08-decisions/04-open-questions.md`, "Reset app" as a distinct action"). A form of data export already exists and is referenced as free even on the free tier (`08-decisions/02-ideas-not-to-build.md`, "Hold+ free trial" row references "free raw data export"). **What needs confirming:** that these tools are surfaced somewhere genuinely easy to find (not buried several taps deep) and easy to use without contacting support, and that rectification/objection are covered honestly — most of this is arguably moot by design, since almost all data lives on-device under direct user control and nothing server-side happens without an explicit user action (backup, AI drafting), but this should be stated plainly to a reviewer rather than assumed self-evidently fine.

## Summary

| # | Standard | Assessment |
|---|---|---|
| 1 | Best interests of the child | Likely already met |
| 2 | Data protection impact assessments | Needs confirmation — real DPIA still outstanding |
| 3 | Age appropriate application | Likely already met (via all-users route) |
| 4 | Transparency | Needs confirmation — Privacy Policy/Terms not yet drafted |
| 5 | Detrimental use of data | Likely already met |
| 6 | Policies and community standards | Likely already met (resolved 2026-08-28, was tied to now-closed minimum-age question) |
| 7 | Default settings | Likely already met |
| 8 | Data minimisation | Likely already met |
| 9 | Data sharing | Needs confirmation — no written processor/data-flow record yet |
| 10 | Geolocation | Not applicable |
| 11 | Parental controls | Not applicable (one edge case flagged re: future Trusted Contact) |
| 12 | Profiling | Likely already met |
| 13 | Nudge techniques | Likely already met |
| 14 | Connected toys and devices | Not applicable |
| 15 | Online tools (data rights) | Needs confirmation — findability/usability of existing tools |

Eight of fifteen standards already have a genuine existing architectural answer, not a promise to build one (corrected count, 2026-08-28 — this line previously said "eight" while the table only supported seven; Standard 6's resolution above is what makes eight now accurate). The remaining four "needs confirmation" items are documentation and drafting tasks (DPIA, Privacy Policy/Terms, processor record, data-rights tool findability), not product rebuilds — consistent with the framing note in `08-decisions/04-open-questions.md` that this groundwork is cheap now and expensive later.

## What this document does not do

This is a working assessment against publicly available ICO guidance, cross-checked across the ICO's own site and independent summaries where the ICO's site itself could not be directly retrieved. It is not a substitute for a solicitor's review, does not constitute legal advice, and does not itself complete the DPIA or Privacy Policy/Terms drafting it recommends. Treat every "likely already met" above as a strong starting position for that review, not a closed item.

## Sources

- ICO, Age appropriate design: a code of practice for online services — https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/age-appropriate-design-a-code-of-practice-for-online-services/
- ICO, FAQs on the 15 standards of the Children's code — https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/faqs-on-the-15-standards-of-the-children-s-code/
- ICO, Age Assurance guidance — https://ico.org.uk/for-organisations/advice-and-services/audits/data-protection-audit-framework/toolkits/age-appropriate-design/age-assurance/
- Independent cross-check of the 15-standard list: Evalian, "The ICO's Age-Appropriate Design Code (Children's Code)" — https://evalian.co.uk/childrens-code/; Ondato, "UK's Age Appropriate Design Code (Children's Code): Full Compliance Guide" — https://ondato.com/blog/uk-age-appropriate-design-code/
