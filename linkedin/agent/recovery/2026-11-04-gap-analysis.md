# Overlimit conversation — preservation gap analysis
**Date:** 2026-11-04  
**Status:** Audit findings and recommended actions, **not canon**.

## Verified preservation
1. [Private archived transcript](https://github.com/rgrack-sys/linkedin-publishing-agent/blob/3e522b0c1e14672cd3c6026df019e7e0565e0f0f/docs/overlimit%20conversation.md) exists on agent `main` at commit `3e522b0c1e14672cd3c6026df019e7e0565e0f0f` (552 lines).
2. Pre-lock convergence control is implemented in agent `services/convergence.py` and `services/orchestrator.py` and documented in Playbook milestone 7 (agent PR #9).
3. Review Capture Ledger is implemented in `services/review_capture.py`, CLI and tests, documented in Playbook milestone 8 (agent PR #10); validation reports 59 passing tests and six CI jobs on each cited branch/merged-main run.
4. BL-001 is preserved in Playbook `linkedin/backlog/content-backlog.md` with v004 finding, reviewed draft hash and evidence snapshot; it is explicitly not canon.
5. The recorded v004 Critic outcome is series PASS, no BLOCKER/MAJOR and one MINOR, tied to draft SHA-256 `83bdd47ccd157d5a33250b6ade5f18843230e7097452118580b02445802e8952`.

## Gaps and actions

| ID | Severity | Gap / precise limitation | Action to close | Closure evidence |
| --- | --- | --- | --- | --- |
| GAP-01 | HIGH | Archived transcript starts midstream and has no reliable speaker/timestamp labels; complete earlier conversation cannot be certified from this archive alone. | Export/recover any missing earlier segments if available; otherwise label the archive **partial** permanently and reconcile earlier requirements against repository history and existing artifacts. | Source coverage manifest with beginning/end markers and verified provenance. |
| GAP-02 | HIGH | Exact local `draft-v004.md`, `critique-v004.json`, `author-decisions-v002/v003/v004.md` and related review evidence are in Git-ignored `workspace/live-smoke-001`; their current bytes have not been independently checked. | On Hugo-1 inventory the workspace, hash v004, check versioned critiques and author decisions; curate a sanitized immutable record outside `workspace/*` for Git. | SHA-256 match, file manifest, committed artifacts/summary, no secrets. |
| GAP-03 | HIGH | `TEXT_LOCKED` is **not proved**. Assistant text recommends `TEXT LOCK: APPROVED` and supplies commands, but no state transition, approval record, or `text-locked.md` execution proof is present in Git. | Inspect `state.json`, `events.jsonl`, `author-decisions-v004.md`, `text-locked.md`; if incomplete, request explicit author disposition/approval and execute through governed workflow. Never infer approval from the Critic PASS alone. | Persisted human decision + valid `TEXT_LOCKED` transition + locked-text hash. |
| GAP-04 | HIGH | Review Capture Ledger is local operational state; `workspace/*` is Git-ignored and Playbook writeback is not connected. | Establish deterministic writeback or a required manual Git reconciliation of approved captures with duplicate detection and provenance. | Durable canonical backlog entry with source links and commit, verified against local ledger. |
| GAP-05 | RESOLVED FOR CLI EXECUTION; FILE INSPECTION PENDING | Operator-provided CLI output confirms `CAP-001` and `CAP-002` were saved, and `captures live-smoke-001` lists both as `OPEN`, sourced to `critique-v004.json / F1`. Exact local `captures.jsonl` / capture JSON contents, bytes, and timestamps remain uninspected. | Keep both IDs linked to the existing `BL-001` (now reconciled in Git); inspect local capture artifacts and hash/backup them under GAP-02/GAP-04. | Operator's save and list command outputs, plus this Git record; local file inspection still required. |
| GAP-06 | MEDIUM | Real visual generation, visual QA, publishing, and automatic archive/writeback adapters are still disconnected; post completion/publication is not proved. | Treat current post as reviewed text only until actual author gates, visual QA, receipts and archive are completed. | Verified final package, author approvals, publication receipt and Git archive. |
| GAP-07 | MEDIUM | Five related image/deck assets remain Library-only per `ARTIFACT-INVENTORY.md`; chat/Library are not synchronized with Git. | Confirm intentional storage policy; publish appropriate binaries through a reviewed Git LFS or equivalent storage workflow. | Versioned asset manifest and durable URL/hash. |
| GAP-08 | LOW | V1 build spec still references `project-bootstrap` v0.2, while the agent's validation report says project metadata targets v0.3.0. | Reconcile specification's historical baseline vs current implementation metadata; do not rewrite historical statements without annotation. | Updated/current spec or clearly documented version history. |
| GAP-09 | MEDIUM | No standard end-of-chat decision-coverage checklist/session handoff is yet enforced by `GIT-WORKFLOW.md`; a committed transcript alone cannot prove all decisions were captured. | Propose (do not silently canonize) an end-of-session decision register, artifact manifest, unresolved questions, and verified Git checkpoint. | Approved workflow change with acceptance test or review checklist. |

## Risk and scope rules
- Keep raw conversation only in the private agent repo, not the public Playbook.
- Preserve finding identity as `post_id + critique_version + finding_id`: `F1` is reused across critique versions.
- Treat a copy-paste shell command as *proposed action* until execution evidence exists.
- Do not promote deferred authorization dimensions to canon.
- Do not lock or publish the post based on audit conclusions alone.

## Related records
- [Decision register](2026-11-04-decision-register.md)
- [Session handoff](2026-11-04-session-handoff.md)
- Playbook `linkedin/backlog/content-backlog.md` (BL-001).

## Audit update: CAP-001 / CAP-002 command results (2026-11-04)

The operator subsequently ran both capture commands successfully:
- `Saved CAP-001 (FOLLOW_ON_POST): What makes an authority boundary sufficiently explicit?`
- `Saved CAP-002 (CRITIC_OBSERVATION): Action class alone may not sufficiently define authority`
- `captures live-smoke-001` displayed both entries with `[OPEN]`.

**GAP-05 execution uncertainty is resolved** based on these terminal outputs. Durable GitHub reconciliation is recorded under BL-001; no extra backlog item is warranted. GAP-02 (local artifact preservation), GAP-04 (automated writeback), and GAP-03 (human disposition and actual text lock) remain open. This report does not assert direct filesystem inspection.

## Follow-up: v004 file hash verified; missing orchestrator state (2026-11-04)

**Verified by operator:** `draft-v004.md` SHA-256 is `83bdd47ccd157d5a33250b6ade5f18843230e7097452118580b02445802e8952`, matching the final Critic artifact. This closes the **draft-v004 hash-matching sub-check of GAP-02**, but other artifacts remain uninspected and unarchived.

**Observed:** `linkedin-publishing-agent status live-smoke-001` raises `FileNotFoundError` for `workspace/live-smoke-001/state.json`.

**Code-level diagnosis:** Standalone CLI `draft` writes evidence/research/draft artifacts without `state.json`; standalone `critic` and `capture` do not advance orchestrator state. Only the orchestrator's `start_post` creates `PostState` and the state/event log; `status` unconditionally tries to load it. The absence of a state file is therefore consistent with an **artifact-only workflow**, not a failed prior state transition or missing draft. Do not recreate state or infer author approvals. Follow-up tracked in private agent issue [#12](https://github.com/rgrack-sys/linkedin-publishing-agent/issues/12).

**GAP-03 stays OPEN:** There is no persisted `TEXT_LOCKED` transition on this CLI path, and the `author-decisions-v004.md` plus `text-locked.md` file presence remains to be checked separately. A valid Critic hash + series PASS + no high-severity finding establishes eligibility only, not approval or a lock.
