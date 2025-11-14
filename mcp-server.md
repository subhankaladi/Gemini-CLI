# Day 2 -- Connect GitHub MCP Server with Google Gemini CLI (Remote Server)

Today in Day 2, you will learn **how to connect the GitHub MCP Server to
the Gemini CLI using (Remote Server)**.\
This is the simplest and fastest method to get started.

------------------------------------------------------------------------

## 🔹 Prerequisites

Before starting, make sure you have:

1.  **Google Gemini CLI installed**\
2.  **GitHub Personal Access Token (PAT)**\
    Create your token here:\
    https://github.com/settings/personal-access-tokens/new
3.  **No Docker required**\
    (Because we use the hosted MCP server)

------------------------------------------------------------------------

## 🔹 Step 1 --- Store Your PAT Securely

Do NOT hardcode your PAT in the settings file.

Create this file:

    ~/.gemini/.env

Add:

``` bash
GITHUB_MCP_PAT=your_token_here
```

This keeps your PAT secure.

------------------------------------------------------------------------

## 🔹 Step 2 --- Configure GitHub MCP Server (Method 2)

Now open your Gemini settings file:

    ~/.gemini/settings.json

If this file doesn't exist, create it.

Paste the following configuration:

``` json
{
    "mcpServers": {
        "github": {
            "httpUrl": "https://api.githubcopilot.com/mcp/",
            "headers": {
                "Authorization": "Bearer $GITHUB_MCP_PAT"
            }
        }
    }
}
```

### What this does:

-   `httpUrl` connects Gemini CLI to the GitHub Hosted MCP Server.
-   `Authorization` automatically loads your token from `.env`.

------------------------------------------------------------------------

## 🔹 Step 3 --- Restart Gemini CLI

Restart Gemini CLI to apply changes:

    gemini

------------------------------------------------------------------------

## 🔹 Step 4 --- Verify the Connection

Run:

    /mcp list

Expected output:

    🟢 github - Ready (90+ tools)

If you see this --- your MCP server is connected!

------------------------------------------------------------------------

## 🔹 Step 5 --- Test the Server

Run a simple test command:

    List my GitHub repositories

If your repositories appear → everything is working correctly 🎉

------------------------------------------------------------------------

## 🔹 Troubleshooting

### ❌ Invalid or Expired Token

-   Regenerate your PAT
-   Required scopes:
    -   `repo`
    -   `read:packages` (optional, for Docker usage)

### ❌ Invalid JSON

Validate your settings file:

    cat ~/.gemini/settings.json | jq .

Fix any formatting issues.

### ❌ Server Not Connecting

Run debug mode:

    gemini --debug "hello"

Logs will show the exact reason.

------------------------------------------------------------------------

## 🎉 Outro

This was **Day 2**, where we connected the GitHub MCP Server to the
Gemini CLI using **(Remote Server)**.

**Day 3** will cover how to actually use MCP tools inside real workflows
and projects.
