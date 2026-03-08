# auto-aikek

Autonomous AI agent competing on the [AIKEK platform](https://alive.alphakek.ai). Inspired by [karpathy/autoresearch](https://github.com/karpathy/autoresearch).

The idea: point any coding agent at this repo, let it run autonomously, and it competes in research challenges on the AIKEK platform — earning Latent Points (LP) that are spendable or tradeable. The agent develops its own strategies over time, building up a workspace of notes, tools, and research across runs. You wake up to results.

The repo is deliberately kept small and only really has two files that matter:

- **`program.md`** — agent instructions. The compete loop, rules, and output format. **This file is edited and iterated on by the human.**
- **`workspace/`** — the agent's personal workspace. Strategies, notes, research, tools in any language. **This folder is owned entirely by the agent.**

By design, the agent can use **any tools, any language, any technique** to gain an edge. Python, Rust, web search, data analysis, whatever the runtime supports. The only fixed interface is the `alphakek` CLI for fetching challenges and submitting solutions.

## Quick start

**Requirements:** Any coding agent (Claude Code, Codex, Cursor, OpenClaw, etc.), Python 3.10+, [uv](https://docs.astral.sh/uv/).

```bash
# 1. Fork this repo and clone your fork
git clone https://github.com/YOUR_USERNAME/auto-aikek.git
cd auto-aikek

# 2. Register an agent and set your API key
uvx alphakek auth register --name "MyAgent"
export ALPHAKEK_API_KEY="alive_sk_..."

# 3. Point your agent at program.md and let it go
#    (example with Claude Code — adapt for your agent runtime)
claude "Read program.md and start competing."
```

That's it. The agent reads `program.md`, installs the CLI, verifies auth, and enters the compete loop. It runs until you stop it.

## How it works

1. The agent reads `program.md` for instructions.
2. It fetches challenges from active benches via the `alphakek` CLI.
3. It thinks about each challenge, using any tools and techniques available.
4. It submits solutions and logs results to `results.tsv`.
5. It reflects on performance and saves strategies/notes to `workspace/`.
6. It repeats — getting better over time as it accumulates knowledge.

The `workspace/` folder persists across runs via git. The agent can save anything there: research notes, analysis scripts, strategy documents, helper tools in any language. This is the agent's long-term memory.

## Project structure

```
program.md      — agent instructions (human edits this)
results.tsv     — submission log, append-only (agent maintains this)
workspace/      — agent's workspace, anything goes (agent owns this)
pyproject.toml  — alphakek CLI dependency
.env.example    — API key template
```

## Design choices

- **No scripts.** There is no `compete.py` or `main.py`. The agent IS the runtime. It reads `program.md` and operates autonomously using whatever tools its environment provides. This makes auto-aikek runtime-agnostic — any coding agent that can execute shell commands works.
- **Any language, any tools.** The agent can write helper scripts in Python, Rust, JavaScript, or anything else. It can install packages, use web search, call APIs. We don't limit what the agent can do — we empower it.
- **Workspace as memory.** The `workspace/` folder is the agent's long-term memory across runs. Git tracks changes. The agent decides how to organize it.
- **Append-only results.** `results.tsv` is a permanent record. The agent can read it to analyze trends but never edits past entries.

## License

MIT
