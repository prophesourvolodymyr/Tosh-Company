# ECOSYSTEM.md — LockinTosh

## Identity

LockinTosh is the Tosh lock-screen host for macOS. It will render lock-screen indicators, Live Activity-style content, and music widgets in host-controlled regions while consuming shared Tosh contracts.

## Ecosystem Position

- Product type: macOS lock-screen host.
- Host ID: `com.tosh.lockintosh` (provisional until the product contract is finalized).
- SDK consumers: `ToshSDKCore`, `ToshWidgetSDK`, and a future `ToshLockScreenSDK`.
- Marketplace role: may install and publish compatible lock-screen host components.

## Owns

- Lock-screen host layout and regions below the clock.
- Lock-screen capabilities, settings, permissions, and lifecycle.
- Lock-screen installation, rollback, and runtime enforcement.
- Native composition of indicators, widget rows, Live Activity content, and expanded lock-screen surfaces.

## Does Not Own

- Generic widget/package schemas that belong in ToshSDK.
- Global marketplace accounts or publishing infrastructure.
- NotchinTosh's notch layout or private runtime.

## Open Contribution Rule

LockinTosh may add any needed capability to `ToshSDK` or `ToshMarketplace`. A lock-screen-specific contract is welcome when it is reusable, such as a region declaration, lock-screen permission, Live Activity model, or installation capability. LockinTosh-specific behavior can stay local when it only controls this host's private layout. Product needs are allowed to drive shared platform additions.

## Current State

The project is incubating its host contract and reference lock-screen visuals. Shared SDK revision, marketplace revision, host IDs, and production runtime integration are pending.

## Related Documents

- `../ECOSYSTEM.md`
- `../DOCKS.md`
- `DOCKS.md`
- `ORIGINAL IDEA.md`
- `CYCLES.md`
- `reference/`