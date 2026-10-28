# Relaticle agent plugins

Connect Claude, Cursor and Gemini CLI to [Relaticle](https://relaticle.com), the open-source CRM your AI agents can read and update: companies, people, opportunities, tasks, notes and custom fields.

Every plugin here points at the hosted MCP server, `https://mcp.relaticle.com`, which uses OAuth sign-in. Each connection is scoped to one Relaticle workspace.

## Claude

Install Relaticle from your organization's plugin library or the Claude directory. The plugin adds one remote MCP server, `https://mcp.relaticle.com`, to Claude. Claude asks you to sign in to Relaticle the first time it connects.

In Claude Code:

```
/plugin install relaticle --marketplace relaticle/agent-plugins
```

## Cursor

Install Relaticle from the Cursor Marketplace, or add this to `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "relaticle": {
      "url": "https://mcp.relaticle.com"
    }
  }
}
```

## Gemini CLI

```bash
gemini extensions install https://github.com/relaticle/agent-plugins
```

## What these plugins connect to

The plugins contain no code. They only point your client at the Relaticle MCP server. Requests from your client go to `https://mcp.relaticle.com`, or to your own instance if you change the URL, and carry the access token from your sign-in. Revoke that access at any time in Relaticle under Settings, Access Tokens, AI Connectors. The [privacy policy](https://relaticle.com/privacy-policy) covers how Relaticle stores your CRM data.

## Self-hosted Relaticle

Every self-hosted instance serves its own MCP endpoint at `https://<your-domain>/mcp`. Replace the URL above with yours.

## Links

- MCP guide: https://relaticle.com/developers/mcp
- Source code: https://github.com/relaticle/relaticle
- Relaticle Cloud has a 14-day free trial. Self-hosting is free under AGPL-3.0.
