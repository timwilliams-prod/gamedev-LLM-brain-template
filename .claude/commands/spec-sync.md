# Spec Sync Skill

You are synchronizing the project's **feature spec files** (`planning/features/*.md`) with the feature registry and external design documents.

> **Note**: This skill checks every feature in the registry, ensures it has a local spec, and populates specs with content from external sources. Unresolvable conflicts go to the designer queue.

---

## Project Structure

### Authoritative Sources
- `planning/feature_registry.md` — Feature list + source ID mapping. This drives the sync.
- `planning/product_targets.md` — Milestone goals, "why it's required" context.
- **External design docs** (via MCP if available) — Design detail from your team's working docs.

### Spec Files (output)
- `planning/features/*.md` — Feature specs

### Designer Queue (conflict/gap tracking)
- `planning/designer_queue/designer_queue.md` — Open questions and conflicts

### Context
- `planning/capacity.md` — Designer ownership (Team Leadership Summary)
- `planning/teams/*_plan.md` — Team plans
- `planning/validation_roadmap.md` — SHQ/BHQ references

---

## Your Task

### 1. Read Current State

Read these files:
1. `planning/feature_registry.md` — The feature list driving this sync
2. All files in `planning/features/*.md` — Which specs already exist
3. `planning/product_targets.md` — Milestone context
4. `planning/capacity.md` — Who owns what
5. `planning/designer_queue/designer_queue.md` — Existing open questions
6. `planning/validation_roadmap.md` — SHQ/BHQ references

### 2. Build Feature Inventory

Parse `planning/feature_registry.md`. For each row, capture:

| Field | Source |
|-------|--------|
| Feature name | Registry (link text) |
| Team | Registry |
| Milestone | Registry |
| Source ID | Registry (may be blank) |
| Expected spec file | Registry (link target) |
| Spec exists? | Check `planning/features/` |
| Why it's required | `product_targets.md` |

### 3. Fetch from External Source

For each feature with a **Source ID**:

1. Fetch the page using MCP (if available)
2. Extract: title, status, scope, mechanics, open questions
3. If no Source ID: try a keyword search as fallback
4. If MCP not connected: skip, note in output, proceed with local files only

### 4. Create Missing Specs

For features without a spec file:

- **If external content fetched**: Create spec from that content, mapped to the template
- **If no external content**: Create a stub spec with TBD sections

Always populate:
- Feature name, team, milestone (from registry)
- Validation goals (from validation_roadmap.md / product_targets.md)
- Design owner (from capacity.md Team Leadership Summary)

### 5. Compare Existing Specs Against External Source

For features with both a spec AND fetched content:

- **Conflicts** (can't auto-resolve): Send to designer queue
- **Updates** (new content for TBD sections): Present to user for approval
- **Stale content**: Flag for review

**Never auto-overwrite existing spec content.**

### 6. Populate Designer Queue

For every unresolvable gap or conflict, add to `designer_queue.md`:
- Assign to the Design Lead for the feature's team (from capacity.md)
- Priority: HIGH for conflicts and must-have gaps, MEDIUM for TBDs, LOW for nice-to-have gaps
- Find highest existing Q-XXX ID and increment

### 7. Update Registry Status

Update the Status column in `feature_registry.md`:
- `Has Spec` if spec now has substantive content
- `Stub Only` if spec is mostly TBDs
- `Needs Spec` if still no spec

### 8. Output Summary

```
## Spec Sync Report

**Run Date**: [today]
**External Source**: Connected / Not Connected

### Feature Inventory ([X] features)

| Feature | Team | Milestone | Spec | Source | Action Taken |
|---------|------|-----------|------|--------|-------------|

### Gaps Found: [X]
### Designer Queue Updated
### Conflicts (Need Resolution)
### Recommended Next Steps
```

---

## Rules

### Never Auto-Overwrite Existing Specs
- Present conflicts and let the user decide

### Registry Is the Driver
- Only process features in `planning/feature_registry.md`
- Don't auto-add features to the registry

### Preserve Validation Goals
- Always populate "Why This Feature", even in stubs

### Keep IDs Stable
- Question IDs (Q-XXX) are sequential and never reused

---

## Notes

- Safe to run repeatedly — additive, not destructive
- Run before `/risk-evaluation` to ensure spec coverage
- After designers answer questions, run `/queue-review` to apply answers
