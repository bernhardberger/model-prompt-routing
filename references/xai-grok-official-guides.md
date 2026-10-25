# Grok 4.7: official guidance

Reviewed 2026-10-25. This is a synthesis of official API and model documentation,
not a locally benchmarked prompting recipe. Current reference: Grok 4.7. Do not
silently change an existing session's selected model.

## Sources and version boundary

- [Current overview](https://docs.x.ai/developers/grok-4-7)
- [Reasoning](https://docs.x.ai/developers/model-capabilities/text/reasoning)
- [Function calling](https://docs.x.ai/developers/tools/function-calling)
- [Cache routing](https://docs.x.ai/developers/advanced-api-usage/prompt-caching/maximizing-cache-hits)
- [Context compaction](https://docs.x.ai/developers/advanced-api-usage/context-compaction)
- [Historical 4.6 announcement](https://x.ai/news/grok-4-6)

The former `/developers/grok-4-6` overview served 4.7 content when checked.
Do not treat that redirect as evidence that a 4.6 endpoint has 4.7 behavior.

## Task packets

Use the shared task contract: a concrete outcome, evidence and context, action
boundaries, output requirements and completion checks. The official positioning
emphasizes coding, knowledge work and long-running agents. That positioning alone
does not justify extra autonomy, child agents or repeated verification.

No dedicated 4.7 behavioral-mitigation guide comparable to the Claude guides was
established in this review. Do not invent Grok-specific prompt tricks or copy its
consumer application's system prompt into an OpenCode child packet.

## Effort and integration

- The overview documents `low`, `medium`, `high` (default), and `xhigh`. Use
  supported controls rather than an invented `max` variant. Select effort for
  the task and budget; labels are not equivalent across vendors.
- The model accepts text and images and returns text. Image/video generation
  uses separate Imagine models: see [media guidance](media-generation-guides.md).
- The overview documents a 500,000-token context window. Check the actual
  adapter/access route before budgeting a session against that number.
- Official guidance strongly recommends a stable `prompt_cache_key` on Responses
  requests for conversation routing. Cache behavior is a harness concern, not
  something a task packet can enable.
- Responses returns encrypted reasoning items; replay them unchanged when
  maintaining conversation history. Do not expose or rewrite them as prompt text.
- For long loops, preserve task state and outstanding work through supported
  compaction. Provider-side features require adapter support.
- The 4.7 overview describes Fast as separate serving infrastructure, available
  through Cursor/Grok Build rather than the public API. Do not fabricate a public
  API model ID from a product label.

Verify exact model availability, effort mapping and subscription entitlement in
the installed provider. These pages do not establish OpenCode adapter support.
