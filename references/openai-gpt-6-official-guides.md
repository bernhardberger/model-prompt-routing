# GPT-6 family official guidance (Astra, Sol, Terra, Luna)

## Current family and earlier Sol

The current official family guide highlights GPT-6 Astra, GPT-6.1 Sol,
GPT-6.1 Terra and GPT-6 Luna. GPT-6 Sol is the earlier Sol version. Resolve the exact provider ID
and available variants in the installed catalog instead of assuming a local pin.
GPT-6.1 Sol supports `low`, `medium` (default), `high`, `xhigh`, and `max`;
neither `none` nor `minimal` is supported. Preserve supported effort and map
unsupported `none`/`minimal` to `low`, while respecting explicit user choices.

Family guide, model-selection page and GPT-6.1 Sol model page checked 2026-10-25.
Terra model page and the family/selection guidance also checked 2026-10-25.
Older Astra/Luna pricing observations are dated explicitly below. Fetch relevant
sources again when behavior or support changes; this is not an adapter guarantee.

- Family guide ("Using GPT-6", prompting + migration): https://developers.openai.com/api/docs/guides/latest-model.md
- Models: https://developers.openai.com/api/docs/models/gpt-6-astra, https://developers.openai.com/api/docs/models/gpt-6-sol, https://developers.openai.com/api/docs/models/gpt-6-luna
- Codex availability: https://developers.openai.com/codex/models
- GPT-6.1 Sol: https://developers.openai.com/api/docs/models/gpt-6.1-sol.md
- GPT-6.1 Terra: https://developers.openai.com/api/docs/models/gpt-6.1-terra.md
- Model selection: https://developers.openai.com/api/docs/guides/model-selection.md
- OpenAI migration skill: https://github.com/openai/codex/tree/main/codex-rs/skills/src/assets/samples/openai-docs

## Tiers

The GPT-6 tiers shift down relative to GPT-5.6. Map by role and cost, not by
name alone:

- **Astra**: flagship for complex, ambiguous, high-stakes work.
  No `none` effort. Successor to the 5.6 Sol frontier role.
- **GPT-6.1 Sol**: balanced intelligence and cost. A starting point for
  ordinary implementation, analysis, exploration and
  bounded review. The initial GPT-6 lineup placed Sol in the former 5.6 Terra
  role; that historical mapping does not replace current task-level selection.
- **GPT-6.1 Terra**: fast, efficient visual reasoning, precise computer use,
  natural writing and scoped code fixes. Compare with Sol on representative tasks.
- **Luna**: cheapest family tier for high-volume, narrow contracts.

Map by the task and exact model version, not the same-named tier alone.
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

## GPT-6.1 Terra: usage and prompting

OpenAI recommends Terra for product-photo matching, technical drawings, acting
on application screens, drafting/revising text and scoped code fixes. Give it
clear inputs, requirements and a way to verify the result. These are vendor
starting points, not measured superiority in this installation.

- Start at `medium` (the default), raising effort when quality gains justify
  the extra time and tokens. Supported levels are `none`, `low`, `medium`,
  `high`, `xhigh` and `max`; `minimal` is not supported.
- For writing, specify audience and voice, preserve required facts and
  qualifications, and judge usefulness rather than brevity alone.
- For computer use, define the outcome and require reopening the saved record
  or page, checking unrelated data was preserved, and matching the completion
  report to the actual result. Keep the project's action and approval boundaries.
- For code, name relevant regression checks; for interactive interfaces, inspect
  the rendered result on desktop and mobile where applicable.
- Compare Terra with GPT-6.1 Sol on the same inputs and effort, including review
  and repair time. Then vary effort while holding model and inputs fixed. This
  is selection guidance, not a mandatory comparison on every ordinary task.

The checked sources provide Terra usage/migration guidance rather than a separate
Terra-specific behavioral prompting playbook. The shared prompting observations
below come from Astra and need evaluation on Terra.

Terra's API page specifies 1,050,000 context, 922,000 maximum input and 128,000
maximum output tokens. Standard per-million-token prices are $1 input, $0.05
cached input, $1.25 cache writes (30-minute retention) and $5 output. Above 272K
input the full request uses 2x input/cache and 1.5x output pricing. Retention,
service modes and regional processing can change rates. These API figures do
not establish subscription quotas or the installed adapter's capabilities.

When migrating from GPT-5.6 Terra, compare representative images and workflows
at the same supported effort. Terra 6.1 requires Responses for tool calling,
including at `none`; do not inherit an older model's Chat Completions tool route.

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
Astra and GPT-6.1 Sol have no `none`; GPT-6.1 Terra, earlier GPT-6 Sol and Luna
support `none`.
Choose higher effort when its expected value justifies cost and latency. Use the owning
project's configured role default and explicit task launch settings; local
defaults are not official or measured effort equivalences. Evident difficulty
can justify higher effort before any failure. Review coverage is independent of
effort; preserve specialized models, permissions and budgets.

Astra, GPT-6.1 Sol and GPT-6.1 Terra require Responses for tool calling; their Chat Completions
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
