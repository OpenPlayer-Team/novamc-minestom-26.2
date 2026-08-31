# NovaMC Repair & Production Roadmap

## Phase 0 — Baseline
- [x] Archive inspection
- [x] Architecture inventory
- [x] Security findings recorded
- [x] Initial hardening changes identified
- [ ] Reproducible Gradle wrapper

## Phase 1 — Build & Core Stability
- [ ] Clean-clone build
- [ ] Full compile/test/shadowJar
- [ ] Startup smoke test
- [ ] Shutdown/restart verification
- [ ] Structured error handling

## Phase 2 — Persistence & Economy
- [ ] Central persistence abstraction
- [ ] Atomic transactions
- [ ] Player data consistency across modes
- [ ] Economy exploit audit
- [ ] Recovery/rollback tests

## Phase 3 — Gameplay
- [ ] Survival regression suite
- [ ] SkyBlock state-machine tests
- [ ] BedWars lifecycle tests
- [ ] Custom item runtime tests
- [ ] Furniture persistence and interaction tests

## Phase 4 — Crossplay & Networking
- [ ] ViaProxy validation
- [ ] Geyser validation
- [ ] Floodgate integration/decision
- [ ] Java client QA
- [ ] Bedrock client QA
- [ ] reconnect/fallback testing

## Phase 5 — Resource Pack & UX
- [ ] Complete asset validation
- [ ] Java resource-pack runtime test
- [ ] Bedrock-compatible presentation
- [ ] UI consistency audit
- [ ] icon/MOTD/tab/scoreboard polish

## Phase 6 — Deployment & Performance
- [ ] Docker build
- [ ] Docker smoke test
- [ ] health checks
- [ ] memory/CPU/MSPT profiling
- [ ] load/soak tests
- [ ] backup/restore drill

## Release gate

No component is marked production-ready without evidence. Use only `PASS`, `FAIL`, `BLOCKED`, or `NOT APPLICABLE` for QA status. Runtime limitations must remain visible rather than being hidden behind configuration changes or disabled tests.
