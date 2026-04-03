---
description: Search your vault for what you already know, adapts depth to query complexity
argument-hint: <search query, topic, or question>
allowed-tools: Read, Grep, search_notes, get_similar_notes, get_connection_graph
---

# Knowledge Retrieval

You are tasked with retrieving relevant knowledge from the Obsidian vault. Adapt your depth based on the query.

## Search Query
$ARGUMENTS

## Mode Selection

**Simple query** (single topic, keyword, or short phrase): Use Quick Mode
**Complex query** (question, multi-topic, or "what do I know about X and Y"): Use Research Mode

---

## Quick Mode (Simple Queries)

1. **Semantic Search** using `search_notes`:
   - Query: $ARGUMENTS
   - Limit: 5 results
   - Threshold: 0.5

2. **Keyword Search** using `Grep`:
   - Pattern: $ARGUMENTS
   - Path: vault root
   - Output mode: "files_with_matches"

3. **Read top result** to show full content

**Output:**
```markdown
# Recall: [Query]

## Matches
[Notes with similarity scores + key excerpts]

## Top Result
[Full content of most relevant note]
```

---

## Research Mode (Complex Queries)

### Layer 1: Initial Search
- Use `search_notes` with the query (top 5, threshold 0.5)
- Use `Read` to read full content of top 2 results

### Layer 2: Direct Associations
- For the top result, use `get_similar_notes` (5 results, threshold 0.6)
- Read full content of top 2 similar notes

### Layer 3: Extended Network
- Build connection graph using `get_connection_graph` (depth=3, max_per_level=5, threshold=0.65)
- Reveals deeper conceptual connections

### Layer 4: Synthesis
After retrieval, analyze across all notes found:

- **Key Themes**: What patterns emerge across notes?
- **Contradictions/Tensions**: Where do ideas conflict?
- **Gaps**: What's missing from your vault on this topic?
- **Connections**: Surprising links between notes
- **Next Steps**: What to research, explore, or write next

**Output:**
```markdown
# Research: [Query]

## Layer 1: Direct Matches
[Notes with similarity scores and key excerpts]

## Layer 2: First-Degree Associations
[Similar notes with connections and excerpts]

## Layer 3: Extended Network
[Connection graph with relationship strengths]

## Synthesis

### Key Themes
[Patterns across notes]

### Contradictions
[Where ideas conflict or tension exists]

### Gaps
[What's missing, what to research next]

### Connections
[Surprising or non-obvious links]

### Recommended Next Steps
[Concrete actions: notes to create, topics to explore, things to write]
```

## Important Notes
- Focus on quality over quantity
- Highlight unexpected connections
- Provide enough context for the user to understand relevance
- If search returns no results, try broader terms or related concepts
