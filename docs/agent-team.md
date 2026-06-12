# Project Pulse agent team

The custom agent team for Mona's **Project Pulse** dashboard lives in `.github/agents/`. The **Orchestrator** coordinates the work, the **Planner** turns the request into phases and file ownership, the **Designer** shapes the dashboard experience, and the **Coder** implements the assigned files.

| Agent | Model | Responsibility | Source file |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 4.7 | Coordinates the request, breaks the work into phases, delegates to specialist agents, keeps file scopes separate, and reports the final outcome. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 | Researches the repository and requirements, identifies dependencies and risks, and produces an implementation plan with steps, sequencing, parallel work, and validation expectations. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.1 Pro | Handles UI/UX, accessibility, layout, visual clarity, and responsive dashboard styling for Project Pulse. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 | Implements code changes in the assigned files, keeps behavior explicit and testable, and can create support files such as `.vscode/launch.json` for Project Pulse. | `.github/agents/coder.agent.md` |

For Project Pulse, the team should work in a clear handoff flow. The Orchestrator first asks the Planner for a step-by-step plan, then uses that plan to assign non-overlapping file scopes. The Designer can define the dashboard structure and styling direction for files such as `app/index.html` and `app/styles.css`, while the Coder implements the static app files and launch configuration details needed to open `app/index.html` from the `app/` directory. The Orchestrator then checks that the combined result fits together as one runnable dashboard and gives Mona a clean final handoff.
