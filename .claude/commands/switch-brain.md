---
description: Switch to a different Obsidian vault by updating configuration files
argument-hint: <full path to vault>
allowed-tools: Read, Edit
---

# Switch Brain Command

Switch the active Obsidian vault by updating all configuration files to point to a new vault path.

## New Vault Path
$ARGUMENTS

## Instructions

1. **Validate the path format:**
   - Ensure $ARGUMENTS is a full absolute path
   - If the path looks invalid or incomplete, ask the user to provide the full path

2. **Update `.claude/settings.md`:**
   - Read the settings.md file in this project's `.claude/` directory
   - Replace the `VAULT_BASE_PATH=` value with: `VAULT_BASE_PATH=$ARGUMENTS`
   - Use the Edit tool to make this change

3. **Update `.mcp.json`:**
   - Read the `.mcp.json` file in this project's root
   - Update vault path references in the MCP server configurations:
     - `obsidian` server: Update any vault path arguments
     - `obsidian-graph` server: Update if it contains vault path references
   - Use the Edit tool to update all occurrences

4. **Confirm completion:**
   - Display a summary of what was changed
   - Show the new vault path that's now configured
   - **IMPORTANT**: Display this final message to the user:

```
Vault configuration updated.

New vault path: $ARGUMENTS

RESTART REQUIRED: You must restart Claude Code for MCP server changes to take effect.
```

## Notes
- This command updates both the settings and MCP server configuration
- Changes only take effect after restarting Claude Code
- Make sure the specified vault path exists and contains a `.obsidian` folder
