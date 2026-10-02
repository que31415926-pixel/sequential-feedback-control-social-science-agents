# Review Request — P0 Runtime Acceptance

Gate: P0

Current state: IN PREPARATION

Requested decision after evidence collection:
PASS / REVISE / BLOCK

## Scope

Determine whether the required application environments, native agents,
native scorers, logging, and information boundaries are sufficiently
operational to proceed beyond P0.

P0 is an infrastructure and measurement-validity gate.

P0 is NOT a method-superiority evaluation.

## Required Application Lines

1. Social-science coder
   Preferred environment: ReplicatorBench

2. Tool-using long-horizon control
   Preferred environment: tau-bench / tau2-bench

3. Multi-turn chatbot
   Preferred environment: TEA-Bench

Initial target:
2 development tasks per application line.

## Evidence Required Before Review

- exact benchmark and repository version;
- environment startup evidence;
- native agent complete trajectory;
- native scorer output;
- event log;
- cost log;
- outcome log;
- task identity and development split;
- clear infrastructure-failure classification;
- confirmation that evaluator-only truth is not available to the controller.

## P0 Prohibitions

P0 must not be used to:

- claim that S outperforms baselines;
- tune on held-out material;
- change native scorer semantics after observing method results;
- silently remove difficult tasks;
- replace an unavailable native benchmark with an artificial favorable task.

## Reviewer Instruction

Do not issue PASS until the required direct evidence exists.

If evidence collection has not yet occurred, the appropriate status is REVISE,
with missing evidence explicitly identified.
