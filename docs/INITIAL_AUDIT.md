# NovaMC Minestom Initial Audit

Date: 2026-08-31
Source: `NovaMC-MINESTORM-26.2-SERVER.zip`

## Architecture found

```text
Java clients -> ViaProxy :25565 -> Minestom :25570
Bedrock clients -> Geyser :19132/udp -> ViaProxy -> Minestom
Webstore :3000 -> private network -> Minestom StoreApi :8082
Resource pack :9083 -> Minestom HTTP server :8083
```

There is **no Velocity implementation in the archive**. Do not silently migrate the project to Velocity.

## Version distinction

The project depends on `net.minestom:minestom:2026.07.22-26.2`. The native protocol exposed by this dependency is Minecraft 1.21.11 / protocol 769. `26.2` is the Minestom release target, not a Minecraft client version.

## Findings and current remediation

### High / Critical

1. **Unauthenticated store grant endpoint** — fixed with `STORE_API_TOKEN`, constant-time token comparison, strict request validation and bounded request bodies.
2. **Immediate store grants could remain persisted** — fixed by removing successfully applied orders while keeping failed deliveries pending.
3. **SkyBlock currency minting** — fixed by removing arbitrary `/island bank <amount>` deposits.
4. **Crate registry was global and not instance-aware** — fixed with instance-aware concurrent keys and cleanup.

### Medium

5. Resource-pack requests previously loaded the whole ZIP into memory — changed to streaming delivery.
6. Docker entrypoint could mask process failures — fixed with explicit exit propagation.
7. ViaProxy startup used a fixed sleep — replaced with Minestom port readiness checks and timeout handling.
8. Rank persistence had partial-write/concurrency risks — improved with serialized writes and atomic replacement.
9. Webstore catalog identifiers were trusted too broadly — server-side catalog validation added.

## Release blockers

- Gradle Wrapper is absent from the original archive.
- Source tests were effectively absent.
- Live Docker/client validation depends on an environment with Docker and Minecraft clients.
- Real Java client QA has not been proven.
- Real Bedrock QA has not been proven.
- Geyser/Floodgate end-to-end authentication is not proven; the archive contains standalone Geyser with offline authentication and no Floodgate integration.
- Webstore checkout is still demo-only; no real payment provider/webhook is implemented.
- Vendored ViaProxy JAR requires provenance/version/checksum validation.
- Survival terrain generation is custom and not a full vanilla-style overworld generator.
- Furniture/custom blocks are not yet a complete production-grade block-entity system.
- The 26 custom items require runtime verification individually on Java and Bedrock.

## Priority next steps

1. Add a Gradle Wrapper and reproducible clean-clone build.
2. Build unit/integration coverage around game state machines and persistence.
3. Centralize persistence behind structured services and atomic transactions.
4. Complete the custom-item interaction and serialization layer.
5. Validate or replace the furniture implementation.
6. Implement and validate real Geyser/Floodgate crossplay.
7. Add live Docker smoke tests and multi-client QA.
8. Replace demo checkout with verified payment webhooks before commercial use.
9. Perform gameplay balance and performance testing after runtime validation.
