# Contribution tracker

Each run of the "OSS contributions" routine updates this file. `PLAYBOOK.md` has the rules.

## Open pull requests

| Opened | Upstream PR | Fork branch | Fixes | Status | Last checked |
|---|---|---|---|---|---|
| 2026-10-18 | [BerriAI/litellm#47222](https://github.com/BerriAI/litellm/pull/47222) fix(http): honor `litellm.aclient_session` and `client_session` across HTTP handlers | `Vmnebula/litellm:fix/http-handler-client-sessions` | #47208 | CLA signed, bot reviews resolved, coverage OK. Waiting on maintainer approval. | 2026-10-18 |
| 2026-10-18 | [BerriAI/litellm#47223](https://github.com/BerriAI/litellm/pull/47223) feat(langsmith): populate `requester_metadata` into `extra.metadata` | `Vmnebula/litellm:feat/langsmith-extra-metadata` | #47018 | CLA signed, coverage OK. No review yet. | 2026-10-18 |

## Ready to open

These branches are pushed and need Muhammad to open the PR from the compare link.

| Prepared | Project | Branch | What it fixes | State |
|---|---|---|---|---|
| 2026-10-18 | BerriAI/litellm | `fix-tiered-pricing-malformed-range` | A pricing tier with `"range": []` or `null` crashes the proxy's pre-request budget estimate instead of being skipped. Self-found, no upstream issue. | Not pushed yet (no App access). Patch: `patches/litellm-tiered-pricing-malformed-range.patch`. PR text: `patches/litellm-tiered-pricing-malformed-range.PR.md`. Needs the live-proxy proof run before opening. |

## Merged or closed

None yet.

## Issues checked and skipped

| Issue | Reason |
|---|---|
| [BerriAI/litellm#46847](https://github.com/BerriAI/litellm/issues/46847) | The reporter claimed it; PR #46862 is open |
| [BerriAI/litellm#46999](https://github.com/BerriAI/litellm/issues/46999) | Claimed; PRs #47068 and #47106 are open |
| BerriAI/litellm#46364 | Claimed by Li-john1021; PRs #46420 and #46387 linked |
| BerriAI/litellm#45999 | Claimed by Mrun25; PR #46070 linked |
| BerriAI/litellm#46060 | PRs #46178 and #46065 linked |
| BerriAI/litellm#45948 | Claimed by Kylinny; PR #46046 linked |
| BerriAI/litellm#47248 | PR #47266 linked the same day it was opened |
| BerriAI/litellm#46050 | PR #46069 linked; report is unclear |
| BerriAI/litellm#46146 | PR #46148 linked |
| langfuse/langfuse-python#1834 | Reporter's PR #1833 open; assigned to a maintainer |
| langfuse/langfuse-python#1971 | Reporter's PR #1972 open |
| traceloop/openllmetry (all recent bugs) | 637 open PRs; every recent issue already has one |

## Run log

| Date (PKT) | Outcome |
|---|---|
| 2026-10-18 | Set up the playbook, tracker and routine. Checked #47222 and #47223: nothing to fix, both waiting on maintainers. |
| 2026-10-18 | Every listed issue checked in LiteLLM, langfuse-python and OpenLLMetry already had a PR. Found a bug by reading LiteLLM's cost code instead, fixed it with a regression test, and passed ruff, basedpyright and the three LIT/TQ/strict gates. Saved as a patch. |
