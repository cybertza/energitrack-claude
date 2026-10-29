# EnergiTrack for Claude

Monitor solar PV systems, solar production, energy consumption, batteries, grid energy, plant health and alarms. This plugin targets Claude chat (web, desktop and mobile), Cowork, and Claude Code (terminal, IDE and desktop Code). It bundles the production EnergiTrack remote MCP connector and three workflows: plant-check, energy and ems-change. Use your existing EnergiTrack account; current plant grants, consent and server availability determine what you can access. No account token or secret is included in the package. This package has not been submitted to Anthropic's public directory.

## Install in Claude chat or Cowork

1. Download `energitrack-claude-1.1.1.zip` from EnergiTrack's Agent connections page.
2. In Claude open Customize > Plugins > Add > Upload plugin and select the ZIP. In Cowork, open the Cowork tab before Customize if required.
3. Open the installed plugin's Connectors tab. Add or connect EnergiTrack. If you already connected the same server, use that existing connection instead of duplicating it.
4. Use `https://tars.energitrack.io/mcp`. If Claude cannot register automatically, choose Sign in now > Use your own OAuth client, enter public client ID `energitrack-claude-mcp-prod`, and leave Client Secret and Request headers blank. Sign in on EnergiTrack's own consent page, never in chat.
5. Review consent. Read access supports monitoring; Write and separate EMS consent support only eligible changes within your existing plant configuration permissions. Every applied EMS change needs a validated preview and your confirmation of the exact effects.
6. Ask Claude to list your plants. Open the plugin's workflows through `/` or the conversation's tools menu. Menus and plan/workspace policies may vary.

The production registration does not apply to development or custom endpoints. Team/Enterprise administrators may need to add the connector before members can sign in. Disconnect in Claude and revoke the OAuth authorisation in EnergiTrack to end access.

See [Connector documentation](docs/CONNECTOR.md) for OAuth scopes, data handling, permissions and verification steps.

## Claude Code

See INSTALL.md for the account-connector path, local plugin loading and duplicate-server handling. Claude Code sessions using an API key or another model provider need separate manual setup through EnergiTrack's Agent connections page. The plugin does not collect credentials from the local machine. The web OAuth client is not a local OAuth registration. Each authentication path still needs live acceptance on the intended client.

## Current boundaries

Tool discovery and client availability can differ. Check capabilities and actual tool discovery; plugin installation alone is not a successful connection. General self-service writes are currently disabled, and OAuth report creation/cancellation awaits worker authorisation support. No workflow enables telemetry deletion or alarm acknowledgement. Saved EMS settings do not prove device receipt or application. Missing telemetry and insufficient PV model coverage remain unknown.

Validation of package structure does not prove account sign-in, client tool execution, mobile/voice support or successful plant writes. Test these with an authorised account before relying on them. No operational write is required to test the read workflows.

## Rebuild

From the React repository run `python scripts/build_claude_plugin.py`. To check that the committed download matches the source, run `python scripts/build_claude_plugin.py --check`. Validate the source with `claude plugin validate ./plugins/energitrack-claude`.

Official reference: https://claude.com/docs/plugins/build

Copyright EnergiTrack (Pty) Ltd. All rights reserved. No open-source license is granted by this package; use of the connected service remains subject to your existing EnergiTrack terms.
