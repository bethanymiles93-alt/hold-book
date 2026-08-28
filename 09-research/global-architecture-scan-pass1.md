# Global architecture scan — pass 1

## Purpose and scope

A narrow, architecture-focused scan — specifically checking for anything that would force a **build change** if discovered post-launch, as distinct from paperwork/policy work that can happen market-by-market later without touching the app itself. Core scope: UK, EU/Ireland, US, Canada, Australia, NZ ("Tier 1"), plus UAE. Part E extends specifically to hard data localization worldwide, since that is the one category of finding that would force infrastructure changes if missed.

This file complements, not duplicates, `09-research/international-data-protection-applicability.md` (small-footprint exemption research for India/Singapore/Nigeria) and `06-privacy-security/06-aadc-compliance-review.md` (UK-specific Children's Code assessment).

## A. Data localization — confirmed no issue for Tier 1 + UAE

**Confirmed no issue** for UK, EU, US, Canada, Australia, NZ, UAE. Hard data localization (a legal requirement that certain data physically stay within a country's borders) does not apply to Hold's data category — general personal data from a consumer communication-support app — in any of these jurisdictions.

Two narrower, sector-specific localization rules were found and confirmed **not applicable**:
- **UAE** has localization requirements for specific regulated sectors (finance, government), not general consumer apps.
- **Canada (Ontario, PHIPA)** has localization-adjacent rules for regulated health-information custodians specifically — Hold is not a health-information custodian and does not fall under PHIPA's scope.

**Architecture implication:** the current single-region (EU/UK) Supabase architecture remains sound for all of Tier 1 plus UAE. No multi-region data residency build is required to serve these markets.

## B. GDPR/EU digital consent age variance — real architecture item, scoped

**This is a genuine build item, not just paperwork** — flagged as distinct from the localization finding above.

EU member states are each permitted under GDPR Article 8 to set their own "digital age of consent" for a child to agree to information-society-service data processing without parental consent, and they don't agree with each other: UK sets 13, Austria sets 14, Germany/Netherlands/several others set 16, and it varies further across the rest of the EU. This is specifically relevant to **Hold+, not the free tier** — the free tier collects no identifiable PII, so this consent-age question doesn't bite there. Hold+ does process identifiable data (name/email) via Sign in with Apple/Google, which is what triggers the question.

**Proposed mechanism** (standard practice for this risk tier, sometimes called "GDPR-K" compliance — e.g. the approach toolkits like SuperAwesome's are built around): at Hold+ sign-up, ask the user's age. If they're under the relevant regional digital-consent threshold for their country, redirect to a lightweight parental/guardian consent step — a parent/guardian email address, a tick-box confirmation, and an emailed confirmation link they must click. This is a proportionate response for this data-sensitivity level (name/email via an existing auth provider, not health records or precise location) — it does not need the heaviest verification tier (e.g. credit-card check, ID upload).

**Explicitly not a free-tier change.** This stays scoped to the Hold+ sign-up moment only — no hard age-gate is added to the free tier, consistent with Hold's no-minimum-age decision (`08-decisions/01-decision-log.md`, 2026-08-27; `06-privacy-security/06-aadc-compliance-review.md`). The two are compatible: applying the Children's Code's protections to everyone doesn't require verifying anyone's age, but *this* EU consent-age rule specifically requires an age question at the one point real identifiable data changes hands (Hold+ sign-up) — a narrower, EU-law-specific trigger, not a reversal of the broader no-age-gate decision.

**Status: spec-complete at concept level, not build-ready yet.** Still needed before this goes into a build: exact sign-up-flow copy, a per-country consent-age threshold table, and the parental-consent email template. Treat as the next spec pass on this item, not something to start coding from this document alone.

## C. GDPR Article 27 — EU representative requirement

Hold (a UK-based company) will need to designate a representative established in an EU member state before actively serving EU users on an ongoing basis. This follows from the UK's status as a "third country" under EU GDPR since Brexit — Article 27 requires non-EU/EEA controllers processing EU residents' data at scale to appoint an in-EU representative who can be contacted by EU data subjects and regulators.

**This is a business/legal setup task, not a code change.** Commercial EU-representative services exist specifically for this purpose (a paid, ongoing service, not a one-off registration). Flag for a direct solicitor conversation and add to the business-setup checklist alongside the other outstanding legal/compliance items already tracked (`07-business/06-business-strategy.md`, "Legal and compliance").

## D. UAE PDPL

The UAE's Personal Data Protection Law (PDPL) is GDPR-structured and extraterritorial in the same broad style as the EU's own law. No hard data localization applies to Hold's data category (see Part A above). **One real, distinct requirement found:** UAE consumer-facing content should carry an Arabic-language disclosure. This is a translation/content task for a future UAE-specific localisation pass, not an urgent MVP requirement — flagged so it isn't lost, not because it blocks anything now.

## E. Global hard data localization scan (worldwide)

Full individual research of all ~195 countries is neither practical nor meaningful — the large majority have no comprehensive data protection law at all, and a country-by-country pass would mostly produce "no finding" entries. Instead, this scan cross-checked multiple current global trackers (DLA Piper's Data Protection Laws of the World, Recording Law, and others) for consistency on one specific, binary question: **which countries impose hard data localization** (a legal requirement to store certain categories of data on servers physically within that country) that would force a dedicated infrastructure build if Hold ever actively served that market.

**Countries with hard localization requirements that would force a build/infrastructure change:** China, Russia, Vietnam, Saudi Arabia, Kazakhstan.

**Everywhere else** — roughly 180+ countries, including every Tier 1 market, UAE, India, Singapore, Nigeria, Brazil, South Korea, Japan, Indonesia, Thailand, Malaysia, and the rest of the countries with comprehensive data protection statutes — has either no comprehensive data protection law at all, or a GDPR-style cross-border-transfer regime (adequacy decisions, standard contractual clauses, and similar mechanisms) rather than hard in-country storage. Hold's existing single-region architecture already accommodates transfer-regime compliance; it does not accommodate hard localization.

**Conclusion:** "build the architecture once, expand legal/policy compliance market-by-market later" is sound as a global strategy, with one explicit, named exception — China, Russia, Vietnam, Saudi Arabia, and Kazakhstan would each require dedicated, separate in-country infrastructure if Hold ever actively pursued those markets. This is worth treating as a deliberate future business decision if any of those markets ever become genuinely relevant, not as default MVP scope, and not as a reason to over-build infrastructure now for markets with no near-term relevance.

## F. App-category restrictions

No jurisdiction researched bans or specifically restricts mental-health/wellbeing-adjacent apps as a category. US regulatory treatment (FDA, FTC) and the Australian regulatory approach are both light-touch and inconsistent rather than prohibitive for a communication-support tool like Hold. The medical-device-classification question already flagged for the solicitor (`04-ux-content/02-voice-and-language.md`, "Public claims/copy rule," 2026-08-27) remains the more relevant risk here than any category-level ban — no new finding changes that assessment.

## G. Emerging under-16 social media bans

Australia's under-16 social media ban is already in force; France, Denmark, and Canada have proposed similar measures. All of the versions researched consistently **exempt standalone messaging apps** whose main purpose is messaging, rather than social interaction, content-sharing, or algorithmic feeds. Hold likely qualifies for this exemption as currently scoped — a private, Circle-based communication tool with no public content, no feed, and no algorithmic recommendation of other users' content.

**This is not a one-time check.** The exemption wording specifically excludes "messaging services that have social-media-style features which allow users to interact in other ways apart from messaging" — meaning the exemption is a property of what the app *currently does*, not a status Hold earns once and keeps regardless of future features. See the new standing design principle in `01-foundation/03-principles.md`, "Stay a private messaging tool, not a social platform," which exists specifically to keep this exemption from being eroded by scope creep in future features (most directly relevant to the "From your circle" future idea — see that entry in `08-decisions/04-open-questions.md`, now cross-linked to the new principle).

## H. European Accessibility Act (EAA)

In force since 28 June 2025. The relevant technical standard is EN 301 549, which incorporates WCAG 2.1 AA — the same accessibility bar Hold's own accessibility audit (already logged, unstarted — see `02-research/04-accessibility.md`) already targets independently of the EAA.

**Hold currently qualifies for the EAA's micro-enterprise exemption** (fewer than 10 employees, under €2M annual turnover) as a sole trader — no additional legal accessibility burden beyond what Hold was already planning to do for its own reasons. No plan changes needed: the existing WCAG-based audit already covers the same ground the EAA would require if the exemption didn't apply.

**Note for the future:** this exemption is size-based and could lapse if Hold scales past the micro-enterprise threshold — worth a re-check at that point, not a current concern.

## Cross-references

- `06-privacy-security/01-privacy-by-design.md` links to this file.
- `08-decisions/04-open-questions.md`'s "From your circle" entry is cross-linked to the new standing principle this file's Part G motivated.
- `01-foundation/03-principles.md` carries the new standing principle itself.
