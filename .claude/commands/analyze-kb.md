---
description: Analyze knowledge base structure and generate a condensed health report
allowed-tools: Read, Glob, Grep, Bash, search_notes, get_similar_notes, get_connection_graph, get_hub_notes, get_orphaned_notes
---

Analyze the Obsidian knowledge base structure and regenerate a **condensed, manageable** analysis report.

Follow these steps:

1. Get vault topology using `get_hub_notes` and `get_orphaned_notes`
2. List all notes with full directory tree using `Glob`:
   - All notes: `**/*.md`
   - Permanent notes: `02_Permanent/*.md`
   - MOCs: `03_MOCs/*.md`
   - Sources: `01_Sources/**/*.md`
   - AI Extracted: `AI_Extracted_Notes/*.md`
3. Read key hub notes from major clusters using `Read` tool
4. Use `get_similar_notes` to identify highly connected notes
5. Use `get_connection_graph` to map relationship networks
6. Analyze thematic clusters, hierarchical organization, and conceptual architecture
7. Use `Edit` or `Write` to create/update `09_Meta/knowledge-base-analysis.md` with a **condensed report** (target: ~600-800 lines max):
   - Executive summary with key statistics
   - Hierarchical structure mapping (condensed)
   - Major thematic hubs with hub nodes (core thesis + key notes only)
   - Network properties and connectivity (metrics + critical bridges)
   - Content topology and source analysis (top-tier influences only)
   - Intellectual trajectory and maturity assessment (phases + current focus)
   - Recommendations for enhancement (high priority only)

**CRITICAL OUTPUT REQUIREMENTS:**

- **Length target:** 600-800 lines maximum
- **Prioritize:** Core insights, actionable frameworks, critical statistics, key bridge notes
- **Eliminate:** Excessive examples, redundant explanations, verbose elaborations
- **Focus:** What's unique, what's actionable, what's growing, what's next
- **Style:** Bullet points over paragraphs, tables over lists where appropriate
- **No duplication:** Say things once, clearly, then move on

Generate a **condensed, scannable, high-signal** report that reveals the knowledge base's personality, cognitive fingerprint, and growth opportunities without overwhelming detail.
