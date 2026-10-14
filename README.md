# QualifyBase for Claude

AI Lead Qualification for your QualifyBase workspace. This plugin pairs the QualifyBase connector with eight workflows for onboarding, Instagram setup, agent setup, prompt editing, lead review, conversation and campaign review, appointments, and weekly customer insights.

## Get started

1. Install the plugin, then open its **Connectors** tab and connect QualifyBase.
2. Sign in to QualifyBase as an administrator of the workspace you want to use. Review the permissions on the consent page before approving.
3. Ask Claude a question or use one of the commands below. A QualifyBase account and a configured workspace are required; available data depends on your connected channels, calendars, and account configuration.

| Command | Example request |
| --- | --- |
| `/qualifybase:account-setup` | Help me set up my QualifyBase workspace. |
| `/qualifybase:instagram-setup` | How do I connect Instagram to my agent? |
| `/qualifybase:agent-setup` | Help me configure a receptionist agent. |
| `/qualifybase:prompt-editing` | Review my current agent prompt and make its tone friendlier. |
| `/qualifybase:lead-review` | Which leads need attention, and why? |
| `/qualifybase:conversation-review` | Summarize this lead's conversations and calls. |
| `/qualifybase:appointments` | Find an available appointment tomorrow. |
| `/qualifybase:weekly-insights` | What did my leads struggle with last week? |

You can also describe your request naturally. Setup workflows guide you through the dashboard. The plugin does not connect Instagram or other integrations, create agents, send messages, start calls, or launch campaigns.

## Prompt previews

Agent prompt access is a separate optional permission. Existing connections retain their original 19 tools. Approving prompt access makes three additional tools available: `list_agents`, `get_agent_prompt`, and `preview_agent_prompt`. If they are absent, reconnect and review the requested permissions; you can still ask Claude to draft changes for the dashboard.

Claude reads the effective prompt from QualifyBase's stored agent configuration, previews exact replacements or additions, and shows you the proposed change. A changed revision or ambiguous replacement is rejected. These tools are read-only: they do not save a prompt or change a voice provider.

To apply a draft, open that agent's Playground → Instructions yourself. Review the current text before pasting; if it differs from the draft's original prompt, ask for a fresh preview first. Keep the greeting and other settings unchanged. Pause the agent before saving, test the affected scenario in a fresh Playground session, then resume when satisfied. Direct prompt saving through MCP is outside this release.

## Customer insights

Weekly insights use accessible chat messages and stored call transcripts to identify observed objections, questions, and booking barriers. Claude states the date range, timezone, sources, and coverage. Counts from lead analytics describe leads created in that period, not necessarily every lead who spoke during it.

Conversation discovery is capped at 100 threads, individual message fetches at 200 messages, and call lists at 200 calls without pagination. A report that reaches these limits is explicitly partial. For a complete workspace reporting view, open [AI Reporting](https://www.qualifybase.com/assistant), available to workspace administrators. The plugin does not manufacture reasons from qualification scores or claim missing transcripts were reviewed.

## Permissions and data

- **Read workspace data:** leads, qualification insights, conversations, calls, campaigns, calendars, and appointments.
- **Lead and appointment updates:** optional permission for changes the user requests. Booking changes can affect a connected external calendar.
- **Agent prompt access:** separate optional `qualifybase.prompts.read` permission for reading prompts and previewing edits. It grants no prompt-writing access.

The connector URL is `https://www.qualifybase.com/api/mcp`, the same URL as the QualifyBase directory connector. Use the existing connection where Claude offers it, so you have one set of tools.

The plugin contains instructions, metadata, and a brand icon. It contains no passwords, API keys, executable scripts, hooks, or local MCP servers. Tool calls go to QualifyBase; results become part of the Claude conversation. The prompt-preview tools make no requests to a voice provider. Disconnecting or revoking the OAuth connection removes future access. Never paste integration passwords or access tokens into chat.

## Development and support

The plugin bundle is licensed under MIT. QualifyBase service use is governed by its [Terms](https://www.qualifybase.com/terms) and [Privacy Policy](https://www.qualifybase.com/privacy). For help, use [QualifyBase Support](https://www.qualifybase.com/support).

Validate a local copy with `claude plugin validate --strict .`. Load it in Claude Code with `claude --plugin-dir .`, or zip the bundle and use **Customize → Plugins → Add → Upload plugin** in Claude. Validation checks the package structure; connected tool behavior also needs testing in your own workspace.
