# Tosh App Registry

This registry tells an agent what each Tosh project is, where its implementation lives, and what ecosystem questions remain open. It is a coordination document, not a replacement for the app's own project documentation.

## Registered Products

| Product ID | Name | Folder | Primary problem | Host status | Marketplace status |
|---|---|---|---|---|---|
| `com.tosh.notchintosh` | NotchinTosh | `NotchinTosh/` | Make the Mac notch a useful, extensible surface | Runtime and public widget SDK exist | Marketplace service contract and publishing reference implementation exist; host client and installation integration remain |
| `com.tosh.launchintosh` | LaunchinTosh | `LaunchinTosh/` | Provide a better macOS launcher/app replacement | Project exists; contract needs confirmation | Not registered as an installable host yet |
| `com.tosh.lockintosh` | LockinTosh | `LockinTosh/` | Provide lock-screen widgets for macOS | Idea/project incubation | Not registered as an installable host |
| `com.tosh.switchintosh` | SwitchinTosh | `SwitchinTosh/` | Provide a polished macOS app switcher | Mockup and product direction exist | Not registered as an installable host |
| `com.tosh.cleanintosh` | CleaninTosh | `CleaninTosh/` | Provide a macOS cleaning and maintenance utility | Product folder exists; scope needs definition | Not registered as an installable host |

## Host Registration Requirements

An app is not marketplace-installable merely because its folder exists. Before registration, its project must define:

- Stable product and host IDs.
- Supported macOS and SDK versions.
- Package format and signature requirements.
- Capability catalog and permission prompts.
- Installation, update, rollback, removal, and quarantine behavior.
- Deep-link scheme or a documented host handoff.
- Accessibility and reduced-motion behavior.
- Privacy boundary for runtime data and credentials.
- Build, test, and target-device evidence.

## Updating the Registry

Update this document when an app is created, renamed, promoted to a host, retired, or changes its marketplace contract. Keep implementation details in the app repository and link the relevant project docs rather than copying them into this registry.