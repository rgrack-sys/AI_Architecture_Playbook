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
