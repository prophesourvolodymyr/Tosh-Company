# ECOSYSTEM.md — CleaninTosh

## Identity

CleaninTosh is the Tosh product space for a macOS cleaning and maintenance utility. It is currently an empty incubation boundary and has no implementation contract yet.

## Ecosystem Position

- Product type: future macOS maintenance host.
- Host ID: not assigned.
- SDK consumer: only if the product adds a widget, status surface, or shared host integration.
- Marketplace role: may publish compatible cleaning/status components after the host and safety model are defined.

## Owns

- Future cleaning workflows, scan results, user confirmation, deletion safety, recovery, and settings.
- Product-specific privacy, filesystem permissions, exclusions, and rollback behavior.

## Does Not Own

- Generic widget or package contracts.
- Shared marketplace catalog, accounts, review, or artifact storage.
- Another Tosh app's private runtime or data.

## Open Contribution Rule

CleaninTosh may add needed capabilities to `ToshSDK` or `ToshMarketplace` at any time. It can request a status widget, filesystem-scan capability, permission explanation, marketplace product type, or installation contract. It may keep the feature app-specific or contribute it as a reusable module; the ecosystem is open to product-driven additions with clear safety and compatibility evidence.

## Current State

No source files or feature specification exist yet. This document establishes the project boundary so future work starts with shared ecosystem context instead of inventing a private parallel platform.

## Related Documents

- `../ECOSYSTEM.md`
- `../DOCKS.md`
- `DOCKS.md`
- `ORIGINAL IDEA.md` when created
- `CYCLES.md` when the first feature is planned