# Open-source contribution playbook

The scheduled "OSS contributions" routine follows this playbook. It runs 3 times a day until 2026-11-18. Each run starts in a fresh container. It reads this file and `TRACKER.md` from branch `claude/opensource-contributions-monthly-3hxkll`, does its work, and writes back to `TRACKER.md`.

Do not merge this branch into `main`. It is working state, not profile content.

## Goal

The goal is merged pull requests in projects close to Muhammad's own work: LLM cost tracking, observability, FastAPI, and cloud infrastructure. Each one should be a link he can show on Mercor, LinkedIn, and in interviews.

Quality counts more than volume. A PR that gets closed as low-effort or duplicate does more harm than a run that does nothing.

## Target projects

Ranked by how likely an outside PR is to merge (checked 2026-10-18; see `OPPORTUNITIES.md`).

| Upstream | Fork | Why it fits | House rules |
|---|---|---|---|
| openlit/openlit | not forked yet | LLM token and cost telemetry (Python and TS). Merges outside PRs the same day. | No CLA. Discuss big changes first. Many issues are filed by people who send the PR themselves within a day, so check open PRs before starting. |
| pydantic/genai-prices | not forked yet | LLM price database, the closest match to Substacker. Pydantic is hiring. | Ask first: post the approach on the issue and wait for a maintainer; a triage bot blocks new-provider PRs until one decides. |
| open-telemetry/opentelemetry-python-genai | not forked yet | OTel GenAI token-usage instrumentation. CNCF, so it helps an LFX mentorship application. | Muhammad must sign the OTel CLA. Read its AGENTS.md. Some issues need confirmation before work starts. |
| BerriAI/litellm | Vmnebula/litellm | LLM gateway with spend tracking. Very crowded, so only self-found bugs. | No `/` in branch names, no Claude attribution, live-proxy proof in the PR body. |
| PrefectHQ/prefect | not forked yet | Orchestration with Azure and AWS integrations. | Ask first: every bug fix needs an issue confirmed by a maintainer. May close low-effort AI PRs. |

Don't prepare PRs for projects whose rules refuse or restrict agent-made PRs. getsentry/sentry-python says it won't review them, so Muhammad should only work there by hand.

Skip these as too crowded or not merging outside work:
- langfuse-python
- openllmetry
- pydantic-ai
- dspy
- mem0
- llama_index
- Arize Phoenix
- Helicone
- Litestar
- Opik
- Agenta
- the Azure SDK and CLI repos

A run can push a branch only to a fork that exists and is covered by the Claude GitHub App. Runs can't create forks. Without a fork, save the change as `opensource/patches/<project>-<slug>.patch` on this branch, record that in the tracker, and ask Muhammad in the summary to fork the project.

**Ask-first projects.** Write the approach comment under "Comments to post" in `TRACKER.md` for Muhammad to post. A later run reads the issue page. Only once a maintainer has agreed does it implement the fix.

## Each run, in order

1. **Date check.** On or after 2026-11-18, disable the routine and stop.
2. **Follow up on open PRs** listed in `TRACKER.md`. Read each PR page and act in this order:
   - A merge conflict: merge upstream's default branch into the fork branch.
   - A failing check caused by the PR's own change: fix it.
   - Changes a human reviewer asked for: make them.

   Run the project's checks, then push. Never force-push or rewrite history. Don't post replies to reviewers; draft the reply text in the run summary for Muhammad to post.
3. **Limit open work.** Start a new fix only when that upstream has fewer than 3 PRs open and unreviewed, and fewer than 6 are open overall.
4. **Prefer a bug you found yourself.** In these projects, almost every listed issue has a PR within a day; on 2026-10-18 every issue checked already had one. Reading the project's code in Muhammad's areas (cost and spend tracking, budgets, logging integrations) and proving a bug with a failing test finds work nobody else is racing for. Before writing it up, search open PRs and issues for the function name to make sure nobody has it already.

   If you go after a listed issue instead, also check the issue page header for linked PRs; the sidebar's Development section misses them. Pick an issue that meets every one of these conditions:
   - It is open and unassigned.
   - It has no linked PR, and no open PR mentions its number.
   - Nobody has commented that they are working on it.
   - It was opened in the last 30 days.
   - It is in the project's open-source code, not enterprise-only code.
   - The fix plus tests fits in about 200 changed lines.

   Prefer cost and spend tracking, logging and observability integrations, and HTTP or client handling. Add every issue you rule out to the "skipped" table with the reason, so later runs don't recheck it.
5. **Reproduce, then fix.** Write the regression test first and confirm it fails. Then fix the code and run the project's own checks. For LiteLLM, read `CONTRIBUTING.md` and `AGENTS.md` first, then run `make format`, `make lint` and `uv run pytest tests/unit/<file> -v`.
6. **Push to the fork.** The project's own `AGENTS.md` and `CONTRIBUTING.md` override the defaults below.
   - By default, name the branch `fix-<slug>`. LiteLLM forbids `/` in branch names.
   - Use Conventional Commits.
   - Set the git author to `Muhammad Osama Amin <muhammad.osama@vmnebula.com>`; that is the identity on the signed LiteLLM CLA.
   - Follow the project's rule on AI attribution. LiteLLM forbids Claude attribution in commits and PR bodies.
   - Don't open the upstream PR. Instead, add these to `TRACKER.md` under "Ready to open": the compare URL, and a PR title and body filled in from the upstream PR template, following any comments in it as rules.
   - Some projects require proof that needs real API keys, such as LiteLLM's curl against a live proxy. Write the exact commands and leave clearly marked placeholders for Muhammad to fill in. Never invent output.
7. **When nothing qualifies,** log "no qualifying issue" and stop. That is a normal outcome.
8. **Save state.** Commit `TRACKER.md` and any patch to this branch, then push.

## Expensify bounties (paid, $175 to $250 each)

Muhammad has a verified Upwork account, so he can take these. Each run, after the steps above:

1. Read the [Help Wanted + External list](https://github.com/Expensify/App/issues?q=is%3Aissue+is%3Aopen+label%3A%22Help+Wanted%22+label%3AExternal+sort%3Acreated-desc). Only consider issues where:
   - "Help Wanted" was added in the last 12 hours or so
   - no Contributor+ reviewer has picked a proposal (look for "🎀👀🎀" or "proposal looks good")
   - it isn't labelled "Needs Reproduction"
   - the fix is TypeScript logic in the app, not backend, native-only or pure styling
2. Read every existing proposal. Write one only if you can show, on current main, a root cause or fix that none of them names. Expensify rejects proposals that repeat an earlier one.
3. Use the official proposal template, with file:line references on main. Put it under "Expensify proposals to post" in `TRACKER.md` with:
   - the issue link
   - the bounty
   - how many proposals existed when you wrote it
   - a "Before posting" checklist: reproduce on a test account, confirm no proposal was accepted in the meantime, confirm main still matches
4. Never post on Expensify. New contributors may hold only one Expensify job at a time, so skip this section while `TRACKER.md` shows one in progress.

Most runs will find nothing. On 2026-10-18, all 15 open issues were already decided or had 4 to 7 detailed proposals.

## Never

- Take an issue someone else has claimed, or duplicate an open PR.
- Comment on upstream issues or PRs, request reviews, or ping maintainers.
- Inflate the count with typo-only changes, pricing-JSON-only edits, or unrelated refactors.
- Skip, weaken, or delete tests to get CI green.
