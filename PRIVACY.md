# Qonto Matchmaker — Data and Privacy Notice

Effective: 22 July 2026

This notice describes the data flow of the Qonto Matchmaker plugin in this
repository. It supplements Fizard's general website and app privacy documents;
those documents have their own stated scope.

## Where processing happens

The plugin consists of instructions, user-interface metadata, and a
configuration for Qonto's official MCP endpoint. It has no Fizard-operated
backend for invoice matching and includes no Fizard analytics or telemetry.
The plugin itself does not transmit mailbox contents, invoice files, or Qonto
transaction data to Fizard.

Data is processed by the services and execution environment the user chooses:

- the Claude Code, Claude Cowork, or Codex surface running the plugin;
- the user's selected mail provider or mail connector;
- Qonto's MCP service and signed upload infrastructure; and
- GitHub for the plugin's best-effort version check and updates.

Those providers' privacy, retention, regional-processing, and administrator
policies apply independently. A community MCP server is an additional third
party chosen by the user and is not operated or audited by Fizard.

Cowork tasks run in an isolated execution environment on Anthropic's servers.
Its shell, temporary files, and remote connectors are therefore processed in
Anthropic's cloud even when the task starts in the desktop app. Qonto's bundled
remote MCP endpoint is reached from that cloud environment.

## Data used

Depending on the selected mode and connected tools, the plugin may access:

- Qonto organization, account, membership, card, transaction, and attachment
  metadata;
- existing Qonto attachment bytes for a narrow duplicate check on competing
  transactions, without auditing their accounting correctness;
- email search results, message metadata, and PDF attachment bytes;
- invoice data needed for matching, such as amount, currency, issuer, invoice
  number, date, billing period, and recipient identity; and
- short-lived Qonto upload URLs and blob references.

The plugin instructs the agent to display only the information needed to
explain a proposed match or an unresolved item. Signed upload URLs are treated
as secrets and must not be printed to the user or added to unnecessary logs.

## Writes and user control

In an interactive standard run, Qonto receives an attachment only after the
user sees the proposed mapping and explicitly approves the upload. This upload
path is currently available only in supported Claude Code and Codex sessions.
Cowork is limited to read-only reporting and manual-file validation; it does
not upload to Qonto. Dry-runs and scheduled runs are report-only. The plugin
does not send email feedback without the user's separate approval and never
sends it from Cowork.

Qonto work in Cowork requires a directly started interactive task with
**Manually approve**. The plugin stops before data access in Auto, Skip,
scheduled, unattended, or mobile-dispatched Cowork tasks. It does not use
Computer Use, Claude in Chrome, or direct Qonto or mail interfaces.

Authentication credentials are handled by the selected surface, connector,
and Qonto OAuth flow; the plugin does not ask the user to reveal a password.

Qonto's official MCP can expose more role-authorized tools than this workflow
needs, including operations unrelated to receipt matching. The bundled MCP
configuration has no per-tool allowlist. Qonto Matchmaker's instructions limit
its own workflow to organization/account/membership/card/transaction reads and
the approved attachment-upload flow, but the host surface and Qonto remain the
technical permission boundary. Users should review tool-approval prompts and
can disconnect the connector or revoke Qonto authorization.

## Temporary files and retention

When the execution surface supports files, downloaded PDFs are stored in a
run-specific temporary directory in that active execution environment. The
plugin instructs the agent to make a best-effort deletion of run-created
temporary files after a controlled success, error, or user stop. A crash,
force-quit, host failure, or provider limitation can prevent that cleanup.
The host surface, connector, mail provider, Qonto, and their logs or session
history may retain data under their own policies even after the temporary file
is deleted.

Users should apply their organization's retention and access-control rules and
should not connect a mailbox or Qonto organization they are not authorized to
use.

## Contact and changes

Privacy questions about the plugin can be sent to
[privacy@fizard.com](mailto:privacy@fizard.com). Product support is available
at [support@fizard.com](mailto:support@fizard.com).

Material changes to this notice are recorded in the repository history. The
general Fizard privacy documents and agreements are available at
[fizard.com/datenschutz-vereinbarungen](https://fizard.com/datenschutz-vereinbarungen).
