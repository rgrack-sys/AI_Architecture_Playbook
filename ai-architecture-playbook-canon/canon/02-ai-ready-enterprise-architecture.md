# Canon 02 - AI-Ready Enterprise Architecture

**Status:** Working Canon v0.3  
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

## 2. Process-first AI architecture

A core architectural discipline is to begin with a real business problem rather than with a technology choice.

### Canonical principle

> **Always tie your architecture to a real business problem.**

AI initiatives should be grounded in a concrete business problem, decision, outcome, risk, or operating need. Architecture that begins with a model, platform, agent framework, or tool and only later searches for a use case risks producing technology demonstrations rather than durable operating systems.

A useful sequence is:

**Business problem -> desired outcome -> process -> decisions -> evidence -> controls -> architecture -> technology**

not:

**Technology -> architecture -> search for a use case.**

### Process engineering thesis

> **The most important engineering in the AI world is process engineering. Yet most organizations are set up to build a process around a set of technology decisions.**

The architectural implication is not that technology can never lead discovery. New model or platform capabilities can reveal previously impossible workflows. But once an AI capability is being operationalized, production architecture should be process-led.

The process should establish:

- what business outcome is being pursued,
- what decisions are being made,
- what evidence is required,
- which humans or systems participate,
- where controls and handoffs occur,
- how exceptions are handled,
- where accountability resides,
- and what success or failure looks like.

Only then should the architecture determine the required models, agents, tools, orchestration, data services, and platforms.

### Working distinction

> **Capability discovery can be technology-led. Production architecture should be process-led.**

This preserves room for experimentation while preventing production systems from becoming accidental consequences of a technology stack.

### Executive shorthand vs. practitioner methodology

The sequence:

**Business problem -> desired outcome -> process -> decisions -> evidence -> controls -> architecture -> technology**

is the **executive shorthand** for the methodology. It establishes direction: begin with the business and work toward the technology.

It is **not a literal waterfall**.

In practice, architecture work is iterative. New evidence can change the process model. Controls can constrain a decision before evidence design is complete. Architecture constraints can expose an invalid process assumption. Evaluation can force a redesign.

The practitioner methodology therefore uses a set of design passes:

> **Frame -> Observe -> Decompose -> Govern -> Redesign -> Architect -> Specify -> Select -> Prove -> Learn**

Each pass exists to answer a different architectural question.

#### 1. Frame

Define:
- the business problem,
- desired outcome,
- beneficiary,
- unit of work,
- scope,
- constraints,
- measures of success,
- and unacceptable outcomes.

The goal is to establish what the system is trying to improve and what it must not make worse.

#### 2. Observe

Establish how the work actually happens today.

Distinguish:
- the process people describe,
- the process documents prescribe,
- and the process systems and observed behavior show actually occurred.

SOPs, interviews, whiteboards, task capture, and system event logs are evidence sources. When those sources disagree, the disagreement is a finding rather than noise to be silently reconciled.

### Canonical principle

> **Process maps used for AI architecture should be evidence-backed models of work, not workshop artwork.**

#### 3. Decompose

Break the current process into more than activities and decisions.

Identify:
- activities,
- decisions,
- actions,
- transformations,
- waits,
- state changes,
- boundaries,
- exceptions,
- loops,
- escalations,
- handoffs,
- and outcomes.

Then determine where reasoning actually occurs.

This allows the architect to separate:
- deterministic work,
- probabilistic reasoning,
- human judgment,
- and external or physical action

before selecting an AI pattern.

### Important distinction

> **A decision is not the only place architecture matters. State, handoffs, waits, actions, exceptions, and proof of completion can be equally consequential.**

#### 4. Govern

For each consequential decision or action, answer three separate questions:

**Evidence — What must be known?**  
What information, observations, records, or proof are required?

**Authority — Who or what is allowed to decide or act?**  
What identity, role, system, agent, or human owns the decision or action?

**Control — Under what conditions may that authority be exercised?**  
What policy, approval, separation-of-duty rule, safety limit, regulation, confidence threshold, stop condition, or escalation rule applies?

These concepts are related but not interchangeable.

Evidence is also not limited to decision support. It can:
- authorize an action,
- establish current state,
- prove that an external or physical action completed,
- trigger re-entry into an automated flow,
- or demonstrate that a control was satisfied.

### Canonical question

> **Given this state, with this evidence, under this authority, may this system perform this action?**

This is a stronger architecture question than:

> Can AI do this?

#### 5. Redesign

Do not collapse current-state discovery and future-state design into one process step.

After the current process is understood, explicitly design the AI-enabled future state.

Ask:
- What work should disappear?
- What should become deterministic automation?
- Where is probabilistic reasoning justified?
- Where must a human remain?
- What authority can be delegated?
- What evidence can be assembled automatically?
- Where does the process stop and wait?
- How does it know external work actually happened?
- What state must survive the handoff?
- What happens when evidence is missing, stale, contradictory, or insufficient?
- What happens when the world changes while the process is waiting?

### Canonical principle

> **AI architecture does not begin by inserting an agent into the existing process. It begins by redesigning the operating process around the capabilities, limits, evidence needs, and control requirements of machine reasoning.**

#### 6. Architect

Only after the future-state operating process is defined should the architect derive the technical responsibilities needed to execute it.

The process and governance requirements determine whether the system needs:
- systems of record,
- governed knowledge,
- task-specific context assembly,
- reasoning models,
- deterministic services,
- tools,
- state,
- triggers,
- runtime,
- harness controls,
- identity and permissions,
- delegation contracts,
- observability,
- provenance,
- and feedback loops.

Every major architectural component should be traceable to an upstream process, evidence, authority, control, state, or outcome requirement.

#### 7. Specify

Translate architecture into **capability requirements before product requirements**.

For example:

> Retrieve authoritative policy evidence with provenance, effective date, access control, and the required response time.

is a capability requirement.

> Use a vector database.

is an implementation choice.

Likewise:

> Persist workflow state across an asynchronous human approval and resume only after proof of completion.

is a capability requirement.

A specific workflow engine, database, platform, or cloud service is a technology choice.

### Canonical principle

> **Architecture defines the required capabilities. Technology is selected to implement them.**

### Architecture test

> **If the product names are removed from the architecture, can we still explain why every capability exists?**

If not, the design probably jumped from problem to product before deriving the architecture.

#### 8. Select

Evaluate models, platforms, stores, frameworks, orchestration systems, process-mining tools, and cloud services against the derived capability requirements.

This is the point where vendor-specific skills and implementation patterns plug into the baseline methodology.

The methodology should remain stable even when products change.

#### 9. Prove

The system is not validated merely because the architecture diagram is coherent or the model gives plausible answers.

Evaluation must test:
- business outcome,
- process execution,
- reasoning quality,
- evidence quality,
- provenance,
- control enforcement,
- authority boundaries,
- state transition correctness,
- handoff and re-entry behavior,
- intervention and escalation behavior,
- failure handling,
- latency,
- cost,
- residual risk,
- and behavior relative to the pre-AI baseline.

Evaluation is therefore an architectural responsibility, not only a QA activity.

#### 10. Learn

Operational outcomes become new evidence.

Observe what happened, update state and knowledge, compare results to the intended outcome, and refine the process, controls, evidence strategy, architecture, or technology as needed.

The methodology is therefore closed-loop rather than a one-time design exercise.

### Canonical methodology thesis

> **AI architecture is derived through process engineering. The architect first understands and redesigns the work, decisions, evidence, authority, controls, state, and outcomes; the required AI architecture is then derived from those requirements.**

This does not mean every system requires a large process-transformation exercise. The depth of each pass should scale with risk, complexity, volatility, and consequence.

---

## 3. The Evidence-First Gate

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

## 4. Evidence requirements should be risk-aware

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

## 5. AI-ready information architecture

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

## 6. Three architectural layers

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

## 7. Governed Knowledge Architecture

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

## 8. Continuous Knowledge Synchronization

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

## 9. Volatility should be first-class metadata

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

## 10. Where Customer Data Platforms fit

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

## 11. Research loop as an architectural capability

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
