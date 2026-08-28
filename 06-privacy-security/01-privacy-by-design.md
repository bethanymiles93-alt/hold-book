# Privacy by design

This is a foundational requirement. Obtain specialist legal advice before launch.

## Why Hold requires particular care

Message drafts, relationship labels, contact data and reasons for reduced capacity may reveal sensitive and intimate information. Free text may contain health information even when Hold does not ask for it.

## Plain-language summary

Hold remembers: who you chose to message, where you are in your journey, your templates, and your completion status in Conversations. It does not read WhatsApp, texts or emails — the only exception is the optional Email out-of-office toggle, which uses official APIs the user explicitly connects, not general inbox reading. This is the plain-language version of the more detailed principles below; both should stay consistent.

## Principles

- Define each purpose before collecting data.
- Collect the minimum data needed.
- Prefer on-device processing and storage where practical.
- Do not upload a full address book by default.
- Separate identifiers from content where possible.
- Encrypt data in transit and at rest.
- Set retention periods.
- Make deletion real and understandable.
- Do not use message content for advertising.
- Do not train models on private content without specific informed agreement.
- Complete a DPIA where processing is likely to create high risk.
- Maintain a record of processors and data flows.

## Age Appropriate Design Code

Hold applies the ICO's Age Appropriate Design Code (Children's Code) principles to all users, rather than age-gating (see `08-decisions/01-decision-log.md`, 2026-08-27). A full standard-by-standard working assessment lives in `06-aadc-compliance-review.md` — internal working assessment, pending solicitor review.

## International and jurisdictional scope

Beyond the UK/AADC assessment above, `09-research/global-architecture-scan-pass1.md` (data localization, EU consent-age variance, GDPR Article 27, UAE PDPL, EAA) and `09-research/international-data-protection-applicability.md` (India/Singapore/Nigeria small-footprint exemption research) and `09-research/ai-act-and-remaining-compliance.md` (EU AI Act, US app-store age-verification laws, UK Online Safety Act, global online-safety and AI-law landscape) cover the wider compliance surface Hold's international reach creates. All three are working research, not solicitor sign-off.

## Sources

- ICO, Data protection by design and by default: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/guide-to-accountability-and-governance/data-protection-by-design-and-by-default/
- ICO, Data minimisation: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-protection-principles/a-guide-to-the-data-protection-principles/data-minimisation/
