# Official Claude Prompting Guides

Current model prompting pages, Opus 5 and Sonnet 5 prompting, and Opus/Sonnet/
Haiku 5.5 migration rechecked on 2026-10-25. Other specification claims retain
their original 2026-10-07 date where identified below. Canonical pages remain
authoritative; these are vendor observations, not local performance measurements.

**Current Opus and Sonnet guidance is for 5.5.** Opus 5 and Sonnet 5 are
outdated models, retained below only for historical interpretation and migration
from an explicitly identified old target. Do not use their sections for new
assignments or as additional instructions for 5.5.

## Canonical Sources

- All current Claude models: [Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices.md)
- Claude Fable 5.1 and Mythos 5.1: [Prompting Claude Fable 5.1](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-1)
- Claude Fable 5 and Mythos 5 (legacy): [Prompting Claude Fable 5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5)
- Claude Haiku 5.5: [Prompting Claude Haiku 5.5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-haiku-5-5)
- Haiku 5.5 migration: [Migrating to Claude Haiku 5.5](https://platform.claude.com/docs/en/models/haiku-5-5/migration-guide)
- Claude Sonnet 5.5: [Prompting Claude Sonnet 5.5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-sonnet-5-5)
- Sonnet 5.5 migration: [Migrating to Claude Sonnet 5.5](https://platform.claude.com/docs/en/models/sonnet-5-5/migration-guide)
- Claude Sonnet 5 (legacy): [Prompting Claude Sonnet 5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-sonnet-5)
- Claude Opus 5.5: [Prompting Claude Opus 5.5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5-5)
- Opus 5.5 migration: [Migrating to Claude Opus 5.5](https://platform.claude.com/docs/en/models/opus-5-5/migration-guide)
- Claude Opus 5 (legacy): [Prompting Claude Opus 5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5)

## Selection Rule

1. Resolve the delegated target's actual model family and version.
2. Use `SKILL.md` alone for routine packet construction.
3. For migration, harness design, or a measured behavior problem, fetch the
   general best-practices page and exactly one matching model page.
4. Prefer the matching model page when its guidance qualifies a general rule.
5. Extract only instructions relevant to the current packet. Never copy a whole
   guide into a system prompt, task packet, or repository policy.
6. Project policy, tool permissions, acceptance criteria, and operator approval
   remain authoritative over vendor examples.

## Stable General Guidance

- Be clear, direct, and explicit about desired output, constraints, and actions.
- Add only context and motivation that help the model make the requested
  judgment. Use a truthful role sentence when it materially focuses expertise.
- For complex prompts that mix instructions, context, examples, variable inputs,
  or multiple documents, use descriptive XML tags when they make boundaries less
  ambiguous. Ordinary prompts can use clear prose, headings, or lists. Put long
  documents first and the query or task last.
- Use examples only when format or tone needs stronger steering; keep them
  relevant, diverse, and clearly tagged.
- Prefer configured effort and adaptive thinking controls over reasoning theater.
- State whether the target should assess, suggest, or use tools to implement.
- Make irreversible, shared, or destructive action boundaries explicit.

## Model-Specific Deltas

### Claude Opus 5.5

- Use this section and the official Opus 5.5 page for current assignments.
  Existing Opus 5 prompts may migrate without a wholesale rewrite, but that
  compatibility does not make the old model's guidance current.
- API default effort drops to `medium` (Opus 5: `high`). Always pin effort
  explicitly. Medium on 5.5 matches or beats Opus 5 high on coding; at any given
  level it thinks more per turn. Anthropic recommends: "Reserve `xhigh` and `max`
  for work where you've measured a quality gain." Lower effort rather than
  prompting it to think less. This is vendor guidance, not a hard limit;
  installation policy and explicit user choices govern the cost/latency tradeoff.
- Adaptive thinking is always on; it cannot be disabled or given a fixed budget.
  Forced `tool_choice` (`any` or a named `tool`) returns a 400 error. Use `auto`;
  strict tool schemas can enforce argument structure, not force a tool call.
  Harness concerns, not packet text.
- Unattended runs can end a turn with a text-only progress report. Treat that as
  a report, not completion: give an explicit done checklist, name the early-stop
  types to avoid, and cap automatic continuations at two or three.
- Code review recall and precision are both stronger; keep recall-oriented
  finding requests and adjudicate downstream.
- Drop legacy "think carefully" / "double-check" instructions. Mark pasted
  material with tagged boundaries (e.g. `<pasted_content id="...">`). Never ask
  it to reproduce hidden reasoning (`reasoning_extraction` refusals are broader).
- Multi-agent work benefits from stated time or turn budgets per child.

### Claude Sonnet 5.5

- Choose it for well-scoped work with a clear spec and a checkable result:
  bounded fixes, feature iteration, repeated investigation/drafting/review
  passes, documents. Route long-horizon work, judgment-heavy review and the
  hardest problems to Opus 5.5. Use this section and the official Sonnet 5.5
  page for current assignments, not the historical Sonnet 5 section.
- Effort is recalibrated; do not carry over Sonnet 5 levels. Agentic packets:
  `medium` for well-specified tasks, `high` for harder or longer ones. Anthropic
  recommends: "Reserve `xhigh` and `max` for work where you've measured a quality
  gain." This is vendor guidance, not a hard limit; installation policy and
  explicit user choices govern the cost/latency tradeoff. Lower effort rather
  than prompting it to think less.
- `thinking.type: disabled` is rejected. `between_tools`, accepted at `high`
  effort or below, turns off up-front thinking while retaining between-tool
  thinking. Forced `tool_choice` (`any` or a named `tool`) returns a 400 error.
  Use `auto`; strict tool schemas enforce argument structure, not invocation.
  Harness concerns, not packet text.
- At `low`/`medium` it may check in before finishing a multipart task. State the
  done criteria and that it should continue until they are met, stopping only
  when blocked or before a risky step. Keep approval boundaries explicit.
- At every effort it tends to add unrequested tests, docs or small files, and at
  `xhigh` it may start its own review rounds or reviewer children. Restate the
  scope: report optional additions or reviews at the end instead of doing them.
- At `low` it can report code done without a real check. Name the check that must
  run and require it to say which check could not run and why.
- For plan- or ideas-only requests, say so; open-ended asks can turn into builds.
- Do not discourage tool use. Ask it to verify facts that may have changed since
  training with tools rather than answering from memory.
- It resists injection and can distrust user text that arrives right after tool
   results. Deliver user steering as user content after tool-result blocks,
   separate from harness notices. If the harness cannot do this, use a fresh
   prompt rather than hiding user text inside a tool result.
- First Sonnet with Opus-level cyber safeguards; treat `stop_reason: refusal` as a
  stop condition, not something to rephrase around. Never request its reasoning
  in the response (`reasoning_extraction`).

### Claude Haiku 5.5

- Choose it for high-volume, latency-sensitive, checkable work: classification,
  extraction, triage, routing and narrow subagent tasks. Route ambiguous,
  long-horizon or judgment-heavy work to Sonnet 5.5 or Opus 5.5.
- First Haiku with effort; API default `medium`, which also suits agentic coding.
  Use `low` only for short chat or short tool tasks, `high` for longer agent
   tasks, knowledge work or strict instruction following. Compare Sonnet 5.5
   when choosing `xhigh`/`max`; higher effort can still be worthwhile. At `xhigh` a
   multi-turn answer can appear entirely in thinking, leaving an empty reply.
   Top-level effort changes invalidate the message cache; supported beta
   per-message effort changes with adaptive thinking can preserve it.
- Thinking can be disabled only at `low`/`medium`/`high`; `none` is not an API
   effort level. Provider variant names are adapter-specific. With
  thinking off plus JSON structured output it can skip a needed tool call; forced
  `tool_choice` is allowed but skips thinking. Harness concerns, not packet text.
- With long agent prompts at `low` it stops early and skips searches and checks.
  State the done criteria, that it should keep working until they are met, and
  not to add unrequested features, tests or docs.
- At `low`/`medium` it can report code done without a real check. Name the check
  that must run and require it to say which check could not run and why.
- Give the current date and ask it to search for facts that may have changed; do
  not issue a blanket "always search".
- User text injected inside tool results is treated as untrusted. Resend a
   mid-turn follow-up as user content, or a fresh prompt if the harness requires it.
- New safeguard refusals (cyber, frontier-LLM, bio, general harms) versus Haiku
  4.5, with no server-side fallback; treat `stop_reason: refusal` as a stop
  condition, since retries usually refuse again.
- Migration from Haiku 4.5: about 30% more tokens for the same text (new
  tokenizer); no `temperature`/`top_p`/`top_k` or assistant prefill; thinking
   blocks are account-bound and history must stay append-only under applicable
   binding checks. Recount prompts and leave thinking headroom in `max_tokens`.
   The original 2026-10-07 check recorded 1M context and 5x pricing above 100K
   input; recheck the current pricing page before budgeting. Subscription and
   per-token routes differ; provider names alone do not establish billing.

### Historical only: Claude Opus 5 (outdated)

- Visible verbosity is independent of effort; request concise responses and
  appropriately sized written deliverables explicitly.
- It narrates progress, broadens scope, verifies, self-corrects, and delegates
  more readily than prior Opus models. Constrain those behaviors directly.
- Remove inherited double-check, re-verification, and verifier-subagent prompts
  unless a concrete requirement needs them.
- For review recall, ask for all behaviorally relevant findings, including
  uncertain and lower-severity issues, then adjudicate separately.
- Keep thinking enabled where possible; thinking-disabled integrations can leak
  textual tool calls or internal XML artifacts.

### Historical only: Claude Sonnet 5 (outdated)

- It calibrates response length to task complexity; specify style only when the
  product requires a fixed output shape.
- It follows instructions more literally, particularly at low and medium effort.
  State broad applicability instead of expecting implicit generalization.
- Adaptive thinking is on by default. Raise effort for hard work rather than
  compensating with elaborate reasoning prompts.
- It reaches for tools, self-verifies, and provides progress more readily than
  Sonnet 4.6; remove legacy nudges before adding new ones.
- Review prompts that say "only high severity" or "be conservative" can suppress
  real findings. Use explicit recall-oriented reporting and downstream ranking.

### Claude Fable 5.1 / Mythos 5.1 (and legacy Fable 5 / Mythos 5)

- Fable 5 prompts carry over to 5.1. Re-run effort selection rather than carrying
  levels over (API default `high`); 5.1 `medium` roughly matches Fable 5 at lower
   cost. Select effort consciously for the task and access route.
- 5.1 writes fewer progress updates in long tool chains and can end with "Next,
  I'll …" or ask permission for covered steps. Request progress updates where
  they matter and state that reversible in-scope steps proceed without asking.
- 5.1 can add unrequested fixes, extensions or tests; restate the scope.
- Expect longer autonomous turns and long-horizon work. Harness timeouts,
  progress delivery, context continuity, and state tracking must support that.
- Ground every progress claim in tool evidence from the current run.
- Define when to act, when state-changing operations need approval, and when the
  model may pause. Avoid re-litigating decisions already made.
- Fable can coordinate persistent parallel children effectively. Use that only
  where project policy authorizes independent work and shared state is controlled.
- Long-running acceptance plans may benefit from periodic fresh-context
  verification, but this is a harness decision, not a default child instruction.
- Never request transcription or explanation of hidden reasoning; this can
  trigger the `reasoning_extraction` refusal category.

## Additional current guidance and harness boundaries

- Fable 5.1 client-side compaction should retain user constraints, decisions and
  reasons, exact hard-to-reconstruct facts, completed work and every open item.
  Low effort can answer volatile questions from memory; ask for current evidence.
  Prefer targeted file edits and allow output headroom for long deliverables.
- For Fable's serial agent loops, the vendor documents a turn-scoped reminder
  to batch independent tools. It is an integration option, not a rule to append
  to every child packet or a reason to parallelize dependent actions.
- Opus/Sonnet 5.5 and Fable 5.1 progress can arrive in thinking blocks whose text
  is omitted by default. Check client delivery before adding narration prompts.
  `display: "updates"` is a beta integration feature, not a packet instruction.
- Top-level effort changes and supported per-message effort changes have different
  caching behavior. Preserve the conversation prefix and replay thinking blocks
  unmodified. Editing earlier history can invalidate them. A UI effort selector
  does not prove that its adapter uses a cache-preserving API path.
- Sonnet 5.5 `between_tools` is accepted only at high or below; use adaptive
  thinking for reasoning without tools. For structured JSON reasoning, its
  guide describes a targeted think-before-answer nudge or higher effort with
  adaptive thinking. This is not general advice for every packet.
- Haiku 5.5 fixed-budget thinking is removed. Select response blocks by type,
  not position; handle an empty visible reply or `max_tokens` without claiming
  task completion. Model-switch compatibility for preserved thinking is
  asymmetric; consult the migration guide before replaying across models.
- For dense images, provide original resolution and crop/zoom tools where
  available. For frontend work, explicit product/design direction is more useful
  than generic aesthetic bans. Preserve the existing design system.

The Opus 5 and Sonnet 5 sections are historical migration references only.
For current work, use the self-contained 5.5 sections and matching official
pages; do not layer old thinking controls or effort semantics onto 5.5.
Legacy Fable 5 specifics were
last reviewed on 2026-10-07; the shared 5.1 section is current for 5.1 behavior.

## Maintenance

Re-fetch the canonical pages before changing a production harness, adopting a
new Claude model revision, or responding to a repeated evaluation failure. When
this index and an official page disagree, follow the official page and update
this file's verification date and affected summary.
