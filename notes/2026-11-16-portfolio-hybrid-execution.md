# Portfolio architecture direction: conversational interface and Linux execution

**Owner direction recorded:** November 16, 2026, Product Sourcing conversation.
**Classification:** Owner-selected portfolio deployment direction and integration contract; supporting architecture note, not a universal enterprise canon claim.
**Implementation status:** Target architecture. No connector, Linux endpoint, deployment or zero-cost integration is established by this record.

## Owner direction

The owner wants to ask through ChatGPT or another interface; the interface passes parameters to the necessary workflow/agentic loop; Python code executes on an owner-controlled Linux host (Hugo-1 or another owner-controlled virtual private server); results return to the originating interface. Apply this separation consistently across portfolio projects. Zero incremental project spending is a constraint. The existing Product Sourcing Python implementation must be reused; a separately selected search provider is not mandatory.

This note records the direction expressed in the visible conversation. It is not a full historical chat export, a deployment receipt, or proof that every project already follows it.

## Logical responsibilities

| Boundary | Responsibility |
| --- | --- |
| Request interface | ChatGPT or an alternative interface gathers intent, clarifies parameters, shows evidence-backed results and obtains any necessary human decisions. |
| Integration bridge | A separately implemented and verified authenticated connection carries versioned structured requests/results. Transport exposes capability; it does not grant new authority. |
| Linux application runtime | Python on an owner-controlled Linux host validates inputs/authority and runs the project workflow, deterministic services and bounded agentic steps when justified. |
| Durable application state | Request identity, checkpoints, evidence, decisions and results live under the application’s retention/access rules, outside an ephemeral chat session. |
| Result presentation | ChatGPT or the originating interface receives structured status, outputs, source evidence and unresolved questions, then explains the result without inventing completion. |

These are logical capabilities, not a mandate to buy or deploy five separate products. GitHub stores versioned source; it is not the production execution host. Codex is a development surface unless a particular deployed responsibility is separately established. A model service, when used, may execute remotely; the Python orchestration/runtime remains separately identified.

## Workflow selection and authority

An agentic loop is optional. Use deterministic code for defined validation, calculations and workflows; invoke reasoning only for an explicit evidence need under a documented event, budget and stop condition. ChatGPT's interpretation does not automatically justify another model call on the server.

The server validates the requesting identity, allowed operation, parameters, evidence and approval scope. A conversational instruction or a callable tool is not a substitute for authorization enforcement. Consequential actions retain the established human/domain approval boundaries; this record does not authorize purchases, publication, deployment or credential changes.

## Common request/result contract

The exact wire schema remains an implementation decision. Every integration must nevertheless make these concepts explicit:

- Request: contract version, request/correlation ID, authenticated caller, workflow/operation, normalized parameters and constraints, required evidence, allowed effects/approval references, resource/cost limits and deadline where supplied.
- Result: matching request ID, application/code version, explicit success/partial/failed/blocked status, outputs and calculations, source provenance and observation times, unknowns, actual action receipts where applicable, elapsed/resource/cost information and the next required decision.
- Re-entry: reconcile a previously submitted request by ID. After a timeout, distinguish failed execution from an unknown outcome before retrying an effectful operation.
- Longer work: return an acknowledgement/task ID; preserve server state and provide a documented resumption/completion route. Closing a chat must not silently erase application execution state. No continuous polling is assumed.

Sending and receiving real requests/results must be tested. A configured URL, passing unit test, generated scaffold, manually copied JSON or chat-assisted demonstration is insufficient proof of an operational integration.

## Cost and tool boundaries

No new paid search subscription, paid model API, hosting plan or other recurring charge is authorized by this direction. Reuse existing capabilities where the actual interface/provider permits them. A chosen connection must demonstrate its availability and zero incremental cost under the owner's existing arrangements; this note does not promise a free integration.

ChatGPT's available search or other tools do not automatically transfer to a Python server. When the interface can legitimately collect evidence, it can pass attributable structured evidence to the server through the verified contract. That is a design option to test, not an already implemented feature. The standalone search adapter can remain optional and unused.

If a necessary capability cannot be delivered within the constraint, report the specific gap and alternatives; do not silently select a paid provider or label a manual handoff automatic.

## Uniform application and proof

For each existing and new project, document: originating interface; bridge and authentication; Linux host; Python entry point; operation/authority contract; state location; external services and costs; return path; timeout/re-entry behavior; proof and current status. Distinguish implemented, configured, tested and deployed.

Project Bootstrap should make these fields visible during onboarding and project documentation, while keeping domain logic provider-agnostic. Any generator change is a separate reviewed implementation increment. This record does not overwrite the current v0.4 standard, regenerate projects or certify uniform adoption.

For Product Sourcing, formal quotes remain optional escalation and wholesale remains a separate workflow. Immediate acceptance target: an actual request from the interface reaches the Python engine on Linux and returns a useful source-attributed answer to that interface, within the cost/authority constraints. The exact bridge is still to be selected and proven.

## Relationship to existing architecture

This applies the logical capabilities and invocation distinctions in [technical mechanisms and execution](2026-11-07-technology-mechanisms-and-execution.md). It preserves portability and the distinction between control, reasoning, execution, evidence and authority. Hosting preference is a portfolio decision, not a claim that every enterprise must use this topology.
