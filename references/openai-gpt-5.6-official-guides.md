# Official GPT-5.6 Prompting Guides

Legacy family: use [GPT-6 guidance](openai-gpt-6-official-guides.md) for GPT-6
targets. Keep this complete reference for actual GPT-5.6 targets and historical
launches; do not silently reinterpret their tier names as GPT-6 tiers.

Family prompting guidance rechecked on 2026-10-25. Model-specific context and
accounting figures below retain their original 2026-08-26 verification date;
re-fetch the exact model/access-route page before using them for current budgets.
Canonical pages remain authoritative as capabilities and limits change.

## Canonical Sources

- GPT-5.6 family prompting: [Prompting guidance for GPT-5.6 Sol](https://developers.openai.com/api/docs/guides/prompt-guidance-gpt-5p6.md)
- Current model selection: [Latest models](https://developers.openai.com/api/docs/guides/latest-model)
- Sol: [GPT-5.6 Sol](https://developers.openai.com/api/docs/models/gpt-5.6-sol)
- Terra: [GPT-5.6 Terra](https://developers.openai.com/api/docs/models/gpt-5.6-terra)
- Luna: [GPT-5.6 Luna](https://developers.openai.com/api/docs/models/gpt-5.6-luna)
- Migration: [Upgrade to GPT-5.6 Sol](https://developers.openai.com/api/docs/guides/upgrading-to-gpt-5p6-sol.md)
- Codex availability: [Codex models](https://developers.openai.com/codex/models)
- Codex allowance accounting: [Codex pricing](https://developers.openai.com/codex/pricing)

## Selection Rule

1. Resolve the delegated target's provider, model ID, tier, and configured
   effort before constructing the packet.
2. Use `SKILL.md` alone for routine packet construction.
3. For prompt migration or a measured behavior problem, fetch the family
   prompting guide and only the relevant migration or model page.
4. For context or cost decisions, fetch the exact API or Codex source for the
   actual access route. Never transfer an API limit or multiplier to OAuth
   without authoritative evidence.
5. Extract only task-relevant instructions. Never copy a whole guide into a
   system prompt, task packet, or repository policy.
6. Project policy, tool permissions, acceptance criteria, and operator approval
   remain authoritative over vendor examples.

## Stable Family Guidance

- Keep prompts lean and outcome-first. State each rule once.
- Default to direct prose or short labeled sections. For complex prompts, the
  official starting structure uses `Role`, `Personality`, `Goal`, `Success
  criteria`, `Constraints`, `Tools`, `Output`, and `Stop rules`; include only
  sections that change behavior.
- Make success criteria, evidence requirements, authority, approval boundaries,
  and stop conditions explicit.
- Route tools directly for the task instead of adding generic tool-use prose.
- Request sparse, outcome-based progress only when progress is user-facing.
- Use configured effort rather than asking the model to expose or imitate
  reasoning.
- Make surgical prompt changes in response to measured failures and evaluate
  them on representative tasks.

## Tier Selection

- **Sol:** frontier reasoning and coding for complex, ambiguous, high-value, or
  high-stakes work where quality dominates latency and allowance cost.
- **Terra:** balanced capability, latency, and cost for ordinary implementation,
  analysis, and review work with bounded complexity.
- **Luna:** fastest, lowest-cost tier for clear, repeatable, high-volume work
  with narrow output contracts and low ambiguity.

The tiers share family prompting guidance. Change the selected model and effort
to fit the task; do not invent tier-specific personalities or reasoning rituals.

## Context And Accounting

Keep access routes separate:

- The API pages checked on 2026-08-26 exposed up to a 1.05M-token context window: 922K
  maximum input plus up to 128K output.
- For API requests whose input exceeds 272K tokens, the full request enters the
  long-context band: input is priced at 2x and output at 1.5x. Re-check current
  model pricing before making production cost decisions.
- An OpenCode Codex OAuth catalog may expose a smaller envelope than the API.
  Inspect the actual provider adapter and catalog; no installation-specific
  envelope is a universal OAuth guarantee.
- Public Codex allowance documentation says larger context consumes more plan
  allowance, but does not publish the API long-context multipliers as OAuth
  allowance multipliers. Do not claim an exact OAuth multiplier without new
  authoritative evidence.

Context limits and billing are harness constraints, not instructions to paste
into delegated prompts. Keep ordinary working context below applicable cliffs
through progressive disclosure and context management.

## Additional guidance from the refreshed official page

- Preserve explicit user values and use decision rules rather than keyword maps
  or invented universal defaults. Keep required facts when shortening output.
- Parallelize independent reads; sequence prerequisites and synthesize before
  acting. Empty or suspiciously narrow retrieval merits one or two meaningful
  fallbacks. Cite retrieved evidence and label inference or conflicting sources.
- Programmatic Tool Calling suits bounded deterministic reduction of large
  results: filtering, joining, deduplication, aggregation and batching similar
  records. Multiple calls alone do not justify it. Define eligible tools, schema,
  retry limits and a handoff back to direct judgment. Keep approvals, citations
  and semantic decisions on the appropriate direct path. Check both program
  output and the final assistant response.
- Preserve assistant phase values when replaying history. Compact at useful
  milestones while retaining constraints. Persisted reasoning helps stable
  objectives; stale reasoning can anchor an outdated approach.
- For frontend changes, preserve existing tokens, components and responsive
  states. Render and inspect output. Use original image detail when spatial
  precision justifies the extra cost.
- Migrate one variable at a time: model first with existing effort, then remove
  obsolete scaffolding and add only targeted mitigations for measured failures.

## Maintenance

Re-fetch the canonical pages before changing a production harness, adopting a
new GPT-5.6 revision or access route, changing context budgets, or responding to
a repeated evaluation failure. When this index and an official page disagree,
follow the official page and update this file's verification date and summary.
