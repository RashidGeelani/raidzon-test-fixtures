# Shared full-match scenarios

`initial-state.json` contains synthetic players. Each scenario patches it using JSON pointers, then applies events in order. Rejected events specify an error. Accepted events contain explicit expected state values and a SHA-256 hash of the complete `{before, state, components, summary}` result.

Canonical JSON sorts object keys recursively, preserves array order, and uses compact UTF-8 JSON. Java maps winner enums to the frontend's numeric sides and omits absent component player IDs before comparison. No other gameplay fields are excluded.

The initial hashes were generated from the frontend after all manually authored expectations passed. Both frontend and Java tests verify these pinned snapshots; Java additionally replays every accepted prefix. Normal test runs never update them.

Run from the repository root:

```sh
npm test
mvn -f raidzonbackend/pom.xml test
```

For an intentional, reviewed rules change, update the explicit expectations first. Then regenerate using PowerShell:

```powershell
$env:UPDATE_MATCH_GOLDENS = '1'
npm test
Remove-Item Env:UPDATE_MATCH_GOLDENS
```

Review fixture changes and run both suites again without that environment variable. Regeneration is not a remedy for an unexplained test failure.
