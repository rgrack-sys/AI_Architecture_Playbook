# Evidence Before Reasoning

We spend a lot of time asking whether an AI model is capable of answering a question.

Enterprise architecture needs to ask a different question first:

**What evidence does the system need before it should be allowed to answer?**

That distinction is becoming fundamental to how I think about AI architecture.

A model may contain enormous amounts of learned knowledge.

That doesn't mean its internal knowledge is:

current,

authoritative,

specific to your organization,

appropriate for this decision,

or even something the model should rely upon.

So before reasoning, I want an **Evidence-First Gate**.

The system should determine:

Is this information volatile?

What is the risk if it is wrong?

Do we need current evidence?

What source is authoritative?

How fresh is the evidence?

Where did it come from?

Can we establish provenance?

Only then do we reason and act.

This changes the architecture significantly.

The basic pattern becomes:

**Assess risk and volatility → Acquire evidence → Validate authority, provenance, and freshness → Reason → Act**

And it leads to a broader principle:

**Data quality defines reasoning quality.**

A more capable model reasoning over stale, incomplete, or poorly governed evidence may simply produce a more convincing wrong answer.

The architecture therefore cannot stop at the model.

Evidence acquisition, provenance, freshness, volatility, context assembly, evaluation, and governance are part of the reasoning system.

That is where I think much of the next generation of enterprise AI architecture will actually be built.

#AIArchitecture #EnterpriseAI #AIEngineering
