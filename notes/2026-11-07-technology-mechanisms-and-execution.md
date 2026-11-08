# November 7, 2026 — Technical mechanisms and execution walk-through

**Classification:** Explanatory corpus / architecture design notes, not additional canon. **Source:** November 7 AI Architecture Playbook discussion. **Scope:** Technical explanation and visualizable execution, not a software build request.

## Architectural sequence

Business outcome and acceptance criteria → process definition/readiness → decide mechanism → authorized execution → evidence-backed verification and recovery.

## What we would actually build

| Capability | Concrete technical component | Function and boundary |
| --- | --- | --- |
| Trigger/intake | API endpoint, event subscriber, scheduler, or user interface | Receives work and creates a correlation ID |
| Process/orchestration | Workflow state machine and durable task store | Executes defined steps; maintains checkpoints, retries and stop conditions |
| Identity and authority | Authentication, policy engine, delegated credentials and approval service | Determines who may request and execute which effects |
| Evidence/context | Source adapters, metadata/provenance registry, retrieval/index, freshness checks | Assembles authorized current evidence for a specific decision |
| Integration | Direct APIs, message queues, MCP servers or other tool adapters | Exposes bounded capabilities; protocol availability does not grant authority |
| Skills/instructions | Versioned procedure and tool-use guidance | Makes reusable behavior available; does not replace runtime policy enforcement |
| Reasoning | Model gateway with optional model calls and evaluation | Handles tasks requiring inference; can be bypassed for deterministic work |
| Action execution | Domain-owned services and transaction/command handlers | Performs authorized effects and returns receipts or authoritative state |
| Verification | Deterministic assertions, independent outcome checks, evidence ledger | Confirms actual business result and governed process behavior |
| Observability/recovery | Correlated logs, traces, checkpoints, idempotency keys, dead-letter queue and escalation | Detects faults and supports safe reconciliation, recovery and audit |

These are **logical capabilities**, not a mandate to deploy separate products or microservices. Combine or federate components when requirements justify it.

## Four invocation patterns to compare

1. **Direct API:** deterministic code calls a trusted endpoint; no model needed.
2. **Model-mediated API:** model interprets a bounded input or produces a constrained proposal; deterministic code validates and executes.
3. **Agent-directed API:** agent chooses among permitted tools within enforced budgets, evidence and authority constraints.
4. **Deterministic workflow with bounded agentic exception handling:** normal path is code; exceptions invoke controlled reasoning or human escalation.

Evaluate latency, API and model costs, retries, orchestration, human work, failure rate and **cost per verified outcome**. A harness governs the full process; a runtime/framework provides execution capabilities; an API/MCP endpoint exposes a capability, not an entitlement. Separate the control plane from the execution plane.

## Illustrative successful execution sequence (not a deployment plan)

1. A business event creates a task with desired outcome, accountable owner and correlation ID.
2. Process readiness and policy gates validate task definition, prerequisites, permitted effects and acceptance criteria.
3. The orchestrator selects deterministic execution or a bounded reasoning step; it does not invoke a model by default.
4. Evidence adapters retrieve authorized source data; provenance, freshness and sufficiency are checked before reasoning.
5. If reasoning is needed, a governed model call proposes a decision or next action; output is validated.
6. The authority gate checks identity, domain permissions, resource limits and approvals before effectful execution.
7. The domain executor invokes the API/tool with an idempotency or operation identifier and records the receipt.
8. An independent verifier checks the external state and business acceptance criteria, not merely an HTTP success code.
9. The system commits the checkpoint, audit trail and result, or enters controlled recovery when uncertain or failed.
10. The accountable owner receives outcome, evidence and exceptions.

## Open design questions (not canon)

- Which exact technology products, framework and deployment topology best fit a particular enterprise?
- What evidence freshness windows, human-approval thresholds, and independent verifier are required for each domain?
- Which actions support idempotency, compensation, or only manual remediation?

## Provenance limitations

This note reconstructs agreed architectural substance from the available conversation context, not a complete verbatim transcript. Historical cross-chat coverage and local-only files require separate reconciliation.
