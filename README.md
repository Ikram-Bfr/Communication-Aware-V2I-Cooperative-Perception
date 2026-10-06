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

| Experiment / analysis | Main configuration | Notebook reference |
| --- | --- | --- |
| Stage-1 cooperative perception | Initial ego–RSU cooperative perception with local camera–LiDAR fusion, initial V2I cooperative fusion, and BEV semantic decoding | Stage-1 training and evaluation cells |
| Stage-2 cooperative perception | RSU-to-ego feature-space adjustment followed by reliability-guided V2I cooperative fusion | Stage-2 training and evaluation cells |
| Temporal RSU recovery | Ego-guided temporal recovery using a three-representation RSU history; model-development evaluation uses the temporal-sequence protocol implemented in the notebook | Temporal-recovery training and evaluation cells |
| Causal communication-robustness evaluation | 37 chronological ego–RSU streams, history length \(K=3\), and 889 post-initialization evaluation frames using causally available RSU history | Causal communication-evaluation cells |
| Independently trained ego-only evaluation | Ego camera, ego LiDAR, local camera–LiDAR fusion, and segmentation decoder only; evaluated on the same 889 post-initialization frames | Ego-only training and evaluation cells |
| Continued Stage-2 evaluation | Continued optimization of the preceding Stage-2 cooperative model without temporal recovery; evaluated with the current ego feature and current adjusted RSU feature available for all 889 frames | Continued Stage-2 training and evaluation cells |
| Temporal-recovery diagnostic controls | Proposed history-conditioned recovery compared with last-received RSU reuse, mean-history aggregation, mismatched history, capacity-matched ego-conditioned input, zero history, and the zero-RSU cooperative-fusion diagnostic under sustained post-initialization interruption | Temporal-recovery diagnostic cells |
| Feature-age analysis | Recovered-RSU fusion and the zero-RSU cooperative-fusion diagnostic evaluated across historical-feature age ranges defined using the preserved original frame indices | Feature-age analysis cells |
| Scene-level and scene-clustered bootstrap analysis | Paired recovered-RSU and independently trained ego-only evaluation over the ten held-out test scenes, with scene-clustered bootstrap resampling | Scene-level and bootstrap-analysis cells |
| Communication-trace evaluation | Fixed recovered-RSU fusion and reception-conditioned current/recovered-RSU policies evaluated using multiple independently generated causal IID packet-loss realizations | Communication-trace evaluation cells |
| D3QN adaptive-selection evaluation | Communication-aware selection among zero-RSU, current-RSU, recovered-RSU, and mixed current–recovered RSU perception modes under causal packet-loss conditions | D3QN training and evaluation cells |
| Computational profiling | Matched batch-size-one profiling of the recovered-RSU pathway and adaptive candidate-evaluation pathway from precomputed ego and adjusted-RSU BEV features | Computational-profiling cells |
