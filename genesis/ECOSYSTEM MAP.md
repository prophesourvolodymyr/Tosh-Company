# Tosh Company Ecosystem Map

## Boundary Model

```text
Tosh Company root
├── Shared identity and design system
├── Shared marketplace and package contracts
├── Product registry and dependency map
└── Independent host applications
    ├── NotchinTosh
    ├── LaunchinTosh
    ├── LockinTosh
    ├── SwitchinTosh
    └── CleaninTosh
```

The root is an umbrella coordination repository. It documents shared decisions and points agents to the correct app repository. It is not a replacement for each app's `AGENTS.md`, `CYCLES.md`, source tree, or test suite.

## Dependency Direction

```text
STYLES.md ───────────────┐
                         ├──> each Tosh app
Marketplace contracts ───┤
                         ├──> web marketplace
Ecosystem identity ──────┘

Host app ──declares──> marketplace host contract
Marketplace ──publishes──> signed host component
Host runtime ──verifies──> component before installation
Installed component ──runs inside──> host boundary
```

Dependencies must point from an app to shared contracts, never from shared documentation into private app implementation details. The marketplace never becomes an arbitrary code loader for another host.

## What Is Shared

- Product naming and Tosh identity.
- Global color, typography, spacing, motion, accessibility, and writing rules.
- Marketplace IDs, host IDs, package formats, compatibility ranges, and signing concepts.
- Publisher/account privacy boundaries.
- Deep-link naming conventions.
- Minimum release evidence and security expectations.
- Cross-app terminology for widgets, extensions, host components, products, releases, and permissions.

## What Stays App-Owned

- App source code and internal architecture.
- App-specific feature docs and implementation cycles.
- App-specific settings, navigation, and interaction details.
- App-specific capabilities that are not exposed through a shared contract.
- App release cadence and CI configuration.
- App-specific mockups and visual experiments.

## Product Communication Contract

Every app repository should contain or link to:

- Its product identity and user problem.
- Its host ID and supported marketplace package format, if applicable.
- The shared `STYLES.md` revision it follows.
- The capabilities it exposes to marketplace components.
- The permissions and privacy behavior for those capabilities.
- Its deep-link and installation behavior.
- Its verification evidence.

## Current Relationship to Existing Folders

| Folder | Use now | Do not do |
|---|---|---|
| `NotchinTosh/` | Develop and verify the notch shell, widget SDK, bridge runtime, and its marketplace slices | Do not move its implementation into the root umbrella repository |
| `LaunchinTosh/` | Develop the launcher product independently | Do not assume its widget contract is identical to NotchinTosh until documented |
| `LockinTosh/` | Incubate the lock-screen product | Do not publish lock-screen components as compatible with another host by default |
| `SwitchinTosh/` | Incubate the switcher and retain mockups as product evidence | Do not treat mockup behavior as an approved shared contract |
| `CleaninTosh/` | Reserve the product identity and future maintenance-app work | Do not add it to marketplace installation until its host boundary exists |

## App Onboarding Sequence

When creating a new Tosh app:

1. Register it in the root app registry.
2. Assign a stable product ID and provisional host ID.
3. Read and adopt the global style system.
4. Create the app's own project repository and F-Cycle docs.
5. Define its host capabilities, package format, and privacy boundary.
6. Document what it consumes from the marketplace and what it may publish.
7. Build and verify app behavior independently.
8. Promote a marketplace component only after host installation and rollback behavior are verified.