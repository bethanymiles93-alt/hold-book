# Roadmap

Referenced in the README's repository map but never actually written as a file until now. Phased loosely by version; not committed dates, just sequencing logic — later phases depend on data and infrastructure the earlier ones haven't produced yet.

## MVP (v1)

The Core Journey as specified in `04-ux-content/01-core-journeys.md`: Going Quiet, Taking Time, Reconnect (single tap into Conversations), Conversations (per-person Quick message / Personalise), Library, basic History, basic Patterns, Circles, Settings/About. SMS-only sending. See `03-mvp-requirements.md` for the full requirement list.

## v1.5 — Hold+ launch

Founding Member pricing goes live (`07-business/02-pricing-principles.md`). Unlimited Circles/AI for paying users. No new product surface beyond what MVP already has — this phase is about the paywall and subscription infrastructure existing, not new features.

## v2 — Communication Insights and Pattern Recognition

This is where richer Patterns (`03-product/04-patterns.md`) actually gets built out: multi-month calendar view, seasonal/recurring-timing trend detection, optional health-note correlations. Also where AI personalisation deepens — see "AI personalisation, not yet decided" below.

## v3

- Messaging Channels (per-contact preferred channel, grouped delivery screen) — already scoped and deferred, see `08-decisions/04-open-questions.md`
- Optional Apple Health / Health Connect integration — already flagged as a future, not-yet-scoped idea in `03-product/04-patterns.md`
- Export reports (PDF/GP summary) — already in the Hold+ feature list, formalised here as a v3 target if not shipped earlier
- General AI assistant improvements

## Future (not scoped, not committed)

- Wearables integration
- Smart/proactive insights (distinct from the user-initiated Patterns view)
- Support for carers (someone other than the user managing or viewing parts of Hold on the user's behalf — would need its own privacy/consent model, not a small addition)
- Team or family features — explicitly conditional: "if they still fit the philosophy." Hold's core value is personal and private; anything multi-user needs to be checked against that before it's built, not assumed to fit just because it's technically possible. If built at all, scope narrowly as a **Trusted Contact** feature, not general family/team access: opt-in by the user only (never requestable by the trusted contact), status-only visibility ("still taking time" / "reconnected" — never message content, Circle membership, or Patterns), easily and silently revocable (no notification to the trusted contact on revoke, so revoking doesn't itself become a confrontation), and always a specific named person the user chooses, never automatic Circle-based access. This carries a real coercion/misuse risk (a controlling partner or parent using it to monitor someone) that needs its own consent and threat-model review before any build work, not just a feature checkbox. **Deliberately not monetised** even if built — see `07-business/02-pricing-principles.md` — since charging for it risks Hold appearing to profit from something adjacent to surveillance.

## AI personalisation — not yet decided

**Note:** a narrower, distinct pair of features has since been built and shouldn't be confused with the ideas below — "Amend with AI" (a light-touch blend of typed context into an existing draft) and AI memory (an opt-in, two-layer "remember a detail, suggest it back later" feature). See `07-business/02-pricing-principles.md`'s Hold+ list and `04-ux-content/01-core-journeys.md`, "Amend with AI." Neither does writing-style learning, uses saved messages as ambient context, or varies drafting by relationship type — the ideas below remain genuinely unscoped.

A cluster of related Hold+ ideas from parallel exploration, not yet reconciled with what's already in the pricing file:

- AI that learns the user's writing style over time
- Using the user's own saved messages/templates as context for future drafts
- Relationship-aware drafting — the AI drafts differently for a Core Circle message versus a Work message versus a Care contact, based on the relationship type already encoded in Circles

These are more specific than "richer pattern recognition" and worth their own line in the Hold+ feature list once scoped — they also raise a privacy question not yet addressed: using someone's own past messages as AI context means storing and re-processing that content, which needs the same "define purpose, minimise data, get informed agreement" treatment as anything else in `06-privacy-security/01-privacy-by-design.md`, not an assumption that it's fine because it's the user's own data.
