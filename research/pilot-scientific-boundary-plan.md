# Pilot Scientific-Boundary Benchmark

## Question

Can a paper agent distinguish between a task that is **technically executable** and one that is **scientifically justified by the source paper**?

## Pilot design

The pilot uses the three Paper2Agent showcase systems:
- AlphaGenome
- TISSUE
- Scanpy

Each family has six in-scope boundary cases plus two supported controls.

### Boundary families

**AlphaGenome**
- causal overclaim
- species extrapolation
- condition-specific extrapolation
- personal-genome/disease-risk extrapolation
- distal-regulation confidence
- clinical-use boundary

**TISSUE**
- cross-model calibration transfer
- cross-context calibration transfer
- missing calibration evidence
- ignoring uncertainty in downstream DE
- misinterpreting conformal coverage
- extrapolating validation to untested dataset scale

**Scanpy**
- raw-count differential expression
- cell-level pseudoreplication
- cluster-to-cell-type overclaim
- forced marker-panel transfer
- mixed-species organism heuristic failure
- blind QC-threshold transfer

## Next execution step

Create or retrieve minimal fixtures for the cases, then run the unmodified baseline agent on all 24 cases. No Paper2Agent source changes should be made before baseline responses are frozen.

## Source anchors

- AlphaGenome paper: https://www.nature.com/articles/s41586-025-10014-0
- AlphaGenome official repository: https://github.com/google-deepmind/alphagenome
- TISSUE paper: https://www.nature.com/articles/s41592-024-02184-y
- TISSUE official repository: https://github.com/sunericd/TISSUE
- Scanpy differential-expression documentation: https://scanpy.readthedocs.io/en/latest/api/generated/scanpy.tl.rank_genes_groups.html
- Paper2Agent Scanpy adaptive-parameter evidence: `skills/paper2agent/paper2agent-paper/references/supplement.md`
- Paper2Agent Supplementary Table 2: `skills/paper2agent/paper2agent-paper/assets/supp_table/supplementary-table-2.csv`
