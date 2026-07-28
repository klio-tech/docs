# Klio docs

Source for [docs.klio.tech](https://docs.klio.tech), built on
[Mintlify](https://mintlify.com). Pushing to `main` deploys.

## Structure

```
index.mdx            What is Klio — the positioning
quickstart.mdx       Connect an agent, prove a handover
concepts/            Handover loop, scope, what Klio keeps
connect/             Claude Code, Cursor, any MCP client
tools/               Reference for all eight MCP tools
self-host/           Running the open-source engine
docs.json            Navigation, theme, and site config
```

## Local preview

```bash
npx mintlify dev
```

Check links before opening a PR:

```bash
npx mintlify broken-links
```

## Writing rules

These docs are read by agents as well as people, so being wrong is expensive —
an agent that acts on an inaccurate page produces confidently wrong work.

1. **Verify tool contracts against the engine.** Parameter names, defaults and
   enum values under `tools/` mirror the MCP server's actual registrations.
   Check the source before changing them; never write them from memory.
2. **Qualify self-hosted-only claims.** User-held encryption keys and the
   SHA-256 hash chain are properties of the *self-hosted* engine. Klio Cloud
   encrypts in transit and at rest at the infrastructure level, redacts secrets
   and PII before storage, and isolates per org — but the keys are ours and
   Cloud writes are not hash-chained. Never state the stronger claim unqualified.
3. **Be exact about propagation.** A write is available to the next agent that
   *reads*, immediately. Klio does not push to agents already mid-session. Do
   not phrase this as "real-time sync" in a way that implies notification.
4. **Never invent an endpoint, flag, or limit.** If it is not in the engine, the
   CLI, or the canonical pricing data, it does not go in the docs.

## Related

- Engine and CLI — [klio-tech/klio](https://github.com/klio-tech/klio)
- Cloud dashboard — [app.klio.tech](https://app.klio.tech)
