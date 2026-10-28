# Relaticle agent plugins

Connect Cursor and Gemini CLI to [Relaticle](https://relaticle.com), the open-source CRM your AI agents can read and update: companies, people, opportunities, tasks, notes and custom fields.

Both plugins point at the hosted MCP server, `https://mcp.relaticle.com`. Your client signs you in with OAuth the first time it connects, and the connection is scoped to the workspace you pick.

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

Then run `/mcp auth relaticle` to sign in.

## Self-hosted Relaticle

Every self-hosted instance serves its own MCP endpoint at `https://<your-domain>/mcp`. Replace the URL above with yours.

## Links

- MCP guide: https://relaticle.com/developers/mcp
- Source code: https://github.com/relaticle/relaticle
- Relaticle Cloud has a 14-day free trial. Self-hosting is free under AGPL-3.0.
