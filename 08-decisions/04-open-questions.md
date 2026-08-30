# Open questions

Unlike `01-decision-log.md`, nothing here is settled. These are live questions that came up while reconciling parallel design work and need a deliberate answer before they're built.

## Framing note: building toward future accreditation, from now

Research this session (see `09-research/nhs-orcha-accreditation-pathways.md`) confirmed Hold does not need NHS DCB0129 or ORCHA accreditation for MVP launch — neither is mandated for a standalone consumer app. However, both explicitly reward groundwork laid early rather than retrofitted later: DCB0129 states clinical risk management "must start at the earliest stage of the development lifecycle," and ORCHA scores against four pillars — Data & Privacy, Clinical/Professional Assurance, Evidence, and Usability & Accessibility — that are far cheaper to build in now than to construct after the fact.

Practical implication: several items below (safeguarding documentation discipline, evidence-gathering, accessibility) aren't just individually useful — they are specifically the groundwork that keeps NHS/ORCHA accreditation realistically open as a future option, without requiring Hold to pursue either now. Treat this as the throughline connecting the public safeguarding policy, evidence-gathering, "did this help?" prompt, and comparable-app-research entries below, not several unrelated tasks. (The minimum-age question this line originally also pointed to is resolved — see below — and no longer part of this throughline.)

## Spec-complete, awaiting build (queued, not started)

This section is deliberately distinct from every other entry in this file. Everything below is **fully specced and ready to build** — no open design or product decision remains — but has not been started because it hasn't yet been prioritised against other work. This is a "when," not a "whether or how" list. Do not confuse these with the genuinely undecided questions later in the file.

### "Did this help?" evidence prompt, History-first

**Logged 2026-08-27. Trigger logic refined 2026-08-27 — spec-complete, not started.**

**What it is:** In History, a simple, optional, skippable prompt on a past Reconnect period's entry: "Did reaching out help?" with 2-3 tap options (e.g. yes / a little / not really). No free text required. Never blocks or interrupts viewing History — appears passively alongside the entry, easily ignored. Store responses as anonymous aggregate data only, consistent with existing privacy model.

**Trigger logic (refined):** Rather than a passive prompt that only shows if someone happens to browse an old History entry, the prompt surfaces at the point a Reconnect flow's entry is finalised into History — whichever of these happens first:
- **Natural completion:** all Reconnect Conversations for that period are finished, and the consolidated History entry is created.
- **Early end:** the person ends the flow before all Conversations are finished. The entry still lands in History (as it already does), and the prompt still surfaces there — this is the fallback that ensures an incomplete flow doesn't silently skip the prompt.

Practically: the prompt appears attached to the entry the first time it's viewed in History after being finalised (either path above), not on every subsequent view once already answered or dismissed. Once answered or explicitly dismissed, don't re-prompt on that entry again.

**Reasoning:** retrospective placement avoids adding friction to the live Going Quiet/Reconnect flow, when the person has the least capacity. Someone looking back in History has already chosen to revisit that moment, so a reflective question fits naturally rather than intruding. This is also the ongoing data source that feeds the Evidence pillar ORCHA's review scores against (see the beta/pilot entry below and `09-research/nhs-orcha-accreditation-pathways.md`) over time, not just a one-off pilot.

**Flagged, not yet decided — do not build without explicit confirmation:** Three further placements were discussed and explicitly NOT approved: end of Reconnect, Reconnect Conversations (per-conversation), and Reconnect's instant message step. Logged as options to revisit only once the History-only version is live and its impact can be assessed. Do not add prompts to any live flow surface without Bethany's explicit go-ahead — the standing concern is not wanting to put users off or add friction during moments of low capacity.

**Status: spec-complete, queued for later build. Not started.**

## Safeguarding trigger logic and wording

**Architecture decided; content is not.** The two-tier detection model (free: on-device keyword/phrase matching; Hold+: the same layer plus a classifier pass), which surfaces get checked, and the non-blocking persistent-banner response are set out in `06-privacy-security/03-safeguarding.md` and settled for now. What's still **not decided, and requires solicitor and/or clinical safety consultant sign-off before launch:** the actual keyword/phrase list, the classifier's detection criteria, the exact thresholds, and the banner/resource wording — none of this is an internal UX decision. The pipeline is built with a placeholder detection list, hard-gated to local dev builds only, not reaching TestFlight/beta/production until this is resolved.

**Separately noted, not decided:** whether the classifier layer should eventually extend to the free tier once Hold+ revenue comfortably covers its cost — an intention for later, not a current commitment, and doesn't affect the free-tier baseline's launch quality.

**Also separately noted, not scoped:** detecting risk language in "What they sent" (someone else's pasted message) is a different problem from this layer — different response flow, different privacy consideration — and isn't part of this pass at all.

**Reviewer-hiring research and a provisional draft framework now exist, logged 2026-08-12 — progress on the process, not a resolution of the content itself.** `06-privacy-security/03-safeguarding.md` now has the full detail: who to hire (CSO vs. clinical psychologist, DCB0129/DCB0160 context), confirmation that no public ready-made trigger-phrase list exists for Hold's specific private-1-to-1-drafting problem (including why the Samaritans Online Excellence Programme's guidance doesn't directly transfer), the international crisis-resource research (core six markets confirmed, several more flagged as researched-but-unreliable), and the region/language-detection setup-screen decision. `06-privacy-security/05-safeguarding-logic-framework-DRAFT.md` is the provisional category/response-tier skeleton itself, now committed to this repo — previously flagged here as referenced-but-missing; that gap is closed as of 2026-08-12. None of this resolves the actual open item at the top of this entry — the real trigger phrases, thresholds and banner wording still need the clinical reviewer this research is meant to help find.

**Named leads for who to actually contact, logged 2026-08-28 — outreach, not resolution.** `09-research/clinical-safety-reviewer-leads.md` has specific contacts and consultancies surfaced while researching Calm Harm: stem4's general and accessibility inboxes, Dr Nihara Krause (Calm Harm's CSO, not confirmed available for outside work), mHabitat (Calm Harm's actual reviewer, but only reachable to date via an NHS-funded programme relationship, not a standalone bookable vendor — see that file for the correction), and eight commercial CSO/clinical-safety consultancies with no confirmed pricing, mostly built around ongoing NHS-supplier retainers rather than the one-off scoped review Hold likely needs. None of these leads have been contacted yet.

**Related, separate question — see "Independence consideration for informal clinical input" below.** Whether an informally-available clinician known personally to Bethany could substitute for this independent review. Answered there: no, not as a substitute — logged separately since it's a distinct question from *finding* a reviewer.

## Independence consideration for informal clinical input

**Logged 2026-08-28.** Bethany's father is a practising GP (GMC-registered) in the UK. Considered and discussed whether he could serve as Hold's Clinical Safety Officer.

**Conclusion, logged so it doesn't need re-litigating later:** GMC registration satisfies one eligibility criterion for formal DCB0129/DCB0160 CSO training, but does not confer CSO status automatically — he would need to complete NHS England's accredited Clinical Risk Management training (pricing already logged in `09-research/nhs-orcha-accreditation-pathways.md`). More importantly, using a family member for a safety-critical review of the founder's own product raises a genuine independence/conflict-of-interest question, separate from credentials or training — this could matter if the review were ever scrutinised (App Store review, a user complaint, a legal issue), and an independent reviewer with no personal connection may be viewed as more credible, particularly given Hold's core calibration challenge (false positives from ordinary phrases like "going quiet") benefits from a genuinely fresh, uninvolved clinical eye.

**Decision leaning, not fully closed:** his input is welcome and valuable as an informal second opinion, but should not substitute for the formal, documented, independent clinical safety review Hold needs before safeguarding features go live. Revisit only if no independent reviewer proves accessible or affordable. See `09-research/clinical-safety-reviewer-leads.md` for the outreach leads this independent review would actually draw from.

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

## Group vs Individual messaging mode — resolved, closing a stale open question

**Resolved.** Decided 2026-08-11, built and verified 2026-08-12. Individual/BCC-style delivery is the default (each recipient gets their own separate message; no one in a Circle knows who else received it), with a per-Circle "send as group" toggle, default off, available at Circle creation and in that Circle's own Manage Circles settings — a combination of Circles with mixed settings still sends as one action, each Circle following its own setting within it. This is already live in the code, not a pending decision. See `08-decisions/01-decision-log.md`'s 2026-08-11 consolidated-pass entry (the delivery-model correction) and its 2026-08-12 follow-up (the accepted N-compose-sheet-confirms trade-off) for the full reasoning. This entry was left open after the decision was made and built; closed now rather than left to imply the question is still live.

## Messaging Channels (per-contact preferred channel, grouped delivery screen)

Deferred as a tracked follow-up rather than built alongside the Core Journey changes, specifically to keep that pass scoped — this was an explicit trade-off, not an oversight. SMS-only remains the default and only path for the current MVP pass.

Scope when picked back up: per-person/Circle preferred channel settings (SMS, iMessage, WhatsApp, Email, Instagram DM, Facebook Messenger, Signal), configured in Circle/contact settings, never mandatory during onboarding or an urgent Going Quiet flow; a grouped delivery screen for non-SMS channels (e.g. SMS — sent / WhatsApp — continue / Instagram — continue / Email — continue), since Hold can prepare a message and hand off to a share/app flow but cannot auto-send through most third-party platforms. **Deferred, not cancelled — revisit once Core Journey ships.**

## Icon placement in the wordmark

Should the "held" icon (soft overlapping/embracing shapes) sit inside the "O" of the "Hold" wordmark, or stay as a fully separate mark? **Not yet decided** — worth testing both, since embedding it in the "O" could read as clever or could read as cluttered/hard to reproduce at small sizes; a separate mark is safer but less distinctive. Note this is about the small wordmark logo specifically, which stays static per `05-design-system/01-design-direction.md` — it's a branding question, not a motion one.

**Added context (2026-08-19), tied to the trademark question in `07-business/06-business-strategy.md`:** there's a long-term aspiration for Hold's logo/wordmark to become a culturally-recognised shorthand symbol — sending just the logo communicating "thinking of you, not gone" without accompanying text, similar to how an emoji functions (related to the instant-symbol-send idea below). This is contingent on Hold reaching meaningful adoption, not a buildable feature now — a brand-adoption outcome, not a near-term one. **Flagged explicitly: further brand-investment thinking here should wait on the existing Class 9 trademark clearance question, not proceed in parallel with it** — a live UK Class 9 registration conflict currently exists on "Hold" (Hold Platform Ltd, Malta-registered fintech).

## Optional Hold signature on template messages

See `03-design-experiments.md`. Beta hypothesis, not a decision.

## Optional account sign-in mechanism

**Decided in principle** (see `08-decisions/01-decision-log.md` for the account/auth model itself): no mandatory account for the core journey. **Not yet decided:** the exact mechanism for the optional lightweight sign-in used for Hold+ restore/future sync — likely Sign in with Apple (and Google equivalent on Android) rather than email/password, to avoid adding a password to remember, but the specific implementation hasn't been chosen.

## Error state copy

What Hold says when the native share sheet fails/is cancelled, SMS isn't available, or AI drafting times out. **Not yet written** — should follow the same voice principles as the rest of the app, not generic system error text. See `04-ux-content/05-onboarding-empty-states.md`.

## Library internal organisation — resolved 2026-08-20

**Resolved.** Circle-first confirmed as the organising structure — someone thinks "I need my Work message" before they think "I need my Reconnect template." Tapping a Circle reveals its saved template within Templates. Scope extended beyond Library alone: the same Circle-first structure applies consistently across Library, Reconnect, and Templates, not just one of them — a broader decision than the original proposal below, which only considered Library in isolation. See `08-decisions/01-decision-log.md`'s 2026-08-20 entry. **Decision only, not yet built** — reconciling the three surfaces to match is separate implementation work, not yet scoped or started.

Original proposal, for reference: organise by Circle first, then by message stage within each Circle (Going Quiet / Reassurance / Reconnect / Conversations expanding inline under a Circle selector). Alternative considered and not chosen: organise by stage first, Circle second.

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

## Additional Wider World channels — two future-spec ideas, none built

**Logged 2026-08-11. Future spec — not committed, not scoped for build.** Email out-of-office and Wider World status were built this pass (see `08-decisions/01-decision-log.md`) — these two additional channels were considered alongside them and are worth keeping on record, not built now. (A third channel considered alongside these, the text-to-speech voicemail greeting, is closed rather than deferred — see its own section below, not listed here.)

1. **Calendar auto-blocking** — automatically block out time on a person's calendar each morning while they're in Taking Time, until manually turned off. Primary benefit: passively communicates unavailability to teammates who share the calendar, without the person needing to explain directly — consistent with Hold's existing goal of reducing the burden of repeated explanation. Requires real calendar API integration (OAuth, ongoing sync) — a meaningfully bigger technical undertaking than a text field, deliberately scoped out of this pass.
2. **SMS auto-reply** — genuine native auto-reply is not available to third-party apps on either platform without disproportionate scope (see "Hold as default SMS handler" below, closed). If pursued at all, this would only ever be a ready-to-paste text fallback the person applies manually via their own phone's Focus/third-party auto-reply settings (iPhone: Driving Focus only; Android: requires a separate third-party auto-reply app) — not something Hold can trigger directly.

**Not yet decided:** whether either of these gets picked up as a future Wider World channel, or in what order.

## Text-to-speech voicemail greeting — closed, not deferred

**Closed 2026-08-19, correcting the 2026-08-11 "deliberately scoped out of this pass" framing above and originally used for this item too** — logged here specifically so it isn't quietly revisited as an open future-spec item without this context, same treatment as "Hold as default SMS handler" below.

Hold could generate a spoken audio file from typed status text, but no public API exists on either platform for a third-party app to set someone's actual carrier voicemail greeting. Would require the person to manually apply the generated audio themselves, or a much larger integration with a separate voicemail-replacement service (YouMail, Google Voice, etc.) — the same category of disproportionate-scope platform constraint already applied to native SMS auto-reply and default-SMS-handler status.

**Closed. Do not revisit without a materially different technical landscape** (e.g. a platform policy change) — this was rejected on the merits, not deferred for later.

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

**Flag added 2026-08-28:** if this is ever scoped for build, check its final shape against the new standing principle "Stay a private messaging tool, not a social platform" (`01-foundation/03-principles.md`) before building — this idea is the one named example in that principle, since regulatory messaging-app exemptions in emerging under-16 protection laws (see `09-research/global-architecture-scan-pass1.md`, Part G) depend on Hold not gaining social-media-style interaction beyond a user's own defined Circle contributing to that user's own flow. The v1 scope described below (pre-vetted phrase bank, attributed "from your circle" labelling, no visible feed) reads as compatible with that line; anything that grows beyond it should be re-checked, not assumed still fine.

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

**Extension logged 2026-08-31 — friend-designed display/Look & Feel.** A friend/family member could design the *display* (colour theme, warmth, visual style) on the user's behalf, distinct from the message-content contributions already scoped above. The same resolved logic from "Preview model" above applies directly: aesthetic choices are lower-risk to leave as a surprise (per the existing "aesthetic surprise is fine, content surprise is not" resolution), so this plausibly fits the "surprise" side of that model, not the "shown in advance" side, if it's ever built. Unscoped, future, not v1 — logged as an extension of this same idea, not a separate feature.

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

**Resolved 2026-08-13.** Confirmed by direct instruction: collapsed by default, correcting the 2026-08-12 entry, which is superseded (not wrong — a legitimate earlier decision point, per this book's standing convention for same-topic reversals). `oooExpanded`'s initial state in `app/return/reconnect.tsx` is `false`. A new exit-time nudge (see `01-core-journeys.md`'s Reconnect section) now surfaces genuinely unresolved Wider World state at the point of leaving instead of defaulting the section open on every visit.

## Two-tier nav bar rule — does swipe-back (gestureEnabled) also need revisiting?

**Resolved 2026-08-13.** Confirmed by direct instruction: yes — swipe-back on Going Quiet and Reconnect is now unconditional (`gestureEnabled: false` statically), matching the four already-static completion/transition screens, not gated on composition state anymore. The explicit Back button is unaffected; only the gestural path was removed.

## Send an Update drawer — are ungrouped audience members reachable at all?

**Resolved 2026-08-13 — confirmed moot, not a gap.** Direct confirmation: every contact ever added to Going Quiet becomes its own Circle (even a Circle of one) — there is no "individual, non-Circle" category in the system as designed. The Update drawer's Circles-only scope was already correct.

## Circle-of-one convention not applied to Reconnect's own "+" (mid-flow add)

**Logged 2026-08-13, surfaced while confirming the ungrouped-audience question above and building "Add to Going Quiet."** The confirmed design — every Going Quiet contact becomes its own Circle — is now followed by the new "Add to Going Quiet" drawer (`app/(tabs)/index.tsx`'s `createCircleFromPickedContact`, `addCircleToAudience`) and already true of `create/people.tsx`'s own "+ New Circle." Home's own older ungrouped-adding mechanic (`addToAudience`) was this new drawer's only caller and has been removed entirely, not left dormant. **But Reconnect's own separate "+" (`addToReconnectingAudience`, mid-flow) still adds the person ungrouped, not as a Circle** — a genuinely separate function from the others (it targets a period that's no longer the currently-open one by the time Reconnect is on screen), not touched by the instruction that confirmed the Circle-of-one design, so left as-is rather than silently also changed.

**Not yet decided:** whether Reconnect's own "+" should be brought in line with the now-confirmed Circle-of-one convention, or is deliberately different because a full Circle feels like more ceremony than a mid-Reconnect add calls for.

## Taking Time drawers still need the real docked bar (Template + pills)

**Logged 2026-08-13.** `TakingTimeUpdateDrawer.tsx` and `AddToGoingQuietDrawer.tsx` (built earlier the same day) use a plain text box, deliberately, since the template-editing interaction was still being finalised at build time. That interaction is now specified (green-highlight Template/pill insertion, `DockedInputBar`), but upgrading both drawers to use it wasn't done in the same pass — `DockedInputBar` depends on `KeyboardStickyView`, which has never been exercised inside an `Animated`-driven bottom sheet in this codebase, an untested combination not folded into an already-large pass.

**Not yet decided:** nothing design-wise — this is purely sequencing. The upgrade itself (swap the plain `TextInput` for `DockedInputBar`, wire each drawer's own per-Circle template into the new `template` prop) is expected to be straightforward once the keyboard-in-a-sheet interaction is confirmed to work.

## DockedFieldPreview's sentence-pill row — remaining call sites

**Logged 2026-08-13.** The new pill row on `DockedFieldPreview` was wired into Going Quiet's and Reconnect's own message-field previews only — the two most central compose surfaces. Not yet threaded into: Library's per-person Conversations fields, Manage Circles' own fields, email out-of-office, wider-world status, or Personalise's reply box.

**Not yet decided:** whether all of these should get the pill row (matching the docked bar's own fully-automatic, app-wide scope), or whether some of them are the "non-message-shaped field" case the row was deliberately made opt-in to exclude (e.g. a Circle name field, matching `aiAmend`'s own existing message-shaped-content-only scoping).

## Nav bar blur needs a native rebuild before it can be evaluated at all

**Logged 2026-08-13, confirmed on-device, not theoretical.** A diagnostic (temporary `intensity={100}` + an unmissable solid tint on `BottomTabBar.tsx`'s `BlurView`, reverted immediately after) showed the tint painting correctly but zero blur softening on the text underneath — the specific signature of the native `ExpoBlur` module not being present in the currently-running app binary, not of `intensity={40}` simply being too low a value. Checked directly: no config-level fix exists — `expo-blur` has no config plugin, `app.json` needs nothing added for it, and the Podfile's `use_expo_modules!` autolinking is already correctly picking up `ExpoBlur` at the source level (confirmed in `ios/Podfile.lock`). The gap is specifically that no binary has been *compiled* since the module was linked — force-quit/reopen relaunches the existing binary; only an actual rebuild (`npx expo run:ios` or an Xcode build) produces a new one.

**Not yet actioned — deliberately deferred, per direct instruction, to be batched with other pending native-level changes** rather than done in isolation just for this. See `hold-app`'s own `docs/09-decision-log.md` for the full diagnostic trail.

**Not yet decided (blocked on the rebuild above, not a design question):** whether `intensity={40}` is actually the right value once blur genuinely renders — that tuning question was raised earlier the same day and still has no on-device answer, since blur has never actually been visible to evaluate against.

## Box B pill-insertion — hypothesis only, not a confirmed fix

**Logged 2026-08-13.** On-device testing found sentence pills correctly inserting text on Box A (`DockedFieldPreview`) but doing nothing when tapped on Box B (`DockedInputBar`, the active docked bar) — a real, reported inconsistency between two surfaces meant to share the same insertion mechanic. Re-reading `onPillPress`/`highlight.insertBlock` found no separate code bug — the logic looks correct in isolation and matches Box A's own working version. Given Box B's overlay rendering was *also* confirmed broken at the same testing moment (see the scroll-architecture entries in `01-core-journeys.md`), the leading hypothesis is that pill taps were updating the underlying message correctly the whole time, just not visibly, because the broken overlay wasn't rendering the result.

**Not confirmed.** This is a hypothesis, not a diagnosis — there's no way to distinguish "data updated but not shown" from "nothing happened at all" without an actual device. Needs explicit on-device re-verification once the rebuilt scroll architecture is confirmed working, not assumed resolved as a side effect of that fix.

## Save to Library reported missing on both docked-bar boxes — cause unconfirmed

**Logged 2026-08-13.** On-device testing reported "Save to Library" absent on both Box A (`DockedFieldPreview`) and Box B (`DockedInputBar`), despite both being verified-by-reading as correctly wired the same session. No code fault found on re-reading either box's gating logic — both are, and always have been (Box A's own gating predates this session), scoped to a single-Circle selection only; a multi-Circle combination has never had a Save-to-Library affordance, only Template (which has always supported combinations).

**Not yet decided:** whether this was a real bug (in which case it hasn't been found yet and needs a fresh look) or the person was testing with a Circle combination selected, where no Save affordance has ever existed by design. Needs the exact selection used during that specific test to resolve either way — not assumed to be either.

## Staged content richness (Taking Time vs. Reconnect) — proposed, pending sign-off

**Logged 2026-08-19.** Proposed: Taking Time notifications/copy stay validation-and-permission only; fuller opt-in content (story, poetry, cultural/research material) becomes available from Reconnect onward via a Transition-screen toggle. Reasoning recorded in `01-decision-log.md`'s 2026-08-19 row.

**Proposed, not yet explicitly confirmed — treat as a strong candidate decision pending sign-off, not settled.**

## "You're reconnected" copy for Care/Professional contacts with no real prior distance

**Logged 2026-08-19.** The main "You're reconnected" question (single friend/single message, standalone Conversations use) is resolved — see `01-decision-log.md`'s 2026-08-19 row. This is a separate, narrower remaining sliver: whether the same copy fits Conversations use with Care/Professional-category contacts, where there may be no real prior distance to "reconnect" from in the first place. **Not resolved.**

## Daily-check-in vs. weekly-rest-day model for a future "tick each day" feature

**Logged 2026-08-19.** No evidence found either way in the current research base for which cadence (a daily tick/check-in vs. a weekly rest-day model) better fits a future tracking feature. **Flagged as needing user testing, not a literature-based answer** — don't build against an assumed answer here.

## Opt-in daily reassurance notification — viable, or does it conflict with the no-re-engagement-notification rule?

**Logged 2026-08-19.** Whether an opt-in daily reassurance notification is viable at all, or conflicts with the app's existing no-re-engagement-notification rule even when gently framed and explicitly opt-in. **Not resolved.**

## Music/playlist feature — scope breakdown, mixed leanings across sub-categories

**Logged 2026-08-19.** Four distinct sub-ideas, not one feature, with different leanings:
- Official Hold-curated playlists — leaning good.
- User-submitted-to-an-approved-pool, with future curators — leaning good.
- Public/followable playlists — **leaning against**, conflicts with Hold's low-visibility ethos and adds UGC-moderation burden with unclear benefit.
- Somatic/sound-frequency content — flagged as a separate, weaker-evidence category from general music-listening research (see `02-research/07-extended-evidence-base.md`'s sound-frequency section) — should not be bundled with the general music research in future copy or specs.

**Not resolved as a whole feature** — the sub-category leanings above are directional, not a committed scope.

## Multi-recipient single-confirmation compose screen (per Circle)

**Logged 2026-08-19.** `MFMessageComposeViewController` supports adding multiple recipients to one compose call, resolved with a single confirmation tap rather than today's per-recipient confirmation loop — worth considering as a UX improvement to the existing sequential per-Circle send. **Tradeoff not yet resolved:** doing this creates one shared group thread (recipients see each other and each other's replies), breaking the individual/BCC-style separation the current sequential send deliberately preserves (see `01-decision-log.md`'s 2026-08-11 delivery-model row). Needs a decision on whether reduced confirmation friction is worth losing that separation before this goes into a build message — likely only applicable to Circles already using the "send as group" opt-in, not the default individual-delivery case, where it would directly undo the existing privacy premise.

## Instant symbol send (one-tap, lightweight)

**Logged 2026-08-19.** A faster alternative to a full Going Quiet message: one tap sends a small fixed asset (logo/symbol, possibly brief fixed wording) via the existing per-Circle send infrastructure, for moments too low-capacity even for the current flow. Buildable now on existing Circle/queue architecture. **Not yet scoped or decided** — needs thinking through against the no-pressure/statements-over-questions rules (does an unexplained symbol read as reassuring, or as confusing/alarming, to a recipient who doesn't already know what Hold is?), and against the fact that the idea depends on the recipient already recognising the symbol — related to the wordmark/symbol-recognition question below.

## "On Hold" presence indicator (cross-user visibility) — open, constrained idea, not rejected

**Logged 2026-08-19 — from a separate design session (2026-08-17) not previously written into hold-book; confirmed as real content, distinct from the automatic cross-platform status-syncing non-feature already logged in `01-decision-log.md` (different features, different constraints, not to be merged).** See `01-decision-log.md`'s 2026-08-19 entry for the full assessment and the visibility constraint. Summarised here as the open question it actually is: if this is ever picked up, it must only ever be visible to someone explicitly included in a Going Quiet Circle — never ambient, never discoverable, never visible app-wide. Not a closed/rejected idea like TTS voicemail generation — genuinely open, but gated on that visibility rule being checked and kept intact, not re-litigated from scratch, whenever it resurfaces.

## AI reply-timing signal: quiet-period duration vs. friend-message timestamp

**Logged 2026-08-19.** When AI drafting for Conversations/Reconnect replies is built, what "elapsed time" should the model use to calibrate tone (amount of apology/context)? **Current leaning:** use the Hold period's own duration (`HoldPeriod` start/end, already tracked for Quiet History/Patterns) rather than the timestamp of the specific friend message being replied to — it's already-known, factual data requiring no new capture (satisfies `06-privacy-security/02-ai-boundaries.md`'s rule against inferring facts not supplied by the user, since it *is* supplied, just not re-asked), avoids trusting a manually-entered date on a pasted message (error-prone, extra friction at low capacity) or reading message metadata Hold doesn't have access to (pasted text only, no inbox integration), and avoids a privacy-minimisation question (storing a timestamp against pasted message content) similar in kind to the Quiet History exception in `docs/03-privacy-model.md`.

**Not formally decided** — no AI drafting is built yet (`draftService.ts` is currently fully local/template-based), so this doesn't block anything today. Revisit when AI drafting moves from boundary doc to implementation.

**Deferred, tracked separately:** capturing the friend-message's own timestamp (distinct from quiet-period duration) as a future, addable feature — e.g. if "they messaged on day 2 of a 3-week Hold" vs. "they messaged yesterday" turns out to meaningfully change what a good reply looks like. Not scoped, not costed, just not lost.

## Lapsed/dormant backup account retention, now that backup isn't Hold+-exclusive

**Flagged 2026-08-21.** `06-privacy-security/04-content-retention.md`'s "Lapsed/dormant Hold+ backup account retention" section (30-day grace period, 6–12 month dormant window before deletion) was scoped entirely around backup being a paid, Hold+-only feature — that premise is no longer accurate, backup is now free for everyone. Unresolved whether the same tiered model just applies once "lapsed subscription" is swapped for a free-tier-appropriate trigger, or whether free-tier backup needs its own rethought policy from scratch (a free account has nothing to "lapse"). Explicitly not decided here — see that section for the full flagged note; do not build against either answer without checking first.

## Hold's minimum age — resolved 2026-08-28, closing a stale blocker

**Logged 2026-08-27, resolved 2026-08-28.** Hold will not set a minimum age or age gate. No minimum age, universal highest-protection standard applied instead of age verification — this is the ICO's own sanctioned alternative path under the Age Appropriate Design Code's age-assurance standard (Standard 3), not a workaround adopted for convenience. See `01-decision-log.md`, 2026-08-27, and the full standard-by-standard assessment in `06-privacy-security/06-aadc-compliance-review.md`, where Standards 3 and 6 have both been updated to reflect this as resolved rather than open. When Terms of Use are drafted with the solicitor, they should state the no-minimum-age position plainly, so published policy matches actual behaviour from day one.

## Analytics SDK: use one, or explicitly decide not to

**Logged 2026-08-27.** Hold currently has no confirmed analytics approach. Two options: (a) no analytics SDK at all — stronger privacy claim, zero build cost, matches privacy-by-design philosophy; (b) a specific SDK for defined anonymous metrics only, scoped and justified. Needs deciding before MVP ships. Bethany to decide; flag back for spec once chosen if (b). Note: the "did this help?" feedback data (below) and the pilot/beta evidence-gathering spec (below) may need their own lightweight storage path if (a) is chosen, rather than piggybacking on a third-party SDK.

## No formal chronic-illness accessibility standard exists — resolved/closed

**Researched and closed 2026-08-27.** Researched whether a formal chronic-illness-specific accessibility certification exists, distinct from general W3C/WCAG standards. None does — chronic-illness accessibility is addressed through practical UX choices (low-effort interactions, reduced motion, generous timeouts, no pressure language) rather than a certifiable standard. Hold's existing principles (low-capacity usability test, warmth bar, no counts/pressure language) are the appropriate substitute, and the eventual accessibility audit (already logged as unstarted, Part 4/Step 11 of master status) should be treated as the Usability & Accessibility groundwork relevant to any future ORCHA review (see `09-research/nhs-orcha-accreditation-pathways.md`), not a separate concern.

## Public-facing Safeguarding Policy page — blocked

**Logged 2026-08-27.** Distinct from the internal `06-privacy-security/03-safeguarding.md` (policy source of truth for reviewers). A short, plain-language public Safeguarding Policy page — no crisis-response promise, redirect to trusted adults/professionals, legal disclosure obligations under duty of care — following the structural template at calmharm.stem4.org.uk/safeguarding-policy. Blocked until `06-privacy-security/03-safeguarding.md` has clinical and legal sign-off. This documentation discipline (internal policy + public summary, kept in sync) is also directly what DCB0129's Clinical Safety Case Report and any future ORCHA Clinical/Professional Assurance review would expect to see — see `09-research/nhs-orcha-accreditation-pathways.md`.

## Lightweight beta/pilot evidence structure

**Logged 2026-08-27, scoped future spec, not yet build-ready.** Propose a lightweight pilot: a small beta group of real target users, structured feedback survey before and after a defined period of use, informed by a genuine co-creation conversation with a few real users about priorities (not just a survey — see the Calm Harm/HMA case study in `09-research/nhs-orcha-accreditation-pathways.md`, which used structured co-creation sessions with clinicians, young people, and safety officers to shape its roadmap). Purpose: build real evidence of Hold's value, independently worthwhile for App Store credibility and press, and directly builds the Evidence pillar ORCHA's review scores against, should that be pursued later. **NOT contingent on pursuing ORCHA/NHS accreditation.**

## "Did this help?" evidence prompt, History-first — see "Spec-complete, awaiting build" section

**Moved 2026-08-27.** This entry now lives in the dedicated "Spec-complete, awaiting build" section near the top of this file, not here, since the trigger logic has since been refined to spec-complete status and it's tracked separately from genuinely undecided questions. Kept as a pointer at this original location so a search for it here still finds it.

## AI disclosure (EU AI Act Article 50) — near-term build item

**Logged 2026-08-28**, from `09-research/ai-act-and-remaining-compliance.md`, Part A. The EU AI Act's Article 50 transparency requirement has applied to all AI systems, not just high-risk ones, since August 2025: users must be clearly informed when they're interacting with AI. Unrelated to, and not waiting on, the much harder open question of whether Hold's safeguarding classifier counts as high-risk under Annex III (see the same research file) — this is a simple, low-effort item that should ship on its own timeline.

**What it is:** a simple, clear in-app disclosure that AI is used for (a) message drafting assistance and (b) safeguarding detection. Not yet written or placed — needs its own short spec pass (where it's surfaced — onboarding, Settings/About, or both — and the actual copy, following `04-ux-content/02-voice-and-language.md`'s voice principles).

## UK Online Safety Act (and likely-equivalent EU/Australia/Singapore/UAE frameworks) — Reconnect Conversations hosting question

**Logged 2026-08-28**, from `09-research/ai-act-and-remaining-compliance.md`, Parts C and F. The OSA doesn't broadly exempt private messaging apps (WhatsApp is named as clearly in-scope in official guidance) — the determining question is whether a service *hosts or facilitates* content exchange between users, versus merely acting on content handed off from external channels it doesn't control.

**Specific feature flagged:** Reconnect Conversations, where a friend's message — received via SMS/WhatsApp/email, then manually pasted in by the user — is used to draft a reply Hold hands back to the user to send via that same external channel. Hold never receives, routes, or transmits the friend's message itself. Whether this is a sufficient distinction to place Hold outside OSA scope (and likely the equivalent EU DSA, Australian OSA, Singapore, and UAE frameworks, which appear to share the same hosting/facilitating test — see the research file) is the actual question for the solicitor, not assumed either way here.

**Not resolved.** One of four items on the consolidated solicitor priority list in `09-research/ai-act-and-remaining-compliance.md`.

## Two portable UX choices from comparable-app research (Calm Harm)

**Logged 2026-08-27, scoped future spec.**

(a) **Hide specific articles/topics.** Research section: allow hiding specific articles/topics a user finds unhelpful or triggering, rather than only a blanket on/off — mirrors Calm Harm's per-activity hide option, adapted to Hold's content model.

(b) **A lighter protection step for one sensitive area only.** Consider whether any specific sensitive area (e.g. health notes within Patterns) warrants its own lighter protection step, separate from the rest of the app staying frictionless — mirrors Calm Harm's approach of removing the app-wide passcode but keeping one on its most sensitive section only. Not yet scoped as a decision, flagging the pattern for consideration.

## "Bridge person" / trusted intermediary

**Logged 2026-08-31**, from an extended external design/research session (2026-08-19 onward) — see `08-decisions/01-decision-log.md`, 2026-08-31. A designated contact who can reassure a person's wider circle ("they're safe but very low capacity, they still care, they'll reconnect when able") without the absent person having to communicate individually. Real potential value, but sits in direct tension with the existing privacy model (metadata only, no third-party sharing by default) — a bridge person necessarily knows more than the people they're reassuring don't. Needs its own scoped decision on who can hold this role, what exactly they're permitted to know versus relay, and how it's revoked. **Constrained directly by `06-privacy-security/07-reconnection-safety-requirements.md`, sub-requirement 6:** mutual contacts or "bridge people" must not be recruited without explicit, specific consent — this requirement governs the feature's eventual design, not the reverse. Not to be folded into the main Reconnect flow as a quick addition.

## A dedicated "recipient view"

**Logged 2026-08-31**, same source as above. Designing for the person waiting, not just the person withdrawing (what silence means, when to worry, whether an emoji reply is enough, permission to protect their own emotional boundaries). A genuine scope expansion beyond everything currently built, which is entirely oriented around the withdrawing person. Log as a deliberate future-phase decision requiring its own product scoping, not an assumed extension of Reconnect. Governed by `06-privacy-security/07-reconnection-safety-requirements.md` throughout — a recipient view is exactly the kind of surface that could leak a safety decision if not audited against it carefully.

## A lightweight, proactive "relationship understanding" exchange

**Logged 2026-08-31**, same source as above. Letting two people establish, before distress fills the silence with interpretation, what silence means for each of them, how long is comfortable, whether contact during Taking Time is welcome. Interesting preventative idea, unscoped.

## AI credit pack draft allowance

**Logged 2026-08-31.** The £2.99 AI credit pack (`07-business/02-pricing-principles.md`) has never had an actual draft-count number attached — price only. A design-session discussion suggested 20-25 drafts as a starting point, reasoning: each draft costs well under £0.01 to generate, so there's no cost-based ceiling forcing a low number; 20-25 was suggested as roughly matching a typical month of Hold+-equivalent use, easy to explain to a user, without being an arbitrary-feeling figure. **Not decided** — flagged as needing a real number before this ships, ideally checked against actual usage data once available rather than picked from reasoning alone.

## Conversational multi-turn AI voice exchange (Hold+, future)

**Logged 2026-08-31.** Distinct from and further out than the free, already-scoped voice dictation (on-device speech-to-text feeding existing text-entry points, already built into the docked bar). This is a genuinely different feature: an actual back-and-forth voice exchange with the AI (e.g. AI asks a clarifying question, user responds by voice, possibly several turns before a draft appears) rather than a single dictate-then-draft step.

Confirmed Hold+ if built, given real added API cost per turn versus a single draft call. **Flagged tension:** Hold+ AI is currently positioned as unlimited/no caps (`07-business/02-pricing-principles.md`). A multi-turn voice feature could be meaningfully more expensive per use than text drafting, which may argue for its own separate, visible usage allowance — which itself sits against Hold's own no-counts/no-pressure-language principle. **Not resolved:** whether this stays under the same unlimited umbrella (simpler, more values-consistent, but exposes real cost risk if it gets popular) or gets its own capped allowance (protects margin, but needs careful, gentle framing to avoid reading as a countdown/pressure UI). Each safeguarding-check pass would also need to run per turn, not just on the final drafted text — carries the same requirement as the existing free-text safeguarding layer, just applied repeatedly within one exchange.

Genuinely future-future — sequenced after the accessibility audit, OS-level voice navigation, and free speak-once dictation, all of which come first.

## Journaling app connection (future, unscoped)

**Logged 2026-08-31.** Newly raised, no prior discussion anywhere in this project. Direction undefined — could mean importing/reading entries from an existing journaling app, exporting Hold data into one, or something else entirely. Tier (free/Hold+) undecided. Needs actual scoping (which app(s), what data, what direction) before it's more than a name on a list.

## "Connected Accounts" naming collision

**Logged 2026-08-31.** The optional lightweight sign-in for Hold+ restore/multi-device sync (already an open question above re: exact mechanism — Sign in with Apple likely) creates a naming problem not yet resolved: "Connected Accounts" already exists as a Settings-drawer row (currently a "Coming later" stub, originally meant for Wider World's email/Gmail-Outlook out-of-office linking — see `04-ux-content/04-navigation-architecture.md`'s Settings panel structure). These are two different kinds of "connection" — one is external-service linking for a feature, the other is an account/identity mechanism for sync/restore. Reusing "Connected Accounts" for both risks real user confusion. **Not decided:** rename one of them, keep both under one row with sub-sections, or something else. Needs resolving before either feature is built, not after.
