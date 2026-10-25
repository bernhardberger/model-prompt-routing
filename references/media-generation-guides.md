# Image and video generation guidance

Reviewed 2026-10-25. Separate creative instructions from model selection,
authentication, billing and available tool capabilities. This reference does not
install media tools or authorize uploads, public URLs or paid generation.

## Sources

- [Codex image generation](https://developers.openai.com/codex/image-generation.md)
- [OpenAI image prompting](https://developers.openai.com/api/docs/guides/image-prompting)
- [Grok Imagine](https://docs.x.ai/developers/model-capabilities/imagine)
- [Grok image generation](https://docs.x.ai/developers/model-capabilities/images/generation)
- [Grok reference-to-video](https://docs.x.ai/developers/model-capabilities/video/reference-to-video)
- [Hermes SuperGrok OAuth integration](https://hermes-agent.nousresearch.com/docs/guides/xai-grok-oauth)
  — third-party implementation documentation, not an xAI entitlement guarantee.

## Codex images

The Codex page documents `$imagegen`, reference-image inputs and built-in
`gpt-image-2` consuming general Codex usage limits. It states that image turns
consume included usage roughly 3–5 times faster on average than comparable turns
without generation, depending on size/quality. API-key generation has separate
API billing. Neither establishes that an OpenCode Codex adapter exposes the tool.

The API prompting guide now features GPT Image 2.5 examples as well as a GPT
Image 2 reference. Use shared prompting techniques, but do not confuse API model
availability with the model actually used by Codex's built-in tool.

For a useful image brief:

1. State purpose, subject, action, setting, composition and visual style.
2. Add aspect ratio, dimensions, material, color and lighting when relevant.
3. Identify each reference image's role: subject, layout, identity or style.
4. Quote exact in-image text and specify its placement; inspect every word.
5. For edits, state the requested change and invariants explicitly. Revise one
   thing at a time and inspect the output for unintended drift.

Example: “Edit the supplied product photo: replace only the background with a
soft grey studio backdrop. Preserve the product geometry, printed text, colors,
camera angle and crop. Add no other objects or text.”

## Grok images and video

Use Imagine models, not a text-only-output Grok reasoning model. The reviewed
docs describe `grok-imagine-image-2.0` and `grok-imagine-video-1.5`; select from
the tool's actual catalog rather than assuming aliases or preview names persist.

For images, use a concrete brief and edit invariants as above. These are portable
briefing practices, not a claim of model-specific measured improvements on Grok.

For video, specify the scene, subject action, camera motion, timing and desired
audio. Match duration, aspect ratio and resolution to supported tool parameters.
Distinguish three different requests:

- **Image-to-video:** animate an existing starting image.
- **Reference-to-video:** use identities/objects/styles from references without
  necessarily locking the first frame. Identify reference roles explicitly.
- **First/last-frame control:** constrain endpoints where the model/tool supports
  them. Do not assume reference images alone pin either frame.

The official reference-to-video examples use indexed image/audio references and
preset voices. Let the adapter translate the brief into its schema; do not guess
whether a raw REST API and an SDK use the same parameter names or indexing.

Example brief: “Use reference 1 for the person and reference 2 for the product.
One continuous eight-second shot: the person lifts the product, turns it toward
the camera, then holds it still. Slow camera push-in; preserve both identities.
No cuts or added text.” Supply the actual references through the supported tool.

Inspect generated frames, motion, continuity, text and audio against the brief.
Download outputs that must be kept to project-owned storage; ephemeral URLs are
not durable deliverables. Do not enable permanent public URLs merely to save a
result when private file output is available.

## Subscription-backed access

Hermes documents xAI OAuth using SuperGrok/X Premium+ and reuse of the bearer
token for image/video calls. It also reports entitlement-related 403 responses
for some subscriptions. This supports the existence of a subscription-backed
route, not universal entitlement or proof that another harness implements it.

Verify the selected adapter and account's supported media surface before use.
Successful login alone is not proof of generation permission. Never silently
fall back to a billable API key when a subscription route is unavailable, and
never put tokens or account details in task packets or shared documentation.
