# EnergiTrack solar PV and energy connector

EnergiTrack connects Claude to the solar PV and energy systems your existing EnergiTrack account can access. An active EnergiTrack subscription and authorised plant access are required. Available readings depend on each plant's equipment, configuration, mappings and retained telemetry.

## Connect

The production remote MCP endpoint is `https://tars.energitrack.io/mcp`. Use OAuth sign-in with public client ID `energitrack-claude-mcp-prod`; no client secret or additional request headers are required. Complete sign-in on EnergiTrack's own page. Never put an account password or token into a conversation.

The supported OAuth scopes match the OpenAI plugin:

| Scope | Purpose |
| --- | --- |
| `mcp:read` | Read supported monitoring data and redacted EMS configuration for authorised plants. |
| `mcp:write` | Optional consent for supported changes; existing feature gates and permissions still apply. |
| `mcp:ems:write` | Separate optional consent for EMS configuration changes, also requiring `mcp:write` and existing EMS edit rights. |
| `offline_access` | Refresh authorisation without repeatedly signing in, where supported by the client. |

The server advertises these options during sign-in. Leave both Write and EMS options unchecked on the EnergiTrack consent page for read-only access. Broader OAuth consent never adds plant grants or overrides company, site, plant or configuration permissions. An existing read-only connection must sign in again to choose additional consent; updating a plugin does not expand an existing token.

## Monitoring and supported changes

Read workflows cover fleet health, solar PV production, consumption, battery/grid measurements, power flow, historical energy, forecasts, alarms, incidents, inventory, mappings and EMS diagnostics where available. Responses retain timestamps, units, freshness and coverage. Missing readings are not measured zero, and insufficient PV model coverage cannot establish a performance-ratio verdict.

For an EMS change, specify the exact supported change, inspect its validated preview, and explicitly confirm its effects before applying. The service rechecks permissions and records the action. Saved active configuration is separate from device receipt or application. Monitoring requests do not apply changes.

General self-service writes remain disabled, and creating or cancelling reports through OAuth is not yet supported. The connector does not offer telemetry deletion or alarm acknowledgement. Claude tool approval settings are separate from EnergiTrack OAuth consent; keep operational changes individually approved.

## Data handling and disconnection

The connector calls EnergiTrack's production APIs. Only the user's authorised results are returned to Claude through the declared MCP endpoint. The plugin contains static workflow instructions and connector configuration, with no bundled credentials, executable background service or independent telemetry collector. The connected service retains its existing access controls, audit records and service data policies.

Disconnect EnergiTrack in Claude and revoke its OAuth authorisation in EnergiTrack to end access. Removing the plugin alone should not be treated as confirmed revocation of a separately connected account.

## Supported Claude experiences

The plugin targets Claude chat on web, desktop and mobile, Cowork, and Claude Code on terminal, IDE and desktop Code. Availability depends on the client's plugin support, subscription and workspace policy. Claude Code sessions signed in with a Claude subscription can reuse account connectors. API-key or other-provider sessions use the explicit manual token configuration described in [INSTALL.md](../INSTALL.md); the plugin does not read environment credentials automatically. Each intended client still requires sign-in and a successful authorised tool call before being considered verified.

## Verify and get help

Start by listing authorised plants, then inspect one permitted plant's mapped readings and capabilities. Check timestamps, units, coverage and the actual enabled tools. Test read-only denial of writes and inaccessible targets without making operational changes. Package validation, tool discovery and a successful read do not establish device application or acceptance of every tool on every client.

Support: support@energitrack.com or https://support.energitrack.com/.

Privacy policy: https://www.energitrack.com/policies/index.html#privacy.

Service terms: https://www.energitrack.com/policies/index.html#terms.
