+++
title = "Agent Skills"
template = "docs.html"
+++

# Agentic Skills & Automations

Boxxy-Terminal uses an advanced **Agentic Skill System** (inspired by [standard Agentic Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)) that allows AI agents to "level up" their expertise on demand. Instead of overwhelming the agent with every possible instruction at once, Boxxy lets agents discover, load, and execute specialized domain knowledge and custom scripts only when they need them.

This adheres to modern **Agentic Standards**, treating agents not just as chatbots, but as autonomous systems capable of executing pre-defined workflows, utilizing local scripts, and strictly following domain-specific rules.

---

## What are Skills?

Skills are specialized instruction sets, workflow definitions, and tool configurations that target specific domains. Examples include:
- `linux-system`: Advanced OS insights, log analysis, and preference management.
- `linux-cleaner`: Safe execution of system-wide cleanup tasks (e.g., clearing package caches, orphaned dependencies, and stale logs).
- `docker-admin`: Specialized commands for managing containers, images, and networks safely.
- `network-analyzer`: Instructions for diagnosing connection issues, checking open ports, and managing firewall rules.

---

## How Activation Works

Activation is entirely **agent-driven**. You don't need to manually tell the agent which skill to use.

1.  **Discovery:** When you send a prompt, the agent evaluates its "Available Skills" list against your request.
2.  **Activation:** If it identifies a relevant skill (e.g., you ask to "deploy the app"), it uses the `activate_skill` tool.
3.  **Instruction Loading:** Boxxy instantly injects the full, detailed instructions, required scripts, and constraints for that skill into the agent's current reasoning loop.
4.  **Autonomous Execution:** The agent then follows those expert-level guidelines—executing any necessary shell commands, reading files, or invoking other tools—to complete the task autonomously and accurately.

---

## Viewing Available Skills

You can see which skills are currently available to your agents simply by asking the agent directly:

> **Example Prompt:** "Which specialized skills can you activate for this task?"

---

## Creating Custom Skills (Power Users)

Skills are defined as Markdown files with YAML frontmatter located in your configuration directory (`~/.config/boxxy-terminal/skills/`).

A basic skill file looks like this:

```markdown
---
name: "my-custom-skill"
description: "Expertise in my company's internal API and deployment"
---

# Instructions
When the user asks about our internal API or asks to deploy, always ensure you:
1. Check the `X-Internal-Header`.
2. Reference the documentation at `https://docs.internal.com`.
3. To deploy, run the script located at `./scripts/deploy.sh`.
```

### Hot Reloading
Once you save a new skill file, Boxxy's **Hot Reload** system detects the change instantly, making the skill available to all active agents without needing to restart the terminal. This allows for rapid iteration of your agentic workflows!
