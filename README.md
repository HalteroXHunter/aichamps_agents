# Agent AI Champs

This repository contains examples of different agent architectures built with [LangGraph](https://langchain-ai.github.io/langgraph/).

## Setup Instructions

### 1. Install `uv`
This project uses `uv` for fast Python package management.

- **macOS/Linux**:
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
- **Windows**:
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```

### 2. Sync Environment
Install the project dependencies:
```bash
uv sync
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory of the project. You will need keys for OpenAI, Tavily, and LangSmith.

```env
OPENAI_API_KEY=sk-...
TAVILY_API_KEY=tvly-...

# LangSmith Configuration
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=lsv2-...
LANGSMITH_PROJECT=agent_aichamps
```

**Get your API Keys:**
- **Tavily**: [Sign up for a free tier account](https://app.tavily.com/)
- **LangSmith**: [Sign up for a LangSmith account](https://smith.langchain.com/)

### 4. Run LangGraph Studio
Launch the local development studio to visualize and interact with the agents:
```bash
uv run langgraph dev
```

---

## Agent Architectures

This repository showcases three distinct agent patterns:

### 1. Simple Agent (`simple_agent/`)
A foundational agent example that demonstrates tool usage.
- **Description**: An assistant equipped with basic arithmetic tools (add, multiply, divide).
- **Pattern**: Uses the `bind_tools` capability of the LLM to determine when to call a function versus when to respond directly.

### 2. Reflection Agent (`reflection_agent/`)
An agent that improves its output through iterative self-critique.
- **Description**: An essay writer composed of two nodes: a **Generator** and a **Reflector**.
- **Pattern**:
  1. The Generator writes an initial draft.
  2. The Reflector (acting as a teacher) critiques the draft.
  3. The Generator revises the work based on the critique.
  4. This loop continues until the Reflector is satisfied or a maximum number of iterations is reached.

### 3. Multi-Agent Collaboration (`multi_agent/`)
A system of specialized agents working together.
- **Description**: A team consisting of a **Researcher** and a **Chart Generator**.
- **Pattern**:
  - The **Researcher** uses Tavily Search to find information.
  - The **Chart Generator** uses a Python REPL to create visualizations.
  - A supervisor or routing logic passes control between them based on the current need, allowing for complex tasks like "Research the current stock price of Apple and plot it."
