# F03 — Cross-App Host Integration (Raw)

F03 defines the shared contract a Tosh app must provide before it can install and run marketplace components. It keeps the marketplace generic while allowing each host to expose a deliberate capability surface.

## What We Build

- Stable host registration and compatibility metadata.
- Host-owned package verification and installation lifecycle.
- Atomic install, update, rollback, removal, and quarantine behavior.
- Capability declarations, permission explanations, consent, and revocation.
- Resource limits and crash isolation for installed components.
- Host-to-component diagnostics without exposing private host state.
- Deep-link and settings handoff conventions.
- A common installed-component state model that each app can render in its own style.

## Architecture

```text
Marketplace catalog/API
        │ compatible component metadata and artifact reference
        ▼
Host marketplace client
        │ user intent and account context
        ▼
Host installation controller
        ├── signature/digest verifier
        ├── compatibility evaluator
        ├── permission and capability gate
        ├── atomic installation store
        ├── process/resource boundary
        └── diagnostics and rollback
                 │
                 ▼
           Host editor/runtime
```

The host owns execution. The marketplace supplies metadata and signed artifacts. A widget or extension cannot create arbitrary top-level windows, bypass host layout, receive another app's process handle, or access private credentials.

## Installation States

| State | Host behavior |
|---|---|
| Available | Show compatible component and install action |
| Verifying | Validate manifest, digest, signature, compatibility, and package paths |
| Permission required | Explain each capability before requesting consent |
| Installing | Keep previous installed version usable until atomic activation succeeds |
| Installed | Register compatible widgets and expose host editor/settings controls |
| Update available | Show release notes and preserve current version until update succeeds |
| Update failed | Keep previous verified version and show retry/diagnostics |
| Quarantined | Disable activation, preserve evidence, and explain recovery path |
| Removed | Remove active component according to policy while keeping audit history |
| Crash limited | Stop or restart the component without taking down the host shell |

## App-Specific Responsibility

Each host app decides:

- Where installed widgets appear.
- Which capabilities exist and how they are explained.
- Which settings and editor controls are appropriate.
- How the app handles offline catalog access.
- What a safe rollback looks like for its architecture.

The app must document those decisions in its own project. This root feature defines the minimum contract, not the final UI.

## Dependencies

- F01 — shared identity, terminology, and style system.
- F02 — marketplace component and release model.
- Host app runtime and SDK implementation.
- Account and artifact service boundaries.

## Reference

- `NotchinTosh/` bridge runtime and `NotchinToshWidgetSDK/` are the first host/runtime reference.
- `NotchinTosh/features/F4-MArketplace/` describes NotchinTosh-specific marketplace behavior.

## Verification

| Scenario | Expected result | Evidence |
|---|---|---|
| Wrong host package | Installation is rejected before activation | Pending host contract audit |
| Signature failure | Package never executes | Pending host contract audit |
| Permission denial | Only the affected capability is unavailable | Pending host contract audit |
| Update failure | Previous verified component remains usable | Pending host contract audit |
| Component crash | Host shell and unrelated components remain usable | Pending host contract audit |
| Removal | Component no longer activates and user settings follow documented retention policy | Pending host contract audit |
| Reduced motion/accessibility | Host UI follows shared style and accessibility rules | Pending host contract audit |