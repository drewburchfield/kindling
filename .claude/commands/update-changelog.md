---
description: Record what was discovered and decided during this session
allowed-tools: Read, Edit, Write
---

# Update Knowledge Graph Changelog

You are updating the vault changelog to track recent modifications to the knowledge graph.

## Your Task

1. **Identify Recent Changes** - Review the session history to identify:
   - New notes created
   - New connections/links added between existing notes
   - Significant edits to note content
   - Focus only on changes made during THIS session

2. **Read Existing Changelog** - Read `09_Meta/Changelogs/` for existing logs, or create a new dated file

3. **Create Session Entry** - Write a dated entry with:
   - Date and session identifier
   - List of changes in format: `- [ACTION] Note Title: Brief description (-> Connected to: [[Other Note]])`
   - Keep each entry to 1-2 sentences maximum
   - Use action verbs: CREATED, CONNECTED, UPDATED, LINKED, DISCOVERED

## Format Example

```markdown
## 2025-10-24 - Session [Brief Description]

- CONNECTED [[Psychological Safety]] -> [[Flow is impossible without Autonomy]]: Psychological safety creates autonomy prerequisite for flow by removing fear-based constraints.
- CONNECTED [[Radical Ownership]] -> [[Flow is impossible without Autonomy]]: True ownership requires autonomy; permission-seeking eliminates both.
- DISCOVERED [[Pleasure-Pain Balance]] <-> [[Prospect Theory]]: Both describe baseline-deviation adaptation dynamics across neuroscience and economics.
- CREATED [[Baseline-Deviation Pattern]]: Meta-principle synthesizing dopamine and prospect theory insights.
```

## Important Guidelines

- Only document changes from THIS session
- Be concise, max 2 sentences per change
- Use bidirectional arrows (<->) for mutual connections, directional (->) for one-way
- Group related changes together
- Focus on WHAT was connected and WHY it matters (the insight)
- If no changelog exists, create one in `09_Meta/Changelogs/`

## When to Run

Run this command after:
- `/find-connections` sessions (record what connections were discovered)
- `/discover` sessions (record cross-domain patterns found)
- `/inbox-processor-hybrid` sessions (record what was extracted and filed)
- Any session where notes were created or connected

## Output

After updating, show the user:
1. Number of changes logged
2. The new entry you added
3. Confirmation that the changelog was updated
