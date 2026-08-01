# CYCLES.md — Tosh Company Ecosystem

**Planned with user:** 2026-08-01

This root cycle file coordinates ecosystem documentation and shared contracts. Each app keeps its own implementation cycles. The future marketplace is documented here first and implemented in its owning project later.

> **Status:** The cycles below are proposed. Cycle 0 documentation is complete; feature promotion and implementation require review and approval.

## Dependency Chain

```text
F01 Tosh ecosystem foundation
            │
            ├──────────────> F02 Tosh Marketplace
            │                         │
            │                         ▼
            └──────────────> F03 Cross-App Host Integration
                                      │
                         independent Tosh app hosts
          NotchinTosh · LaunchinTosh · LockinTosh · SwitchinTosh · CleaninTosh
```

The apps can develop independently. An app cannot become an installable marketplace host until it satisfies F03's host contract.

## Cycle 0 — Root Documentation

- [x] Run `projinit` in the Tosh Company root
- [x] Initialize the Tosh Company root Git repository
- [x] Capture the ecosystem origin idea
- [x] Write the ecosystem superstructure and ownership boundary
- [x] Create the Tosh app registry
- [x] Create the ecosystem map and onboarding direction
- [x] Define shared Tosh styles, motion, accessibility, and writing rules
- [x] Document the shared Tosh Marketplace direction
- [x] Create raw F01, F02, and F03 DOCKS documents
- [x] Create the root feature index
- [ ] Review the proposed feature breakdown and promote the first approved feature

## Cycle 1 — F01: Tosh Ecosystem Foundation

- [ ] Promote `genesis/F01-raw/` to an approved feature after review
- [ ] Finalize product and host ID rules
- [ ] Finalize app onboarding contract
- [ ] Define shared contract versioning and deprecation policy
- [ ] Record each app's adopted `STYLES.md` revision
- [ ] Verify a new agent can start an app using only the root ecosystem docs

## Cycle 2 — F02: Tosh Marketplace

- [ ] Promote `genesis/F02-raw/` to an approved feature after F01
- [ ] Define public product and host-component API contracts
- [ ] Define publisher account, Developer Mode, and signing-key boundaries
- [ ] Define package validation and review policy
- [ ] Define immutable artifact storage and release history
- [ ] Migrate the verified marketplace service from `NotchinTosh/marketplace/` into the designated `ToshMarketplace/` repository before new service work begins
- [ ] Build the public web marketplace in its owning project
- [ ] Build publisher submission and moderation flows
- [ ] Verify privacy, compatibility, quarantine, rollback, and trust states

## Cycle 3 — F03: Cross-App Host Integration

- [ ] Promote `genesis/F03-raw/` to an approved feature after F01 and F02 contracts
- [ ] Define host registration and compatibility requirements
- [ ] Define installation, update, rollback, removal, and quarantine lifecycle
- [ ] Define capability and permission contracts
- [ ] Define crash/resource boundaries and diagnostics
- [ ] Verify the first host end to end
- [ ] Add additional Tosh hosts only after each app passes its own host evidence

## App Adoption Track — Documentation Complete

- [x] NotchinTosh — add `ECOSYSTEM.md` and root `DOCKS.md`
- [x] LaunchinTosh — add `ECOSYSTEM.md` and root `DOCKS.md`
- [x] LockinTosh — add `ECOSYSTEM.md` and root `DOCKS.md`
- [x] SwitchinTosh — add `ECOSYSTEM.md` and root `DOCKS.md`
- [x] CleaninTosh — add `ECOSYSTEM.md` and root `DOCKS.md`

## Cycle 0 Evidence — Shared Repository Setup

The root repository now has canonical `ECOSYSTEM.md` and `DOCKS.md` documents. `ToshSDK/` and `ToshMarketplace/` are initialized Git repositories with their own ecosystem and architecture documents. Every Tosh project boundary has the same explicit rule: app-specific needs may be contributed to the shared SDK or marketplace through versioned, tested, compatibility-aware contracts.

## Root Verification Standard

The root project is ready to promote a feature when:

- The relevant DOCKS document explains behavior, ownership, states, dependencies, and verification.
- The app registry and ecosystem map agree with the feature's host/product IDs.
- `STYLES.md` covers the shared visual and accessibility behavior.
- Private app implementation and credentials remain outside the root documentation layer.
- A new AI session can find the next file and understand what is approved versus proposed.