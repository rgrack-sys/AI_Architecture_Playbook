# linkedin-publishing-agent V1 core build status

**Date:** 2026-11-02  
**Target repository:** `rgrack-sys/linkedin-publishing-agent`  
**Build specification:** `linkedin/agent/v1-build-spec.md`

## Completed locally

The project was bootstrapped from the current `rgrack-sys/project-bootstrap` v0.2 scaffold and the pre-provider V1 core was implemented.

Implemented:

- persistent post state and append-only event log;
- typed workflow/artifact schemas;
- deterministic state machine;
- explicit Richard-only gates for critic review, text lock, graphic lock, and publication approval;
- replaceable adapter contracts;
- fake corpus, drafter, critic, visual designer, image generator, visual QA, publisher, and archive adapters;
- deterministic LinkedIn character counting using both Unicode code points and UTF-16 code units;
- hard 3,000-unit publication ceiling;
- SHA-256 freezing of final text and graphic;
- end-to-end offline acceptance workflow;
- Windows/Linux CI matrix configuration for Python 3.10, 3.12, and 3.14.

## Validation

- project-bootstrap v0.2 audit: compliant;
- unit/integration/acceptance tests: 10 passed;
- compile check: passed;
- wheel build without network dependencies: passed;
- fresh virtual-environment install with `--no-index --no-deps`: passed;
- installed-package import: passed;
- full tests using independently installed package: 10 passed.

The acceptance test proves a seeded first visual defect is rejected, publication is blocked before explicit approval, final text equals locked text, a publication receipt is required, and archive hashes must match the frozen publication package.

## Local source checkpoint

Local Git commit: `fbb6b5e` — `Bootstrap governed LinkedIn publishing agent V1 core`

Exported source ZIP SHA-256:

`9c230962bb630041391d7a8a7eb20aacd5ac60a1074921e736eb8de894ba70de`

Local Git bundle SHA-256:

`8ce702940d9a3460a3a7b4d202fb03200d6dd529c30c45fa909d37f3fe5e1b6a`

## GitHub publication

The target repository now exists and the verified V1 core has been published to:

`rgrack-sys/linkedin-publishing-agent`

Published main commit:

`aaa9f6b4c5329ca9e0b6a26637bde8e3b3271f7a` — `Bootstrap governed LinkedIn publishing agent V1 core`

The published Git tree was verified against the validated local source by Git blob SHA for all tracked source files.

GitHub Actions CI run `41663966248` completed successfully across the full configured matrix:

- Ubuntu: Python 3.10, 3.12, 3.14
- Windows: Python 3.10, 3.12, 3.14

All six jobs passed.

## Publication verification

- repository visibility: private;
- default branch: `main`;
- GitHub connector permissions: pull + push available;
- repository tree contains the expected source, tests, docs, workflow, and project-standard metadata;
- CI conclusion: **success**.

## Milestone 2 — real Playbook corpus/GitHub adapter

Implemented November 3, 2026 and merged through `linkedin-publishing-agent` PR #1.

Current main commit:

`93812fdd3f630ce9662103015207b0b136e21d31` — `Implement real Playbook corpus/GitHub adapter`

The adapter now:

- resolves the Playbook default branch to a specific commit SHA and tree SHA;
- retrieves candidate content by blob SHA from that immutable snapshot;
- reads current canon, prior LinkedIn posts, and curriculum material;
- classifies current canon as `CANON` and other retrieved material as `SUPPORTING`;
- excludes archived canon under `canon/archive/`;
- excludes LinkedIn agent metadata, assets, and publication metadata from content retrieval;
- fails closed if GitHub returns a truncated repository tree;
- records the repository, branch, commit SHA, and tree SHA in the evidence pack;
- resolves GitHub authentication from an explicit token, `PLAYBOOK_GITHUB_TOKEN`, `GITHUB_TOKEN`, or the existing `gh` CLI login without persisting credentials;
- exposes a CLI evidence-pack smoke command.

Validation expanded from 10 to **16 unit/integration/acceptance tests**. The implementation commit before documentation-only follow-up changes passed the complete six-job Ubuntu/Windows, Python 3.10/3.12/3.14 CI matrix. The current Playbook repository structure was separately inspected through the authenticated GitHub connection to verify the configured source boundaries and the need to exclude archived canon.

## Intentionally not connected

No real drafter/critic model, image-generation provider, visual inspection model, LinkedIn publisher, or Playbook writeback adapter has been connected yet. The next milestone is the model-backed researcher/drafter layer operating on the commit-pinned evidence pack.
