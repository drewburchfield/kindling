# Kindling - Quick Reference

## Commands

| Your state of mind | Command | What it does |
|---|---|---|
| "I have stuff piling up" | `/inbox-processor-hybrid` | Triage inbox items, extract insights to staging |
| "I just added a note, what connects?" | `/find-connections <note>` | Map conceptual network around a note |
| "What patterns am I missing?" | `/discover` | Vault-wide cross-domain pattern hunting |
| "What do I already know about X?" | `/recall <topic>` | Semantic search, adapts depth to complexity |
| "Help me think through X" | `/thinking-partner <topic>` | Socratic exploration |
| "Make this sound like me" | `/de-ai-ify <file>` | Remove AI voice, restore human language |
| "What did I do today?" | `/daily-review` | End-of-day capture |
| "What happened this week?" | `/weekly-synthesis` | Weekly patterns and energy audit |
| "Log what was discovered" | `/update-changelog` | Record session connections and decisions |
| "Switch vaults" | `/switch-brain <path>` | Update config for different vault |
| "Vault health check" | `/analyze-kb` | Generate structure report |

---

## Workflow Chains

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

---

## Where Does It Go?

**"Is this building knowledge or managing action?"**

- Building knowledge: `01_Sources -> 02_Permanent -> 03_MOCs -> 06_Output`
- Managing action: `04_Projects` (deadline) or `05_Life_Areas` (ongoing)

| Content | Destination |
|---|---|
| Source material | `01_Sources/[Category]/` |
| Extractable insight | `AI_Extracted_Notes/` (staging) |
| Your original insight | `02_Permanent/YYYYMMDD-Title.md` |
| Time-bound work | `04_Projects/` |
| Ongoing responsibility | `05_Life_Areas/` |
| Published/synthesized | `06_Output/` |
| Completed | `07_Archive/` |
| No value | `07_Archive/Trash/` |

---

## Voice Preservation

1. AI extracts to `AI_Extracted_Notes/` with #ai-extracted tag
2. You review and rewrite in your voice
3. Run `/de-ai-ify` if needed
4. Promote to `02_Permanent/` when ready

---

## Permanent Note Format

- Title states the insight
- 50-300 words, your voice
- YYYYMMDD prefix
- Links to related notes
- Source attribution

---

## Suggested Rhythm

| When | What | Time |
|---|---|---|
| Throughout day | Capture to `00_Inbox/` | Seconds |
| Evening | `/daily-review` | 5 min |
| Weekly | `/inbox-processor-hybrid` + `/weekly-synthesis` | 30 min |
| Monthly | `/analyze-kb` + `/discover` | 1 hour |
