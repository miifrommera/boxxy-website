+++
title = "How It Works"
template = "docs.html"
+++

# How it Works

Boxxy is designed to be more than just a terminal with a chat window. It is built from the ground up to be a truly agentic environment that learns from you as you work.

Below is a breakdown of the core components that make Boxxy tick.

---

## Terminals & ClawAgents

When =BoxxyClaw= is enabled, every terminal instance is associated with a =BoxxyAgent=. An Agent is 
essentially a dedicated session from your chosen =LLM Model=. 

The core philosophy here is isolation: users typically spawn a new terminal to tackle a specific task. By assigning a unique agent to each terminal, we ensure that the context for that specific task remains isolated from your other ongoing work. 

To provide assistance, the agent tracks your terminal's activity—what commands were run in the past and what is currently executing. When necessary, it can also read directly from the terminal buffer. To optimize resource usage and reduce token consumption, Boxxy employs a paging system: the agent might initially request the last 50 lines of output. If that isn't sufficient to understand the context, it will request the preceding 50 lines, and so on.

However, it's very common to use multiple terminals simultaneously for a single, complex project. In these scenarios, you can explicitly ask an agent (by its name) to collaborate with another agent. When linked this way, the agents will share their context, allowing them to work together seamlessly across multiple terminal panes or windows.

---

## Self-Improving

Boxxy doesn't just forget everything when you close a tab. It is designed to learn your preferences, project structures, and "lessons learned" through a sophisticated, dual-layered memory system.

### A Mirror of Your Brain
While you work, Boxxy silently extracts facts—like your favorite editor or local environment specs—and mirrors them to a human-readable file at `~/.config/boxxy-terminal/boxxyclaw/MEMORY.md`. You are always in control of what the AI knows:

- **Verification**: New facts appear in  =Pending= until you move them to =Active.=
- **Manual Edits**: You can open the file and type your own facts directly into the agent's "brain" at any time.
- **Smart Scoping**: Memories can be =Global= (applying everywhere) or =Project-Specific= (only active when you are working in a specific folder).
- **Pinning (📌)**: Add a 📌 emoji to any memory in the file to ensure it is always injected into the agent's context, regardless of what you are doing.

---

---

## Terminal Buffer

Boxxy's agents aren't disconnected chatbots; they are deeply integrated into your terminal environment. Each terminal pane has its own dedicated agent, and you can see its unique name displayed directly in the terminal interface.

### Intelligent Paging
To provide the best assistance, agents have "eyes" on your terminal's activity. When necessary, they can read directly from the active terminal buffer to understand exactly what error you are seeing.

To optimize resource usage and radically reduce token consumption, Boxxy employs a smart **paging system**:
1. When you ask a question or an error occurs, the agent initially requests only a small snapshot of the last **50 lines** of output.
2. If that snapshot isn't sufficient to understand the context, the agent will dynamically request the *preceding* 50 lines.
3. It iterates backwards through the buffer history until it identifies the root cause of the issue.

This ensures the agent gets the precise context it needs without unnecessarily flooding the model with thousands of lines of irrelevant history.

---

## Resume Session 

Boxxy supports a stateless =Resume Session= model that allows you to restore any of your last 10 active sessions—or any session you've explicitly pinned—into any terminal pane.

### Stateless Resumption
Unlike other AI tools that rely on provider-side "Threads," Boxxy stores your entire conversation history locally in its SQLite database. When you use `/resume`:
- **Rehydration:** Boxxy loads the previous messages and "cleans" them of transient data (like old terminal snapshots).
- **Visual Logs:** Your entire sidebar history—diagnoses, proposed actions, and tool results—is re-rendered instantly.
- **Environment Sync:** Boxxy attempts to restore the terminal's =Working Directory= and re-activates any pending scheduled tasks.

### Switching Brains on the Fly
Because Boxxy's resumption is stateless, you can start a session with one model (e.g., "Gemini 3.1" ) and resume it with another (e.g., "Claude 4.6"). The new model simply reads the previous exchange and continues as if it were there all along.

### Persistent Analytics
Resuming a session also restores its =Cumulative Context Analytics=. Your sidebar will accurately reflect the total token spend for the entire life of that session, even if you've switched model providers or restarted the application.

---

## Toolbox

Think of the **Toolbox** as the agent's set of "superpowers." Instead of the AI simply guessing and typing commands into your terminal, it uses a library of highly reliable, structured tools to interact with your computer.

These tools are grouped into specialized categories:
- **File Operations**: Safely read, write, and list directories. The AI can even read specific line ranges to save time and tokens.
- **System Monitoring**: View active processes and hardware specs as clean, structured data.
- **Web & Network**: Fetch documentation or look up code examples directly from the web with built-in safety limits.
- **Clipboard Access**: Securely read from and write to your system clipboard.

### Safety First: The Approval Protocol
We believe in **Supervised Autonomy**. Boxxy never performs a "dangerous" action (like deleting a file, killing a process, or reading your clipboard) without your explicit permission. 

When an agent wants to use a sensitive tool, it will pause and present its plan to you in a popover. Only after you click **Approve** will the tool execute and return its results to the agent. This ensures you are always in control of what the AI is doing on your machine.

---

## Boxxy Agent

Because Boxxy is primarily distributed as a secure, sandboxed =Flatpak=, it faces a unique challenge: sandboxed applications usually cannot see or interact with the host operating system. This is great for security, but terrible for a terminal emulator that needs to run your local tools!

To solve this, Boxxy uses a hidden background process called the =Boxxy Agent=. 

When you open Boxxy, it securely spawns this agent *outside* of the sandbox directly on your host machine. The terminal UI and the Host Agent then talk to each other over a private, lightning-fast D-Bus connection. 

This bridge is what allows Boxxy to:
- Spawn real shells (like Bash or Fish) with full access to your system's files and programs.
- Accurately track your Current Working Directory (CWD) across tabs.
- Let the AI =ClawAgents= safely read files and execute commands on your actual machine, rather than being trapped inside the Flatpak bubble.

In short: Boxxy's UI stays safely sandboxed, while the Boxxy Agent does the heavy lifting on your host system.
