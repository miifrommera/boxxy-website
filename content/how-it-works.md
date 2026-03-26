+++
title = "How It Works"
template = "docs.html"
+++

# How it Works

Work in progress...

---

## Terminals & Agents

When =BoxxyClaw= is enabled, every terminal instance is associated with a =BoxxyAgent=. An Agent is 
essentially a dedicated session from your chosen =LLM Model=. 

The core philosophy here is isolation: users typically spawn a new terminal to tackle a specific task. By assigning a unique agent to each terminal, we ensure that the context for that specific task remains isolated from your other ongoing work. 

To provide assistance, the agent tracks your terminal's activity—what commands were run in the past and what is currently executing. When necessary, it can also read directly from the terminal buffer. To optimize resource usage and reduce token consumption, Boxxy employs a paging system: the agent might initially request the last 100 lines of output. If that isn't sufficient to understand the context, it will request the preceding 100 lines, and so on.

However, it's very common to use multiple terminals simultaneously for a single, complex project. In these scenarios, you can explicitly ask an agent (by its name) to collaborate with another agent. When linked this way, the agents will share their context, allowing them to work together seamlessly across multiple terminal panes or windows.

---

## Self-Improving



---

## Toolbox

---

## Boxxy Agent
