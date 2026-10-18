Title: fix(cost): skip tiered pricing tiers with a malformed range instead of raising

Base: BerriAI/litellm main
Head: Vmnebula/litellm fix-tiered-pricing-malformed-range

Before opening, fill in the two <...> placeholders from your own run (see "Proof of fix" in
the session summary), then delete this header down to the line of dashes.

------------------------------------------------------------------------------------------

## TLDR

Problem this solves:

- A pricing tier with `"range": []` or `"range": null` raises instead of being skipped
- The proxy budget estimate runs this before every budgeted request

How it solves it:

- Drop tiers without a two item range before sorting them, not after

## User Flow

Before: keys with a budget can't call a model whose tier table has one incomplete tier

1. The admin adds a deployment whose `model_info.tiered_pricing` has a tier with `"range": []` next to a valid `[0, 32000]` tier
2. A developer whose key has `max_budget` set sends POST http://localhost:4000/v1/chat/completions for that model
3. The request fails with <status code and error text from your Before run>

After: the same request is priced from the valid tier and goes through

1. The admin adds the same deployment
2. The developer sends the same POST http://localhost:4000/v1/chat/completions
3. The response comes back 200 and the request shows up in the logs priced at the `[0, 32000]` tier rate

## Pre-Submission checklist

**Please complete all items before asking a LiteLLM maintainer to review your PR**

- [x] I have added meaningful tests
- [x] The handful of test files covering my change pass locally, e.g. `uv run pytest tests/unit/<your_test_file>.py -v`. Leave the suites (`make test-unit-*`, `make test-unit`) to CI: it finishes in ~15 minutes where a laptop takes an hour or more
- [ ] My PR passes all required CI/CD checks (e.g., lint, schema.d.ts sync check, etc.)
- [x] My PR's scope is as isolated as possible; it only solves 1 specific problem
- [ ] Every automated review on my PR's latest commit has finished, and I have addressed or replied to each of its findings before requesting a maintainer review

## Delays in PR merge?

If you're seeing a delay in your PR being merged, ping the LiteLLM Team on [Slack (#pr-review)](https://join.slack.com/t/litellmossslack/shared_invite/zt-3o7nkuyfr-p_kbNJj8taRfXGgQI1~YyA).

## Screenshots / Proof of Fix

Shared setup is a `config.yaml` with one deployment, `openai/gpt-4o-mini` under the name `tiered-model`, whose `model_info.tiered_pricing` is `[{"range": [], "input_cost_per_token": 9e-06, "output_cost_per_token": 9e-06}, {"range": [0, 32000], "input_cost_per_token": 1e-06, "output_cost_per_token": 2e-06}]`, plus a virtual key created with `"max_budget": 1`

### Before (<merge base sha>)

1. `curl -sS http://localhost:4000/v1/chat/completions -H "Authorization: Bearer $KEY" -H "Content-Type: application/json" -d '{"model": "tiered-model", "messages": [{"role": "user", "content": "hello"}], "max_tokens": 100}'`
2. <paste output>

### After (<PR tip sha>)

1. Same curl as above
2. <paste output>

## Type

🐛 Bug Fix

## Caveats (if any)

### Low

- Only the shape of `range` is checked, so string bounds like `["0", "32000"]` still raise on comparison

## Final Attestation

- [x] The tests check the right things, including the edge cases, and regressions in the respective real-world customer use-cases are not possible after this PR
