---
name: model-prompt-routing
description: Choose model and effort, and construct bounded prompts for delegated agents, sessions or media-generation tools.
license: MIT
metadata:
  version: "2.1"
---

# Model prompt routing

Use the resolved target model, not the caller's family. Project policy, role
permissions, acceptance and operator authority govern the assignment; this skill
does not expand them. OpenCode supplies the target's native system prompt.

## Task contract

State the goal, scope, relevant evidence, permitted actions, required result and
stop conditions once. Use concise prose or labeled sections, not a mandatory
template. Distinguish a bounded assessment from implementation through completion.
Routine choices within scope belong to the assigned agent.

Supply enough context to act without replaying ledgers or a whole repository.
Honor the target role's output/verdict contract rather than redefining it. When a
child cannot read policy or run Git/checks, inline the relevant hard requirements
and label supplied identity, ancestry and gate evidence as caller-provided.

Keep independent paired-review packets substantively identical and the second
initial packet blind to the first verdict/findings. Follow-up packets identify
only unresolved findings and materially changed behavior. Configure effort through
the model controls, weighing expected quality against total cost and latency.
There is no universal effort ceiling: higher effort, including supported `max`,
can be worthwhile on smaller models or demanding tasks. Respect explicit user
choices and actual installation restrictions; distinguish recommendations from
hard limits. This skill does not authorize delegation. Avoid generic thinking,
repeated verification or delegation mandates. The primary retains integration
and completion responsibility.

## Contextual guidance

Routine packets need only the contract above. Read a reference when the named
decision actually arises; do not load all model guides.

| Decision | Reference |
|---|---|
| Claude-specific packet adaptation or migration | [Claude guidance](references/claude-official-guides.md), matching model section only |
| GPT-6 (Astra/Sol/Luna) tier selection, workflow adaptation, effort or migration | [GPT-6 guidance](references/openai-gpt-6-official-guides.md) |
| Legacy GPT-5.6 target or provider/context accounting | [GPT-5.6 guidance](references/openai-gpt-5.6-official-guides.md) |
| Grok 4.7 target or migration | [Grok guidance](references/xai-grok-official-guides.md) |
| DeepSeek V4.1 Flash 1017 target | [DeepSeek guidance](references/deepseek-official-guides.md) |
| Muse Spark 1.3 Contributor target | [Muse guidance](references/meta-muse-official-guides.md) |
| GLM 5.3 Flash target | [GLM guidance](references/glm-official-guides.md) |
| Codex image or Grok image/video generation | [Media guidance](references/media-generation-guides.md) |
| Service-specific dispatch or local effort policy | Owning project's routing policy and runtime instructions |
| OpenCode/OpenChamber integration and local policy | [Integration](references/integration.md) |
| Worked task packets | [Examples](references/examples.md), relevant example only |

For another target without sourced family guidance, use the shared
contract rather than inventing prompt tricks. Fetch vendor sources only for the
specific migration or measured behavior question. Provider limits need provider
evidence; a model's API envelope does not establish its OAuth envelope.
