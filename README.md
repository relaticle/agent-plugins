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

## Claude's sales plugin on Relaticle

Anthropic publishes an open-source [sales plugin](https://github.com/anthropics/knowledge-work-plugins/tree/main/sales) for Claude. Its skills prepare calls, review deals and pipeline, write forecasts and account plans, and log follow-ups. Its connector notes say any MCP server in the CRM category works.

```bash
claude plugin marketplace add anthropics/knowledge-work-plugins
claude plugin install sales@knowledge-work-plugins
```

Connect Relaticle as described above. Then run a skill by name, for example `/sales:pipeline-review`.

### What we tested

On 2026-11-14 we ran every skill in version 2.1.0 once, in Claude Code. Each run used a fresh Relaticle workspace, loaded with the same invented companies, people, opportunities, notes and tasks. Relaticle was the only connector. The test ran on a local Relaticle server, on the same code the hosted service ran that day.

- Every skill finished. None ended in an error.
- The writes landed. `update-opportunity` changed a stage, an amount and a close date. `call-summary` created a note and a task. We read each change back in the database.
- Some runs named a missing calendar, mailbox or call recorder. Those runs still finished.
- Some calls used a filter or an include the server refused. Every run still finished.

One run per skill is a small sample. A second run of the same skill can answer differently.

### Attributes the skills ask for

A new workspace has three opportunity attributes: amount, close date and stage. Many skills look for more, and say so when one is missing. To add one, open Workspace Settings, then Custom attributes. You can also ask Rela, the built-in AI assistant. Rela proposes the attribute. A workspace owner or admin approves it. Attributes cannot be created over MCP.

| Record | Attribute | Skills that asked for it |
|---|---|---|
| Opportunity | Next Step | deal reviews, close plans, hygiene checks, briefings |
| Opportunity | Probability, Forecast Category | forecasts, weighted pipeline, slip scenarios |
| Opportunity | Owner, a select of your members | "my deals", pipeline by rep |
| Opportunity | Competitor, Loss Reason | competitive and win-loss reviews |
| Company | Industry, Employees | account tiering, lead triage |
| Company | Renewal Date, Health | renewal radar, customer health |

We ran those skills again on workspaces with these attributes filled. Most of them used the new attributes. `account-plan` saved its plan into the company Description and the opportunity Next Step. `pipeline-review` weighted the pipeline by Probability.

### Limits to know

- An opportunity can link to one person, with no roles.
- An opportunity has no owner of its own. The select attribute above stands in for it.
- There is no call or meeting record over MCP. A logged call is saved as a note, and a booked meeting as a task.
- The activity tool returns at most 30 days of changes.
- A write over MCP commits directly. It is scoped to the workspace you connected. The activity log records it.

## What these plugins connect to

The plugins contain no code. They only point your client at the Relaticle MCP server. Requests from your client go to `https://mcp.relaticle.com`, or to your own instance if you change the URL, and carry the access token from your sign-in. Revoke that access at any time in Relaticle under Settings, Access Tokens, AI Connectors. The [privacy policy](https://relaticle.com/privacy-policy) covers how Relaticle stores your CRM data.

## Self-hosted Relaticle

Every self-hosted instance serves its own MCP endpoint at `https://<your-domain>/mcp`. Replace the URL above with yours.

## Links

- MCP guide: https://relaticle.com/developers/mcp
- Source code: https://github.com/relaticle/relaticle
- Relaticle Cloud has a 14-day free trial. Self-hosting is free under AGPL-3.0.
