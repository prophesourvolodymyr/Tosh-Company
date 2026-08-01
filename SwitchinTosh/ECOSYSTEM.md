# ECOSYSTEM.md — SwitchinTosh

## Identity

SwitchinTosh is the Tosh macOS app switcher. It owns a fast, native-feeling switcher surface and may later expose compatible switcher widgets or marketplace components.

## Ecosystem Position

- Product type: macOS app switcher host.
- Host ID: provisional; define before marketplace publication.
- SDK consumer: shared Tosh contracts when widget or package integration begins.
- Marketplace role: optional publisher and client for compatible switcher extensions.

## Owns

- App-switcher activation, selection, ordering, keyboard navigation, and dismissal.
- Native glass surface, focus behavior, transitions, and app lifecycle integration.
- Switcher-specific settings and performance constraints.

## Does Not Own

- Generic widget/package schemas.
- Shared marketplace publishing and catalog infrastructure.
- Another Tosh host's windows, layouts, or runtime.

## Open Contribution Rule

SwitchinTosh may contribute any real need to `ToshSDK` or `ToshMarketplace`: switcher actions, app identity metadata, focus events, host-specific widgets, catalog fields, or installation behavior. A feature can begin as a private implementation and become shared when reuse is demonstrated. App origin is not a restriction; safety, compatibility, and tests are the requirements.

## Current State

The project has a v3 switcher mockup direction and an Xcode implementation workspace. Native glass styling, rounded macOS geometry, and final interaction behavior are being consolidated into the host contract.

## Related Documents

- `../ECOSYSTEM.md`
- `../DOCKS.md`
- `DOCKS.md`
- `ORIGINAL IDEA.md`
- `CYCLES.md`