# Data access is not model training

**Date:** November 23, 2026  
**Classification:** Accepted technical principle and supporting explanation, with retained teaching hooks.  
**Acceptance:** Richard accepted the source-vetted candidate on November 23, 2026 and directed that its catchphrases remain part of the teaching material.  
**Repository baseline examined:** main at 0f46a0fb61dbcaf6e5b93df3005c5daebff33270.  
**Scope:** Ordinary inference with fixed trained parameters; distinguish the underlying LLM from the application, tools, retrieval stores, and persistent state around it.

## Richard's clarified argument

> My core argument is : Just because you have an LLM that can access your data either directly or through skill or MCP or whatever, the LLM is not being trained by your data when you query that data, nor does the fact that the LLM gets an answer from your data make your data part of the LLMs overall set of knowledge

## Assessment

The core argument is technically sound for ordinary LLM inference. A query can supply new information for an answer without updating the model's learned parameters. Answering a question correctly using retrieved information is evidence that the information was usable in that interaction; it is not, by itself, evidence that the model was trained on it. Brown et al. demonstrate useful adaptation to textual instructions and examples without gradient updates or fine-tuning [S1].

In the technical explanation, **the model's learned, or parametric, knowledge** gives precision to the informal phrase **the LLM's overall set of knowledge**. This does not require replacing the memorable catchphrases with technical definitions. An AI application's accessible knowledge resources can expand through documents, retrieval indexes, saved conversation state, and external memory while its underlying language model's trained parameters remain unchanged. Lewis et al. explicitly distinguish parametric memory from external, non-parametric memory [S2].

The earlier assistant response broadened the discussion into reasoning reliability, truth, accountability, and systems of record. Those are related architectural subjects, but they are not needed to establish or challenge Richard's clarified claim. This note centers the causal distinction: receiving data does not itself establish a model-training operation.

## Retained teaching hooks and accepted explanation

### Teaching hook

> **The data doesn't know.**  
> **The data does not train the LLM.**  
> **And getting an answer does not mean the LLM now has the data.**

### Let me explain why I say that

Data can represent facts, relationships, and rules. The first hook distinguishes that recorded information from the system that processes it. The model uses information supplied to it, together with what it learned during training, to generate an interpretation or answer.

> **Giving an LLM access to your data does not, by itself, train the model on that data. During ordinary inference, retrieved information supplies context for generating an answer; it does not update the model's learned parameters. The application may retain or retrieve that information again, but those capabilities are separate from training the underlying model.**

When we say that the LLM does not "now have the data," the point is that receiving an answer has not, by itself, incorporated the information into learned parameters. It can still be present in context or retained by the surrounding application. The hook introduces that distinction; this explanation specifies its meaning.

Precise short summary, retained alongside the hooks:

> **Querying your data can inform the answer without training the model.**

Richard explicitly accepted the technical candidate and added the teaching direction to preserve catchphrases that attract attention and invite a deeper explanation. The catchphrase need not be a complete standalone technical definition or literally accurate in every possible context. Vet the phrase and its explanation as one teaching unit, preserving the intended idea and a technically defensible explanation. This direction is recorded in the [Playbook teaching convention](https://github.com/rgrack-sys/AI_Architecture_Playbook/blob/main/ai-architecture-playbook-canon/README.md#teaching-convention-catchphrase-then-explanation) and applied in [Canon 01](https://github.com/rgrack-sys/AI_Architecture_Playbook/blob/main/ai-architecture-playbook-canon/canon/01-ai-foundations.md#7-data-access-is-not-model-training--november-23-2026).

## What changes when a query is answered?

| Mechanism | What changes | Does that operation itself train the LLM? |
| --- | --- | --- |
| Retrieve a database result or document excerpt | Information becomes available to the application and, if included, the model's current context | No |
| Process information in context | Intermediate representations and the resulting answer depend on the supplied information | No parameter update in ordinary inference |
| Save history, a result, or an external memory record | Persistent application state changes | No; the information can be supplied again later |
| Add material to a retrieval index | The application's retrievable content changes | No; index construction is separate from training the language model |
| Run an explicit training or adaptation operation | Model parameters, adapters, or another trainable component may change | Only if the LLM or its adapters are trained. Training another component, such as a retriever, does not itself train the LLM. |

The first four rows describe mechanisms that can operate with a fixed language model. The last row describes a distinct operation. The original RAG research itself trained model components, so [S2] must not be misrepresented as saying that every RAG architecture is never trained. Its relevant contribution here is the distinction between parameter learning and retrieval-based memory.

An API, an MCP server, or a skill can help route the work. None of those labels establishes that training occurred. MCP defines tool discovery, invocation, and returned content; the semantics of the invoked operation determine what it does [S3]. A tool that explicitly launches training would be a different operation from a tool that only queries records.

## Concrete teaching example

**Hypothetical example; these are invented records, not actual business data.** A newly created order record says order Q-7284 has status READY_FOR_PICKUP. A tool retrieves that status, and the model answers that the order is ready for pickup according to the retrieved record.

The model can use that status in a follow-up while it remains in context. The application can also save the result and supply it to a later invocation. Neither event establishes a weight update.

Now consider a fresh invocation of the same fixed model with no retrieved record, conversation history, saved summary, external memory, or other source containing the order status. The earlier query gives that invocation no dependable route to the newly created fact. An answer might be guessed or independently obtained, but the prior successful response is not proof of learned retention. This is a thought experiment derived from the stated architecture, not a reported empirical test.

The useful distinction is between **being able to answer with supplied information** and **having incorporated that information into learned parameters**.

## Stress test and boundaries

### In-context learning

An expert may object that models learn from examples in a prompt. The terminology is legitimate: in-context learning describes adaptation using the context. Brown et al. explicitly distinguish those demonstrations from gradient updates and fine-tuning [S1]. Avoid the blanket statement that an LLM cannot learn anything from a prompt. The precise claim concerns updates to trained parameters.

### Persistent application memory

An assistant may answer a question again in a later session because the application supplied saved information. That demonstrates persistence and renewed access. It does not alone establish that the underlying model was retrained. The system boundary matters: the application and its knowledge resources are larger than the language model [S2].

### Training at query time

An unconditional claim that no query workflow can ever involve training would be false. Hardt and Sun describe a system that retrieves neighboring documents and explicitly fine-tunes a language model on them at test time [S4]. This is why the formulation includes **does not, by itself** and **during ordinary inference**. A designed training/adaptation step must be identified and evaluated separately; it is not an inherent consequence of receiving a query result.

### Retention and later use

The absence of a weight update does not establish deletion, confidentiality, or exclusion from a later training pipeline. This is a logical scope limit of the claim, not a statement about any provider's current policies. Verify retention and data use separately when evaluating a real service.

### Limits of training as storage

Even when a training operation occurs, it does not follow that every source fact has been faithfully or reliably retained. The appropriate claim is that parameters were updated using a training process, not that a complete source database now exists inside the model. This is consistent with Canon 01's distinction between distributed learned representations and database records [R1].

## Architectural implications

These are design conclusions drawn from the distinctions above:

1. Describe separately what the model was trained on, what the application can retrieve, and what the application retains.
2. Evaluate answers that depend on enterprise records together with the retrieval, context, source version, and application state that supplied those records.
3. Do not treat a correct retrieved answer as proof of durable model learning.
4. Identify the mechanism that makes information available on the next invocation: renewed retrieval, supplied history, an external memory store, or an explicit adaptation process.
5. For changing business facts, preserve authoritative source access and freshness requirements; a successful prior response does not make the model a current source of record.

Retrieval and training can both be useful. Retrieval allows externally maintained information to inform answers; it also creates dependencies on access, relevance, availability, and freshness. Training changes learned behavior through an additional process. The correct choice follows from the task requirements, rather than from an assumption that using the application automatically teaches its model.

## Relationship to existing Playbook material

Canon 01 already separates training from inference, model weights from databases, and external retrieval from learned knowledge. The present argument sharpens those existing foundations into a concise teaching statement. The November 7 glossary also distinguishes model, agent, MCP, and skill roles [R1, R2]. The initial archive at e5531ffe36aabb32866eaa40dc6126374f3d6470 preserved a candidate without changing canon. Following Richard's explicit acceptance, the hooks and accepted explanation are incorporated in Canon 01, section 7, and the teaching convention is recorded in the Playbook README.

The repository's canon review rule calls for counterarguments and revision conditions [R3]. The main revision trigger is a specific implementation that performs training, updates adapters or other trainable state, or uses a different boundary for what it calls the model. Such a system requires its actual learning and persistence mechanisms to be documented. It does not invalidate the narrower claim that mere access and retrieval do not establish training.

## Vetting record

- Root review: primary sources S1-S4 opened and examined; relevant repository material R1-R3 and GIT-WORKFLOW.md read at the stated baseline.
- Separate technical Critic: independently supported the argument under fixed-weight inference and identified the in-context learning, system-boundary, explicit adaptation, and retention qualifications incorporated here.
- Evidence type: source review and architectural reasoning. No experiment was run on a particular proprietary model, and no claim is made about a provider's actual training or retention configuration.
- Approval state: Richard explicitly stated, "The candidate is acceptable and correct," and directed preservation of catchphrases with a deeper explanation. The technical candidate is accepted; the teaching convention implements that author direction. Acceptance of this principle does not certify a future deck, post, or publication as having completed its own review.
- Editorial review after acceptance: a separate Critic supported preserving the hooks with the accepted explanation, identified the relevant possible misreadings, and advised against requiring every hook to serve as a complete technical definition. The accepted technical explanation remains intact.
- Conversation provenance: [Session record](2026-11-23-data-access-is-not-training-session.md).

## Sources

**S1.** Brown et al. (2020), [Language Models are Few-Shot Learners](https://arxiv.org/html/2005.14165v4). Abstract and introduction describe evaluation with textual instructions/examples and no gradient updates or fine-tuning. Supports context use and in-context learning without parameter updates.

**S2.** Lewis et al. (2020; revised 2021), [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/html/2005.11401v4). Abstract, introduction, and index hot-swapping section distinguish learned parameters from external retrieval memory. The paper includes training; it is not evidence that all RAG systems exclude training.

**S3.** Model Context Protocol, [Tools specification, version 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25/server/tools). Defines external operations and returned content. Used for the role of the protocol, not as a warranty about every tool implementation or a claim that this is the latest protocol version.

**S4.** Hardt and Sun (ICLR 2024), [Test-Time Training on Nearest Neighbors for Large Language Models](https://proceedings.iclr.cc/paper_files/paper/2024/hash/f02f1185b97518ab5bd7ebde466992d3-Abstract-Conference.html). Provides an explicit example of retrieval followed by parameter adaptation at test time.

**R1.** [Canon 01 - AI Foundations at the examined commit](https://github.com/rgrack-sys/AI_Architecture_Playbook/blob/0f46a0fb61dbcaf6e5b93df3005c5daebff33270/ai-architecture-playbook-canon/canon/01-ai-foundations.md).

**R2.** [Architecture glossary at the examined commit](https://github.com/rgrack-sys/AI_Architecture_Playbook/blob/0f46a0fb61dbcaf6e5b93df3005c5daebff33270/notes/2026-11-07-architecture-glossary.md).

**R3.** [Playbook README and canon review rule at the examined commit](https://github.com/rgrack-sys/AI_Architecture_Playbook/blob/0f46a0fb61dbcaf6e5b93df3005c5daebff33270/ai-architecture-playbook-canon/README.md).

All sources examined November 23, 2026.
