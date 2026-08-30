# Universal web page and acknowledgement mechanism

**Status:** Spec, not built. From an extended external design/research session (2026-08-19 onward), handed to this repo 2026-08-31. See `08-decisions/01-decision-log.md`, 2026-08-31. Governed throughout by `06-privacy-security/07-reconnection-safety-requirements.md` — nothing on this page may violate that requirement.

## Why this exists

Solves four problems: recipients don't need Hold installed; the glyph (`05-design-system/03-glyph-and-state-system.md`) has somewhere to be explained in full; current permissions can be updated without repeatedly sending long messages; recipients can acknowledge without starting a conversation.

## What the page shows — and what it must never show

**Shows, only what the Hold user selected to share:**
- The glyph and its plain-language meaning ("Bethany is on Hold — her capacity for messages is limited. Messages are welcome, but replies may not come.")
- Any optional layer the user chose to include: "this is about my capacity, not our relationship" / practical-or-time-sensitive-only guidance / "please don't call" / "no return date is currently known" / "no response is needed" / "I may start from current messages rather than the backlog when I reconnect."

**Must never show, under any configuration:**
- Activity tracking or "last seen" information.
- A countdown to any date.
- A social feed or any content beyond this one status.
- Recipient accounts, or any pressure to install Hold.
- Medical information, unless the user has deliberately and specifically chosen to share it.
- Visible numbers of other recipients, or any indication of who else has been contacted.

## Critical privacy fix — link-preview metadata leakage

**The risk:** when a Hold link is shared inside WhatsApp, iMessage, Slack, or similar apps, those platforms automatically fetch the page to generate a preview card — this happens the moment the link is pasted into a chat, before any human clicks anything. If the page's title/description metadata contains actual status content, that content becomes visible as a preview snippet to **everyone in a group chat**, including people who never opened the link and were never intended to receive that information. This is a materially bigger and less consensual disclosure than the rest of this specification carefully protects against.

**Required fix:**
- The page's `og:title`, `og:description`, and any other metadata consumed by link-preview generators must contain **only generic, non-revealing text** — e.g. "A message from Bethany" or "Hold status" — never the actual status, meaning, or permissions content.
- The real content must only render once a human has actually opened and loaded the page as a genuine visit, not as part of automated preview generation.
- Verify this specifically against major platforms' preview-fetching behaviour (WhatsApp, iMessage, Slack, Discord) before launch — these differ in exactly what they fetch and cache, and caching means a stale or incorrect preview could persist even after the underlying status changes.

## Acknowledgement mechanism — explicit button press only, never automatic

**The risk this guards against:** messaging apps, security scanners, and link-preview generators frequently open/fetch links automatically. If merely loading the page counted as acknowledgement, Hold would generate false acknowledgements and effectively create a hidden read receipt — a serious violation of the spirit of the whole feature, and of `06-privacy-security/07-reconnection-safety-requirements.md`'s "no read receipt may reveal that a return request was viewed" sub-requirement.

**Required flow:**
1. Recipient taps the Hold link. The universal page opens.
2. Recipient sees status and permissions (per "What the page shows" above).
3. They may press an explicit button: **"◉ Hold this — no reply needed."**
4. Only this explicit press registers as acknowledgement.
5. The Hold user sees this reflected only in that specific person's connection view (per `04-ux-content/06-state-architecture-and-memory.md` — never in an aggregate list), and only if they've chosen to receive acknowledgements at all.

**Additional required safeguards:**
- Acknowledging generates no push notification to the sender unless the sender has explicitly opted in.
- The recipient's identity/device/location must never be exposed through this mechanism.
- Acknowledgement must be undoable by the recipient.
- The mechanism must not reveal *when* the page was viewed, separately from whether it was acknowledged.
- Forwarded links must not expose any additional private information to whoever they're forwarded to, beyond what the original recipient could see.
- The sender must be able to disable receiving acknowledgements entirely.

## Recipient identification without accounts

For a direct one-to-one message, Hold generates an opaque, recipient-specific link so the acknowledgement can be attributed to the right connection without requiring the recipient to create an account. The link itself must contain no readable health, identity, or status data (i.e. not human-readable or guessable from the URL structure alone).

**For group chats:** the safer first-version behaviour is to show status/guidance without collecting individual per-person acknowledgements at all — do not attempt to distinguish individual readers in a group context unless each person has been deliberately issued their own distinct link.

## Recipient-suggested responses — optional, user-curated, never auto-generated as a default

The Hold user may optionally select or write suggested replies shown on the page to help recipients respond safely, e.g.: "Good to hear from you — take your time." / "Welcome back. No explanation needed." / "I'm here when you're ready." / "Would you prefer a reply, a reaction, or space?" / "I care, but I need some time too." These must be copyable without an account, entirely optional to display, and the user must be able to disable suggested replies or disable replies altogether (acknowledgement-only mode).

## Guidance on uncertainty

The page should be honest about what it doesn't know, not just what it does. Include a plain-language section covering: what this status means; what it does not tell you (private cause, when capacity will return, what every relationship means); what the Hold user has chosen to share; and what a recipient can do (respect the stated preference, avoid repeated requests for explanation, and — separately — what to do if there's a genuine safety concern, distinct from trying to interpret the status itself). For indefinite Hold specifically, include explicit language that "no return date available" is not a request for the recipient to wait indefinitely or suspend their own boundaries — this protects the recipient's wellbeing, not just the Hold user's.

## Accessibility — independent implementation required

**This is the one surface of the whole feature set that runs entirely outside the app**, on the open web, viewed by people who have never configured any Hold accessibility setting — it cannot inherit the app's existing reduced-motion, contrast, or dynamic-text handling by default. It needs its own independent accessibility implementation, not an assumption that the app's settings apply:

- The page must meet WCAG AA on its own terms: 4.5:1 contrast for body text, 3:1 for large text and the glyph/UI elements, tested independently of the app's existing token system since this is a separate HTML surface.
- Respect the *browser's* `prefers-reduced-motion` setting directly (not the app's internal setting, which this page has no access to) — any animation on the page (e.g. the glyph state) must have a static fallback triggered by this OS/browser-level signal.
- The page must be fully operable by keyboard alone (tab to the acknowledgement button, activate with Enter/Space) and by screen reader, since a meaningful proportion of recipients opening this link will not be Hold users and may be on assistive technology Hold has no way to detect in advance.
- The "◉ Hold this — no reply needed" button and any suggested-reply copy buttons must meet the same touch target minimums as native controls (44×44pt equivalent), given a large proportion of opens will be on mobile.
- Semantic HTML throughout (proper heading structure, button elements rather than styled divs) rather than a purely visual implementation — this page is a stranger's first and possibly only contact with Hold, and may be their only impression of whether the product is trustworthy and well-built.

## Research panel candidate — Settings → Research

> "Sharing a link in a group chat can leak information before anyone even clicks it, because chat apps auto-generate previews. Hold's status page is built so nothing revealing appears in that preview — only a generic label, never your actual status."

## Status

Not built in `hold-app` yet. Reference/spec material for future scoped feature work.
