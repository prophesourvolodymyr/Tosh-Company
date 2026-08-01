# Tosh Company Root Repository Structure

## Recommended Shape

```text
Tosh-Company/
├── AGENTS.md                         # root AI/project management rules
├── CYCLES.md                         # ecosystem documentation and shared-contract cycles
├── STYLES.md                         # shared visual, motion, accessibility, and writing system
├── genesis/
│   ├── ORIGINAL IDEA.md              # raw ecosystem spark
│   ├── INITIAL IDEA.md               # approved-direction candidate for the ecosystem
│   ├── APP REGISTRY.md               # every Tosh product and host status
│   ├── ECOSYSTEM MAP.md              # ownership and dependency boundaries
│   ├── MARKETPLACE VISION.md         # marketplace direction and trust model
│   ├── REPOSITORY STRUCTURE.md       # this document
│   ├── REFERENCE/                    # external repos, links, images, and research
│   ├── F01-raw/DOCKS.md              # ecosystem foundation incubation
│   ├── F02-raw/DOCKS.md              # marketplace incubation
│   └── F03-raw/DOCKS.md              # cross-app host integration incubation
├── features/
│   └── DOCKS.md                      # approved ecosystem feature index
├── prompts/                          # prompts for root ecosystem slices
├── skills/                           # reusable ecosystem skills
├── junk/                             # disposable mockups and temporary files
├── protocols/                        # shared F-Cycle protocols installed by projinit
│
├── NotchinTosh/                      # independent app project/repository
├── LaunchinTosh/                     # independent app project/repository
├── LockinTosh/                       # independent app project/folder
├── SwitchinTosh/                     # independent app/folder and mockups
└── CleaninTosh/                      # independent app/folder
```

## Ownership Rules

### Root owns

- Shared ecosystem identity and naming.
- The app registry and product/host IDs.
- Shared styles and writing conventions.
- Cross-app contracts and versioning rules.
- Marketplace direction and ecosystem-level trust rules.
- Which feature proposals are raw, promoted, or archived.

### Each app owns

- Source code, tests, build settings, and release artifacts.
- App-specific `AGENTS.md`, `CYCLES.md`, `STYLES` extensions, and DOCKS files.
- Product-specific visual details and interaction states.
- Host runtime and capability implementation.
- App credentials and deployment configuration.

## Repository Relationship

The root may contain app folders for convenient discovery, but it should not force all apps into one build. Existing nested Git repositories remain independently versioned. New apps should be created as separate projects and registered here.

If a future web marketplace becomes large enough to need its own deployment, it should receive its own project repository while remaining linked from this root registry. The root marketplace documents should then become the shared product contract, not a duplicate of the web service's implementation docs.

## Documentation Flow

```text
genesis/ raw idea and raw feature docs
              │
              ▼
root review and dependency decision
              │
              ▼
features/ approved ecosystem DOCKS
              │
              ▼
app or marketplace project implementation
              │
              ▼
verification evidence in owning project
```

Do not copy an app's entire DOCKS tree into the root. Link the app and summarize only the cross-app contract that other agents need.