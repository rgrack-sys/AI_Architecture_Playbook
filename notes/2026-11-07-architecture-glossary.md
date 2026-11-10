# Architecture glossary — November 7, 2026 additions

**Classification:** Supporting definitions, integrated with existing canon; not a replacement glossary.

- **Outcome:** The business result sought, expressed with independently checkable acceptance criteria; not synonymous with successful tool execution.
- **Process readiness:** The degree to which work, decisions, tacit practice, context, evidence, authority, exceptions and verification are defined well enough to automate responsibly.
- **Mechanism selection:** Choosing deterministic code, API integration, bounded model use or agentic execution from process requirements rather than from available technology.
- **Harness (current project):** The governing envelope around agent execution: instructions, evidence rules, policy, tools, budgets, checkpoints, validation, human gates and recovery. Not merely a test harness (older common meaning).
- **Runtime:** The execution environment and lifecycle machinery for workflows and agent tasks; distinct from the governing harness.
- **MCP server:** A server implementing Model Context Protocol to expose tools, resources and/or prompts to a compatible client. The protocol describes interaction; it does not itself establish business authorization.
- **Skill:** Versioned reusable task guidance or procedures consumed by an agent/harness; exact packaging varies by platform. A skill is not a policy enforcement boundary.
- **Information authority:** A source's legitimacy and suitability to support a factual claim or decision, including provenance, currency and permitted use.
- **Integration authority:** Permission to invoke a system capability or produce a business effect; distinct from source credibility or technical connectivity.
- **Idempotency:** A property or design strategy that prevents duplicate business effects when a request is repeated; especially important after uncertain outcomes.
- **Unknown outcome:** A state where a request may have committed but the caller lacks confirmation. Requires reconciliation before retry.
- **Compensation:** A governed follow-up action to mitigate a completed effect; not necessarily a true rollback.
- **Control plane / execution plane:** Logical distinction between defining/enforcing policy and carrying out tasks; implementation may distribute controls across services.

## November 10 reconciliation of November 7 terminology

**Classification:** Supporting explanatory definitions only. The applicable governing principles are in Canon 02 and Canon 03; a glossary entry does not independently authorize a tool, approve an implementation, or promote a proposal to canon. **Provenance:** November 7 architecture discussion, targeted reconstruction November 10.

- **Model (current project):** An inference capability used for prediction, classification, generation, or reasoning when justified by a task. It is not synonymous with the agent, runtime, or harness. *Older/alternate use:* A mathematical, statistical, or domain model need not be an LLM.
- **Agent (current project):** The assembled, governed executable workflow that can adaptively determine authorized next steps toward a delegated goal using models, tools, code, state, and controls as needed. It does not inherit unlimited discretion from a model or its tools. *Alternate use:* A background software daemon, monitoring agent, or human representative can be called an agent without using generative AI.
- **API:** An application programming interface: a defined contract for invoking operations or exchanging information with a system. An API's technical availability does not establish the caller's organizational permission to use it. *Older use remains valid:* APIs also include local libraries and in-process interfaces, not only HTTP/web services.
- **Classifier:** A function that assigns an input to one or more defined categories, often with scores and explicit rejection/review cases. It can be implemented through deterministic rules, classical machine learning, or a model service; a classifier is not inherently an autonomous agent or a generative LLM. *Older use:* Rule-based category or pattern recognizer.
- **Deterministic software/workflow:** Defined operations and transitions executed according to explicit rules, including validation, scheduling, state handling, and direct API use. Its behavior can still depend on external data and failures; deterministic does not mean infallible. It remains a first-class alternative to model-backed decisions.
- **Flat file:** File-based data representation such as CSV, JSON, or Markdown, useful for bounded or versioned data without demanding a database service. It is not automatically suitable for high-concurrency transactional state.
- **Relational database:** Data organized into tables with defined relationships, constraints, and query/transaction semantics. Appropriate when identity, integrity, joins, or atomic changes matter; not synonymous with all structured data.
- **Graph database/representation:** A structure optimized for entities, edges, and relationship-focused queries. It can improve traversal use cases, but graph concepts can also be implemented in relational or other stores.
- **Big-data/analytical platform:** Storage and processing designed for volume, distributed workloads, or analytical query patterns that justify added operational complexity. Large scale is a requirement to prove, not a default design choice.
- **Invocation/interaction pattern:** The way work is initiated and fulfilled: synchronous response, batch processing, cached reuse, event-driven trigger, asynchronous durable workflow, or polling. Selection depends on outcome latency, freshness, consistency, policy, and economics; none is universally superior.

**Cross-references:** Existing definitions above for Harness, Runtime, MCP server, Skill, Information authority, and Integration authority remain unchanged. The terms API, MCP, model, agent, classifier, and skill name different roles; their names alone do not determine authority.

**Separate proposals, not promoted here:** `lexical match` and `semantic sufficiency` remain proposed glossary definitions under LinkedIn Publishing Agent Issue #29 (commit `3d271bb9`). Their existence in that project's glossary does not make them approved Playbook canon.
