# AI Architecture Design Methodology — Curriculum and Syllabus

**Status:** Draft v0.2 — curriculum working draft, aligned to Canon 02 v0.3; curriculum itself is not canon  
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
2. Define a business problem and measurable outcome before discussing technology.
3. Establish an evidence-backed current-state process model from interviews, transcripts, whiteboards, documents, screen recordings, and system event data.
4. Decompose the work into activities, decisions, actions, waits, state changes, boundaries, exceptions, handoffs, and outcomes, and identify where reasoning actually matters.
5. Identify automation boundaries and engineer the handoff and re-entry state explicitly.
6. Distinguish evidence, authority, and control for consequential decisions and actions.
7. Determine when model knowledge is sufficient and when authoritative external evidence is required.
8. Redesign the future-state operating process before deriving the AI architecture.
9. Design the information architecture needed to provide current, governed evidence for reasoning.
10. Separate model, agent, runtime, harness, tools, state, trigger, and deterministic software responsibilities.
11. Define evaluation, observability, provenance, and closed-loop outcome feedback before production.
12. Translate architecture into capability requirements and only then evaluate specific products.
13. Defend the design to a CIO, CDO, security leader, business owner, regulator, engineering team, and skeptical architect.

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

### What I teach

- Training vs. inference.
- Tokens and context.
- Model weights are learned machinery, not a hidden database.
- Embeddings are numerical representations, not "the model's memory."
- Vector databases store and retrieve external content by similarity.
- Context changes representation and therefore reasoning.
- Model knowledge is different from external evidence.
- Retrieval is an evidence-acquisition technique, not a universal requirement.
- Deterministic software still belongs in AI systems.

### Why the architect needs it

A customer will ask:

- Why do I need RAG if the model already knows things?
- Why can the model answer this question but not be trusted to answer another one?
- Why do I need a vector database?
- Why can't I just put all of the documents in the prompt?
- Why do I need an API or deterministic service when the model can calculate it?
- What exactly is an agent?

The architect should be able to answer without hiding behind product vocabulary.

### Existing course material

Use Canon 01 as the baseline:
- training vs. inference,
- weights vs. embeddings,
- contextual representation,
- vector retrieval,
- activation vs. retrieval,
- external evidence,
- the limits of "RAG everywhere."

### Exercise

Explain the difference between:
1. model knowledge,
2. retrieved evidence,
3. enterprise system-of-record data,
4. current task context,

to a nontechnical executive in five minutes.

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
1. an as-is process map,
2. a list of contradictions between sources,
3. a decision inventory,
4. an automation-boundary inventory,
5. a future-state candidate map.

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

## Module 7 — Automation Boundaries and Real-World State

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

## Module 8 — From Model to Agentic System

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

## Module 9 — Evidence, Authority, Controls, Risk, and the Harness

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

## Module 10 — Delegation, Domains, and Execution Authority

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

## Module 11 — Evaluation, Observability, and Closed-Loop Learning

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

## Module 12 — Technology Selection: Plugging Tools into the Architecture

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
- domain execution.

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

## Module 13 — Capstone: Redesign a Real Enterprise Process

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
12. Agent/runtime/harness decomposition where needed.
13. Delegation contracts where needed.
14. Evaluation and observability plan.
15. Technology capability requirements.
16. Tool mapping and selection rationale.
17. Executive explanation of why the design exists.

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
- stakeholders,
- baseline,
- desired outcome,
- measures,
- constraints.

## 2. Process Discovery Worksheet
- scope,
- trigger,
- completion,
- actors,
- systems,
- activities,
- decisions,
- evidence,
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
- decision,
- evidence,
- authoritative source,
- freshness,
- volatility,
- provenance,
- permissions,
- fallback.

## 6. Automation Boundary Contract
- trigger,
- actor,
- required action,
- context,
- proof of completion,
- latency / escalation,
- re-entry condition.

## 7. Governance Matrix
- consequential decision or action,
- required evidence,
- authorized actor or system,
- risk,
- control,
- enforcement point,
- owner,
- audit evidence,
- failure behavior.

## 8. Delegation Contract
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

## 9. Tool Placement Card
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

## 10. Evaluation Plan
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

These should be challenged before the curriculum itself is labeled canon.
