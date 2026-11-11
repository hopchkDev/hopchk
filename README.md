# hopchk

Verify and record what AI agents do, across MCP and A2A.

> **Status: early concept.** There is no released code yet. This repository holds the design and the plan. Expect change.

## The problem

Agents now call tools and talk to other agents, including agents that belong to other organizations. When something goes wrong, three questions are hard to answer:

- Who authorized this agent to do that?
- Was the action allowed under the agreement between the parties?
- Can either side prove what happened, without trusting the other side's logs?

## What hopchk is

hopchk is a transparent proxy that sits beside an MCP server or an A2A agent and watches the traffic at the boundary where it meets a partner.

- **Contracts:** a YAML file states what an agent may do (tools, arguments, limits). hopchk checks each call against it before the call is executed.
- **Signed ledger:** every decision is written to a hash-chained, Ed25519-signed ledger. Canonical JSON (RFC 8785) and SHA-256 keep the records reproducible.
- **Offline verification:** anyone can verify a ledger with a standalone verifier, no account and no network needed.
- **Sidecar, not a gateway:** internal traffic is untouched. hopchk is only active for partner-to-partner exchanges.

Audit-only is the default. Strict mode (deny and stop) is a switch.

## Planned CLI

```
hopchk init
hopchk wrap <command>
hopchk proxy
hopchk verify <ledger>
hopchk agreements
hopchk contract validate|test
hopchk ledger show
hopchk keys
```

## Roadmap

1. v1: standalone sidecar for MCP over stdio and HTTP, YAML contracts, signed ledger, offline verifier, Petstore demo.
2. Browser (WASM) verifier.
3. Later: cross-organization connectivity and agreements between partners, with signed receipts. Think of the role a value-added network plays in B2B integration, applied to agents.

## Non-goals

- Not a blockchain. Tamper evidence comes from signed, hash-chained logs and, later, a transparency log.
- Not a replacement for an MCP gateway. Gateways govern traffic inside an organization. hopchk produces evidence between organizations.
- A sidecar on MCP and A2A does not see direct API calls an agent makes on its own. An HTTP egress mode is a later goal.

## License

Apache-2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE).

## Contact

dev@hopchk.com
