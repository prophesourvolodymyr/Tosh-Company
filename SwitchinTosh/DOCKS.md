# SwitchinTosh — App Switcher Host

SwitchinTosh is a native macOS app switcher under Tosh Company. The current visual direction is a refined v3 mockup with rounded macOS geometry and an `NSGlassEffectView`-style background. The host must remain fast, keyboard-first, and independent from any marketplace package.

## What We Build

- Global app-switcher activation and dismissal.
- Glass-backed switcher surface with rounded native geometry.
- App icons, names, selection state, and predictable ordering.
- Keyboard selection and activation flow.
- Mouse/pointer selection where supported.
- Smooth open, selection, and dismiss transitions that do not block the desktop.
- Settings for switcher behavior and appearance.
- A future bounded widget/extension surface only if the host contract requires it.

## Architecture

```text
SwitchinTosh
├── activation monitor
├── running-application snapshot
├── selection and focus model
├── glass switcher surface
├── keyboard/pointer interaction
├── settings
└── optional ToshSDK/ToshMarketplace clients
```

## States

| State | Behavior |
|---|---|
| Inactive | No visible surface; desktop and active app are untouched |
| Opening | Surface appears with native-feeling motion and selection is initialized deterministically |
| Active | Current app selection is prominent; keyboard focus remains inside the switcher |
| Moving selection | Selection updates without rebuilding unrelated content or losing focus |
| Empty | If no switchable app exists, show a safe brief fallback and dismiss cleanly |
| Activating | Selected app is activated once; duplicate key repeats do not create duplicate launches |
| Dismissing | Surface leaves without stealing focus from the resulting active app |
| Permission denied | Explain unavailable app/system data and keep manual recovery possible |
| App list changed | Update safely without jumping selection unless the selected app disappeared |
| Reduced motion | Use direct/fade-only appearance and selection changes |
| Failure | A stale app snapshot or rendering issue does not trap keyboard input or block the desktop |

## Visual and Interaction Rules

- Use the physical display and menu-bar safe areas; do not hardcode a universal position.
- Prefer native glass materials, rounded corners, clear hierarchy, and restrained shadows.
- Keep hit targets and focus indicators accessible.
- Support Escape and the documented modifier-release behavior for dismissal.
- Motion must be interruptible when activation or dismissal happens.
- Do not let an installed extension create a separate unrestricted window.

## Open SDK and Marketplace Extensions

SwitchinTosh can propose shared SDK additions or marketplace contracts whenever a switcher feature needs them. Examples include app identity models, switcher actions, focus events, host-specific widgets, or installation metadata. It is acceptable to keep an idea private to this host; it is equally acceptable to contribute a reusable module. The decision is evidence-based and open to all Tosh projects.

## Files

- `SwitchinTosh.xcodeproj/` — primary Xcode project.
- `Switch.xcodeproj/` — legacy/alternate project boundary to reconcile.
- `Sources/` — app implementation.
- `tools/` — build or development tooling.
- `switchin Mock UP/` — visual reference and mockup work.
- `ORIGINAL IDEA.md` — initial product intent.

## Dependencies

- `../ToshSDK` when public extension contracts are introduced.
- `../ToshMarketplace` only for optional compatible component discovery.
- Root `../STYLES.md`.
- macOS application and event APIs.

## Verification

| Scenario | Expected result | Evidence |
|---|---|---|
| Open switcher | Surface appears in the intended location without blocking unrelated desktop content | Pending device verification |
| Selection | Keyboard and pointer select the intended app with visible focus | Pending device verification |
| Activation | Selected app activates exactly once and switcher dismisses cleanly | Pending device verification |
| App list mutation | Selection remains stable or recovers predictably when apps change | Pending device verification |
| Reduced motion | Motion fallback respects system preference | Pending device verification |
| Failure/permission | Desktop remains usable and user receives a recoverable state | Pending device verification |