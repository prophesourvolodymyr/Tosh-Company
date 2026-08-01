# Tosh Company Ecosystem — Initial Idea

## Purpose

Tosh Company is an umbrella ecosystem for focused macOS products. The root repository does not replace the individual app repositories. It provides the shared context that lets every app understand where it belongs, what it may reuse, how it should look, and how it can participate in the Tosh Marketplace.

The ecosystem has four layers:

1. **Identity** — Tosh naming, product roles, visual language, writing voice, accessibility standards, and trust expectations.
2. **Shared contracts** — marketplace package formats, host capability declarations, account boundaries, deep links, telemetry rules, and interoperability rules.
3. **Products** — independently buildable apps such as NotchinTosh, LaunchinTosh, LockinTosh, SwitchinTosh, and CleaninTosh.
4. **Marketplace** — the future web platform and embedded host clients that publish and distribute compatible products, widgets, and extensions.

## Product Families

| Product | Role | Current repository state | Ecosystem relationship |
|---|---|---|---|
| NotchinTosh | Notch shell, widgets, bridge runtime, and widget SDK | Existing Git repository | First host for the Tosh widget and marketplace contract |
| LaunchinTosh | macOS launcher and app replacement with custom widgets | Existing project repository | Host for launcher widgets and future marketplace components |
| LockinTosh | macOS lock-screen widget experience | Existing project folder | Host for lock-screen widgets and lock-screen-specific capabilities |
| SwitchinTosh | macOS app switcher | Existing project folder and mockups | Host for switcher actions, themes, and future extensions |
| CleaninTosh | macOS cleaning and maintenance utility | Existing project folder | Host for maintenance workflows and future extensions |

The registry is descriptive, not a promise that every product already shares runtime code. Each app keeps its own build, tests, release process, and detailed feature tree.

## Shared Marketplace Direction

The Tosh Marketplace is a public web platform with embedded clients inside Tosh apps. A publisher creates one product listing and may provide host-specific signed components. A host only installs the component compatible with its own app, SDK, platform, permissions, and runtime contract.

The marketplace must separate:

- Public catalog metadata from private publisher/account data.
- Package validation from host execution.
- Publisher identity from runtime user data.
- Product identity from host-specific component identity.
- Local Developer Mode from public marketplace publication.
- Trust/review decisions from user permission consent.

The first version distributes free widgets and extensions. Commerce, payouts, subscriptions, and creator revenue are later decisions, not assumptions for the initial architecture.

## Root Project Responsibilities

The root project owns:

- Ecosystem identity and app registry.
- Shared style system and writing conventions.
- Marketplace product, package, host, and publisher concepts.
- Cross-app dependency and compatibility decisions.
- Shared security, privacy, accessibility, and release principles.
- Proposals for future ecosystem features.

The root project does not own:

- Individual app implementation files.
- App-specific UI details that do not affect the shared system.
- Private credentials or deployment secrets.
- A forced monorepo build command for all apps.
- Marketplace production infrastructure before it is explicitly designed and approved.

## Working Principle

Every new Tosh app should be able to answer five questions before implementation begins:

1. Which user problem does this app own?
2. Which shared Tosh contracts does it consume or publish?
3. Which parts of `STYLES.md` are global and which are app-specific?
4. Which marketplace host component, if any, will this app expose?
5. What must remain isolated so a broken app, bridge, or extension cannot damage another product?