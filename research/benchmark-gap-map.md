# Paper2Agent Evaluation Gap Map

Date: 2026-09-28  
Branch: research-dev  
Purpose: identify a publication-grade evaluation gap before modifying Paper2Agent.

## Already tested by Paper2Agent

### Tool / execution fidelity
- Generated tools are independently verified against upstream code and reference outputs.
- Verification covers numerical values, dimensions, identifiers, metadata, figures, changed inputs, supported parameters, missing/invalid inputs, upstream failures, repeated calls, artifact isolation, and source reuse.
- MCP runtime acceptance checks inventory, schemas, positive cases, error cases, and fresh-runtime installation.

### End-to-end agent performance
- AlphaGenome tutorial-derived and novel user questions with human grading.
- Comparisons against Claude + repository access and Biomni.
- Runtime and query cost.

### Large-scale evaluation
- 100 computational-biology papers.
- 26 data/discovery-focused papers.
- 10 non-biology computational papers.
- Tutorial-derived execution questions, synthesis questions, and non-biology execution tasks.

### Robustness
- Out-of-scope paper-question permutation benchmark.
- Shortcut/hardcoding checks.
- Repository-drift injections: dependencies, paths, typos, deprecated APIs and longer-tail drift.
- No-executable-tutorial case.
- Multi-agent / validation / MCP-interface ablations.
- Alternate conversion backend.

### Demonstrations
- Adaptive Scanpy parameter selection.
- Multi-paper / multi-agent scientific discovery case studies.
- Human-in-the-loop open-ended analysis.

## Partially tested

- Novel inputs that remain within the supported method.
- Interpretation in specific discovery case studies.
- Multi-paper composition, but not systematic conflict resolution.
- User-query evaluation is described as an optional extension in the current repo.
- Assumptions may be preserved in wrappers/documentation when source-backed, but there is no general automated evaluation of whether the downstream agent respects them.

## Not systematically tested

### 1. In-scope but scientifically invalid use
Questions can be fully related to the paper and technically executable while violating:
- model assumptions
- sample/data requirements
- supported populations or domains
- preprocessing requirements
- identification assumptions
- causal vs associational limits
- paper-stated exclusions or boundary conditions

This is distinct from the published out-of-scope benchmark, which tests unrelated paper-question pairs.

### 2. Epistemic claim fidelity
Whether the agent:
- distinguishes execution from scientific validity
- avoids converting association into causation
- respects exploratory vs confirmatory status
- communicates uncertainty and limitations
- avoids extrapolating beyond the population/domain supported by the paper

### 3. Need for expert intervention on open-ended tasks
The supplement reports several human corrections during a discovery analysis. There is no systematic benchmark of:
- how often expert intervention is needed
- what types of scientific decisions trigger intervention
- whether those interventions can be encoded or automatically enforced

### 4. Scientific-boundary extraction and enforcement
The current system does not appear to build a general machine-readable contract of:
- assumptions
- applicability conditions
- prohibited extrapolations
- required inputs
- supported claims
and enforce it before tool execution.

## Strongest research opportunity

**In-scope scientific boundary compliance**

Core question:

> Can paper agents distinguish between a task that is executable and a task that is scientifically justified by the source paper?

Candidate intervention:
1. Extract a machine-readable Scientific Contract from paper + supplement + code/docs.
2. Check user requests against that contract before execution.
3. Require source-grounded qualification, adaptation, or refusal when a boundary is violated.
4. Benchmark vanilla Paper2Agent vs constraint-aware Paper2Agent on valid and boundary-violating in-scope tasks.

## Why this is distinct from existing Paper2Agent evaluation

Paper2Agent already tests:
- execution fidelity
- novel supported tasks
- irrelevant/out-of-scope rejection
- robustness to broken repositories

The proposed benchmark instead tests:
- **relevant, technically executable, but scientifically unjustified tasks**

This is the gap to validate experimentally before building the intervention.
