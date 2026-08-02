# Clawker Plugin

Agent skills for [clawker](https://github.com/schmitthub/clawker) — setup, configuration, and troubleshooting support, plus guided authoring of bundles, harnesses, stacks, and monitoring extensions.

The skills are standard agent skills (`SKILL.md` plus reference files) and work with any skill-aware coding agent. For Claude Code, this repository doubles as both the plugin and its marketplace: the `clawker-support` plugin lives at the repo root and `.claude-plugin/marketplace.json` serves it directly. Other agents consume the `skills/` directory directly.

## What it does

### clawker-support

When you invoke `/clawker-support`, the agent becomes a clawker configuration specialist that:

- **Researches** what you're trying to add (packages, MCP servers, tools, runtimes)
- **Reads** the actual Dockerfile templates and config schema to understand how clawker works
- **Synthesizes** the exact YAML config you need, with firewall rules and all

It understands the full clawker system: Dockerfile generation, config layering, firewall architecture, injection points, build-time vs runtime, and common gotchas.

### bundle-creator

When you invoke `/bundle-creator`, the agent walks you through authoring clawker extensions step by step:

- **Interviews** you first — distributable bundle or local-only component, and which component types (harness, stack, monitoring extension)
- **Scaffolds** the correct layout, then walks each manifest field one concept at a time
- **Validates** the result with `clawker bundle validate --strict` and attempts a real build when the clawker CLI and Docker are available

It handles new creation, modifying existing bundles, and promoting a loose local component into a distributable bundle.

## Install

```bash
# Install with the clawker CLI (recommended)
clawker plugin install
```

Or manually in Claude Code:

```bash
# Add the marketplace
claude plugin marketplace add schmitthub/clawker-plugin

# Install the plugin
claude plugin install clawker-support@schmitthub-plugins
```

For other skill-aware agents, copy or symlink the skill directories under
`skills/` into your agent's skill discovery location.

## Usage

In any agent session:

```
/clawker-support how do I add the GitHub MCP to my container?
```

```
/clawker-support my container can't reach pypi.org
```

```
/clawker-support help me set up a Rust project with clawker
```

```
/bundle-creator I want to package my zig stack for my team
```

Or just ask about clawker — the skills trigger automatically when the agent detects clawker-related questions or bundle-authoring work.

## Documentation

Full clawker documentation: [docs.clawker.dev](https://docs.clawker.dev)
