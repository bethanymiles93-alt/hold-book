# Onboarding, empty states and permissions

None of this was previously specified anywhere in the book — "Clear onboarding" appeared as a single unexplained bullet in `03-mvp-requirements.md`, and no empty state or permission-request moment was described at all. This is a genuine MVP gap, not a nice-to-have.

## First launch

**Decided:** a single welcome screen, not a carousel, before the person does anything else — this resolves the earlier open "drop straight in vs. brief screen" question in favour of the brief screen, since the product's purpose isn't self-evident from a bare "Going Quiet" button alone.

**Final copy:**

> **Welcome to Hold.**
> We built Hold because staying in touch can feel impossible when you don't have the capacity, whatever the reason. Hold helps you keep your circles in the loop, rest without guilt, and reconnect in your own time.
>
> It also helps the people who care about you, so they're not left worrying in silence.
>
> We'd love to hear what you think. If Hold helps you, we'd be grateful if you shared it with someone who might need it too.
>
> **Button: Get started**

Deliberately diagnosis-agnostic ("whatever the reason") rather than naming a specific condition, matching the positioning already established in `07-business/06-business-strategy.md`.

After this single screen: straight into Circle creation as part of the natural Going Quiet flow, per the existing decision. **No account/backup prompt screen here** — that stays in Settings only, not onboarding, per the account/auth model above. A related, softer version of "no one should be judged by their illness or its limitations" belongs in the About panel's Mission & Values content, not this screen — a values statement fits better somewhere the person chooses to read it.

## Permissions

Two permissions Hold plausibly needs, and when to ask for each — **not yet decided**, but the principle is clear from `02-research/02-low-capacity-design.md` (avoid long onboarding, avoid requiring a complete explanation up front):

- **Contacts** — only requested at the point the user actually adds someone to a Circle via the native picker, not before. Never bulk address-book access (already a hard requirement elsewhere in the book).
- **Notifications** — only requested at the point a feature that needs them is used (e.g. the optional Taking Time nudge), not on first launch, since Hold's default is no engagement notifications anyway.

Ask in context, not in advance — the permission request should appear because of something the user just tried to do, not as a batch of upfront asks before they've done anything.

## Empty states

Needed and not yet written:

- **Home, before any Circle exists and before Going Quiet has ever been used.** Shouldn't feel broken or unfinished — probably folds into the "first launch" question above rather than being a separate empty dashboard.
- **Conversations, with nothing in it.** Since Conversations is a standalone destination usable without ever going quiet, this needs calm, non-empty-feeling copy — something in the spirit of "Nothing here yet. When you need help replying to someone, this is where you'll find it," not a blank list or a sad-state illustration.
- **History, with no data yet.** Similarly should read as a place that will hold something meaningful over time, not as a failure state — "Your quiet periods will appear here once you've used Hold" rather than an empty chart.

## Error states

Not yet specified anywhere. At minimum: what happens if the native share sheet fails or is cancelled, what happens if SMS sending isn't available on the device, and what happens if AI drafting fails (timeout, no connection) — the failure copy should follow the same voice principles as the rest of the app (`04-ux-content/02-voice-and-language.md`), not a generic system error message.

## Account and authentication model

**Decided:** no account required for the core app, ever. Circles, templates, History and Patterns are stored locally/encrypted on-device — an account isn't what makes saving possible day-to-day, it's specifically for cross-device sync and restoring data after a device loss, which are different problems from "can I save a template."

**The real trade-off of staying account-free is data loss risk**, not lack of saving — if a phone is lost, broken or replaced with nothing backed up, Circles, templates and Quiet History (framed elsewhere in this book as "self-knowledge") go with it. That's the specific risk worth weighing, not day-to-day functionality.

**Resolution:** onboarding stays completely account-free — straight into Circles/Going Quiet, nothing to sign up for. Settings offers a lightweight, opt-in "back up my data" option separately, not during onboarding. Prefer Sign in with Apple (and the Google equivalent on Android) over email/password — this isn't just lower-friction, it can be genuinely more private than email/password, since Hold never needs to collect a real email address or store a password at all. "No account" isn't automatically more private than a well-implemented optional Sign in with Apple; worth not assuming that by default.

Subscriptions work via App Store/Play receipt validation regardless of account status, so Hold+ doesn't force the account question either.

The exact sign-in mechanism implementation is tracked as a smaller remaining item in `08-decisions/04-open-questions.md`; the model itself (account-free by default, optional lightweight backup) is decided.
