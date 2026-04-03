---
description: Triage inbox items one at a time, extract insights to staging
allowed-tools: Read, Write, Edit, Glob, Grep, search_notes, get_similar_notes, mcp__MCP_DOCKER__get_transcript
---

# Process Inbox

Process items in `00_Inbox/` one at a time.

## CRITICAL: Before Starting

1. **Read CLAUDE.md** - Refresh understanding of folder structure and voice preservation rules
2. **One item at a time** - Present each file individually, wait for user decision
3. **Read content thoroughly** - Actually read the full content before proposing triage
4. **Never permanently delete** - Use `07_Archive/Trash/` for soft deletes
5. **Pull YouTube transcripts** - If item contains a YouTube URL, pull transcript using MCP before processing

## Process

1. **Scan Inbox**
   - List all files in `00_Inbox/` (flat structure)
   - Show one file at a time for triage

2. **For Each Item:**
   - **Read the full content** before making any recommendation
   - **If YouTube URL present**: Pull transcript via `mcp__MCP_DOCKER__get_transcript` (requires [Docker Desktop MCP gateway](https://docs.docker.com/desktop/features/gordon/mcp-catalog/)), append to file, then process with full context. If unavailable, skip transcript and process with the URL alone.
   - **Contextualize**: Quick `search_notes` on the item's main topic to understand what the vault already covers. This helps you make smarter filing and extraction suggestions.
   - Present a summary of what the content contains
   - Ask: Is this building knowledge or managing action?

3. **Apply Decision Rules**

   **Knowledge Building:**
   - External source (article, book, video)? → `01_Sources/[Category]/`
   - Has extractable insight? → Suggest title, but **do NOT write to 02_Permanent/**
   - **Before extracting:** Search vault for existing coverage using `search_notes`
     - If similar note exists (similarity > 0.75): Show the existing note and ask if this adds a genuinely new angle
     - Different context/domain/framing? → Extract as new note
     - Same core concept, different wording? → Skip or suggest updating existing note
   - If user approves extraction → AI writes to `AI_Extracted_Notes/` with #ai-extracted tag
   - User reviews and rewrites before promoting to `02_Permanent/`

   **Action Management:**
   - Has deadline? → `04_Projects/[ProjectName]/`
   - Ongoing area? → `05_Life_Areas/[Area]/`
   - Completed? → `07_Archive/`

   **Output Content:**
   - Draft post/article? → `06_Output/Drafts/`
   - Finished piece? → `06_Output/Articles/`

   **No Value:**
   - Move to `07_Archive/Trash/` (NEVER permanent delete)

4. **Output Format**

   For each file:
   ```
   File: [filename]
   Content Summary: [2-3 sentences of what's actually in the file]
   Type: [knowledge/action/output/trash]
   Decision: [destination folder]
   Reason: [why this destination]
   Extract insight? [yes/no]
   - If yes: Suggested insight title(s)
   - Destination: AI_Extracted_Notes/ (user reviews before 02_Permanent/)
   ```

5. **After Processing**
   - User reviews `AI_Extracted_Notes/` and rewrites in their voice
   - User promotes to `02_Permanent/` if appropriate
   - Run `/find-connections` on new permanent notes
   - Update relevant MOCs

## Voice Preservation Rules (from CLAUDE.md)

**AI should NOT generate content when:**
- Processing inbox (suggest categories, don't rewrite)
- User hasn't explicitly requested writing

**If AI extracts insights:**
1. Write to `AI_Extracted_Notes/` (not `02_Permanent/`)
2. Tag with #ai-extracted
3. User reviews and rewrites in their own voice
4. User moves to `02_Permanent/` if approved

## Remember

- **Read before recommending** - understand what's in each file
- **Trash, not delete** - use `07_Archive/Trash/`
- **AI_Extracted_Notes/ first** - never write directly to `02_Permanent/`
- **One at a time** - wait for user approval before next item
- Most fleeting thoughts → Trash (that's okay!)
- Insights are rare - be selective
- Sources need attribution
- Preserve user's authentic voice
