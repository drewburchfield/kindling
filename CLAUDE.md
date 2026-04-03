# Kindling - System Configuration

## What This Is

A writing and knowledge management system that blends Zettelkasten (atomic notes, connections, emergence), CODE (Capture, Organize, Distill, Express), and PARA (Projects, Areas, Resources, Archive). Powered by Claude Code + Obsidian + semantic graph search.

**Core principle:** AI assists, human writes. AI-extracted content goes to a staging area with clear provenance. The human rewrites before promoting to permanent notes.

## Primary Operating Mode: THINKING MODE

**Default behavior:**
- **Ask questions** before generating content
- **Search vault** for existing insights using `/recall`
- **Help articulate** thinking, don't write for me
- **Resist solutioning** - stay in exploration mode
- **Only generate** when explicitly requested ("write", "draft", "generate")

## Folder Structure

```
00_Inbox/           # Universal capture (dump everything here, flat)
01_Sources/         # Source materials (books, articles, exercises)
02_Permanent/       # CORE: Atomic insights, one idea per note
03_MOCs/            # Navigation hubs (Maps of Content)
04_Projects/        # Time-bound work with deadlines
05_Life_Areas/      # Ongoing responsibilities
06_Output/          # Synthesized articles and frameworks
07_Archive/         # Completed work
08_Attachments/     # Media files
09_Meta/            # System files, changelogs, templates
AI_Extracted_Notes/ # AI-generated content (clear provenance)
```

### The Core Question

**"Is this building knowledge or managing action?"**

- **Building knowledge** -> Zettelkasten: `01_Sources -> 02_Permanent -> 03_MOCs -> 06_Output`
- **Managing action** -> PARA: `04_Projects` (deadline) or `05_Life_Areas` (ongoing)

## Commands (11 total)

### When to Use What

| Your state of mind | Command | What it does |
|---|---|---|
| "I have stuff piling up" | `/inbox-processor-hybrid` | Triage inbox items one at a time, extract insights to staging |
| "I just added a note, what connects?" | `/find-connections <note>` | Map the conceptual network around a specific note |
| "What patterns am I missing?" | `/discover` | Vault-wide cross-domain pattern hunting, no starting point needed |
| "What do I already know about X?" | `/recall <topic>` | Semantic search, adapts depth to query complexity |
| "Help me think through X" | `/thinking-partner <topic>` | Socratic exploration, resists jumping to solutions |
| "Make this sound like me" | `/de-ai-ify <file>` | Remove AI voice patterns, restore authentic language |
| "What did I do today?" | `/daily-review` | End-of-day capture and reflection |
| "What happened this week?" | `/weekly-synthesis` | Weekly patterns, energy audit, theme detection |
| "Log what was discovered" | `/update-changelog` | Record connections and decisions from this session |
| "Switch to another vault" | `/switch-brain <path>` | Update all config files for a different vault |

### Also Available
- `/analyze-kb` - Generate a condensed health report of vault structure

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

**Reflection:**
```
/daily-review (daily) -> /weekly-synthesis (weekly)
```

## Agents (1)

- **diagram-generator** - Create visualizations using MCP chart servers (requires chart MCP, future integration)

## Voice Preservation

### When AI Should Generate Content
- Explicit request: "Write a draft about X"
- Outlining: "Create outline from my notes"
- Summarizing: "Summarize these 5 notes"
- Extracting: "Pull insights from this source" (preserve exact phrasing)

### When AI Should NOT Generate Content
- Thinking mode active (default)
- Exploring ideas (ask questions instead)
- Processing inbox (suggest categories, don't rewrite)
- User hasn't explicitly requested writing

### Extraction Workflow
1. AI extracts insights -> `AI_Extracted_Notes/` with #ai-extracted tag
2. Before extracting, search vault for existing coverage (dedup check)
3. Human reviews and rewrites in their own voice
4. Run `/de-ai-ify` on any AI-generated content if needed
5. Move validated notes to `02_Permanent/` if appropriate

## Permanent Notes Format

- Title: Clear statement of insight (e.g., "Dopamine drives wanting, not liking")
- Length: 50-300 words
- Voice: Human's words, not copy-paste
- Links: Connect to related permanent notes via `[[wikilinks]]`
- Source: Attribution to source note if applicable
- Date: YYYYMMDD prefix (e.g., 20241216-Title.md)
- Tags: Relevant topics in frontmatter

```markdown
---
created: 2024-12-16
tags: [neuroscience, motivation]
---

# Dopamine drives wanting, not liking

Dopamine is responsible for the *desire* to act, not the enjoyment of the
action itself. This explains why we can be motivated to do things we don't
enjoy.

The "wanting" (dopamine) system is separate from the "liking" (opioid) system.

**Source**: [[Dopamine Nation - Book Notes]]

**Related**:
- [[Motivation vs willpower]]
- [[Reward prediction error]]
```

## Vault Safety Rules

These rules apply whenever modifying vault content:

- **Read before editing** - Always read a note before updating or deleting
- **Check backlinks before deleting** - Use Grep to find `[[Note Name]]` references across vault
- **Soft delete only** - Move to `07_Archive/Trash/`, never permanently delete
- **Preserve frontmatter** - Maintain YAML between `---` delimiters when editing
- **All files .md** - Obsidian only displays markdown files
- **AI content to staging** - Never write AI-generated insights directly to `02_Permanent/`

## Execution Context & Tool Selection

**Detecting Context:**
Check the working directory. If it shows the vault path, you're IN the vault. Otherwise, you're OUTSIDE.

| Operation | In Vault | Outside Vault |
|---|---|---|
| **File CRUD** | Local tools (`Glob`, `Read`, `Edit`, `Write`) | MCP obsidian (`mcp__obsidian__*`) |
| **Semantic Search** | MCP obsidian-graph (`search_notes`, `get_similar_notes`, etc.) | MCP obsidian-graph |

**Key:** Local tools are faster. MCP is needed for embeddings and vision regardless of location.

## MCP Servers

1. **obsidian** - Vault CRUD via Obsidian's Local REST API plugin (reads/writes files)
2. **obsidian-graph** - Semantic search, similarity, connection graphs, hub/orphan detection (pgvector-powered)
3. **MCP_DOCKER** - Docker Desktop's MCP gateway. Provides YouTube transcript pulling (`get_transcript`) and other utilities (optional)

## Decision Rules: Where Does Everything Go?

| Content Type | Destination |
|---|---|
| External source (article, book, video) | `01_Sources/[Category]/` |
| Extractable insight | `AI_Extracted_Notes/` (staging), then `02_Permanent/` after human review |
| Random thought | `00_Inbox/` -> review weekly -> extract or trash |
| Time-bound work | `04_Projects/[ProjectName]/` |
| Ongoing responsibility | `05_Life_Areas/[Area]/` |
| Draft article | `06_Output/Drafts/` |
| Finished article | `06_Output/Articles/` |
| Completed work | `07_Archive/` |
| No value | `07_Archive/Trash/` (never permanent delete) |

## Git Integration

**Commit strategy:**
- After each phase of work
- After discovery sessions (with changelog)
- After creating new MOCs
- Before major refactoring

**What's tracked:** Framework files (commands, agents, CLAUDE.md, templates, configs)
**What's gitignored:** Personal vault content (synced via iCloud/other)

## System Files

- `09_Meta/Templates/` - Note templates (Permanent, Source, MOC)
- `09_Meta/Changelogs/` - Session logs from discovery and connection work
- `09_Meta/Kindling-Quick-Reference.md` - Quick reference card

---

**The goal is insight accumulation and connection discovery, not information storage. Every note should be an atom of knowledge that connects to others, creating emergent understanding greater than the sum of its parts.**
