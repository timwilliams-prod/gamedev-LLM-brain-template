# Examples

Realistic examples of interacting with the documentation brain and creating skills.

---

## Example 1: Running Spec Sync

You've populated the feature registry with Notion IDs and want to generate local specs.

```
You:   /spec-sync

Brain: ## Spec Sync Report

       **Run Date**: 2026-04-01
       **External Source**: Connected (Notion)

       ### Feature Inventory (12 features in registry, 3 TBD placeholders skipped)

       | Feature         | Team    | Milestone | Spec    | Source  | Action Taken              |
       |-----------------|---------|-----------|---------|---------|---------------------------|
       | Governors        | Alpha   | M1        | Exists  | Fetched | Compared — no conflicts   |
       | Map System       | Alpha   | M1        | Created | Fetched | New spec from Notion      |
       | Combat Overhaul  | Bravo   | M1        | Created | Fetched | New spec from Notion      |
       | Gear System      | Charlie | M2        | Created | Not found | Stub spec created       |

       ### Gaps Found: 7
       - 3 specs created from Notion content
       - 1 stub spec created (no Notion content)
       - 4 open questions added to designer queue
       - 2 TBD sections flagged

       ### Conflicts (Need Resolution)
       - Combat Overhaul: Notion says "3 unit types" but existing design brief says "5 unit types"
         — assigned to Jamie (Bravo) as Q-012

       ### Recommended Next Steps
       1. Designers should run /designer-quiz to answer open questions
       2. Resolve the Combat Overhaul conflict with Jamie
       3. Add Notion ID for Gear System to the registry
```

**What happened**: The skill read the feature registry, fetched Notion pages for features that had IDs, created specs from the content, flagged a conflict it couldn't resolve, and added open questions to the designer queue.

---

## Example 2: Authoring a Feature Spec

A designer wants to document a new feature interactively.

```
You:   /doc-author

Brain: Who are you, and which feature are you working on?

You:   I'm Jamie, working on the Gear System.

Brain: Found you — Jamie, Design Lead for Bravo team.

       I see a stub spec exists at planning/features/gear_system.md (created by spec-sync,
       mostly TBDs). I'll work in **Expand mode** — we'll fill in the gaps.

       The Gear System is in the feature registry for Milestone 2.
       I also found 2 open questions in the designer queue for this feature.

       Let's start with validation. I see this feature could relate to BHQ-3
       ("Can our progression systems remain compelling long-term?").
       Which SHQs does the Gear System contribute to?

You:   It's mainly SHQ10 — does equipping gear feel meaningful and differentiated?
       And SHQ12 — do players want to collect gear beyond just stat increases?

Brain: Got it. For success criteria — how would you know the Gear System is working
       in a playtest? What would players be doing or saying?

You:   Players should be making deliberate gear choices based on playstyle, not just
       equipping the highest number. They should be able to articulate why they chose
       a specific loadout.

       [... interview continues through each section ...]

Brain: ## Doc Author Session Complete

       **Feature**: Gear System
       **Mode**: Expanded
       **File**: planning/features/gear_system.md

       ### What Was Covered
       - Validation goals (SHQ10, SHQ12)
       - Success criteria
       - Scope and core mechanics
       - In/out of scope

       ### Still TBD
       - Sprint estimates (needs engineering input)
       - Art asset requirements
       - Pre-conditions

       ### Designer Queue Items Addressed
       - Q-008: "What stats does gear affect?" — answered during Scope section
       - Q-009: "Is gear per-hero or shared?" — answered: per-hero

       ### Recommended Next Steps
       1. Review the spec file
       2. Run /queue-review to apply the answered questions
```

---

## Example 3: Risk Evaluation

Checking whether your plans align with your targets and capacity.

```
You:   /risk-evaluation

Brain: ## Risk Evaluation Report

       **Date**: 2026-04-01
       **Milestone**: M1 (ends Jun 23, 2026) — 5 sprints remaining

       ### Coverage Analysis

       | Target Feature         | Has Plan? | Has Spec? | Resourced? | Risk   |
       |------------------------|-----------|-----------|------------|--------|
       | Governors              | Yes       | Yes       | Yes        | Low    |
       | Map System             | Yes       | Yes       | Partial    | Medium |
       | Combat Overhaul        | Yes       | Yes       | No         | HIGH   |
       | [TBD multiplayer]      | No        | No        | No         | HIGH   |

       ### Resource Gaps

       | Discipline | Needed (sprints) | Available (sprints) | Gap    |
       |------------|------------------|---------------------|--------|
       | Engineering | 14              | 12                  | -2     |
       | Design      | 6               | 7                   | +1     |
       | Art         | 8               | 4                   | -4 !!  |

       ### Critical Risks
       1. **Art is severely under-resourced** — 4 sprint-slots needed but only 2
          available. Map System and Combat Overhaul both need art in the same window.
       2. **No multiplayer feature defined** — M1 is "Multiplayer & Meta" but no
          multiplayer feature has a spec, plan, or resources assigned.
       3. **Combat Overhaul has no engineer assigned** — spec exists but capacity.md
          shows no engineering allocation.

       ### Recommended Actions
       1. Define the multiplayer feature ASAP — it's a must-have with no plan
       2. Review art capacity — either scope down or add resources
       3. Assign engineering to Combat Overhaul or descope to nice-to-have
```

---

## Example 4: Designer Q&A Flow

The full pipeline from question generation to answer application.

```
Step 1: /spec-sync generates questions
        -> Q-015: "How many gear slots per hero?" (Jamie, Bravo) — MEDIUM
        -> Q-016: "What's the gear rarity tier system?" (Jamie, Bravo) — HIGH

Step 2: Designer runs /designer-quiz

You:    /designer-quiz
Brain:  Who are you?
You:    Jamie
Brain:  Hi Jamie! I have 2 open questions for you.

        Q-016 (HIGH): What's the gear rarity tier system for the Gear System?
You:    4 tiers: Common, Rare, Epic, Legendary. Each tier adds one stat modifier
        slot. Legendary also gets a unique passive effect.

Brain:  Q-015 (MEDIUM): How many gear slots per hero?
You:    6 slots: weapon, armor, helmet, boots, accessory x2.

Brain:  Saved your answers to planning/designer_queue/raw_input/jamie_20260401.md
        Run /queue-review to validate and apply these answers.

Step 3: Tim runs /queue-review

You:    /queue-review
Brain:  Found 1 raw input file: jamie_20260401.md (2 answers)

        Q-016: Gear rarity tiers — 4 tiers, Common through Legendary, stat modifier slots
        -> Would update: planning/features/gear_system.md (Scope > Core Mechanics)
        -> Looks good? [Y/n]

You:    Y

Brain:  Q-015: 6 gear slots per hero
        -> Would update: planning/features/gear_system.md (Scope > Core Mechanics)
        -> Looks good? [Y/n]

You:    Y

Brain:  ## Queue Review Complete
        - 2 answers validated and applied to planning/features/gear_system.md
        - Updated designer_queue.md: Q-015, Q-016 marked APPLIED
        - Log written to planning/designer_queue/output/applied_20260401.md
```

---

## Example 5: Creating a New Skill

You want a skill that generates a design review briefing for a specific feature.

```
You:   /new-skill

Brain: What problem does this skill solve?

You:   Before design reviews, I want a one-page briefing that shows scope overlaps
       with other features, dependency gaps, and open questions. Saves 30 min of
       prep per review.

Brain: Who will run it?

You:   Me (producer) or design leads, before a review meeting.

Brain: What's the expected output?

You:   A generated markdown file — one per feature, saved somewhere I can share it.

Brain: ## New Skill Assessment

       ### Proposed: /feature-review-prep
       **Problem**: Pre-review briefing for design meetings
       **Runner**: Producer or design leads
       **Output**: generated/design_briefs/[feature].md

       ### Architecture Check
       - Authority: PASS — reads planning files, writes to generated/
       - File Impact: PASS — output is disposable (generated/)
       - Safety: PASS — idempotent, regenerates each run
       - Maintenance: PASS — generated files, no manual upkeep
       - Overlap: PARTIAL — /risk-evaluation covers some of this, but at project
         level, not single-feature level. Different enough to justify a new skill.

       ### Recommendation: PROCEED

       Shall I design the workflow?

You:   Yes.

Brain: ### Workflow

       1. User specifies which feature to review
       2. Read the feature spec from planning/features/
       3. Read all OTHER feature specs — scan for scope overlap
       4. Read dependency_map.md — find dependency gaps
       5. Read designer_queue.md — find open questions for this feature
       6. Read capacity.md — check if the feature is resourced
       7. Generate briefing to generated/design_briefs/[feature]_brief.md

       ### File Interactions

       | File | Access | Why |
       |------|--------|-----|
       | planning/features/*.md | Read | Feature being reviewed + overlap scan |
       | planning/dependency_map.md | Read | Dependency gap analysis |
       | planning/designer_queue/designerQueue.md | Read | Open questions |
       | planning/capacity.md | Read | Resource check |
       | generated/design_briefs/ | Write | Output briefing |

       ### Guardrails
       - Does NOT modify any planning files
       - Does NOT resolve issues — only surfaces them
       - Regenerates the briefing each run (overwrites previous)

       Ready to write the skill file?

You:   Go for it.

Brain: Created .claude/commands/feature-review-prep.md
       Updated README.md with the new skill.
```

### Anatomy of a Skill File

Every skill follows this structure:

```markdown
# [Skill Name] Skill

[One-sentence description.]

> **Note**: [How this relates to other skills. What it does NOT do.]

---

## Project Structure

[Files this skill reads and writes, grouped by purpose]

---

## Your Task

### 1. Read Current State
[What to read first]

### 2. [Core Analysis / Gathering]
[Main workflow]

### 3. [Produce Output]
[What gets created or changed]

### 4. Summary
[Output format for the user]

---

## Rules

[Skill-specific guardrails — what to never do, how to handle edge cases]

---

## Notes

[Tips, related skills, when to run this]
```

---

## Tips for Effective Brain Usage

1. **Start conversations with context**: "I'm working on the Gear System for M2" gives the LLM a starting point to load relevant files.

2. **Use skills for repeatable work**: If you're doing the same analysis more than twice, it should be a skill.

3. **Let the brain surface conflicts**: The value isn't just storage — it's that skills can cross-reference files and find contradictions humans miss.

4. **Keep planning files honest**: If a feature slips or is descoped, update the files. A brain with stale data is worse than no brain.

5. **Run risk evaluation regularly**: It's the fastest way to catch gaps between what you promised and what you're building.
