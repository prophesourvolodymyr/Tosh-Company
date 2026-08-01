# F02 — Tosh Marketplace (Raw)

F02 defines the shared marketplace direction for discovering, publishing, validating, and installing compatible Tosh widgets and extensions. It is an ecosystem feature, not a promise that every app is immediately installable.

## What We Build

- Public web catalog for Tosh products and host components.
- Publisher account and Developer Mode eligibility boundary.
- Product, host component, widget, release, artifact, and compatibility concepts.
- Signed package submission and automated validation.
- Two-reviewer quality/originality review with human escalation.
- Host-filtered discovery and compatibility explanations.
- Deep-link handoff to the correct installed host app.
- Immutable artifact and release history.
- Quarantine, revocation, takedown, appeals, and rollback concepts.
- Privacy boundary that excludes runtime data, credentials, and private drafts from public metadata.

## Architecture

```text
Publisher account
       │ submits signed component
       ▼
Marketplace service ──> validation ──> automated review ──> human escalation
       │                                          │
       ├── public catalog metadata                └── release decision/audit
       └── immutable artifact store
                         │
                         ▼
              host-specific marketplace client
                         │
                         ▼
              host verification and installation
                         │
                         ▼
                    host runtime/editor
```

The marketplace service never executes package code. The host verifies the package, evaluates compatibility, requests user permissions, installs atomically, and isolates runtime failures.

## Required States

| Area | States |
|---|---|
| Catalog | Loading, populated, empty, offline, incompatible, unavailable, quarantined |
| Publisher | Not signed in, ineligible, Developer Mode enabled, terms missing, active, restricted, suspended, removed |
| Submission | Draft, validating, rejected, under review, needs human review, approved, published, quarantined |
| Release | Draft, published, superseded, revoked, archived |
| Installation | Not installed, verifying, permission required, installing, installed, update available, update failed, rolled back |
| Artifact | Missing, digest mismatch, signature failure, immutable, unavailable |

Every state needs user-visible copy, safe retry behavior, and a defined effect on existing installed components.

## Compatibility

Every host component declares host ID, package format, host version range, SDK range, platform range, capabilities, permission risk, and supported widget contract. The catalog may show an incompatible product for discovery, but it must not enable installation for the wrong host.

## Security and Privacy

- Actor identity comes from the authenticated account boundary, not request JSON.
- Publisher ownership is checked for all mutations.
- Signing keys are never logged or stored in public metadata.
- Artifact paths are content-addressed and immutable.
- Runtime user data and credentials never enter product metadata.
- Quarantine removes install actions while keeping history auditable.
- Host verification is mandatory even after marketplace approval.

## Dependencies

- F01 — Tosh ecosystem foundation and stable host/product vocabulary.
- Host apps — each host must define its package, capability, permission, and installation contract before it becomes installable.
- A separately operated account, metadata, and artifact service for production deployment.

## Reference

- `NotchinTosh/marketplace/` — current first-host reference implementation; learn its service boundaries and tests, but do not assume it is the complete shared marketplace.
- `NotchinTosh/features/F4-MArketplace/` — current NotchinTosh marketplace specifications.
- `genesis/MARKETPLACE VISION.md` — root ecosystem direction.

## Verification

| Scenario | Expected result | Evidence |
|---|---|---|
| Product with several hosts | One product has separate compatible host components without duplicate product identity | Pending root feature audit |
| Host filtering | A host sees only installable components for its own contract | Pending root feature audit |
| Signed submission | Invalid source, manifest, digest, or signature stops publication | Pending root feature audit |
| Review disagreement | Release enters human review without changing the previous published release | Pending root feature audit |
| Quarantine | New installation is disabled while history remains available for audit | Pending root feature audit |
| Host failure | A failed component cannot damage the host shell or unrelated installed components | Pending host-runtime implementation |
| Privacy | Public metadata contains no runtime user data or credentials | Pending root feature audit |