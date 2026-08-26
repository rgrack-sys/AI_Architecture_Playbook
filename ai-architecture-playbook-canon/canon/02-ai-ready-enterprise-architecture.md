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

