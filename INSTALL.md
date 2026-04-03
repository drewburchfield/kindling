# Installation

## Prerequisites

```bash
node --version    # 18+
docker --version  # For MCP servers
```

You also need:
- [Obsidian](https://obsidian.md) installed
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) installed
- The [Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api) Obsidian plugin enabled

<br>

## 1. Clone the Repository

```bash
git clone https://github.com/drewburchfield/kindling.git
cd kindling
```

<br>

## 2. Open as an Obsidian Vault

In Obsidian: **File > Open Vault > Open folder as vault** and select the cloned directory.

Enable the Local REST API plugin:
1. Settings > Community Plugins > Browse
2. Search "Local REST API"
3. Install and enable
4. Copy the API key from the plugin settings

<br>

## 3. Configure MCP Servers

Copy the template and fill in your values:

```bash
cp .mcp.json.template .mcp.json
```

Edit `.mcp.json`:

```json
{
  "mcpServers": {
    "obsidian": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "-e", "OBSIDIAN_HOST", "-e", "OBSIDIAN_API_KEY", "mcp/obsidian"],
      "env": {
        "OBSIDIAN_HOST": "host.docker.internal",
        "OBSIDIAN_API_KEY": "your-api-key-from-step-2"
      }
    },
    "obsidian-graph": {
      "command": "docker",
      "args": ["exec", "-i", "mcp-obsidian-graph", "python", "-m", "src.server"],
      "disabled": false
    }
  }
}
```

**Two required servers, one optional:**

| Server | What it does | Setup |
|---|---|---|
| **obsidian** | Reads/writes files in your vault via Obsidian's REST API | Uses the API key from step 2 |
| **[obsidian-graph](https://github.com/drewburchfield/obsidian-graph)** | Semantic search, connection graphs, hub/orphan detection (pgvector) | See the [obsidian-graph repo](https://github.com/drewburchfield/obsidian-graph) for Docker setup |
| **[Docker MCP gateway](https://docs.docker.com/desktop/features/gordon/mcp-catalog/)** | YouTube transcript pulling and other utilities | Optional. Requires Docker Desktop with MCP gateway enabled |

<br>

## 4. Configure Claude Code Settings

```bash
cp .claude/settings.local.json.template .claude/settings.local.json
cp .claude/settings.md.template .claude/settings.md
```

Edit `.claude/settings.md` and set your vault path:

```
VAULT_BASE_PATH=/path/to/your/kindling
```

Edit `.claude/settings.local.json` and replace `YOUR_VAULT_PATH_HERE` with your actual path.

<br>

## 5. Verify

Start Claude Code from the vault directory:

```bash
claude
```

Test semantic search:
```
/recall test
```

Test file access:
```
/analyze-kb
```

If both work, you're set.

<br>

## Troubleshooting

**"MCP server not found"**
- Verify Docker is running: `docker ps`
- Check `.mcp.json` has correct server names and paths
- Restart Claude Code after config changes

**"Permission denied reading vault"**
- Check vault path in `.claude/settings.local.json`
- Use absolute paths (e.g., `/Users/name/kindling`)
- Verify file permissions: `ls -la /path/to/vault`

**Semantic search returns no results**
- Ensure the obsidian-graph container is running: `docker ps | grep obsidian-graph`
- The graph server needs time to index on first run
- Try broader search terms

**Commands not showing up**
- Verify `.claude/commands/` directory exists with `.md` files
- Restart Claude Code

<br>

## What's Tracked vs. Ignored

The `.gitignore` separates your **framework** (tracked) from your **personal notes** (ignored):

| Tracked | Ignored |
|---|---|
| `.claude/commands/`, `.claude/agents/` | `00_Inbox/*` through `08_Attachments/*` |
| `CLAUDE.md`, templates, config templates | `AI_Extracted_Notes/*` |
| `.gitignore`, `LICENSE`, docs | `.mcp.json`, `settings.local.json`, `settings.md` |

Your notes sync however you prefer (iCloud, Dropbox, Syncthing, etc.).

<br>

## Updating

```bash
git pull origin main
```

Your personal config files are gitignored and won't be overwritten. If templates change, diff them:

```bash
diff .mcp.json .mcp.json.template
diff .claude/settings.local.json .claude/settings.local.json.template
```

<br>

## Uninstalling

This system is non-destructive. To remove:

1. Delete the `.claude/` directory
2. Delete `CLAUDE.md` and the doc files
3. Your notes in `00_Inbox/` through `07_Archive/` are untouched
