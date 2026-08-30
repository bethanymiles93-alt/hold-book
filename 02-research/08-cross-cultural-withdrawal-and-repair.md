# Cross-cultural withdrawal and repair — research pages reference v2

**Status:** Source/reference material for `hold-book`'s Research pages, not a build spec. From an extended external design/research session (2026-08-19 onward), handed to this repo 2026-08-31. See `08-decisions/01-decision-log.md`, 2026-08-31. **Nothing in this file should be implemented directly into `hold-app` without first being scoped as an actual feature** — the parts of this research that already reached that stage are `06-privacy-security/07-reconnection-safety-requirements.md`, `04-ux-content/02-voice-and-language.md`, `05-design-system/03-glyph-and-state-system.md`, `04-ux-content/06-state-architecture-and-memory.md`, and `04-ux-content/07-universal-web-page.md`.

**Supersedes:** an earlier v1 reference document from the same external design process — not previously committed to this repo (checked directly, no trace of it here), so nothing existing is being overwritten; this file is the first version of this research actually in `hold-book`.

## The central thesis — state this plainly, near the top of the ethos page

Across very different, historically unconnected societies, humans have repeatedly built **legible states** — recognised social categories in which the ordinary rules of participation and availability are understood, by everyone around the person, to have temporarily changed. The important feature was never the withdrawal itself. It was that other people had a shared script for interpreting it, so absence wasn't read as rejection.

Modern digital messaging has no equivalent script. Someone goes quiet on WhatsApp for two weeks and their friend has no shared cultural protocol for interpreting it — are they angry, did I do something, do they not care, should I message again. Hold's core function is to manufacture, for the first time in a purely digital context, exactly the kind of legible state humans have built again and again throughout history: *this person's capacity has changed; the relationship has not.*

**Required methodological discipline, carried through every page:** we cannot claim an ancient society "accepted going quiet" in the modern messaging sense. Every entry below is filed under one (or more) of four distinct categories, kept separate rather than blurred together:

1. **Sanctioned withdrawal / rest** — was reduced availability itself a recognised, legitimate state?
2. **Relational obligations while absent** — did the relationship/community owe the absent person anything, or vice versa, during the withdrawal?
3. **Restorative / reconciliation practice after rupture** — when something *did* go wrong, was the response oriented toward repair or punishment?
4. **Reintegration / return** — was there a structured bridge back to ordinary participation, or was return left to chance?

**Verification status key:** ✅ Verified (independently checked via search) · ⚠️ Plausible, unverified (from external source material, not yet checked) · 🔍 Needs dedicated research pass (named but not substantively checked at all)

**Update this table in place as each 🔍 or ⚠️ item gets checked, rather than creating parallel documents.**

## Category 1: Sanctioned Withdrawal / Rest

| Tradition | Era | Status | Detail |
|---|---|---|---|
| Judaism — Shabbat | c. 1200 BCE onward | ✅ | Rest as bounded, legitimate, recurring — not earned by finishing your obligations first, not conditional on an empty inbox. Likely Hold's single strongest concept: *rest doesn't have to be earned by completing your social inbox.* |
| Christianity — Jesus's repeated withdrawals | 1st c. CE | ✅ | Mark 1:35, Luke 5:16, Matthew 14:23, Mark 6:31–32. A deliberate, repeated pattern, not a one-off. |
| Christianity — Desert Fathers and Mothers | 3rd–5th c. CE | ✅ | Solitude as legitimate spiritual practice (Apophthegmata Patrum). |
| Islam — khalwa / Muhammad's retreats to Cave of Hira | 7th c. CE | ✅ | Withdrawal before transformation. Use this rather than stretching the Elijah narrative onto Islam — the Quran's Ilyas account doesn't include it. |
| Hinduism — ashrama system | Vedic era onward | ✅ | Four life stages, different expected levels of worldly engagement — variable engagement across time is structurally normal, not deviant. |
| Buddhism — the Saṅgha | c. 6th–5th c. BCE onward | ✅ | A person could leave ordinary household life for a formally organised, differently-regulated community. The relevant analogy for Hold isn't "users are monks" — it's that *society can recognise someone is operating under a different level of social availability without reading it as reduced affection.* |
| Daoism — wu wei, and Zhuangzi's association with reclusion | c. 4th c. BCE onward | ⚠️ | Zhuangzi specifically linked to withdrawal-as-self-cultivation rather than social failure. The general wu wei concept is independently well-sourced; the specific Zhuangzi-reclusion framing needs its own check before being stated as fact. |
| Confucianism — the tradition of reclusion, incl. Wang Fu | Han dynasty onward | 🔍 | Claim: even relationship-obligation-heavy Confucian thought developed a real tradition of withdrawal when "morally worthwhile participation" wasn't possible, and that a later Han thinker (named as Wang Fu) argued withdrawal needn't mean abandoning responsibility to the community — one could remain committed from outside active participation. **Not yet independently verified** — the specific attribution needs checking before use. If confirmed, one of the most directly useful entries in the whole project: "withdrawal ≠ lack of care" with a 2,000-year-old precedent. **Priority: high.** |
| Aboriginal Australian societies | Deep time onward | ⚠️ | Ritual seclusion, mourning practices, differentiated social obligations existed across many distinct nations — genuinely diverse, not one system. Requires nation-specific research before any further detail is added; do not generalise. |

## Category 2: Relational Obligations While Absent

| Tradition | Era | Status | Detail |
|---|---|---|---|
| Baha'i — prohibition on backbiting | 19th c. CE | ✅ | Even listening to backbiting without objecting is treated as complicity. Directly informs Circle privacy: a person's absence shouldn't become something discussed about them while they're away. |
| Confucianism — ren, li, ongoing relational maintenance | 6th c. BCE onward | ✅ | Relationship as continuous responsibility rather than episodic transaction. |
| Norse — Hávamál on friendship | Recorded 13th c., older oral roots | ✅ | Visit a trusted friend often — but note the reciprocal half of this is about *presence*, not absence; less directly about obligations *during* a withdrawal than about the general shape of an ongoing bond. |

**This category is the thinnest of the four so far** — most traditions researched address either the legitimacy of withdrawal or the process of repair, not what (if anything) is owed by either party during the gap itself. Worth a dedicated research question in its own right: which traditions specify duties that continue across an absence (e.g. does anyone check in, is there a designated person who keeps the absent party's place in the community)? **Priority for next research pass: high** — see queue below.

## Category 3: Restorative / Reconciliation Practice After Rupture

**The reframed core finding, worth stating precisely:** the sharpest common thread isn't "who was wrong, punish them" — it's **"what happened, what was damaged, how do the people involved keep living together."** Where this shows up, it consistently reframes the question from *why haven't you replied* to *what's happening to you that makes replying difficult*, and then *how do we preserve the relationship while this is happening.*

| Tradition | Era | Status | Detail |
|---|---|---|---|
| Navajo Nation Peacemaking (Hózhǫ́) | Revived 1982, ancient roots | ✅ | "What does the relationship need to be whole?" instead of "who's at fault?" Centrepiece entry. Yazzie, "Life Comes from It," New Mexico Law Review 24 (1994). |
| Haudenosaunee Condolence Ceremony | Great Law of Peace, pre-contact | ✅ | Traditionally performed specifically to mourn a deceased leader and install a successor — "clear the eyes, clear the ears, clear the throat" so the community can see, hear, and speak clearly again. Origin story: the Peacemaker consoled a grieving Hiawatha so his judgment, "clouded" by loss, could clear. Modern practice has genuinely extended this to general grief and healing support (patients, at-risk teens, people in recovery) — treat the traditional and modern-extended uses as two related but distinct facts, not one. |
| The Great Treaty of 1722 (Albany) | 1722 CE | ✅ | Following the killing of Sawantaeny (a Seneca hunter) by two colonial traders, Indigenous negotiators secured a process of acknowledgment, restitution, condolence ceremony, and ultimately forgiveness, over English colonial officials' initial assumption that "real" justice meant trial and punishment. Documented in Nicole Eustace, *Covered with Night* (2021). Genuinely striking contrast: "you failed to reply, rectify your failure" (conventional messaging model) vs. "connection has been interrupted, make returning to connection easier" (the relational model) — this comparison should never imply equivalence between a homicide and an unanswered message; the *structure* of the response is the transferable insight, not the severity of the underlying event. |
| Brehon Law, Cyfraith Hywel, Anglo-Saxon wergild, Isle of Man breast law | Medieval British Isles | ✅ | Restorative, compensation-based; progressively displaced by Norman/English/Tudor conquest. |
| Ancient Egypt — kenbet courts, Ma'at/isfet | New Kingdom onward | ✅ | Restitution for most offences; harsher penalties reserved specifically for crimes against state/temple. |
| Sumer — Code of Ur-Nammu | c. 2100 BCE | ✅ | Oldest surviving law code, more restorative than what followed it (Hammurabi). |
| Somalia — Xeer | Ongoing | ✅ | Clan-elder compensation-based system, notable for not depending on centralised state institutions. |
| Rwanda — Gacaca courts | Revived 2001–2012 | ✅ | Community truth-telling and reintegration for genocide-era cases. |
| Uganda — Mato Oput (Acholi) | Ongoing | ✅ | Grouped with Gacaca in the literature; healing-oriented. |
| New Zealand — Māori-influenced Family Group Conferencing / Te Ao Mārama | 1989 onward | ✅ | Widely credited as an origin point of the modern global restorative justice movement. Contemporary NZ courts explicitly ask what happened *to* a person, not only what they did — closely mirrors Hold's "this isn't a character defect, something is happening to my capacity." |
| Canada — sentencing circles, Gladue principles | 1990s onward | ⚠️ | Verify specific case names/dates before publication. |
| Andes — Ayni | Inca-era onward | ✅ | Suppressed by Spanish colonial extraction, same conquest-displacement pattern as the Druids. |
| India — panchayat systems | Ancient onward | ✅ | Caveat required: modern khap panchayats associated with harmful extrajudicial rulings; frame around historic mediation function specifically. |
| China — Confucian "no litigation" tradition | 6th c. BCE onward | ✅ | Confucius's own stated aim was to make litigation unnecessary, not just to judge well. Modern caveat: mediation also documented as a tool of state social control in contemporary China — present both honestly. |
| Ottoman millet system | 1453 onward | ✅ | Religious communities self-governing internal matters under their own law; not equality, but a stable model for deep coexistence without demanding sameness. |
| Rome — Twelve Tables | 449 BCE | ✅ | Mixed: compensation-as-alternative-to-retaliation for injury, but also punitive elements; drifted more punitive as Rome centralised. |
| Norway/Viking — the Thing, wergild, outlawry | c. 900–1300 CE | ✅ | Compensation preferred; outlawry (loss of all legal protection) the harsh backstop if unpaid. Connects physically to the Isle of Man entry via the shared "Thing" place-name root (Tynwald). |
| Islam — diyah, 'afw, sulh | 7th c. CE onward | ✅ | Quran (2:178) explicitly frames forgiveness and compensation as superior alternatives to retaliation. |
| Southern Africa — Ubuntu, communal reconciliation traditions | Precolonial onward | ✅ | Explicit emphasis on reconciliation, reparation, and reintegration into community rather than exclusion, across multiple (not singular) customary systems. Contemporary scholarship explicitly warns against treating African customary law as one tradition — many distinct systems, recurring but non-identical principles (dispute avoidance, reconciliation, consensus-building, matching dispute to process). |
| Ndebele — ukuxolisana | Precolonial onward | 🔍 | Described in source material as reconciliation, metaphorically "washing one another's scars." Not yet independently verified. |
| San communities | Precolonial onward | 🔍 | Described as extended collective deliberation until resolution, without romanticising as inherently conflict-free. Not yet independently verified. |
| Hawaiian — hoʻoponopono | Precolonial onward | 🔍 | Widely cited (including by UNESCO, per source material) as explicitly focused on restoring relationships. Well-known enough in general culture that verification should be straightforward —**priority for the next research pass, not a long-term gap.** |
| Mongol Empire, Khmer Empire, Mughal Empire | Various | 🔍 | Low-to-moderate confidence; not independently reviewed. Lower priority — these read as thinner fits for Hold's specific question than the entries above. |
| The Oresteia (contrast case, not a match) | 458 BCE | ✅ | Explicitly a different category — ending a vengeance cycle through one final impartial trial verdict, not relational repair. Keep separate from the restorative cluster above. |

## Category 4: Reintegration / Return

**This may be the least-developed category so far relative to its importance.** Most of what's been gathered addresses *why withdrawal is legitimate* or *how rupture gets repaired*; comparatively little addresses the specific, structured *bridge* back to full participation after time away. This is arguably the most directly useful category for Reconnect specifically. **Priority for next research pass: high** — see queue below.

| Tradition | Era | Status | Detail |
|---|---|---|---|
| Christianity — the prodigal son | 1st c. CE | ✅ | Welcome before explanation; no accounting of absence required. |
| Hittite — Myth of Telepinu ("Vanishing God" pattern) | Bronze Age | ✅ | Return can't be forced, only gently made possible — a small bee, not confrontation, brings the god back. |
| Aboriginal Australian — Dadirri | — | ✅ | The *waiting* side of reconnection: attentive, still listening rather than anxious monitoring, as publicly offered by Miriam-Rose Ungunmerr-Baumann. |
| Mandaeism — masbuta | 2nd–5th c. CE onward | ✅ | Weekly calendared purification *and* an on-demand practice after a lie or quarrel specifically — one of the closest ritual precedents for "a sanctioned, non-shameful practice for after something has gone wrong." |
| Korean — Ssitgim-gut | Ongoing | ✅ | Knots tied to represent unresolved grief, physically untied during the ritual — direct inspiration for a possible visual release feature (not yet scoped; see open questions if/when this is picked up). |
| Psychology — rupture and repair (Tronick) | 1975 onward | ✅ | What predicts security isn't the absence of rupture, it's the reliability of repair afterward. The clearest modern secular anchor for this entire category. |

## Formal Reconnect-phase architecture

**Supersedes any earlier "Recognise → Reassure → Return → Repair → Renegotiate" linear model.** A model assuming continued relationship as the destination is the wrong shape. Correct architecture is **branching, not linear**, with two clearly separated pathways rather than one default sequence.

### Pathway 1 — Ordinary return (the dominant, default pathway). No wrongdoing presumed, ever.

Governing assumption: *capacity changed; no offence occurred; no apology is required.* This must be the default emotional grammar of returning — repair-flavoured language must not appear automatically, even in a soft "acknowledge the impact" form, because that still risks converting another person's possible reaction into the absent person's presumed fault.

*Appropriate language:* "I have a little more capacity now." / "I'm beginning to reconnect." / "I wasn't available, but I still cared." / "You don't need to reply." / "I'd like to start gently." / "I'm not ready to discuss my absence."

*Avoid entirely in the default pathway* — see `04-ux-content/02-voice-and-language.md`'s "Language the product should never use" section for the full list and its cross-reference here.

### Pathway 2 — Optional repair

Only entered by explicit, affirmative user choice, e.g. prompted with "Is there something you want to acknowledge or repair?" — never inferred by the system from duration, unread-message count, repeated contact attempts, or another person's visible distress. An absence can affect someone without being an offence; an effect does not automatically create culpability. Options at this gate should include: "No — nothing wrong happened." / "I'm unsure." / "Yes, but I don't want help wording it." / "Yes — help me acknowledge their experience." / "I need support before contacting them." The verified apology-element checklist below belongs only inside this optional pathway, never in Pathway 1.

### Full branching steps, replacing the linear five-step model

1. **Recognise** — my capacity and circumstances belong to me.
2. **Choose** — do I want contact with this person at all?
3. **Protect** — do I need privacy, distance, restriction, or permanent separation?
4. **Reconnect** — if choosing to, what's the smallest safe form of contact? ("Bridge not leap": a heart, a brief line, one person first — the smallest credible act counts.)
5. **Acknowledge** — is there anything I *freely* want to recognise — never something the product presumes?
6. **Redefine** — what level of relationship is sustainable now?

**Legitimate completion states — all equally valid, none ranked as more "successful" than another:** reconnect normally; reconnect gradually; reconnect with new boundaries; remain on Hold; stay connected without conversation; decline this particular contact; end the relationship; block for safety. See `06-privacy-security/07-reconnection-safety-requirements.md`, sub-requirement 9.

### Verified, build-usable checklist for reconnection message copy

Victim-centered vs. defensive apology elements (Robichaud, Schumann, Kil, Koestner & Mageau, 2025, *Journal of Research on Adolescence*, 35, e70024; parent-adolescent context, but the element taxonomy generalises). Confirmed via direct review of the full paper, not just the abstract.

*Elements that help (associated with greater forgiveness, satisfaction, no loss of standing):* expressing remorse; accepting responsibility; admitting the wrongdoing where one occurred; acknowledging the other person's hurt; committing to change; offering repair; giving an internally-oriented explanation ("I lost control" / "my capacity dropped") rather than an external excuse; making a non-pressuring forgiveness request.

*Elements that don't help, and sometimes actively hurt:* external excuses ("I was busy"); justifications ("I did it for a good reason"); blame; minimising ("it wasn't a big deal"); pressuring forgiveness requests ("please forgive me").

Useful finding worth keeping in mind for copy calibration: a *basic* acknowledgement performed about as well as a more elaborate one — Hold does not need to engineer long, effortful reconnection messages to be effective. A short, honest one clears the same bar.

## Cross-cutting notes

- Framing note for every Research page built from this material: these traditions are referenced for psychological/structural insight, not endorsement of any faith.
- Never reproduce quoted text from any source, including public-domain translations — describe and cite, source exact wording separately when the page is actually built.
- Yazidism: state plainly that Yazidis are not devil worshippers, and that their own account of Melek Taus rejects the "fallen angel" framing that fuelled centuries of persecution.
- Zeigarnik Effect and ego depletion: both carry serious modern replication problems — usable only with the caveat attached, never presented as settled.
- Vedic religion "evolved into," did not simply become or remain separate from, Hinduism.
- 1 Kings 19 (Elijah) is Nevi'im/Tanakh (Hebrew Bible), not Torah.

## Priority queue for the next research pass, in order

1. Hawaiian hoʻoponopono (likely quick to confirm, high relevance)
2. Wang Fu / Han-dynasty Confucian reclusion argument (high relevance if confirmed — direct 2,000-year-old precedent for "withdrawal ≠ lack of care")
3. Ndebele ukuxolisana, San consensus practices (moderate relevance, currently unverified)
4. Category 2 (relational obligations while absent) generally — thin across the whole project, deserves a dedicated search pass in its own right, not just incidental entries
5. Category 4 (reintegration/return) — also thinner than 1 and 3; worth deliberately seeking out more entries here specifically, since it's the most directly applicable category to Reconnect
