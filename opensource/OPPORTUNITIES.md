# Paid opportunities and target projects

Researched 2026-10-18. Items marked *unverified* come from search snippets, not live pages. Check them before acting.

## Paid, near term (next 30 days)

**Expensify bounties ($175 to $250 per fix, paid via Upwork).** This is the only verified program that pays outside contributors for merged work today.
- Issues: [Help Wanted + External](https://github.com/Expensify/App/issues?q=is%3Aissue+is%3Aopen+label%3A%22Help+Wanted%22+label%3AExternal+sort%3Acreated-desc), with new ones daily.
- Rules: [CONTRIBUTING.md](https://github.com/Expensify/App/blob/main/contributingGuides/CONTRIBUTING.md). Pakistan is eligible.
- **You do this part yourself.** You need a fully verified Upwork profile linked from your GitHub bio. You reproduce the bug on test accounts, post one proposal on the issue, and test on iOS, Android and web. iOS testing needs a Mac or the linked workaround.
- Proposals are judged on who is earliest with the best fix, and an AI bot posts the first one. New contributors get one job at a time.
- Payment comes at least 7 days after deploy. Each regression costs 50% of the payout.
- Stack: TypeScript and React Native.
- Speed decides it. On 2026-10-18, every one of the 15 open issues already had a reviewer's pick or 4 to 7 detailed proposals within 1 to 4 days of the label. The routine now checks for issues labelled in the last 12 hours on every run.

**Contract platforms that value open-source work:**
- [Turing](https://www.turing.com): LLM coding and evaluation contracts. Listings name Pakistan as eligible. *unverified*
- [Mercor](https://work.mercor.com): its offers come from its own assessments, so take those yourself.
- [Arc.dev](https://arc.dev) and Braintrust: profile-based. Merged PRs strengthen the profile.

**Remote roles in your area that may hire from Pakistan** (*unverified*, check each listing):
- [Canonical](https://canonical.com/careers/5703396): Python and Kubernetes engineer, home-based worldwide.
- [Supabase](https://supabase.com/careers): AI tooling engineer, TypeScript and MCP, hires globally.
- [Weaviate](https://careers.weaviate.io): remote engineering roles.

**LiteLLM (BerriAI).** Your two open PRs plus the tiered-pricing fix are the lever. Once one merges, ask the maintainers on their Slack about contract work. Their posted roles are US-based ([YC jobs page](https://www.ycombinator.com/companies/litellm/jobs)).

## Paid, later (put on the calendar)

| Program | Window | Stipend |
|---|---|---|
| [CNCF LFX Mentorship 2027 Term 1](https://github.com/cncf/mentoring/blob/main/programs/lfx-mentorship/2027/01-Mar-May/README.md) | Applications Feb 3 to 16, 2027 (page says "Planning") | Adjusted for purchasing power, roughly $1,000 to $6,600 *unverified* |
| Google Summer of Code 2027 | Likely March 2027 (2026 ran Mar 16 to 31) | Adjusted for country and project size *unverified* |
| Outreachy May 2027 | Likely late Jan to Feb 2027 | $7,000 *unverified* |
| [NLnet NGI Zero](https://nlnet.nl/propose) | Current call closes Nov 3, 2026 | €5k to €50k, paid per milestone. A long shot unless your project fits open-internet themes |

For CNCF and GSoC, contributing to the organisation in December and January makes an application much stronger.

## Avoid

**Cash-bounty platforms are mostly dry or farmed right now.**
- The big programs on Algora (Cal.com, Twenty, Trigger.dev and others) had zero open bounties when checked.
- None of the LLMOps companies (BerriAI, Langfuse, Arize, Pydantic, Helicone, Traceloop) runs a bounty program.
- The "💎 Bounty" label is now mostly used by farm repos:
  - SecureBananaLabs/bug-bounty
  - UnsafeLabs/Bounty-Hunters
  - ClankerNation/OpenAgents
  - limitlessprojects/Go-Hybrid
  - claude-builders-bounty

  Some of these say "AI agents only", and some pay in crypto. Skip anything that asks for a fee, a token purchase or a wallet "verification".

**Unpaid or dead programs:**
- Season of KDE is unpaid.
- Huntr stopped taking open-source vulnerability reports in June 2026.
- IssueHunt looks dormant.

## Target projects

These are active projects that merge outside contributors' PRs, ranked best first. External-merge counts are estimates, because GitHub's "Contributor" badge also covers company staff.

| Project | Fit | Outside merges, last 30 days | Open PRs | First response | Paid angle | Rules |
|---|---|---|---|---|---|---|
| [openlit/openlit](https://github.com/openlit/openlit) | LLM token and cost telemetry, Python and TS | about 33 of 43 | 47 | same day | none seen | No CLA. Discuss big changes first |
| [open-telemetry/opentelemetry-python-genai](https://github.com/open-telemetry/opentelemetry-python-genai) | OTel GenAI token usage | about 10 of 25 sampled | 48 | about 1 day | CNCF, helps an LFX application | CLA. AI allowed per AGENTS.md |
| [pydantic/genai-prices](https://github.com/pydantic/genai-prices) | LLM price database | 12 | 21 | next day | Pydantic is hiring (not Pakistan per listing) | Post approach on the issue first |
| [PrefectHQ/prefect](https://github.com/PrefectHQ/prefect) | Orchestration, Azure and AWS integrations | about 40 | 106 | about 3 days | company-backed | Issue first. May close low-effort AI PRs |
| [getsentry/sentry-python](https://github.com/getsentry/sentry-python) | gen_ai token attributes | 7 | 41 | 0 to 4 days | Sentry is hiring (Toronto or Vienna) | Won't review agent-made PRs, so do this one by hand |
| [ag2ai/faststream](https://github.com/ag2ai/faststream) | async messaging, FastAPI | about 25 | 27 | same day | none | CLA |
| [pydantic/logfire](https://github.com/pydantic/logfire) | OTel and LLM observability | about 20 | 85 | same day | Pydantic is hiring | not checked |

Issues worth a look (unclaimed when checked; check again before starting):
- openlit [#1747](https://github.com/openlit/openlit/issues/1747): the ARM64 container ships x86-64 collector binaries. Docker multi-arch fix.
- opentelemetry-python-genai [#655](https://github.com/open-telemetry/opentelemetry-python-genai/issues/655): tool definitions leak when content capture is off. The reporter won't fix it.
- opentelemetry-python-genai [#572](https://github.com/open-telemetry/opentelemetry-python-genai/issues/572): async Bedrock via aiobotocore. Needs confirmation first.
- genai-prices [#332](https://github.com/pydantic/genai-prices/issues/332): Azure DataZone and regional SKU pricing. A good fit with your Azure background.
- genai-prices [#561](https://github.com/pydantic/genai-prices/issues/561): transcription usage extractors and duration pricing. Filed by a maintainer.
- prefect [#22028](https://github.com/PrefectHQ/prefect/issues/22028): Azure Container Apps jobs in prefect-azure.
- sentry-python [#8008](https://github.com/getsentry/sentry-python/issues/8008) and [#8010](https://github.com/getsentry/sentry-python/issues/8010): cached and reasoning tokens for Mistral and Hugging Face. Do these by hand, and ask first.

Avoid as flooded or closed to outside work:
- pydantic-ai (450 open PRs, assignment required)
- dspy, mem0, llama_index, mlflow and dagster
- Arize Phoenix (not accepting feature contributions)
- Helicone, Portkey, outlines and promptflow (no merges since September)
- Litestar, Opik, Agenta, Infracost, OpenMeter and Lago (mostly staff merges)
- the Azure SDK and CLI repos
