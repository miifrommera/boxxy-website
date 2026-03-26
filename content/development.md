+++
title = "Development"
template = "docs.html"
+++

# Development

Boxxy is largely developed using =AI Agents=. The most efficient way to start contributing to Boxxy is to clone the repository and ask your preferred agent to read the `AGENTS.md` file to familiarize itself with the project's architecture and conventions.

---

## Workflow & Committing

Boxxy is currently in an early, high-velocity development phase. To maintain maximum speed, we utilize a private =dev= branch for active development. 

Once a major task or feature is finalized, we squash all related commits into a single =consolidated commit= before merging into the =main= branch. While this results in larger individual commits, the logic remains easy to parse and understand when analyzed by an =Agent=.

---

## Contributing

We welcome code contributions! However, due to the rapid pace of downstream development, traditional PRs can be difficult to merge if they fall out of sync. 

For the best results, we prefer =agentic-style= contributions: clear prompts accompanied by code examples or detailed implementation strategies that our internal agents can help integrate seamlessly.

---

## Building & Testing

Boxxy is built with =Rust 1.94=. For standard development and local testing, you can use =Cargo= directly:

```bash
cargo build -p boxxy-agent -p boxxy-terminal
```

Please note that a successful Cargo build does not always guarantee identical behavior within a =Flatpak= environment, especially for components involving `boxxy-agent`.

### Building the Flatpak

To build and test the =Flatpak= bundle locally, follow these steps:

1. **Generate Sources:**
   ```bash
   python3 flatpak/flatpak-cargo-generator.py Cargo.lock -o flatpak/cargo-sources.json
   ```

2. **Build & Export Bundle:**
   ```bash
   flatpak-builder --repo=repo --force-clean build-dir flatpak/dev.boxxy.BoxxyTerminal.yml
   flatpak build-bundle repo boxxy.flatpak dev.boxxy.BoxxyTerminal
   ```

**Alternative:** To build and install the Flatpak to your user environment in a single command:
```bash
flatpak-builder --user --install --force-clean build-dir flatpak/dev.boxxy.BoxxyTerminal.yml
```
