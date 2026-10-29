# Install across Claude experiences

The same plugin targets chat, Cowork and Claude Code. It contains commands and a fixed remote HTTP MCP reference; it has no local executable, hook or bundled credentials. Installation, authentication and actual tool-use acceptance are separate steps. Verify each experience your team uses.

## Chat: web, desktop and mobile

Install the ZIP at Customize > Plugins > Add > Upload plugin on Claude web or desktop. Open the plugin's Connectors tab and connect EnergiTrack. Use the server URL and public web client ID from README.md when Claude asks for custom OAuth settings. Review consent on EnergiTrack's own page.

Use the same Claude account and organization in the desktop or mobile app. Enable the connector for the conversation where offered. The command workflows load as skills in chat. Confirm in text that Claude can list your authorised plants; test mobile and voice separately. Do not assume an account-level installation proves every client can execute the tools.

## Cowork

Open Cowork in Claude Desktop, then Customize. The account plugin and its Connectors tab provide the same remote EnergiTrack connection. Connect with your own account and review consent. Run `/energitrack:plant-check`, `/energitrack:energy` or `/energitrack:ems-change` for the corresponding workflow. Team/Enterprise administrators may need to make the plugin and connector available first.

## Claude Code with a Claude account

1. Authenticate EnergiTrack at https://claude.ai/customize/connectors.
2. Sign in to Claude Code with that same claude.ai subscription account and organization. Start a new session and inspect `/mcp` for the claude.ai EnergiTrack connector. Terminal and supported IDE sessions can fetch account connectors; desktop Code sessions receive them through the desktop app. Availability depends on client version and organization controls.
3. An account-installed plugin can sync to Claude Code at the next session. For a local copy, extract the ZIP and run `claude --plugin-dir "/absolute/path/to/energitrack"`. The commands load as `/energitrack:plant-check`, `/energitrack:energy` and `/energitrack:ems-change`.
4. The bundled `.mcp.json` also offers a direct server. If that duplicate requests local OAuth or takes precedence over the working account connector, disable only the plugin's direct EnergiTrack server in `/mcp`; keep the plugin enabled for its workflows and use the claude.ai connector. Do not remove unrelated MCP servers.

The existing public Claude web OAuth registration accepts the web callback only. Do not reuse it for a local loopback redirect. A future direct OAuth setup needs a separately reviewed matching registration. Connector reuse avoids that requirement for Claude-account sessions.

## Claude Code with an API key or another model provider

These sessions do not inherit claude.ai connectors. Use a dedicated personal EnergiTrack token instead:

1. In EnergiTrack Agent connections, create or select a personal token with only the access you intend. Read is sufficient for monitoring. Write requires its separate approval and still follows your current plant permissions.
2. Store it securely in `ENERGITRACK_AGENT_TOKEN` in the environment that launches Claude Code. For an IDE, restart the extension host with that environment; for SSH or a remote session, set it on the remote host. Never paste the token into a plugin source file, a command line recorded in shell history, or chat.
3. Merge `mcpServers.energitrack-token` from `config/claude-code-token.json` into your existing project `.mcp.json`, preserving other servers. The packaged file contains an environment reference, not a real token. A missing environment variable must be supplied before connecting.
4. Load the workflows with `claude --plugin-dir "/absolute/path/to/energitrack"`. Disable the plugin's duplicate direct OAuth server in `/mcp` if necessary, then connect `energitrack-token` and list your plants.

Revoking this personal token and revoking the OAuth account connector are separate actions. No setup path grants new plant access automatically.

## Acceptance for each experience

Check actual discovered tools and get_connection_capabilities, list your authorised plants, then run a read-only plant check. Verify timestamp, unit and missing-coverage handling. Test a write only on an authorised sample plant after a specific requested change, a validated preview and confirmation of its exact effects. Saving EMS intent is not device application. No plant write is required to verify installation.

References:

- https://claude.com/docs/plugins/platform-support
- https://code.claude.com/docs/en/mcp#use-mcp-servers-from-claudeai
- https://code.claude.com/docs/en/mcp#environment-variable-expansion-in-mcpjson
