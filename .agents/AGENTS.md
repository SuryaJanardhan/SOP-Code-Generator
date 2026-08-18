# Workspace Workflow Rules (AG Kit Integration)

This repository adheres to the Antigravity Kit (AG Kit) agent engineering framework. All agent activities within this workspace are subject to the rules and protocols defined below.

## 1. AG Kit Architecture & Discovery

- **Rules Directory**: [.agents/rules](file:///home/surya/Desktop/SOP-Code-Generator/.agents/rules) (P0 Priority - binding on all operations)
- **Specialist Personas**: [.agents/agent](file:///home/surya/Desktop/SOP-Code-Generator/.agents/agent) (20 domain-tuned developer roles)
- **Context-Aware Skills**: [.agents/skills](file:///home/surya/Desktop/SOP-Code-Generator/.agents/skills) (modular knowledge packs)
- **Workflows**: [.agents/workflows](file:///home/surya/Desktop/SOP-Code-Generator/.agents/workflows) (slash commands for development lifecycle)
- **Persistent Memory**: [.agents/memory/MEMORY.md](file:///home/surya/Desktop/SOP-Code-Generator/.agents/memory/MEMORY.md) (session-persistent context and architectural decisions)
- **Native Safety Hook**: [.agents/hooks/validate-tool-call.mjs](file:///home/surya/Desktop/SOP-Code-Generator/.agents/hooks/validate-tool-call.mjs) (PreToolUse security gate blocking destructive root/disk operations)

## 2. Request Classification & Workflow Commands

1. **Plan & Architectural Requests**: Trigger `/plan` or `/brainstorm` flow to construct implementation plans before code execution.
2. **Complex Development Cycle**: Route through `/orchestrate` or `/coordinate` to manage multi-agent workflows.
3. **App Scaffolding & Creation**: Execute `/create` or route through `project-planner` using the `app-builder` skill.
4. **Testing & Diagnostics**: Utilize `/test` and validate environment integrity using the Antigravity Doctor (`.agents/hooks/antigravity-doctor.mjs`).

## 3. Formatting & Communication Rules

- Zero emojis in code, documentation, markdown files, and commit logs.
- Zero em-dashes across all text output and explanations.
- Natural, clear humanized tone in technical explanations.
- Mandatory file path links using the `file://` scheme for absolute paths.
