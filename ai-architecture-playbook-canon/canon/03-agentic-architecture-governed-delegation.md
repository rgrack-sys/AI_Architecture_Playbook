# Canon 03 - Agentic Architecture & Governed Delegation

**Status:** Working Canon v0.1  
**Origin:** August 26, 2026 architecture conversation  
**Added in:** AI Architecture Playbook v0.2

## 1. Chat and agents are different execution contexts

A reasoning model can support both interactive chat and agentic execution, but those are not the same architectural construct.

### Interactive chat

Interactive chat is best understood as a **human-driven interaction context**.

A useful old-school analogy is a foreground command:

1. the user invokes it,
2. the system reasons and responds,
3. control returns to the user,
4. the system waits for the next interaction.

The chat application or session is analogous to the terminal through which the user interacts.

### Agentic execution

An agent is closer to a **governed background process**.

It may be invoked by:

- a user,
- a schedule,
- an event,
- a workflow,
- another agent,
- or another governed runtime.

The agent can maintain task state, use tools, perform multiple reasoning/action cycles, and report an outcome or request intervention.

It does not need to run continuously. It may be event-triggered, scheduled, task-based, or long-running.

### Canonical distinction

> **Chat is an interaction context. An agent is an execution context.**

The same reasoning model may serve both, but the execution responsibilities are different.

---

## 2. The model is not the agent

Reasoning models such as GPT, Claude, Gemini, and other foundation models are **reasoning engines**.

They should not be treated as synonymous with agents.

Platforms may wrap those models with:

- instructions,
- context management,
- tools,
- permissions,
- memory,
- retrieval,
- orchestration,
- logging,
- policy controls,
- and user interfaces.

Those environments may then host agentic workflows.

### Canonical principle

> **Do not say "the model is the agent." The agent is the assembled executable workflow in motion.**

This distinction prevents architecture diagrams from collapsing the model, the runtime, the harness, and the agent into one ambiguous box.

---

## 3. Runtime and harness are different

The **runtime** is where the agent executes.

The **harness** is how the agent is governed while it executes.

### Runtime / execution environment

The runtime provides the workroom in which the agent can:

- maintain task state,
- call models,
- invoke tools,
- execute workflow steps,
- wait for events,
- handle retries,
- and continue until a stop condition is reached.

### Harness / governance wrapper

The harness surrounds or constrains that execution with:

- system instructions,
- evidence requirements,
- permissions,
- model policy,
- tool policy,
- memory and retrieval rules,
- validation,
- confidence thresholds,
- audit and logging,
- retry/error handling,
- human approval gates,
- and stop conditions.

### Mental model

> **Runtime is where it runs. Harness is how it is constrained, observed, and governed.**

---

## 4. Agent assembly formula

When building an agent, the architect is not merely writing a prompt.

The architect is **assembling an operational workflow inside a governed environment**.

A useful canonical formula is:

> **Harness governs. Runtime executes. Model reasons. Tools act. State remembers. Trigger starts. The agent is the assembled workflow pursuing the delegated goal.**

The assembled system may include:

- reasoning model,
- instructions/rules,
- skills,
- tools/connectors,
- APIs,
- MCP servers,
- databases,
- files,
- browser capabilities,
- email or messaging systems,
- Python or other deterministic code,
- memory/state,
- triggers,
- permissions,
- evidence gates,
- validation,
- stop conditions,
- observability,
- audit,
- and human intervention.

### Important diagram rule

Do not draw **Agent** as a peer box beside Model, Rules, Tools, and State.

Those are components or capabilities of the assembled workflow.

> **The agent is the whole operational system in motion.**

---

## 5. Deterministic code remains part of the agentic system

Agentic systems do not replace deterministic software.

For example, a Python script may:

- collect structured input,
- normalize data,
- perform calculations,
- call an API,
- validate a response,
- transform an output,
- or execute a deterministic task.

That script may be:

1. a tool the agent invokes,
2. a runtime component,
3. an upstream input collector,
4. or a downstream action executor.

### Canonical position

> **Agentic architecture combines probabilistic reasoning with deterministic execution.**

The architectural goal is to place each responsibility where it belongs rather than force every problem into model reasoning.

### Model-invocation necessity gate

> **The fact that we can call an AI model doesn't mean we should.**

Model-backed reasoning is an architectural capability, not a default implementation choice. Before introducing a model call into a workflow, require an explicit justification against the available deterministic alternatives.

#### Architecture review checklist

1. **What capability are we introducing?** Model-backed reasoning.
2. **Why is it necessary?** Deterministic software cannot adequately perform that particular task.
3. **Where does it belong?** Behind a defined interface in the agent architecture.
4. **How do we govern it?** Authentication, cost controls, evidence boundaries, logging, and evaluation.
5. **Can we replace it?** Yes. The architecture should remain model-provider independent.

**Decision rule:** If a deterministic approach adequately meets the task's correctness, maintainability, latency, and control requirements, prefer it. Invoke a model when its reasoning capability adds demonstrable value relative to that alternative. Keep data collection, filtering, validation, state transitions, and other predictable work in ordinary software where appropriate.

**Implementation implication:** Put justified model calls behind an explicit, testable interface; preserve inputs, outputs, provenance, failure handling, and budget controls. The agent should remain usable in offline tests through a deterministic fake or mock model adapter.

#### Stress test

- **Counterargument:** A model call can be cheaper to implement than complex bespoke deterministic logic, especially for language ambiguity or unstructured inputs.
- **Response:** The rule does not prohibit a model. It requires comparing total cost, accuracy, operational risk, and maintainability before choosing it.
- **Tradeoff:** A necessity gate adds design effort and may rule out useful experimentation if imposed too rigidly. Lightweight prototypes can explore model capabilities, while production calls require an explicit justification.
- **Failure modes:** Treating AI as the default for simple transformations; quietly growing API usage; leaking credentials or evidence across boundaries; or binding core workflow logic to a single provider.
- **Skeptical review question:** What breaks, degrades, or becomes unreasonably complex if this specific model call is removed?
- **Revision condition:** Reassess when deterministic methods, model capabilities, cost, latency, or governance requirements change materially.

---

## 6. Instruction design becomes executable architecture

In traditional software, much system behavior is encoded directly in deterministic application logic.

In agentic systems, important behavior increasingly moves into:

- problem framing,
- task decomposition,
- instruction sets,
- evidence requirements,
- tool contracts,
- constraints,
- escalation rules,
- validation criteria,
- and governance policy.

Code remains essential for deterministic behavior, integrations, performance, infrastructure, security, and reliability.

But the center of gravity changes.

### Canonical principle

> **Instruction design is executable architecture.**

Clear reasoning workflows and explicit constraints are not merely documentation. They influence runtime behavior directly.

---

## 7. AI architecture is not traditional architecture plus a model

Traditional application architecture often centers on a pattern resembling:

**User Interface -> Application Logic -> Database -> Deterministic Action**

AI-enabled architecture introduces governed reasoning between intent, enterprise knowledge, and operational action.

The center of gravity expands to include:

- context construction,
- evidence selection,
- provenance,
- freshness,
- instruction design,
- harness/governance,
- orchestration,
- tool permissions,
- model policy,
- evaluation,
- confidence,
- state and memory,
- human approval,
- and observability.

### Canonical distinction

> **Traditional architecture optimizes primarily for deterministic execution. AI architecture must additionally optimize for governed reasoning and controlled action.**

This is not a claim that traditional architecture patterns disappear. They remain foundational beneath and around the reasoning layer.

---

## 8. Governed evidence boundary / clean room

In regulated, sensitive, or high-risk environments, source data should not simply flow unbounded into an agent.

The architecture should introduce a **governed data/evidence boundary**.

A clean-room pattern can serve this role when appropriate.

The boundary may enforce:

- identity resolution,
- authorization,
- consent,
- purpose limitation,
- minimization,
- de-identification or pseudonymization,
- policy checks,
- provenance,
- data classification,
- jurisdiction or residency requirements,
- transformation,
- and evidence packaging.

What should cross the boundary is not necessarily raw source data.

### Canonical principle

> **The reasoning environment should receive authorized context and evidence, not indiscriminate access to source data.**

This extends the existing principle:

> **Don't move governed data to AI. Move AI reasoning to governed knowledge.**

---

## 9. Domain-owned execution and harness-to-harness delegation

An enterprise agent should not automatically receive direct access to every operational capability required to complete an outcome.

A stronger enterprise pattern is:

> **The enterprise agent can delegate an intent or bounded task into another governed agentic environment that owns the domain capability.**

Example:

An enterprise agent may determine that a customer qualifies for an approved intervention.

It does not necessarily need:

- direct SMS credentials,
- campaign execution rights,
- commerce APIs,
- journey orchestration permissions,
- personalization systems,
- or channel-specific policy logic.

Instead, it delegates a bounded task to a domain environment such as an Adobe CX / Coworker execution environment.

That domain environment applies its own harness, permissions, business rules, tools, and audit requirements before acting.

### Canonical principle

> **Reason where the enterprise has context. Act where the domain has authority.**

This separation is especially important in regulated industries because reasoning authority and execution authority may be intentionally different.

---

## 10. The Delegation Contract

Harness-to-harness delegation introduces an explicit architectural boundary.

That boundary should be governed by a **Delegation Contract**.

A delegation contract defines:

- the task or intent being delegated,
- the allowed purpose,
- the bounded context that may cross the boundary,
- the evidence accompanying the request,
- provenance requirements,
- the actions the receiving environment may perform,
- actions it must not perform,
- data minimization requirements,
- authorization ownership,
- audit ownership,
- required result or acknowledgement,
- error/rejection semantics,
- escalation behavior,
- expiry or time-to-live,
- and whether human approval is required.

### Why it matters

Without a delegation contract, one agentic system can become an uncontrolled proxy for another.

The receiving environment should be able to reject a request that violates its own:

- policy,
- permissions,
- regulatory obligations,
- confidence thresholds,
- data-use restrictions,
- or business rules.

### Canonical principle

> **Delegation transfers a bounded task, not unlimited authority.**

---

## 11. Domain harnesses remain authoritative for domain action

A delegated agentic environment should retain authority over the tools and actions it owns.

For example, an Adobe CX environment may own:

- journey orchestration,
- customer profile activation,
- offer selection,
- commerce actions,
- messaging,
- push notifications,
- web personalization,
- or other customer-experience capabilities.

The enterprise reasoning environment may decide **what outcome is appropriate**.

The domain execution environment decides **whether and how that outcome may be executed within its governed capabilities**.

### Architectural implication

This supports separation of duties.

It also reduces the need for one central agent to accumulate excessive credentials and privileges.

---

## 12. Model access should be abstracted from agent identity

An agent architecture should not imply that a specific foundation model *is* the agent.

Where practical, model access should sit behind a governed **Model Gateway / Model Policy** abstraction.

That layer may select among approved models according to:

- task type,
- sensitivity,
- regulatory constraints,
- performance,
- cost,
- latency,
- context-window requirements,
- reasoning capability,
- or deployment boundary.

Conceptually:

```text
Agent Runtime
    |
    +-- Model Gateway / Model Policy
            +-- OpenAI
            +-- Anthropic
            +-- Google
            +-- approved internal/private models
```

### Canonical principle

> **Agents should depend on approved reasoning capability, not unnecessarily on one model vendor identity.**

This is a target architecture principle, not a requirement that every implementation support dynamic multi-model routing.

---

## 13. Closed-loop agentic systems

Consumer action should not be treated as the end of the architecture.

The outcome becomes new enterprise evidence.

A generalized closed loop is:

> **Observe -> Govern -> Reason -> Delegate -> Act -> Observe outcome -> Update knowledge -> Reason again**

Customer responses, operational outcomes, transaction results, failures, and interventions may flow back into:

- systems of record,
- the governed knowledge layer,
- agent state,
- evaluation systems,
- and later decisions.

### Important constraint

Feedback must itself be governed.

A model or agent should not automatically convert every observed response into trusted knowledge.

The feedback loop must preserve:

- provenance,
- authority,
- reconciliation,
- freshness,
- and appropriate validation.

---

# Emerging Reference Architecture — Draft 0.1

**Status:** Emerging / intentionally non-canonical at the component-box level  
**Origin:** Whiteboard and receipt sketches, August 25-26, 2026  
**Purpose:** First-pass conceptual layout for regulated enterprise agentic systems.

The principles beneath the architecture are candidates for working canon. The specific boxes, products, labels, and placement remain subject to refinement and stress testing.

```text
SOURCE / APPLICATION
       |
       v
GOVERNED DATA / EVIDENCE BOUNDARY
"Clean Room"
       |
       | authorized context / evidence
       v
+---------------------------------------------------+
| ENTERPRISE AGENTIC EXECUTION ENVIRONMENT          |
|                                                   |
|   +--------- Harness / Governance -------------+  |
|   | evidence rules                            |  |
|   | permissions                               |  |
|   | model policy                              |  |
|   | audit / logging                           |  |
|   | validation / confidence                   |  |
|   | human approval                            |  |
|   +--------------------------------------------+  |
|                                                   |
|   Runtime / Orchestrator                           |
|          |                                         |
|          +-- Agent workflow A                      |
|          +-- Agent workflow B                      |
|          +-- Agent workflow C                      |
+----------+-----------------------------------------+
           |
           | Delegation Contract
           | bounded task + authorized context/evidence
           v
+---------------------------------------------------+
| DOMAIN AGENTIC EXECUTION ENVIRONMENT              |
| Example: Adobe CX / Coworker                      |
|                                                   |
| Domain harness + runtime + domain-owned tools     |
|                                                   |
| Journey / AEP / Commerce / Messaging / etc.       |
+----------+-----------------------------------------+
           |
           | approved domain action
           v
      CHANNEL / ACTION
   SMS / Push / Web / Offer
           |
           v
        CONSUMER
           |
           | observed outcome / interaction
           v
   SYSTEMS OF RECORD / KNOWLEDGE UPDATE
           |
           +---------------------------> feedback loop
```

## Architectural reading

This architecture deliberately separates five concerns:

### 1. Source truth
Applications and systems of record own authoritative operational data.

### 2. Governed evidence
The clean-room / governed evidence boundary determines what information may be exposed for reasoning and under what purpose and controls.

### 3. Enterprise reasoning
The enterprise agentic environment reasons over the authorized evidence and determines an appropriate goal, decision, or requested outcome.

### 4. Delegated domain execution
A bounded task crosses a Delegation Contract into the domain environment that owns the operational capability.

### 5. Controlled action and feedback
The domain environment executes within its own permissions and policies. The outcome becomes governed evidence for later decisions.

## Why this matters in regulated industries

This architecture avoids giving a single central agent unrestricted access across data and execution domains.

It enables:

- least privilege,
- purpose limitation,
- separation of duties,
- policy enforcement at multiple boundaries,
- independent audit trails,
- bounded data movement,
- domain-specific authorization,
- human approval where necessary,
- and explicit rejection of non-compliant delegated actions.

The architecture therefore does not rely on a single universal "AI governance layer."

Governance is enforced at multiple control points:

1. source-data boundary,
2. governed evidence boundary,
3. enterprise reasoning harness,
4. Delegation Contract,
5. domain execution harness,
6. action/channel policy,
7. feedback/knowledge-update path.

---

# Agentic Architecture Stress-Test Agenda

The following questions should be challenged before the reference architecture is promoted beyond draft status.

## 1. Is "clean room" the correct universal term?

A clean room is one implementation pattern.

Other environments may use:

- governed data service,
- privacy boundary,
- policy enforcement point,
- trusted execution environment,
- federated query layer,
- secure data exchange,
- or domain-specific knowledge service.

**Working position:** The architectural concept is the **Governed Data / Evidence Boundary**. "Clean Room" is a possible implementation and useful regulated-industry example.

## 2. When should enterprise reasoning delegate rather than act directly?

Delegation adds latency and operational complexity.

Direct action may be appropriate when:

- the enterprise environment itself owns the capability,
- permissions are narrow,
- the risk is low,
- and there is no meaningful domain-governance boundary.

**Working position:** Delegate when another domain owns the capability, policy, credentials, or regulatory responsibility.

## 3. Can two harnesses conflict?

Yes.

The enterprise harness may authorize a request that the domain harness rejects.

This is not necessarily a defect.

**Working position:** The receiving domain remains authoritative for its own actions. Rejection semantics must be part of the Delegation Contract.

## 4. How much reasoning belongs in the domain environment?

This remains deliberately open.

A domain runtime might:

- execute a fully specified task,
- select among approved actions,
- perform additional reasoning,
- request missing evidence,
- or escalate to a human.

The appropriate boundary depends on accountability, data ownership, and domain capability.

## 5. How do we prove what happened?

Every cross-boundary invocation needs sufficient correlation and auditability to reconstruct:

- original intent,
- evidence used,
- reasoning policy/version,
- delegation request,
- receiving policy/version,
- action taken,
- and observed result.

This likely requires a shared correlation identifier and event lineage model.

---

# v0.2 Working Thesis

The emerging architecture can now be stated more completely:

> **AI architecture is not traditional architecture plus a model. It is an architecture for governed reasoning, evidence, delegation, and controlled action.**

And for agentic systems:

> **Harness governs. Runtime executes. Model reasons. Tools act. State remembers. Trigger starts. The agent is the assembled workflow pursuing the delegated goal.**

And for enterprise delegation:

> **Reason where the enterprise has context. Act where the domain has authority. Delegation transfers a bounded task, not unlimited authority.**

These formulations are working canon and should continue to be stress-tested.


---

## November 7, 2026 integration — Authority, accountability, and recovery

**Status:** Approved additions to existing working canon; implementation patterns remain subject to design-specific verification.

### Distinguish information authority from integration authority

An information source can be authoritative for *what is known* without being authorized to perform an action. An API, MCP server, or other integration endpoint provides an access mechanism, not automatic business authorization. Separate source provenance, evidence sufficiency, identity, permissions, domain policy, action authorization, and proof of effect. A tool's technical ability to execute is not a delegation of organizational authority.

### Bounded autonomy and ownership

> **Agentic authority must be earned, bounded, and verifiable.**

Define allowed actions, resources, scope, limits, prerequisites, approval and escalation boundaries, and explicit prohibited effects. Enforce constraints at the relevant control and domain execution boundaries, not solely in prompt wording. The agent must not alter its own authority, evidence requirements, or governance rules.

> **You own every word or action your agents generate.**

This is an accountability hook, not a claim that every generated output is automatically endorsed or legally attributable in every context. An identifiable human or organization remains accountable for deploying, supervising, and responding to agent behavior. Delegating execution does not delegate away ultimate organizational responsibility. Record who owns the outcome, who authorized the action, and who is accountable for exceptions and remediation.

### Failure and recovery are designed before autonomy

> **Autonomous execution requires a designed failure-and-recovery path, not merely a retry policy.**

The recovery sequence is: **detect failure → preserve state → reconcile the actual or uncertain outcome → select controlled recovery (retry, resume, compensate, escalate or stop) → verify and retain accountable evidence**. A timeout after a possible external commit is an *unknown outcome*, not proof of failure; blindly retrying can duplicate effects. A recovery may be a new authorized state and must be governed as such. Recovery controls must preserve evidence and prevent loops, uncontrolled spending, privilege expansion, or silent partial completion.

### Stress tests and limits

- Evidence can be fresh and authentic but still insufficient for the decision or unauthorized for use.
- A human approval step is not a substitute for enforceable technical constraints and auditable effect verification.
- Compensation is not always a true rollback; some external actions are irreversible and require escalation.
- Recovery cannot be considered successful until the required business outcome *and* the governed process behavior have been verified.

**Related execution and visualization notes:** `notes/2026-11-07-technology-mechanisms-and-execution.md` and `presentations/2026-11-07-agent-execution-animation-scenarios.md`.


### Human authorship is more than an approval gate — November 7, 2026 clarification

> **The human is not merely an approval gate. The human remains the accountable author and decision-maker. AI produces governed candidates; people determine what they ultimately communicate.**

For human-authored publication workflows, preserve three distinct artifacts: (1) the immutable, traceable agent-generated candidate with its evidence and review status; (2) the human-edited, explicitly accepted final artifact, with provenance of substantive edits; and (3) publication evidence showing the actual content, destination, time and publishing actor. Approval of a candidate does not automatically approve a later edited version. Revalidate or obtain renewed approval when edits change meaning, claims, risk, or governed constraints; ordinary editorial changes should be handled proportionately. The system must not imply that agent-generated text was published unchanged when a human modified it. Human ownership is an accountability principle, not a claim that every output is legally attributable in all jurisdictions.

**Provenance:** User-supplied excerpt from another AI Architecture Playbook chat, reconciled as a clarification of the already established human-accountability canon.

---

## November 7, 2026 targeted reconciliation — Adaptive need, governed acquisition, and accountable execution

**Classification:** Approved working-canon clarification, reconciled November 10, 2026. **Provenance:** November 7 AI Architecture Playbook discussion and its previously committed glossary and mechanism notes. This section clarifies Sections 2–5 and the November 7 authority/accountability integration; it neither grants new authority nor replaces prior controls.

> **An agent decides what it needs; the architecture decides how to get it.**

**Meaning and boundary:** Within an authorized delegated task, an agent may assess which information, reasoning, or next action appears necessary and propose an appropriate capability. The architecture and harness determine which sources and tools are eligible, how the information is obtained, what is fresh and sufficient, when a model call is justified, what cost and time limits apply, and which actions require independent permission or human approval. **Need identification is not access permission, and technical connectivity is not business authority.** An adaptive suggestion must never bypass deterministic orchestration, evidence rules, policy enforcement, domain-owned execution, or outcome verification.

Use the correct mechanism for the job: deterministic code for defined transforms and state transitions; a direct API for contracted operations; an MCP server or other adapter to expose governed capabilities; a classifier for bounded categorization/routing where justified; model reasoning for interpretation that deterministic methods cannot adequately provide; and agentic tool selection only where adaptive delegated execution adds demonstrable value. A classifier need not be a generative model, and a model, skill, API, or MCP endpoint is not itself an autonomous accountable agent.

For every consequential workflow, ask explicitly: **Who is accountable for the activity and its outcome?** Name the human or organizational owner, the delegated scope, enforceable controls, required receipts and verification evidence, and the person or role responsible for exception handling. The prior accountability hook — **“You own every word or action your agents generate.”** — remains in force, with its existing caveat regarding legal attribution.

**Stress tests and limits:** An agent's proposed evidence may be unauthorized or insufficient; a technically available API may be unsafe to invoke; a classifier's confidence score is not proof of source authority; an executed tool call does not prove a business outcome. The architecture must be able to refuse, pause, reconcile, escalate, and record the outcome without inventing missing process definition.

**Supporting terminology, not independent policy:** `notes/2026-11-07-architecture-glossary.md`. **Illustrative component patterns, not a mandated implementation:** `notes/2026-11-07-technology-mechanisms-and-execution.md`.
