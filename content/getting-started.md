+++
title = "Getting Started"
template = "docs.html"
+++

# Getting Started

Boxxy is an agentic terminal. You can certainly use it without the AI features...
<br />but then again, where's the fun in that? 😅

Press `Control + Shift + p` to open the Command Palette and start exploring!

---

## Shell Integration

Boxxy respects your environment. It relies on your existing shell and avoids injecting features to modify it. For the best experience, it is **strongly** recommended to use a modern, Rust-based shell like [Fish](https://github.com/fish-shell/fish-shell). 

To enable terminal hyperlinks =(OSC 8)=, ensure that CLI tools like `ls` or `eza` are configured to use the `--hyperlink=auto` flag.

---

## Model Selection

Navigate to =Preferences= -> =APIs= and enter the connection strings for your preferred LLM providers. Then, open =Model Selection= to assign specific models to Boxxy's core functions:

- `AI Chat:` Used exclusively for the AI Chat in the sidebar. This model is completely stateless and separate from the rest of the application's UI and Database.
- `Claw:` Powers the Boxxy Agents and assists with `Bookmarks Scripts`. A highly capable, reasoning-focused model is recommended here.
- `Memories:` Responsible for extracting background facts and matching database memories. A fast, lightweight model is ideal for this task.

**Pro Tip:** Press `Shift + Control + p` and type =Models= to quickly jump to the =Model Selection= menu. Experiment with different models until you find the perfect balance of speed and intelligence.

--- 

## BoxxyClaw

Press `Control + /` and send your first message to activate =BoxxyClaw=. This setting is managed per-terminal pane, but you can configure an option in Preferences to always start new terminals with Claw enabled.

Claw operates in two distinct modes; you can switch modes directly from the =ClawMsgBar=.

- **Proactive:** Boxxy will attempt to assist immediately when a terminal error occurs or when a task fails to complete successfully. This is incredibly useful for troubleshooting multi-step workflows.
- **Lazy:** When an error occurs, Claw will wait and offer a prompt to look for a solution. The Claw Indicator will become visible with a 5-second cooldown, giving you the choice to request help.

You can also use the Message Bar to paste large chunks of text or even **images** directly from your clipboard to provide extra context to the agent! 

---

## Reminders & Scheduled Tasks

Boxxy agents understand when you ask them to **remind you of something!** For example, you can ask an agent "Remind me to take my dog out in 10 minutes", and the agent will send you a notification. You can set as many reminders as you like, and at any time you can ask an agent to list them.

You can also set scheduled tasks — for example, "Please clean up my PC in 20 minutes". In this case, Boxxy will present an approval widget before executing.

**Note:** Tasks and Reminders are scoped per agent. Closing an agent will automatically cancel its pending reminders and scheduled tasks.

## Bookmarks

Open =Bookmarks= from the =Command Palette=. Here, you can create and save =Python= and =Shell= scripts. Boxxy automatically registers your saved bookmarks as quick-actions in the =Command Palette= for lightning-fast execution. 

Need dynamic inputs? Define runtime variables using the `{{{my_var}}}` syntax. Boxxy will prompt you to fill them out right when you invoke the script.

All your scripts are safely stored locally at `config/boxxy-terminal/bookmarks`.

## Picking Up Where You Left Off

Never lose your context again. You can resume any of your **last 10 sessions** in any terminal pane by pressing `Control + /` and typing `/resume`. Boxxy will present your recent history, making it easy to pick up exactly where you left off.

If you want to keep a specific session forever, you can =Pin it= using the pin toggle in the message bar. Pinned sessions are always displayed at the top of your list and are never automatically deleted, no matter how many new sessions you start! 

See more at [How It Works](@/how-it-works.md#resume-session).

--- 

## Agent Skills
From =Preferences=, open the =config folder= and navigate to `boxxyclaw/skills`. Boxxy supports standard [Agentic Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) (and a dedicated Boxxy Skills marketplace is planned!). 

Be sure to add your specific system specifications to the default "linux-system" skill so Boxxy understands your environment perfectly.

--- 

## Memories

Boxxy is a self-improving system driven by =Memories=. Tell BoxxyClaw something like ='My favorite editor is micro'=, and Boxxy will remember your preference for next time!

While the core functionality is present, Boxxy is currently in =PREVIEW=. Because there isn't a firm migration strategy yet, your short-term memories might be wiped during application updates. 

However, your =Long Term Memory= will survive updates! You can manually view and edit these persistent facts in `.config/boxxy-terminal/boxxyclaw/MEMORY.md`.

--- 

## Token Consumption

Boxxy is nor context-cheap! To perform at its best, it simultaneously processes a comprehensive set of data: the core toolbox, your active skills, relevant memories, and a snapshot of the terminal buffer. 

You can monitor real-time usage via the =ClawSidebar=. However, modern flagship models (like Gemini, Claude, and GPT) utilize advanced **Context Caching**. This typically reduces the actual billable tokens by up to 80-90% for subsequent requests in the same session. 

To inspect the exact payload Boxxy is broadcasting, you can run Booxy with =Context Logging Env= `BOXXY_DEBUG_CONTEXT=1`

--- 

## Other Tweaks
Depending on your distribution, you may need to raise your system's `inotify` limits. You can check your current values with:

```bash
cat /proc/sys/fs/inotify/max_user_instances
cat /proc/sys/fs/inotify/max_user_watches
```

For example, Fedora's defaults are often too low for modern development. You can safely raise both values by running:

```bash
echo fs.inotify.max_user_instances=65536 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```
