# AI Automation Studio — Portfolio Hub

The client-facing front door for five production-grade AI automation systems. Static, dependency-free,
deployed on GitHub Pages.

**Live site:** https://wasay-09.github.io/ai-automation-studio/

---

## What this is

A single-page portfolio that does one job: turn a stranger into a booked call. It leads with five
**clickable live demos** rather than screenshots, because a prospect who has just watched a lead get
scored in their own browser needs a lot less convincing than one reading a bullet list.

Structure of the page:

| Section | Purpose |
|---|---|
| Hero | Positioning + immediate route to the demos |
| Stats strip | Credibility markers (systems shipped, tests, deploy time) |
| Selected work | Five case studies: problem → mechanism → outcome → demo + source |
| Services | The four problem categories, so prospects self-identify |
| Process | Removes "how does this even work" friction |
| Pricing | Ranges, to filter out unserious enquiries before the call |
| FAQ | Handles the six objections that otherwise eat the first call |
| Contact | Pre-filled mailto with the three questions worth answering |

## The five systems it links to

| Project | Category | Live demo | Source |
|---|---|---|---|
| **LeadFlow AI** — inbound lead qualification & routing | Sales ops | [demo](https://wasay-09.github.io/leadflow-ai/) | [repo](https://github.com/wasay-09/leadflow-ai) |
| **Concierge Agent** — embeddable RAG support & booking agent | Customer support | [demo](https://wasay-09.github.io/concierge-agent/) | [repo](https://github.com/wasay-09/concierge-agent) |
| **DocuFlow** — invoice & receipt processing pipeline | Finance ops | [demo](https://wasay-09.github.io/docuflow/) | [repo](https://github.com/wasay-09/docuflow) |
| **Outreach Engine** — AI SDR with deliverability linting | Growth | [demo](https://wasay-09.github.io/outreach-engine/) | [repo](https://github.com/wasay-09/outreach-engine) |
| **ContentForge** — content repurposing engine | Content | [demo](https://wasay-09.github.io/contentforge/) | [repo](https://github.com/wasay-09/contentforge) |

Every one of those demos runs its real logic client-side with **no API key and no sign-up**. That is a
deliberate sales decision: the moment a prospect has to create an account, most of them leave.

## Tech

Deliberately none. One `docs/index.html` — inline CSS, inline vanilla JS, no build step, no external
requests, no fonts or scripts fetched from a CDN. It loads instantly anywhere in the world, survives
any hosting change, and can never break because a dependency moved.

- System font stack, monospace accents
- Dark palette (`#0a0c0e` base, `#c8f24e` accent), CSS custom properties throughout
- `IntersectionObserver` scroll reveals, `prefers-reduced-motion` respected
- Responsive down to 360px; semantic landmarks; contrast checked against WCAG AA

## Local preview

```bash
cd ai-automation-studio/docs
python3 -m http.server 8080
# open http://localhost:8080
```

## Customising it

Everything a new owner needs to change lives in a handful of places:

| What | Where |
|---|---|
| Contact email | `docs/index.html` — the `mailto:` links, the footer, and `var EMAIL` in the script |
| Accent colour | `:root { --accent }` |
| Pricing | the `#pricing` section |
| Case studies | the five `<article class="case">` blocks |
| Availability banner | `.avail` in the hero |

> **Note:** the email currently used is `wasayabdul71@gmail.com` (taken from the local git identity)
> and the display name is "Abdul Wasay". Swap both if you'd rather route enquiries to a business
> address such as a `@yourdomain.com` inbox — a custom domain measurably improves reply rates on
> outbound.

## Deployment

See [DEPLOY.md](DEPLOY.md) — written to be executed step by step by an AI coding agent.

## Sales playbook

[`playbook/`](playbook/) contains the assets that turn this portfolio into revenue: a discovery-call
script, a proposal template, cold outreach sequences for UAE and US markets, and a pricing calculator.
