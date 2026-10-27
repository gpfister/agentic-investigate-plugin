# agentic-investigate-plugin

Autonomous multi-repository issue investigation plugin for [Google Antigravity](https://antigravity.google).

## Overview
`agentic-investigate-plugin` provides dedicated subagents and progressive-disclosure skills to diagnose root causes across repositories, interrogate users for missing context, produce structured `issue-assessment.md` artifacts, and hand off approved remediation plans to `@coding`.

## Features
- **Declarative Subagent (`@investigate`)**: Autonomous root cause investigator defined in [`agents/investigate/agent.md`](file:///Users/gpfister/Development/Projects/gpfister/agentic/agentic-investigate-plugin/agents/investigate/agent.md).
- **Progressive Skill (`investigate`)**: Diagnostic workflow and user clarification procedures in [`skills/investigate/SKILL.md`](file:///Users/gpfister/Development/Projects/gpfister/agentic/agentic-investigate-plugin/skills/investigate/SKILL.md).
- **Interactive Approval Gates**: Requires explicit user approval for `issue-assessment.md` via Antigravity's interactive modal before remediation begins.
- **Remediation Confirmation**: Asks user confirmation before handing off fixes to `@coding`.

## Installation & Activation

```bash
# Enable in Antigravity session:
agy plugin enable agentic-investigate-plugin
```

## Contributing
See [CONTRIBUTING.md](file:///Users/gpfister/Development/Projects/gpfister/agentic/agentic-investigate-plugin/CONTRIBUTING.md) for contribution guidelines and testing practices.

## License
This project is licensed under the [MIT License](file:///Users/gpfister/Development/Projects/gpfister/agentic/agentic-investigate-plugin/LICENSE).
