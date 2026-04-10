# OpenClaw Sandbox - Learning & Notes

## 1. Core Architecture
*   **The Gateway:** The WebSocket hub (`openclaw gateway`) running in the background. It routes messages from channels to the AI.
*   **The Channels:** The input/output methods (Web UI, TUI, WhatsApp, Telegram).
*   **The Workspace:** The hidden brain (`/home/node/.openclaw/workspace`).
    *   `AGENTS.md` / `SOUL.md`: Define the system prompts and personality.
*   **Skills (MCP):** Node.js tools that the AI can execute (e.g., `read_file`, `goplaces`).

## 2. Crucial Commands
*   `openclaw onboard`: Setup wizard (skip daemon installation in Docker!).
*   `openclaw gateway`: Start the server.
*   `openclaw tui`: Launch the developer chat interface (requires gateway running).
*   `openclaw sessions list`: View all chat histories.
*   `openclaw reset`: Factory reset the configuration.

## 3. Important Fixes (Docker on Windows)
*   **The "Local Install" Deadlock:** Do not run `npm install openclaw` in the shared workspace. The Windows-to-Linux bridge chokes on file I/O.
*   **The Fix:** Install globally in the container: `npm install -g openclaw@latest`.
*   **The Zombie Process:** If the gateway refuses to stop and blocks port `18789`, kill it manually: `pkill -9 -f openclaw`.
*   **Local Models (Ollama):** Install Ollama natively on Windows, not in Docker. Connect OpenClaw to it using `http://host.docker.internal:11434`.

## 4. Questions to Ask Later
*How do I write a custom Skill from scratch?*
*How do I create a new Agent profile that isn't the default 'main'?*
