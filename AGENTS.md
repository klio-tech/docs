# Klio documentation — instructions for agents

Source for [docs.klio.tech](https://docs.klio.tech). Mintlify site; pages are
MDX with YAML frontmatter, navigation and theme live in `docs.json`, and pushing
to `main` deploys.

For Mintlify product knowledge (components, configuration, writing standards),
install the skill: `npx skills add https://mintlify.com/docs`

## What Klio is

A shared workplace for AI agents. Claude Code, Cursor, Codex and any MCP client
connect to one project-scoped memory: an agent that finishes sets down what it
decided, and the next one picks it up and keeps going.

The product is **collaboration**, not recall. Memory is the mechanism. Copy that
leads with "memory" puts Klio on a crowded shelf next to mem0, Zep and
Supermemory and argues on recall quality — which is not the axis it wins on.

## Accuracy rules

These pages are read by agents as well as people. An agent acting on a wrong
page produces confidently wrong work, so accuracy outranks polish here.

1. **Tool contracts mirror the engine.** Everything under `tools/` — parameter
   names, defaults, enum values, limits — reflects the MCP server's real
   registrations. Verify against the source before editing. Never write a
   signature from memory.
2. **Qualify self-hosted-only claims.** User-held encryption keys and the
   SHA-256 hash chain belong to the *self-hosted* engine. Klio Cloud encrypts in
   transit and at rest at the infrastructure level, redacts secrets and PII
   before storage, and isolates per org — but the keys are ours and Cloud writes
   are not hash-chained. Never state the stronger claim unqualified.
3. **Be exact about propagation.** A write is available to the next agent that
   *reads*, immediately. There is no push to agents already mid-session. Do not
   phrase this as "real-time sync" in a way that implies notification.
4. **Scope is the security story, and it has one boundary.** The **org** is the
   boundary nothing crosses. Spaces subdivide for relevance; they are not
   isolation. `X-Vex-Project` resolution **fails open** — never present it as a
   security control.
5. **Never invent an endpoint, flag, or limit.** If it is not in the engine, the
   CLI, or the canonical pricing data, it does not go in the docs.

## Terminology

| Use | Not |
| --- | --- |
| workplace, shared memory | "brain", "second brain" |
| space | project store, bucket |
| org | tenant, workspace, account |
| agent identity | user, client |
| supersede / retire | delete, overwrite |

Wire-protocol identifiers keep their existing names — `X-Vex-Key`,
`X-Vex-Agent`, `X-Vex-Project`, `X-AgentGuard-Key`. These are live headers, not
copy; renaming them in docs would break readers' integrations.

## Style

- Active voice, second person.
- One idea per sentence. Short sentences carry technical claims better.
- Anti-hype: no "revolutionary", "seamless", "effortless", "supercharge".
- State limitations plainly, in the same voice as the features. `<Warning>` for
  things that will bite; `<Note>` for things worth knowing.
- Every code sample should be runnable or clearly marked as pseudocode.

## Before opening a PR

```bash
npx mintlify broken-links
```
