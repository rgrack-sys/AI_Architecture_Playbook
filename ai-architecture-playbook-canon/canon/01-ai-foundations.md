# Canon 01 - AI Foundations

**Status:** Working Canon v0.1  
**Origin:** August 25, 2026 conversation

## 1. Training and inference are different processes

### Training
Training is the process by which a model's parameters (weights) are adjusted from initially unhelpful values into a structure that captures useful statistical patterns.

The training process repeatedly:
1. receives tokens,
2. predicts,
3. measures error,
4. adjusts weights,
5. repeats at enormous scale.

The resulting model contains a **distillation of patterns learned during training**.

### Inference
Inference is what happens when we use the trained model.

At inference time, the model:
1. tokenizes incoming text,
2. creates internal numerical representations,
3. transforms those representations through its trained weights,
4. uses context to form richer representations,
5. predicts subsequent tokens.

The model is generally **applying learned weights, not retraining them during the conversation**.

---

## 2. Model weights are not a database

A useful correction from the conversation:

> Do not think of the model as querying a hidden database of everything it knows.

The weights are better understood as the learned machinery that transforms input into useful internal representations and predictions.

Knowledge is distributed across the model's parameters. There is not normally one discrete location containing "dog," another containing "red," and another containing "CPR."

A word or token activates and interacts with a large distributed mathematical structure.

### Mental model

A human does not normally hear "dog" and search every memory containing dogs before recognizing the concept.

Likewise, the model does not normally perform a database-style search across everything encountered during training.

**Activation is not retrieval.**

---

## 3. Embeddings and contextual representation

Tokens begin with learned numerical representations.

But meaning is not merely a fixed lookup.

For example:

- "the puppy is blue"
- "the puppy is green"

The initial representation associated with `puppy` begins from the same learned vocabulary representation, but the model's internal representation of that token changes as surrounding context is processed.

Therefore:

> Meaning in a transformer is contextual.

The model does not simply assign independent labels such as:

- puppy = noun
- is = verb
- green = color

Instead, many interacting dimensions form a distributed representation of the complete context.

---

## 4. Distillation is a useful form of compression

A useful mental model developed in the conversation:

If thousands of examples repeatedly express patterns about dogs, the trained model does not need to retrieve all of those examples whenever it encounters a dog-related prompt.

Training has **distilled** statistical regularities from those examples into the weights.

"Compressed" is useful shorthand, with an important caveat:

> The result is not one compressed record or one vector for a concept. The learned representation is distributed across the model.

---

## 5. Vector databases solve a different problem

A vector database should not be confused with the model's learned knowledge.

A retrieval system typically:

1. takes a concrete piece of content such as a paragraph, document section, product description, policy, or note,
2. uses an embedding model to create a vector representing that content,
3. stores the vector along with the original content and metadata,
4. embeds a later query,
5. searches for nearby vectors,
6. retrieves the associated content,
7. provides that content to the model as evidence/context.

This is an **external retrieval mechanism**.

### Key distinction

**Model weights:** learned machinery and distilled patterns.

**Embeddings:** numerical representations produced for inputs/content.

**Vector database:** external storage/index used to retrieve concrete content by similarity.

---

## 6. Why retrieval matters

The model's internal knowledge is finite and can become stale.

This is especially important when information is:

- time-sensitive,
- regulated,
- safety-critical,
- organization-specific,
- proprietary,
- frequently changing,
- or dependent on authoritative current sources.

The architecture should therefore not ask only:

> Can the model answer this?

It should ask:

> **What evidence does the model need before it should answer this?**

That question leads directly to the Evidence-First architecture pattern developed in Canon 02.

---

## Stress test

### Counterargument
"If a capable model already knows the answer, retrieval adds latency and complexity."

### Response
Correct. Retrieval should not be mandatory for every question. The architecture needs a gate that determines whether external/current evidence is required.

### Failure mode
Blindly applying RAG to every question can:
- increase latency,
- introduce irrelevant evidence,
- increase infrastructure cost,
- degrade otherwise-correct answers,
- and create another system that must be governed.

### Canonical position
**Retrieval is a tool for evidence acquisition, not a universal substitute for model knowledge.**

