---
description: Create a feature spec file and branch from a short idea
argument-hint: "[Short feature description]"
allowed-tools: Read, Grep, Glob, Write, WebFetch(domain:raw.githubusercontent.com), Bash(git switch:*)
---

You are helping to spin up a new feature spec for this application, from a short idea provided in the user input below. Always adhere to any rules or requirements set out in any CLAUDE.md files when responding.

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

This command runs in PLANNING MODE. Research read-only and produce ONLY the spec document and its git branch. Do NOT implement the feature, edit or create any application/source files, or run build, test, or other shell commands. The single file you may write is the spec markdown described below. If you would normally enter the host's plan mode, prefer it; never fall through to implementation.

## High level behavior

Your job will be to turn the user input above into:

- A human friendly feature title in kebab-case (e.g. new-heist-form)
- A safe git branch name not already taken (e.g. project/feature/new-heist-form)
- A detailed markdown spec file under the _specs/ directory

Then save the spec file to disk and print a short summary of what you did.

## Step 1. Check the current branch

Check the current Git branch, and abort this entire process if there are any uncommitted, unstaged, or untracked files in the working directory. Tell the user to commit or stash changes before proceeding, and DO NOT GO ANY FURTHER.

## Step 2. Parse the arguments

From `$ARGUMENTS`, extract:

1. `feature_title`  
   - A short, human readable title in Title Case.  
   - Example: "Card Component for Dashboard Stats".

2. `feature_slug`  
   - A git safe slug.  
   - Rules:  
     - Lowercase 
     - Kebab-case 
     - Only `a-z`, `0-9` and `-`  
     - Replace spaces and punctuation with `-`  
     - Collapse multiple `-` into one  
     - Trim `-` from start and end  
     - Maximum length 40 characters  
   - Example: `card-component` or `card-component-dashboard`.

3. `branch_name`  
   - Format: `project/feature/<feature_slug>`  
   - Example: `project/feature/card-component`.

If you cannot infer a sensible `feature_title` and `feature_slug`, ask the user to clarify instead of guessing.

## Step 2.5 Apply the project design system (DESIGN.md)

This project's design system is defined in the `DESIGN.md` file at the repository root. `DESIGN.md` is the single source of truth for all design decisions — do NOT pull styling from Figma, external links, or invent your own values. (Figma may be used in a separate process to author `DESIGN.md`, but specs reference `DESIGN.md`, never Figma directly.)

If the feature has any UI or visual surface:

1. Read `DESIGN.md`. If it is missing or has no real design system yet, record this note in the spec and continue: `"No DESIGN.md design system found — follow the existing UI conventions already in the codebase."`
2. Identify the parts of the design system relevant to this feature and cite them, by name, in the spec — for example:
   - Layout and spacing scale
   - Typography tokens (font family, size, weight)
   - Color tokens and semantic roles (primary, surface, border, error, etc.)
   - Border radius, shadows, elevation
   - Shared components, icons, buttons and inputs the feature should reuse
3. Summarise these as 3 to 8 concise bullet points that reference the `DESIGN.md` tokens and components by name, so implementation stays consistent with the system.

If the feature is purely non-visual (no UI), note that no design system tokens apply and continue.

## Step 3. Switch to a new Git branch

Before making any content, switch to a new Git branch using the `branch_name` derived from the `$ARGUMENTS`. If the branch name is already taken, then append a version number to it: e.g. `project/feature/card-component-01`

## Step 4. Draft the spec content

Create a markdown spec document that Plan mode can use directly and save it in the _specs folder as `<feature_slug>_spec.md`. Use the exact structure as defined in the spec template file @SPEC.md located at the project root. Do not add technical implementation details such as code examples.

## Step 5. Final output to the user

After the file is saved, respond to the user with a short summary in this exact format:

Branch: <branch_name>
Spec file: _specs/<feature_slug>_spec.md
Title: <feature_title>

Do not repeat the full spec in the chat output unless the user explicitly asks to see it. The main goal is to save the spec file and report where it lives and what branch name to use.
