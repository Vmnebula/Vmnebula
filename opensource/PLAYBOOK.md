# Open-source contribution playbook

The scheduled "OSS contributions" routine follows this playbook. It runs 3 times a day until 2026-11-18. Each run starts in a fresh container. It reads this file and `TRACKER.md` from branch `claude/opensource-contributions-monthly-3hxkll`, does its work, and writes back to `TRACKER.md`.

Do not merge this branch into `main`. It is working state, not profile content.

## Goal

The goal is merged pull requests in projects close to Muhammad's own work: LLM cost tracking, observability, FastAPI, and cloud infrastructure. Each one should be a link he can show on Mercor, LinkedIn, and in interviews.

Quality counts more than volume. A PR that gets closed as low-effort or duplicate does more harm than a run that does nothing.

## Target projects

| Upstream | Fork | Why it fits |
|---|---|---|
| BerriAI/litellm | Vmnebula/litellm | LLM gateway; its spend and cost tracking overlaps with Substacker |
| langfuse/langfuse-python | not forked yet | LLM observability SDK |
| traceloop/openllmetry | not forked yet | OpenTelemetry instrumentation for LLM apps |
| Arize-ai/phoenix | not forked yet | LLM tracing and evals |

A run can push a branch only to a fork where the Claude GitHub App is installed. Otherwise, it saves the change as `opensource/patches/<project>-<slug>.patch` on this branch and records that in the tracker.

## Each run, in order

1. **Date check.** On or after 2026-11-18, disable the routine and stop.
2. **Follow up on open PRs** listed in `TRACKER.md`. Read each PR page and act in this order:
   - A merge conflict: merge upstream's default branch into the fork branch.
   - A failing check caused by the PR's own change: fix it.
   - Changes a human reviewer asked for: make them.

   Run the project's checks, then push. Never force-push or rewrite history. Don't post replies to reviewers; draft the reply text in the run summary for Muhammad to post.
3. **Limit open work.** Start a new fix only when that upstream has fewer than 3 PRs open and unreviewed, and fewer than 6 are open overall.
4. **Pick an issue** that meets every one of these conditions:
   - It is open and unassigned.
   - It has no linked PR, and no open PR mentions its number.
   - Nobody has commented that they are working on it.
   - It was opened in the last 30 days.
   - It is in the project's open-source code, not enterprise-only code.
   - The fix plus tests fits in about 200 changed lines.

   Prefer cost and spend tracking, logging and observability integrations, and HTTP or client handling. Add every issue you rule out to the "skipped" table with the reason, so later runs don't recheck it.
5. **Reproduce, then fix.** Write the regression test first and confirm it fails. Then fix the code and run the project's own checks. For LiteLLM, read `CONTRIBUTING.md` and `AGENTS.md` first, then run `make format`, `make lint` and `uv run pytest tests/unit/<file> -v`.
6. **Push to the fork.**
   - Name the branch `fix/<slug>` or `feat/<slug>`.
   - Use Conventional Commits.
   - Set the git author to `Muhammad Osama Amin <muhammad.osama@vmnebula.com>`; that is the identity on the signed LiteLLM CLA.
   - Don't open the upstream PR. Instead, add these to `TRACKER.md` under "Ready to open": the compare URL, and a PR title and body filled in from the upstream PR template. The body must say the change was prepared with Claude Code.
7. **When nothing qualifies,** log "no qualifying issue" and stop. That is a normal outcome.
8. **Save state.** Commit `TRACKER.md` and any patch to this branch, then push.

## Never

- Take an issue someone else has claimed, or duplicate an open PR.
- Comment on upstream issues or PRs, request reviews, or ping maintainers.
- Inflate the count with typo-only changes, pricing-JSON-only edits, or unrelated refactors.
- Skip, weaken, or delete tests to get CI green.
