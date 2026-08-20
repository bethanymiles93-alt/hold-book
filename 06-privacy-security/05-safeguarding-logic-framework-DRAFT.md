# Hold — Provisional Safeguarding Logic Framework (DRAFT for clinical review)

**Status: not clinically validated. Not for production use. This is a starting structure for a Clinical Safety Officer / clinical psychologist to review, correct, and build the actual detection logic against — not a finished specification.**

Prepared by: Bethany Miles (founder, Hold), with Claude as a drafting/structuring aid. Logged into `hold-book` 2026-08-12 — this file was drafted in an earlier session and referenced from the decision log and `08-decisions/04-open-questions.md`'s safeguarding entry before actually being committed here; that gap is now closed.

Purpose: give a clinical reviewer a concrete skeleton to react to, rather than starting from a blank page — speeding up review, not replacing it.

See also `06-privacy-security/03-safeguarding.md` for the built architecture this framework feeds into, and `08-decisions/04-open-questions.md`'s "Safeguarding trigger logic and wording" entry for the standing open question this document is meant to help resolve.

---

## 1. What Hold is, for the purpose of this review

Hold is a communication-drafting tool for people whose capacity to reach out to friends/family fluctuates (due to illness, burnout, depression, grief, or similar). It is **not** a therapy app, crisis service, or clinical product. Users type free-text messages (to loved ones) into the app, sometimes with AI assistance to draft or amend them. Because the user base skews toward people who are unwell, isolated, or in difficult periods, free-text input may occasionally surface genuine risk disclosures — even though that is not the app's purpose.

This framework concerns: **what should happen when a user's own typed text suggests they may be at risk**, before that text is used to draft a message to someone else.

---

## 2. Proportionality — why the bar is lower than a clinical/therapy app, but not zero

Reference points already considered (see `03-safeguarding.md` for full detail):
- **Wysa** classifies every message into seven risk types and is AI-led triage, partnered with the NHS — a much higher clinical bar than Hold needs, because Wysa's core function *is* mental health support.
- **Woebot** was originally a clinician-designed CBT chatbot with peer-reviewed efficacy studies.

Hold is closer to "a messaging assistant that happens to have a safety net" than either of these. The proposed approach (below) is intentionally proportionate: detect, redirect to real help, don't attempt to counsel or reason with the user.

**Question for reviewer:** does this proportionality framing hold up clinically, or does Hold's specific audience (people already isolated, already struggling to communicate) push the bar higher than a "general purpose" comms app would need?

---

## 3. Two-tier detection architecture (already decided, included for context)

| Tier | User group | Mechanism | Rationale |
|---|---|---|---|
| 1 | Free tier | On-device keyword/phrase matching | Zero cost, runs locally, fully auditable, no data leaves device |
| 2 | Hold+ (paying) | AI classifier (Claude Haiku) | Better at catching indirect/context-dependent language; cost gated to paying tier |

**Question for reviewer:** is a two-tier system (weaker net for free users) clinically/ethically defensible, or does it need to be flagged as a risk to mitigate — e.g. is there a minimum viable keyword net that must apply to *everyone* regardless of payment tier?

---

## 4. Provisional category framework (skeleton only — no specific phrases)

This is a category structure, not a phrase list. Actual trigger phrases/patterns need to be built by the clinical reviewer, ideally validated against real (anonymised, consented) language patterns rather than assumed vocabulary.

### Category A — Direct statements of intent or plan
Explicit language stating an intention to end one's life or seriously harm oneself, with or without a stated method or timeframe.
*Severity: highest. Should trigger the strongest response tier (Section 5).*

### Category B — Hopelessness / entrapment language
Expressions of feeling trapped, of there being "no way out," of being a permanent burden to others, or of the future being foreclosed.
*Severity: high, but more ambiguous than Category A — may reflect situational distress rather than acute risk. Needs reviewer input on threshold.*

### Category C — Farewell / finality behaviour
Language suggestive of "tying up loose ends" — unusual goodbyes, giving away possessions (may surface obliquely in a message being drafted to a loved one), expressions of finality inconsistent with the ordinary tone of a "going quiet" message.
*Severity: high. Particularly relevant to Hold given the app's core function involves users writing goodbye-adjacent or "stepping back" messages as normal, non-risk behaviour — this category needs the most careful calibration to avoid false positives against Hold's ordinary use case (see Section 6).*

### Category D — Method or means specificity
Any mention of a specific method, access to means, or a specific timeframe ("tonight," "by the weekend").
*Severity: highest — combined with Category A this likely represents the clearest case for the strongest response tier.*

### Category E — Escalation / trajectory language
Language indicating a worsening trajectory from vague distress toward something more acute — may not fit neatly into A–D alone but represents a pattern across a conversation or across repeated Going Quiet periods rather than a single message.
*Severity: variable — flagged separately because this may require conversation-level or pattern-level logic, not just single-message keyword matching. Open question for reviewer: is this in scope for v1, or a later-phase capability?*

### Category F — Self-harm (non-suicidal) language
References to self-harm behaviours or urges distinct from suicidal ideation.
*Severity: high, handled with the same redirect-to-resources approach but may warrant different resource signposting (e.g. self-harm-specific services alongside Samaritans/Shout).*

### Category G — Risk to others / domestic abuse disclosures
Given Hold's use case involves writing to specific named people, free text may surface disclosures of abuse, coercive control, or fear of another named person, rather than self-directed risk.
*Severity: high, but the correct *response* is likely different from Categories A–F (different resources, different considerations around whether the app should ever suggest notifying a Core Circle member, since the risk may involve someone close to the user). Flagged as a distinct category needing its own logic branch, not folded into general self-harm handling.*

**Question for reviewer:** is this category set complete, clinically sound, and correctly separated? Are there established taxonomies (e.g. from Wysa's public materials, NICE guidance, or standard risk-screening frameworks) this should map to more formally?

---

## 5. Provisional response tiers (not final wording — see `03-safeguarding.md` "Proposed approach")

Already decided in principle, included here for the reviewer's context:

1. **Detection layer** runs on free-text input before it reaches AI drafting.
2. **If triggered:** a non-blocking, persistent banner appears above the message box (resources + Core Circle notify option) — **reversed 2026-08-10 from an earlier hard-stop design, which is no longer current.** Drafting stays available throughout; the app doesn't attempt to console, reason with, or draft a "sensitive" message on the user's behalf, but it never stops the person from writing and sending their own words either. The message someone is trying to write is very often the real reaching-out behaviour Hold exists to enable in the first place — blocking it would work against Hold's own purpose (see the Wysa 2.4%-called-a-helpline evidence in `03-safeguarding.md`). Flagged for the clinical/legal reviewer as a real safety judgment call, not an assumed-safe UX default. See `08-decisions/01-decision-log.md`, 2026-08-10.
3. **Minimum shown, UK (default/home market), regardless of category:**
   - Samaritans — 116 123 (free, 24/7, any crisis, UK & Ireland)
   - Shout — text "SHOUT" to 85258 (free, 24/7 text-based, UK)
   - 999 for immediate danger to life
   - NHS 111, option 2 — urgent mental health crisis support, 24/7, all ages. **Note: this replaced the previous patchwork of local NHS trust crisis-line numbers and 0800/0300 Mental Health Direct numbers as of 1 April 2026, following a national NHS rollout. NHS 111 option 2 is now the single, current, correct number to use across England — confirm no further changes before production, given how recently this changed.**
4. **Lightweight safety-plan layer** (not just numbers): resources above, plus one grounding prompt, plus an option to notify a Core Circle contact right now.
5. **International resource sets — see `06-privacy-security/03-safeguarding.md`, "International crisis resources," for the researched core-six table and its limits.** Resource shown must match the user's region, not default to UK numbers for non-UK users.

**Open question for reviewer:** should different categories (A–G above) route to different response depths, or is a single proportionate response appropriate across all triggered categories? E.g. does Category G (risk from another person) need materially different wording/resources than Category A (self-directed risk)?

---

## 6. The specific false-positive risk unique to Hold

This is flagged prominently because it's structurally different from a general-purpose app: **Hold's entire core function is helping people write "I need to step back," "I can't do this right now," "I need space" messages — language that shares surface vocabulary with genuine crisis language, but is Hold's normal, healthy use case.**

Example of the tension (illustrative, not exhaustive): a user drafting a Going Quiet message might write something like "I just can't keep going like this" meaning *social contact*, not *life*. A naive keyword net could over-trigger on ordinary, non-risk Going Quiet drafting, which would:
- Undermine trust in the app very quickly
- Potentially feel intrusive or alarming to someone who is not in crisis, but is already in a vulnerable state
- Create alert fatigue that could cause genuine triggers to be dismissed by the user

**This is likely the single most important thing for the clinical reviewer to help calibrate** — the boundary between Hold's ordinary vocabulary and genuine risk language, which is not a generic problem other apps have solved for, because other apps don't have "helping someone write a withdrawal message" as their core feature.

---

## 7. Explicitly out of scope for this framework (flagging, not deciding)

- Exact phrase/keyword lists (Category A–G above are categories only — reviewer to build actual detection patterns)
- Exact banner/resource-screen wording (separate deliverable, can be drafted alongside this once categories are agreed)
- Whether Category E (pattern/trajectory-level detection) is v1 or later-phase
- Whether free-tier keyword matching needs a mandated minimum regardless of monetisation tier
- Formal DCB0129/DCB0160 applicability determination — separate legal/regulatory question, not a clinical-content one

---

## 8. Questions for the clinical consultant, consolidated

1. Does the proportionality framing (Section 2) hold clinically for this specific audience?
2. Is the two-tier free/paid detection model (Section 3) ethically defensible?
3. Is the category set (Section 4) complete and correctly separated — does it map to an existing established taxonomy we should be using instead?
4. Should response depth (Section 5) vary by category, particularly for Category G (risk from another named person)?
5. How should Section 6's false-positive risk (Hold's own vocabulary overlapping with risk language) be addressed — calibration approach, testing methodology, or something else?
6. Do you have an existing framework/methodology from prior work that supersedes or should replace this draft, or does this represent a reasonable starting point to build from together?
