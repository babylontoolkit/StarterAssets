---
description: Create the detailed technical plan for the specified feature spec file
tools: ['search/codebase', 'edit/editFiles', 'search', 'fetch']
---

Create a detailed technical implmentation plan for the specified feature spec and save in the _plans/<feature-name> folder. Always generate implmentation tasks or steps (prefer to call them tasks).

User input: $ARGUMENTS

---

## ⚠️ Required Reading Before Any Babylon Work

The Babylon Toolkit Agent Reference is the source of truth for the FRAMEWORK.
Any task involving Babylon, BabylonJS, or the Babylon Toolkit requires
fetching and reading the Agent Reference FIRST, before scaffolding or
writing any code:

  https://raw.githubusercontent.com/babylontoolkit/agent/main/reference.md

Treat it as the authority for conventions, API, and patterns. It is a router to deeper docs — follow the links relevant to the task:
- Modern ES6/ESM code → references/node-esm.md  (preferred style)
- Project install / npm / submodules → references/project-installer.md
- UI work → references/ui-design-system.md
- React → references/react-framework.md
- Scene components → references/scene-components.md
- Custom shaders → references/shader-materials.md
- Examples / playgrounds → references/training-reference.md

If the fetch fails, STOP and tell me — do not guess at the API.

---

## Planning mode — do not implement

This command runs in PLANNING MODE. Research read-only and produce ONLY the technical plan document. Do NOT implement the feature, edit any existing application/source files, or run build, test, or other terminal commands. The only file you may create is the plan markdown under `_plans/<feature-name>/`.

## Step 0. Confirm planning mode

A trustworthy plan requires a thorough, read-only investigation of the codebase before any plan is written.

- This prompt is intended to run as a read-only planning pass. If you have been invoked in an edit/agent mode that would modify source, begin your response with a short visible warning that you will only produce the plan document, then continue.
- Either way, you MUST still perform the comprehensive analysis in Step 1 with full rigor. Never skip it.

## Step 1. Comprehensive project analysis (REQUIRED before any plan)

Before writing a single implementation step, investigate the actual codebase read-only. This is mandatory — do NOT generate any plan content until this analysis is complete. Use codebase search and file reads to discover, not assume:

1. Read the referenced feature spec in full (from `_specs/` or the file named in `$ARGUMENTS`).
2. Map the project: top-level structure, entry points, how the app is built and run (build scripts, test runner, package manifests).
3. Identify the conventions actually used in this repo: naming, file/folder organization, state management, styling, error handling, testing patterns.
4. Find the closest existing feature(s) or modules to the one being planned and study how they are implemented — the plan should follow these patterns.
5. List the concrete integration points the feature will touch: files, modules, APIs, data models, routes, config.
6. Note relevant dependencies already available (and their versions) versus anything new that would be required.
7. Capture any constraints from `.github/copilot-instructions.md` and the feature spec.

If the spec or codebase is too ambiguous to analyze responsibly, stop and ask the user rather than guessing.

## Step 2. Write the plan

Only after Step 1 is complete, write the plan markdown to `_plans/<feature-name>/`. The document MUST open with a `## Codebase Analysis` section that summarizes the findings from Step 1 (cite the real files/modules you inspected) — this is the evidence that the analysis happened. A plan without a grounded analysis section is invalid; do not produce one.

Then write the implementation as an ordered checklist of discrete tasks. Use GitHub-style checkboxes so progress can be tracked directly in the file — one task per line, numbered T1, T2, T3 … in dependency order, each small enough to be implemented and verified on its own:

```markdown
## Tasks

- [ ] **T1** — <short task title>
  - Files: `path/one`, `path/two`
  - Details: <what to do>
  - Acceptance: <how to know it is done>
- [ ] **T2** — <short task title>
  - Files: `...`
  - Details: <...>
  - Acceptance: <...>
```

Finally, include this exact `## How to execute this plan` section verbatim in the document so the plan is self-describing no matter how it is later run:

```markdown
## How to execute this plan

Each task above is a checkbox. To implement:
- Run a single task with `/task #<this-file> T<n>`, run every remaining task in order with `/task #<this-file> ALL` (resumable — it skips tasks already checked), or implement the whole plan from a prompt like "implement the plan at #<this-file>".
- Work the tasks top to bottom unless a task notes a different dependency order.
- When a task is fully implemented and its **Acceptance** criteria are met, mark it complete by editing this file and changing that task's `- [ ]` to `- [x]`.
- Stop and report if a task cannot be completed. Do NOT check a box for partial, skipped, or unverified work.
```
