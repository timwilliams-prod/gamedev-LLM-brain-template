# Onboarding Guide

How to populate a new documentation brain from scratch.

> **Time estimate**: Steps 1-4 take about an hour. Steps 5-8 are ongoing as your project evolves.
> You don't need everything filled in to start getting value — a partially populated brain is better than none.

---

## Prerequisites

- [ ] Claude Code (or another LLM tool that reads local files) installed
- [ ] Git repository initialized
- [ ] Read `project-charter.md` (understand the architecture before building)
- [ ] (Optional) Notion MCP configured for design doc syncing

---

## Step 1: Define Your Project

Before touching any files, answer these questions:

**Teams**: What are your teams/pods? Who leads each one? What discipline areas exist (engineering, design, art, etc.)?

**Milestones**: What are your upcoming milestones? What are their dates and goals? What milestones are already complete?

**Validation**: What are the big bets your product is making? What questions need answering to prove those bets?

**External tools**: Where do design docs live (Notion, Confluence, Google Docs)? Where are tasks tracked (ClickUp, Jira, Linear)?

Write these answers down — you'll use them in the next steps.

---

## Step 2: Create Product Targets

**File**: `planning/product_targets.md`

This is the **stable, leadership-authored** definition of what each milestone must achieve. It changes rarely.

### What to include:

```markdown
# Product Targets

Last Updated: [date]

> **What this file is**: The stable, leadership-authored definition of what each milestone must achieve.
> This is the benchmark that plans are measured against.

---

## Milestone Definitions

| # | Milestone | End Date | Sprints | Phase |
|---|-----------|----------|---------|-------|
| 1 | [Milestone Name] | [date] | [X] | [Iteration / Polish / Scale] |
| 2 | [Milestone Name] | [date] | [X] | [Phase] |

**Cadence**: [X]-week sprints
**Prior Milestones (complete)**: [list completed milestones]

---

## Milestone: [Name]

**Goal**: [One sentence — what this milestone proves or delivers]

### Must-Have Features

| Feature | Team | Why It's Required |
|---------|------|-------------------|
| [Feature Name] | [Team] | [Why this must ship in this milestone] |

### Nice-to-Have Features

| Feature | Team | Notes |
|---------|------|-------|
| [Feature Name] | [Team] | [Context] |

### Success Criteria

- [ ] [Observable, measurable outcome]
- [ ] [Another outcome]

### Validation Alignment

| Key SHQ | Question | Must Be Answered? |
|---------|----------|-------------------|
| [SHQ ID] | [Question text] | Yes / No |

---

## How This File Is Used

product_targets.md    "What must each milestone achieve?"
        | compared against
generated/roadmap.md  "What are we actually building?"
        | checked against
capacity.md           "Do we have the people?"
        | gaps surfaced by
/risk-evaluation      "Are we on track?"
```

### Tips:
- Start with your next 2-3 milestones — you don't need to plan everything
- "Why It's Required" is the most valuable column — it forces clarity on prioritization
- Leave `[TBD]` placeholders for features you know you need but haven't defined yet
- This file should feel stable; if you're updating it weekly, it's too detailed

---

## Step 3: Set Up Capacity

**File**: `planning/capacity.md`

Central staffing file — who's available, on which team, for which milestones.

### What to include:

```markdown
# Capacity

Last Updated: [date]

> **What this file is**: The single source of truth for team staffing across milestones.
> Skills use this to determine ownership, check resource availability, and assign questions.

---

## Team Leadership Summary

| Team | Lead | Design Lead | Eng Lead |
|------|------|-------------|----------|
| [Team A] | [Name] | [Name] | [Name] |
| [Team B] | [Name] | [Name] | [Name] |

---

## Staffing by Discipline

### Engineering

| Name | Team | Allocation | Milestones | Notes |
|------|------|------------|------------|-------|
| [Name] | [Team] | 100% | M1-M3 | |

### Design

| Name | Team | Allocation | Milestones | Notes |
|------|------|------------|------------|-------|
| [Name] | [Team] | 100% | M1-M3 | |

### Art

| Name | Team | Allocation | Milestones | Notes |
|------|------|------------|------------|-------|

[Add sections for each discipline in your project]

---

## Notes

- Allocation is percentage of time dedicated to this project
- Milestone ranges indicate when the person is expected to be available
- Part-time or shared resources should note which teams they split between
```

### Tips:
- Organize by discipline, not by team — this prevents the same person appearing in multiple team files
- The Team Leadership Summary is critical — skills use it to assign questions to the right person
- Update when people join, leave, or change teams

---

## Step 4: Create Validation Roadmap

**File**: `planning/validation_roadmap.md`

Your hypotheses and the questions you need to answer to prove (or disprove) them.

### What to include:

```markdown
# Validation Roadmap

Last Updated: [date]

> **What this file is**: The single source of truth for all validation hypotheses and questions.
> Other files reference questions by ID (e.g., SHQ7), never duplicate them.

---

## Winning Hypotheses

### WH1: [Hypothesis Name]
**We believe**: [Core bet about the product — e.g., "Players will find our combat system
uniquely satisfying on mobile"]

### WH2: [Hypothesis Name]
**We believe**: [Another core bet]

---

## Big Hypothesis Questions (BHQs)

### BHQ-1: [Question]
**Hypothesis**: WH1
**Status**: [Not Started | In Progress | Answered]
**Answer**: [If answered — what we learned]

---

## Sub-Hypothesis Questions (SHQs)

| ID | Question | Parent BHQ | Target Milestone | Status | Answer |
|----|----------|------------|-----------------|--------|--------|
| SHQ1 | [Specific testable question] | BHQ-1 | [Milestone] | [Status] | |
| SHQ2 | [Another question] | BHQ-1 | [Milestone] | [Status] | |

---

## How to Use

- Feature specs reference SHQs by ID in their "Why This Feature" section
- SHQs are cross-team — don't assign them to specific teams
- When an SHQ is answered, update the Status and Answer columns here
- Next SHQ number: [X]
```

### Tips:
- Start with 3-5 winning hypotheses — the big bets your product is making
- BHQs should be answerable within a few milestones
- SHQs should be answerable by building and testing specific features
- Don't force every feature to map to an SHQ — some work is just necessary infrastructure

---

## Step 5: Register Features

**File**: `planning/feature_registry.md`

Maps features to their external source documents and local spec files.

### What to include:

```markdown
# Feature Registry

Last Updated: [date]

> **What this file is**: The authoritative mapping of features to source documents and local specs.
> `/spec-sync` reads this file to know which features need specs.

---

## Registry

| Feature | Team | Milestone | Source ID | Status |
|---------|------|-----------|----------|--------|
| [Feature A](features/feature_a.md) | [Team] | [Milestone] | [external-doc-id] | Needs Spec |
| [Feature B](features/feature_b.md) | [Team] | [Milestone] | | Has Spec |

## Status Values

- **Has Spec** — Local spec exists and is maintained
- **Needs Spec** — No local spec yet
- **Stub Only** — Spec exists but is mostly TBDs
- **Archived** — Feature removed from scope
```

### Tips:
- Feature names in the first column should be hyperlinks to the spec file path (relative)
- Source ID is the page UUID from your external tool (Notion, Confluence, etc.)
- Include features from completed milestones — they're useful reference
- Not every external doc needs a registry entry — only features that warrant a local spec

---

## Step 6: Write Your First Feature Spec

**File**: `planning/features/[feature_name].md`

Pick your most well-understood feature and write the first spec. This becomes your living template.

### Feature Spec Template:

```markdown
# Feature: [Name]

- **Last Updated**: [date]
- **Status**: [NOT STARTED | IN PROGRESS | COMPLETE]
- **Team**: [Team name]
- **Design Owner**: [from capacity.md]
- **Task Tracker**: [Epic link]
- **Source Doc**: [External doc link]

---

## Why This Feature

### Validation Goals

| SHQ | Question | Status |
|-----|----------|--------|
| [ID] | [Question text from validation_roadmap.md] | [Status] |

**Parent BHQ**: [BHQ ID and name]

**What [Feature] Must Prove**: [Why this feature matters for your hypotheses]

### Success Criteria

- [Observable, testable outcomes]
- [Focus on user behavior, not implementation]

---

## Scope

[High-level description — what the feature does and why it exists. 2-3 paragraphs.]

### Core Mechanics

- **[Mechanic]**: [Description]

### In Scope

- [Specific deliverables]

### Out of Scope

- [What this explicitly does NOT cover]

---

## Estimate & Approach

**Total Estimate**: [X sprints (Y weeks)]

### Disciplines Required

| Discipline | Needed | Sprints | Notes |
|-----------|--------|---------|-------|
| Engineering | [Yes/No] | [X] | [What they build] |
| Design | [Yes/No] | [X] | [What they define] |
| Art | [Yes/No] | [X] | [What assets are needed] |

### Implementation Flow

Sprint 1: [Phase name]
  - [What gets built]
  - [Needs: prerequisites]

Sprint 2: [Phase name]
  - [What gets built]

### Pre-Conditions

- [ ] [What must be true before work starts]

---

## Dependencies

| Dependency | Direction | Details |
|-----------|-----------|---------|
| [System] | [Depends on / Depended on by / Bidirectional] | [How they connect] |

---

## Risks

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| [What could go wrong] | [H/M/L] | [H/M/L] | [Plan] |

---

## Open Questions

- [ ] [Unresolved design decisions]
- [x] ~~[Resolved — answer here]~~

---

## References

- Source Doc: [link]
- Task Tracker Epic: [link]
- Related: planning/teams/[team]_plan.md, planning/validation_roadmap.md
```

### Tips:
- Validation goals come FIRST — if you can't articulate why a feature matters, reconsider it
- Mark unknowns as `[TBD]` rather than guessing — these become designer queue items
- Open Questions are valuable — they're the work that's left to do, not a sign of failure
- Your first spec becomes the template others follow, so invest in getting the structure right

---

## Step 7: Create Team Plans

**File**: `planning/teams/[team]_plan.md` (one per team)

Lightweight plans per team — priorities and validation focus, NOT detailed specs.

```markdown
# [Team Name] Plan

Last Updated: [date]

## Team Mission
[One sentence — what this team is responsible for]

## Current Milestone: [Name]

### Validation Focus
- Contributes to: [BHQ IDs]
- Key SHQs: [SHQ IDs with brief descriptions]

### Feature Priorities

| Priority | Feature | Status | Notes |
|----------|---------|--------|-------|
| 1 | [Feature](../features/feature.md) | In Progress | |
| 2 | [Feature](../features/feature.md) | Not Started | Blocked by [X] |

### Risks & Flags
- [Team-level risks not covered in individual feature specs]
```

### Tips:
- Keep these lightweight — feature detail lives in feature specs, not here
- "Contributes to" BHQs, not "owns" — validation questions are cross-team
- Update these per milestone, not per sprint

---

## Step 8: Connect External Sources (Optional)

If your design docs live in Notion (or another tool with MCP support):

1. **Set up the MCP connection** — Configure the Notion MCP server in your Claude Code settings
2. **Find your database ID** — Open your documentation database in Notion, copy the URL, extract the UUID
3. **Populate the feature registry** — Add Notion page IDs to the Source ID column
4. **Run `/spec-sync`** — It will fetch Notion content and create/update local specs

If your external tool doesn't have MCP support:
- Export docs as markdown or PDF and place them in `reference/`
- Create specs manually using `/doc-author` or by copying the template
- The brain works fine without external syncing — it just means more manual spec authoring

---

## What's Next

Once the core files are populated:

1. **Run `/risk-evaluation`** to compare targets vs plans vs capacity
2. **Run `/spec-sync`** to check coverage and populate the designer queue
3. **Have designers run `/designer-quiz`** to answer open questions
4. **Run `/validation-review`** before milestone boundaries to check hypothesis progress
5. **Create new skills** as your workflow demands (see `EXAMPLES.md` for guidance)

---

## Common Mistakes

| Mistake | Why It's Bad | Instead |
|---------|-------------|---------|
| Duplicating feature lists across files | Creates conflicting sources of truth | Feature registry is the list; other files reference it |
| Putting sprint-level detail in the brain | Duplicates task tracker, goes stale fast | Keep sprint detail in ClickUp/Jira; brain tracks strategy |
| Writing specs without validation goals | Features ship without proving anything | Always start with "Why This Feature" |
| Creating files nobody reads | Clutters the brain, wastes maintenance effort | Every file should be read by at least one skill or person |
| Auto-overwriting planning files | Destroys human-authored decisions | Skills always ask before modifying planning/ |
