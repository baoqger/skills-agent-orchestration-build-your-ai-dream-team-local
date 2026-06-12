# Project Pulse implementation plan

## Summary

Build a lightweight static **Project Pulse** dashboard for contributors using plain frontend files in `app/`, backed by `app/project-data.json`, styled as a polished card-based UI, and runnable from VS Code through **Run Project Pulse Dashboard** in `.vscode/launch.json`. The repository currently has no `app/` directory, so the work must create the app structure from scratch while matching the exercise’s exact file names, field names, and launch behavior.

## Ordered implementation steps

1. **Confirm scope and create the file ownership split**
   - Lock the required outputs and exact strings from the brief and workflow checks.
   - Confirm that implementation will stay framework-free: static HTML, CSS, JSON, and minimal inline JavaScript in `app/index.html` if needed to load/render data.
   - Reserve file scopes so Designer and Coder do not overlap during the same phase.

   **File assignments**
   - No content changes required in this step.
   - Future ownership reservation:
     - `app/index.html` — Designer guidance first, then Coder implementation
     - `app/styles.css` — Designer guidance first, then Coder implementation
     - `app/project-data.json` — Coder
     - `.vscode/launch.json` — Coder

2. **Designer defines the dashboard experience**
   - Provide a clear layout and accessibility direction for the dashboard before HTML/CSS implementation.
   - Specify the information hierarchy: page title, project grid/list, card sections, owner/status/activity/priority display, and contributor-friendly summary treatment.
   - Define badge treatment, spacing, responsive behavior, contrast expectations, and required CSS hooks.

   **File assignments**
   - Advisory scope only for:
     - `app/index.html`
     - `app/styles.css`

3. **Coder creates the data source and preview configuration**
   - Create the `app/` directory if missing.
   - Author `app/project-data.json` with a top-level `projects` array and multiple project objects using the exact required keys:
     - `name`
     - `owner`
     - `status`
     - `recentActivity`
     - `priority`
   - Create `.vscode/launch.json` as strict JSON with no comments.
   - Configure the launch entry as **Run Project Pulse Dashboard**.
   - Ensure launch behavior serves from `${workspaceFolder}/app`, uses `python3 -m http.server 5500`, and opens `http://localhost:%s/index.html` rather than a directory root.

   **File assignments**
   - `app/project-data.json` — Coder
   - `.vscode/launch.json` — Coder

4. **Coder implements the dashboard markup and rendering**
   - Build `app/index.html` using the Designer’s structure guidance.
   - Use the exact visible title **Project Pulse**.
   - Reference `styles.css`.
   - Reference or load `project-data.json`.
   - Render visible project cards from the `projects` data.
   - Use the class name `project-card` for each project card.
   - Ensure the markup contains and displays `status`, `recentActivity`, and `priority`.

   **File assignments**
   - `app/index.html` — Coder

5. **Coder implements the polished styling**
   - Build `app/styles.css` to match the Designer’s direction.
   - Include `.dashboard` and `.project-card`.
   - Add polished card styling with readable spacing, responsive layout, `border-radius`, and `box-shadow`.
   - Make status/priority visually scannable without depending on color alone.

   **File assignments**
   - `app/styles.css` — Coder

6. **Integrate and validate the full dashboard flow**
   - Verify the dashboard loads from the launch configuration and opens `index.html`.
   - Verify the JSON parses and the page renders multiple cards.
   - Confirm the app does not rely on opening the file directly from disk; it should work through the local server flow expected by the exercise.

   **File assignments**
   - Validation across:
     - `app/index.html`
     - `app/styles.css`
     - `app/project-data.json`
     - `.vscode/launch.json`

## Designer responsibilities

- Define the visual direction for `app/index.html` and `app/styles.css`.
- Specify dashboard layout, card structure, hierarchy, spacing, responsive behavior, and accessibility expectations.
- Require deterministic styling hooks, especially `.dashboard` and `.project-card`.
- Define status badge and priority presentation so the first view clearly looks like a polished dashboard.
- Call out semantic/accessibility needs such as headings, readable contrast, and scan-friendly labels.
- Do **not** own `app/project-data.json` or `.vscode/launch.json`.

## Coder responsibilities

- Implement all repository changes.
- Create missing directories/files as needed.
- Own `app/project-data.json` and `.vscode/launch.json` end to end.
- Implement `app/index.html` and `app/styles.css` using the Designer’s guidance.
- Keep the solution lightweight and static, with no framework or build step.
- Preserve exact required strings, field names, class names, and launch behavior used by the exercise checks.
- Validate JSON syntax, launch JSON syntax, and the runnable preview flow.

## Dependencies between steps

- Step 1 must finish before delegation to avoid overlapping file scopes.
- Step 2 must happen before final HTML/CSS implementation so the visual direction is settled.
- Step 3 can begin after Step 1 and does not depend on Step 2.
- Step 4 depends on:
  - Step 2 for layout/styling direction
  - Step 3 for available project data
- Step 5 depends on Step 2 and should align with Step 4.
- Step 6 depends on Steps 3, 4, and 5 being complete.

## Work that can run in parallel

- **Parallel after Step 1**
  - Designer guidance for `app/index.html` and `app/styles.css`
  - Coder implementation of `app/project-data.json`
  - Coder implementation of `.vscode/launch.json`

## Work that must run sequentially

- File ownership split before delegation
- Designer guidance before final implementation of:
  - `app/index.html`
  - `app/styles.css`
- Data creation before final validation of rendered project cards
- Launch configuration validation after all app files exist

## Edge cases or risks to handle

- The repository currently has **no `app/` directory**, so the implementation must create it.
- `recentActivity` casing must stay exact in both JSON and HTML references.
- The exercise checks search for literal strings like `project-data.json`, `project-card`, `status`, `recentActivity`, and `priority`; avoid abstracting them away so far that those strings disappear from the files.
- `app/project-data.json` and `.vscode/launch.json` must both be valid JSON.
- `.vscode/launch.json` must be strict JSON with no comments.
- The dashboard must open `index.html`, not a server directory listing.
- Loading JSON from `file://` can fail in browsers, so the preview must use the local server launch flow.
- Status/priority styling should not rely on color alone.
- The brief mentions a contributor-friendly summary, but the required JSON schema does not include a `summary` field.

## Validation expectations

- `app/index.html` exists.
- `app/styles.css` exists.
- `app/project-data.json` exists.
- `.vscode/launch.json` exists.
- `app/index.html` includes:
  - `Project Pulse`
  - `styles.css`
  - `project-data.json`
  - `project-card`
  - `status`
  - `recentActivity`
  - `priority`
- `app/styles.css` includes:
  - `.dashboard`
  - `.project-card`
  - `border-radius`
  - `box-shadow`
- `app/project-data.json`:
  - parses as JSON
  - includes top-level `projects`
  - includes `name`, `owner`, `status`, `recentActivity`, and `priority`
- `.vscode/launch.json`:
  - parses as JSON
  - includes **Run Project Pulse Dashboard**
  - serves from the `app/` directory
  - uses `python3 -m http.server 5500`
  - opens `http://localhost:%s/index.html`
- Manual preview expectation:
  - Run **Run Project Pulse Dashboard**
  - Browser opens the dashboard frontend at `index.html`
  - Visible project cards render from the JSON data

## Open questions

- Should the contributor-friendly summary be a dedicated field in `app/project-data.json`, or should the dashboard derive/display summary text from the existing required fields? The exercise checks do not require a `summary` key, so the safest default is to keep the required schema unchanged unless Mona explicitly asks for an additional field.
