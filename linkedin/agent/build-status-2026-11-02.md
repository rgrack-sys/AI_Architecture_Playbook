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

Validation expanded from 10 to **16 unit/integration/acceptance tests**. The merged main commit passed the complete six-job Ubuntu/Windows, Python 3.10/3.12/3.14 CI matrix in GitHub Actions run `41685374351`. The current Playbook repository structure was separately inspected through the authenticated GitHub connection to verify the configured source boundaries and the need to exclude archived canon.

## Milestone 3 — model-backed researcher/drafter layer

Implemented November 3, 2026 and merged through `linkedin-publishing-agent` PR #2.

Current main commit:

`4d83bd1ccb520b47d799f433dfa2f8c6d6808d1f` — `Implement model-backed researcher and drafter layer`

The workflow now inserts explicit model-reasoning states between evidence retrieval and drafting:

```text
EVIDENCE_READY
  -> RESEARCH_ANALYSIS
  -> RESEARCH_READY
  -> DRAFTING
  -> AWAITING_AUTHOR_DRAFT_REVIEW
```

The researcher consumes only the commit-pinned `EvidencePack` and produces a versioned `ResearchAnalysis`. Material ideas remain classified as `CANON`, `SUPPORTING`, `CANON_CANDIDATE`, `CONFLICT`, `EXTERNAL`, or `GAP`.

Deterministic controls now enforce source boundaries around the model:

- `CANON` ideas must cite only evidence already classified as canonical;
- supporting material cannot be promoted to canon through model output;
- `CANON_CANDIDATE` ideas must cite at least one supplied evidence item;
- an empty evidence pack fails before model invocation rather than allowing the model to fill the corpus gap;
- unknown evidence references are rejected;
- `GAP` ideas cannot be used as factual draft support;
- the governed primary argument selected by research must appear in the draft;
- unresolved gaps and critic-attention items remain visible in draft metadata;
- model/provider/response/token provenance and the Playbook snapshot SHA are retained.

The drafter produces paired artifacts:

- `draft-vNNN.md` — human-readable post text;
- `draft-result-vNNN.json` — used research idea IDs, unresolved gaps, critic-attention points, model provenance, and LinkedIn safety count.

Author revision instructions are treated as constraints. In particular, instructions such as “change nothing else” require preservation of unrelated approved text.

The first real model provider implementation uses the OpenAI Responses API behind a provider-neutral `StructuredModelClient`. Requests use strict structured output, `store=false`, explicit reasoning effort, and expose no web/file/MCP tools. The model is configurable; the current default is `gpt-6.1-sol`.

Validation expanded to **30 unit/integration/acceptance tests**. PR #2 passed the complete six-job Ubuntu/Windows, Python 3.10/3.12/3.14 CI matrix before merge, and merged main commit `4d83bd1ccb520b47d799f433dfa2f8c6d6808d1f` passed the same matrix in GitHub Actions run `41690338787`.

A real OpenAI network call has deliberately not been executed in CI because no API credential is stored or exposed in the repository. A live local smoke command is available once `OPENAI_API_KEY` is configured.

## Milestone 4 — live researcher/drafter validation, cleanup, and runtime documentation

Completed November 3, 2026 and merged through `linkedin-publishing-agent` PR #5.

Current agent main commit:

`d63a7832c02c6fc86cb0e5fd6420a2db2834b4ab` — `Clean live draft artifacts and document autonomous runtime topology`

A live billable smoke test was executed on Hugo-1 using the project Python 3.12 virtual environment. The real execution path completed:

```text
GitHub Playbook
  -> commit-pinned EvidencePack
  -> OpenAI Researcher
  -> deterministic source-boundary validation
  -> OpenAI Drafter
  -> deterministic draft validation
```

Observed live behavior:

- Researcher and Drafter both returned real OpenAI responses using `gpt-6.1-sol`.
- The run used Playbook commit `54cb32a293a326fda1b374424dfc97045d674697`.
- The Researcher kept established material separated as `CANON` / `SUPPORTING`.
- The new explicit-authority design discipline remained a `CANON_CANDIDATE`, not established canon.
- Authority assignment/enforcement remained an explicit `GAP`; the Drafter did not turn the gap into factual support.
- The draft used the governed primary argument and returned a LinkedIn safety count of 2,336.

Two cleanup findings from the live run were then fixed:

1. equivalent unresolved-gap wording is deduplicated deterministically using conservative normalized/leading-clause comparison;
2. Markdown draft and locked-text artifacts now end with a trailing newline.

The test suite expanded to **33 unit/integration/acceptance tests**. Merged agent main commit `d63a7832c02c6fc86cb0e5fd6420a2db2834b4ab` passed the full six-job Ubuntu/Windows, Python 3.10/3.12/3.14 matrix in GitHub Actions run `41722112192`.

### Autonomous component/runtime documentation standard

The agent repository now maintains:

- `docs/autonomous-component-inventory.md` — what each agent/autonomous function does, implementation language/module, execution environment, remote services, state/artifacts, commands, configuration names, authority and operational status;
- `docs/autonomous-component-documentation-standard.md` — required documentation fields and same-change update rule;
- `docs/glossary.md` — common definitions and overloaded acronyms.

The inventory explicitly distinguishes:

- where the application code executes;
- where remote model/service execution occurs;
- where durable state is stored;
- where Continuous Integration (CI) tests execute.

This documentation discipline was propagated into `rgrack-sys/project-bootstrap` standard **v0.3.0** and merged there at commit:

`e54b98a7db94a9bc6f60a3fe75ae76f9b33f0f62`

The project-bootstrap v0.3 main CI matrix passed on Ubuntu and Windows across Python 3.10, 3.12, and 3.14. The LinkedIn agent metadata now targets project standard v0.3.0.

## Milestone 5 — independent model-backed Critic

Implemented November 3, 2026 and merged through `linkedin-publishing-agent` PR #6.

Current agent main commit:

`0d942d1a86b02e32af23e83873f064e8de0f7d58` — `Implement independent model-backed Critic agent`

The Critic now performs an adversarial review after author draft approval and before text lock.

The enforced context boundary is:

```text
Critic input = current draft + commit-pinned EvidencePack
```

The Critic does **not** receive:

- `ResearchAnalysis`;
- `DraftResult`;
- drafter rationale;
- author feedback/history;
- drafter chain-of-thought.

This is context separation rather than a requirement for a different model vendor. The implementation uses a fresh stateless structured request through the same provider-neutral `StructuredModelClient` boundary.

The Critic checks:

- technical correctness;
- conflict with canon;
- unsupported claims;
- overclaims;
- novelty / prior-art claims;
- terminology;
- hidden assumptions;
- counterexamples;
- enterprise applicability;
- series repetition;
- logic;
- clarity;
- questions requiring external verification.

Findings use the severity scale:

`BLOCKER / MAJOR / MINOR / NOTE`

Evidence controls remain deterministic around the model:

- every cited support item must be a real EvidencePack evidence ID;
- unknown evidence IDs are rejected;
- duplicate finding IDs are rejected;
- `CANON_CONFLICT` findings must cite canonical evidence;
- `NOVELTY_PRIOR_ART` conclusions require supplied evidence;
- where supplied evidence is insufficient, the Critic must use `EXTERNAL_VERIFICATION_NEEDED` rather than treating pretrained model knowledge as proof;
- a failed structured result can receive one bounded corrective retry without expanding the source set.

The resulting `critique-vNNN.json` artifact preserves:

- structured findings;
- a harness-generated context-separation note;
- model/provider/response/token provenance;
- Playbook commit SHA;
- SHA-256 of the exact draft reviewed;
- explicit context inputs: `["draft", "evidence_pack"]`.

A new operator/live-test command is available:

```bash
linkedin-publishing-agent critic --post-id <post-id>
```

It reviews the latest `draft-vNNN.md` by default, can target a specific draft version, and writes the next versioned critique artifact. In the governed stateful workflow, the Critic still runs only after Richard authorizes the transition into `CRITIC_REVIEW`.

Documentation was updated in the same change:

- `docs/model-backed-critic.md`;
- `docs/prompts/critic.md`;
- `docs/autonomous-component-inventory.md`;
- `docs/architecture.md`;
- `docs/operating-rules.md`;
- `docs/glossary.md`.

The glossary now also defines Independent Critic, context separation, adversarial review, prior art, critique severity, Retrieval-Augmented Generation (RAG), and ReAct in project context.

Validation expanded to **44 unit/integration/acceptance tests**.

PR #6 passed all six Ubuntu/Windows × Python 3.10/3.12/3.14 jobs in GitHub Actions run `41776700496`.

Merged main commit `0d942d1a86b02e32af23e83873f064e8de0f7d58` passed the same complete matrix in GitHub Actions run `41776840685`.

A live billable Critic API call has not yet been run. The real adapter is implemented and CI-validated; the next live validation step is to run the Critic against the existing `live-smoke-001` draft/evidence workspace on Hugo-1.

## Intentionally not connected

No real image-generation provider, visual inspection model, LinkedIn publisher, or Playbook writeback adapter has been connected yet. The independent Critic is implemented and CI-validated; its live OpenAI smoke test remains pending. After that validation, the next architectural milestone is the real visual-design/image-generation path.
