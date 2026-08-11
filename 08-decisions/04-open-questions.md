# Open questions

Unlike `01-decision-log.md`, nothing here is settled. These are live questions that came up while reconciling parallel design work and need a deliberate answer before they're built.

## Safeguarding trigger logic and wording

**Architecture decided; content is not.** The two-tier detection model (free: on-device keyword/phrase matching; Hold+: the same layer plus a classifier pass), which surfaces get checked, and the non-blocking persistent-banner response are set out in `06-privacy-security/03-safeguarding.md` and settled for now. What's still **not decided, and requires solicitor and/or clinical safety consultant sign-off before launch:** the actual keyword/phrase list, the classifier's detection criteria, the exact thresholds, and the banner/resource wording — none of this is an internal UX decision. The pipeline is built with a placeholder detection list, hard-gated to local dev builds only, not reaching TestFlight/beta/production until this is resolved.

**Separately noted, not decided:** whether the classifier layer should eventually extend to the free tier once Hold+ revenue comfortably covers its cost — an intention for later, not a current commitment, and doesn't affect the free-tier baseline's launch quality.

**Also separately noted, not scoped:** detecting risk language in "What they sent" (someone else's pasted message) is a different problem from this layer — different response flow, different privacy consideration — and isn't part of this pass at all.

## Verify release-mode build before first TestFlight submission

The safeguarding placeholder-list gate (see `08-decisions/01-decision-log.md`, 2026-08-10) relies on React Native's `__DEV__` being false in any build that reaches TestFlight or production — true in any release-mode bundle, which is what EAS Build's preview/production profiles always produce. Once EAS Build is actually set up for the first real submission, do a sanity check that the resulting build is genuinely release-mode, not an accidental dev client, before it ships — the placeholder list (not clinically reviewed) must never reach a real device. **Not yet actioned — no `eas.json` exists yet.** Revisit when EAS Build is first configured.

## Worker deploy pending — three new AI-amend surfaces not yet live

`worker/src/prompts.ts` and `worker/src/index.ts` (see `08-decisions/01-decision-log.md`, 2026-08-10, "Unified text entry app-wide") gained three new `AiSurface`/`PromptSurface` values — `email-ooo`, `wider-world-status`, `template` — so Amend with AI works on OOO/status/Library-template editing for the first time. This is a code change only; the live `hold-ai-proxy` worker still runs the old build until someone manually runs `cd worker && npm run deploy` with Cloudflare/wrangler credentials — nothing in the app repo's own push/CI triggers this. **Not yet actioned; Bethany's own responsibility, not a code task.** Until deployed, tapping AI-assist on those three surfaces specifically will throw an "unknown surface" error against the live proxy — the four pre-existing surfaces (going-quiet, reassurance, reconnect, conversations-reply) are unaffected either way. Revisit/close once the deploy has actually run.

## Voice control for navigation/actions (not dictation) — deferred, open question

**Status:** Not scoped, not started. Logged as a distinct future consideration, separate from speech-to-text dictation (already decided and built — see `08-decisions/01-decision-log.md`, 2026-08-10, "Unified text entry app-wide").

**The need:** Raised as an accessibility case — someone whose hands hurt too much to type or tap reliably (physical pain/mobility limitation, distinct from the emotional/cognitive low-capacity cases the rest of the app is designed around) may still be able to speak.

**What this would mean, if built:** Voice-driven navigation and action-triggering across the app — e.g. "go to Reconnect," "select Close Circle" — not just dictating text into a box. This is a materially larger undertaking than the STT-for-composing feature already shipped: it needs intent recognition across the whole app's navigation and action space, not speech-to-text into one field.

**Provisional shape discussed (not committed):** Voice could plausibly drive everything except the final "Send" — that one action stays gated behind a deliberate confirm step, given it's the one truly consequential, hard-to-undo action in these flows. Two options discussed for that confirm step, both with real trade-offs and neither obviously correct:
- A physical tap to confirm — lower burden than typing, but still requires some physical action, which may not fully solve for the person this is meant to serve on a bad day.
- A spoken double-confirm (app reads back what it's about to do, listens for a narrow yes/no) — zero physical action needed, but introduces a different risk: background speech or a misheard word triggering an unintended send. Narrowing the listening window to just after a read-back mitigates but doesn't eliminate this.

Current lean, not decided: offer both as options rather than picking one, since they serve overlapping but not identical accessibility needs.

**Why deferred rather than scoped now:** Raised in the middle of an already-large in-progress batch of work (docked input bar rollout, AI-amend relocation, dictation). Logged here to make sure it isn't lost, not to imply it's next.

## Group vs Individual messaging mode

**Discussion, not yet fully decided.** Whether to build Group/Individual sending per Circle now, alongside the Core Journey work, or defer it as a tracked follow-up (the way Messaging Channels/per-contact preferences were deferred).

- **Group** — one message, sent to everyone in the Circle at once.
- **Individual** — the same or separate drafts prepared per person in the Circle.

The case for keeping it in scope: the Conversations per-person tracking model ("2 of 5 replies sent," tick/untick per person) requires per-person state to exist underneath regardless of whether a message was sent as a group or individually. Individual tracking isn't really optional given that — so Group becomes a comparatively cheap UI layer (one drafted message, fanned out to several people) on top of tracking that has to exist either way, rather than a separately expensive feature to build or cut.

The case for deferring: it still adds UI surface (a Group/Individual toggle per Circle) and drafting-flow complexity at a stage where the Core Journey rename and restructure is already substantial. Worth a explicit decision — not silently defaulting either way — before this goes into a build message.

**Current leaning:** keep in scope, for the tracking-model reason above. **Not formally decided.**

## Messaging Channels (per-contact preferred channel, grouped delivery screen)

Deferred as a tracked follow-up rather than built alongside the Core Journey changes, specifically to keep that pass scoped — this was an explicit trade-off, not an oversight. SMS-only remains the default and only path for the current MVP pass.

Scope when picked back up: per-person/Circle preferred channel settings (SMS, iMessage, WhatsApp, Email, Instagram DM, Facebook Messenger, Signal), configured in Circle/contact settings, never mandatory during onboarding or an urgent Going Quiet flow; a grouped delivery screen for non-SMS channels (e.g. SMS — sent / WhatsApp — continue / Instagram — continue / Email — continue), since Hold can prepare a message and hand off to a share/app flow but cannot auto-send through most third-party platforms. **Deferred, not cancelled — revisit once Core Journey ships.**

## Icon placement in the wordmark

Should the "held" icon (soft overlapping/embracing shapes) sit inside the "O" of the "Hold" wordmark, or stay as a fully separate mark? **Not yet decided** — worth testing both, since embedding it in the "O" could read as clever or could read as cluttered/hard to reproduce at small sizes; a separate mark is safer but less distinctive. Note this is about the small wordmark logo specifically, which stays static per `05-design-system/01-design-direction.md` — it's a branding question, not a motion one.

## Optional Hold signature on template messages

See `03-design-experiments.md`. Beta hypothesis, not a decision.

## Optional account sign-in mechanism

**Decided in principle** (see `08-decisions/01-decision-log.md` for the account/auth model itself): no mandatory account for the core journey. **Not yet decided:** the exact mechanism for the optional lightweight sign-in used for Hold+ restore/future sync — likely Sign in with Apple (and Google equivalent on Android) rather than email/password, to avoid adding a password to remember, but the specific implementation hasn't been chosen.

## Error state copy

What Hold says when the native share sheet fails/is cancelled, SMS isn't available, or AI drafting times out. **Not yet written** — should follow the same voice principles as the rest of the app, not generic system error text. See `04-ux-content/05-onboarding-empty-states.md`.

## Library internal organisation

Not previously specified at this level of detail. One proposal: organise by Circle first, then by message stage within each Circle (Going Quiet / Reassurance / Reconnect / Conversations expanding inline under a Circle selector) — reasoning being that in practice someone thinks "I need my Work message" before they think "I need my Reconnect template." Alternative: organise by stage first, Circle second (the reverse). **Not yet decided** — worth resolving once the broader Library scope is picked back up, not urgent for the current MVP pass.

## Exact free-tier AI allowance — moot, superseded, fully resolved

This question (what number to set a free monthly AI-drafting allowance at) no longer applies: AI-assisted drafting is now Hold+-only, with no free allowance at all. `draftService.ts` gates AI drafting behind Hold+ directly; the AI proxy's (`worker/`) monthly cap (`MONTHLY_DRAFT_SAFETY_CAP` in `wrangler.toml`, still 20/month) is now a blunt cost-safety backstop against abuse of the endpoint itself, not a user-facing allowance to size correctly. The removed-free-tier decision itself is now logged in `08-decisions/01-decision-log.md` (2026-08-10, retroactive), and `07-business/06-business-strategy.md`'s ARR/conversion reasoning has since been rewritten to reflect it — nothing left open here.

## "Reset app" as a distinct action from "Delete my data"

Right now "Delete my data" wipes content only (Circles, history, templates, drafts, reply/AI state) and deliberately leaves behind non-content UI flags (seen-welcome-screen, seen-retention-note) so the app doesn't force someone back through onboarding after a deliberate wipe. A separate "Reset app" action — full fresh-install state, content and flags both — is a real pattern (Android's "clear cache" vs "clear storage" distinction, similar OS-level settings-reset patterns) but hasn't been requested by any real use case yet; the plausible one is someone handing off or selling their phone and wanting zero trace, not the everyday "delete my data" moment. **Not yet decided whether to build this** — deliberately not scoped now, since adding a second destructive button next to "Delete my data" adds a decision at exactly the kind of low-capacity moment Hold's design principles guard against, and nothing currently requires it. Revisit only if a real need surfaces.

## BYOK (bring your own AI key) as a possible free-tier path

**Explored, not decided or built.** Idea: let users optionally connect their own Anthropic/OpenAI/paid-Gemini API key in Settings, so people who can't afford Hold+ can still get AI drafting, at zero cost to Hold. Key points from the exploration:

- Scoped as Settings-only and opt-in — never surfaced as a choice mid-flow, so the structured one-tap journey is unaffected.
- Free-tier providers that train on user data by default (e.g. Gemini's free tier) should not be offered as an option, even as the user's own informed choice — Hold shouldn't steer people who can't pay toward the one option that trains on sensitive personal disclosures. Paid-tier Gemini, OpenAI, and Anthropic keys are all privacy-comparable and fine to support.
- Hold's own safeguarding detection layer must run in front of any provider a user brings — BYOK cannot create a path around Hold's own safety layer.
- Claude was chosen originally on a reputation-based read (warmer, less clinical by default vs. other providers), not a benchmarked one — worth a real blind-rated comparison test across providers using representative Hold prompts before claiming any provider is "better," since this hasn't actually been measured.
- If built, Hold+'s value proposition should stay "convenience, zero setup" rather than "better AI" — BYOK users should get the same Hold system prompts/voice/safeguarding integration as Hold+, since there's no cost reason to withhold prompt quality from someone paying their own token costs.

**Not yet decided:** whether to build this at all, which providers to support, where API keys are stored/used (needs its own privacy-model writeup, same rigor as Your Circle's contact data), and how much setup friction is acceptable for Hold's actual low-capacity audience.

## Fair-access funding mechanisms — three future-spec ideas, structure captured, none built

Logged 2026-08-11, alongside the current pricing decision (`01-decision-log.md`). None of these are scoped for implementation — this is a record of the shape each idea would take if picked up later, not a commitment.

- **"Pay more if you can" / supporter tier:** an optional higher amount at checkout beyond the base Hold+ price, framed plainly and without pressure — no progress bars, no urgency framing, consistent with the app's existing voice — letting people with means subsidise people without.
- **Gift-a-year:** a one-time purchase generating a redemption code for 12 months of Hold+, since Apple/Google don't support native subscription gifting directly.
- **Charity partnerships:** distributing free Hold+ access via charity-vetted eligibility, so Hold itself never has to build or judge a means-testing system.

All three serve the same underlying goal already stated in `07-business/02-pricing-principles.md`'s "Ethical access options" (scholarship/sponsored access, regional pricing) — these are three concrete mechanisms for that principle, not a new principle. **Not yet decided:** whether to build any of them, which one(s) first, or how they'd interact with the Founding Member pricing structure.
