# NovaMC — Minestom 26.2

NovaMC is a custom Minecraft network built on Minestom, currently targeting the Minestom 26.2 release line (native protocol currently exposed by the project: Minecraft 1.21.11 / protocol 769).

## Status

This repository is an active repair and modernization effort based on the uploaded NovaMC server archive. It is **not declared production-ready yet**. Runtime Java/Bedrock, Docker, Geyser/Floodgate, gameplay, load and recovery validation remain release gates.

## Architecture currently found

```text
Java clients   -> ViaProxy :25565 -> Minestom :25570
Bedrock        -> Geyser :19132/udp -> ViaProxy -> Minestom
Webstore       -> private network -> Minestom Store API :8082
Resource pack  -> Minestom HTTP service :8083
```

There is currently no Velocity implementation in the source archive. Do not introduce a proxy migration without a documented architecture decision.

## Development principles

- Inspect before changing.
- Preserve existing gameplay and data.
- Fix root causes rather than hiding symptoms.
- Never fake tests or production readiness.
- Back up before destructive operations.
- Prefer thread-safe, non-blocking server code.
- Keep secrets out of Git.
- Every release claim must have evidence.

## Build

Use the project's configured Java toolchain and Gradle installation. The original archive did not include the Gradle Wrapper; adding a reproducible wrapper is a release task.

```bash
gradle clean test shadowJar
```

## QA status

See `docs/INITIAL_AUDIT.md` and `docs/ROADMAP.md` for the current evidence, blockers and development plan.
