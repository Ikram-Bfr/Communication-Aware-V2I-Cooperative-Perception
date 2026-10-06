# Communication-Aware V2I Cooperative Perception

This repository contains the implementation and revision-specific reproducibility materials for:

**Communication-Aware V2I Cooperative Perception for Bird's-Eye-View Semantic Segmentation with Adaptive Fusion Selection**

## Latest reproducibility release

The latest revision-specific implementation is available as:

**v1.1 — Causal Evaluation and Reproducibility Update**

This release corresponds to the revised experimental evaluation and includes the causal, diagnostic, statistical, communication-trace, and computational analyses reported in the revised manuscript.

The implementation includes:

- Local camera-LiDAR feature fusion for ego vehicle and RSU observations
- Learned RSU-to-ego feature-space adjustment
- Reliability-guided V2I cooperative fusion
- Ego-guided temporal RSU feature recovery using a three-frame history
- D3QN-based adaptive perception-mode selection
- Causal communication-interruption evaluation
- Feature-age and temporal-history diagnostics
- Independently trained ego-only and zero-RSU cooperative-fusion comparisons
- Scene-level and scene-clustered bootstrap analysis
- Communication-trace variability analysis
- Computational-complexity and matched GPU-latency evaluation

## Reproducibility scope

The public release provides the source implementation and revision-specific analysis cells in `Communication_Aware.ipynb` used to reproduce the reported experiments.

The repository does not include trained checkpoint files. The released implementation specifies the matched random seeds, training configurations, checkpoint-selection criteria, causal-evaluation protocol, semantic-label mappings, and analysis procedures used in the manuscript.

The principal experiments use matched random seeds:

- 7
- 17
- 27

The causal evaluation uses:

- 37 chronological ego-RSU streams
- Three-frame causal RSU history
- 889 post-initialization evaluation frames
- Causal history updates performed only after successful packet reception
- The same represented semantic class set and evaluation mask across compared methods



| Communication-trace variability | Independent IID packet-loss traces at `p_drop = 0.3`, `0.5`, and `0.7`, with 10 traces per seed/probability | 7, 17, 27 | Communication-trace analysis; `recovered_vs_ego_multiple_traces.json`, `multiple_trace_summary.json` |
| Semantic-class distribution | Valid semantic cells over the 889-frame causal subset and complete 1,000-frame test pool | - | Semantic-distribution analysis section |
| Computational analysis | Precomputed ego and feature-adjusted RSU BEV features; matched batch-size-one GPU profiling | Seed 7 for matched latency profiling | Computational analysis; `matched_recovered_vs_adaptive_latency.json` |
