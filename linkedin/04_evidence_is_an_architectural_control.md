# Evidence Is an Architectural Control

In my last post, I argued that an observation is not automatically sufficient evidence.

That raises the next architectural question:

Who decides what evidence is good enough?

If the answer is “the model will figure it out,” we have moved an important control into probabilistic behavior. The model can help determine what evidence is needed. It should not be the sole authority on what evidence is sufficient.

The organization defines the evidence standard. Architecture makes that standard executable.

Evidence qualification should not depend entirely on whether the model remembers to ask the right question.

Evidence itself is input. The rules that determine what evidence is required, acceptable, and sufficient are architectural controls.

The policy can vary with the decision.

If a fact is highly volatile, current evidence may be mandatory.

If the decision is high consequence, authoritative evidence may be mandatory.

If provenance is missing, the evidence may not be sufficient.

If the evidence does not support the claim being evaluated, the system should not advance to a state that assumes the claim is true.

If the outcome is ambiguous, the system may need more evidence before acting.

The evidence gate can evaluate:

Volatility — How quickly could this fact change?

Risk — What happens if the system is wrong?

Source Authority / Trust — Which source is allowed to establish the fact?

Freshness — How current must the evidence be?

Provenance — Can we establish where the evidence came from?

Relevance — Does the evidence actually support the claim being evaluated?

Sufficiency — Is what we have enough to justify the next action?

Some evidence controls can be deterministic. Others require governed judgment.

Those requirements do not all have to live inside the model.

They can be expressed through workflow rules, schemas, validators, permissions, policy engines, tool contracts, and state-transition controls.

The model may reason about the evidence.

The architecture determines what evidence is required before that reasoning can be trusted enough to change state or take action.

And when the world changes, the same controls apply again:

Observe → Re-qualify evidence → Update state → Reason again

The goal is not to eliminate uncertainty. It is to stop treating uncertainty as if it were verified state.

Evidence is not just input to reasoning. The requirements for evidence are part of the architecture that governs reasoning.

#AIArchitecture #EnterpriseAI #AgenticAI #AIGovernance
