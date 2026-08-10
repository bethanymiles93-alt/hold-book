# Open questions

Unlike `01-decision-log.md`, nothing here is settled. These are live questions that came up while reconciling parallel design work and need a deliberate answer before they're built.

## Safeguarding trigger logic and wording

The proportionate approach (detection layer, crisis resources, lightweight safety-plan option) is set out in `06-privacy-security/03-safeguarding.md`, but the exact trigger logic, thresholds and wording are **not yet decided** — this requires solicitor and/or clinical safety consultant sign-off before launch, not just an internal UX decision.

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

## Exact free-tier AI allowance

`07-business/02-pricing-principles.md` treats 10–20 AI-assisted drafts/month as a working assumption, not a tested figure. **Not yet decided precisely** — should be set from real usage data (actual API cost per draft, actual distribution of how often free users need AI help) once available, not guessed permanently in a design conversation. The *principle* is decided (one shared monthly pool, generous, episodic usage keeps average cost low); the *number* isn't.

**Now technically enforced, still a placeholder:** the AI proxy (`worker/`) implements this as a real cap — 20/month, the upper end of the working range — configurable via a plain Worker variable (`FREE_MONTHLY_DRAFT_LIMIT` in `wrangler.toml`), not hardcoded into application logic. Enforcing *something* from day one was necessary for cost safety; this doesn't mean 20 is the resolved answer, just the current placeholder value in a config field that's trivial to change once real data exists.

## "Reset app" as a distinct action from "Delete my data"

Right now "Delete my data" wipes content only (Circles, history, templates, drafts, reply/AI state) and deliberately leaves behind non-content UI flags (seen-welcome-screen, seen-retention-note) so the app doesn't force someone back through onboarding after a deliberate wipe. A separate "Reset app" action — full fresh-install state, content and flags both — is a real pattern (Android's "clear cache" vs "clear storage" distinction, similar OS-level settings-reset patterns) but hasn't been requested by any real use case yet; the plausible one is someone handing off or selling their phone and wanting zero trace, not the everyday "delete my data" moment. **Not yet decided whether to build this** — deliberately not scoped now, since adding a second destructive button next to "Delete my data" adds a decision at exactly the kind of low-capacity moment Hold's design principles guard against, and nothing currently requires it. Revisit only if a real need surfaces.
