# Model prompt routing

Model-specific agent briefing, model selection and effort guidance for
**OpenCode V2 and OpenChamber**. A Markdown skill package with selectively loaded
references. It helps an agent make routing decisions; it does not automatically
switch models, install providers or launch workers.

## Install

Copy this entire directory, including `references/`, into one of:

- Project: `.opencode/skills/model-prompt-routing/`
- Global, on the OpenCode backend: `~/.config/opencode/skills/model-prompt-routing/`

The resulting entry point must be `model-prompt-routing/SKILL.md`. Install on
the machine running OpenCode, which may differ from the machine displaying
OpenChamber. OpenChamber uses the connected backend's skill and permission
configuration; this package needs no separate UI plugin.

In a session, ask the agent to load `model-prompt-routing`. OpenCode V2 also
documents explicit invocation with `@model-prompt-routing`. Confirm the loaded
base directory if an older copy exists: a later source with the same ID can
override it. Keep existing agent permissions and model settings.

See the [official OpenCode V2 skills documentation](https://opencode.ai/v2/docs/skills)
for discovery, precedence and permissions. Installation guidance checked
2026-10-25. This package has been statically checked; it has not been benchmarked
across every provider or OpenChamber version.

## Usage

Ask: "Use model-prompt-routing to recommend a model and effort for this bounded
bug fix, then prepare a brief. Keep my current model until I approve a change."

For an implementation task with a clear reproduction, a balanced model is a
reasonable starting point. Use the live catalog and local permissions rather
than assuming a particular provider ID exists. A brief could be:

> Fix the CSV parser's handling of quoted commas in `src/csv.ts`. The failing
> fixture is `tests/fixtures/quoted-comma.csv`; the parser currently splits the
> quoted field. Limit edits to the parser and relevant existing tests. Preserve
> the public API and add no dependencies. Run the repository's focused parser
> tests. Return the changed files, check results and any remaining blocker.
> Stop when this behavior works and its checks pass; ask if the fix requires an
> API change. Do not publish or deploy.

That example is illustrative, not a claim that those files exist in your project.
For assessment-only work, replace implementation authority with a request for
findings and evidence. Use OpenChamber sessions when the user wants a session
they can follow; use bounded subagents only where the current harness permits.

## Contents and policy

- `SKILL.md`: concise task contract and selective reference routing.
- `references/openai-gpt-6-official-guides.md`: current family, Sol 6.1 and Terra 6.1 guidance.
- `references/claude-official-guides.md`: current Claude model-specific guidance.
- `references/openai-gpt-5.6-official-guides.md`: full legacy-family guidance and
  API versus subscription accounting caveats.
- `references/integration.md`: session/subagent ownership, provider boundaries
  and single-source installation policy.
- `references/examples.md`: implementation, investigation, research and review
  packets, plus targeted adjustments for observed failures.
- `references/xai-grok-official-guides.md`: current Grok 4.7 guidance and the
  boundary with historical 4.6 documentation.
- `references/deepseek-official-guides.md`: DeepSeek V4.1 Flash 1017 identity,
  prompt encoding and inference/hosted-route distinctions.
- `references/meta-muse-official-guides.md`: Muse Spark 1.3 Contributor guidance,
  data-use policy and tier-specific effort support.
- `references/glm-official-guides.md`: GLM 5.3 Flash visual workflows and controls.
- `references/media-generation-guides.md`: Codex images, Grok images/video and
  subscription-versus-API access boundaries.

Model guidance is sourced from linked vendor documentation and is a starting
point, not a cross-vendor benchmark. Project rules own approval, delegation,
review requirements and effort policy. Set those in your own agent/project
configuration. There is no universal effort ceiling: choose higher effort,
including supported `max`, when quality gains justify the added cost and latency.
Vendor guidance is not proof that the installed adapter exposes a capability.

## Maintenance

Before changing model guidance, check the official family index and exact model
page for new material. Update the relevant section and its review date; do not
mark unreviewed sections verified. Separate vendor observations, local policy,
provider capabilities and measured results. Evaluate representative tasks when
claiming performance improvements. Static validation alone proves none.

Maintain one authoritative tree; runtime installations, mirrors and release
exports should be verified copies rather than independently edited versions.
Keep installation-specific policy outside this package and load it separately.
See [integration guidance](references/integration.md).

Derived from a locally maintained OpenCode skill. MIT licensed; see `LICENSE`.
Linked vendor documentation remains subject to its publishers' terms. This
package summarizes that material and is not an official vendor integration.
