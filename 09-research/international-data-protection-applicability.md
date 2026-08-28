# International data protection applicability — small-footprint exemption research

Background research only, informing a genuine strategic decision point (see "Strategic implication" below) — not itself a decision.

## Question researched

Whether smaller/newer data protection regimes — India's Digital Personal Data Protection Act (DPDPA), Singapore's Personal Data Protection Act (PDPA), Nigeria's Data Protection Act (NDPA) — have any data-volume or small-business threshold that would exempt Hold given its genuinely low data footprint (no ads, no data brokerage, minimal PII collected even on Hold+).

## Finding: no such exemption exists

None of the three laws researched has a footprint-based exemption. All three apply extraterritorially based on **whose data is processed and whether goods/services are offered to that country's residents** — not on processing volume, revenue, company size, or technical sophistication. This is a materially different test from, for example, the EAA's micro-enterprise exemption (see `09-research/global-architecture-scan-pass1.md`), which is genuinely size-based.

The only exemption found across all three is for purely personal/household data processing carried out by an individual for their own purposes — not applicable to a business offering an app, regardless of how small that business is.

**Practical implication:** a single Hold+ sign-up (name/email via Apple/Google auth) from a user physically in India, Singapore, or Nigeria brings that country's data protection law into scope for Hold — immediately, not at some user-count threshold. There is no "too small to count" floor to rely on.

## Extending the pattern: Kenya, Ghana, Philippines

Kenya's Data Protection Act, Ghana's Data Protection Act, and the Philippines' Data Privacy Act were not individually deep-researched to the same standard as India/Singapore/Nigeria above. They are **presumed similar, not yet confirmed** — i.e. structurally likely to follow the same no-threshold, extraterritorial pattern common to nearly all modern comprehensive data protection statutes (most are explicitly modelled on GDPR's own extraterritoriality design), but this is an inference from pattern, not a verified finding for these three specifically. Treat as a reasonable working assumption, not as confirmed research, if this ever becomes decision-relevant.

## Strategic implication — Bethany's call, with solicitor input

This research surfaces a genuine choice, not a problem with only one answer:

1. **Launch store availability broadly** (most countries, by default, as is typical for App Store/Play Store listings) and accept that compliance obligations likely apply the moment any user in any covered country signs up for Hold+ — regardless of how few users that ends up being.
2. **Restrict initial store availability** to a deliberately smaller set of already-covered/already-understood markets (e.g. UK, EU/Ireland, US, Canada, Australia, NZ — see `09-research/global-architecture-scan-pass1.md`), and expand market-by-market as each new market's compliance picture is actually worked through.

Neither is obviously correct — option 1 maximises reach at the cost of an open-ended, hard-to-scope compliance surface; option 2 trades reach for a bounded, plannable one. This is a business decision informed by risk appetite, not something this research resolves on its own.

## Sources

Researched directly against each law's own extraterritoriality/scope provisions (India DPDPA 2023, Singapore PDPA, Nigeria Data Protection Act 2023) rather than secondary summaries alone, cross-checked for the specific question of volume/size-based exemptions.
