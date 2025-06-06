# Browser-use
mikewho90/ai-browser-ui:v1.0 — Docker Image Overview

This image was originally built by the Browser Use project and has been modified by Mike Jones to support local LLM integrations, notably Ollama.

The modifications resolve key limitations that prevented local LLM backends—especially Ollama—from running smoothly inside the container, addressing compatibility challenges faced by myself and the wider community.

🔧 I do not claim authorship of the underlying Browser Use framework. This fork includes essential adjustments to improve compatibility and usability for local-first LLM workflows.

🚀 Key Features

🖥️ Headless browser UI with full VNC access (Xvfb + fluxbox)

🧪 Scriptable automation using Playwright + Chromium

🤖 Built-in support for a wide range of LLM APIs:

OpenAI, Ollama, Anthropic, Azure, Mistral, Moonshot, IBM, DeepSeek, and more

📦 Native Ollama support for local model inference

🧠 Compatible with GPU-accelerated inference (NVIDIA passthrough)

🐳 Fully containerized — no build-time dependencies on the host

🛠️ Technical Notes

Environment Variables

This image is pre-configured to support a broad spectrum of LLMs and API providers, including OpenAI, Ollama, Anthropic, Azure, IBM, DeepSeek, Mistral, and others. Environment variables for endpoints and API keys can be set via Docker Compose.

GPU Support

To enable GPU acceleration, the container uses deploy.resources.reservations.devices with driver: nvidia. Make sure your host system has the NVIDIA Container Toolkit installed and properly configured.

Ollama Integration

Ollama is installed inside the container and launched via Supervisor. For local model access and persistence:

volumes:
  - /DATA/AppData/OllamaData:/root/.ollama  # Ollama model storage

This ensures local models are preserved across container restarts.

Display & VNC

Xvfb creates a headless X display

x11vnc exposes this via port 5901

noVNC provides a browser-accessible VNC interface on port 6080

Playwright is pre-installed and set up to use the Chromium backend

Ports Summary

7788: Web UI

6080: Web-based VNC (noVNC)

5901: VNC (x11vnc)

9222: Chrome debugging (DevTools protocol)

Stability & Health

Health checks monitor VNC port

Shared memory (shm_size: 2gb) ensures Chromium stability

/tmp mounted as tmpfs for performance and compatibility

transparincy note about the modafide files from browser use a local web baised ai deep search tool
