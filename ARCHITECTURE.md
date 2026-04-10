# DeskClaw - Architecture Blueprint

## 1. The Stack
*   **Infrastructure:** Docker Dev Container (Windows WSL2)
*   **AI Engine:** Local Ollama (`gemma4:e4b`) via `host.docker.internal:11434`
*   **Gateway:** OpenClaw (`ws://127.0.0.1:18789`)
*   **Human Handoff:** Custom Node.js/React dashboard (Planned)

## 2. Channels to Connect
*   [ ] WhatsApp Business
*   [ ] Instagram
*   [ ] Gmail (`gog` OAuth)

## 3. Skills (MCP Tools) Required
*   `check_appointment_availability`
*   `escalate_to_human`
*   `read_knowledge_base`

## 4. Open Questions / Roadmap
*How do we integrate a specific database for the appointments?*
*What triggers the human escalation flag?*
