# Feature Registry

Last Updated: [date]

> **What this file is**: The authoritative mapping of features to source documents and local specs.
> `/spec-sync` reads this file to know which features need specs and where to pull content from.
> For milestone goals and priorities, see `planning/product_targets.md`.

---

## How to Use This File

- Add a row for each feature that should have a local spec in `planning/features/`
- **Milestone**: When this feature is planned for introduction
- **Source ID**: The page UUID from your external doc tool (Notion, Confluence, etc.)
- **Feature** column links to the local spec file in `planning/features/`

---

## Registry

| Feature | Team | Milestone | Source ID | Status |
|---------|------|-----------|----------|--------|
| [Feature A](features/feature_a.md) | [Team] | [M1] | | Needs Spec |

---

## Status Values

- **Has Spec** — Local spec exists and is maintained
- **Needs Spec** — No local spec yet
- **Stub Only** — Spec exists but is mostly TBDs
- **Archived** — Feature removed from scope
