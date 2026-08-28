# AI boundaries

## Role of AI

AI may help users reduce composition effort. It must remain an assistant, not an autonomous participant in the relationship.

## Allowed

- Draft from user-selected intent
- Shorten or soften user-written text
- Offer tone variants
- Help prepare a return message
- Explain why a draft may sound unclear or overly apologetic

## Not allowed

- Auto-send
- Invent a diagnosis or reason
- Infer relationship facts not supplied by the user
- Manipulate the recipient
- Claim certainty about the recipient’s feelings
- Train on private messages by default
- Generate crisis or medical advice as though Hold were a clinician

## User controls

- AI use must be disclosed.
- The user can write without AI.
- The user sees and edits every draft.
- Sensitive content should be minimised before sending to a model.
- Retention and provider terms must be documented.

## Implementation approach

**Connect to an existing model via API, don't build or fine-tune one.** For a solo-built MVP, prompting a strong general model well gets nearly all the value of fine-tuning at a fraction of the cost and complexity, and fine-tuning needs a large curated dataset and ongoing upkeep that isn't worth it before real usage data exists.

- **Separate system prompts per surface**, not one generic prompt behind every "AI Help" button — a Going Quiet prompt, a Reassurance prompt, a Reconnect prompt, a Conversations reply prompt, each carrying the relevant rules from this file and from `04-ux-content/02-voice-and-language.md` (never guilt, never diagnose, permission over pressure), plus the relevant Circle/relationship context and current journey stage.
- **Model choice by task, not one model for everything:** a cheaper, fast model (e.g. Claude Haiku 4.5) for the safeguarding detection layer (`06-privacy-security/03-safeguarding.md`) — a classification task, not creative writing — and a stronger model (e.g. Claude Sonnet) for actual message drafting, where tone quality genuinely matters.
- **Cost reality (checked July 2026, £ at ~$1.33/£1):** a typical short draft (roughly 800–1,500 input tokens, 200–400 output tokens) costs well under £0.01 on Sonnet-tier pricing (Sonnet intro rate ≈ £1.50 input / £7.50 output per million tokens through August 2026, rising to ≈ £2.25 / £11.25 after). AI-assisted drafting is Hold+-only, with no free allowance (see `07-business/02-pricing-principles.md`) — at this per-draft cost, even a generous per-install monthly usage ceiling of 20 drafts costs under £0.15/month against a paying subscriber, comfortably inside Hold+'s pricing.
- **AI personalisation** (writing-style learning, saved-messages-as-context) should work by injecting a few of the user's own saved templates into the prompt as style examples at generation time, not by training or fine-tuning on them.

### Built: the server-side proxy (`worker/` in hold-app)

The app has no backend and no user accounts, which shaped every choice below:

- **Hosting: Cloudflare Workers**, chosen over an always-on server (fixed monthly cost regardless of traffic, a poor fit for this app's episodic usage) and over Vercel/Lambda (more setup complexity, or a product mismatch, for a solo builder with no existing account elsewhere). Free tier comfortably covers MVP volume; Workers KV solves the usage-metering need below without a second product.
- **Metering built from day one, not retrofitted.** With no accounts, there's no server-verifiable way to check Hold+ entitlement, so the client-side gate in `draftService.ts` isn't the only protection needed — the practical backstop is an anonymous per-install UUID (generated once, stored in `expo-secure-store`, never a name or phone number) that the Worker counts against in KV, as a monthly safety cap rather than a free-tier allowance. This exists in the first version of the proxy, not added after launch, because it's what makes the next point acceptable at all.
- **App-to-proxy auth is a bundled shared key, not a strong secret** — with no accounts, there's no cleaner option at this stage. It's explicitly *not* the real protection; the monthly safety cap and per-install rate limit are. A determined attacker extracting the key from the app binary is bounded by the same cap everyone else is.
- **Non-AI route confirmed still in place**: `draftService.ts`'s local templates are the fallback on any proxy failure — unconfigured, network error, rate limit, timeout, provider error — never removed.

### Built: "Amend with AI" (Hold+) — a blend, not a regenerate

A distinct request shape from the plain per-surface draft above: the client additionally sends the message box's current content (`existingMessage`) and whatever the user typed into the amend prompt (`additionalContext`). The system prompt gets an extra instruction block only for this request shape — preserve wording/tone/structure that still fits, edit only what the new context makes necessary, never discard the existing message for an unrelated one. Gated on a local Hold+ flag (`holdPlusService.ts` — a placeholder dev/test toggle today, swappable for real entitlement logic later); absent entirely for free users, never greyed out or shown-then-locked. Manual editing of the box is always available regardless of Hold+ status — AI is additive, never the only way to change a message.

### Planned, logged 2026-08-11 — NOT YET BUILT: AI drafting quality bar

Two requirements for draft quality, neither implemented yet:

- **Personalisation via style reference.** When generating a draft, pull 2–3 of the user's most relevant saved templates (same Circle if available, otherwise general) and include them in the prompt as style reference, instructing the model to match the person's own natural phrasing. This is a more specific version of the "AI personalisation" line already in the bullet list above ("should work by injecting a few of the user's own saved templates into the prompt as style examples at generation time") — that line stated the principle; this adds the concrete selection rule (2–3 templates, same-Circle-first) that was previously unspecified.
- **Explicit anti-AI-phrasing quality requirement.** Every surface-specific system prompt should include a stated instruction to actively avoid generic AI-sounding phrasing (e.g. "I hope this message finds you well," excessive hedging, overly formal structure) as its own stated requirement, not assumed as a side effect of general "write naturally" instructions. None of the built system prompts referenced above currently carry this as an explicit, separate instruction.

### Built: AI memory (Hold+) — two-layer, both-must-consent

A separate opt-in on top of Amend with AI, not a default behaviour of it. Layer 1 is a standing "Remember helpful details" toggle (off by default, set in the Hold+ area, never an in-the-moment prompt during Going Quiet or Reconnect). Only when Layer 1 is on does the client set `memoryCaptureEnabled: true` on an Amend-with-AI request — which adds a further instruction asking the model to end its response with an optional, tightly bounded note (under 15 words, a durable factual detail only, explicitly never the user's psychological/emotional state) on its own delimited line, parsed out server-side before the draft is returned to the client. No note is ever requested, extracted, or stored unless Layer 1 is explicitly on. Full consent/retention/deletion model: `docs/03-privacy-model.md` (in `hold-app`), "AI memory."
