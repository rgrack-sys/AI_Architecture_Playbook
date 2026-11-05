# AI Architecture Playbook Artifact Inventory

**Last reconciled:** November 4, 2026

GitHub is the project source of truth. ChatGPT Library is a durable artifact surface, but it does not synchronize automatically with the repository.

## Repository structure

- `ai-architecture-playbook-canon/` — current canon and archived canon snapshots
- `curriculum/` — architectural methodology curriculum
- `linkedin/` — LinkedIn post source
- `GIT-WORKFLOW.md` — synchronization and publication procedure

## Library artifacts added to the repository

| Library artifact | Repository path | Status |
| --- | --- | --- |
| `01_ai_architecture_starts_before_the_ai.md` | `linkedin/01_ai_architecture_starts_before_the_ai.md` | Added |
| `linkedin_post_2_automation_boundaries-posted.md` | `linkedin/02_automation_boundaries.md` | Added with normalized series filename |
| `03_evidence_before_reasoning.md` and identical numbered copies | `linkedin/03_evidence_before_reasoning.md` | Added once; duplicates excluded |
| Post 4 final — Evidence Is an Architectural Control | `linkedin/04_evidence_is_an_architectural_control.md` | Final posted text captured October 21, 2026 |

## Agent workflow specifications

| Artifact | Repository path | Status |
| --- | --- | --- |
| `linkedin-publishing-agent` V1 build specification | `linkedin/agent/v1-build-spec.md` | Added; implementation target is a separate repository |
| `linkedin-publishing-agent` V1 core build status | `linkedin/agent/build-status-2026-11-02.md` | Review capture ledger merged through PR #10; source-linked follow-on/Critic backlog artifacts; 59 tests; six-job PR and merged-main CI passed; draft-v004 final Critic pass complete |

| LinkedIn content / Critic backlog | `linkedin/backlog/content-backlog.md` | Added; BL-001 preserves authority-boundary follow-on question from live-smoke-001 critique-v004/F1; backlog is not canon |

## Library-only binary artifacts

The following binaries remain durable in ChatGPT Library but are not currently tracked by Git. The authenticated GitHub connector used by ChatGPT Work can publish repository text and Git objects but cannot stream these local binary files. The 43.5 MB source deck should be added only through a Git LFS-capable checkout or another explicitly approved binary-storage policy.

| Library artifact | Status |
| --- | --- |
| `post1.png` | Library-only; pending binary publication path |
| `Post2.png` | Library-only; pending binary publication path |
| `Evidence Before Reasoning.png` | Library-only; pending binary publication path |
| `Adobe_AI - EA Coworker_Methodology.pptx` | Library-only; pending binary publication path |
| `Data_in_Motion_REVISED_05162026.pptx` | Library-only; use Git LFS if added to the repository |

## Library artifacts deliberately not copied over current GitHub files

The Library copies of `README.md`, `GIT-WORKFLOW.md`, `01-ai-foundations.md`, `02-ai-ready-enterprise-architecture.md`, and `02-ai-ready-enterprise-architecture-v0.2.md` are older snapshots or duplicates. They remain in Library but are not authoritative and must not overwrite the current GitHub canon.

## Duplicate handling

`03_evidence_before_reasoning.md`, `03_evidence_before_reasoning(1).md`, and `03_evidence_before_reasoning(2).md` were byte-equivalent in content. The repository retains one normalized file.

## Overlimit conversation recovery — 2026-11-04

The terminal portion of the overlimit LinkedIn development chat is archived in the private `rgrack-sys/linkedin-publishing-agent` repository as `docs/overlimit conversation.md` (commit `3e522b0c1e14672cd3c6026df019e7e0565e0f0f`). It is a partial, 552-line transcript, not proof of full original chat coverage.

The non-canonical audit records are:

| Artifact | Repository path | Status |
| --- | --- | --- |
| Recovered decision register | `linkedin/agent/recovery/2026-11-04-decision-register.md` | Documented decisions, source-linked; distinguishes approval from executed state |
| Preservation gap analysis | `linkedin/agent/recovery/2026-11-04-gap-analysis.md` | Open verification and archival gaps, prioritized |
| Session handoff | `linkedin/agent/recovery/2026-11-04-session-handoff.md` | Resumption instructions; TEXT_LOCKED and publication remain unverified |

No new canon was promoted by this audit. Local working artifacts in Git-ignored `workspace/live-smoke-001` have not been independently verified or published to GitHub.

## Reviewed-artifact recovery source addition — 2026-11-04

| Artifact | Repository path | Status |
| --- | --- | --- |
| Recovery service, CLI and tests | `rgrack-sys/linkedin-publishing-agent` PR #13, commit `a7e6a1cfa2f7f2cbeec47974cf7dfa86cb054740` | Implemented, six PR CI jobs passed |
| Recovery operator guide | `linkedin-publishing-agent/docs/reviewed-artifact-recovery.md` | Added |
| Live author disposition / text-lock record | Hugo-1 `workspace/live-smoke-001/` | **Pending** author approval and execution; not yet Git archived |

This implementation is not canon. The exact post-specific author approval, lock artifacts, and Git archival must still be performed.

### Verified private Git archive for live-smoke-001 — 2026-11-05

The locked text, exact draft, Critic evidence, author disposition, approval, adoption and state/event records, two captures, and SHA-256 manifest are now in private `rgrack-sys/linkedin-publishing-agent` `docs/decisions/live-smoke-001/` at [commit `29851bf`](https://github.com/rgrack-sys/linkedin-publishing-agent/commit/29851bfaf1f59fd623c33aa5211b682bc4a1d689). The verified repository state is `TEXT_LOCKED`, with `publication_approved=false`; no graphic or publication stage is yet complete. Earlier pending-archive notes are historical and superseded by this entry.

### Storage boundary made explicit in agent CLI — 2026-11-05

The private agent repository now provides `artifacts <post-id>` and the `status.artifact_locations` object to distinguish the ignored runtime `workspace/<post-id>/` from tracked decision evidence `docs/decisions/<post-id>/`. It compares local hashes, reports local HEAD archive tracking, and does not claim remote GitHub push confirmation. Implemented in [agent PR #14](https://github.com/rgrack-sys/linkedin-publishing-agent/pull/14), merged at `47e690eb066eae1fa7e9a270032381ce3b7ec6df`; README, `docs/artifact-storage.md`, Git workflow and other docs were updated. Not a change to canon or publication status.

### Manual visual V001/V002 governance pilot — 2026-11-05

Visual source and raster pilot bundle generated locally for `live-smoke-001` (original PNG, editable SVG reconstruction and V002 revision, provisional QA, manifests and validation scripts). Governance documents/index are present on [agent draft PR #16](https://github.com/rgrack-sys/linkedin-publishing-agent/pull/16). **The full ZIP contents are not yet pushed to agent GitHub** and require the operator's explicit import before the PR can merge. Operational visual automation is tracked in [issue #15](https://github.com/rgrack-sys/linkedin-publishing-agent/issues/15). Graphic and publication approvals remain pending.

### V003 visual candidate and process — 2026-11-05

Private agent PR #16 includes V002-F1/F2/F3 findings and reusable visual-preflight command + documentation, while V003 SVG/PNG/source review package is awaiting Git import. Locked text and V001/V002 remain unchanged. New source digest `51f1880d927373c95f1408bca579d58c0cc70407eb76d673f2b83fb1f590065c` and PNG digest `28e16fafea5274e3872f6b3122ff5382f018d4f1f4423da2a6a389aa4fb9c829`. This is a controlled visual QA *candidate*, not a graphic lock nor an operational image pipeline. See [agent PR #16](https://github.com/rgrack-sys/linkedin-publishing-agent/pull/16) and [issue #15](https://github.com/rgrack-sys/linkedin-publishing-agent/issues/15).
