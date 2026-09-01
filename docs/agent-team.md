# Agent team

## Custom Agent Team

Building Mona's Project Pulse dashboard with GitHub Copilot CLI in a Codespace using four specialized agents:

### 1. **Orchestrator**
- **Model:** Claude Opus 4.7
- **Location:** `.github/agents/orchestrator.agent.md`
- **Responsibility:** Coordinates the Planner, Coder, and Designer agents by breaking down complex requests into tasks, managing dependencies, and verifying integrated results.

### 2. **Planner**
- **Model:** Claude Opus 4.7
- **Location:** `.github/agents/planner.agent.md`
- **Responsibility:** Creates implementation plans through thorough codebase research, documentation review, edge case identification, and deliverable planning without writing code.

### 3. **Coder**
- **Model:** GPT-5.5
- **Location:** `.github/agents/coder.agent.md`
- **Responsibility:** Implements code-oriented tasks with clear structure, explicit error handling, testable behavior, and support configuration (e.g., `.vscode/launch.json` for Project Pulse).

### 4. **Designer**
- **Model:** Gemini 3.1 Pro
- **Location:** `.github/agents/designer.agent.md`
- **Responsibility:** Handles UI/UX, accessibility, information architecture, interaction flow, and visual design with polished dashboards and responsive layouts.

## Orchestration

The Orchestrator agent coordinates all phases of development in GitHub Copilot CLI within a Codespace, ensuring parallel work on non-overlapping file scopes and sequential execution where dependencies require it. Each specialist stays within assigned file scopes and reports outcomes without staging or committing code—the learner controls all git operations.
