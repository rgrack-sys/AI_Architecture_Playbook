# AI Architecture Design Methodology — Curriculum and Syllabus

**Status:** Draft v0.4 — curriculum working draft, aligned to Canon 02 v0.4; curriculum itself is not canon  
**Purpose:** Train enterprise architects to redesign business processes for an AI-enabled operating model and then select architecture patterns and tools that implement that design.  
**Audience:** Enterprise architects, solution architects, business architects, senior technologists, and architecture leaders who may already know the technologies but need to explain what they are, why they are needed, where they belong, and when they should not be used.

---

# Core teaching position

I do not want this course to start with models, agents, RAG, vector databases, or an AI platform.

Those are implementation choices.

The course starts with the business problem and teaches the architect to work toward the technology.

At the executive level, the shorthand remains:

**Business problem -> Outcome -> Process -> Decisions -> Evidence -> Controls -> Architecture -> Technology**

The direction matters, but this is not a literal waterfall.

The practitioner methodology underneath it is:

**Frame -> Observe -> Decompose -> Govern -> Redesign -> Architect -> Specify -> Select -> Prove -> Learn**

The architect should be able to explain every technology choice by tracing it back to a process, evidence, authority, control, state, outcome, or capability requirement.

The methodology should also teach the inverse test:

> If I remove the product name from the architecture diagram, can I still explain why every architectural capability exists?

If the answer is no, we probably started with the technology.

---

# Course outcomes

At the end of the baseline course, an architect should be able to:

1. Explain the AI fundamentals a customer needs in order to make architecture decisions.
2. Explain the major agent interoperability standards and conventions — including MCP, Agent Skills, and A2A — and distinguish the architectural boundary each one addresses.
3. Recognize the supporting interface, event, identity, schema, observability, lineage, provenance, and content-authenticity standards that modern AI systems inherit from the broader software and data ecosystem.
4. Define a business problem and measurable outcome before discussing technology.
5. Establish an evidence-backed current-state process model from interviews, transcripts, whiteboards, documents, screen recordings, and system event data.
6. Decompose the work into activities, decisions, actions, waits, state changes, boundaries, exceptions, handoffs, and outcomes, and identify where reasoning actually matters.
7. Identify automation boundaries and engineer the handoff and re-entry state explicitly.
8. Distinguish evidence, authority, and control for consequential decisions and actions.
9. Determine when model knowledge is sufficient and when authoritative external evidence is required.
10. Redesign the future-state operating process before deriving the AI architecture.
11. Design the information architecture needed to provide current, governed evidence for reasoning.
12. Start from what the system must do with its data, derive the required access, authority, freshness, consistency, relationship, provenance, and governance characteristics, and then select the appropriate data structures, store/index patterns, formats, and movement technologies.
13. Separate model, agent, runtime, harness, tools, state, trigger, and deterministic software responsibilities.
14. Define evaluation, observability, provenance, and closed-loop outcome feedback before production.
15. Translate architecture into capability requirements and only then evaluate specific products.
16. Defend the design to a CIO, CDO, security leader, business owner, regulator, engineering team, and skeptical architect.

---

# The baseline methodology

The course will teach one repeatable methodology with two levels of expression.

### Executive shorthand

**Business problem -> Outcome -> Process -> Decisions -> Evidence -> Controls -> Architecture -> Technology**

This establishes direction: start with the business and work toward the technology.

It is not a literal waterfall.

### Practitioner methodology

> **Frame -> Observe -> Decompose -> Govern -> Redesign -> Architect -> Specify -> Select -> Prove -> Learn**

## Pass 1 — Frame

Define the business problem, desired outcome, beneficiary, unit of work, scope, constraints, measures of success, and unacceptable outcomes.

Do not accept "we need an agent" as a problem statement.

## Pass 2 — Observe

Establish how the work actually happens today.

Distinguish:
- the process people describe,
- the process documents prescribe,
- and the process observed behavior and systems show actually occurred.

Contradictions between these sources are findings to validate, not noise to hide.

## Pass 3 — Decompose

Break the process into:
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

Then determine which work is deterministic, which requires probabilistic reasoning, which remains human judgment, and which depends on external or physical action.

## Pass 4 — Govern

For each consequential decision or action answer three separate questions:

**Evidence — What must be known?**  
**Authority — Who or what is allowed to decide or act?**  
**Control — Under what conditions may that authority be exercised?**

Evidence, authority, and control are related but not interchangeable.

The architecture question becomes:

> **Given this state, with this evidence, under this authority, may this system perform this action?**

## Pass 5 — Redesign

Design the future-state operating process only after the current state is understood.

Determine what work disappears, what becomes deterministic, where reasoning is justified, where humans remain, what can be delegated, where the process waits, what state must survive, and how the process re-enters after external work.

## Pass 6 — Architect

Derive the technical responsibilities required to execute the redesigned process:
- reasoning,
- deterministic execution,
- knowledge,
- context,
- state,
- triggers,
- runtime,
- harness,
- identity and permissions,
- integration,
- delegation,
- observability,
- provenance,
- and feedback.

## Pass 7 — Specify

Translate the architecture into capability requirements before naming products.

A capability requirement describes what the architecture must do and under what conditions. A product is only one possible implementation.

## Pass 8 — Select

Only now choose models, platforms, data stores, agent frameworks, workflow products, process-mining tools, vector stores, orchestration systems, or cloud services.

## Pass 9 — Prove

Evaluate whether the design works across business outcomes, process execution, reasoning, evidence, authority, controls, state transitions, handoffs, failure behavior, latency, cost, and residual risk.

## Pass 10 — Learn

Observe outcomes, update state and knowledge, compare results to the intended outcome, and refine the process, controls, evidence strategy, architecture, or technology as needed.

The important distinctions remain:

> Capability discovery can be technology-led. Production architecture should be process-led.

> Architecture defines the required capabilities. Technology is selected to implement them.

---

# Syllabus

## Module 1 — AI Fundamentals an Architect Must Be Able to Explain

### Topic description

This is not an ML engineering class. The goal is to give the architect a correct mental model and enough depth to explain why an architectural capability exists.

The basics now include two things:

1. how the model and context system work,
2. how an agentic system interoperates with tools, data, other agents, users, and enterprise services.

### What I teach

#### A. Model and context fundamentals

- Training vs. inference.
- Tokens and context.
- Model weights are learned machinery, not a hidden database.
- Embeddings are numerical representations, not "the model's memory."
- Vector databases store and retrieve external content by similarity.
- Context changes representation and therefore reasoning.
- Model knowledge is different from external evidence.
- Retrieval is an evidence-acquisition technique, not a universal requirement.
- Deterministic software still belongs in AI systems.

#### B. The agent interoperability stack

Teach these as different architectural boundaries rather than as competing products.

**Agent Skills — reusable procedural knowledge**

A Skill packages instructions, procedures, scripts, references, and assets that teach an agent how to perform a class of work.

The important architectural idea is:

> **Skills package HOW to perform work.**

The open Agent Skills format centers on a `SKILL.md` file with metadata and instructions, with optional scripts, references, and assets. Skills are loaded progressively so detailed procedure enters context only when needed.

Also distinguish the Agent Skills format from the MCP Skills extension. The format defines the skill package. The MCP extension defines one standardized way to publish and retrieve skills through MCP.

**Model Context Protocol (MCP) — agent to tools, resources, and context**

MCP standardizes how AI applications connect to external capabilities and information.

Teach:
- host / client / server roles,
- tools,
- resources,
- prompts,
- structured tool schemas,
- authorization and consent,
- remote vs. local servers,
- long-running task extensions,
- the distinction between exposing a capability and granting authority to use it.

The architectural shorthand is:

> **MCP connects the reasoning environment to tools, resources, and context.**

**Agent2Agent (A2A) — agent to agent**

A2A standardizes communication between independent agent systems.

Teach:
- agent discovery,
- capability advertisement,
- task delegation,
- message / artifact exchange,
- task state,
- interoperability across frameworks and vendors,
- why a remote agent should not need access to another agent's internal memory or implementation.

The architectural shorthand is:

> **A2A connects governed agents to other governed agents.**

### The distinction the architect must be able to explain

**Skill:** How do I perform this kind of work?  
**MCP:** What tools, resources, or context can I use?  
**A2A:** What other agent can I collaborate with or delegate to?

These solve different problems and can be used together.

#### C. Supporting standards an AI architect should recognize

These are not all "AI standards." That is exactly the point. Production AI systems inherit the contracts of the software and data systems around them.

**Core supporting standards**

- **OpenAPI** — machine-readable contracts for HTTP APIs and services.
- **JSON Schema** — structured input/output definition and validation; foundational to many tool contracts.
- **AsyncAPI** — machine-readable contracts for asynchronous and event-driven APIs.
- **CloudEvents** — common event envelope and metadata model for events moving between systems.
- **OAuth 2.x / OpenID Connect** — authorization and identity. Agentic systems do not eliminate identity; they make delegated identity and scope more important.
- **OpenTelemetry semantic conventions** — traces, metrics, logs, and increasingly GenAI / agent / MCP observability.

**Data, knowledge, provenance, and content standards that appear later in the course**

- **OpenLineage / provenance models** — where data came from and how it changed.
- **RDF / OWL / SPARQL** — semantic graph and knowledge representation where that model is appropriate.
- **C2PA Content Credentials** — provenance and authenticity of digital content, increasingly relevant when agents consume or generate media.
- **Apache data formats and table standards** such as Arrow, Parquet, Avro, and Iceberg — portable representations used throughout analytical and AI data pipelines.

**Emerging protocols worth recognizing, but not yet core course dependencies**

- **AG-UI** — agent-to-user application interaction.
- **A2UI** — declarative, agent-generated UI payloads.
- **AGENTS.md** — project-level instructions for coding agents.

The architect should know these exist and know what boundary they address without treating every emerging protocol as mandatory architecture.

### Why the architect needs it

A customer will ask:

- Why do I need RAG if the model already knows things?
- Why can the model answer this question but not be trusted to answer another one?
- Why do I need a vector database?
- Why can't I just put all of the documents in the prompt?
- Why do I need an API or deterministic service when the model can calculate it?
- What exactly is an agent?
- What is the difference between MCP and an API?
- What is the difference between MCP and A2A?
- Is a Skill a tool, an agent, or instructions?
- Why do I still need OAuth, schemas, API contracts, and observability if I am using agents?

The architect should be able to answer without hiding behind product vocabulary.

### Existing course material

Use Canon 01 as the model baseline:
- training vs. inference,
- weights vs. embeddings,
- contextual representation,
- vector retrieval,
- activation vs. retrieval,
- external evidence,
- the limits of "RAG everywhere."

Use Canon 03 when connecting the basics to the larger agent system:
- model vs. agent,
- runtime vs. harness,
- tools,
- state,
- trigger,
- delegation.

### Exercise

Part 1: Explain the difference between:
1. model knowledge,
2. retrieved evidence,
3. enterprise system-of-record data,
4. current task context,

to a nontechnical executive in five minutes.

Part 2: Given an agent that must read a policy, perform a workflow, call a claims API, delegate a specialist review to another agent, and stream progress to a user interface, identify which concerns belong to:
- Skill,
- MCP,
- A2A,
- OpenAPI / JSON Schema,
- identity / authorization,
- observability,
- and application UI interaction.

---

## Module 2 — Architecture Starts Before the AI

### Topic description

This establishes the operating principle for the entire course.

### What I teach

- Always tie the architecture to a real business problem.
- Business problem -> outcome -> process -> decisions -> evidence -> controls -> architecture -> technology is the executive shorthand.
- Frame -> Observe -> Decompose -> Govern -> Redesign -> Architect -> Specify -> Select -> Prove -> Learn is the practitioner methodology.
- The methodology is iterative, not a literal waterfall.
- Technology-led experimentation is legitimate.
- Technology-led production architecture is dangerous.
- AI can make a bad process operate faster.
- AI can automate a decision that should not have been automated.
- AI can scale architectural mistakes extremely efficiently.

### Customer explanation

The question is not:

**"What can this model do?"**

The better architecture question is:

**"What does this business process need to accomplish, and where can machine reasoning improve it?"**

### Existing course material

- Canon 02: Process-first AI architecture.
- LinkedIn Post 1: "AI Architecture Starts Before the AI."
- Infographic: "Starting with the model is not strategy."

### Exercise

Give the class a technology-first request:

> "We need an agent that uses RAG on our policy documents."

Force the team to work backward until they can state:
- the business problem and desired outcome,
- the observed current-state process,
- the work and decision decomposition,
- the evidence, authority, and controls,
- and the capability requirements implied by the redesigned process.

Then decide whether an agent and RAG are still required.

---

## Module 3 — Process Discovery and Process Mapping

### Topic description

This should be one of the largest sections of the course.

The most important engineering in the AI world is process engineering. If the architect cannot discover and describe the real process, the rest of the AI architecture is guesswork.

### What I teach

#### A. Start with scope, not shapes

Before drawing a flowchart, define:

- process name,
- business owner,
- trigger,
- starting state,
- ending state,
- desired outcome,
- customer or beneficiary,
- unit of work / case,
- systems involved,
- actors involved,
- known constraints,
- major measures,
- in-scope and out-of-scope boundaries.

#### B. Build the current-state map

Capture:

- activities,
- actors / swimlanes,
- systems,
- inputs,
- outputs,
- decisions,
- decision criteria,
- required evidence,
- handoffs,
- waits,
- queues,
- approvals,
- exceptions,
- escalations,
- rework loops,
- real-world actions,
- automation already present,
- state changes,
- completion evidence,
- latency,
- failure conditions.

Do not sanitize the process while discovering it.

The current-state map should describe what actually happens, including awkward workarounds.

#### C. Separate process flow from decision logic

Use process notation for the work flow and decision modeling for significant choices.

BPMN is useful for formal process notation.

DMN is useful when a decision has explicit inputs, rules, or decision logic.

The course does not need to become BPMN certification. The architect needs enough notation discipline to produce an unambiguous process model.

#### D. Use a process hierarchy

A process taxonomy such as APQC's Process Classification Framework can help locate the process in a broader enterprise context.

The architect should understand the difference between:
- enterprise capability,
- process family,
- process,
- activity,
- task,
- decision.

#### E. Separate current-state truth from future-state design

Do not treat "process" as one design step.

The current-state model establishes how work actually happens.

The future-state model is a separate redesign pass that determines how the process should operate when deterministic automation, machine reasoning, human judgment, governed delegation, and real-world boundaries are deliberately recomposed.

Build the future-state map only after the current state is understood.

Ask:
- What work disappears?
- What work becomes deterministic automation?
- What work requires reasoning?
- What work remains human?
- What evidence can be assembled automatically?
- Which decisions can be delegated?
- Which decisions require approval?
- Which boundaries become new state transitions?
- What must be observable?

### Process discovery evidence ladder

Treat process discovery as an evidence problem.

A useful source hierarchy is:

1. **System event logs** — evidence of what the system recorded as happening.
2. **Task / screen capture** — evidence of what a worker actually did in the interface.
3. **Documents and SOPs** — evidence of the designed or documented process.
4. **Whiteboards and workshop artifacts** — evidence of what participants collectively described.
5. **Interview / meeting transcripts** — evidence of what participants said happens.
6. **Memory and anecdote** — useful, but least authoritative by itself.

These sources can disagree.

That disagreement is useful.

Do not let AI silently reconcile contradictions. Surface them for validation.

### Automating process discovery

There are now several ways to accelerate process mapping.

#### Transcript -> process map

1. Ingest the transcript.
2. Identify actors and roles.
3. Extract actions in chronological order.
4. Identify decisions and conditional branches.
5. Extract inputs, outputs, evidence, systems, waits, approvals, exceptions, and handoffs.
6. Normalize synonyms without losing the source wording.
7. Create a structured intermediate representation of nodes and edges.
8. Generate a draft flowchart/BPMN-style model.
9. Link each extracted element back to the transcript segment that supports it.
10. Have process owners validate the map.

The AI-generated map is a hypothesis, not source truth.

#### Whiteboard -> process map

For digital boards:
- use board objects, sticky notes, images, and text as context,
- cluster related material,
- extract actors/actions/decisions,
- generate a draft diagram.

For photographs of physical whiteboards:
1. use image/vision processing to recover sticky notes, text, arrows, groupings, and spatial relationships,
2. convert that material to structured process elements,
3. generate an editable diagram,
4. validate the interpretation with the workshop participants.

#### Screen recording / task capture -> process map

Screen or task capture can reveal:
- clicks,
- application transitions,
- manual copy/paste,
- repetitive data entry,
- waiting,
- rework,
- hidden handoffs.

This is especially useful when people describe the official process but perform a different process.

#### Event logs -> process mining

Where systems produce event data, process mining can reconstruct observed paths and process variants.

At minimum, classic process-mining event data normally needs:
- case identifier,
- activity,
- timestamp.

The result can expose:
- dominant path,
- variants,
- loops,
- delays,
- rework,
- conformance problems,
- bottlenecks.

### Canonical principle used by this module

> **Process maps used for AI architecture should be evidence-backed models of work, not workshop artwork.**

This principle is now part of Canon 02.

### Public tools to demonstrate

Tool-neutral concepts first, then examples:
- BPMN 2.0 / DMN standards.
- APQC Process Classification Framework.
- Microsoft Power Automate Process Mining.
- SAP Signavio Process Intelligence.
- Celonis process mining.
- Miro AI for text/board-context diagram generation and sticky capture.
- Lucid AI for text/image-to-diagram and Process Capture from screen recordings.

### Exercise

Give students:
- a 30-minute discovery transcript,
- a photo of a whiteboard,
- a short SOP,
- and a small event log.

Have them produce:
1. an evidence-backed as-is process map,
2. a list of contradictions between sources,
3. a work decomposition inventory,
4. a decision inventory for the places where reasoning or judgment occurs,
5. an automation-boundary inventory,
6. a future-state candidate map.

---

## Module 4 — Decompose the Work: Find the Places Where Reasoning Actually Matters

### Topic description

Not every process step needs AI, and decisions are not the only places architecture matters.

The architect must decompose the process into the kinds of work that affect execution: activities, decisions, actions, transformations, waits, state changes, boundaries, exceptions, loops, escalations, handoffs, and outcomes.

Then identify the places where the process contains uncertainty, judgment, classification, prioritization, interpretation, prediction, recommendation, approval, or exception handling.

### What I teach

First classify the work as:
- deterministic execution,
- probabilistic reasoning,
- human judgment,
- external or physical action.

For every material decision capture:
- decision owner,
- decision question,
- inputs,
- evidence,
- rules,
- uncertainty,
- consequence of error,
- frequency,
- latency requirement,
- reversibility,
- approval requirement,
- current decision method,
- candidate execution mode.

### Candidate execution modes

A decision may be:
- deterministic rule,
- deterministic calculation,
- traditional predictive model,
- LLM reasoning,
- agentic reasoning with tools,
- human judgment,
- hybrid / human approval.

Do not use an LLM merely because a box is labeled "decision."

### Standards connection

DMN provides a useful established method for explicitly modeling business decisions and rules alongside process models.

### Exercise

Take one process and first identify its activities, decisions, actions, waits, state changes, boundaries, exceptions, handoffs, and outcomes.

Then classify every material decision or action by:
- deterministic vs. probabilistic,
- low vs. high consequence,
- static vs. volatile evidence,
- reversible vs. irreversible,
- machine-executable vs. human-required.

---

## Module 5 — Evidence Before Reasoning

### Topic description

This is where the architecture departs sharply from "the model can probably answer it."

Evidence is not only an input to a decision. It may also authorize an action, establish current state, prove completion, trigger re-entry, or demonstrate that a control was satisfied.

### What I teach

The first question is:

**What evidence does the system need before it should be allowed to answer or act?**

The Evidence-First Gate:

**Assess risk and volatility -> Acquire evidence -> Validate authority, provenance, and freshness -> Reason -> Act**

Teach:
- authoritative source,
- provenance,
- freshness,
- volatility,
- confidence,
- completeness,
- scope,
- ownership,
- review status,
- governance classification.

### Core principle

> **Data quality defines reasoning quality.**

A more capable model reasoning over stale or ungoverned evidence can produce a more convincing wrong answer.

### Existing course material

- Canon 02: Evidence-First Gate.
- LinkedIn Post 3: "Evidence Before Reasoning."

### Exercise

For each consequential decision or action in the process map, build an Evidence Requirement Card:
- evidence needed,
- source,
- authority,
- freshness requirement,
- volatility,
- provenance requirement,
- access rule,
- consequence if missing,
- fallback behavior.

---

## Module 6 — Information Architecture for Governed Reasoning

### Topic description

Once we know what evidence consequential decisions and actions require, we can design how the enterprise makes that evidence available.

### What I teach

The three-layer model:

1. **Systems of Record** — what happened / what the organization formally knows.
2. **Governed Knowledge Layer** — what we know and how it should be understood.
3. **Agent Context / Evidence Layer** — what this agent needs right now for this decision.

Teach:
- semantic relationships,
- governed summaries,
- embeddings,
- policy,
- provenance,
- freshness,
- volatility,
- confidence,
- authorization,
- federation vs. duplication,
- current evidence vs. enterprise knowledge.

### Canonical principles

> **Don't move governed data to AI. Move AI reasoning to governed knowledge.**

> **Organize the trustworthiness and lifecycle of information, not merely the information itself.**

### Volatility

Teach the working V0-V5 volatility model as provisional:
- stable,
- slow,
- periodic,
- active,
- real-time,
- critical-current.

Volatility should influence retrieval, caching, refresh, review, and confidence decay.

### Exercise

Take the Evidence Requirement Cards from Module 5 and place each evidence source into:
- source-of-truth system,
- governed knowledge service,
- task context assembly,
- external authoritative lookup.

---

## Module 7 — Data Design for AI: Structures, Stores, Motion, and Context

### Topic description

This is a survey, not a database engineering class.

The architect needs to understand the major ways enterprise information is represented, stored, moved, indexed, related, governed, and assembled into AI context.

There is no single "AI database."

The purpose of this module is not to teach architects to start with a list of database types and pick one.

It is to teach them to start with the **required use of the information**.

### Start with the use requirement, not the store

The first question is:

> **What does the system need to do with this data?**

For example, does the system need to:
- preserve authoritative transactional state,
- retrieve a record by identity,
- aggregate large historical datasets,
- traverse relationships,
- find semantically similar content,
- perform exact lexical search,
- react when state changes,
- reconstruct history,
- reason over time or location,
- maintain workflow state,
- assemble task-specific evidence,
- or temporarily cache context for low-latency execution?

Only after answering that question should the architect derive:
- the logical representation,
- access pattern,
- read/write pattern,
- latency,
- freshness and volatility,
- consistency,
- relationship model,
- temporal requirements,
- authority,
- provenance and lineage,
- governance,
- retention,
- and failure / reconciliation behavior.

Those requirements determine the structure, store, index, movement pattern, and technology.

### Canonical principle used by this module

> **Design data from the required use backward. What the system must do with the data determines the representation, access pattern, and technology — not the other way around.**

This is the data-specific application of:

> **Architecture defines the required capabilities. Technology is selected to implement them.**

### One source, multiple legitimate representations

The same authoritative information may need several derived representations because the system has several different requirements.

For example, the same business entity might be:
- stored relationally as authoritative transactional state,
- projected into a search index for lexical retrieval,
- embedded into a vector index for semantic retrieval,
- emitted as events for real-time reaction,
- aggregated into analytical tables for historical analysis,
- or exposed as a graph for relationship traversal.

The requirement justifies the projection.

The projection does not become authoritative merely because it is optimized for that use.

The architect must preserve the path back to source evidence, provenance, reconciliation, and governance.

### Data in Motion as the conceptual bridge

Use the Data in Motion presentation as the teaching story, but generalize it beyond customer profiles and Adobe products.

#### Data at rest — queries in motion

The traditional pattern:
- data is persisted,
- a query is created when someone needs an answer,
- the query scans or joins the stored data,
- results are materialized for a report, list, decision, or downstream process.

This remains entirely valid.

The problem is using it as the only pattern when the process requires current state.

#### Data in motion — standing logic against changing state

A different pattern:
- events arrive continuously,
- state or profiles are updated,
- standing rules, features, segments, models, or policies are evaluated as the state changes,
- downstream interaction can react to the new state.

The critical architectural shift is from repeatedly reconstructing context from disconnected data toward maintaining or assembling current context at the time the decision needs it.

### Technical correction to the shorthand

The presentation uses the phrase:

> AI doesn't operate on raw data — it operates on context.

Keep the teaching idea, but make it technically precise:

> **Models reason over representations placed into their execution context. Architecture determines how raw, authoritative, derived, and semantic data are transformed into those representations.**

Raw data is not inherently unusable. The issue is whether it has the structure, semantics, identity, freshness, authority, and context required for the task.

### Profiles, entities, features, and derived context

Teach the useful ideas from the Data in Motion model:

- streaming events can update an entity or profile view,
- a profile is a logical collection of related attributes about an entity, not necessarily one physical table,
- derived classifications such as segment membership can become features or context signals,
- changing state can trigger re-evaluation,
- governance labels and policies can apply at the data-element level,
- content should also be treated as data with metadata, attributes, provenance, and policy,
- content attributes and entity/context attributes can be combined at decision time,
- when information crosses system boundaries, meaning and policy must survive any transformation or integration.

### Survey of major data structures and store patterns

The goal is recognition and architectural placement, not implementation mastery.

#### 1. Relational / row-oriented data

Examples:
- transactional records,
- orders,
- claims,
- accounts,
- normalized business entities.

Good for:
- strong relationships,
- transactions,
- constraints,
- authoritative state,
- SQL access.

Architectural question:
**Is this the system of record, or merely a copy optimized for another purpose?**

#### 2. Columnar / analytical data

Examples:
- warehouses,
- analytical tables,
- Parquet-backed datasets,
- columnar execution engines.

Good for:
- scans,
- aggregations,
- historical analysis,
- feature generation,
- large-scale analytical workloads.

Teach the distinction between row-optimized transactional access and column-optimized analytical access.

#### 3. Document / semi-structured data

Examples:
- JSON documents,
- XML documents,
- application objects,
- API payloads.

Good for:
- flexible schemas,
- nested structures,
- objects that are naturally retrieved together.

Important distinction:
A document database and a document corpus for retrieval are not the same architectural responsibility.

#### 4. Key-value data

Good for:
- fast lookup by key,
- cache,
- session state,
- feature lookup,
- idempotency keys,
- small pieces of workflow state.

The architect should recognize when relational semantics are unnecessary overhead.

#### 5. Wide-column data

Good for:
- very large sparse datasets,
- high write throughput,
- access patterns organized around known partition keys.

Survey only; emphasize that the access pattern must be designed before the schema.

#### 6. Graph data

Two useful families:

**Property graphs**
- entities and relationships with properties,
- traversal-heavy application questions.

**Semantic / RDF knowledge graphs**
- triples / statements,
- ontologies,
- shared semantics,
- inference and linked knowledge.

Good for:
- relationship-rich reasoning,
- dependency and lineage analysis,
- semantic knowledge representation.

Do not teach "knowledge graph" as a synonym for "AI database."

#### 7. Vector / embedding indexes

Store numerical representations optimized for similarity search.

Good for:
- semantic retrieval,
- nearest-neighbor search,
- matching related content or entities.

Important principle:

> **A vector index is an access structure for similarity retrieval, not the authoritative source of truth.**

Teach hybrid retrieval:
- lexical / keyword,
- metadata filters,
- relational constraints,
- graph relationships,
- vector similarity,
- reranking.

#### 8. Search / inverted indexes

Good for:
- keyword and lexical search,
- faceting,
- filters,
- ranking,
- log and document search.

This is often complementary to vector search rather than obsolete because vector search exists.

#### 9. Time-series data

Good for:
- measurements over time,
- telemetry,
- sensors,
- operational metrics,
- financial or market sequences,
- environmental data.

Teach:
- timestamp semantics,
- sampling rate,
- retention,
- aggregation windows,
- late-arriving data.

#### 10. Geospatial data

Good for:
- location,
- distance,
- containment,
- routes,
- spatial relationships.

Important when physical-world agents or business processes reason about place.

#### 11. Event streams / append-only logs

Examples:
- business events,
- clickstreams,
- transactions,
- CDC events,
- device events.

Good for:
- data in motion,
- event-driven state updates,
- replay,
- temporal reconstruction,
- triggering workflows.

Teach the difference between:
- an event,
- current state,
- and a materialized view derived from events.

#### 12. Object / blob / unstructured content stores

Examples:
- PDFs,
- images,
- audio,
- video,
- office documents,
- scanned records.

AI architectures frequently need to derive:
- text,
- chunks,
- metadata,
- embeddings,
- captions,
- structured facts,
- provenance

without losing the original authoritative artifact.

#### 13. Multimodal content structures

Treat image, audio, video, text, layout, and associated metadata as related evidence.

Content fragments, versions, rights, source, audience, language, modality, and generation history may all matter to context assembly.

#### 14. Entity / profile views

A profile is a logical, current representation of an entity assembled from identifiers, attributes, events, derived features, relationships, and policy.

Teach:
- identity resolution,
- merge rules,
- source priority,
- freshness,
- temporal validity,
- derived vs. authoritative attributes.

A profile may be physically materialized or assembled on demand.

#### 15. Feature stores and derived features

Features are machine-usable derived signals.

Examples:
- segment membership,
- risk score,
- recency,
- propensity,
- aggregate behavior.

Teach the risk of losing:
- source lineage,
- feature definition,
- calculation time,
- validity window,
- training/serving consistency.

#### 16. Workflow / process state

This is not the same as model memory.

Process state records what the business workflow currently believes has happened.

Examples:
- current case state,
- approval status,
- retry count,
- pending external action,
- completion evidence.

This state often belongs in deterministic storage even when reasoning is probabilistic.

#### 17. Cache and ephemeral context

Useful for:
- low-latency repeated access,
- temporary context assembly,
- session acceleration.

The architect must define:
- TTL,
- invalidation,
- authority,
- whether stale data is safe.

### Survey of data formats and interoperability representations

Architects should recognize the major families:

- **CSV / delimited text** — portable tabular interchange, weak typing.
- **JSON** — ubiquitous semi-structured interchange.
- **XML** — structured interchange with strong enterprise and industry-standard usage.
- **JSON Schema** — structure and validation for JSON.
- **Avro / Protocol Buffers** — schema-driven serialization, common in service and event pipelines.
- **Parquet / ORC** — columnar analytical file formats.
- **Arrow** — standardized in-memory columnar representation and interchange.
- **Iceberg / Delta / Hudi** — table formats over object storage; understand the role even if implementation details vary.
- **RDF / JSON-LD** — semantic linked-data representations.
- **media-native formats** — images, audio, video, PDFs and documents retain value as authoritative evidence even when derived representations are created.

### Data movement patterns the architect should recognize

- batch ETL,
- ELT,
- change data capture,
- event streaming / pub-sub,
- request-response API access,
- file exchange,
- federated query,
- stream processing,
- materialized views,
- cache,
- reverse ETL / activation,
- replication,
- synchronization,
- on-demand retrieval.

The question is not "batch or streaming?"

The question is:

> **How current must this evidence be when the decision is made, and what movement pattern satisfies that requirement without destroying authority, governance, or cost discipline?**

### Metadata is part of the data design

For AI, the record alone is often insufficient.

The design should consider:
- identity / key,
- source,
- provenance,
- event time,
- processing time,
- effective time,
- freshness,
- volatility,
- owner,
- policy / classification,
- confidence,
- review state,
- lineage,
- version,
- relationships,
- retention,
- consent / purpose,
- rights and permitted use.

This reinforces the canon:

> **Organize the trustworthiness and lifecycle of information, not merely the information itself.**

### Data design decision criteria

For each evidence, state, event, content, or knowledge requirement ask in this order:

1. **What does the system need to do with this information?**
2. Which business decision, action, state transition, or evidence requirement does that use support?
3. What is the authoritative source?
4. What access pattern must be optimized?
5. What is the logical data shape required by that access pattern?
6. Is the requirement transactional, analytical, semantic, event-driven, document-oriented, temporal, spatial, or some combination?
7. How current must the data be?
8. How volatile is it?
9. What consistency is required?
10. What relationships matter?
11. What latency and scale must be supported?
12. What metadata and provenance must travel with it?
13. What security, privacy, consent, residency, retention, or purpose policy applies?
14. What transformation creates any derived representation?
15. Can the derived form be traced back to authoritative evidence?
16. How will the data enter task-specific agent context or deterministic execution?
17. What happens when the authoritative source and a derived representation disagree?
18. Only now: what structure, store, index, movement pattern, or technology satisfies those requirements?

### Anti-patterns

- Starting with "we need a graph/vector database/lakehouse" before defining the system requirement.
- Choosing a database because the data superficially resembles its marketing category.
- "Put everything in a vector database."
- "Embed everything."
- Treating the retrieval index as the source of truth.
- Copying governed data into an AI store without preserving policy and lineage.
- Treating a profile as one mandatory physical repository.
- Assuming real-time architecture is always better than batch.
- Allowing event streams, caches, features, or embeddings to drift from authoritative state.
- Treating model memory as enterprise process state.
- Stripping metadata and provenance while transforming data for AI.

### Existing course material

Use:
- Canon 02: AI-ready information architecture.
- Canon 02: systems of record -> governed knowledge -> agent context/evidence.
- Canon 02: volatility and continuous knowledge synchronization.
- Data in Motion presentation: data at rest vs. data in motion, profiles, segments as derived context signals, real-time re-evaluation, element-level governance, and content as attributed data.

### Exercise

Give students one AI-enabled business process with:
- transactional records,
- documents,
- streaming events,
- a customer or case profile,
- unstructured content,
- a graph relationship,
- historical analytics,
- and a semantic retrieval requirement.

Have them build an **AI Data Design Matrix** that identifies for each data requirement:
- required system use,
- business decision / action / state / evidence need,
- authoritative source,
- logical structure,
- storage / index pattern,
- access pattern,
- freshness / volatility,
- movement pattern,
- schema / format,
- identity,
- metadata / provenance,
- governance,
- transformation,
- derived representations,
- task-context use,
- fallback when data is missing or stale.

Then ask the team to defend each data choice in this order:

**requirement -> representation -> access pattern -> derived capability -> technology**

If they have to begin the explanation with the name of a database technology, they have skipped the design step.

---

## Module 8 — Automation Boundaries and Real-World State

### Topic description

The goal is not to automate everything.

The goal is to engineer the entire process so automated and non-automated work operate as one coherent system.

### What I teach

An Automation Boundary occurs when:
- a human acts,
- a customer responds,
- a physical task occurs,
- another organization acts,
- a regulated approval is required,
- an external system changes state outside our control.

For each boundary define:

1. Trigger.
2. Actor.
3. Required action.
4. Context that must survive the handoff.
5. Evidence / proof of outcome.
6. Latency and escalation.
7. Re-entry condition.

### Core principle

> **A handoff is not complete when the real-world action happens. It is complete when the system receives evidence of the outcome and updates its state.**

The boundary is a governed state transition.

### Existing course material

- LinkedIn Post 2: "The Goal Is Not to Automate Everything."
- Automation Boundary infographic.
- Canon 03 closed-loop concepts.

### Exercise

Take a process with a field technician, nurse, legal approval, or customer consent step.

Design the handoff and re-entry contract in enough detail that the automated system cannot continue from stale state.

---

## Module 9 — From Model to Agentic System

### Topic description

Only after the current process has been observed and decomposed, the future state has been redesigned, and evidence, authority, controls, and boundaries are understood do we introduce the agent architecture.

### What I teach

- Chat is an interaction context.
- Agent is an execution context.
- The model is not the agent.
- Runtime and harness are different.
- Agentic systems combine probabilistic reasoning and deterministic execution.
- Instruction design becomes executable architecture.

### Canonical assembly formula

> **Harness governs. Runtime executes. Model reasons. Tools act. State remembers. Trigger starts. The agent is the assembled workflow pursuing the delegated goal.**

### Teach each component by asking WHY it exists

**Model** — reasoning capability.  
**Tools** — retrieve evidence or change external state.  
**State** — preserve task progress and current process condition.  
**Trigger** — starts work.  
**Runtime** — executes the workflow and handles cycles, waits, retries, tool calls.  
**Harness** — constrains, validates, observes, governs, and stops execution.  
**Instructions / skills** — encode task and domain behavior.  
**Deterministic code** — executes responsibilities that should not be left to probabilistic reasoning.

### Exercise

Give students a product diagram labeled "AI Agent."

Make them decompose it into the actual execution and governance responsibilities.

---

## Module 10 — Evidence, Authority, Controls, Risk, and the Harness

### Topic description

Governance starts before the harness.

For each consequential decision or action, the architect must distinguish:
- **Evidence:** what must be known,
- **Authority:** who or what is allowed to decide or act,
- **Control:** under what conditions that authority may be exercised.

The harness is one of the primary places those requirements become operational.

The governing architecture question is:

> **Given this state, with this evidence, under this authority, may this system perform this action?**

### What I teach

A production harness may control:
- evidence requirements,
- identity,
- permissions,
- model policy,
- tool policy,
- context rules,
- memory rules,
- input/output validation,
- confidence thresholds,
- human approval,
- retries,
- error handling,
- time limits,
- cost limits,
- stop conditions,
- observability,
- audit.

### Control design rule

Authority and controls should trace back to:
- decision consequence,
- data sensitivity,
- regulatory obligation,
- process responsibility,
- authority,
- reversibility,
- blast radius.

Do not add "guardrails" as a generic box after the architecture is complete.

### External alignment

Use NIST AI RMF / GenAI Profile as a governance reference and established cloud well-architected guidance as supporting material, without turning the course into a vendor framework.

### Exercise

Create a Governance Matrix for the target process:
- consequential decision or action,
- required evidence,
- authorized actor or system,
- control,
- enforcement point,
- evidence that the control operated,
- owner,
- failure behavior.

---

## Module 11 — Delegation, Domains, and Execution Authority

### Topic description

A central enterprise agent should not accumulate every credential and permission in the organization.

### What I teach

> **Reason where the enterprise has context. Act where the domain has authority.**

A governed environment can delegate a bounded task into another governed environment.

The Delegation Contract defines:
- task / intent,
- allowed purpose,
- bounded context,
- evidence,
- provenance,
- allowed actions,
- prohibited actions,
- authorization owner,
- audit owner,
- result contract,
- rejection semantics,
- escalation,
- expiry,
- human approval.

### Core principle

> **Delegation transfers a bounded task, not unlimited authority.**

Teach why two harnesses can legitimately disagree.

The receiving domain remains authoritative for the actions it owns.

### Exercise

Design an enterprise-to-domain delegation:
- enterprise customer reasoning -> marketing execution,
- clinical reasoning -> care workflow,
- fraud reasoning -> transaction intervention,
- legal analysis -> filing workflow.

---

## Module 12 — Evaluation, Observability, and Closed-Loop Learning

### Topic description

We need to prove that the architecture works, not merely that the model produced a plausible answer.

Evaluation is an architectural responsibility because failure can occur in reasoning, evidence, authority, controls, process execution, state transitions, handoffs, or outcomes.

### What I teach

Evaluate at several levels:

#### Model / reasoning quality
- correctness,
- groundedness,
- evidence usage,
- uncertainty,
- refusal/escalation behavior.

#### Process quality
- cycle time,
- completion rate,
- rework,
- exception rate,
- escalation,
- customer outcome.

#### Tool / action quality
- correct tool selection,
- valid parameters,
- action success,
- idempotency,
- failure recovery.

#### Boundary quality
- context preservation,
- completion evidence,
- stale-state incidents,
- re-entry correctness.

#### Governance quality
- authorization,
- provenance,
- policy compliance,
- audit completeness.

#### System / operating quality
- state-transition correctness,
- intervention rate,
- residual risk,
- latency,
- cost,
- behavior relative to the pre-AI baseline.

### Prove, then learn

The practitioner methodology does not end at technology selection.

**Prove** tests whether the redesigned process and architecture actually achieve the intended outcome within acceptable risk, cost, and operational limits.

**Learn** treats operational outcomes as new evidence:

**Observe -> Govern -> Reason -> Delegate -> Act -> Observe outcome -> Update knowledge -> Refine**

Observed outcomes do not automatically become trusted knowledge.

Feedback itself needs provenance, authority, validation, and reconciliation.

### Exercise

Build an Evaluation Plan before selecting the implementation platform.

---

## Module 13 — Technology Selection: Plugging Tools into the Architecture

### Topic description

Technology selection follows capability specification.

The curriculum needs a repeatable way to translate the architecture into capability requirements and then evaluate specific tools without allowing the tool to define the architecture.

### Tool Placement Framework

Before evaluating products, write the capability requirement without a product name.

For every proposed product, service, model, framework, or platform ask:

1. **What capability requirement does it satisfy?**
2. **Which step in the process does it support?**
3. **Which decision does it enable?**
4. **What evidence does it consume or produce?**
5. **What state does it own?**
6. **What authority does it have?**
7. **What boundary does it cross?**
8. **What controls does it enforce?**
9. **What happens when it fails?**
10. **How is it observed and evaluated?**
11. **What data or context leaves an existing governance boundary?**
12. **How replaceable is it?**
13. **What capability disappears if the product disappears?**
14. **Could a simpler deterministic component satisfy the same requirement?**

### Capability categories to plug products into

- reasoning model,
- model gateway / model policy,
- retrieval,
- vector search,
- enterprise search,
- knowledge graph,
- evidence service,
- context assembly,
- workflow engine,
- agent runtime,
- harness / policy,
- identity and permissions,
- tool / API layer,
- MCP infrastructure,
- deterministic compute,
- state / memory,
- human approval,
- process mining,
- task mining,
- observability / tracing,
- evaluation,
- audit,
- data governance,
- eventing,
- integration,
- domain execution,
- API contracts / OpenAPI,
- asynchronous API contracts / AsyncAPI,
- event envelope / CloudEvents,
- agent interoperability / MCP / A2A,
- skill packaging / distribution,
- relational / transactional data,
- analytical / columnar data,
- document data,
- graph / knowledge data,
- vector indexes,
- search indexes,
- time-series / geospatial data,
- event streams,
- object / multimodal content,
- feature / profile data,
- lineage / provenance.

### Anti-pattern

Do not compare Agent Platform A to Agent Platform B until the required capabilities have been defined.

Otherwise the vendor's product taxonomy becomes the architecture.

### Exercise

Have teams map several vendors into the same capability architecture and identify:
- overlaps,
- gaps,
- lock-in,
- redundant capabilities,
- governance boundaries,
- replacement seams.

---

## Module 14 — Capstone: Redesign a Real Enterprise Process

### Goal

Produce an architecture from a business process rather than a product list.

### Required deliverables

1. Business problem statement.
2. Outcome measures.
3. Current-state process map.
4. Process discovery source inventory and provenance.
5. Work decomposition inventory, including decisions, actions, waits, state changes, boundaries, exceptions, handoffs, and outcomes.
6. Decision inventory where reasoning or judgment occurs.
7. Evidence Requirement Cards.
8. Governance Matrix covering evidence, authority, and controls.
9. Automation Boundary definitions.
10. Future-state AI-enabled process map.
11. Knowledge / evidence architecture.
12. AI Data Design Matrix covering authoritative source, data structure, access pattern, movement, freshness, provenance, governance, and derived representations.
13. Agent/runtime/harness decomposition where needed.
14. Delegation contracts where needed.
15. Evaluation and observability plan.
16. Technology capability requirements.
17. Tool mapping and selection rationale.
18. Executive explanation of why the design exists.

### Final defense

The student should be able to explain the design twice:

- once to the engineering team,
- once to the business executive.

If the explanation depends on product names, the architecture is not finished.

---

# Recommended course artifacts

The methodology should eventually ship with reusable templates.

## 1. Business Problem / Outcome Card
- problem,
- affected process,
- beneficiary,
- unit of work,
- stakeholders,
- baseline,
- desired outcome,
- measures,
- constraints,
- unacceptable outcomes.

## 2. Process Discovery Worksheet
- scope,
- trigger,
- completion,
- actors,
- systems,
- activities,
- decisions,
- evidence,
- authority,
- handoffs,
- waits,
- exceptions,
- controls,
- sources used to validate each claim.

## 3. Work Decomposition Inventory
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
- outcomes,
- execution mode.

## 4. Decision Inventory
- decision,
- owner,
- inputs,
- evidence,
- consequence,
- frequency,
- reversibility,
- execution mode.

## 5. Evidence Requirement Card
- consequential decision or action,
- evidence,
- authoritative source,
- freshness,
- volatility,
- provenance,
- permissions,
- fallback.

## 6. AI Data Design Matrix
- required system use,
- business decision / action / state / evidence need,
- authoritative source,
- logical data structure,
- physical store / index pattern,
- access pattern,
- freshness / volatility,
- consistency requirement,
- movement pattern,
- schema / format,
- identity / key,
- metadata,
- lineage / provenance,
- governance / policy,
- transformation,
- derived representations,
- context-assembly role,
- retention,
- fallback / reconciliation.

## 7. Automation Boundary Contract
- trigger,
- actor,
- required action,
- context,
- proof of completion,
- latency / escalation,
- re-entry condition.

## 8. Governance Matrix
- consequential decision or action,
- required evidence,
- authorized actor or system,
- risk,
- control,
- enforcement point,
- owner,
- audit evidence,
- failure behavior.

## 9. Delegation Contract
- purpose,
- task,
- context,
- evidence,
- allowed authority,
- prohibited actions,
- result,
- rejection,
- expiry,
- approvals.

## 10. Tool Placement Card
- required capability,
- process role,
- decision role,
- evidence,
- state,
- authority,
- control,
- interfaces,
- failure,
- observability,
- portability.

## 11. Evaluation Plan
- reasoning metrics,
- process metrics,
- action metrics,
- boundary metrics,
- risk metrics,
- operational metrics.

---

# Public material reviewed for this draft

These are supporting references, not adopted canon.

## Architecture methods and business-process foundations

### TOGAF Architecture Development Method
Useful because it reinforces that architecture is a method tied back to business needs and iteratively moves from business architecture toward information systems and technology architecture.

Reference:
https://www.opengroup.org/architecture/togaf7-doc/arch/p2/p2_intro.htm

### OMG BPMN 2.0.2
The formal Business Process Model and Notation standard. Useful as the process-language foundation.

Reference:
https://www.omg.org/spec/BPMN/2.0.2/

### OMG DMN
Useful for separating decision logic from process flow and making decisions explicit.

Reference:
https://www.omg.org/dmn/

### APQC Process Classification Framework
Useful as an enterprise process taxonomy and common naming framework.

Reference:
https://www.apqc.org/process-frameworks

---

# Agent interoperability and supporting standards reviewed

These are supporting standards, protocols, and conventions for the baseline course. They are not automatically architecture requirements.

## Model Context Protocol (MCP)
Open protocol for connecting LLM applications to external tools, resources, prompts, and context. The 2026-07-28 revision is the current baseline used for this curriculum.

Reference:
https://modelcontextprotocol.io/specification/2026-07-28

## Agent Skills
Open format for reusable agent procedures centered on `SKILL.md`, with optional scripts, references, and assets.

Reference:
https://agentskills.io/specification

## MCP Skills extension
Defines a transport binding for publishing and consuming Agent Skills through MCP.

Reference:
https://skills.extensions.modelcontextprotocol.io/specification/stable/skills

## Agent2Agent (A2A)
Open standard for discovery, communication, task management, and collaboration between independent agent systems.

Reference:
https://a2a-protocol.org/

## OpenAPI
Machine-readable, language-agnostic description of HTTP APIs.

Reference:
https://spec.openapis.org/oas/latest.html

## JSON Schema
Standard vocabulary for describing and validating JSON structure.

Reference:
https://json-schema.org/specification

## AsyncAPI
Machine-readable contracts for asynchronous and event-driven APIs.

Reference:
https://www.asyncapi.com/docs/reference/specification/v3.1.0

## CloudEvents
Common specification for describing event data.

Reference:
https://cloudevents.io/

## OpenID Connect / OAuth
Identity and authorization standards used to secure human, application, tool, and delegated access.

Reference:
https://openid.net/specs/openid-connect-core-1_0.html

## OpenTelemetry
Common telemetry model and semantic conventions for traces, metrics, logs, and GenAI operations.

Reference:
https://opentelemetry.io/docs/specs/semconv/

## Emerging awareness: AG-UI, A2UI, AGENTS.md
Useful emerging conventions for agent-user interaction, declarative agent-generated UI, and coding-agent project instructions. Teach awareness and architectural boundary, not mandatory adoption.

References:
https://github.com/ag-ui-protocol/ag-ui
https://a2ui.org/
https://aaif.io/projects

---

# Data structures, formats, and provenance material reviewed

## Data in Motion — The AI Version
Internal presentation used as the conceptual source for:
- data at rest vs. data in motion,
- profiles as evolving collections of related attributes,
- segments / classifications as derived context signals,
- state-change-driven re-evaluation,
- element-level governance,
- content as attributed data,
- combining profile and content attributes at decision time.

## Apache Arrow
Standardized in-memory columnar representation and interchange for analytical data.

Reference:
https://arrow.apache.org/docs/format/

## Apache Parquet
Column-oriented file format for efficient analytical storage and retrieval.

Reference:
https://parquet.apache.org/docs/overview/

## Apache Avro
Schema-driven data serialization used heavily in event and data pipelines.

Reference:
https://avro.apache.org/docs/current/specification/

## Apache Iceberg
Open table format for large analytical tables over distributed/object storage.

Reference:
https://iceberg.apache.org/spec/

## OpenLineage
Open lineage and metadata collection API for data pipelines.

Reference:
https://openlineage.io/

## RDF / semantic graph standards
W3C standards for graph-based semantic representation. Teach the mature RDF model and awareness of current RDF 1.2 evolution.

Reference:
https://www.w3.org/RDF/

## C2PA Content Credentials
Technical standard for content provenance and authenticity.

Reference:
https://spec.c2pa.org/specifications/

---

# Public AI architecture material reviewed

## AWS Well-Architected Generative AI / Agentic AI guidance
Useful supporting alignment:
- scoping starts with understanding the business problem,
- controlled autonomy,
- observability,
- bounded agents,
- explicit contracts,
- human oversight,
- context and RAG considerations.

References:
https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lifecycle.html
https://docs.aws.amazon.com/wellarchitected/latest/agentic-ai-lens/design-principles.html

## Microsoft Azure Architecture Center
Useful supporting alignment:
- choose the lowest complexity that meets the requirement,
- direct model -> single agent -> multi-agent progression,
- explicit orchestration patterns,
- context/state, reliability, security, and cost as first-class concerns.

Reference:
https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns

## Anthropic — Building Effective Agents
Useful supporting alignment:
- distinguish workflows from agents,
- start with the simplest solution,
- add agentic complexity only when justified,
- treat retrieval, tools, and memory as augmentations around the model,
- preserve ground truth from the environment during execution.

Reference:
https://www.anthropic.com/engineering/building-effective-agents

## OpenAI — A Practical Guide to Building Agents
Useful supporting alignment:
- agents execute workflows,
- model/tools/instructions are core building blocks,
- tools retrieve context and take actions,
- guardrails and human intervention remain necessary,
- start simple and evolve only as required.

Reference:
https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/

## NIST AI RMF Generative AI Profile
Useful as a governance and risk reference for trustworthy AI design, development, use, and evaluation.

Reference:
https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence

---

# Public process-discovery and process-mapping tooling reviewed

## Microsoft Power Automate Process Mining
Uses event logs from systems of record to discover and analyze actual process paths. The documented event model includes case ID, activity, and timestamp.

References:
https://learn.microsoft.com/en-us/power-automate/process-advisor-overview
https://learn.microsoft.com/en-us/power-automate/process-mining-processes-and-data

## SAP Signavio Process Intelligence
Uses event data from SAP and non-SAP systems to reconstruct how processes actually run.

Reference:
https://www.signavio.com/products/process-intelligence/

## Celonis
Uses event logs to generate process maps and expose paths, variants, bottlenecks, and deviations.

Reference:
https://www.celonis.com/blog/how-process-mining-modernizes-process-discovery

## Miro AI
Can generate diagrams from text and use visible board content as AI context. Sticky Capture can convert an image of physical sticky notes into editable board stickies.

References:
https://help.miro.com/hc/en-us/articles/20164358139794-Create-with-AI
https://help.miro.com/hc/en-us/articles/28781881506834-Miro-AI-with-Sticky-notes

## Lucid AI
Can generate diagrams from text or image input. Process Capture can turn a screen recording into a diagram and written SOP.

References:
https://help.lucid.co/hc/en-us/articles/30324063850516-Boost-productivity-with-Lucid-AI
https://help.lucid.co/hc/en-us/articles/49874443096980-Use-Process-Capture-to-turn-screen-recordings-into-diagrams-with-Lucid-AI

---

# What is different about this methodology

Most public architecture guidance becomes technical relatively quickly:
- model selection,
- orchestration,
- RAG,
- agent patterns,
- security,
- cloud implementation.

Those are important, but this playbook should force one more layer of discipline in front of them.

The executive shorthand remains:

**Business problem -> Outcome -> Process -> Decisions -> Evidence -> Controls -> Architecture -> Technology**

The practitioner methodology underneath it is:

**Frame -> Observe -> Decompose -> Govern -> Redesign -> Architect -> Specify -> Select -> Prove -> Learn**

Several ideas in the current canon make this especially useful for enterprise architecture:

1. **Current-state process models should be evidence-backed.**
2. **Evidence, authority, and control are separate architectural questions.**
3. **Automation boundaries are explicit state transitions.**
4. **Architecture defines capabilities before technology is selected.**
5. **Governed delegation separates reasoning authority from execution authority.**
6. **Evaluation and operational learning close the loop.**

Combined with process-first architecture, these give us a methodology that can remain tool-neutral while still telling an architect exactly why a specific capability belongs in the design.

---

# Items to stress-test before promoting the curriculum itself into canon

The methodology questions resolved in Canon 02 v0.3 are no longer open curriculum questions:
- the eight-step sequence is executive shorthand, not the practitioner workflow,
- evidence, authority, and control are distinct,
- evaluation is an explicit **Prove** pass,
- future-state redesign is distinct from current-state observation,
- capability specification precedes technology selection.

The remaining curriculum questions are:

1. How formal should process notation be for the baseline course?
2. Should BPMN/DMN be required vocabulary or optional formalization?
3. Should the Process Discovery Evidence Ladder rank event logs above human context in every domain?
4. How do we represent processes with weak digital exhaust where the human narrative is the best evidence available?
5. How should we distinguish "process state" from "agent memory" in the teaching model?
6. What traceability mechanism best connects technology choices back through capability, architecture, process, and business outcome?
7. Should Tool Placement become a formal architecture decision record template?
8. What minimum **Prove** artifacts are required before a design is considered production-ready?
9. What minimum operational evidence is required before the **Learn** pass is allowed to change process, policy, or knowledge?

10. Which agent-interoperability protocols should be required knowledge versus awareness-only as the ecosystem evolves?
11. Where should the baseline course draw the line between data-architecture literacy and database implementation detail?
12. Do we need a formal decision tree that maps data requirements to structures/stores, or is the AI Data Design Matrix sufficient?
13. How should we teach profile / entity views without implying that every enterprise needs a CDP or a physically centralized profile store?
14. Which provenance model should be the default teaching example across data, documents, and generated content?

These should be challenged before the curriculum itself is labeled canon.
