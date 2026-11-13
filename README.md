# resilience-report

A set of MCP prompts to generate an overall Resilience Evidence Report for a deployed Commvault instance.

## What is in here

- `resilience-report.md` — the prompt set. Paste the steps in order, in one session, with the Commvault Command Center MCP connector enabled. Each step's output feeds the next.

## How it works

| Step | What it does |
|---|---|
| 0 · Guardrails | Read-only session rules: every figure comes from a tool result, every query gets a status, nothing is estimated from memory. |
| 1 · Collect | The evidence sweep across jobs, storage, plans, posture, failed jobs, restores, verification, audit trail and identity. |
| 2 · Score | The Service Resilience Index table. |
| 3 · Cards | Findings merged with practitioner use cases, each with its tool-call chain and result. |
| 4 · Backlog | Prioritised backlog and a first-90-days plan. |
| 5 · Substitute | Replace tenant names, users, tokens and IPs before anything leaves your machine. The map is kept in a separate restricted file. |
| 6 · Build the HTML | One self-contained, XHTML-strict HTML report with a full design and layout specification. |
| 7 · QA | Strict parsing, undefined-class check, multi-width render asserts, identifier sweep, completeness and invented-content checks. |
| 8 · Local model (optional) | Delegate the HTML writing to a local OpenAI-compatible model while you orchestrate, assemble and verify. |

## Requirements

- Claude Code (or another MCP client) with the Commvault Command Center MCP server connected.
- A read-only account on the CommCell. The prompts never call job-control, schedule or user-enable tools.
- For step 1.8 only: the ability to make a read-only REST GET to the reports engine with the same access token, because there is no MCP tool for the audit trail.
- Optional for step 8: a local OpenAI-compatible model endpoint.

## Changes since the first upload

- Audit trail is now collected through the reports-engine dataset API (dataset lookup, paging, severity counts, token and approval events) instead of a tool that does not exist.
- The report header keeps the real CommCell name and ID so the reader knows which estate the evidence belongs to; everything else is still substituted.
- Substitution of audit-event details is specified as a scripted, mechanical step.
- The HTML step is a full specification: masthead and logo, colour variables, typography, breakpoints, components, collapsible audit table, XHTML-strict markup.
- QA grew from five checks to seven, including completeness and invented-content detection.
- New optional step for delegating the HTML build to a local model, with the failure modes to prompt against.

## Output

The deliverables (the evidence markdown and the HTML report) and the substitution map are produced on your machine and are not part of this repository.
