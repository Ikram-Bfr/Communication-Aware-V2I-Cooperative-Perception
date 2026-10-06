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



## Reproducibility manifest

The table below links the principal reported results to the corresponding experimental configuration and implementation/output in `Communication_Aware.ipynb`.

| Reported result | Configuration | Seeds | Notebook section / generated output |
| --- | --- | --- | --- |
| Stage-1 cooperative reference | Initial cooperative perception with ego and RSU camera-LiDAR fusion, initial V2I fusion, and BEV segmentation decoder | 7, 17, 27 | Stage-1 multi-seed evaluation; `stage1_multiseed_test_results.json`, `stage1_multiseed_statistics.json` |
| Stage-2 cooperative result | Learned RSU-to-ego feature-space adjustment with reliability-guided V2I fusion | 7, 17, 27 | Stage-2 multi-seed evaluation; `stage2_multiseed_test_results.json`, `stage2_multiseed_statistics.json` |
| Temporal-recovery validation | Three-frame history, recovery training with `p_drop = 0.5`, current/recovered reception-conditioned evaluation | 7, 17, 27 | Stage-3 temporal-recovery training and validation |
| Causal communication-interruption evaluation | 37 chronological ego-RSU streams, three-frame causal history, 889 post-initialization frames | 7, 17, 27 | Causal evaluation; `stage3_causal_multiseed_statistics.csv` |
| Feature-age analysis | Historical RSU features grouped into frame-index age ranges 1-5, 6-10, 11-20, and >20 | 7, 17, 27 | Feature-age analysis; `reviewer3_feature_age_analysis.csv` |
| Temporal-recovery diagnostics | Proposed recovery, last-received RSU reuse, mean-history aggregation, mismatched history, zero history, zero-RSU diagnostic, and capacity-matched ego-conditioned control | 7, 17, 27 | Temporal-recovery diagnostic section |
| Independently trained ego-only baseline | Ego camera branch, ego LiDAR branch, local fusion, and segmentation decoder only | 7, 17, 27 | Ego-only controlled baseline; `ego_only_causal_889_results.json` |
| Continued-training control | Stage-2 cooperative checkpoint further optimized without temporal recovery | 7, 17, 27 | Continued-training control; `stage2_continued_causal_889_results.json` |
| Scene-level and bootstrap analysis | Ten held-out scenes and scene-clustered bootstrap evaluation | 7, 17, 27 | Scene-level/bootstrap analysis; `scene_level_recovered_vs_ego_bootstrap.json` |
| Communication-trace variability | Independent IID packet-loss traces at `p_drop = 0.3`, `0.5`, and `0.7`, with 10 traces per seed/probability | 7, 17, 27 | Communication-trace analysis; `recovered_vs_ego_multiple_traces.json`, `multiple_trace_summary.json` |
| Semantic-class distribution | Valid semantic cells over the 889-frame causal subset and complete 1,000-frame test pool | - | Semantic-distribution analysis section |
| Computational analysis | Precomputed ego and feature-adjusted RSU BEV features; matched batch-size-one GPU profiling | Seed 7 for matched latency profiling | Computational analysis; `matched_recovered_vs_adaptive_latency.json` |
