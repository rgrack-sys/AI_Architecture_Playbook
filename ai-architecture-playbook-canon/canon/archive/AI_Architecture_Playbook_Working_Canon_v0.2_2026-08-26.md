# AI Architecture Playbook

**Working Canon v0.2 — August 26, 2026**  
**Supersedes for working purposes:** v0.1 starter, while preserving all prior content below.  
**Versioning rule:** prior versions remain immutable in git history / versioned files; canon evolves by explicit revision and change log.

## Purpose

This repository is a living enterprise AI architecture playbook. The goal is not merely to explain AI technologies; it is to establish reusable, defensible architecture principles for designing AI systems in real organizations.

## Canon rule

**Nothing becomes canon until we try to break it.**

Every important principle should eventually include:
- the claim,
- why it matters,
- architectural implications,
- counterarguments,
- tradeoffs,
- failure modes,
- questions a skeptical CIO, CDO, security leader, regulator, or architect would ask,
- and the conditions under which the principle should be revised.

Future conversations should **refine the canon rather than reinvent it**.

## Initial canonical papers

1. `canon/01-ai-foundations.md`
   - Training vs. inference
   - Weights vs. embeddings
   - Contextual representation
   - Vector databases and retrieval
   - Model knowledge vs. external evidence

2. `canon/02-ai-ready-enterprise-architecture.md`
   - Evidence-First Gate
   - AI-ready information architecture
   - Governed knowledge architecture
   - Systems of record, knowledge layer, and agent context
   - Continuous knowledge synchronization
   - Data in motion and volatility
   - CDPs in the architecture
   - Data quality defines reasoning quality

## Working architectural thesis

> Traditional systems organize data for transactions, reporting, and retrieval. AI-ready architecture must additionally organize governed knowledge and current evidence for reasoning.

---

# Canon 01 - AI Foundations

**Status:** Working Canon v0.1  
**Origin:** August 25, 2026 conversation

## 1. Training and inference are different processes

### Training
Training is the process by which a model's parameters (weights) are adjusted from initially unhelpful values into a structure that captures useful statistical patterns.

The training process repeatedly:
1. receives tokens,
2. predicts,
3. measures error,
4. adjusts weights,
5. repeats at enormous scale.

The resulting model contains a **distillation of patterns learned during training**.

### Inference
Inference is what happens when we use the trained model.

At inference time, the model:
1. tokenizes incoming text,
2. creates internal numerical representations,
3. transforms those representations through its trained weights,
4. uses context to form richer representations,
5. predicts subsequent tokens.

The model is generally **applying learned weights, not retraining them during the conversation**.

---

## 2. Model weights are not a database

A useful correction from the conversation:

> Do not think of the model as querying a hidden database of everything it knows.

The weights are better understood as the learned machinery that transforms input into useful internal representations and predictions.

Knowledge is distributed across the model's parameters. There is not normally one discrete location containing "dog," another containing "red," and another containing "CPR."

A word or token activates and interacts with a large distributed mathematical structure.

### Mental model

A human does not normally hear "dog" and search every memory containing dogs before recognizing the concept.

Likewise, the model does not normally perform a database-style search across everything encountered during training.

**Activation is not retrieval.**

---

## 3. Embeddings and contextual representation

Tokens begin with learned numerical representations.

But meaning is not merely a fixed lookup.

For example:

- "the puppy is blue"
- "the puppy is green"

The initial representation associated with `puppy` begins from the same learned vocabulary representation, but the model's internal representation of that token changes as surrounding context is processed.

Therefore:

> Meaning in a transformer is contextual.

The model does not simply assign independent labels such as:

- puppy = noun
- is = verb
- green = color

Instead, many interacting dimensions form a distributed representation of the complete context.

---

## 4. Distillation is a useful form of compression

A useful mental model developed in the conversation:

If thousands of examples repeatedly express patterns about dogs, the trained model does not need to retrieve all of those examples whenever it encounters a dog-related prompt.

Training has **distilled** statistical regularities from those examples into the weights.

"Compressed" is useful shorthand, with an important caveat:

> The result is not one compressed record or one vector for a concept. The learned representation is distributed across the model.

---

## 5. Vector databases solve a different problem

A vector database should not be confused with the model's learned knowledge.

A retrieval system typically:
1. takes a concrete piece of content such as a paragraph, document section, product description, policy, or note,
2. uses an embedding model to create a vector representing that content,
3. stores the vector along with the original content and metadata,
4. embeds a later query,
5. searches for nearby vectors,
6. retrieves the associated content,
7. provides that content to the model as evidence/context.

This is an **external retrieval mechanism**.

### Key distinction

**Model weights:** learned machinery and distilled patterns.

**Embeddings:** numerical representations produced for inputs/content.

**Vector database:** external storage/index used to retrieve concrete content by similarity.

---

## 6. Why retrieval matters

The model's internal knowledge is finite and can become stale.

This is especially important when information is:

- time-sensitive,
- regulated,
- safety-critical,
- organization-specific,
- proprietary,
- frequently changing,
- or dependent on authoritative current sources.

The architecture should therefore not ask only:

> Can the model answer this?

It should ask:

> **What evidence does the model need before it should answer this?**

That question leads directly to the Evidence-First architecture pattern developed in Canon 02.

---

## Stress test

### Counterargument
"If a capable model already knows the answer, retrieval adds latency and complexity."

### Response
Correct. Retrieval should not be mandatory for every question. The architecture needs a gate that determines whether external/current evidence is required.

### Failure mode
Blindly applying RAG to every question can:
- increase latency,
- introduce irrelevant evidence,
- increase infrastructure cost,
- degrade otherwise-correct answers,
- and create another system that must be governed.

### Canonical position
**Retrieval is a tool for evidence acquisition, not a universal substitute for model knowledge.**

---

# Canon 02 - AI-Ready Enterprise Architecture

**Status:** Working Canon v0.1  
**Origin:** August 25, 2026 conversation

## 1. Data quality defines reasoning quality

The long-standing principle remains:

> You are only as good as your data.

AI expands the definition of "good data."

Traditional quality dimensions such as correctness, completeness, consistency, and integrity remain necessary. AI systems additionally need to understand:

- provenance/source,
- freshness/date,
- volatility,
- confidence,
- ownership,
- review status,
- review cycle,
- governance classification,
- relationships to other knowledge.

### Canonical principle

> **Data quality defines reasoning quality.**

The mathematics of statistics, machine learning, and AI can be extraordinarily powerful, but poor, stale, ambiguous, or ungoverned evidence produces poor reasoning.

---

## 2. The Evidence-First Gate

ReAct is commonly described as a loop involving reasoning, action, observation, and further reasoning.

The architectural concern identified here sits **above** that loop.

Before asking an agent to reason or act, determine whether it requires external evidence.

### Evidence-First Gate

1. Understand the intent/question.
2. Assess risk and domain.
3. Assess whether relevant knowledge is volatile.
4. Determine whether current or authoritative evidence is required.
5. Acquire and validate that evidence when necessary.
6. Establish provenance and freshness.
7. Only then enter the reasoning/action loop.

### Canonical question

> **What evidence does the agent need before answering or acting?**

This is stronger than:

> Can the model answer this?

---

## 3. Evidence requirements should be risk-aware

Evidence acquisition becomes increasingly important when the subject is:

- safety-critical,
- medical,
- legal,
- regulatory,
- financial,
- operationally consequential,
- time-sensitive,
- or rapidly changing.

For high-risk questions, authoritative current evidence can be mandatory.

### Important nuance

Historical guidance does not always need to be retrieved and compared before giving a time-critical answer.

The primary obligation is to establish the **current authoritative guidance**. Historical differences can then be explained when useful.

---

## 4. AI-ready information architecture

Do not begin an enterprise AI data strategy with:

> "Embed everything."

Instead ask:

> What does an intelligent agent need to know about this information in order to determine whether it can trust and use it?

Useful metadata includes:

- source/provenance,
- creation date,
- last verified date,
- volatility classification,
- owner,
- review status,
- review cadence,
- confidence,
- regulatory/governance classification.

### Principle

> **Organize the trustworthiness and lifecycle of information, not merely the information itself.**

---

## 5. Three architectural layers

A useful separation emerged from stress-testing the initial concept.

### Layer 1 - Systems of Record
**Question:** What happened? What does the organization formally know?

Examples:
- transactional databases,
- operational applications,
- warehouses,
- Snowflake,
- BigQuery,
- CRM systems,
- governed master data.

These systems optimize for integrity, transactions, history, reconciliation, and authoritative records.

### Layer 2 - Governed Knowledge Layer
**Question:** What do we know, and what does that knowledge mean?

This may contain or expose:
- semantic relationships,
- knowledge graphs,
- curated summaries,
- embeddings,
- policies,
- derived facts,
- provenance,
- freshness,
- volatility,
- confidence,
- governance metadata.

Crucially, this does **not necessarily need to be another physical database**.

It can be a logical, federated, or on-demand abstraction over governed sources.

### Layer 3 - Agent Context / Evidence Layer
**Question:** What does this agent need to know **right now** for this decision?

This layer assembles task-specific evidence from the governed knowledge layer and, where appropriate, current authoritative external sources.

It is optimized for the immediate decision rather than for representing everything the enterprise knows.

### Summary

> **Systems of record:** what happened / what the organization knows.  
> **Knowledge layer:** what do we know and how should it be understood.  
> **Agent context:** what does this agent need now.

---

## 6. Governed Knowledge Architecture

A central principle from the conversation:

> **Don't move governed data to AI. Move AI reasoning to governed knowledge.**

In regulated environments, blindly copying governed data into external AI infrastructure can create unnecessary privacy, security, compliance, residency, and control problems.

Instead:

- keep authoritative/governed information within its permitted boundary,
- expose only the knowledge/evidence the agent is authorized to use,
- bring approved reasoning capability to that governed environment or interface,
- control what information may leave the boundary.

### Important architectural implication

The knowledge layer is not merely an optimization for AI performance.

It can become a **policy enforcement and abstraction boundary** between enterprise data and agent reasoning.

---

## 7. Continuous Knowledge Synchronization

Periodic summarization alone is insufficient because different information changes at different rates.

The stronger pattern is:

> **Continuous knowledge synchronization driven by volatility.**

Each class of knowledge should have a refresh policy appropriate to how quickly it can change.

Examples:

- physical constants: extremely low volatility,
- product documentation: low/moderate volatility,
- customer profile: moderate volatility,
- transactions/interactions: high volatility,
- market prices: extremely high volatility,
- active regulations or safety guidance: potentially consequential volatility even if changes are infrequent.

### Data in motion

"Data in motion" is the operational side of this principle.

Events that materially change organizational knowledge may need to update both:

1. the authoritative system of record, and
2. the knowledge available to agents.

This avoids a dangerous architecture in which the system of record is current while the agent's knowledge representation remains stale.

---

## 8. Volatility should be first-class metadata

Not all knowledge deserves the same refresh policy.

A volatility classification can drive:

- refresh frequency,
- cache lifetime,
- retrieval requirements,
- source validation requirements,
- whether live lookup is mandatory,
- review cadence,
- confidence decay.

This turns freshness from an afterthought into an architectural property.

### Candidate volatility model

- **V0 - Stable:** effectively timeless for the system's purpose.
- **V1 - Slow:** expected to change over years.
- **V2 - Periodic:** changes on known or moderate cycles.
- **V3 - Active:** can change frequently and should be refreshed regularly.
- **V4 - Real-time:** decision quality depends on current event/transaction state.
- **V5 - Critical-current:** stale information can create material safety, regulatory, financial, or operational harm.

This scale is provisional and must be stress-tested before becoming mature canon.

---

## 9. Where Customer Data Platforms fit

A CDP is valuable because it unifies customer information and identity across systems.

It primarily answers questions such as:

> Who is this customer, and what do we know about their interactions?

That makes the CDP a valuable **input/source** for AI knowledge.

But a CDP is not automatically the reasoning layer.

The governed knowledge architecture may additionally need:

- policy,
- product knowledge,
- regulatory evidence,
- semantic relationships,
- provenance,
- volatility,
- agent permissions,
- decision-specific context.

### Canonical position

> **A CDP can unify customer data; the knowledge layer prepares governed evidence for reasoning.**

---

## 10. Research loop as an architectural capability

Agents should not blindly rely on their finite pretrained knowledge.

The system should classify when augmentation is:

- mandatory,
- optional,
- unnecessary.

A generalized loop is:

**Classify -> assess risk/volatility -> acquire evidence -> validate provenance/freshness -> reason -> act -> observe -> repeat as necessary.**

This can coexist with ReAct rather than replacing it.

The Evidence-First Gate governs whether the ReAct loop is allowed to begin with existing context or must first acquire better evidence.

---

# Stress Test

## Hole 1 - Are we over-architecting?

Not every application needs a formal enterprise knowledge layer.

For simple, low-risk, low-volatility applications, direct retrieval from a small governed corpus may be sufficient.

**Response:** Treat the architecture as a pattern with scalable implementation, not a requirement to deploy every component.

---

## Hole 2 - Derived knowledge can drift

Summaries, embeddings, graphs, and derived facts can become inconsistent with systems of record.

**Response:** Derived knowledge needs lineage, refresh policies, reconciliation, and an authoritative path back to source evidence.

---

## Hole 3 - Latency

Fresh evidence, federation, policy checks, and source validation can make agents slower.

**Response:** Volatility classification should determine where caching is acceptable and where latency must be paid to obtain current evidence.

---

## Hole 4 - Knowledge layer becomes another uncontrolled repository

Creating another giant copy of enterprise data defeats the purpose.

**Response:** Prefer logical/federated knowledge services where appropriate. Materialize only when performance, availability, or use-case requirements justify it.

---

## Hole 5 - Enterprise knowledge and task context are not the same thing

Trying to place everything an organization knows into an agent prompt is impossible and undesirable.

**Response:** Keep enterprise knowledge distinct from task-specific agent evidence.

---

# Emerging thesis

Traditional architecture focused heavily on storing and retrieving trustworthy data.

AI-ready architecture must additionally make that information:

- understandable,
- current,
- attributable,
- governed,
- and consumable as evidence for reasoning.

A working formulation:

> **Traditional architecture retrieves data. AI-ready architecture produces governable knowledge and current evidence for reasoning.**

This statement is deliberately provisional. It should be challenged before being promoted to mature canon.


---

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

# Change Log

## v0.2 — August 26, 2026

Preserves all v0.1 material and adds:

- Chat vs. agent execution contexts.
- Foreground-command vs. governed-background-process mental model.
- Model vs. agent distinction.
- Runtime vs. harness distinction.
- Agent assembly formula.
- Deterministic code as part of agentic systems.
- Instruction design as executable architecture.
- Traditional vs. AI architecture distinction.
- Governed Data / Evidence Boundary.
- Clean room as an implementation pattern, not a universal label.
- Harness-to-harness delegation.
- Domain-owned execution.
- Delegation Contract.
- Model Gateway / Model Policy abstraction.
- Closed-loop outcome feedback.
- **Emerging Reference Architecture — Draft 0.1.**
- Regulated-industry control points.
- Initial stress-test agenda for the reference architecture.

No v0.1 principles were intentionally removed or overwritten.
