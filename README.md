<p align="center">
  <img src="assets/banner.png" alt="Hermes Agent" width="100%">
</p>

# Hermes Agent

<p align="center">
  <a href="https://hermes-agent.nousresearch.com/docs/"><img src="https://img.shields.io/badge/Docs-hermes--agent.nousresearch.com-FFD700?style=for-the-badge" alt="Documentation"></a>
  <a href="https://discord.gg/NousResearch"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/NousResearch/hermes-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License: MIT"></a>
  <a href="https://nousresearch.com"><img src="https://img.shields.io/badge/Built%20by-Nous%20Research-blueviolet?style=for-the-badge" alt="Built by Nous Research"></a>
</p>

> My personal fork of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) &mdash; a self-improving AI agent with persistent memory, multi-platform messaging, and fully local inference. No cloud LLM APIs. No subscriptions. No data leaving your machine.

---

## The Core: Local Heretic Model

Everything runs through **Qwen 3.6 35B-A3B Abliterated Heretic** &mdash; a locally-hosted, uncensored model served via [LM Studio](https://lmstudio.ai). This is the foundation the entire system is built on.

```
localhost:1234 &rarr; Hermes Agent &rarr; Tools, Memory, Gateway, Platforms
```

**Why this matters:**

- **Zero API costs** &mdash; no per-token billing, no rate limits, no usage caps. Run it 24/7 for the cost of electricity.
- **Zero data leakage** &mdash; every prompt, every tool call, every memory stays on your hardware. Nothing is transmitted to any third-party API.
- **Uncensored reasoning** &mdash; the abliterated heretic variant removes artificial refusal patterns, giving the agent unrestricted problem-solving capability across all domains.
- **Full context window** &mdash; 65,536 tokens of context, enough for deep multi-turn conversations with tool use and memory injection.
- **Mixture-of-Experts efficiency** &mdash; 35B total parameters with only 3B active per forward pass (A3B), meaning it runs fast on consumer hardware while punching well above its weight class.
- **Always available** &mdash; no outages, no provider downtime, no API deprecations. The model is a file on your disk.

The agent, the gateway, the memory system, the tools &mdash; none of it depends on OpenAI, Anthropic, or any external provider. Swap the model in LM Studio whenever a better one drops. The architecture is model-agnostic; the philosophy is model-local.

---

## What Makes This Agent Different

Hermes isn't a chatbot wrapper. It's a persistent, self-improving system that learns from every interaction, runs tools autonomously, and lives across every platform you use &mdash; all from a single process.

### Holographic Memory

A fully local memory system powered by **Holographic Reduced Representations** (HRR) &mdash; a vector symbolic architecture from cognitive science. No embedding models, no cloud APIs, no external dependencies beyond NumPy.

| Capability | How It Works |
|-----------|-------------|
| **Fact Storage** | SQLite-backed with FTS5 full-text search and trust scoring |
| **Compositional Retrieval** | Algebraic bind/unbind/bundle operations on phase vectors &mdash; find facts by structural relationships, not just keywords |
| **Entity Resolution** | Auto-extracts entities from stored facts, resolves aliases, links them in a knowledge graph |
| **Trust Scoring** | Asymmetric feedback loop &mdash; helpful facts gain trust slowly (+0.05), unhelpful facts decay fast (-0.10) |
| **Contradiction Detection** | Finds facts that share entities but diverge in content &mdash; automated memory hygiene |
| **Multi-Entity Reasoning** | Vector-space JOINs across entities &mdash; "find everything about X *and* Y together" |
| **Hybrid Search** | FTS5 keyword (40%) + Jaccard overlap (30%) + HRR similarity (30%), trust-weighted |

Zero sustained RAM cost. Vectors live on disk, loaded only during queries (~400KB per search).

### Self-Improving Skills

The agent creates procedural skills from experience, improves them during subsequent use, and persists them across sessions. Skills are portable Markdown files compatible with the [agentskills.io](https://agentskills.io) open standard.

### Multi-Platform Gateway

A single `hermes gateway` process connects to all your messaging platforms simultaneously:

- **Discord** &mdash; full bot with slash commands
- **Telegram** &mdash; bot with voice memo transcription
- **Slack** &mdash; workspace app with subcommand routing
- **WhatsApp** &mdash; via WhatsApp Business API
- **Signal** &mdash; via signal-cli
- **Home Assistant** &mdash; smart home integration
- **Email, SMS, Matrix, Mattermost, DingTalk, WeChat, Feishu, QQ** &mdash; and more

Cross-platform conversation continuity &mdash; start on Telegram, continue on Discord.

### Local-First Inference

The default setup runs entirely on local hardware via LM Studio &mdash; no cloud API keys required. The agent connects to `localhost:1234` and speaks the OpenAI-compatible chat completions protocol.

For scaling up, the same config pattern works with a rented H200 running vLLM or TGI &mdash; just change the `base_url` to your remote GPU endpoint. The architecture doesn't care where inference happens, only that it speaks OpenAI format.

Also supports 15+ cloud providers if needed: [Nous Portal](https://portal.nousresearch.com), [OpenRouter](https://openrouter.ai), NVIDIA NIM, Google Gemini, OpenAI, Anthropic, Hugging Face, Ollama, and more. But the point is you don't need any of them.

### Autonomous Tool Use

40+ built-in tools organized into toolsets. The agent decides when and how to use them:

| Category | Tools |
|----------|-------|
| **Terminal** | Execute commands across 6 backends (local, Docker, SSH, Daytona, Singularity, Modal) |
| **Files** | Read, write, search, patch files with full filesystem access |
| **Code** | Execute Python with persistent state, install packages |
| **Web** | Browse pages, search the web, take screenshots |
| **Git** | Full git operations &mdash; clone, commit, branch, PR creation |
| **Memory** | Fact store with 9 actions: add, search, probe, related, reason, contradict, update, remove, list |
| **Delegation** | Spawn subagents for parallel workstreams |

### Context Compression

Intelligent conversation compression that preserves prompt caching. When context grows long, Hermes compresses older turns while protecting recent messages and cached prefixes.

```yaml
compression:
  enabled: true
  threshold: 0.5
  target_ratio: 0.2
  protect_last_n: 20
```

### Scheduled Automations

Built-in cron scheduler delivers results to any connected platform:

```
/cron add "Every morning at 8am, check my GitHub notifications and summarize them"
```

### Session Management

SQLite-backed session store with FTS5 search. Resume any past conversation, search across all sessions, get LLM-powered summaries of previous work.

### Skin Engine

Data-driven CLI theming &mdash; customize banners, spinners, colors, and branding with pure YAML. Ships with `default`, `ares`, `mono`, and `slate` themes. Drop custom skins into `~/.hermes/skins/`.

---

## Quick Install

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

Works on Linux, macOS, WSL2, and Android (Termux).

```bash
source ~/.bashrc    # reload shell
hermes              # start chatting
```

## Getting Started

```bash
hermes              # Interactive CLI
hermes model        # Choose provider + model
hermes setup        # Full setup wizard
hermes gateway      # Start messaging gateway
hermes tools        # Configure toolsets
hermes doctor       # Diagnose issues
```

## Configuration

All settings live in two files (neither is committed to the repo):

| File | Contains | Location |
|------|----------|----------|
| `config.yaml` | Model, tools, display, memory, compression, skills, scheduling | `~/.hermes/config.yaml` |
| `.env` | API keys and tokens only | `~/.hermes/.env` |

Secrets never touch the repository. The `.gitignore` excludes `.env`, `logs/`, private keys, and all credential files.

## Project Structure

```
hermes-agent/
  run_agent.py          # Core conversation loop (AIAgent class)
  model_tools.py        # Tool orchestration and discovery
  cli.py                # Interactive CLI (HermesCLI class)
  tools/                # 40+ tool implementations, auto-discovered
    environments/       # Terminal backends (local, Docker, SSH, Modal, ...)
  gateway/              # Multi-platform messaging gateway
    platforms/          # Per-platform adapters
  plugins/
    memory/             # Memory providers (holographic, honcho, mem0, ...)
  skills/               # Built-in skill library
  optional-skills/      # Extended skills (installable on demand)
  ui-tui/               # Ink-based terminal UI
  agent/                # Provider adapters, memory, caching, compression
  cron/                 # Scheduled task engine
  tests/                # ~15K tests across ~700 files
```

## CLI Quick Reference

| Action | Command |
|--------|---------|
| New conversation | `/new` or `/reset` |
| Switch model | `/model [provider:model]` |
| Set personality | `/personality [name]` |
| Retry / undo | `/retry`, `/undo` |
| Compress context | `/compress` |
| Check usage | `/usage` |
| Browse skills | `/skills` |
| Search sessions | `/search [query]` |
| Resume session | `/resume` |
| Interrupt | `Ctrl+C` or new message |

---

## Upstream

This is a personal fork. The upstream project is maintained by [Nous Research](https://nousresearch.com):

- [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)
- [Documentation](https://hermes-agent.nousresearch.com/docs/)
- [Discord](https://discord.gg/NousResearch)
- [Skills Hub](https://agentskills.io)

## License

MIT &mdash; see [LICENSE](LICENSE).
