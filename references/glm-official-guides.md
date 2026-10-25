# GLM 5.3 Flash

Reviewed 2026-10-25 against the official [GLM-5.3-Flash/FlashX overview and best
practices](https://docs.z.ai/guides/vlm/glm-5.3-flash). This includes concrete
vendor workflow examples; their benchmark claims are not local evaluations.

## Prompting patterns worth adapting

- For UI work, provide related screenshots or recordings and identify page
  relationships, shared components, interaction states and acceptance criteria.
  Run the result and compare matching views rather than judging source alone.
- For documents, specify audience, structure, style and editable output formats.
  Render and inspect for overflow, cropping, overlap and alignment.
- For research, distinguish disclosed facts, assumptions and derived conclusions;
  retain supporting sources and check formulas and consistency.
- For 3D/CAD, provide spatial or dimensional constraints, make uncertain dimensions
  explicit, and compare fixed-camera renders with the reference.
- For games or GUI work, verify complete user flows, not merely a generated scene.

These are selective patterns, not a mandatory lifecycle. Vendor examples include
fixed iteration counts and goal mode: do not turn those into default repeated
reviews, autonomous launches or permission to use unavailable tools. Stop when
the task's actual acceptance criteria and relevant checks are met.

## Model and integration controls

- `glm-5.3-flash` and `glm-5.3-flashx` are separate serving choices. The page
  documents Flash on the GLM Coding Plan, but not FlashX; verify current access.
- Inputs include text, images, video and files; output is text. This supports
  visual inspection and tool-driven media workflows, not native image generation.
- The vendor recommends `temperature: 1`, `top_p: 0.95`, `reasoning_effort: max`,
  enabled thinking and `thinking.clear_thinking: false`. It says thinking cannot
  be disabled. These are provider controls, not instructions to paste into tasks.
- `max` can be an appropriate choice here. Evaluate its quality benefit and
  latency/cost consciously; do not impose an unrelated large-model ceiling or
  treat a vendor recommendation as a requirement for every task.
- Preserve thinking through the supported adapter rather than manually editing
  reasoning text. Streaming/tool streaming support also belongs to the adapter.
- The documented context and output limits are 1M and 128K respectively; verify
  the selected route before using them as session budgets.
