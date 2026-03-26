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

You can toggle =BoxxyClaw= using the Claw icon located in the Headerbar. This setting is managed per-window, but you can configure an option in Preferences to always start new windows with Claw enabled.

Claw operates in two distinct modes:

- `Proactive:` Boxxy will attempt to assist immediately when a terminal error occurs or when a task fails to complete successfully. This is incredibly useful for troubleshooting multi-step workflows.
- `Lazy:` When an error occurs, Claw will wait and offer a prompt to look for a solution. The Claw Indicator will become visible with a 5-second cooldown, giving you the choice to request help.

Press `Control + /` to message BoxxyClaw.

---

## Bookmarks

Open =Bookmarks= from the =Command Palette=. Here, you can create and save =Python= and =Shell= scripts. Boxxy automatically registers your saved bookmarks as quick-actions in the =Command Palette= for lightning-fast execution. 

Need dynamic inputs? Define runtime variables using the `{{{my_var}}}` syntax. Boxxy will prompt you to fill them out right when you invoke the script.

All your scripts are safely stored locally at `config/boxxy-terminal/bookmarks`.

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
