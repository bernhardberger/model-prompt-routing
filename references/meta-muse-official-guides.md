# Muse Spark 1.3 Contributor

Reviewed 2026-10-25. Distinguish the hosted Contributor model from Standard,
Muse Code subscription behavior, Muse Wonder and the open-weight Spark release.

## Sources

- [Models and Contributor policy](https://dev.meta.ai/docs/models)
- [Reasoning controls](https://dev.meta.ai/docs/reasoning)
- [OpenCode one-shot game recipe](https://dev.meta.ai/docs/cookbook/one-shot-game-dev)

The models page, reasoning controls and cookbook were inspected. Recheck exact
request syntax before changing an adapter. Cookbook examples are
task-specific demonstrations, not evidence that all projects work in one pass.

## Prompting and selection

- Use the shared task contract. Supply the project's load-bearing constraints,
  the intended experience, technical requirements and explicit acceptance criteria.
  Meta's OpenCode game recipe uses `AGENTS.md` plus one structured task prompt.
- Preserve the relevant coordinate, collision, state or domain invariants instead
  of asking vaguely for a polished result. Require verification appropriate to
  the result; a one-shot demonstration is not a reason to skip tests or inspection.
- The current model page positions Spark for high-volume, latency-sensitive or
  cost-sensitive tasks and tight tool loops. Treat that as a starting point,
  not a measured cross-provider ranking.
- The page documents text, image, video, audio and PDF inputs, but specifically
  warns that Spark 1.3 audio understanding is not fully supported and may degrade.
  Do not infer robust audio capability from the modality list alone.

## Contributor and effort boundaries

- `muse-spark-1.3-contributor` is not just a cheaper spelling of Standard:
  Contributor content may be used to train future Meta models. Confirm that the
  task's code, files and context are suitable for that data policy before routing
  them there. Do not silently replace a private-data route with Contributor.
- The official model page states that Standard supports `max` but the Contributor
  model does not. Subscription announcements or third-party mappings are not
  enough to override that API distinction. Resolve any conflicting route-specific
  claims against its current catalog and provider documentation.
- A cookbook's effort naming does not establish equivalence between `high`,
  `xhigh` and `max`. Use the exact supported variant and choose effort based on
  expected benefit, latency and total cost.
- The documented context window is 1,048,576 tokens; verify the adapter's actual
  limits rather than automatically filling it.
