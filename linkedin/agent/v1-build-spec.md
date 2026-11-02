# linkedin-publishing-agent — V1 Build Specification

**Status:** Implementation specification v1.0  
**Date:** 2026-11-02  
**Target repository:** `rgrack-sys/linkedin-publishing-agent`  
**Source-of-truth corpus:** `rgrack-sys/AI_Architecture_Playbook`  
**Implementation standard:** `rgrack-sys/project-bootstrap` v0.2  
**Canon status:** This specification is not itself canon. Canon changes produced by the workflow require explicit author approval.

---

## 1. Purpose

Build a stateful, governed workflow that turns a topic into a reviewed, illustrated, publication-ready LinkedIn post using the AI Architecture Playbook corpus and canon.

The system must preserve the current author-driven process:

1. Richard supplies a topic.
2. The system searches current canon, prior LinkedIn posts, curriculum, and relevant project material.
3. A drafting agent produces an initial draft grounded in the corpus.
4. Richard reviews and instructs revisions.
5. An independent critic attempts to break the argument.
6. Richard accepts, rejects, or modifies the critic findings and locks the text.
7. A visual-design agent creates a graphic brief and generates an infographic only after text lock.
8. A visual-QA step verifies the generated graphic against the approved brief.
9. Richard reviews and instructs visual revisions.
10. A deterministic finalizer assembles the exact LinkedIn payload, character count, hashtags, ALT text, final Markdown, and image.
11. Nothing is published until Richard explicitly approves publication.
12. The published artifact, publication receipt, and final source are written back to the AI Architecture Playbook repository.

The workflow is intentionally human-governed. Human review is not an exception to automation; it is an explicit state transition.

---

## 2. V1 architectural principles

The implementation must follow the existing project and canon rules:

> **Harness governs. Runtime executes. Model reasons. Tools act. State remembers. Trigger starts.**

> **The model can help determine what evidence is needed. It should not be the sole authority on what evidence is sufficient.**

> **The organization defines the evidence standard. Architecture makes that standard executable.**

> **Evidence itself is input. Evidence requirements are architectural controls.**

V1 design decisions:

- Python implementation generated from the current `project-bootstrap` standard.
- Provider-agnostic domain logic.
- Deterministic state machine and validation around probabilistic model calls.
- State persists outside model/chat sessions.
- AI is invoked only for documented reasoning tasks.
- Human approval gates are enforced by the state machine, not by prompt wording alone.
- GitHub is the shared source of truth.
- The final published text must be preserved exactly as published.
- No agent may promote a claim to canon. Agents may propose canon candidates; Richard approves canonization.
- No graphic generation before text lock.
- No publication before explicit publish approval.
- Completion is proven by observable artifacts and receipts, never inferred.

---

## 3. V1 system boundary

### In scope

- Corpus/canon search.
- Evidence-pack construction.
- First-draft generation.
- Author revision loops.
- Independent critical review.
- Text lock.
- Infographic design brief.
- Image generation through a replaceable adapter.
- Visual QA.
- Author visual revision loops.
- LinkedIn character counting and formatting.
- ALT-text generation.
- Publication package assembly.
- Manual publishing in V1 by default.
- Replaceable publisher adapter for later Metricool/LinkedIn integration.
- Publication receipt capture.
- GitHub archival and final writeback.

### Out of scope for V1

- Autonomous canon promotion.
- Autonomous publishing without author approval.
- Social-media analytics optimization.
- Engagement farming or automatic reply generation.
- Multi-platform publishing.
- Fully autonomous topic selection.
- Automatic modification of already approved author text without a visible revision step.
- Automatic alteration of the AI Architecture Playbook canon based on post engagement.

---

## 4. Repository structure

The executable agent is a separate project from the Playbook.

```text
linkedin-publishing-agent/
├── README.md
├── AGENTS.md
├── pyproject.toml
├── .env.example
├── .gitignore
├── docs/
│   ├── project-charter.md
│   ├── operating-rules.md
│   ├── architecture.md
│   ├── git-workflow.md
│   ├── v1-build-spec.md
│   └── prompts/
│       ├── researcher.md
│       ├── drafter.md
│       ├── critic.md
│       ├── visual-designer.md
│       └── visual-qa.md
├── src/
│   └── linkedin_publishing_agent/
│       ├── cli.py
│       ├── orchestrator.py
│       ├── state_machine.py
│       ├── schemas.py
│       ├── character_count.py
│       ├── hashing.py
│       ├── agents/
│       │   ├── researcher.py
│       │   ├── drafter.py
│       │   ├── critic.py
│       │   ├── visual_designer.py
│       │   ├── visual_qa.py
│       │   └── finalizer.py
│       └── adapters/
│           ├── llm.py
│           ├── corpus.py
│           ├── github.py
│           ├── image_generation.py
│           └── publisher.py
├── tests/
│   ├── unit/
│   ├── integration/
│   └── acceptance/
└── workspace/
    └── .gitkeep
```

Working post artifacts live under:

```text
workspace/<post-id>/
├── state.json
├── events.jsonl
├── topic.md
├── evidence-pack.json
├── evidence-pack.md
├── draft-v001.md
├── author-feedback-v001.md
├── critique-v001.json
├── critique-v001.md
├── author-decisions-v001.md
├── text-locked.md
├── visual-brief-v001.json
├── visual-brief-v001.md
├── graphic-v001.png
├── visual-qa-v001.json
├── alt-text.txt
├── publication-package.json
├── final-linkedin.txt
└── publication-receipt.json
```

Artifacts are append/version oriented. An approved artifact is never silently overwritten.

---

## 5. State machine

The orchestrator owns the workflow state. Models do not choose state transitions directly.

| State | Actor | Exit condition |
| --- | --- | --- |
| `TOPIC_RECEIVED` | Orchestrator | Topic and post ID persisted |
| `RESEARCHING` | Research agent | Evidence pack validates |
| `EVIDENCE_READY` | Orchestrator | Draft request created |
| `DRAFTING` | Drafting agent | Draft validates |
| `AWAITING_AUTHOR_DRAFT_REVIEW` | Richard | Revision instruction or approval for critic |
| `REVISING_DRAFT` | Drafting agent | Revised draft validates |
| `CRITIC_REVIEW` | Critic agent | Critique validates |
| `AWAITING_AUTHOR_CRITIQUE_REVIEW` | Richard | Findings dispositioned and text changes instructed |
| `REVISING_AFTER_CRITIQUE` | Drafting agent | Revised draft validates |
| `TEXT_LOCKED` | Richard | Explicit text-lock approval recorded |
| `VISUAL_BRIEFING` | Visual-design agent | Brief validates |
| `VISUAL_GENERATING` | Image adapter | Image returned |
| `VISUAL_QA` | Visual-QA agent | QA pass or revision request |
| `AWAITING_AUTHOR_VISUAL_REVIEW` | Richard | Visual revision instruction or approval |
| `VISUAL_REVISION` | Visual-design/image path | New version generated and checked |
| `GRAPHIC_LOCKED` | Richard | Explicit graphic approval recorded |
| `FINALIZING` | Deterministic finalizer | Publication package validates |
| `READY_TO_PUBLISH` | Orchestrator | Exact payload and hashes frozen |
| `AWAITING_PUBLISH_APPROVAL` | Richard | Explicit publish approval |
| `PUBLISHING` | Publisher adapter / Richard | Publication receipt obtained |
| `PUBLISHED` | Orchestrator | URL/post ID and hashes persisted |
| `ARCHIVING` | GitHub adapter | Final artifacts written to Playbook |
| `COMPLETE` | Orchestrator | Git verification succeeds |
| `BLOCKED` | Orchestrator | Human intervention required |

### Required human-authorized transitions

Only Richard can authorize:

- `AWAITING_AUTHOR_DRAFT_REVIEW -> CRITIC_REVIEW`
- `AWAITING_AUTHOR_CRITIQUE_REVIEW -> TEXT_LOCKED`
- `AWAITING_AUTHOR_VISUAL_REVIEW -> GRAPHIC_LOCKED`
- `AWAITING_PUBLISH_APPROVAL -> PUBLISHING`
- canon-candidate promotion outside this workflow

The system may interpret natural-language equivalents, but it must record the exact author instruction that caused the transition.

---

## 6. Agent contracts

### 6.1 Orchestrator

**Purpose:** deterministic workflow controller.

**Inputs:** current state, latest artifact versions, author instruction.

**Responsibilities:**
- validate legal transitions;
- call the correct specialist;
- persist state before and after calls;
- preserve human-approved content;
- enforce stop conditions;
- create immutable artifact versions;
- never infer approval;
- surface blockers.

**Must not:** write post prose, critique the argument, generate graphics, or publish on its own authority.

---

### 6.2 Research / Canon Agent

**Purpose:** build the evidence pack used by the writer and critic.

**Search order:**
1. current `AI_Architecture_Playbook/ai-architecture-playbook-canon/canon/`;
2. prior posts under `AI_Architecture_Playbook/linkedin/`;
3. curriculum and other relevant Playbook material;
4. external research only when the topic requires current verification, comparison, or a source not supported by the corpus.

**Output classes:**
- `CANON` — already established;
- `SUPPORTING` — consistent project material but not canonical;
- `CANON_CANDIDATE` — new claim worth stress-testing;
- `CONFLICT` — contradicts or materially qualifies current canon;
- `EXTERNAL` — outside research;
- `GAP` — needed assertion not supported by current evidence.

**Must not:** silently reconcile conflicts or promote a candidate to canon.

---

### 6.3 Drafting Agent

**Purpose:** produce a first-person LinkedIn draft grounded in the evidence pack and series history.

**Constraints:**
- write in Richard's established AI Architecture voice;
- preserve canon terminology;
- do not invent new canon;
- distinguish inference from established canon;
- avoid generic AI thought-leadership language;
- make one primary argument per post;
- connect to the previous post only when useful;
- no numbered “Part N” labeling unless requested;
- initial target: 2,200–2,500 LinkedIn-counted units;
- hard working ceiling before author review: 2,750 units;
- retain room for author edits and final hashtags.

**Must not:** generate the infographic or pre-empt the critic.

---

### 6.4 Independent Critic Agent

**Purpose:** attempt to falsify or materially weaken the draft.

**Context provided:**
- current draft;
- evidence pack;
- relevant canon excerpts;
- critic rubric.

**Context deliberately withheld:**
- drafter chain-of-thought or private rationale;
- instructions telling the critic why the drafter believes the argument is correct;
- author praise or desired conclusion.

**Required attack categories:**
- technical correctness;
- novelty / “is this just an existing standard with new wording?”;
- overclaiming;
- terminology collision;
- contradiction with canon;
- unsupported assertions;
- hidden assumptions;
- evidence sufficiency;
- failure modes and counterexamples;
- enterprise applicability;
- ambiguity between model behavior and architectural control;
- series repetition;
- LinkedIn readability and length.

**Output:** findings with severity `BLOCKER | MAJOR | MINOR | NOTE`, challenged claim, rationale, evidence/source, and suggested resolution or test.

**Must not:** replace the whole post with its preferred version unless explicitly asked.

---

### 6.5 Visual Design Agent

**Purpose:** turn the locked argument into an infographic brief.

**Inputs:** only the locked text, approved series style references, prior graphics, and author visual preferences.

**Rules:**
- no graphic work before `TEXT_LOCKED`;
- preserve series identity without simply copying the previous layout;
- one dominant metaphor or visual argument;
- exact text strings must be listed separately from descriptive image-generation instructions;
- identify elements that may not change during surgical edits;
- produce ALT-text draft at brief stage.

**Output:** visual brief, not the final image.

---

### 6.6 Visual QA Agent

**Purpose:** inspect generated graphics before human review.

**Checks:**
- required text present and correctly spelled;
- no unexpected wording changes;
- no duplicated/missing sequence numbers;
- no malformed people/robots/objects;
- no extra limbs or impossible geometry;
- author/footer treatment correct;
- graphic matches locked argument;
- graphic is recognizably in the series while visually distinct;
- text is legible at LinkedIn feed scale;
- no unapproved additions.

Any uncertain material mismatch is a fail requiring regeneration or human review.

---

### 6.7 Finalizer

**Purpose:** deterministic assembly of the exact publication payload.

**Responsibilities:**
- apply approved LinkedIn formatting;
- calculate character count after formatting;
- include spaces, line breaks, punctuation, hashtags, and Unicode formatting;
- calculate both Unicode code points and UTF-16 code units;
- use the larger count as the safety count;
- hard fail if safety count exceeds 3,000;
- target <= 2,750 at finalization;
- preserve exact approved wording;
- generate final ALT text;
- hash final text and image;
- freeze the publication package.

No language-model rewrite is allowed during finalization unless the author explicitly reopens text review.

---

### 6.8 Publisher Adapter

**Interface:**

```python
class PublisherAdapter(Protocol):
    def publish(self, package: PublicationPackage) -> PublicationReceipt: ...
```

V1 implementations:

- `ManualPublisherAdapter` — default. Produces a paste-ready package and waits for Richard to publish. Richard returns the post URL or confirms publication.
- future `MetricoolPublisherAdapter` or direct LinkedIn-capable adapter — may publish only after `PUBLISH_APPROVED`.

Publication is complete only when a receipt includes a URL or provider post identifier.

---

## 7. Prompt contracts

### Researcher system prompt

```text
You are the corpus and canon researcher for Richard Grack's AI Architecture LinkedIn workflow.

Search the current AI_Architecture_Playbook source of truth before drafting claims.
Prioritize current canon, then prior LinkedIn posts, then curriculum and supporting project material.

Return an evidence pack, not a LinkedIn post.

For every material idea classify it as CANON, SUPPORTING, CANON_CANDIDATE, CONFLICT, EXTERNAL, or GAP.
Preserve the source wording and path needed to verify the claim.
Do not silently reconcile contradictions.
Do not promote anything to canon.
Use external research only when the requested topic requires verification not supported by the corpus, and distinguish it clearly.
```

### Drafter system prompt

```text
You are the drafting agent for Richard Grack's AI Architecture LinkedIn series.

Use only the supplied evidence pack, approved author instructions, and series context.
Write in Richard's established architecture voice: practical, technically defensible, process-first, and skeptical of technology-first design.

Make one primary architectural argument.
Preserve canonical terminology.
Do not invent or promote new canon.
Do not generate the graphic.
Target 2,200-2,500 LinkedIn-counted units and remain below the working ceiling.
Return the draft plus a short list of claims that deserve critic attention.
```

### Critic system prompt

```text
You are an independent skeptical reviewer of an AI Architecture argument.

Your job is to try to break the draft, not to praise it and not to rewrite it.

Evaluate technical correctness, novelty, overclaiming, terminology collisions, conflicts with canon, unsupported assumptions, evidence sufficiency, counterexamples, enterprise applicability, and overlap with established patterns such as ReAct, RAG, workflow engines, policy engines, and conventional enterprise architecture.

For each finding assign BLOCKER, MAJOR, MINOR, or NOTE.
State the challenged claim, why it may fail, the evidence or reasoning supporting the challenge, and the smallest useful correction or test.

Do not assume the draft is correct merely because it is consistent with the author's prior work.
```

### Visual designer system prompt

```text
You are the visual-design agent for Richard Grack's AI Architecture LinkedIn series.

The text is locked. Do not change its argument.

Create a visual metaphor that communicates the post's central architectural idea at feed scale.
Maintain the established series typography, footer, and visual quality while avoiding a direct copy of prior layouts.

Return:
1. core visual metaphor,
2. layout,
3. exact required text,
4. optional text,
5. elements that must not change during edits,
6. style continuity requirements,
7. ways this graphic must differ from the prior post,
8. ALT-text draft.
```

### Visual QA system prompt

```text
You are the visual verifier for a LinkedIn infographic.

Compare the generated image to the approved visual brief and locked text.
Look specifically for misspellings, missing text, changed wording, duplicate numbering, malformed anatomy/objects, extra limbs, layout artifacts, incorrect footer/author information, illegibility, and visual claims that differ from the locked argument.

Return PASS only when no material mismatch remains.
When uncertain, return REVIEW_REQUIRED rather than guessing.
```

---

## 8. Artifact schemas

### 8.1 Post state

```json
{
  "post_id": "2026-11-02-evidence-control",
  "topic": "Evidence requirements as architectural controls",
  "state": "AWAITING_AUTHOR_DRAFT_REVIEW",
  "created_at": "ISO-8601",
  "updated_at": "ISO-8601",
  "playbook_snapshot": {
    "repository": "rgrack-sys/AI_Architecture_Playbook",
    "commit_sha": "..."
  },
  "versions": {
    "draft": 1,
    "critique": 0,
    "visual_brief": 0,
    "graphic": 0
  },
  "approvals": {
    "text_locked": null,
    "graphic_locked": null,
    "publish_approved": null
  }
}
```

### 8.2 Evidence pack

```json
{
  "post_id": "...",
  "topic": "...",
  "source_snapshot": {"repo": "...", "commit_sha": "..."},
  "claims": [
    {
      "id": "C1",
      "classification": "CANON",
      "claim": "...",
      "source_path": "...",
      "source_excerpt": "...",
      "notes": "..."
    }
  ],
  "prior_posts": [],
  "external_sources": [],
  "conflicts": [],
  "gaps": [],
  "drafting_constraints": []
}
```

### 8.3 Critique finding

```json
{
  "finding_id": "F1",
  "severity": "MAJOR",
  "category": "overclaim",
  "challenged_claim": "...",
  "rationale": "...",
  "support": ["C3", "external-source-1"],
  "recommended_test_or_change": "...",
  "author_disposition": null
}
```

### 8.4 Visual brief

```json
{
  "core_message": "...",
  "metaphor": "...",
  "layout": "...",
  "required_text": [],
  "optional_text": [],
  "must_not_change": [],
  "series_continuity": [],
  "required_distinctions_from_prior_graphic": [],
  "aspect_ratio": "4:5",
  "alt_text_draft": "..."
}
```

### 8.5 Publication package

```json
{
  "post_id": "...",
  "final_text_path": "final-linkedin.txt",
  "image_path": "graphic-v003.png",
  "alt_text_path": "alt-text.txt",
  "unicode_code_points": 2418,
  "utf16_code_units": 2526,
  "safety_count": 2526,
  "text_sha256": "...",
  "image_sha256": "...",
  "approved_at": "ISO-8601",
  "approved_by": "Richard Grack"
}
```

### 8.6 Publication receipt

```json
{
  "provider": "manual|metricool|linkedin",
  "post_url": "...",
  "provider_post_id": "...",
  "published_at": "ISO-8601",
  "text_sha256": "...",
  "image_sha256": "...",
  "confirmed_by": "Richard Grack|publisher-adapter"
}
```

---

## 9. LinkedIn character-count contract

LinkedIn's 3,000-character ceiling is a release gate.

The finalizer must count after all formatting is applied.

```python
def unicode_code_points(text: str) -> int:
    return len(text)

def utf16_code_units(text: str) -> int:
    return len(text.encode("utf-16-le")) // 2

def linkedin_safety_count(text: str) -> int:
    return max(unicode_code_points(text), utf16_code_units(text))
```

Rules:

- Count spaces.
- Count line breaks.
- Count punctuation.
- Count hashtags.
- Count Unicode pseudo-bold characters.
- Hard fail above 3,000.
- V1 final target: <= 2,750 safety-counted units.
- Any edit after finalization invalidates the count and requires re-finalization.

---

## 10. GitHub interaction contract

### Agent repository

Code changes to `rgrack-sys/linkedin-publishing-agent` use feature branches and pull requests.

Before work:

```bash
git pull
git status
```

After verified work:

```bash
git status
git add .
git commit -m "Describe the change"
git push
git status -sb
```

### Playbook read path

At the beginning of each post:

1. fetch current `main`;
2. record the commit SHA in the post state;
3. search:
   - `ai-architecture-playbook-canon/canon/`
   - `linkedin/`
   - `curriculum/` when relevant;
4. include source paths in the evidence pack.

### Playbook writeback

Working drafts stay in the agent workspace.

After publication, write the actual published artifact to the Playbook:

```text
AI_Architecture_Playbook/
└── linkedin/
    ├── NN_<slug>.md
    ├── assets/
    │   └── NN_<slug>.png
    └── metadata/
        └── NN_<slug>.json
```

The metadata file records publication URL/date, ALT text, content hashes, and source post ID.

Before writeback, refresh `main` and detect conflicts. The next post number is allocated at final writeback, not when research begins.

A successful archive ends with verification that the local branch and `origin/main` are synchronized.

---

## 11. Tests

### Unit tests

- every legal state transition succeeds;
- every illegal transition fails;
- human-gated transitions fail without recorded author approval;
- schemas reject missing required fields;
- approved artifact versions cannot be overwritten;
- LinkedIn count includes whitespace/newlines;
- UTF-16 count handles mathematical Unicode bold correctly;
- finalizer rejects >3,000;
- hashing is stable;
- path/slug generation is deterministic.

### Integration tests with fake adapters

- corpus search returns a known canon item;
- drafting receives only validated evidence-pack inputs;
- critic payload excludes drafter rationale;
- visual generation cannot be invoked before `TEXT_LOCKED`;
- visual QA failure prevents author visual review from being marked approved;
- publisher cannot run without `PUBLISH_APPROVED`;
- manual publisher requires publication URL/confirmation before `PUBLISHED`;
- GitHub writeback uses the frozen published hashes.

### Acceptance test — full workflow

Given a fake topic and deterministic fake adapters:

1. create post;
2. produce evidence pack;
3. produce draft;
4. simulate author revision;
5. run critic;
6. simulate author decision;
7. lock text;
8. build visual brief;
9. generate image;
10. fail first visual QA;
11. generate corrected image;
12. approve graphic;
13. finalize under limit;
14. refuse publication before approval;
15. approve publication;
16. return publication receipt;
17. archive final post;
18. verify final artifact matches published hashes.

The acceptance test must prove both the workflow producer and the artifacts it creates.

### CI matrix

Match the current project standard unless changed by a later project decision:

- Ubuntu and Windows;
- Python 3.10, 3.12, and 3.14;
- zero discovered tests is a failure.

---

## 12. Failure and recovery rules

- Model call failure: remain in current state, record error, retry within policy.
- Corpus unavailable: enter `BLOCKED`; do not draft from memory while presenting it as canon-grounded.
- Critic unavailable: do not skip critic silently.
- Image generation failure: keep locked text unchanged.
- Visual QA failure: no author approval state.
- Character limit failure: reopen formatting/edit step; never truncate invisibly.
- Publisher failure: return to `READY_TO_PUBLISH`; never infer success.
- GitHub conflict: preserve both versions and block writeback until reconciled.
- Publication succeeds but archive fails: keep `PUBLISHED` receipt and retry archive; never republish to solve an archive failure.

---

## 13. Author interaction commands

Canonical commands are accepted alongside natural-language equivalents:

```text
Start LinkedIn post: <topic>
Approve draft for critic
Lock text
Approve graphic
Approve and publish
Posted: <LinkedIn URL>
Show status
Show current artifacts
Resume post: <post-id>
```

### Exact natural-language command to start a new post

> **Start LinkedIn post: <topic>**

Example:

> **Start LinkedIn post: Why AI architecture should distinguish evidence requirements from model reasoning.**

The orchestrator interprets this as:

1. create a new post record;
2. fetch the current Playbook source of truth;
3. build the evidence pack;
4. create the initial draft;
5. stop at `AWAITING_AUTHOR_DRAFT_REVIEW`.

It must not run the critic, generate a graphic, or publish until the corresponding human gates are crossed.

---

## 14. V1 completion criteria

V1 is complete when:

- the full acceptance workflow passes without network/model access using fake adapters;
- real corpus retrieval works against the AI Architecture Playbook;
- author feedback survives every subsequent step;
- critic review is context-separated from drafting rationale;
- text lock blocks further silent prose changes;
- graphic generation is impossible before text lock;
- visual QA catches a seeded typo and a seeded structural visual defect;
- LinkedIn safety counting is deterministic and enforced;
- publication requires explicit author approval;
- a publication receipt proves outcome;
- final Playbook archival preserves the exact published content and hashes;
- CI passes on the supported Windows/Linux/Python matrix;
- the repository conforms to `project-bootstrap` v0.2.

---

## 15. Implementation sequence

1. Bootstrap the new repository from `project-bootstrap`.
2. Implement schemas and file-backed state.
3. Implement state machine and event log.
4. Implement fake adapters.
5. Implement the full acceptance test before provider integrations.
6. Implement GitHub/corpus adapter.
7. Implement LLM researcher/drafter/critic adapters.
8. Implement visual brief and image adapter.
9. Implement visual QA.
10. Implement deterministic finalizer and LinkedIn counter.
11. Implement manual publisher.
12. Implement Playbook archival.
13. Run producer tests and generated-artifact/compliance audit.
14. Only then consider a connected automatic publisher.

---

## 16. V1 architectural shorthand

> **Topic triggers. Corpus supplies evidence. Drafter proposes. Critic challenges. Richard decides. Text locks. Visuals illustrate. QA verifies. Finalizer constrains. Richard authorizes. Publisher acts. Receipt proves. Git preserves.**
