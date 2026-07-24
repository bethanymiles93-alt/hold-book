# Safeguarding

Hold is a communication-drafting tool, not a therapy app or a crisis service — but because it exists for people who are unwell, overwhelmed or isolated, free-text input can surface genuine risk disclosures. This file sets the current thinking; **the exact trigger logic and wording must be signed off by a solicitor and/or clinical safety consultant before launch** — see `08-decisions/04-open-questions.md`.

## Why numbers alone aren't enough

The evidence points against a numbers-only approach:

- Wysa's global data found that when a crisis instance was confirmed, only 2.4% of people chose to call a helpline even when repeatedly encouraged to, while a personal safety plan — co-created with the user, containing personal contacts, reasons to live and grounding exercises — was the most-used intervention.
- A 2025 evaluation of 29 mental-health chatbot apps found 15.2% of high-harm-potential responses failed to surface a specific, valid 24/7 crisis resource, and over half failed to properly confirm whether the user was currently unsafe rather than just detecting risk language.

A phone number alone is a necessary legal/duty-of-care baseline, not the thing most likely to actually help someone in the moment.

## Proposed approach for Hold

Given Hold is a comms tool, not a clinical product, the safeguarding layer should be proportionate rather than a full clinical safety-planning system:

1. **Detection layer** runs on free-text input before it reaches the AI drafting step — a keyword/classifier check for self-harm, suicide or abuse language.
2. **If triggered:** stop the drafting flow. Do not attempt to draft a "sensitive" message anyway. Do not have the app try to console or reason with the person — redirect to a human/service instead.
3. **Show, at minimum:**
   - **Samaritans** — 116 123 (free, 24/7, any crisis)
   - **Shout** — text "SHOUT" to 85258 (free, 24/7 text-based, for people who can't or don't want to talk)
   - **999** for immediate danger to life
   - **111, option 2** for urgent mental health crisis (NHS)
4. **A lightweight safety-plan layer, not just numbers:** the numbers above, plus one grounding prompt, plus an option to notify someone from the user's Core Circle right now. This is a proportionate version of the safety-plan-intervention technique, not an attempt to replicate a full clinical tool.

## Who to model against, and why Hold's bar is different

- **Wysa** — AI-led intake/triage; classifies every message into seven risk types (suicidal ideation, homicidal ideation, self-harm, domestic violence, substance use, eating disorders, abuse of vulnerable populations); "Guided Journeys" are structured, clinician-authored content the AI guides users through rather than improvising; partnered with the NHS.
- **Woebot** — originally a consumer CBT chatbot designed by clinical psychologists with peer-reviewed efficacy studies; shifted to enterprise-only in 2024, no longer available directly to individual consumers.

Both are closer to clinical/therapeutic tools than Hold is trying to be. Hold is a communication assistant for people who happen to often be unwell, not a mental health chatbot — so the safeguarding bar is lower than Wysa's, but not zero, given who is likely to use it.

## Legal and clinical review

This sits on the existing outstanding legal/compliance list (see `hold-app-idea` project notes), not as a separate item:

- Treat the detection trigger logic and crisis-resource wording as part of the DPIA and legal review already flagged as outstanding — not just a copy/UX decision.
- A solicitor should review liability and duty-of-care framing (Hold is not medical/crisis advice).
- A clinical safety consultant (or equivalent) should sign off on the actual trigger logic, thresholds and wording — this should not be designed solely by an AI drafting tool or in a brainstorm.
