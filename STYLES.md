# STYLES.md — Tosh Company Shared Design System

This document defines the shared visual and interaction language for Tosh products. It is the default for new apps and marketplace surfaces. An app may add a documented extension, but it must not silently redefine the shared foundations.

## Design Intent

Tosh products should feel calm, capable, native to macOS, and slightly more intentional than the system utility they improve. The interface should make a focused action obvious without turning every surface into a dashboard. Visual polish comes from hierarchy, spacing, material, motion, and writing—not from decoration added without purpose.

The system has three qualities:

- **Native:** respect macOS conventions, keyboard behavior, accessibility, menu semantics, safe areas, and user preferences.
- **Focused:** one primary action per surface; secondary actions stay discoverable but quiet.
- **Alive:** use restrained material, depth, and motion to communicate state, not to make the interface busy.

## Product Expression

The ecosystem has a shared foundation rather than one identical skin:

| Layer | Shared rule | App extension |
|---|---|---|
| Identity | Tosh wordmark, naming voice, semantic colors, typography, spacing, accessibility | Product icon, accent hue, and product-specific symbol |
| Window/surface | Native macOS geometry and material behavior | NotchinTosh may use notch/glass surfaces; LaunchinTosh may use launcher panels |
| Interaction | Clear focus, keyboard support, safe dismissal, reduced-motion fallback | Product-specific shortcuts and gestures |
| Marketplace | Same product metadata hierarchy, compatibility language, and trust states | Host-specific installation and settings flow |

No app should borrow another product's visual metaphor without documenting why it belongs to the new product.

## Color Tokens

Use semantic tokens in code. Do not scatter raw colors through views or CSS.

| Token | Meaning | Light appearance | Dark appearance |
|---|---|---|---|
| `canvas` | Main app/background canvas | Warm neutral white | Near-black graphite |
| `surface` | Primary card or panel | White with low contrast | Elevated graphite |
| `surfaceSecondary` | Secondary grouped surface | Cool translucent gray | Translucent charcoal |
| `textPrimary` | Main readable content | Near-black | Near-white |
| `textSecondary` | Supporting content | Neutral gray | Muted gray |
| `textTertiary` | Metadata and hints | Light gray | Dim gray |
| `separator` | Group boundaries | Low-alpha black | Low-alpha white |
| `accent` | Product action and selected state | Product accent | Product accent with contrast check |
| `success` | Completed/healthy state | Accessible green | Accessible green |
| `warning` | Attention required | Accessible amber | Accessible amber |
| `danger` | Destructive/revoked/error state | Accessible red | Accessible red |
| `focusRing` | Keyboard focus | High-contrast accent | High-contrast accent |

### Color Rules

- Semantic state colors must not be the only indication of state; pair them with text, iconography, or shape.
- Accent color may identify a product, but it must not reduce text contrast.
- Translucency never replaces a readable background. Use an opaque or stronger fallback when the backdrop is noisy, unavailable, or accessibility settings require it.
- Marketplace trust states use `success`, `warning`, and `danger` consistently across web and host clients.
- Each product chooses one primary accent and at most two supporting accents. The root registry should record the choice when a product becomes public.

## Typography

Use the platform system font unless a product has a documented reason to add a typeface.

| Role | macOS default | Web fallback | Use |
|---|---|---|---|
| Display | SF Pro Display | `-apple-system`, `BlinkMacSystemFont`, ` sans-serif` | Product names and large hero statements |
| Title | SF Pro Display/SF Pro Text | Same | Window and page titles |
| Body | SF Pro Text | Same | Explanations and settings |
| Label | SF Pro Text medium | Same | Buttons, tabs, field labels |
| Caption | SF Pro Text | Same | Metadata, hints, timestamps |
| Code | SF Mono | `ui-monospace`, monospace | IDs, versions, diagnostics, package paths |

Typography rules:

- Preserve the platform's Dynamic Type/Text Size preference where available.
- Prefer sentence case.
- Use bold weight for hierarchy, not all caps.
- Limit a paragraph to a readable line length on web surfaces.
- Do not use tiny text to fit more controls into a panel.
- Product names, publisher names, host names, and release versions must remain visually distinct.

## Spacing and Geometry

Use a four-point base grid with an eight-point rhythm for major composition:

```text
space-1  = 4
space-2  = 8
space-3  = 12
space-4  = 16
space-5  = 20
space-6  = 24
space-8  = 32
space-10 = 40
space-12 = 48
space-16 = 64
```

Rules:

- Use `space-2` or larger between unrelated controls.
- Use `space-4` between label/content groups.
- Use `space-6` or larger between sections.
- Keep interactive targets at least 44 points on macOS touch-oriented surfaces and at least 24 points for pointer/keyboard controls where the platform convention allows; do not make a control visually small and impossible to use.
- Use intrinsic layout, grids, and constraints. Never hardcode a product surface to one screen size.
- Respect the physical notch, safe areas, menu bar, window margins, and web responsive breakpoints.

## Shape, Materials, and Depth

| Element | Default |
|---|---|
| Small control radius | 8 |
| Card radius | 12 |
| Primary panel radius | 16 |
| Floating/hero surface radius | 20, only when it supports the composition |
| Border | One-pixel semantic separator or low-alpha edge |
| Shadow | Soft, broad, low opacity; never the only separation |
| Material | Native macOS material where available; opaque fallback elsewhere |

Glass is a material, not a brand requirement. A surface using glass must still work over light/dark, high contrast, reduced transparency, and visually complex content. Do not stack multiple unrelated blur layers.

## Components

Shared component conventions:

- **Button:** one clear primary action, quiet secondary action, destructive action separated and labeled.
- **Tab/navigation:** selected state has text/icon plus a non-color cue; keyboard traversal is predictable.
- **Card:** communicates one object or one decision; avoid cards nested inside cards without hierarchy.
- **List:** stable row height unless content requires expansion; preserve focus and scroll position through updates.
- **Form:** labels remain visible, validation appears next to the field and in a summary when needed, errors do not erase entered values.
- **Popover/sheet:** has an obvious focus destination, safe Escape/outside-click behavior, and a clear dismissal path.
- **Marketplace product tile:** product name, publisher, host compatibility, primary preview, and install/discover action have a stable hierarchy.
- **Compatibility badge:** states the host and compatibility result in text; an icon alone is insufficient.
- **Permission explanation:** explains what is accessed, why, when, and how to deny or change it.
- **Diagnostic surface:** uses readable code and copyable text; never exposes secrets.

## Motion

Motion should explain a change in state or preserve spatial continuity.

| Motion | Default feel | Trigger | Reduced-motion fallback |
|---|---|---|---|
| Surface reveal | Short ease-out, opacity plus bounded scale | Panel/popover opens | Fade only |
| Surface dismiss | Short ease-in, content leaves toward origin | Close, Escape, outside click | Fade only |
| Selection change | Quick color/opacity transition | Tab, row, widget selection | Immediate state change |
| Layout update | Spring-like movement with bounded overshoot | Reorder, resize, install completion | Crossfade or immediate layout |
| Loading | Calm opacity/progress motion | Network or validation work | Static progress indicator |
| Error/success | Small emphasis, never a shake loop | Validation result | Color/icon/text only |

Rules:

- Animations must be interruptible when the user closes a surface or changes context.
- Do not animate essential content in a way that delays access.
- Never use continuous motion as decoration in a focused utility surface.
- Test with reduced motion and increased contrast enabled.
- Document app-specific spring values in the app's own `STYLES` extension or DOCKS file.

## Interaction and Accessibility

Every interactive surface must support the relevant combination of:

- Mouse, trackpad, keyboard, and VoiceOver.
- Visible focus and logical focus order.
- Escape and safe dismissal where a transient surface is used.
- Full keyboard operation without requiring a drag or hover.
- Dynamic text size and high-contrast settings.
- Reduced motion and reduced transparency.
- Empty, loading, error, offline, disabled, denied, and success states.
- Copyable error/diagnostic details without exposing secrets.

A visual state is incomplete until its announcement, focus behavior, and keyboard behavior are documented.

## Writing Voice

Tosh copy is direct, calm, and specific:

- Say what happened and what the user can do next.
- Prefer “Couldn’t install this widget” over “Something went wrong.”
- Prefer “This widget needs Calendar access” over “Permission required.”
- Avoid exaggerated claims, fake urgency, and vague AI language.
- Use the same terms everywhere: product, host, component, widget, release, publisher, permission, quarantine, and rollback.
- Keep labels short; put explanation in supporting text.

## Marketplace Style Rules

Marketplace surfaces must feel like a trusted product catalog, not an ad network:

- Product previews lead; metadata supports the decision.
- Compatibility is visible before installation.
- Publisher identity, source, license, permissions, and release history are easy to find.
- Install actions show the target host and the expected permission step.
- Quarantined, revoked, incompatible, and unavailable states are explicit and never represented as normal installable products.
- Public catalog surfaces never reveal private drafts, account tokens, package filesystem paths, or raw runtime data.

## App Extensions

Each app may add a local style document containing:

- Product accent and icon rules.
- App-specific surfaces and layout constraints.
- App-specific motion values.
- Host-specific capability and permission presentation.
- Product-specific vocabulary.

The extension must reference this file and list every intentional deviation. If a rule is needed by two or more apps, move it back into this shared document rather than duplicating it.