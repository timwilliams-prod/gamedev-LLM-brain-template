# Onboard Apply Skill

You are applying a Brain Forge export to populate this project's documentation brain.

> **Note**: This skill reads the exported JSON from The Brain Forge onboarding game and populates all planning files. It also creates the custom `/roadmap` skill the user built during onboarding. Run this once after completing the onboarding game.

---

## Project Structure

### Input
- `onboarding/context/brain-forge-export.json` — The exported JSON from The Brain Forge game

### Files to Populate
- `project-charter.md` — Project identity, architecture (update the Purpose section and Change Log)
- `planning/product_targets.md` — Milestone goals, must-have features, success criteria
- `planning/capacity.md` — Team staffing by discipline
- `planning/validation_roadmap.md` — Winning hypotheses, BHQs, SHQs
- `planning/feature_registry.md` — Feature-to-team-to-milestone mapping
- `.claude/commands/roadmap.md` — The custom roadmap skill the user built

### Context (read for reference)
- `ONBOARDING.md` — Template structure and field descriptions
- `EXAMPLES.md` — Example content for reference

---

## Your Task

### 1. Read the Export

Read `onboarding/context/brain-forge-export.json`. Parse the JSON and understand what the user provided for each mission.

The export has this structure:
```json
{
  "missions": {
    "boot_sequence": { "projectName", "projectMission", "sprintCadence", "additionalContext" },
    "oracle_chamber": { "hypotheses", "questions", "attachedFiles": [...] },
    "war_table": { "milestones", "successCriteria", "attachedFiles": [...] },
    "guild_hall": { "teams", "attachedFiles": [...] },
    "armory": { "features", "externalLinks", "attachedFiles": [...] },
    "forge": { "skillProblem", "skillReads", "skillOutput", "skillCustomRules" }
  }
}
```

Each mission may have:
- **Natural language text** — the user's free-form descriptions
- **Attached files** — with `content` (text files) or `base64` (binary files)

For attached files that are binary (PDFs, etc.), write them to `onboarding/context/` first, then read them using your file reading capabilities.

### 2. Read Existing Templates

Read these files to understand the expected format:
- `planning/product_targets.md`
- `planning/capacity.md`
- `planning/validation_roadmap.md`
- `planning/feature_registry.md`

These contain the template structure with placeholder values. You'll replace the placeholders with real content.

### 3. Process Each Mission

#### Boot Sequence → `project-charter.md`
- Update the Purpose section with the project name and mission
- Add sprint cadence and any additional context
- Update the Change Log with today's date and "Initial brain population via Brain Forge"

#### Oracle's Chamber → `planning/validation_roadmap.md`
- Parse the user's hypotheses into Winning Hypotheses (WH1, WH2, etc.)
- Parse their questions into BHQs and SHQs
- Use your judgment to organize — the user wrote in natural language, you structure it
- If attached files contain validation/strategy content, cross-reference and incorporate
- Assign SHQ IDs sequentially (SHQ1, SHQ2, etc.)
- Set all statuses to "Not Started"
- Update "Next SHQ number" at the bottom

#### War Table → `planning/product_targets.md`
- Parse milestones into the Milestone Definitions table
- Create a section per milestone with must-have features, nice-to-haves, and success criteria
- Cross-reference with validation roadmap — if a milestone clearly maps to BHQs/SHQs, add Validation Alignment
- If attached files contain roadmap content, parse and incorporate
- Update the Change Log

#### Guild Hall → `planning/capacity.md`
- Parse teams into the Team Leadership Summary
- Organize people by discipline (Engineering, Design, Art, etc.)
- Include allocation percentages and milestone ranges where mentioned
- If attached files contain org/staffing data, parse and incorporate

#### Armory → `planning/feature_registry.md`
- Parse features into the Registry table
- Link each feature to its team and milestone
- Set Status to "Needs Spec" for all features (no specs exist yet)
- Create the feature file path as `features/[feature_name_snake_case].md`
- If external links were provided, add them to the Source ID column

#### The Forge → `.claude/commands/roadmap.md`
- Generate the roadmap skill file using the user's configuration:
  - Problem statement from `skillProblem`
  - Read files from `skillReads`
  - Output path from `skillOutput`
  - Custom rules from `skillCustomRules`
- Follow the standard skill template structure (see EXAMPLES.md "Anatomy of a Skill File")

### 4. Handle Ambiguity

The user wrote in natural language. When parsing:
- **Be generous with structure** — infer hierarchy where the user implied it
- **Ask before guessing** — if something is truly ambiguous (e.g., "is this a team name or a person's name?"), ask the user
- **Preserve original language** — for descriptions and goals, keep the user's phrasing rather than rewriting it
- **Flag gaps** — if a critical field is empty, note it but don't block on it

### 5. Summary

After populating all files, output:

```
## Brain Forge Applied

**Date**: [today]
**Project**: [project name]

### Files Updated
| File | Status | Notes |
|------|--------|-------|
| project-charter.md | Updated | [what changed] |
| product_targets.md | Populated | [X milestones, Y features] |
| capacity.md | Populated | [X teams, Y people] |
| validation_roadmap.md | Populated | [X hypotheses, Y SHQs] |
| feature_registry.md | Populated | [X features registered] |
| .claude/commands/roadmap.md | Created | Custom roadmap skill |

### What's Next
1. Review each file — especially validation_roadmap.md (your hypotheses drive everything)
2. Run `/spec-sync` to create feature spec stubs
3. Run your new `/roadmap` skill to generate your first roadmap
4. Run `/risk-evaluation` to check targets vs plans vs capacity

### Gaps Noted
- [any fields left empty or ambiguous]
```

---

## Rules

### Respect the Templates
- Keep the existing file structure and headers intact
- Replace placeholder content, don't restructure the files
- Preserve "How This File Is Used" sections and other meta-documentation

### Ask Before Overwriting
- If any planning file already has non-template content, show the user what exists and what you'd replace before making changes

### One Source of Truth
- Don't duplicate information across files
- Features go in the registry, not in product targets (product targets reference by name)
- Staffing goes in capacity, not in team plans
- SHQs go in validation roadmap, not in feature specs (feature specs reference by ID)

### Handle Attached Files Intelligently
- Text files: parse their content and incorporate relevant information
- PDFs: write to disk, read them, extract key information
- Spreadsheets: do your best to parse CSV content; for xlsx, note that the user should export as CSV
- If an attached file contains information that spans multiple brain files, distribute it correctly

---

## Notes

- This skill is designed to run once during initial setup
- Running it again will ask before overwriting any existing content
- After this skill completes, the brain is ready for ongoing use with other skills
- The user built their `/roadmap` skill during onboarding — encourage them to try it
