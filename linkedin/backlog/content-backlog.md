# LinkedIn Content / Critic Backlog

**Purpose:** Preserve useful follow-on post ideas, Critic observations, research questions, and architecture backlog items that should survive beyond the current post.

This is a backlog, **not canon**. Items become canon only through the normal vetting process.

## Status values

- **OPEN** — retained for future work.
- **IN_RESEARCH** — actively being researched or stress-tested.
- **PROMOTED_TO_POST** — converted into a LinkedIn post work item.
- **PROMOTED_TO_CANON_CANDIDATE** — moved into formal canon-candidate vetting.
- **DISMISSED** — intentionally closed with rationale.

---

## BL-001 — What makes an authority boundary sufficiently explicit?

**Type:** FOLLOW_ON_POST / CRITIC_OBSERVATION  
**Status:** OPEN  
**Origin post:** `live-smoke-001` — authority boundaries  
**Origin critique:** `critique-v004.json` / finding `F1`  
**Reviewed draft SHA-256:** `83bdd47ccd157d5a33250b6ade5f18843230e7097452118580b02445802e8952`  
**Playbook snapshot used by Critic:** `c90374055ec967ab50b3d58f55d36a4dba427b98`

### Critic observation

The current post establishes that **the task being delegated and the authority being delegated are separate design decisions**.

The Critic then identified a deeper design question: naming the permitted action category and the source of authority may still leave the authority boundary underspecified.

An agent may be authorized to **execute** a payment, for example, while important boundary dimensions remain unresolved:

- scope;
- limits or thresholds;
- permitted resources;
- prerequisites;
- approval conditions;
- duration;
- revocation;
- exceptions.

This observation was intentionally **deferred from the current post** so the post could remain focused on the task-versus-authority distinction.

### Follow-on post / research question

> **What dimensions are required to define an authority boundary sufficiently for an enterprise AI agent?**

Potential framing:

- Action: what class of action may the agent take?
- Scope: on what objects/processes/accounts?
- Limits: what quantitative or qualitative boundaries apply?
- Conditions / prerequisites: what must be true before the action is permitted?
- Approval: which actions require escalation or human approval?
- Resources: which tools/data/systems may the agent use?
- Duration: how long does the authority remain valid?
- Revocation: how is authority withdrawn or suspended?
- Exceptions: what cases force re-entry or escalation?

### Vetting requirement

Do **not** assume this list is complete or canonical.

Before using it in a post or canon:

1. compare it with established authorization / access-control models;
2. compare it with agent-specific authority/delegation work;
3. distinguish authority definition from enforcement implementation;
4. test whether the dimensions are mutually distinct and operationally useful;
5. determine which controls can be deterministic versus governed judgment.


## Local Review Capture Ledger reconciliation — 2026-11-04

The operator supplied Hugo-1 CLI output proving the local workflow successfully executed two source-linked captures and listed both as **OPEN**:

| Capture ID | Kind | Exact local title | Tags | Shared source |
| --- | --- | --- | --- | --- |
| `CAP-001` | `FOLLOW_ON_POST` | What makes an authority boundary sufficiently explicit? | `authority`, `follow-on` | `live-smoke-001 / critique-v004.json / F1` |
| `CAP-002` | `CRITIC_OBSERVATION` | Action class alone may not sufficiently define authority | `authority`, `critic` | `live-smoke-001 / critique-v004.json / F1` |

**Reconciliation:** Both represent two classifications of **BL-001**, not two different architectural questions. Keep this single backlog item OPEN. The capture service wrote the local artifacts according to its executed command responses, but the underlying Git-ignored JSON/JSONL bytes and timestamps have not been independently audited. This GitHub note is the durable shared index; the local full capture objects remain on Hugo-1 until archived/synchronized.

**Authority:** These captures do not approve the Critic v004/F1 disposition, promote a canon candidate, perform `TEXT_LOCKED`, or authorize publication.
