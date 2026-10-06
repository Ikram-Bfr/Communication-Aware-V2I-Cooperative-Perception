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


| Analysis | Corresponding notebook section |
|---|---|
| Causal communication-robustness evaluation | Causal evaluation cells |
| Independently trained ego-only evaluation | Ego-only evaluation cells |
| Temporal-recovery diagnostic controls | Temporal-recovery diagnostic cells |
| Feature-age analysis | Feature-age analysis cells |
| Scene-level and bootstrap analysis | Scene-level/bootstrap analysis cells |
| Communication-trace evaluation | Communication-trace evaluation cells |
| D3QN adaptive-selection evaluation | D3QN evaluation cells |
| Computational profiling | Computational profiling cells |



## Reproducibility manifest

| Experiment / analysis | Main configuration | Generated output |
| --- | --- | --- |
| Stage-1 cooperative perception | Ego and RSU camera-LiDAR fusion with initial V2I cooperative fusion; seeds 7, 17, 27 | `stage1_multiseed_test_results.json`, `stage1_multiseed_statistics.json` |
| Stage-2 cooperative perception | RSU-to-ego feature-space adjustment with reliability-guided V2I fusion; seeds 7, 17, 27 | `stage2_multiseed_test_results.json`, `stage2_multiseed_statistics.json` |
| Causal communication evaluation | 37 chronological ego-RSU streams, three-frame history, 889 post-initialization frames | `stage3_causal_multiseed_statistics.csv` |
| Feature-age analysis | Historical-feature age ranges 1–5, 6–10, 11–20, and >20 frames; seeds 7, 17, 27 | `reviewer3_feature_age_analysis.csv` |
| Ego-only evaluation | Independently trained ego-only perception; seeds 7, 17, 27; 889 causal frames | `ego_only_causal_889_results.json` |
| Continued Stage-2 evaluation | Continued Stage-2 cooperative training and evaluation on the same 889 frames | `stage2_continued_causal_889_results.json` |
| Scene-level bootstrap analysis | Ten held-out scenes with scene-clustered bootstrap evaluation | `scene_level_recovered_vs_ego_bootstrap.json` |
| Communication-trace analysis | IID packet-loss traces at drop probabilities 0.3, 0.5, and 0.7; 10 traces per seed and probability | `recovered_vs_ego_multiple_traces.json`, `multiple_trace_summary.json` |
| Matched latency analysis | Batch-size-one profiling of recovered-RSU and adaptive candidate-evaluation pathways | `matched_recovered_vs_adaptive_latency.json` |
