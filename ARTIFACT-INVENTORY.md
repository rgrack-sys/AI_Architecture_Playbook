# AI Architecture Playbook Artifact Inventory

**Last reconciled:** October 21, 2026

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
| Post 4 working draft — Evidence Is an Architectural Control | `linkedin/04_evidence_is_an_architectural_control.md` | Added as series source |

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
