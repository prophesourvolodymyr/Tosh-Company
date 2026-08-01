# CleaninTosh — Cleaning And Maintenance Host

CleaninTosh is an empty product boundary for a future macOS cleaning and maintenance utility. No implementation is claimed here. This document records the ownership and safety requirements that must be resolved before code begins.

## What We Build

The first approved feature must define the exact cleaning scope. The product may eventually include:

- A scan model that explains what will be inspected.
- Categorized findings with size, path, reason, and risk.
- Explicit user confirmation before destructive actions.
- Exclusions, safe-listing, and permission-aware access.
- Preview, progress, cancellation, recovery, and rollback behavior.
- Local settings and audit history.
- Optional status widgets or marketplace components after the host safety model is verified.

No deletion behavior, filesystem claim, or marketplace component is implied until its feature DOCKS document is approved.

## Architecture Boundary

```text
CleaninTosh host
├── scan engine (future)
├── findings and risk model (future)
├── confirmation and exclusion UI (future)
├── safe mutation/recovery layer (future)
├── settings and audit history (future)
├── optional ToshSDK client
└── optional ToshMarketplace client
```

## Required States

Every future cleaning feature must specify:

- Idle, scanning, paused, cancelled, and completed.
- No findings and findings grouped by risk/category.
- Permission denied, partial access, inaccessible path, and stale result.
- Destructive action confirmation, in progress, success, partial failure, and rollback.
- Offline behavior for any remote metadata or marketplace operation.
- Empty, loading, error, and reduced-motion presentation.

## Safety Rules

- Never delete without explicit confirmation of the selected scope.
- Show exact paths or an understandable privacy-preserving equivalent before mutation.
- Keep system-critical paths excluded by default.
- Make cancellation and failure recoverable.
- Keep credentials, private file content, and scan results inside the host unless a future contract explicitly says otherwise.
- A widget or marketplace package cannot receive unrestricted filesystem access merely because it is installed.

## Open SDK and Marketplace Extensions

CleaninTosh may propose shared SDK or marketplace additions whenever implementation reveals a reusable need. It may contribute scan status contracts, permission explanations, safe-action models, catalog metadata, or host-specific components. The app does not need to wait for another Tosh project; it must document the proposed boundary, security model, compatibility, and tests.

## Files

- `ECOSYSTEM.md` — project role and shared ownership.
- `DOCKS.md` — current boundary and pre-build requirements.
- Future `features/` or `genesis/` docs — approved product scope.
- Future `Sources/`, tests, and project manifest — created only after the first feature is planned.

## Dependencies

- `../ToshSDK` for any shared widget or host contract.
- `../ToshMarketplace` for optional discovery and publishing.
- Root `../STYLES.md`.
- macOS filesystem permissions and security APIs.

## Verification

| Scenario | Expected result | Evidence |
|---|---|---|
| Project initialization | First feature documents scan scope, risk, permissions, and recovery before implementation | Pending first feature |
| Safe preview | User can understand selected findings before any mutation | Pending implementation |
| Permission failure | No unauthorized operation occurs and recovery is clear | Pending implementation |
| Partial failure | Successful and failed operations are distinct and recoverable | Pending implementation |
| SDK contribution | Any reusable status or permission contract is proposed with safety evidence | Pending shared integration |
| Marketplace component | Installation cannot grant unrestricted filesystem access | Pending marketplace integration |