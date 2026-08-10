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

## Legal and clinical review

A placeholder detection list exists in code for pipeline-testing purposes only — see `hold-app`'s `src/services/safeguardingService.ts` (the on-device keyword/phrase list) and `worker/src/safeguarding.ts` (the Hold+ classifier's placeholder criteria). Both are explicitly marked as not clinically reviewed and are hard-gated to local dev builds only (never reaches TestFlight or production). This is what the clinical safety consultant needs to review and replace — the book intentionally does not duplicate the placeholder content itself here, only points to where it lives, so this document stays the policy source of truth rather than an implementation dump.

This sits on the existing outstanding legal/compliance list (see `hold-app-idea` project notes), not as a separate item:

- Treat the detection trigger logic and crisis-resource wording as part of the DPIA and legal review already flagged as outstanding — not just a copy/UX decision.
- A solicitor should review liability and duty-of-care framing (Hold is not medical/crisis advice).
- A clinical safety consultant (or equivalent) should sign off on the actual trigger logic, thresholds and wording — this should not be designed solely by an AI drafting tool or in a brainstorm.
