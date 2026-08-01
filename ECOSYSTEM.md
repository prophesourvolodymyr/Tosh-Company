# ECOSYSTEM.md — Tosh Company

## Identity

Tosh Company is an ecosystem of independent macOS products, shared SDKs, and marketplace services. The root repository is the orientation and coordination layer. It does not replace the source repository, tests, or release process of any product.

## Projects

| Project | Role | Repository path | Current relationship |
|---|---|---|---|
| ToshSDK | Shared Swift contracts and host SDKs | `ToshSDK/` | New shared platform repository |
| ToshMarketplace | Future web marketplace and publishing service | `ToshMarketplace/` | New platform repository; implementation follows documented contracts |
| NotchinTosh | Notch host, widget SDK reference, bridge runtime | `NotchinTosh/` | First host and current SDK/marketplace implementation reference |
| LockinTosh | Lock-screen widget host | `LockinTosh/` | Incubating host; needs shared lock-screen contracts |
| LaunchinTosh | Launcher and app replacement | `LaunchinTosh/` | Independent host/product project |
| SwitchinTosh | macOS app switcher | `SwitchinTosh/` | Independent product project with mockups |
| CleaninTosh | Cleaning and maintenance utility | `CleaninTosh/` | Product incubation |

## Dependency Direction

```text
Tosh Company root documentation
        │
        ├── ToshSDK ───────────────> host applications
        │                              ├── NotchinTosh
        │                              ├── LockinTosh
        │                              ├── LaunchinTosh
        │                              ├── SwitchinTosh
        │                              └── CleaninTosh
        │
        └── ToshMarketplace ───────> marketplace clients and host installation flows
```

The SDK defines reusable contracts. The marketplace defines discovery, publishing, and distribution. Each host owns its own windows, layout, capabilities, permissions, runtime, and app-specific UI.

## Shared Contracts

- Root `STYLES.md` defines shared visual, motion, accessibility, and writing conventions.
- `ToshSDK/` defines shared package, widget, compatibility, permission, and host-extension contracts.
- `ToshMarketplace/` defines public catalog, publisher, submission, review, artifact, and release contracts.
- Each app's `ECOSYSTEM.md` declares the SDK and marketplace revisions it consumes.

## Open Contribution Rule

Every Tosh project is allowed to add something to the shared SDK or marketplace when the product needs it. The path is open:

- App-specific behavior may be implemented in the app first.
- If it should be reusable, the app may propose a new `ToshSDK` module or marketplace contract.
- Host-specific modules such as `ToshLockScreenSDK` and `ToshNotchSDK` are valid; “shared” does not mean “generic UI only.”
- Marketplace products may include app-specific host components as long as they declare compatibility and permissions honestly.
- The proposing app owns the first implementation and tests; the shared repository owns the accepted reusable contract after review.
- No app should silently fork or change a shared contract. Add a versioned change, compatibility evidence, and migration note.

This openness is intentional. The ecosystem should grow from real app needs rather than guessing every API in advance.

## Ownership Rules

### Root owns

- Ecosystem identity and product registry.
- Cross-project dependency direction.
- Shared style and terminology decisions.
- Feature promotion and documentation integrity.

### ToshSDK owns

- Language-level and package-level contracts.
- Shared widget/bridge declarations.
- Host-specific SDK modules that are intentionally reusable.
- SDK versioning and compatibility policy.

### ToshMarketplace owns

- Web catalog and publishing service.
- Publisher accounts and review boundaries.
- Product/release metadata and immutable artifact distribution.
- Marketplace API and client contracts.

### Host apps own

- Native windows and surfaces.
- Host layout and placement.
- Runtime process lifecycle and resource limits.
- Capability enforcement and user permission prompts.
- App-specific features, tests, and release evidence.

## Current State

The root ecosystem is in documentation and repository setup. `NotchinTosh` contains the first working SDK and marketplace reference implementation. `ToshSDK` and `ToshMarketplace` now exist as independent initialized repositories, but their production implementation has not been transferred yet. Existing app repositories remain independent.

## Reading Order

1. This file.
2. `DOCKS.md` for root ecosystem architecture.
3. `STYLES.md` for shared design rules.
4. `CYCLES.md` for planned work.
5. The target project's `ECOSYSTEM.md` and `DOCKS.md`.
6. The target project's `AGENTS.md` and feature documentation.