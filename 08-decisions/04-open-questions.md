# Open questions

Unlike `01-decision-log.md`, nothing here is settled. These are live questions that came up while reconciling parallel design work and need a deliberate answer before they're built.

## Safeguarding trigger logic and wording

**Architecture decided; content is not.** The two-tier detection model (free: on-device keyword/phrase matching; Hold+: the same layer plus a classifier pass), which surfaces get checked, and the non-blocking persistent-banner response are set out in `06-privacy-security/03-safeguarding.md` and settled for now. What's still **not decided, and requires solicitor and/or clinical safety consultant sign-off before launch:** the actual keyword/phrase list, the classifier's detection criteria, the exact thresholds, and the banner/resource wording — none of this is an internal UX decision. The pipeline is built with a placeholder detection list, hard-gated to local dev builds only, not reaching TestFlight/beta/production until this is resolved.

**Separately noted, not decided:** whether the classifier layer should eventually extend to the free tier once Hold+ revenue comfortably covers its cost — an intention for later, not a current commitment, and doesn't affect the free-tier baseline's launch quality.

**Also separately noted, not scoped:** detecting risk language in "What they sent" (someone else's pasted message) is a different problem from this layer — different response flow, different privacy consideration — and isn't part of this pass at all.

**Reviewer-hiring research and a provisional draft framework now exist, logged 2026-08-12 — progress on the process, not a resolution of the content itself.** `06-privacy-security/03-safeguarding.md` now has the full detail: who to hire (CSO vs. clinical psychologist, DCB0129/DCB0160 context), confirmation that no public ready-made trigger-phrase list exists for Hold's specific private-1-to-1-drafting problem (including why the Samaritans Online Excellence Programme's guidance doesn't directly transfer), the international crisis-resource research (core six markets confirmed, several more flagged as researched-but-unreliable), and the region/language-detection setup-screen decision. `06-privacy-security/05-safeguarding-logic-framework-DRAFT.md` is the provisional category/response-tier skeleton itself, now committed to this repo — previously flagged here as referenced-but-missing; that gap is closed as of 2026-08-12. None of this resolves the actual open item at the top of this entry — the real trigger phrases, thresholds and banner wording still need the clinical reviewer this research is meant to help find.

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

## Adult-only scope boundary — youth/family variant out of scope, not forgotten

Logged 2026-08-11. Hold is designed for adults managing their own communication capacity, and that scope boundary is deliberate, not an oversight to revisit lightly. Pediatric chronic-illness self-management research shows a youth/family variant would need a fundamentally different, multi-person/family-inclusive design — not a smaller or simplified version of the current single-user model, since a child or teenager's communication needs, capacity, and consent structure inherently involve parents/carers as active participants, not passive bystanders. **Not scoped, not planned** — this line exists so the absence of a youth variant reads as a considered boundary rather than a gap nobody noticed.

## Taking Time widget — calming photo display

**Logged 2026-08-11. Future spec — design idea, not yet scoped for build.** No existing widget open-question to cross-reference against; this is the first widget-related entry in this log. (The widget implementation itself — `expo-widgets` / `react-native-android-widget` — is existing, separately-tracked work; this entry is about a specific display feature within it.)

**Concept:** The Taking Time widget shows a calming photo instead of (or alongside) text reassurance — sensory, glanceable calm that doesn't require reading or parsing anything, consistent with low-capacity design principles. Over repeated use, the person comes to associate the specific image with the feeling of Taking Time itself.

**Photo sources — two tiers, both free:**
1. **Curated starter set** — a small selection of calming images (e.g. Jordan's salt flats, Dead Sea, flowers) sourced from free-to-use stock libraries (Unsplash, Pexels, or similar). Each individual image's license must be checked and confirmed before inclusion — terms can vary photo-to-photo even on the same platform, so this is a per-image check, not a blanket assumption. No cost, but not to be skipped.
2. **Personal upload** — confirmed **free tier, not Hold+**. Reasoning: a photo of someone's own child, pet, or meaningful place may genuinely help them more than any curated option, and this sits closer to core emotional support than to a paywallable customisation perk.

**Personal upload — privacy requirements, non-negotiable:**
- On-device storage only. The image must never be uploaded to any server, never synced to Hold's backend, never touch the Cloudflare Workers proxy or the Anthropic API in any form. No legitimate reason for this image to leave the phone under any circumstance.
- No AI processing of these images, under any circumstance — no auto-tagging, no content analysis, no categorisation, local or otherwise. Stated explicitly because these images may include photos of a child or pet.
- Getting a locally-stored image to render inside a home-screen widget will need a shared on-device storage mechanism the widget extension can read (e.g. App Groups on iOS, an equivalent shared-container approach on Android) — still on-device only, just needs the right technical approach so the widget can access the file without it ever leaving the device. **Flag for scoping alongside the existing widget work, not solved here.**
- Brief in-app disclosure needed at upload time that the photo stays local to this device and is not backed up by Hold — so nobody is caught out expecting it to survive a phone change or app reinstall.

**Placement — widget only, not duplicated in-app.** The calming photo lives on the widget only. Deliberately not added to the in-app Taking Time screen, which has a different job (functional: Reconnect button, day-2 contact-update flow, etc.) — adding imagery there risks clutter and could hurt legibility of the actual functional elements on that screen. Treat the widget and the in-app screen as two different surfaces with two different jobs, not something needing visual consistency with each other.

**Reconnect widget state — wording confirmed.** Simpler text for the Reconnect widget state: "Reconnecting" (not "Continue Reconnecting," which read too close to task/checklist framing). Stays unquantified, consistent with the existing no-counts rule for that state.

**Explicitly out of scope — logged separately, not part of this spec.** Community photo-sharing (users sharing their calming images with each other for shared engagement/sense of community) is **not** included here. This is structurally the same shape as the community/social-content-feed feature already explicitly rejected earlier in this project for safeguarding and passive-scroll concerns. If pursued at all, it needs its own dedicated future conversation covering moderation, reporting/blocking mechanisms, and safeguarding review — not folded into the personal-photo feature above. Logged here explicitly so the two don't get conflated later.

**Curated set — licensing clarification.** Bethany's own photography, if included in the curated starter set, requires no licensing at all — she holds copyright as photographer. A brief Terms of Service line noting curated in-app images are for use within Hold only, not external redistribution, is worth adding when this is built, but is not a blocker to scoping or building this feature.

**Not yet decided:** whether/when to build this, which curated images to include (pending per-image license checks), and the App Groups/shared-container technical approach for the personal-upload path.

## Fair-access funding mechanisms — three future-spec ideas, structure captured, none built

Logged 2026-08-11, alongside the current pricing decision (`01-decision-log.md`). None of these are scoped for implementation — this is a record of the shape each idea would take if picked up later, not a commitment.

- **"Pay more if you can" / supporter tier:** an optional higher amount at checkout beyond the base Hold+ price, framed plainly and without pressure — no progress bars, no urgency framing, consistent with the app's existing voice — letting people with means subsidise people without.
- **Gift-a-year:** a one-time purchase generating a redemption code for 12 months of Hold+, since Apple/Google don't support native subscription gifting directly.
- **Charity partnerships:** distributing free Hold+ access via charity-vetted eligibility, so Hold itself never has to build or judge a means-testing system.

All three serve the same underlying goal already stated in `07-business/02-pricing-principles.md`'s "Ethical access options" (scholarship/sponsored access, regional pricing) — these are three concrete mechanisms for that principle, not a new principle. **Not yet decided:** whether to build any of them, which one(s) first, or how they'd interact with the current pricing structure (£17.99/year, £4.99/3-month — the earlier Founding Member/Standard split referenced here has since been removed, see `08-decisions/01-decision-log.md`, 2026-08-11 correction).

## Additional Wider World channels — three future-spec ideas, none built

**Logged 2026-08-11. Future spec — not committed, not scoped for build.** Email out-of-office and Wider World status were built this pass (see `08-decisions/01-decision-log.md`) — these three additional channels were considered alongside them and are worth keeping on record, not built now.

1. **Calendar auto-blocking** — automatically block out time on a person's calendar each morning while they're in Taking Time, until manually turned off. Primary benefit: passively communicates unavailability to teammates who share the calendar, without the person needing to explain directly — consistent with Hold's existing goal of reducing the burden of repeated explanation. Requires real calendar API integration (OAuth, ongoing sync) — a meaningfully bigger technical undertaking than a text field, deliberately scoped out of this pass.
2. **SMS auto-reply** — genuine native auto-reply is not available to third-party apps on either platform without disproportionate scope (see "Hold as default SMS handler" below, closed). If pursued at all, this would only ever be a ready-to-paste text fallback the person applies manually via their own phone's Focus/third-party auto-reply settings (iPhone: Driving Focus only; Android: requires a separate third-party auto-reply app) — not something Hold can trigger directly.
3. **Text-to-speech voicemail greeting** — Hold could generate a spoken audio file from typed status text, but no public API exists on either platform for a third-party app to set someone's actual carrier voicemail greeting. Would require the person to manually apply the generated audio themselves, or a much larger integration with a separate voicemail-replacement service (YouMail, Google Voice, etc.) — deliberately scoped out of this pass.

**Not yet decided:** whether any of these get picked up as future Wider World channels, or in what order.

## Hold as default SMS handler — closed, not open

**Closed 2026-08-11. Explicitly considered and rejected, not a future-spec candidate** — logged here specifically so it isn't quietly revisited without this context, unlike every other entry in this file.

Hold becoming the device's default SMS-handling app (Android) to enable native auto-reply was investigated and rejected on privacy-scope grounds. Google Play policy requires an app to be the **full** default SMS handler (sending/receiving/reading every text message on the device) to access the relevant permissions at all — there is no scoped-down version limited to just auto-reply. This would mean Hold gaining permanent visibility into every text message a person sends and receives, not just during Taking Time — a disproportionate expansion of what the app touches, directly contradicting Hold's privacy-by-design principle (on-device-only storage, no unnecessary data access, established repeatedly elsewhere in this project).

On iOS, this is not possible at any scope — Apple's architecture has no third-party default SMS handler concept at all; Messages is a fixed system app, and the only native auto-reply mechanism (Driving Focus) is OS-exclusive and not extensible by any third-party app.

**Closed. Do not revisit without a materially different technical landscape** (e.g. a platform policy change) — this was rejected on the merits, not deferred for later.

## Does Reconnect need its own "save this message" mechanism?

**Logged 2026-08-11**, from a request to add a "change template/save" control beneath Reconnect's message box, matching Going Quiet's. Going Quiet already has this (single-Circle default auto-save/"Save to Library," combination-keyed templates, "start from X's message") — confirmed present and working, no change needed there.

Reconnect has no equivalent concept at all: its message box starts from `QUICK_RECONNECT_MESSAGES` (a fixed set of canned starter lines), not a saved-per-Circle default, and nothing in Reconnect currently persists an edited message back anywhere. Building an equivalent "Save"/"Change template" control would mean deciding, from scratch: save against what key (a Circle? the current multi-select combination, the same way Going Quiet does combinations? a person, for ungrouped contacts?); whether it should compete with or replace the existing quick-message picker; and whether "template" even means the same thing here, since Reconnect's own message is deliberately generic/one-size ("Reach everyone at your own pace") rather than Circle-specific by design.

**Not yet decided:** whether Reconnect needs this at all, and if so, what it should key against. Flagged rather than guessed at, since it's a real scope/design decision, not an implementation detail.

## Should Going Quiet's completion also fold into one continuous screen, matching Reconnect's new pattern?

**Logged 2026-08-12.** Reconnect's own post-coverage-complete state was folded into one continuous screen (no page-swap; circle row stays visible; the vacated text-box space becomes an inline, collapsible Personalise/Not-now choice; OOO/status opens expanded by default at that point) — see `01-decision-log.md`. Given the priority placed throughout this project on keeping Going Quiet and Reconnect cohesive with each other, the same question was raised for Going Quiet's own completion step but explicitly not answered or built either way, per direct instruction not to assume.

**Not yet decided:** whether Going Quiet's completion (`app/create/people.tsx`) should adopt the same pattern — no separate feel to the completion state (it already doesn't page-swap, being one continuous screen already), text controls disappearing once nothing's left to compose, a collapsible early-exit choice, and OOO/status defaulting open rather than the collapsed-by-default it currently uses. Going Quiet's OOO section was deliberately left untouched (`oooExpanded` still defaults `false`) pending this answer.

## Does Library need a Conversations/Templates/Research tab structure?

**Logged 2026-08-12**, from a request to confirm Library has three segmented tabs (Conversations/Templates/Research, Conversations default) — "given how many other established patterns turned out to be missing from this screen, don't assume this is already correctly built." Checked directly against this book's own record: `04-ux-content/04-navigation-architecture.md`'s "Library screen structure" section documents exactly two things, Conversations (primary, top of one continuous scrolling screen) and Templates (secondary section, below) — not segmented tabs, and with no mention of Research anywhere in Library at all. Research is a separate, standalone destination (`app/settings/research.tsx`, reached via Settings), unrelated to Library in every version of this book's history.

The app's current code already matches the two-part documented structure (unchanged by the same-day Conversations rebuild — see `01-decision-log.md`). A 3-tab structure, or moving Research content into Library, would be a genuine, undocumented product change, not a bug fix — not built, since it directly conflicts with what's already on record here.

**Not yet decided:** whether Library should actually move to three tabs with Research folded in, whether "Research" here meant something else (e.g. the "Where this comes from" links already scattered through the app, pointing at Settings' Research page), or whether the report was based on a different app/mockup. Needs a direct answer before any of this gets built.

## "From your circle" (Hold+, future — after MVP + Phase 10 paywall)

**Logged 2026-08-11, from a session write-up.** Design/decision-layer discussion only — nothing below has been built, and this is explicitly deferred until after MVP and the Phase 10 paywall are live.

**Concept:** an opt-in way for a user's own circle to contribute to their Going Quiet/Taking Time experience. Entry point: "Would you like your circle to personalise your flow?" — sender-initiated only, never prompted to friends directly, no visible consequence for declining.

**Core mechanism:** the user generates a unique, time-limited invite link per Going Quiet/Taking Time period (Hold+ gated on the sender's side). A friend opens the link in a browser — no login, no app download. Friend content is always labelled "from your circle," never presented as the user's own words — this sidesteps the AI-boundaries voice-ownership problem by being a distinct, attributed human voice by design, not an AI-drafted one.

**V1 scope (low-risk, template-first):**
- A pre-written, pre-vetted phrase bank for friends to choose from ("you're amazing," "thanks for messaging lovely," "I/we love you") — no safeguarding classifier needed, since phrases are vetted once, centrally.
- Seasonal/location visual themes (autumn/winter/summer, sea/forest/meadow) and plain-tone options — reusing the existing moon-cycle overlay colour system rather than building a second visual system.
- An optional free-text box, character-limited (~200 chars) for friends who want to write their own message. The brevity limit is a deliberate soft guardrail against guilt-spiral/justification-style writing, not just a UI constraint.
- Free text only (never template selections) runs through the existing Haiku safeguarding-classifier pattern before storage, checking for guilt-spiral/pressure phrasing ("you always," "I miss the old you"). Flagged text should prompt a rephrase, not silently vanish — exact UX still open (see open sub-questions below).
- Select screens only, not the full flow — candidate screens: a Taking Time variant, one or two notification/message moments. Needs an explicit, finalised screen list before build.
- Optional light psychoeducation copy shown to friends while filling the form — general framing around low-capacity communication only (why brief, pressure-free contact helps). Must **not** imply or state a diagnosis/condition for the specific user.

**Later-phase scope (higher-risk, deliberately deferred from v1):**
- Custom stickers from friend-uploaded photos — a new moderation surface (inappropriate/irrelevant image content), plus storage/privacy questions (retention window, EXIF stripping, deletion on Going Quiet period end).
- Widget photo selection: a friend can upload and preview what a photo would look like as a widget, but this does **not** amend the user's actual widget — the user must separately choose to apply it. Friend-submitted photos are presented to the user for that purpose only, never auto-applied. (Confirms third parties cannot write to a user's home-screen widget directly on iOS/Android — this design correctly doesn't attempt that, consistent with the on-device-only approach already logged for the Taking Time widget's personal-photo feature above.)

**Storage:** friend submissions stored temporarily server-side (likely Cloudflare Workers/KV, reusing existing infra) until synced to the user's device on next app open, then deleted from the server — mirrors the existing shorter-retention pattern used for Conversations reply drafts. No read receipt / "seen by user" status is shown to the friend, to avoid a performance-anxiety loop for the contributor. Needs a decided fallback expiry (e.g. delete after N days) if sync never happens — open question, not decided.

**Preview model — resolved direction:** content/wording is never fully blind to the user. Before the Going Quiet period begins, a one-page preview shows the exact message/quote text in full (no surprises in wording), and what type each item is (sticker, photo, quote-style message) via a neutral default layout — structural context only, no final styling. What stays hidden until the real moment: colour theme, font, sticker/photo size and placement, all visual styling. **Rationale, reached during this session as a direct application of the low-capacity design principle:** content-surprise carries real risk for someone in a low-capacity state (wording could land wrong, reference something they're not ready for); aesthetic-surprise (colours, stickers) carries essentially none, and is fine to preserve for delight — "heart stickers and pink font as a surprise are fine, content is not." Preview screen copy needs to briefly explain *why* content is shown now but styling isn't, framed warmly, not clinically, not as a trust/vetting statement about the friend's circle — rough direction only, not final ("no surprises in the words when you're taking time; colours/stickers/styling stay a surprise for then"), and needs the same shame/guilt voice review as the rest of Hold's copy before use (`04-ux-content/02-voice-and-language.md` / `02-research/06-guilt-spiral-and-supportive-language.md`).

**Open sub-questions — genuinely not decided, logged as open rather than resolved:**
1. Exact screen list for "from your circle" variants.
2. UX for a flagged/rejected free-text message — silent block vs. rephrase prompt.
3. Fallback server-side expiry window if sync never happens.
4. Whether Hold+ gating applies only to the sender, or also affects what the friend can access.
5. Final preview screen copy (needs voice review).
6. Preview format detail — plain unstyled list of text, or neutral default layout with type indicators (leaning toward the latter, discussed this session, but not yet built/decided).

**Why this is worth prioritising eventually, not a reason to build it now:** the first Hold+ feature that's inherently relational rather than solo (unlike AI amend, AI memory, moon-cycle overlay) — plausibly a stronger conversion driver and word-of-mouth vector, though this is reasoning, not tested data. A cheap fake-door test (an inert "invite your circle" button, measuring taps) is recommended before committing to a full build. **Not scoped for build — explicitly deferred until after MVP + Phase 10 paywall are live.**

## Notification content ideas (future, opt-in, Hold+) — three strands, none scoped for build

**Logged 2026-08-11, from a session write-up, consolidated into one entry per that write-up's own recommendation.** Sits alongside the previously-scoped relationship/psychology "did you know" facts idea (if one exists elsewhere in this book) as a related but distinct set of content strands.

1. **Historical/cultural facts about chronic illness and coping** — how different eras/cultures understood or treated conditions resembling chronic illness; whether a given condition is a "new phenomenon" or newly *named* rather than newly *experienced*. Emotional core: "all humans across time are one community, coping and surviving together" — reframes isolation as historical continuity. Needs the same sourcing rigour as existing Research content (primary/credible sources only), and explicit care not to manufacture false continuity between historical and modern conditions where the medical/social context genuinely differs, while being honest that naming/diagnosis evolves even when human experience is old.
2. **Quotes on friendship/family/support** — flagged as higher-risk than the above: quote misattribution is extremely common online, and copyright/attribution rules apply directly. Needs verified sourcing or shouldn't be used at all — no reproducing quotes from unverifiable sources. A safer alternative/complement: original Hold-voice lines (no attribution risk, full tonal control), used alongside verified quotes rather than replacing them as the default.
3. **Per-category notification toggles** — given the growing number of distinct content strands (supportive Hold-voice lines, relationship/psychology research, history/culture of chronic illness, quotes), this needs a proper settings sub-screen with individual toggles per category, not one blanket on/off. Interacts with the already-resolved "basic notification control is free for everyone, finer-grained control could be Hold+" split in `07-business/02-pricing-principles.md` — which tier this specific toggle screen belongs to isn't decided here.

**Not yet decided:** whether to build any of these, which one(s) first, exact sourcing process for strands 1 and 2, or how the per-category toggle screen (3) fits the free/Hold+ notification-control split already documented elsewhere.

## Lapsed/dormant Hold+ backup account — retention windows and warning gap

**Logged 2026-08-12, pointer entry — full proposal lives in `06-privacy-security/04-content-retention.md`, "Lapsed/dormant Hold+ backup account retention."** Scoped only to the optional, opt-in Hold+ backup account (Sign in with Apple/Google) — not free-tier local-only data, which has nothing server-side to warn about or delete.

Three genuinely open sub-questions, not decided:
1. **Exact grace/dormant window figures** (proposed: 30-day grace period, 6–12 month dormant window before deletion) need confirmation from a solicitor/DPIA reviewer — founder-proposed starting numbers, not validated ones.
2. **Sign in with Apple's private email relay** as a secondary warning-delivery channel — its exact mechanics for backend-initiated communication weren't confirmed against current Apple developer documentation; needs verification before being relied on.
3. **The "app deleted, unreachable" gap:** if someone has deleted the app entirely, a push-notification-only deletion warning can't reach them. Whether this is acceptable as-is or needs a fallback contact method (with its own privacy trade-offs) isn't decided.

**A file-placement note, since the source material named a file that doesn't exist in this repo:** the source material for this item referred to `03-privacy-model.md` as the target location — that file lives in `hold-app`'s own `docs/` directory, not in `hold-book`. Within `hold-book`, `06-privacy-security/04-content-retention.md` ("What personal content is kept, and for how long") was the closest existing structural fit, so the full proposal was added there instead, alongside the on-device draft-retention windows it sits next to conceptually. Flagging this choice explicitly rather than assuming it's uncontroversial — if the intent was genuinely for this to live in `hold-app`'s `docs/03-privacy-model.md` instead (or in addition), that's a different repo and needs saying explicitly before it happens.

## Reconnect's resumed-view OOO/status default — collapsed or expanded?

**Logged 2026-08-13, a direct conflict between two on-record instructions, not silently resolved either way.** The 2026-08-12 decision log entry deliberately flipped Reconnect's OOO/status section's default from collapsed to *expanded*, scoped explicitly to "Reconnect's own post-coverage-complete moment." A 2026-08-13 message specifying the resumed "Finish Reconnecting" view — itself that exact same moment — asked for OOO/status "closed/collapsed but reopenable." Built with the 2026-08-12 default (expanded/`true`) left unchanged, since reversing it wasn't confirmed as deliberate rather than the two instructions simply not having been cross-checked against each other.

**Not yet decided:** whether the 2026-08-13 message meant to reverse the 2026-08-12 default, in which case `oooExpanded`'s initial state in `app/return/reconnect.tsx` should flip back to `false`.
