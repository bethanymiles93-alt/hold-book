# EU AI Act and remaining compliance research

Background research only. Genuinely significant items in here need solicitor input and are explicitly not resolved by this document — flagged as such throughout, not treated as settled.

## A. EU AI Act

**Genuinely significant — needs solicitor input, not resolved here.**

Hold's safeguarding classifier (the Haiku-tier model used for crisis/self-harm risk detection on Hold+, see `06-privacy-security/03-safeguarding.md`) sits in a domain explicitly named as a concern under the AI Act's Annex III (health/safety-related high-risk AI systems) — crisis/risk detection is a commonly cited high-risk-relevant use case under current guidance on the Act.

**Real obligations if classified high-risk:** a documented risk management system, human oversight mechanisms, logging/audit trails, and technical documentation. This would be a genuine, non-trivial compliance programme, not a checkbox.

**Mitigating factors — reasons for cautious optimism, not certainty:**
- Text-based sentiment/crisis analysis is not automatically caught by the Act's "emotion recognition" high-risk category specifically, because that category is defined around **biometric data** — Hold's classifier works on typed text, not biometric signals, so this particular high-risk trigger likely doesn't apply as written.
- **Article 6(3)** offers an exemption path for Annex III systems that don't pose a "significant risk of harm," provided the provider completes and documents a formal assessment reaching that conclusion. This is plausibly relevant to Hold: the classifier feeds a supportive, non-blocking banner (crisis resources, a grounding prompt, an option to notify a Core Circle contact) rather than any clinical decision, diagnosis, or gatekeeping action — this is the same distinction already built into Hold's public-copy rules (`04-ux-content/02-voice-and-language.md`, "Public claims/copy rule: communication framing, not treatment framing," 2026-08-27): Hold assists communication, it does not treat. That existing framing discipline directly supports (though does not by itself prove) an Article 6(3) argument.
- **Regulatory runway:** high-risk obligations, even where applicable, don't take effect until **2 December 2027** (delayed from the originally planned August 2026 date). This is not an immediate launch blocker for an MVP shipping well before that date — but it is real work that needs doing before that date, not something to forget about because it isn't urgent today.

**Immediate, low-effort action required regardless of the high-risk question:** the AI Act's **Article 50 transparency requirement** has applied to *all* AI systems, high-risk or not, since **August 2025** — users must be clearly informed when they are interacting with AI. This is unrelated to the harder high-risk classification question and shouldn't wait for it to be resolved. **Action:** add a near-term build item — a simple, clear in-app disclosure that AI is used for (a) message drafting assistance and (b) safeguarding detection — logged in `08-decisions/04-open-questions.md`.

## B. US state app-store age-verification laws

Texas, Utah, Louisiana, California, and Alabama (the last from 2027) have each passed or proposed laws requiring app stores to verify user age and pass age signals to developers. This landscape is real, active, and **legally unsettled** — Texas's law is currently under a court injunction/active legal challenge, so its eventual shape isn't fixed yet.

**Practically important distinction:** the technical burden of these laws sits primarily with **Apple and Google** (building and operating the age-signal APIs), not with individual developers building age verification from scratch. Hold's role, if these laws stabilise into real platform APIs, would be to integrate with and respond to the age signal the platform provides — not to build its own age-verification infrastructure.

This **reinforces, rather than conflicts with**, the Hold+ age-check-plus-parental-consent flow already scoped in Part B of `09-research/global-architecture-scan-pass1.md` — same underlying mechanism (ask/receive an age signal at a specific point, respond with a lighter or heavier consent flow depending on the answer), different legal trigger (EU digital-consent-age variance there, US state app-store law here).

**Status: monitor, don't build yet.** The landscape is actively shifting (active litigation, laws not yet in force in most states). Re-check platform API availability closer to actual build time rather than building against today's unsettled picture.

## C. UK Online Safety Act (OSA)

**A genuine open question for the solicitor — now precisely scoped, not previously captured anywhere in this book.**

The OSA exempts services where the *only* user-generated content is email, SMS, MMS, or one-to-one live voice calls — but it does **not** broadly exempt app-based messaging services in general. Official guidance explicitly names WhatsApp as clearly in-scope, despite being a private messaging app — "it's private messaging" is not, on its own, an exemption.

**The determining question for Hold is not "is this private messaging"** (that alone doesn't settle it, per WhatsApp's own in-scope status) — **it's whether Hold itself hosts or facilitates the exchange of content between users, versus purely drafting content that is then handed off to an external channel** (SMS, WhatsApp, email) which does the actual hosting/transmission between the two people.

**Specific feature to flag for the solicitor:** the Reconnect Conversations reply flow, where a friend's message — received via an external channel (SMS/WhatsApp/email), then manually copy-pasted in by the user — is used as context to help draft a reply. This is meaningfully different in kind from a service that itself routes messages between two of its own users on its own infrastructure: Hold never receives, stores as a routed message, or transmits the friend's message to anyone; the user pastes it in themselves, and Hold hands the drafted reply back to the user to send through an external channel it doesn't control. Whether this distinction is sufficient to place Hold outside OSA scope is exactly the question to put to the solicitor — not assumed either way here.

**Action:** this is a new, precisely-scoped open question — add it to `08-decisions/04-open-questions.md` (no pre-existing OSA entry was found in that file to update in place, despite the framing of "update the existing entry" — flagged explicitly rather than silently treated as already covered).

## D. Encryption / export controls

**Lower priority — brief note only, not deep-researched.**

Hold does not build its own encrypted transport layer. It hands drafted content off to existing channels (SMS, WhatsApp, email), each of which already has its own encryption (or lack thereof) entirely outside Hold's control. Export-control classifications that apply to companies building their own cryptographic protocols are unlikely to apply to Hold on this basis, since Hold builds no cryptography of its own.

**Flag as "low risk, not deep-researched"** rather than "confirmed clear" — this hasn't had the same research rigour as the items above. Revisit properly only if Hold ever builds its own encrypted transport layer (e.g. a first-party messaging channel rather than handing off to SMS/WhatsApp/email) — not a near-term scenario per the current architecture.

## E. Global picture: AI-specific law

As of mid-2026, only the **EU and South Korea** have comprehensive, binding AI-specific statutes in force. South Korea's AI Framework Act took effect **22 January 2026**. Log this as a distinct future check if Hold ever actively serves South Korea as a market — not relevant to current scope, but worth not forgetting.

Everywhere else in Hold's realistic target markets — UK, Australia, Singapore, Japan, Canada, US — governs AI through existing sector regulators, general privacy law, or voluntary/non-binding frameworks, not a dedicated AI statute. China has a narrower, differently-shaped stack (content-labelling rules, algorithmic-recommendation regulation) that is not relevant unless China becomes an active target market (which would also trigger the hard-data-localization finding in `09-research/global-architecture-scan-pass1.md`, Part E).

**Conclusion:** the already-queued EU AI Act question (Part A above) is **the single most significant AI-specific regulatory question globally** for Hold right now, not one item among several roughly-equivalent regimes to track in parallel.

## F. Global picture: online safety law

Broader than initially scoped when the UK OSA question alone was raised. Real, dedicated online-safety laws exist in:
- **EU** — the Digital Services Act (DSA), plus national supplementary laws in Germany, France, Italy, Spain, and Ireland.
- **UK** — the Online Safety Act (Part C above).
- **Australia** — its own Online Safety Act.
- **Singapore** — the Online Safety (Miscellaneous Amendments) Act.
- **UAE** — the Child Digital Safety Law.
- **Thailand, Indonesia, South Africa** — each using their own adapted regulatory approaches, not identical frameworks but addressing similar ground.

The **US has no federal equivalent yet** — the Kids Online Safety Act (KOSA) passed the Senate but has not become law.

**Important pattern, not yet solicitor-confirmed:** every framework listed above shares the same underlying organising concept — whether a service **hosts or facilitates user-to-user content exchange**, versus merely acting on content that arrives from, and is sent back out to, external channels the service doesn't control. This strongly suggests that the precise question already flagged for the UK solicitor in Part C (the Reconnect Conversations hosting-vs-drafting distinction) is likely **the same determining question** across the EU, Australian, Singaporean, and UAE frameworks too — not four independent legal analyses each starting from scratch.

**Explicit instruction for the solicitor conversation:** ask directly whether the same architectural answer (Hold doesn't host or route messages between users; it drafts content the user themselves sends via external channels) transfers cleanly across these jurisdictions, or whether any of them define "hosting" or "facilitating" narrowly/broadly enough to require separate treatment. Don't assume transferability without asking — the pattern is suggestive, not confirmed.

## Final consolidated list — items requiring solicitor input, in priority order

1. **EU AI Act** — high-risk classification question for the safeguarding classifier (Part A above).
2. **Online Safety Act / DSA-equivalent scope**, re: the Reconnect Conversations mechanism — likely a shared analysis across UK, EU, Australia, Singapore, and UAE rather than four+ separate questions (Parts C and F above).
3. **GDPR Article 27** — EU representative requirement (`09-research/global-architecture-scan-pass1.md`, Part C).
4. **Medical device classification** (MHRA) — already queued from earlier work, see `04-ux-content/02-voice-and-language.md`, "Public claims/copy rule: communication framing, not treatment framing" (2026-08-27).

**Everything else surfaced across this whole research thread** — data localization, the AADC/Children's Code assessment, the EAA, US app-store age-verification laws, app-category restrictions — is confirmed either a non-issue for Hold's current architecture, confirmed low-cost business-setup work (not a code change), or a scoped-but-not-yet-built spec item already logged in its proper place (the EU digital-consent-age flow in `09-research/global-architecture-scan-pass1.md`, Part B, being the clearest example).
