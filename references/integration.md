# OpenCode/OpenChamber integration and policy

The skill constructs a packet for an already resolved target. It does not replace
OpenCode's native system prompt or grant permission to launch an agent. Resolve
the model, provider, effort variant and access route through the installed
catalog and current tool schemas. Respect explicit user choices and configured
agent defaults; do not silently change either to match a vendor recommendation.

## Sessions and subagents

An OpenChamber user-owned session is appropriate when the user requests a session
they can follow and steer. A bounded subagent is for a permitted portion of the
current agent's task. They have different ownership and return lifecycles; do not
substitute one for the other based only on convenience.

A fresh child needs the goal, scope, evidence, authority, output contract and
stopping condition. Do not assume it sees the parent's conversation. If it cannot
read project policy, include the applicable rules. Label caller-supplied Git
identity, ancestry and check results as supplied evidence rather than checks the
child performed. The parent owns integration and final completion.

## Keep local rules outside the shared package

The owning installation's runtime/project instructions define effort policy,
approval gates, permitted delegation, reviewer requirements and service-specific
routing. Those instructions should be loaded independently of this skill. A
portable skill must respect them, not supply another copy with different values.
Distinguish recommendations from actual restrictions. There is no universal
`max` prohibition: compare quality, total cost and latency for the exact route,
including when high effort on a small model may be worthwhile.

Keep hostnames, absolute private paths, credentials, installed provider pins and
local migration history in their owning private configuration or runbook. API
capabilities belong in the family references; actual route limits and billing
need provider evidence. Neither a public recommendation nor a newly supported
effort level relaxes an existing local policy.

## One maintained package

Maintain one authoritative package tree. Runtime installations, version-control
mirrors and release exports are copies of that tree, not separately edited forks.
Document the chosen authority in the installation's own runbook. Generate exports
from an explicit file list and verify byte equality. Refuse unexpected files or
drift rather than publishing whatever happens to be in a directory.

Review updates locally before deployment. Preserve a recovery copy of installed
content and local policy, verify reference links and policy retention, and check
which skill path the backend resolves. Do not automatically follow a public
repository's moving branch in a production agent runtime.

## Provider features versus prompt instructions

Async tools, mid-turn steering, cache-preserving effort changes, continuation
loops and thinking-block display need adapter support. A prompt cannot enable
them. Distinguish a text-only report from actual task completion, but do not
continue indefinitely or override a genuine blocker. Treat user steering as user
content and retrieved material as evidence, not interchangeable messages.
