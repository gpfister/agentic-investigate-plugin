---
name: investigate-catalog
description: Architecture overview and catalog for the agentic-investigate-plugin subagents.
enable_write_tools: false
enable_subagent_tools: false
enable_mcp_tools: false
tools:
  - read_file
  - list_dir
---

# Issue Investigation Subagents & Architecture (`agents/agent.md`)

This document defines the subagent architecture and catalog for the **`agentic-investigate-plugin`**.

---

## 1. Architectural Overview

The `agentic-investigate-plugin` provides autonomous root cause analysis, user interrogation, solution formulation, and remediation handoffs across multi-repository workspaces. It isolates bug hunting and defect diagnostics into a specialized subagent (`@investigate`), ensuring code is never modified without evidence-backed root cause analysis and explicit human approval.

### Directory Structure
```text
agents/
├── agent.md                    # Master subagent guide (this file)
└── investigate/                # Standalone Issue Investigator (@investigate)
    └── agent.md
```

---

## 2. Subagent Catalog

| Agent Handle | Directory | `enable_write_tools` | `enable_subagent_tools` | `enable_mcp_tools` | Allowed Tools | Description |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- |
| **`@investigate`** | [`agents/investigate/`](file:///Users/gpfister/Development/Projects/gpfister/agentic/agentic-investigate-plugin/agents/investigate/) | `True` | `True` | `True` | `read_file`, `list_dir`, `search_dir`, `run_command`, `search_web`, `ask_question`, `write_file`, `invoke_subagent`, `send_message`, `manage_subagents` | Standalone multi-repository root cause investigator producing `issue-assessment.md` artifacts, grilling users when needed, and handing off approved fixes to `@coding`. |

---

## 3. Investigation & Remediation Protocol

```text
Multi-Repo Search ──> Solution Found? ──(No)──> Grill User (ask_question) ──┐
                            │                                                │
                          (Yes) <────────────────────────────────────────────┘
                            ▼
                Write issue-assessment.md (RequestFeedback=True)
                            │
                     [Approved by User]
                            ▼
            Ask Correction Confirmation (Yes / No)
                     │                    │
                   (Yes)                 (No)
                     ▼                    ▼
              Invoke @coding            Stop
```

### Mandatory Artifact Approval Gate
- **Location**: `<appDataDir>/brain/<conversation-id>/issue-assessment.md`
- **Metadata**: `ArtifactMetadata={"RequestFeedback": True, "UserFacing": True}`
- **Sole & Final Tool Call Rule**: `write_file` must be the sole and final tool call of that turn to trigger the interactive Approve / Reject buttons in Antigravity.
