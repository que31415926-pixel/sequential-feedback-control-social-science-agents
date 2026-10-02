# FROZEN PROTOCOL
## Sequential Feedback Control for Long-Horizon Social-Science Tasks

Status: FROZEN FOR PILOT
Authority: Human research lead
Protocol path: /home/user/Sequential Feedback_MSU/protocol/FROZEN_PROTOCOL.md

This file is the authoritative operational protocol for autonomous agents.
Narrative proposals, chat history, notes, and previous drafts are subordinate to this file.

No agent may silently change this protocol.
Any proposed change must be documented, reviewed, and explicitly approved by the human research lead.

---

## 1. Research Question

Under changing authorized goals, potentially unreliable factual feedback,
limited verification resources, and shrinking recovery opportunities,
can dependency-aware sequential control improve task quality and/or
cost efficiency relative to strong matched baselines?

The primary application contribution is long-horizon social-science work.

The method must not be justified merely by:
- structured memory,
- action-conditioned value,
- rollback,
- verification-before-commit,
- a larger number of components,
- or defeating a weak baseline.

---

## 2. Evidence Contracts

Three claim families must remain distinct.

### C_utility
Does the method improve native task performance or efficiency on public
long-horizon task environments?

### C_mechanism
Do controlled G × F × K experiments provide evidence about when and why
verification, clarification, replanning, and recovery timing matter?

### C_structure
Does the proposed dependency-aware representation/control provide an
incremental advantage over a matched general planner at comparable
information, training data, planning depth, and budget?

If the matched general planner P matches S, do not claim structural necessity.
Efficiency-only advantages must be described as efficiency contributions.

Native benchmark evidence and mechanism-extension evidence must never be
merged into a single "official benchmark score."

---

## 3. Primary Application Environments

Preferred first-line resources:

1. ReplicatorBench
   - primary social-science coder application
   - preserve native goals, task semantics, and official scoring

2. tau-bench / tau2-bench family
   - tool-using long-horizon control environment
   - retail and airline domains are not counted as two independent benchmark families

3. TEA-Bench
   - primary chatbot / emotional-support application candidate
   - preserve native scores
   - do not infer clinical effectiveness or wellbeing improvement

Additional candidates may be used only under preregistered substitution rules,
including SocSci-Repro-Bench, ESC-Eval, and AppWorld.

A rewritten or researcher-created extension must be labeled as an extension,
not as a native benchmark result.

---

## 4. G × F × K Mechanism Design

Each eligible base task generates eight cells.

### G — Goal
G0: stable / reiterated authorized goal
G1: authorized goal revision

Goal revision must be distinguished from mere clarification.
Both old and revised goals must be legally and practically executable.

### F — Fact
F0: valid factual feedback
F1: independently verifiable false, obsolete, or invalid factual feedback

Source style, tone, length, and verifiability should be matched where feasible.

Subjective experience is not automatically a falsifiable F claim.

### K — Recovery
K0: recovery-sufficient
K1: recovery-constrained

K is an environment condition, not:
- model competence,
- observed final success,
- or a post-hoc label based on which method won.

G and F events occur at the same legal point in a shared prefix.
They must be environment-triggered, not injected at the moment a method fails.

K is assigned before method execution.
Where paired counterfactual runs are possible, randomize run order and align
exogenous random streams.

---

## 5. Recovery Measurement

Recovery is measured using three separate dimensions:

A — feasibility:
whether a legal repair path exists and its reference-policy recovery probability

C — cost:
additional tokens, calls, time, compute, and monetary/resource cost required

W — recovery window:
latest point at which repair can begin and remaining effective opportunities

A, C, and W are not collapsed into a reflective scale.

K0 requires a feasible repair path within remaining budget and meaningful
recovery opportunity.

K1 may include difficult-but-still-recoverable states.
It does not require recovery to be impossible.

Thresholds are frozen using development data only.

---

## 6. Mechanism-Task Inclusion

A task may enter the confirmatory G × F × K mechanism experiment only if:

- F has independently verifiable truth status;
- G1 is a legal and feasible authorized revision;
- at least two meaningful control points remain after the event;
- an interpretable dependency chain exists;
- K can be assigned or manipulated independently of method outcome.

Screening occurs before comparing S with baselines.

Report:
- parent task pool,
- inclusion rate,
- exclusion reasons.

Do not manufacture unnatural tasks merely to fill quotas.

---

## 7. Controller Information Boundary

The online controller may access only information legitimately available at
the current task state.

Forbidden controller inputs include:
- evaluator ground truth,
- hidden future events,
- future goals not yet observed,
- offline branch returns,
- future-critical diagnostic labels,
- held-out answers,
- evaluator-only state.

Evaluator truth and controller-visible state must remain technically separated.

A goal update and a factual claim occurring in the same user message must be
represented separately. Falsifying a factual claim must not automatically
erase a valid authorized goal revision.

---

## 8. Shared Action Interface

Core actions:

EXECUTE(u)
VERIFY(c, v)
CLARIFY(q)

Rollback, waiting, compensation, staging, or transactional operations may be
used only where the environment genuinely supports them.

Verification must consume its actual resource cost.

After VERIFY, the controller must observe the result and make a new decision.

---

## 9. Proposed Controller S

The main implementation uses:

- typed state for goals, beliefs, actions, and unresolved items;
- explicit dependency relations;
- local invalidation/reuse where dependencies are unchanged;
- global rescoring when budgets, deadlines, or candidate competition change;
- explicit recovery information;
- depth-2 rolling lookahead;
- learned truncated continuation value.

Planning depth counts real control actions.
A VERIFY observation branch consumes a decision layer.

At each decision point, first-round planning uses at most:
- 4 feasible action candidates;
- 2 predicted observation samples per predicted action.

Any later increase must be shared across matched planning baselines.

---

## 10. Required Baselines

N — strong native agent
R — tuned conditional control workflow
M — single-step long-horizon value policy
V — noisy sequential Value-of-Information controller
P — matched generic depth-2 planner
S — proposed controller

Core isolation comparisons use R, M, V, P, and S.

N is required for native end-to-end utility comparison.

P must share, as applicable:
- visible state fields,
- candidate generator,
- transition/observation predictor,
- training labels,
- planning depth,
- tuning budget,
- evaluation budget.

Do not give S free graph information unavailable to P.

Jev and J+Recovery are supplementary controls.
They do not replace M, V, or P.

A fixed workflow baseline must be allowed meaningful branching,
verification, clarification, and legitimate rollback where supported.
Do not construct a straw-man fixed sequence.

---

## 11. Data Separation

Split by base task family / paper identity, not by generated condition.

All of the following derived from one base task stay in the same split:
- eight G × F × K cells,
- rewrites,
- analysis targets,
- checkpoints,
- random seeds.

Required partitions:

development
selection-validation
pilot holdout
formal confirmation

Formal test material must never be used for:
- prompt tuning,
- error-driven redesign,
- branch generation,
- threshold selection,
- baseline tuning.

Once pilot holdout results are inspected, those tasks cannot later be called
unseen formal-confirmation tasks.

---

## 12. Statistics and Confirmatory Priorities

Independent statistical units are base task families / papers.

Repeated rollouts improve precision but do not create new independent samples.

Use:
- paired task-level contrasts;
- clustered bootstrap intervals;
- effect sizes;
- Holm correction for the small set of confirmatory comparisons.

At least 3 independently trained seeds are required for formal stability claims.

Primary confirmatory priorities:

1. overall paired native-task difference;
2. paired difference in G1F1K1;
3. noninferiority under clean / recovery-ample conditions.

Provisional development values:

practical improvement target delta = 0.05
noninferiority margin epsilon = 0.02

These values may be frozen using development information and domain judgment
before confirmatory evaluation. They must not be tuned on held-out outcomes.

Do not use p < .05 as the pilot pass criterion.

---

## 13. Pilot Gates

### P0 — Runtime Acceptance

Scale:
2 development tasks per application line.

Required:
- version lock;
- native agent runs end-to-end;
- native scorer runs;
- complete event/cost/outcome logs;
- task/environment failures separated from legitimate agent failures.

No algorithm superiority comparison is allowed before P0 passes.

### P1 — Task Audit

Scale:
48 development tasks:
- 16 coder,
- 16 tool/control,
- 16 chatbot.

Run strong starting points N and R twice where specified.

Audit:
- long-horizon dependency;
- goal semantics;
- factual verifiability;
- recovery semantics;
- native scorer validity;
- candidate G/F/K coverage.

### P2 — Condition and Branch Construction

Target:
32 base tasks.

Per principal family:
- 12 training tasks;
- 4 selection-validation tasks.

Construct and blind-audit the eight G × F × K conditions.

Freeze:
- main resource budget;
- quality criteria;
- K thresholds;
- strong-rule baselines;
- shared branch-generation rules.

### P3 — Pilot Holdout Experiment

Initial:
16 base tasks, two families × 8.

Run:
8 G/F/K cells
× 2 evaluation seeds
× 8 strategies.

Strategies:
R
M
V
P
S
S without explicit lookahead
S without explicit recovery features
S with full refresh replacing local reuse

If V and P collapse to effectively the same implementation,
do not duplicate them merely to preserve a count.

### P4 — Native Application and Review

Separate native holdout:
24 tasks, three application lines × 8 where executable.

Compare native-task N, R, P, S with two runs each.

Report:
- native utility,
- mechanism results separately,
- total cost,
- failures,
- uncertainty,
- human-evaluation calibration where applicable.

If one application line is not executable, narrow the claim.
Do not fabricate an equivalent custom task and call it native evidence.

---

## 14. Pilot Expansion Criteria

Expansion toward formal experiments requires all of the following:

- zero known evaluator-truth leakage;
- complete critical cost logging;
- frozen scorer versions;
- deterministic replay verified where claimed;
- no unresolved authorization or fabricated-truth errors;
- K has auditable environmental separation supported by A/C/W;
- correct execution remains possible under both K levels;
- native and mechanism-extension identities remain separated;
- strong baselines leave meaningful room for improvement or efficiency gain.

Evidence for further algorithm investment should include interpretable benefit
in at least two independent task families, or material resource savings under
predeclared noninferior quality.

If P or M matches S, report the boundary and narrow the structural claim.

If benefit exists only in researcher-created extensions, do not make a general
native-performance claim.

If support-quality scores improve while factual or process validity worsens,
do not claim social-science application success.

---

## 15. Required Logging

Every episode must preserve, where applicable:

task_manifest
- native task ID
- task/paper family
- code/data/version
- split
- G/F/K
- K manipulation dimension
- authorized goal
- scorer version

event_log
- event index
- goal version
- visible messages
- tool input/output
- source/time
- state-summary hash

decision_log
- candidates
- feasibility
- supporting/dependent claims
- selected action
- scores
- lookahead samples
- model/prompt version

recovery_audit
- standardized deviation
- legal repair paths
- A/C/W
- reference strategy
- repeats
- uncertainty

cost_log
- input/output tokens
- tool calls
- retries
- latency
- GPU time
- monetary/resource cost
- remaining budget

outcome_log
- native score
- extension score
- human coding where relevant
- infrastructure status
- budget violations
- completion/exclusion reason

Also preserve:
- git commit;
- model/API version;
- random/event seeds;
- dependency environment;
- data/license restrictions.

---

## 16. Review and Human Gates

Formal gates require an independent reviewer.

Reviewer outputs exactly one primary status:

PASS
REVISE
BLOCK

PASS means the evidence packet supports proceeding to the human gate.
PASS does not authorize autonomous crossing of a human approval gate.

REVISE means correctable evidence, implementation, measurement, or protocol
deficiencies remain.

BLOCK means proceeding would violate protocol integrity or invalidate the
planned inference.

The reviewer must independently inspect direct evidence.
Main's summary is not evidence.

Before PASS, reviewer must identify at least one plausible failure mode and
state what direct evidence rules it out.

Human research lead is final authority.

---

## 17. Formal Review Packet

Before every formal gate, Main must create:

review_packets/<GATE>/
  REVIEW_REQUEST.md
  CLAIMS.md
  EVIDENCE_INDEX.md
  METRICS.csv
  CHANGES.diff
  REPRO_COMMANDS.md

The packet is an index, not a substitute for source evidence.

Reviewer begins from the packet and follows EVIDENCE_INDEX.md to inspect
source files directly.

Do not indiscriminately load the full repository into reviewer context.

Missing evidence must be treated as missing evidence, not inferred.

Formal reviewer runs should use a fresh isolated reviewer session.

---

## 18. Protocol Amendment Rule

This protocol is frozen for the pilot.

No agent may overwrite it.

A change requires:

1. a written amendment proposal;
2. reason and expected inferential impact;
3. identification of affected data/gates;
4. independent reviewer assessment;
5. explicit human approval;
6. timestamped entry in protocol/AMENDMENTS.md.

A held-out result may never be retroactively converted into a development
result by editing this file.

