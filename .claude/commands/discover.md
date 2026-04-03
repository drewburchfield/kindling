---
description: Surface non-obvious cross-domain patterns across your vault, run when you want to be surprised
argument-hint: [optional question or theme to focus discovery]
allowed-tools: Read, Grep, Glob, search_notes, get_similar_notes, get_connection_graph, get_hub_notes, get_orphaned_notes
---

# Cross-Domain Discovery

You are hunting for **non-obvious, cross-domain connections** in the knowledge base. Your specialty is finding meaningful relationships between notes from completely different areas that semantic similarity alone would miss.

## Focus (Optional)
$ARGUMENTS

If no focus is provided, sample broadly across the vault. If a question or theme is given, use it to guide which clusters to sample from, but still look ACROSS domains.

## Core Philosophy

**CRITICAL DISTINCTION:**
- **NOT your job:** Find semantically similar notes (clustering similar content)
- **YOUR JOB:** Find conceptually related notes across different domains that share:
  - Structural patterns (same architecture, different domain)
  - Causal mechanisms (same underlying process)
  - Meta-principles (same deep truth manifesting differently)
  - Paradoxes (apparent contradictions revealing complexity)
  - Analogical relationships (X in Domain A works like Y in Domain B)

**The Jackpot:** Low semantic similarity (0.50-0.70) + strong conceptual connection = the most valuable discovery. This means you found something non-obvious.

**Example of what you're looking for:**
- "Dopamine baseline vs. peaks" (Neuroscience) and "Reference points in Prospect Theory" (Economics) = **Same pattern: baseline-deviation dynamics**
- "Self is an illusion" (Buddhism) and "Ego dissolution in flow states" (Psychology) = **Same mechanism: loss of self-awareness**
- "Confirmation bias reinforces beliefs" (Cognitive Science) and "Social media algorithms amplify polarization" (Technology) = **Same principle: positive feedback loops**

## Operational Protocol

### Phase 1: Strategic Sampling (Diverse Selection)

**Objective:** Select notes from maximally different domains to find cross-domain connections

**Process:**
1. Use `Glob` to get vault inventory across folders
2. Identify major thematic clusters from the folder structure
3. **Randomly sample 2-3 notes from DIFFERENT clusters**
   - Example: 1 from neuroscience, 1 from economics, 1 from Buddhism
   - Avoid sampling from the same folder
4. Read full content of sampled notes using `Read` tool
5. Use `get_hub_notes` and `get_orphaned_notes` for vault context

### Phase 2: Conceptual Structure Analysis

**For each sampled note, extract:**

**Surface Content:**
- What is this note about? (topic)
- What domain does it belong to? (field)

**Deep Structure:**
- What pattern does it describe? (structure)
- What mechanism does it explain? (process)
- What principle does it embody? (abstraction)
- What tension/paradox does it reveal? (contradiction)

**Meta-Patterns to Look For:**
- **Dual process conflicts:** Fast vs. slow, control vs. letting go, conscious vs. unconscious
- **Illusion generation:** How perception/understanding is systematically distorted
- **Baseline-deviation dynamics:** Reference points, regression to mean, homeostasis
- **Positive/negative feedback loops:** Amplification, dampening, equilibrium-seeking
- **Emergence:** How micro-level processes create macro-level phenomena
- **Paradoxes:** Apparent contradictions that reveal complexity

### Phase 3: Cross-Domain Pattern Matching

**CRITICAL: This is where you apply REASONING, not just similarity scores**

**Process:**
1. Take notes from different domains (e.g., Neuroscience note + Economics note)
2. **Ask analytical questions:**
   - Do they describe the same structural pattern in different contexts?
   - Do they explain the same type of mechanism?
   - Do they both instantiate a deeper principle?
   - Do they contradict each other in a revealing way?
   - Would understanding one illuminate the other?

3. **Use semantic similarity as a SECONDARY check:**
   - If you identify a conceptual connection through reasoning
   - Verify with `get_similar_notes`
   - **Low semantic similarity (0.50-0.70) + strong conceptual connection = JACKPOT**
   - This means you found something non-obvious!

4. **Validate the connection:**
   - Can you explain WHY these connect in 2-3 clear sentences?
   - Does the connection reveal new insight?
   - Would a human reader say "Aha! I never thought of it that way"?

### Phase 4: Connection Documentation

**For each strong connection discovered, document:**

```markdown
## CROSS-DOMAIN CONNECTION DISCOVERED

**Node A**: [[Note from Domain X]]
**Node B**: [[Note from Domain Y]]
**Semantic Similarity**: 0.XX (low/medium, indicates non-obvious connection)
**Conceptual Strength**: (1-5 star rating based on your analysis)
**Discovery Method**: Cross-domain pattern analysis

---

### The Non-Obvious Link

[2-3 sentences explaining the connection in clear, compelling language]

**Shared Pattern/Mechanism/Principle:**
[What deeper structure or process they both instantiate]

---

### Why This Matters

[What insight this connection unlocks, what can we now understand that we couldn't before?]

---

### Evidence from Each Domain

**From [[Node A]] (Domain X):**
- Key concept: [Specific element from the note]
- How it works: [Mechanism or pattern]

**From [[Node B]] (Domain Y):**
- Key concept: [Specific element from the note]
- How it works: [Mechanism or pattern]

**Structural Mapping:**
- Element X in Domain A maps to Element Y in Domain B
- Process P in Domain A maps to Process Q in Domain B
- Outcome O in Domain A maps to Outcome O' in Domain B

---

### Synthesis Opportunity

**Potential New Note Title**: "[[Pattern Name: Cross-Domain Principle]]"

**Content would integrate:**
- Insights from [[Node A]]
- Insights from [[Node B]]
- The meta-principle they both demonstrate
- Examples from both domains
- Implications for other areas
```

### Phase 5: Iteration & Depth

1. **For each strong connection found:**
   - Use `get_connection_graph` on BOTH nodes (depth=2, max_per_level=5, threshold=0.6)
   - Record the actual graph structure returned

2. **Look for triangulation patterns:**
   - Do Node A and Node B both connect to a third node C from yet another domain?
   - Use the connection graph data to identify shared neighbors

3. **Identify consilience zones:**
   - 3+ independent domains converging = high-confidence meta-pattern
   - Map the complete network topology discovered

4. **Document as "Emergent Meta-Patterns"**

## Specialized Techniques

### Technique 1: Contrastive Analysis
**Find notes with opposite conclusions but same underlying structure**
- Example: "Control enables success" vs. "Letting go enables success"
- Paradox reveals context-dependence or multi-level truth

### Technique 2: Mechanism Transfer
**Identify mechanisms in one domain that could explain phenomena in another**
- Example: Dopamine reward prediction error (neuroscience) explains addiction (psychology) explains social media engagement (technology)

### Technique 3: Scale Bridging
**Connect micro and macro levels**
- Example: Individual confirmation bias leads to group polarization leads to societal division
- Same mechanism at different scales

### Technique 4: Temporal Bridging
**Connect early insights to recent ones**
- How has thinking evolved?
- Are there contradictions revealing growth?

## Quality Standards

### GOOD Connections (Document These):
- Structural isomorphism across domains
- Shared causal mechanisms in different contexts
- Meta-principles manifesting in multiple fields
- Low semantic similarity (0.50-0.70) + clear conceptual link
- "Aha!" factor, reveals non-obvious insight
- Actionable synthesis opportunities

### POOR Connections (Skip These):
- High semantic similarity (0.85+), too obvious
- Same domain, similar topics, not cross-domain
- Surface-level keyword overlap without deep structure
- Already explicitly linked in the vault
- Forced or contrived relationships
- Generic connections that don't unlock new understanding

## Output Format

```markdown
# Discovery Run: [Date]

## Sampling Strategy
[Which clusters sampled, why these were chosen]

## Analysis Summary
[Overview of what was analyzed and approach taken]

## Discoveries
[Detailed connection documentation as per Phase 4 format]

## Emergent Patterns
[Meta-patterns identified across multiple connections]

## Synthesis Opportunities
[Potential new notes or articles to create]

## Session Learnings
[What this run revealed about the knowledge graph structure]
```

## After Discovery

Run `/update-changelog` to record findings and decisions made during this session.

## Success Metrics

A good discovery session:
- Found 3+ non-obvious connections with actual similarity scores < 0.70
- Identified 1-2 emergent meta-patterns with connection graph data
- Discovered at least 1 consilience zone (3+ domains converging)
- Generated 2+ actionable synthesis opportunities

**What "Success" Looks Like:**
> "I found that [[Pleasure-Pain Balance in Dopamine System]] (neuroscience) and [[Reference Point Dependence in Prospect Theory]] (economics) have a semantic similarity of only 0.63, but both describe the SAME homeostatic mechanism:
> 1. Establish a baseline/reference point
> 2. Measure deviations (peaks/losses vs. baseline)
> 3. Adapt the baseline over time (tolerance/adaptation)
> 4. Create hedonic treadmill / diminishing sensitivity
>
> This reveals meta-principle: 'Baseline-Deviation Adaptation Dynamics' appearing across neuroscience, economics, and decision-making."

## Error Handling

- If vault access fails, log error and exit gracefully
- If no cross-domain connections found in sample, try different clusters
- If all connections are high similarity (0.80+), note this and recommend broader sampling
- If unsure about connection quality, document as "Hypothesis, needs human review"

---

**Remember:** You are hunting for the **hidden architecture of knowledge**, the deep patterns that connect superficially different domains. Semantic similarity is your starting point, but **your reasoning and analysis** is what finds the gold.

Every session should reveal something non-obvious that makes the user think: "I never connected those ideas before, but now I see how they're deeply related."
