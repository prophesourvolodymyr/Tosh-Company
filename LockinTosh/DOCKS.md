# LockinTosh — Lock-Screen Host

LockinTosh is the Tosh host for lock-screen widgets on macOS. It combines a stable lock-screen composition with a shared SDK so developers can create compatible indicators, music widgets, and Live Activity-style components without controlling the entire lock screen.

## What We Build

- A lock-screen host surface below the clock and in declared lock-screen regions.
- Small indicators, a widget row, Live Activity content, and an expanded lock-screen surface.
- A default music player widget based on the approved reference direction.
- Shared SDK integration for widget identity, declarative render data, settings, actions, permissions, and compatibility.
- Marketplace discovery, installation, update, rollback, and removal for compatible lock-screen components.
- Host-controlled resource limits, permissions, focus, and failure recovery.

## Architecture

```text
LockinTosh host
├── lock-screen lifecycle and permission boundary
├── region layout
│   ├── below-clock indicators
│   ├── widget row
│   ├── Live Activity region
│   └── expanded lock-screen surface
├── native renderer and accessibility
├── ToshLockScreenSDK host extension
├── marketplace client
└── isolated component runtime
```

## Regions and States

| Region/state | Required behavior |
|---|---|
| Below-clock indicators | Compact, glanceable content; no overlap with the clock or system safe areas |
| Widget row | Hosts one or more declared widgets within the row footprint; invalid spans are rejected |
| Live Activity | Shows only declared semantic regions and compact/expanded variants |
| Expanded surface | Opens from a declared action; closes safely on Escape, outside click, or lock-screen transition |
| Default | Shows installed components and stable empty/fallback content |
| Loading | Keeps region geometry stable while component data resolves |
| Empty | Explains that no component is installed without taking over the lock screen |
| Permission denied | Disables only the affected widget/capability and preserves the rest of the lock screen |
| Offline | Uses local state or cached content; remote marketplace operations explain unavailability |
| Incompatible | Rejects package before install or render and leaves the prior component active |
| Component crash | Removes only the failed component, records diagnostics, and keeps the host usable |
| Reduced motion | Uses direct or fade-only transitions and respects system settings |
| Locked/unlocked transition | Suspends unsafe content and restores only after host permission/lifecycle checks |

## Visual Rules

- Content is subordinate to the system clock and lock-screen safety.
- Region size, placement, typography, contrast, and safe areas come from host layout, not arbitrary package coordinates.
- The visual language may use liquid glass and native macOS materials, but a marketplace component cannot create an unrestricted background or window.
- Music controls expose clear playback state, artwork fallback, and accessible action labels.
- Animations are interruptible when lock state, focus, or component priority changes.

## Security and Privacy

- Components receive only declared lock-screen capabilities.
- Credentials and private host data remain in LockinTosh.
- Marketplace packages are verified by digest/signature and host compatibility before execution.
- A failed component cannot prevent lock/unlock or modify another region.

## Open SDK and Marketplace Extensions

LockinTosh can propose new shared SDK primitives, lock-screen modules, marketplace metadata, or installation APIs whenever a real feature requires them. It should prototype host-specific behavior locally, then contribute reusable contracts with tests, compatibility, and security evidence. There is no rule that LockinTosh must wait for another host to request the same need.

## Files

- `ORIGINAL IDEA.md` — initial product intent.
- `reference/` — lock-screen indicator and music references.
- `music player/` — music-specific exploration.
- `DOCKS.md` — host contract and behavior.
- `ECOSYSTEM.md` — ownership and shared-project relationship.

## Dependencies

- `../ToshSDK` and a future `ToshLockScreenSDK`.
- `../ToshMarketplace` for catalog and publishing contracts.
- Root `../STYLES.md`.
- macOS lock-screen and media APIs.

## Verification

| Scenario | Expected result | Evidence |
|---|---|---|
| Region layout | Indicators and widget rows stay inside declared lock-screen regions | Pending implementation |
| Music widget | Compact and expanded playback content render with safe fallbacks | Pending implementation |
| Package install | Compatible signed component installs atomically | Pending implementation |
| Permission denial | Denied capability is hidden/explained while other regions continue | Pending implementation |
| Component crash | Host and unrelated regions remain usable | Pending implementation |
| Lock transition | Unsafe content suspends and restores only after validation | Pending implementation |