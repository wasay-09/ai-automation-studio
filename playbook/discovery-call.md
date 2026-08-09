# Discovery call — 30 minutes, ends in a scoped project

The goal is not to demo. The goal is to find one workflow that is expensive, repetitive and bounded,
and to leave with agreement on what a pilot would look like.

## Structure

**0–2 min · Frame it**

> "Thanks for the time. Plan for the next 30: I'll ask about how work actually flows through your
> team, we'll find the one or two things worth automating first, and I'll send you a written map of it
> by tomorrow — free either way. Sound right?"

Setting the agenda upfront makes the rest of the call feel like a working session rather than a pitch.

**2–15 min · Find the pain**

Ask these, and shut up after each one:

1. Walk me through what happens from the moment an enquiry arrives to someone replying.
2. Who touches it, and what do they do by hand at each step?
3. How many of those come in a week? What's the range on a bad week?
4. Where does it break — what falls through, and how do you find out it fell through?
5. What have you already tried? What happened?
6. If this worked perfectly, what changes for you specifically?

Question 5 is the one people skip. A failed previous attempt tells you the real constraint — usually
that the last vendor built something nobody would use.

**15–22 min · Quantify it**

Get to a number, out loud, in their words:

> "So that's roughly 40 invoices a week, about 4 minutes each — call it 3 hours weekly, 12 a month.
> What's a loaded hour worth in your finance team?"

Then reflect it back: *"So we're looking at somewhere around $X a month in labour, plus whatever the
duplicate payments cost."* Now every price you quote is measured against that number instead of against
your hourly rate.

**22–27 min · Show, briefly**

One demo, the one matching their pain, three minutes maximum. Share the link so they click it
themselves — a prospect operating the thing remembers it far better than one watching your screen.

Say the honest version: *"This is the same logic that would run for you; your version reads from your
actual CRM and your document formats."*

**27–30 min · Close to a next step**

> "Here's what I'd suggest. I'll send the audit — the three highest-value automations, with hours
> saved on each — by tomorrow. If the top one looks right, I scope it as a fixed-price pilot, usually
> five to ten days, and you decide from there. No obligation on the audit. Fair?"

Never end a call with "let me know your thoughts". End with a dated deliverable that you owe them.

---

## Qualifying — who to walk away from

| Green flag | Red flag |
|---|---|
| Names a specific recurring process | "We want to use AI somehow" |
| Knows roughly how many/how often | Cannot quantify volume at all |
| One decision-maker on the call | "I'll need to run it past several people" (and none are named) |
| Has a budget range in mind | "What's your hourly rate?" as the opening question |
| Frustrated by a concrete failure | Curious about the technology in the abstract |
| Timeline in weeks | "Sometime next quarter, maybe" |

Two or more red flags: send the audit, do not chase.

---

## Objection handling

**"That's more than I expected."**
> "Understood. Compared to what — another vendor, or an internal estimate? … The way I'd frame it:
> you described roughly $X a month in manual time. A one-off $Y pays that back in Z weeks and keeps
> paying. If the budget's genuinely fixed, I'd rather cut scope to one workflow than cut quality."

Never discount without removing scope. A discount teaches them your first number was invented.

**"Can we just use ChatGPT for this?"**
> "For a one-off, absolutely — and you should. What it doesn't do is run unattended: pick the email
> up, check it against your records, handle the ones that fail validation, retry when an API is down,
> and tell you when something needs a human. That reliability layer is most of what you're paying for."

**"How do we know it won't make things up?"**
> "Because the parts that must be correct don't go through a model at all. Scoring, arithmetic and
> validation are plain deterministic code you can audit line by line. The model only writes language,
> and where it answers questions it's restricted to your documents with citations and a confidence
> threshold — below that it says it doesn't know and hands off." *(Then show the citations in the demo.)*

**"We'd want our own team to maintain it."**
> "Good — that's how it should end. You get the repository, the tests and a runbook, and I record a
> walkthrough for whoever inherits it. I'd rather you not need me in six months."

**"Send me a proposal."**
> "Will do — one question so it's actually useful rather than generic: if we could only fix one of
> the things we discussed this quarter, which one?"

**"We're not ready yet."**
> "Fair enough. What would need to be true for it to be worth doing? … I'll check back around then —
> and the audit's still yours in the meantime."

---

## After the call — within 24 hours

Send the audit. Keep it to one page:

1. What I understood about how it works today *(prove you listened — this is the whole document's credibility)*
2. Three automation opportunities, ranked
3. For the top one: what it does, roughly how long, roughly what it costs
4. Estimated hours and money saved per month
5. One clear next step with a date

The audit being genuinely useful — even to someone who never hires you — is what makes it worth
offering for free. People forward useful documents to their colleagues. They don't forward pitches.
