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

## Teaching convention: catchphrase, then explanation

**Author direction accepted November 23, 2026.**

**Teach with a memorable hook, then explain it.** A catchphrase may simplify, compress, or use metaphor to introduce an architectural idea. It does not have to be literally accurate in every possible context or function as a complete standalone technical definition. Its purpose is to catch attention, give the audience something memorable, and invite a deeper explanation.

Preserve the force of the phrase and the author's intended wording. Follow it with the bridge:

> **Let me explain why I say that.**

The explanation supplies the precise meaning, evidence, example, and material boundaries needed to understand and apply the principle. Qualifications belong where they help explain the idea; do not require every qualification in the opening line.

**Vet the catchphrase and explanation together as a teaching unit.** Review whether the hook introduces the intended idea and whether the explanation develops it accurately. An incomplete or context-dependent hook is not automatically a conceptual defect. A substantive error in the explanation still requires correction. This preserves the existing canon review standard while applying it to the complete lesson.

Keep the catchphrase and its explanation associated in the canon, talk track, and accompanying material. A slide can carry the short phrase while speaker notes or the next part of the same teaching segment carry the explanation. When reusing an excerpt, preserve a route to that explanation rather than rewriting every hook as a technical paragraph.

The approved application appears in [Canon 01, section 7](canon/01-ai-foundations.md#7-data-access-is-not-model-training--november-23-2026).

## Canonical papers

1. `canon/01-ai-foundations.md`
   - Training vs. inference
   - Weights vs. embeddings
   - Contextual representation
   - Vector databases and retrieval
   - Model knowledge vs. external evidence
   - Data access is not model training: retained catchphrases and accepted explanation

2. `canon/02-ai-ready-enterprise-architecture.md`
   - Data quality defines reasoning quality
   - Data readiness and business context: governed semantics and verifiable evidence
   - Process-first AI architecture
   - Executive shorthand vs. practitioner methodology
   - Frame -> Observe -> Decompose -> Govern -> Redesign -> Architect -> Specify -> Select -> Prove -> Learn
   - Current-state process truth vs. future-state process design
   - Evidence vs. authority vs. control
   - Architecture capability requirements before technology selection
   - Effect-level reachability testing for authority controls
   - Acceptance-boundary testing for proof of completion
   - Detection vs. intervention and verified containment
   - Verifier independence and separate acceptance of business outcomes and governed process behavior
   - Integrated model-harness configuration testing
   - Evidence-First Gate
   - Evidence sufficiency and evidence requirements as architectural controls
   - Organization-defined evidence standards made executable through architecture
   - AI-ready information architecture
   - Requirements-driven data design: derive representation and technology from what the system needs the data to do
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
   - Model-invocation necessity gate and five-question architecture review checklist
   - Instruction design as executable architecture
   - Governed Data / Evidence Boundary
   - Harness-to-harness delegation
   - Delegation Contract
   - Domain-owned execution
   - Model Gateway / Model Policy abstraction
   - Portable agency and retained institutional knowledge (November 20, 2026)
   - Closed-loop outcome feedback
   - Emerging Reference Architecture — Draft 0.1

## Working architectural theses

> Traditional systems organize data for transactions, reporting, and retrieval. AI-ready architecture must additionally organize governed knowledge and current evidence for reasoning.

> Always tie your architecture to a real business problem.

> The most important engineering in the AI world is process engineering. Yet most organizations are set up to build a process around a set of technology decisions.

> AI architecture is derived through process engineering. The architect first understands and redesigns the work, decisions, evidence, authority, controls, state, and outcomes; the required AI architecture is then derived from those requirements.

> AI architecture is not traditional architecture plus a model. It is an architecture for governed reasoning, evidence, delegation, and controlled action.

> The fact that we can call an AI model doesn't mean we should.

> **An agent's intelligence may be rented. Its business logic, operating state, and institutional knowledge must remain portable.** (See Canon 03, November 20, 2026: vendor-exit / relocation drill.)
