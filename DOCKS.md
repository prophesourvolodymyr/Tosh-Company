# Tosh Company — Ecosystem Foundation

The root Tosh Company project coordinates independent apps, a shared SDK, and a future marketplace. This DOCKS document describes the root-level system, not the private implementation of any app.

## What We Build

- A canonical ecosystem orientation layer.
- A registry of Tosh products, shared repositories, host IDs, and project status.
- Shared terminology, design, accessibility, privacy, and security rules.
- A versioned SDK ownership and contribution model.
- A versioned marketplace ownership and contribution model.
- Clear boundaries between shared contracts and host-owned implementations.
- App onboarding guidance that tells a new agent where the project belongs.
- Documentation links and verification evidence for every Tosh project.

## Architecture

```text
Tosh Company root
├── ECOSYSTEM.md             ecosystem identity and dependency map
├── DOCKS.md                 root architecture and ownership
├── STYLES.md                shared design and interaction rules
├── CYCLES.md                root documentation and contract work
├── ToshSDK/                 reusable Swift package contracts
├── ToshMarketplace/         future web/API marketplace platform
└── host projects
    ├── NotchinTosh
    ├── LockinTosh
    ├── LaunchinTosh
    ├── SwitchinTosh
    └── CleaninTosh
```

```text
Shared contract change
        │
        ├── app-specific first implementation
        ├── reusable SDK proposal ──> ToshSDK review/version
        └── marketplace proposal ──> ToshMarketplace review/version

Host app
  ├── consumes shared contracts
  ├── owns native surface and runtime
  ├── declares capabilities and permissions
  └── may publish a compatible host component
```

The root project must not become a shared dumping ground. A file belongs at the root only when multiple Tosh projects need the decision or orientation.

## Project States

| State | Meaning | Required documentation |
|---|---|---|
| Incubating | Product or shared platform is being shaped | `ECOSYSTEM.md`, `DOCKS.md`, `ORIGINAL IDEA.md`, raw feature docs where needed |
| Contracting | Public interfaces and ownership are being defined | `ECOSYSTEM.md`, `DOCKS.md`, API/schema docs, compatibility notes |
| Building | Implementation is active in the owning repository | `CYCLES.md`, feature DOCKS, tests, implementation evidence |
| Verified | Required behavior has evidence on the target platform | Verification evidence in the owning project and root registry status |
| Retired | No new work; retained for historical context | Archive note and dependency migration record |

## Open SDK and Marketplace Extensions

Every project may contribute to both shared platforms:

- A host may request a host-specific SDK module.
- A widget project may request new declarative primitives, permissions, or events.
- A product may publish a host component to the marketplace.
- A marketplace client may request a catalog or installation API.
- A project may keep a feature private until it is proven reusable.

The contribution is not complete until the owning project documents the need, implementation, compatibility, security implications, and tests. The shared repository must not reject a feature merely because it originated in one app; it should accept it when the contract is clear and the ownership boundary is safe.

## Root States and Failure Behavior

| Situation | Root behavior |
|---|---|
| New project appears | Add it to the registry and require `ECOSYSTEM.md` and `DOCKS.md` before shared integration |
| Project has a private feature | Keep it app-owned; do not force it into the SDK or marketplace |
| Project needs shared capability | Add a versioned proposal to `ToshSDK` or `ToshMarketplace` |
| Shared contract changes | Record compatibility, migration, and affected consumers before promotion |
| App is incompatible | Keep its project usable; do not show its marketplace component as installable |
| SDK or marketplace failure | Host apps retain their core behavior and do not depend on arbitrary remote execution |
| Documentation disagrees | Root `ECOSYSTEM.md` defines cross-project ownership; app docs define app-private behavior |

## Files and Ownership

- `ECOSYSTEM.md` — where Tosh Company and this root project fit.
- `DOCKS.md` — root architecture and behavior.
- `STYLES.md` — shared visual and interaction system.
- `CYCLES.md` — root tasks and promotion order.
- `genesis/` — origin ideas, raw features, research, and references.
- `features/` — approved root ecosystem features only.
- `ToshSDK/ECOSYSTEM.md` and `ToshSDK/DOCKS.md` — shared SDK project contract.
- `ToshMarketplace/ECOSYSTEM.md` and `ToshMarketplace/DOCKS.md` — marketplace project contract.
- Each host's `ECOSYSTEM.md` and `DOCKS.md` — local role and host boundary.

## Dependencies

- Root `STYLES.md`.
- Root `ECOSYSTEM.md`.
- `ToshSDK` for reusable contracts.
- `ToshMarketplace` for discovery and publishing contracts.
- Each host project for native runtime and installation evidence.

## Verification

| Scenario | Expected result | Evidence |
|---|---|---|
| New project orientation | An agent can identify ownership, dependencies, current state, and next documents | Pending root setup verification |
| SDK contribution | An app can propose and test a shared or host-specific SDK addition without editing another app's private source | Pending SDK repository implementation |
| Marketplace contribution | An app can publish a host-specific component or propose a marketplace API without bypassing compatibility and privacy rules | Pending marketplace implementation |
| Contract change | A versioned change lists affected consumers and migration behavior | Pending contract process verification |
| Documentation coverage | Every Tosh project has `ECOSYSTEM.md` and `DOCKS.md` | Pending repository scan |