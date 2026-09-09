# AI Architecture Playbook

**Canonical starter captured from the August 25, 2026 architecture conversation.**

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

## Canonical papers

1. `canon/01-ai-foundations.md`
   - Training vs. inference
   - Weights vs. embeddings
   - Contextual representation
   - Vector databases and retrieval
   - Model knowledge vs. external evidence

2. `canon/02-ai-ready-enterprise-architecture.md`
   - Data quality defines reasoning quality
   - Process-first AI architecture
   - Evidence-First Gate
   - AI-ready information architecture
   - Governed knowledge architecture
   - Systems of record, knowledge layer, and agent context
   - Continuous knowledge synchronization
   - Data in motion and volatility
   - CDPs in the architecture

3. `canon/03-agentic-architecture-governed-delegation.md`
   - Chat vs. agent execution context
   - Model vs. agent distinction
   - Runtime vs. harness
   - Agent assembly formula
   - Deterministic code in agentic systems
   - Instruction design as executable architecture
   - Governed Data / Evidence Boundary
   - Harness-to-harness delegation
   - Delegation Contract
   - Domain-owned execution
   - Model Gateway / Model Policy abstraction
   - Closed-loop outcome feedback
   - Emerging Reference Architecture — Draft 0.1

## Working architectural theses

> Traditional systems organize data for transactions, reporting, and retrieval. AI-ready architecture must additionally organize governed knowledge and current evidence for reasoning.

> Always tie your architecture to a real business problem.

> The most important engineering in the AI world is process engineering. Yet most organizations are set up to build a process around a set of technology decisions.

> AI architecture is not traditional architecture plus a model. It is an architecture for governed reasoning, evidence, delegation, and controlled action.
