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

## Recovery implementation milestone (2026-11-04)

[Agent PR #13](https://github.com/rgrack-sys/linkedin-publishing-agent/pull/13) was merged into `main` at `a7e6a1cfa2f7f2cbeec47974cf7dfa86cb054740`. The six GitHub Actions PR jobs passed: Ubuntu/Windows with Python 3.10, 3.12, 3.14.

The new `lock-reviewed` command allows **read-only preflight** (`--check`) and a separately **explicitly authorized** (`--approve-text-lock`) adoption+TEXT_LOCKED transition. It validates the exact latest reviewed draft hash, the latest Critic's hash, series PASS, no BLOCKER/MAJOR, and complete written dispositions for MINOR/NOTE findings. It records `review-adoption-vNNN.json`, `author-text-lock-vNNN.json`, `text-locked.md`, `events.jsonl`, and `state.json` without inventing prior state transitions.

**Important:** This was code/CI verification only. No live lock was performed on Hugo-1; the operator still needs to run read-only preflight, decide the F1 disposition, and explicitly approve the lock. GAP-03 remains **OPEN** until that evidence exists. GAP-02 (local artifact archival) and GAP-04 (automatic writeback) remain **OPEN**. Issue #12 tracks any remaining artifact-only status enhancements (e.g., richer read-only summary and operator acceptance). No publication or canon promotion occurred.

### CI evidence for recovery PR #13

- PR CI: GitHub Actions run `41942987787`, all six Ubuntu/Windows × Python 3.10/3.12/3.14 jobs passed.
- Merged-main CI: GitHub Actions run `41943185191` for `a7e6a1cfa2f7f2cbeec47974cf7dfa86cb054740`, all six jobs passed.
- Live `live-smoke-001` preflight, human disposition, lock execution, and durable archival remain **pending**.

## 2026-11-05 operator verification: author lock approval recorded

The operator reported a successful `lock-reviewed --check` preflight: `eligible_for_author_lock=true`, reviewed draft SHA-256 `83bdd47ccd157d5a33250b6ade5f18843230e7097452118580b02445802e8952`, F1 `DEFER` to BL-001, and `state_mutated=false`. The operator subsequently reported an exact SHA match between `draft-v004.md` and `text-locked.md` and supplied a populated `status` approval block `approvals.text_locked` with `by=Richard Grack`, `at=2026-11-05T13:45:09.979695+00:00` and explicit reviewed draft/hash and `author-text-lock-v004.json` reference.

**Updated GAP-03:** Author approval record and locked-text integrity are **operator-confirmed**. The full `state` value and event-log files were not directly inspected through this chat. Confirm `state=TEXT_LOCKED` and archive the actual `review-adoption-v004.json`, `author-text-lock-v004.json`, `state.json`, `events.jsonl`, `critique-v004.json`, and locked text into private GitHub. **GAP-02 and GAP-04 remain open** until the files are committed / automatic writeback exists. Do not claim archival completion yet.


## Final verification — 2026-11-05: locked text and evidence archived in private GitHub

**Verified through the live GitHub connector**, not merely inferred from terminal output. The private agent repository `main` has commit [`29851bfaf1f59fd623c33aa5211b682bc4a1d689`](https://github.com/rgrack-sys/linkedin-publishing-agent/commit/29851bfaf1f59fd623c33aa5211b682bc4a1d689), message "Archive approved authority-boundary text lock and Critic evidence".

The archive at `docs/decisions/live-smoke-001/` contains reviewed draft, exactly matching locked text, critique and refreshed Critic evidence, author decision/approval, adoption checkpoint, `state.json`, `events.jsonl`, both local captures, original evidence and `SHA256SUMS`. The manifest records the SHA-256 of both `draft-v004.md` and `text-locked.md` as `83bdd47ccd157d5a33250b6ade5f18843230e7097452118580b02445802e8952`. The archive's `state.json` explicitly reports `TEXT_LOCKED`, with `approvals.text_locked.by = Richard Grack` at `2026-11-05T13:45:09.979695+00:00`. The approval record disposition is `F1=DEFER` to BL-001; `publication_approved=false` and `canon_promoted=false`. The event log includes an explicit adoption from `ARTIFACT_ONLY` and the authorized `AWAITING_AUTHOR_CRITIQUE_REVIEW -> TEXT_LOCKED` transition; no fictitious prior history.

**Resolution:** GAP-02 for the current `live-smoke-001` draft/review/approval artifact set is CLOSED; GAP-03 for `live-smoke-001` is CLOSED; GAP-05 was already CLOSED based on successful CLI capture execution. GAP-04, automated writeback/long-term synchronization design, remains OPEN. Earlier conversation coverage (GAP-01), future workflow discipline, binary asset gaps, and downstream visual/publisher integrations remain separate outstanding items. This archival verification is not authorization to publish and does not itself promote new canon.

