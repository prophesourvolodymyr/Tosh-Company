# Tosh Marketplace — Ecosystem Direction

## Purpose

Tosh Marketplace is the shared discovery, publishing, and distribution platform for Tosh products. It will eventually have a public web marketplace and embedded marketplace clients inside Tosh host applications. The root repository documents the ecosystem-level contract; the implementation remains in the marketplace or host project that owns each slice.

## Product Model

```text
Publisher account
└── Product listing
    ├── Product metadata
    ├── Host component for NotchinTosh
    │   ├── Signed package artifact
    │   ├── Compatible widgets/extensions
    │   └── Capability declarations
    ├── Host component for LaunchinTosh
    └── Other host-specific components
```

- A **product** is what users discover and evaluate.
- A **host component** is what one Tosh app installs.
- A **widget or extension** is the user-facing unit inside an installed host component.
- A **release** is an immutable version of one host component.
- An **artifact** is the signed package bytes referenced by a release.
- A **publisher** owns the product namespace and release history.

One product may support several Tosh apps, but a host must never install a component that does not declare compatibility with that host.

## Public Web Marketplace

The public web platform will eventually provide:

- Product discovery and search.
- Host filtering before installation.
- Product detail pages with screenshots, widget previews, supported sizes, permissions, release notes, source repository, license, support, and privacy metadata.
- Publisher pages and trust information.
- A deep-link handoff to the correct installed host app or host download path.
- Clear unavailable states for incompatible, removed, quarantined, or retired components.

The public surface must not expose private drafts, package filesystem paths, credentials, runtime user data, reviewer secrets, or unpublished moderation information.

## Embedded Marketplace Clients

A host app may provide an embedded marketplace surface using the same versioned API. It must:

- Show only components compatible with that host by default.
- Explain why an incompatible component cannot be installed.
- Hand off installation to the host runtime rather than executing marketplace code.
- Preserve the host's settings, editor, permission, and accessibility conventions.
- Keep the user inside the normal host flow when installation succeeds.
- Show loading, empty, offline, authorization, rejected, quarantined, and success states.

Other Tosh products may be promoted from product-detail surfaces, but cross-product promotion must never make an incompatible component appear installable.

## Publisher Flow

1. A Tosh account becomes eligible for Developer Mode.
2. The publisher accepts terms and creates a stable publisher identity.
3. The publisher creates a product listing and declares supported hosts.
4. The publisher submits a signed host component package.
5. The service validates package paths, manifest schema, compatibility, digest, signature, source/secret policy, and namespace ownership.
6. Independent automated reviewers evaluate usefulness, integration, quality, originality, and capability risk.
7. Agreement may approve the release; disagreement, sensitive capability, or policy flags enter human review.
8. Approved release metadata and artifact bytes become immutable.
9. A host discovers, verifies, and installs the compatible component atomically.
10. A later security or policy event can quarantine, revoke, or supersede the release without rewriting historical evidence.

## Trust and Safety Rules

- Publisher authentication is separate from runtime user permissions.
- The actor identity comes from the authenticated account boundary, never from a submission body.
- Publisher ownership is checked for every product, component, and release mutation.
- Suspended or removed publishers cannot publish.
- Signing keys can rotate and be revoked without silently mutating approved history.
- Package bytes are stored as immutable content-addressed artifacts.
- Metadata never stores raw runtime data or credentials.
- Quarantine disables install actions while preserving an auditable event history.
- A host verifies the package again; web approval is not execution permission.
- Reports, takedowns, appeals, and moderation decisions remain separate from public ratings.

## Compatibility Contract

A component must declare:

- Host ID and package format.
- Minimum and maximum host version when applicable.
- SDK version range.
- macOS/platform version range.
- Capability declarations and risk levels.
- Supported widget sizes, states, settings, actions, and installation behavior.

Compatibility is evaluated before an install action is enabled. Unsupported components are explained, not falsely enabled.

## Required States

Every marketplace surface and installation flow must document:

| State | Required behavior |
|---|---|
| Loading | Preserve host navigation and show a bounded progress state |
| Empty | Explain that no compatible products or releases are available |
| Offline | Keep the host usable and offer retry without losing local state |
| Unauthorized | Ask for the appropriate Tosh account action; never expose private data |
| Forbidden | Explain that the account or host is not eligible without leaking policy internals |
| Incompatible | Show the host, SDK, or platform mismatch clearly |
| Validation failed | Show actionable publisher errors and keep the draft private |
| Under review | Show review status without promising publication |
| Published | Enable discovery and host installation |
| Quarantined | Disable installation and explain the safety status |
| Revoked | Prevent new installation and notify affected hosts according to policy |
| Installed | Return to the host editor/settings flow with the component available |
| Update failed | Keep the previous verified release installed |

## Implementation Boundary Today

NotchinTosh currently contains the first marketplace service contract and publishing reference implementation under `NotchinTosh/marketplace/`. It is the first host-specific implementation, not the complete Tosh Company marketplace. The root ecosystem project documents the shared direction so future apps can adopt the same vocabulary and contracts without copying NotchinTosh's private implementation.