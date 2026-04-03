[![kindling](https://ghrb.waren.build/banner?header=kindling+%21%5Bphoenixframework%5D&subheader=Zettelkasten+for+people+who+could+never+stick+with+it&bg=1A1A1A-4A4A4A&color=FFFFFF&headerfont=Inter&subheaderfont=Inter&support=false)](https://github.com/drewburchfield/kindling)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A writing and knowledge management system that blends [Zettelkasten](https://zettelkasten.de/overview/), [CODE](https://fortelabs.com/blog/the-4-levels-of-personal-knowledge-management/) (Capture, Organize, Distill, Express), and [PARA](https://fortelabs.com/blog/para/) (Projects, Areas, Resources, Archive) with [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) as the discipline layer.

The foundation is Zettelkasten's atomic philosophy: capture a three-word phrase, a single sentence, or a thousand-word rant. The system treats all of it as valid raw material. No structure required upfront, just get it out of your head. That flexibility is the core value.

Layer on Claude Code + CODE methodology and things actually get processed (most people's inbox is where ideas go to die). Layer on PARA and processed knowledge feeds into real projects and areas of your life.

Built on [Obsidian](https://obsidian.md) + [semantic graph search](https://github.com/drewburchfield/obsidian-graph).

## What You Can Do

- **Process your inbox** into atomic notes with AI-assisted triage and insight extraction
- **Discover hidden connections** between notes across completely different domains
- **Search your knowledge** with semantic search that adapts depth to your query
- **Think through problems** with a Socratic partner that resists jumping to solutions
- **Preserve your voice** with AI staging, human rewriting, and de-AI-ification tools
- **Track your intellectual evolution** with daily reviews, weekly synthesis, and changelogs

## Quick Start

See [INSTALL.md](INSTALL.md) for full setup. The short version:

1. Clone this repo and open it as an Obsidian vault
2. Configure MCP servers ([obsidian REST API](https://github.com/modelcontextprotocol/servers/tree/main/src/obsidian) + [obsidian-graph](https://github.com/drewburchfield/obsidian-graph))
3. Copy config templates and update vault paths
4. Start Claude Code from this directory

```bash
claude
```

Test it:
```
/recall test
```

## Commands

| Your state of mind | Command | What it does |
|---|---|---|
| "I have stuff piling up" | `/inbox-processor-hybrid` | Triage items one at a time, extract insights to staging |
| "I just added a note, what connects?" | `/find-connections <note>` | Map the conceptual network around a specific note |
| "What patterns am I missing?" | `/discover` | Vault-wide cross-domain pattern hunting |
| "What do I already know about X?" | `/recall <topic>` | Semantic search, adapts depth to query complexity |
| "Help me think through X" | `/thinking-partner <topic>` | Socratic exploration, resists jumping to solutions |
| "Make this sound like me" | `/de-ai-ify <file>` | Remove AI voice patterns, restore human language |
| "What did I do today?" | `/daily-review` | End-of-day capture and reflection |
| "What happened this week?" | `/weekly-synthesis` | Weekly patterns, energy audit, theme detection |
| "Log what was discovered" | `/update-changelog` | Record connections and decisions from this session |
| "Switch vaults" | `/switch-brain <path>` | Update all config files for a different vault |

Plus `/analyze-kb` for vault health reports.

### Workflow Chains

**Processing new content:**
```
/inbox-processor-hybrid -> human review -> /find-connections -> /update-changelog
```

**Periodic discovery:**
```
/discover -> /update-changelog
```

**Preparing to write:**
```
/recall <topic> -> /thinking-partner <angle> -> write -> /de-ai-ify
```

## How It Works

Three methods, layered:

| Layer | Method | Role |
|---|---|---|
| **Foundation** | Zettelkasten | The engine. Atomic insights that connect and compound over time. |
| **Workflow** | CODE | The nudge layer. Tells you what phase you're in: Capture, Organize, Distill, Express. |
| **Structure** | PARA | The collection layer. Predetermined areas where processed work lands: Projects, Areas, Archive. |

**The core question for every piece of content:** "Is this building knowledge or managing action?"

- Building knowledge: `Sources -> Permanent Notes -> MOCs -> Output`
- Managing action: `Projects` (deadline) or `Life Areas` (ongoing)

### AI Assists, Human Writes

AI-extracted content never goes directly into your permanent notes. It goes to `AI_Extracted_Notes/` tagged with `#ai-extracted`. You review it, rewrite it in your voice, then promote to `02_Permanent/`.

### What Makes `/discover` Different

Most knowledge tools find similar content. `/discover` does the opposite: it hunts for notes with **low** semantic similarity but **high** conceptual connection. A note about dopamine dynamics and one about prospect theory might score 0.63 similarity, but they describe the same mechanism (baseline-deviation adaptation). That's the kind of connection that sparks an article.

## Folder Structure

```
00_Inbox/           # Dump everything here (flat, no subfolders)
01_Sources/         # Books, articles, writing exercises
02_Permanent/       # Atomic insights, one idea per note (THE CORE)
03_MOCs/            # Maps of Content (navigation hubs)
04_Projects/        # Time-bound work with deadlines
05_Life_Areas/      # Ongoing responsibilities
06_Output/          # Synthesized articles and frameworks
07_Archive/         # Completed work
08_Attachments/     # Media files
09_Meta/            # System files, changelogs, templates
AI_Extracted_Notes/ # AI-generated content (clear provenance)
```

Only the framework is tracked in git. Your actual notes sync however you prefer (iCloud, Dropbox, etc.). Each folder has a README explaining what belongs there.

## Permanent Notes

Every permanent note is one atomic insight, written in your words. 50-300 words, clear title that states the insight, `[[wikilinks]]` to related notes, YYYYMMDD prefix.

```markdown
---
created: 2024-12-16
tags: [neuroscience, motivation]
---

# Dopamine drives wanting, not liking

Dopamine is responsible for the *desire* to act, not the enjoyment
of the action itself. This explains why we can be motivated to do
things we don't enjoy.

The "wanting" (dopamine) system is separate from the "liking" (opioid) system.

**Source**: [[Dopamine Nation - Book Notes]]

**Related**:
- [[Motivation vs willpower]]
- [[Reward prediction error]]
```

## Requirements

- [Obsidian](https://obsidian.md) with the [Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api) plugin
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview)
- Docker (for MCP servers)
- Node.js 18+

| MCP Server | Purpose | Required |
|---|---|---|
| **[obsidian](https://github.com/modelcontextprotocol/servers/tree/main/src/obsidian)** | Read/write files in your vault via Obsidian's REST API | Yes |
| **[obsidian-graph](https://github.com/drewburchfield/obsidian-graph)** | Semantic search, connection graphs, hub/orphan detection (pgvector) | Yes |
| **[Docker MCP gateway](https://docs.docker.com/desktop/features/gordon/mcp-catalog/)** | YouTube transcript pulling and other utilities | Optional |

## Getting Started

| Week | Focus | Commands |
|---|---|---|
| **1** | Capture. Dump thoughts, articles, notes into `00_Inbox/` | `/inbox-processor-hybrid` |
| **2** | Connect. Run connection analysis on permanent notes | `/find-connections`, `/update-changelog` |
| **3** | Discover. Look for cross-domain patterns | `/discover`, `/recall` |
| **4** | Reflect. Establish your rhythm | `/daily-review`, `/weekly-synthesis` |

| When | What | Time |
|---|---|---|
| Throughout the day | Capture to `00_Inbox/` | Seconds |
| Evening | `/daily-review` | 5 min |
| Weekly | `/inbox-processor-hybrid` + `/weekly-synthesis` | 30 min |
| Monthly | `/analyze-kb` + `/discover` | 1 hour |

See [EXAMPLES.md](EXAMPLES.md) for full workflow walkthroughs.

## License

MIT License - see [LICENSE](LICENSE) for details.
