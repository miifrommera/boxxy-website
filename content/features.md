+++
title = "Core Features"
template = "docs.html"
+++

# Terminal Features

Boxxy is, first and foremost, a high-performance Linux terminal built for modern developers. Before you even turn on the AI features, you're using a top-tier terminal emulator designed for speed, clarity, and deep shell integration.

---

### The Core Engine (boxxy-vte)
At the heart of Boxxy is a custom-built, 100% Rust terminal engine. It replaces traditional C-based libraries with a modern, async-first architecture.

- **GPU Accelerated Rendering**: Uses GTK4's GSK scene graph to render text and images with silky-smooth performance and zero tearing.
- **Kittygraphics Support**: Native support for the Kitty graphics protocol, allowing you to render high-resolution images and even rich media directly in your terminal grid.
- **Semantic Shell Integration**: Full support for **OSC 133** markers. Boxxy understands the difference between your prompt, your command, and the resulting output, allowing for smarter context awareness.
- **Bidirectional Reflow**: Smart text wrapping and unwrapping when you resize your window, ensuring your logs remain readable at any size.
- **Advanced Regex Search**: A lightning-fast, Unicode-aware search system with automatic viewport scrolling and word-boundary detection.
- **Robust CWD Tracking**: Instant directory tracking via **OSC 7**, which works seamlessly even over SSH or through sandboxed environments.

### UI & Layout
Boxxy is designed to maximize your screen real estate and keep you focused on your work.

- **Dynamic Splits with Soft Swap**: Split your terminal vertically or horizontally as many times as you need. With "Soft Swap", you can seamlessly exchange the contents of two active panes via a simple keyboard shortcut without breaking your workflow.
- **iTerm2 Themes**: Fully supports the popular iTerm2 color scheme format, giving you access to thousands of community-created themes. Switch between them instantly.
- **Seamless Background Images**: Set a background image for your entire tab. Boxxy intelligently spans the image across all transparent terminal splits for a gorgeous, unified look.
- **Inactive Pane Dimming**: Never get lost in your splits again. Boxxy automatically dims inactive terminal panes so your active focus is always crystal clear.
- **Modern Hyperlinks**: Support for **OSC 8** hyperlinks with robust media previews on hover, making your terminal feel more like a modern web browser.
- **Native Progress Bars**: Intercepts **OSC 9;4** sequences (like those from Cargo or Flatpak) to render native GTK progress bars directly in the UI.

---

## Agentic Features

And then there is the =Agentic Part= 🤖
