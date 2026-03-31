# Critical Thinking Agent

A [pi](https://github.com/badlogic/pi-mono) agent profile designed as a thinking partner — not an answer machine. It helps you understand concepts, refine ideas, weigh tradeoffs, and extend thinking beyond its original scope through structured dialogue.

Built on **critical thinking** (surface assumptions, evaluate evidence, steelman opposing views, spot biases) and **systems thinking** (map feedback loops, find leverage points, consider unintended consequences).

## How it works

```
┌─────────────────────────────────┐
│  You ←→ Critical Thinking Agent │  Opus · high thinking
│         (dialogue, analysis)    │
│              │                  │
│              │ delegates        │
│              ▼                  │
│         Researcher Agent        │  Haiku · fast & cheap
│     (web search, synthesis)     │
└─────────────────────────────────┘
```

The main agent is your thinking partner. When facts or external evidence are needed, it delegates to a **researcher subagent** that searches the web and returns structured findings — keeping the main agent's context clean and focused on reasoning.

Research findings are labeled:
- **[FACT]** — empirically verified, multiple independent sources
- **[CONSENSUS]** — most experts agree, but not a hard fact
- **[OPINION]** — a specific perspective, attributed to its source
- **[DISPUTED]** — active disagreement among credible sources

## What it does

- Surfaces assumptions in your reasoning (and its own)
- Steelmans ideas before critiquing them
- Maps systems: components, feedback loops, emergent properties
- Evaluates evidence quality — not all sources are equal
- Challenges respectfully and directly
- Goes deep on one thread at a time instead of covering everything superficially
- Always pauses for your input — it thinks *with* you, not *for* you

## What it doesn't do

- Write code or edit files
- Produce final deliverables
- Agree just to be agreeable
- Try to reach conclusions on its own

## Setup

### Prerequisites

- [pi](https://github.com/badlogic/pi-mono) installed
- An Anthropic API key or subscription
- The following pi packages installed:
  ```bash
  pi install npm:pi-subagents
  pi install npm:pi-web-access
  ```

### Install

Clone this repo as your pi config directory:

```bash
git clone https://github.com/ruliana/pi-critical-thinking.git ~/.pi/critical-thinking
```

Add a shell alias (in `.zshrc`, `.bashrc`, or equivalent):

```bash
alias think='PI_CODING_AGENT_DIR=~/.pi/critical-thinking pi'
```

Authenticate on first run:

```bash
source ~/.zshrc
think
# Then use /login to authenticate with Anthropic
```

### Models

| Role | Model | Purpose |
|------|-------|---------|
| Main agent | `claude-opus-4-6` | Deep reasoning, nuanced analysis |
| Researcher | `claude-haiku-4-5` | Fast, cheap web search and synthesis |

Models use floating aliases (no date-pinned versions), so they stay current with Anthropic's latest releases within each family.

You can cycle between Opus and Sonnet with `Ctrl+P` during a session.

## File structure

```
~/.pi/critical-thinking/
├── SYSTEM.md          # System prompt: critical & systems thinking partner
├── AGENTS.md          # Context: research delegation conventions
├── settings.json      # Model config, packages
├── agents/
│   └── researcher.md  # Research subagent (Haiku, web search tools)
└── .gitignore         # Excludes sessions/ and runtime dirs
```

## How it uses pi

This is a standard [pi agent profile](https://github.com/badlogic/pi-mono) using `PI_CODING_AGENT_DIR` for full isolation from your default coding agent. It relies on:

- **[pi-subagents](https://github.com/nicobailon/pi-subagents)** — provides the `subagent` tool for delegating research to an isolated subprocess
- **[pi-web-access](https://github.com/nicobailon/pi-web-access)** — provides `web_search`, `fetch_content`, and `get_search_content` tools used by the researcher agent

## License

MIT
