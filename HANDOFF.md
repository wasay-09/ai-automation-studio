# Handoff — resume prompts for a fresh chat

If a session ends mid-build (weekly limit, crash, new machine), paste the matching prompt into a new
Claude Code chat opened in `/Users/elphinstone/Projects/personal`. Each one is self-contained and
requires no further input.

---

## A. Finish or repair a single project

> You are finishing a portfolio-grade project autonomously. No human will answer questions — make every
> decision yourself and finish.
>
> Project directory: `/Users/elphinstone/Projects/personal/{{PROJECT}}`
> GitHub: `wasay-09/{{PROJECT}}` (gh is authenticated as wasay-09 with repo+workflow scope)
>
> Do this, in order:
> 1. Read the README and DEPLOY.md to understand what was intended.
> 2. Install dependencies and run the full test suite. Fix every failure. For Python use `uv`; for
>    Node use npm. Report the final summary line.
> 3. Run the type checker / linter (`ruff check` or `tsc --noEmit`) and fix everything it reports.
> 4. Start the server and smoke-test every documented API endpoint with curl. Fix anything broken.
> 5. Open `docs/index.html` and verify the static client-side demo is complete, works with no network
>    access, and looks like a real SaaS product — modern dark UI, good typography, responsive to 360px.
>    Improve it if it falls short.
> 6. Confirm the whole system runs with NO API key set (DEMO_MODE default). This is non-negotiable.
> 7. Grep for TODO, FIXME, `pass  #`, `throw new Error("not implemented")` and finish anything stubbed.
> 8. Commit in logical chunks, push, and ensure GitHub Pages serves `/docs` on main:
>    `gh api -X POST repos/wasay-09/{{PROJECT}}/pages -f "source[branch]=main" -f "source[path]=/docs"`
>    (409 means already enabled.) Then poll the Pages URL until it returns 200.
> 9. Report: repo URL, live demo URL, test summary, and anything still incomplete — be honest.

Substitute `{{PROJECT}}` with one of: `leadflow-ai`, `concierge-agent`, `docuflow`,
`outreach-engine`, `contentforge`.

---

## B. Build an additional project from scratch

> You are building a PORTFOLIO-GRADE, production-quality open-source project end-to-end, autonomously.
> No human will answer questions. Target a complete, tested, pushed, deployed deliverable.
>
> **Project:** `{{NAME}}` — {{one-line description}}
> **Root:** `/Users/elphinstone/Projects/personal/{{NAME}}` (do not touch anything outside it)
> **Business problem it solves:** {{2–3 sentences — who loses money today and why}}
>
> Non-negotiable requirements:
> - Stack: Python 3.14 + FastAPI + SQLite via `uv`, OR Node 22 + TypeScript (strict) + Fastify +
>   better-sqlite3. Both toolchains and network access are confirmed working on this machine.
> - **Zero-key demo mode.** Default `DEMO_MODE=true`. An `LLMProvider` interface with a real
>   `AnthropicProvider` (model id `claude-sonnet-5`, structured output via tool-use, robust parsing and
>   retry) and a deterministic `MockProvider`. There is NO API key on this machine, so everything —
>   tests, demo, UI — must work perfectly without one.
> - 25+ meaningful tests that you actually run and make pass. Paste the summary.
> - `ruff check` or `tsc --noEmit` passes cleanly.
> - No placeholders, no TODOs, no stubbed functions.
> - `docs/index.html`: a single self-contained HTML file (inline CSS + vanilla JS, no build step, no
>   external network requests) that runs the real logic client-side on bundled fixtures. It must look
>   like a genuine SaaS product — modern dark UI, excellent typography, smooth transitions, responsive.
>   This is the sales asset.
> - `README.md` (business problem, buyer, outcome metrics, mermaid architecture, 2-min quickstart, API
>   reference, "how this is deployed for a client") and `DEPLOY.md` written for an AI agent to execute
>   literally — Docker, a managed host, env var table, smoke tests, rollback.
> - Several logical git commits, then:
>   `gh repo create wasay-09/{{NAME}} --public --source=. --remote=origin --push --description "..."`
>   then enable Pages on `/docs` and poll until the URL returns 200.
>
> Report: repo URL, live demo URL, test summary, a one-paragraph pitch usable in a proposal, and any
> known limitation — honestly.

Project ideas that fit this portfolio and don't overlap what exists:

| Idea | Buyer |
|---|---|
| WhatsApp Business appointment bot with calendar sync | Clinics, salons, home services |
| Contract review assistant — clause extraction + risk flags | Law firms, procurement |
| Property matching engine — brief in, ranked listings out | Dubai brokerages |
| Recruitment screener — CV → structured scorecard vs a JD | Agencies, HR teams |
| E-commerce ops bot — order status, returns, WISMO deflection | Shopify sellers |
| Competitor monitor — pricing/positioning change alerts | SaaS, retail |

---

## C. Refresh the portfolio hub after adding a project

> Open `/Users/elphinstone/Projects/personal/ai-automation-studio/docs/index.html`. Add a new
> `<article class="case">` block for the project `{{NAME}}` matching the existing five exactly in
> structure and tone: case number, title, one-line tag, the amber "problem" callout, four `→` bullets
> describing the mechanism, stack chips, an outcome paragraph, and the two buttons linking to
> `https://wasay-09.github.io/{{NAME}}/` and `https://github.com/wasay-09/{{NAME}}`.
>
> Also update the stats strip count, the work-section subheading, and the project table in README.md.
> Commit and push — GitHub Pages redeploys automatically. Then verify the live page returns 200 and
> contains the new project name.

---

## D. Weekly maintenance

> Check every project under `/Users/elphinstone/Projects/personal/` that has a GitHub Pages demo
> (`leadflow-ai`, `concierge-agent`, `docuflow`, `outreach-engine`, `contentforge`,
> `ai-automation-studio`). For each: confirm the Pages URL returns 200, run the test suite and report
> failures, and check for dependency security advisories. Fix what's broken, commit, push, and give me
> a one-table summary. Do not make cosmetic changes I didn't ask for.
