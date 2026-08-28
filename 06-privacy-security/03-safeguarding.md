# Safeguarding

Hold is a communication-drafting tool, not a therapy app or a crisis service — but because it exists for people who are unwell, overwhelmed or isolated, free-text input can surface genuine risk disclosures. This file sets the current thinking; **the exact trigger logic and wording must be signed off by a solicitor and/or clinical safety consultant before launch** — see `08-decisions/04-open-questions.md`.

**Build status:** the detection pipeline itself (the check, the response UI, resource content, grounding prompt, Core Circle notify option) is built, but the actual detection content — the keyword/phrase list, and the Hold+ classifier's criteria — is a placeholder, explicitly marked as such in code, and hard-gated to never run outside local dev builds. Nothing safety-critical reaches TestFlight, beta testers, or production until the content below is actually reviewed.

## Why numbers alone aren't enough

The evidence points against a numbers-only approach:

- Wysa's global data found that when a crisis instance was confirmed, only 2.4% of people chose to call a helpline even when repeatedly encouraged to, while a personal safety plan — co-created with the user, containing personal contacts, reasons to live and grounding exercises — was the most-used intervention.
- A 2025 evaluation of 29 mental-health chatbot apps found 15.2% of high-harm-potential responses failed to surface a specific, valid 24/7 crisis resource, and over half failed to properly confirm whether the user was currently unsafe rather than just detecting risk language.

A phone number alone is a necessary legal/duty-of-care baseline, not the thing most likely to actually help someone in the moment.

## Proposed approach for Hold

Given Hold is a comms tool, not a clinical product, the safeguarding layer should be proportionate rather than a full clinical safety-planning system:

1. **Detection layer** runs on free-text input before it reaches the AI drafting step — a keyword/classifier check for self-harm, suicide or abuse language. Checked surfaces: Going Quiet's own-words box, Personalise's "Your reply," and Amend with AI's prompt box — all the user's own words. Deliberately not checked in this pass: the "What they sent" paste box (someone *else's* message) — a different problem (detecting risk in a third party's words, not the user's own), needing its own response flow and its own privacy consideration, tracked separately in `08-decisions/04-open-questions.md` rather than folded into this layer.
2. **Revised — non-blocking, not a hard stop.** If triggered, do not block or stop drafting: Hold's own evidence above shows the message being written is very often the real reaching-out-to-support behaviour the app exists to enable, and hard-blocking it would fight that. Instead, a **persistent banner** appears above the message box — crisis resources plus the Core Circle notify option (below) — while drafting stays available and the person can still write and send to their Circle. The banner isn't a one-time dismiss; it stays visible and reachable for the rest of that screen's session. **This non-blocking approach is itself a real safety judgment call, not settled UX** — flagged explicitly for the clinical/legal reviewer alongside the detection wording, not assumed correct.
3. **Show, at minimum:**
   - **Samaritans** — 116 123 (free, 24/7, any crisis)
   - **Shout** — text "SHOUT" to 85258 (free, 24/7 text-based, for people who can't or don't want to talk)
   - **999** for immediate danger to life
   - **111, option 2** for urgent mental health crisis (NHS)
4. **A lightweight safety-plan layer, not just numbers:** the numbers above, plus one grounding prompt, plus an option to notify someone from the user's Core Circle right now, delivered via the same persistent banner rather than a separate interstitial screen. This is a proportionate version of the safety-plan-intervention technique, not an attempt to replicate a full clinical tool.

## Two-tier detection: free vs. Hold+

Not one mechanism for everyone — a baseline-for-everyone-plus-enhanced-accuracy-for-subscribers model, never a paid-only safety net:

- **Free tier:** on-device keyword/phrase matching only. No network call, zero marginal cost per user, content never leaves the device for this check.
- **Hold+ tier:** the same on-device layer, *plus* a classifier check (Haiku-tier model, via the existing server-side proxy) as an additional, more accurate pass. Planning-estimate cost, not measured: roughly £0.0004–0.0005 per check at current Haiku 4.5 pricing ($1/$5 per million tokens) — stays in the tens-to-low-hundreds of pounds per year even at real scale, since cost scales with Hold+ subscriber count only.

**What tiering does and doesn't affect:** only detection accuracy. Whatever happens once something *is* flagged — resources shown, wording, the response flow above — is identical regardless of tier. Free users are never left with zero protection, and never see a lesser response once triggered.

**Future revisit, logged as an intention, not a decision:** once Hold+ subscriber revenue comfortably covers the classifier layer's unbounded per-user cost, reconsider extending it to the free tier too, so free users eventually get the same detection accuracy as paying ones. This is only ever about upgrading detection accuracy later — it does not mean the free-tier keyword baseline can launch at lower quality now on the assumption it'll be fixed later. The baseline has to be real and reviewed at launch regardless of revenue; only the *upgrade path* is revenue-gated.

**Precedent for a keyword-triggered crisis banner working in practice:** Google has run one on search results since 2010 (updated to 988 in 2022), with published RCT evidence it drives real hotline engagement — not a novel or unproven pattern.

**Why the real keyword/phrase list can't come from existing published guidance:** Samaritans and Crisis Text Line don't publish an operational detection keyword list — their public guidance covers safe media-reporting language (how journalists/creators should talk about suicide/self-harm), not what to detect in free text written by someone at risk. The actual list has to be developed directly with the clinical safety consultant, not derived or approximated from what's already public.

## Who to model against, and why Hold's bar is different

- **Wysa** — AI-led intake/triage; classifies every message into seven risk types (suicidal ideation, homicidal ideation, self-harm, domestic violence, substance use, eating disorders, abuse of vulnerable populations); "Guided Journeys" are structured, clinician-authored content the AI guides users through rather than improvising; partnered with the NHS.
- **Woebot** — originally a consumer CBT chatbot designed by clinical psychologists with peer-reviewed efficacy studies; shifted to enterprise-only in 2024, no longer available directly to individual consumers.

Both are closer to clinical/therapeutic tools than Hold is trying to be. Hold is a communication assistant for people who happen to often be unwell, not a mental health chatbot — so the safeguarding bar is lower than Wysa's, but not zero, given who is likely to use it.

## Finding a clinical reviewer — researched 2026-08-12

Progress on *who* to hire, not on the detection content itself:

- **Clinical Safety Officer (CSO)** is the formal UK role for this risk category, under the DCB0129/DCB0160 NHS clinical safety standards — typically a GMC/NMC/GPhC-registered healthcare professional with 5+ years' clinical practice and specific DCB0129/DCB0160 training (a recognised 2-day course exists). Whether DCB0129/DCB0160 is strictly mandatory for a purely consumer-facing app (as opposed to a supplier into NHS/health-and-care settings, where it's clearly required) is unconfirmed and worth checking directly — but going through an equivalent process voluntarily is a credible, defensible standard regardless of whether it's technically mandated. Formal DCB0129/DCB0160 applicability is a separate legal/regulatory question from the clinical-content review itself (see `06-privacy-security/05-safeguarding-logic-framework-DRAFT.md`, Section 7).
- **Clinical psychologist** is a separate, complementary role — can advise specifically on crisis-detection wording, tone and approach without formal CSO qualification. Treat as a potentially distinct second engagement, not interchangeable with the CSO.
- Practical routes to find either: UK consultancies specialising in DCB0129/DCB0160/DTAC/SaMD compliance, or freelance/contract CSOs (an established niche, findable via LinkedIn search terms like "Clinical Safety Officer freelance" or "DCB0129 consultant"). No verified cost data was found specific to this niche — general adjacent figures exist (legal ~£360–480/hr, psychology consultation ~£65–350, safeguarding consultancy ~£125/hr) but these are unverified estimates, not quotes; real pricing needs direct outreach.
- Worth asking prospective reviewers directly whether they have an existing generalised framework/methodology from prior work, to avoid reinventing the wheel — with the caveat that specific past-client deliverables may be confidential IP and not transferable, though a generalised methodology often is.

**Named leads, logged 2026-08-28:** `09-research/clinical-safety-reviewer-leads.md` has specific contacts gathered while researching Calm Harm — stem4's inboxes, Calm Harm's named CSO, the mHabitat/Digital Development Lab correction (mHabitat is a verified real example of who can do this work, not a standalone bookable vendor), and eight commercial CSO consultancies with no confirmed pricing. None contacted yet — a starting point for outreach, not a shortlist.

**A separate, related question — whether informal input from a personally-known clinician (Bethany's father, a GMC-registered GP) could substitute for this independent review — is answered no in `08-decisions/04-open-questions.md`, "Independence consideration for informal clinical input": credentials aren't the blocker, independence from the founder is.**

## No ready-made safeguarding list exists — confirmed 2026-08-12

Researched directly, not assumed: no public resource hands Hold a ready-made trigger-phrase list for its specific problem.

- **NICE guidance (NG225)** is clinical-practice guidance for practitioners, not app-development wording. Its most transferable, directly citable principle: risk should be explored collaboratively rather than through scoring/prediction tools, and scoring tools shouldn't be used to gate who receives support — directly supports Hold's existing non-blocking, resource-forward approach above, rather than any "risk score" mechanic.
- **StayingSafe.net** (NHS England co-funded) provides personal safety-plan templates and structure — the closest existing reusable *language/structure* found, oriented around helping a person build their own plan, consistent with Hold's philosophy of not imposing solutions.
- **Samaritans Online Excellence Programme / Industry Guidelines** is a real, credible programme: Samaritans advises platforms directly on effective policies, products, and moderation of self-harm/suicide content, provides specialist guidance, and helps test new safety features with people with lived experience — explicitly including emerging AI tools as a current focus area. Their flagship guidance was built with a named Expert Academic Advisory Panel, funded in partnership with the Department of Health and Social Care and major tech platforms (Facebook/Instagram, Google/YouTube, Pinterest, Twitter). Samaritans also offers a direct advisory service (Online Harms Advisory Service) including template content policies on request — exact current contact details weren't fully confirmed and should be pulled directly from samaritans.org before outreach.
- **Important limitation, not a reason to dismiss the above:** Samaritans' guidance is explicitly framed around platforms hosting user-generated content — social platforms, forums, public/visible content moderation. Hold's actual technical problem is different: private, one-to-one message *drafting*, not public content moderation. Their guidance is valuable context and credibility, and a good source of a reviewer referral, but not a direct source of reusable detection logic or phrase lists for Hold's specific use case.

**Conclusion: the category framework below and clinical/CSO engagement remain necessary — nothing found substitutes for that.**

## The provisional logic framework — draft awaiting clinical review

`06-privacy-security/05-safeguarding-logic-framework-DRAFT.md` is the current working draft: a category skeleton (seven provisional categories, A–G, covering direct intent, hopelessness/entrapment, farewell/finality language, method/means specificity, escalation/trajectory language, non-suicidal self-harm, and risk-to-others/abuse disclosures), provisional response tiers, and six consolidated questions for a clinical reviewer. Deliberately built **without** specific trigger phrases — an AI-drafted phrase list carries real risk (too narrow misses genuine risk; badly calibrated either causes alert fatigue or teaches evasion language) and needs to originate from clinical training, not pattern-matching. **Not clinically validated, not for production use** — a starting skeleton for a reviewer to react to, not a specification. See that file for the full detail, including the false-positive risk unique to Hold's own vocabulary (Category C and Section 6 of that document) — Hold's core function of helping people write "I need to step back" messages shares surface vocabulary with genuine crisis language in a way most other apps don't structurally have to deal with, flagged there as the single most important thing for clinical calibration.

## International crisis resources — researched 2026-08-12

**Framing:** Hold's crisis resources must be region-appropriate, not UK-only, once the app supports users outside the UK. Showing a UK number to a US or Australian user is a real safety gap, not a minor localisation detail — it could mean showing a number the person can't actually call or that connects them to the wrong country's service. This needs resolving before any wider-English-market launch, not treated as post-launch polish.

**Confirmed current numbers, corroborated across official/government sources (SAMHSA, FCC, Mental Health Commission of Canada, NHS, and others) — the "core six" markets:**

| Country | Primary crisis line | Notes |
|---|---|---|
| **UK** (England/Scotland/Wales) | Samaritans 116 123; NHS 111, option 2; 999 for immediate danger | Per "Proposed approach for Hold" above. Scotland/Wales use the same UK-wide Samaritans and 999; NHS 111 coverage specifics for Scotland (historically NHS 24 / 111 differently) and Wales (NHS 111 Wales) should be verified separately before assuming full option-2 parity — flagged as needing confirmation, not assumed. |
| **Ireland** | Samaritans 116 123 (freephone, 24/7, same number as UK); Aware 1800 80 48 48 (10am–10pm) | Samaritans operates across UK and Ireland under the same number, which simplifies things. |
| **USA** | 988 (Suicide & Crisis Lifeline) — call or text, 24/7 | Replaced the old 10-digit National Suicide Prevention Lifeline in July 2022. Well-established, actively growing in use, with published outcome data suggesting a genuine positive impact. Veterans can press 1 after dialling for the Veterans Crisis Lifeline. Crisis Text Line (text HOME to 741741) is a commonly cited secondary resource. |
| **Canada** | 988 (Suicide Crisis Helpline) — call or text, 24/7 | Launched November 2023, using the same 988 short code as the US but a separate national service. |
| **Australia** | Lifeline 13 11 14; Beyond Blue 1300 22 4636 | Both well-established, widely cited national services. |
| **New Zealand** | 1737 — free call or text, "Need to Talk?" | Also Lifeline NZ 0800 543 354 cited as a secondary resource. |

**Not yet researched to a reliable standard — flagged explicitly, not filled in speculatively:** South Africa, Singapore, Philippines, India, Caribbean English-speaking nations, and other English-speaking markets. An attempt was made to research these; results were genuinely too inconsistent to include with confidence — numbers cited from 2015–2016 news articles (Philippines), multiple conflicting regional/city-level helplines rather than one clear national number (India), and no usable results at all (South Africa). Singapore was the one exception with a consistently-cited, seemingly current number (Samaritans of Singapore / SOS — 1-767), but even this should be re-verified against an official source before shipping, not taken from this research alone.

**Recommendation:** treat the core six above as the reliable v1 set. Every other market needs its own dedicated research pass from official government/health-ministry sources (not general web search aggregation) at the point it's actually being scoped for a real launch, not filled in now.

**Verification discipline going forward:** crisis line numbers and services do change — the UK's own NHS 111 option 2 rollout completed only weeks before this document's most recent update, replacing numbers that had been correct for years. Whatever numbers ship in v1 should be re-verified close to each actual launch date, not treated as permanently fixed once entered.

## Region and language detection — decided

Location and language are confirmed on a **setup screen at onboarding**, pre-filled from App Store storefront country as a sensible default, with the user confirming — not silently assumed, and not asked reactively later. **Rationale:** this is deliberately done while the person is well, at initial setup, rather than surfaced for the first time at the moment a safeguarding screen actually triggers — consistent with the low-capacity design principle of not introducing new configuration decisions at someone's lowest-capacity moment. By the time it matters, it's already correctly set and forgotten about, with a manual override always available in Settings. No location permission or server-side storage involved — this stays a local, changeable-in-Settings preference throughout.

This also serves a secondary purpose: presenting language/region confirmation at setup signals international readiness from day one, supporting broader download appeal beyond a UK-only-feeling app, even before every region's resources are fully built out.

**Technical note for the pre-fill mechanism:** App Store storefront country can be read via StoreKit as the pre-fill default, though it has known accuracy issues on recent iOS versions — since this is a user-confirmed value rather than a silent one, that unreliability matters less (the user corrects it if wrong), but device locale (`Locale.current.regionCode`, more reliable, no permission needed) is worth weighing against storefront country as the pre-fill source.

**Build implication:** the crisis-resource screen needs to be **data-driven by region/locale**, not hardcoded UK text — an internal resource table keyed by country, surfaced based on the user's set region/locale, with a clear process for adding and verifying new countries' numbers before each new market launch. Scope as part of Phase 10 or a dedicated localisation phase, not bolted on ad hoc per country.

## Legal and clinical review

A placeholder detection list exists in code for pipeline-testing purposes only — see `hold-app`'s `src/services/safeguardingService.ts` (the on-device keyword/phrase list) and `worker/src/safeguarding.ts` (the Hold+ classifier's placeholder criteria). Both are explicitly marked as not clinically reviewed and are hard-gated to local dev builds only (never reaches TestFlight or production). This is what the clinical safety consultant needs to review and replace — the book intentionally does not duplicate the placeholder content itself here, only points to where it lives, so this document stays the policy source of truth rather than an implementation dump.

This sits on the existing outstanding legal/compliance list (see `hold-app-idea` project notes), not as a separate item:

- Treat the detection trigger logic and crisis-resource wording as part of the DPIA and legal review already flagged as outstanding — not just a copy/UX decision.
- A solicitor should review liability and duty-of-care framing (Hold is not medical/crisis advice).
- A clinical safety consultant (or equivalent) should sign off on the actual trigger logic, thresholds and wording — this should not be designed solely by an AI drafting tool or in a brainstorm.
