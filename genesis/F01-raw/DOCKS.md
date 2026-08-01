# F01 — Tosh Ecosystem Foundation (Raw)

F01 defines the shared identity, vocabulary, registry, design-system adoption, and onboarding rules that let independently developed Tosh apps behave as one ecosystem without becoming one implementation.

## What We Build

- Stable product and host ID conventions.
- Root app registry with product role, repository path, status, owner, and marketplace readiness.
- Shared Tosh terminology for products, hosts, components, widgets, releases, publishers, permissions, and capabilities.
- App onboarding document that every new Tosh project reads before implementation.
- Shared privacy, security, accessibility, release, and support principles.
- A clear boundary between root ecosystem decisions and app-owned implementation.
- Revision and compatibility rules for shared contracts and `STYLES.md`.

## Architecture

```text
Root ecosystem docs
├── identity and vocabulary
├── STYLES.md
├── app registry
├── shared contracts
└── onboarding guidance
    └── independent Tosh app project
        ├── app-specific AGENTS.md
        ├── app-specific CYCLES.md
        ├── app-specific DOCKS.md
        └── app implementation and tests
```

The root may define a contract; it must not reach into an app's private views, data, credentials, or build system. An app adopts a root contract by recording the revision it implements.

## States

| State | Meaning | Behavior |
|---|---|---|
| Proposed | A shared rule is being discussed | It lives in `genesis/` and cannot block app implementation unless the app explicitly opts in |
| Adopted | The rule is approved and documented | New apps follow it; existing apps migrate through their own cycles |
| Deprecated | A newer rule replaces it | Existing apps remain supported for the declared compatibility period |
| Retired | The rule is no longer supported | No new app may depend on it; migration evidence remains in history |

## Dependencies

- Existing app folders and their original ideas.
- Root `STYLES.md`.
- Root `genesis/APP REGISTRY.md` and `ECOSYSTEM MAP.md`.

## Reference

- Existing app repositories are evidence of current product direction, not direct implementation references.
- `NotchinTosh/` provides the first verified SDK and bridge-runtime example.

## Files

- `AGENTS.md` — root management rules.
- `STYLES.md` — shared visual and interaction conventions.
- `genesis/APP REGISTRY.md` — product and host registry.
- `genesis/ECOSYSTEM MAP.md` — ownership and dependency boundaries.
- App repositories — implementation-specific contracts and evidence.

## Verification

| Scenario | Expected result | Evidence |
|---|---|---|
| New app onboarding | An agent can identify the app's role, host status, shared style revision, and next documentation step | Pending root documentation review |
| Product identity | Every registered app has a stable product ID and clear owner | Pending registry review |
| Boundary check | Root docs do not require app implementation code to be moved into the umbrella repository | Pending architecture review |
| Style adoption | An app can add a documented extension without silently changing shared tokens | Pending style review |