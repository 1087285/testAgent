# Agent Migration Design (No-Execution Plan)

## Purpose
This document defines how to convert the current documentation-style assets in `agent/`, `prompt/`, and `skills/` into runnable Copilot customization assets.

Scope in this document:
- Folder layout and naming conventions
- Mapping rules from current files to target files
- Minimum metadata to add
- Validation checklist before first execution

Out of scope in this document:
- Running any agent
- Publishing releases
- Automatic execution orchestration

## Current State
Current assets are organized as:
- `agent/*.md` (stage behavior definitions)
- `prompt/*.md` (task instructions with placeholders)
- `skills/*.md` (quality/process criteria)

These are useful as source materials, but are not yet in guaranteed runnable shape for Copilot customization discovery.

## Target Layout
Use a Copilot-oriented structure under `.github/`:

```text
.github/
  copilot-instructions.md
  agents/
    01_requirements.agent.md
    02_basic_design.agent.md
    03_detailed_design.agent.md
    04_implementation.agent.md
    05_unit_test.agent.md
    06_integration_test.agent.md
    07_system_test.agent.md
    08_release.agent.md
    09_bug_analysis.agent.md
  prompts/
    01_requirements.prompt.md
    02_basic_design.prompt.md
    03_detailed_design.prompt.md
    04_implementation.prompt.md
    05_unit_test.prompt.md
    06_integration_test.prompt.md
    07_system_test.prompt.md
    08_release.prompt.md
    09_bug_analysis.prompt.md
  skills/
    01_requirements/
      SKILL.md
    02_basic_design/
      SKILL.md
    03_detailed_design/
      SKILL.md
    04_implementation/
      SKILL.md
    05_unit_test/
      SKILL.md
    06_integration_test/
      SKILL.md
    07_system_test/
      SKILL.md
    08_release/
      SKILL.md
    09_bug_analysis/
      SKILL.md
```

## Mapping Rules
### Agents
Map each stage file in `agent/` to `.github/agents/*.agent.md` one-to-one.

Required additions per target agent file:
- YAML frontmatter:
  - `name`
  - `description`
  - `argument-hint`
  - optional `tools` restriction
- Explicit references to:
  - stage prompt file (`.github/prompts/...`)
  - stage skill file (`.github/skills/<stage>/SKILL.md`)

### Prompts
Map each stage file in `prompt/` to `.github/prompts/*.prompt.md` one-to-one.

Required normalization:
- Keep placeholder sections (`{{...}}`) but standardize variable names per stage
- Keep output path naming fixed (`project/document/XX_*.md` fixed forms already normalized)
- Remove wrapper artifacts (already resolved for stage 09)

### Skills
Map each stage file in `skills/` to `.github/skills/<stage>/SKILL.md`.

Required normalization:
- Preserve process/quality logic
- Ensure each SKILL has:
  - purpose
  - inputs
  - step-by-step method
  - quality checks

## Stage Mapping Table
| Stage | Source Agent | Source Prompt | Source Skill | Target Agent | Target Prompt | Target Skill |
|---|---|---|---|---|---|---|
| 01 | `agent/01_requirements_agent.md` | `prompt/01_requirements_prompt.md` | `skills/01_requirements_skill.md` | `.github/agents/01_requirements.agent.md` | `.github/prompts/01_requirements.prompt.md` | `.github/skills/01_requirements/SKILL.md` |
| 02 | `agent/02_basic_design_agent.md` | `prompt/02_basic_design_prompt.md` | `skills/02_basic_design_skill.md` | `.github/agents/02_basic_design.agent.md` | `.github/prompts/02_basic_design.prompt.md` | `.github/skills/02_basic_design/SKILL.md` |
| 03 | `agent/03_detailed_design_agent.md` | `prompt/03_detailed_design_prompt.md` | `skills/03_detailed_design_skill.md` | `.github/agents/03_detailed_design.agent.md` | `.github/prompts/03_detailed_design.prompt.md` | `.github/skills/03_detailed_design/SKILL.md` |
| 04 | `agent/04_implementation_agent.md` | `prompt/04_implementation_prompt.md` | `skills/04_implementation_skill.md` | `.github/agents/04_implementation.agent.md` | `.github/prompts/04_implementation.prompt.md` | `.github/skills/04_implementation/SKILL.md` |
| 05 | `agent/05_unit_test_agent.md` | `prompt/05_unit_test_prompt.md` | `skills/05_unit_test_skill.md` | `.github/agents/05_unit_test.agent.md` | `.github/prompts/05_unit_test.prompt.md` | `.github/skills/05_unit_test/SKILL.md` |
| 06 | `agent/06_integration_test_agent.md` | `prompt/06_integration_test_prompt.md` | `skills/06_integration_test_skill.md` | `.github/agents/06_integration_test.agent.md` | `.github/prompts/06_integration_test.prompt.md` | `.github/skills/06_integration_test/SKILL.md` |
| 07 | `agent/07_system_test_agent.md` | `prompt/07_system_test_prompt.md` | `skills/07_system_test_skill.md` | `.github/agents/07_system_test.agent.md` | `.github/prompts/07_system_test.prompt.md` | `.github/skills/07_system_test/SKILL.md` |
| 08 | `agent/08_release_agent.md` | `prompt/08_release_prompt.md` | `skills/08_release_skill.md` | `.github/agents/08_release.agent.md` | `.github/prompts/08_release.prompt.md` | `.github/skills/08_release/SKILL.md` |
| 09 | `agent/09_bug_analysis_agent.md` | `prompt/09_bug_analysis_prompt.md` | `skills/09_bug_analysis_skill.md` | `.github/agents/09_bug_analysis.agent.md` | `.github/prompts/09_bug_analysis.prompt.md` | `.github/skills/09_bug_analysis/SKILL.md` |

## Shared Review Policy Handling
Current shared policy file:
- `agent/_common_review_policy.md`

Target handling:
- Option A: keep as source and copy into `.github/agents/_common_review_policy.md`
- Option B: move global review rules into `.github/copilot-instructions.md`

Recommended:
- Keep brief global rules in `.github/copilot-instructions.md`
- Keep stage-specific approval gates in each `.agent.md`

## Minimum Agent Frontmatter Template
Use this pattern in each `.agent.md`:

```yaml
---
name: <stage_id_name>
description: <one-line role summary>
argument-hint: <what user should provide>
# tools: ['read', 'edit', 'search', 'execute']
---
```

## Validation Checklist (Before First Run)
1. Stage file naming alignment is complete (01..09 across agents/prompts/skills).
2. Every agent references the same-number prompt and skill.
3. Document output paths are fixed names (no wildcard placeholders in paths).
4. No fenced-wrapper artifacts in prompt files.
5. Approval gates remain in release and bug-analysis stages.
6. Shared review rules are referenced from one source of truth.

## Rollout Strategy (Safe)
1. Create target files under `.github/` without deleting current source folders.
2. Dry review only: verify references and placeholders manually.
3. Run one stage pilot (01) after approval.
4. Expand to 02..09 incrementally.
5. After stabilization, archive or remove old `agent/`, `prompt/`, `skills/` folders.

## Notes
- This document is a design artifact only.
- No execution action is included.
