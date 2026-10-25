# GPT-6 family official guidance (Astra, Sol, Luna)

## Current family and earlier Sol

The current official family guide highlights GPT-6 Astra, GPT-6.1 Sol and
GPT-6 Luna. GPT-6 Sol is the earlier Sol version. Resolve the exact provider ID
and available variants in the installed catalog instead of assuming a local pin.
GPT-6.1 Sol supports `low`, `medium` (default), `high`, `xhigh`, and `max`;
neither `none` nor `minimal` is supported. Preserve supported effort and map
unsupported `none`/`minimal` to `low`, while respecting explicit user choices.

Family guide, model-selection page and GPT-6.1 Sol model page checked 2026-10-25.
Older Astra/Luna pricing observations are dated explicitly below. Fetch relevant
sources again when behavior or support changes; this is not an adapter guarantee.

- Family guide ("Using GPT-6", prompting + migration): https://developers.openai.com/api/docs/guides/latest-model.md
- Models: https://developers.openai.com/api/docs/models/gpt-6-astra, https://developers.openai.com/api/docs/models/gpt-6-sol, https://developers.openai.com/api/docs/models/gpt-6-luna
- Codex availability: https://developers.openai.com/codex/models
- GPT-6.1 Sol: https://developers.openai.com/api/docs/models/gpt-6.1-sol.md
- Model selection: https://developers.openai.com/api/docs/guides/model-selection.md
- OpenAI migration skill: https://github.com/openai/codex/tree/main/codex-rs/skills/src/assets/samples/openai-docs

## Tiers

The GPT-6 tiers shift down relative to GPT-5.6. Map by role and cost, not by
name alone:

- **Astra**: flagship for complex, ambiguous, high-stakes work.
  No `none` effort. Successor to the 5.6 Sol frontier role.
- **GPT-6.1 Sol**: balanced intelligence and cost. A starting point for
  ordinary implementation, analysis, exploration and
  bounded review. Successor to 5.6 Terra; also the name-successor of 5.6 Sol.
- **Luna**: cheapest family tier for high-volume, narrow contracts.

The current family lineup has no Terra. Map the role, not the same-named tier.
The original 2026-09-22 reference recorded Astra $10/$50 and Luna $0.1/$0.5
per million input/output tokens and 1.05M context for the then-current family;
recheck exact model pages before treating those historical figures as current.

GPT-6.1 Sol's current API page specifies 1,050,000 context, 922,000 maximum input
and 128,000 output. Standard per-million-token prices: $2 input, $0.10 cached
input, $2.50 cache writes and $10 output. Above 272K input the full request uses
2x input/cache and 1.5x output pricing. Service modes and regional processing
change rates; these are not subscription allowance or adapter context promises.

The current selection page suggests Luna low for fine-grained edits and simple
extraction; Luna xhigh for context gathering under clear constraints; Sol 6.1
medium for complex technical drafts and xhigh for polished deliverables or
conflicting evidence; Astra low for nuanced concise writing, medium for ambitious
projects and xhigh for demanding analysis. Treat these as vendor starting points,
not equivalent effort across models or authorization to override local settings.

## Prompting

The guide's prompting observations come from Astra; OpenAI says to evaluate them
on the selected model. It highlights stronger sensitivity to skills and
AGENTS.md, more clarification questions, heavy list/markdown writing, less
delegation than some coordinators need, and excess testing on small tasks.
State each instruction once and make role, acceptance criteria, autonomy and
stopping conditions explicit. Ask for action with approval only after a concrete
reviewable result where the project allows it. Preserve the owning project's
writer, approval and child-depth boundaries; do not copy the guide's
recursive-delegation example as authorization.

## Migration

Official migration advice preserves effort initially; `minimal` becomes `low`.
Astra and GPT-6.1 Sol have no `none`; earlier GPT-6 Sol and Luna support `none`.
Choose higher effort when its expected value justifies cost and latency. Use the owning
project's configured role default and explicit task launch settings; local
defaults are not official or measured effort equivalences. Evident difficulty
can justify higher effort before any failure. Review coverage is independent of
effort; preserve specialized models, permissions and budgets.

Astra and GPT-6.1 Sol require Responses for tool calling; their Chat Completions
support is without tools. Earlier GPT-6 Sol/Luna tool calling through Chat
Completions requires effort `none`; use Responses for reasoning with tools.
Drop `temperature`/`top_p`/`top_logprobs`
when effort is not `none`. Async tools, mid-turn steering and cache-preserving
effort changes require harness support; prompts alone do not enable them.
Published API context/pricing must not be treated as verified ChatGPT OAuth
quota or context behaviour. Keep provider implementation changes separate from
agent prompt migration.

Cache-preserving effort changes use `configuration_update` on supported routes;
keep the request-level setting stable and check compatibility before integration.
For GPT-5.5-or-earlier migrations the family guide replaces
`prompt_cache_retention` with `prompt_cache_options.ttl: "30m"`. These are API
integration changes, not child-prompt instructions.

Do not sweep started or historical launch records. Preserve historical
manifests, fixtures and cheaper workers. Compare accepted results, correction
turns and total usage without adding an evaluation workflow to ordinary tasks.
