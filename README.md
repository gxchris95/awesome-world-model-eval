# Awesome World Model Evaluation [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of **benchmarks and metrics for evaluating world models** — across language, video, 3D/4D, driving, and embodied settings.

![Papers](https://img.shields.io/badge/papers-63-blue) ![Updated](https://img.shields.io/badge/updated-2026--06-green) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing) ![License](https://img.shields.io/badge/license-CC0-lightgrey)

World models learn to *simulate* an environment and predict how it changes under actions. As they scale, the hard question shifts from *"can it generate a plausible-looking future?"* to *"is that future physically correct, geometrically consistent, controllable, and useful for a task?"* This list collects the benchmarks and metrics that try to answer it.

---

## Contents

- [Why Evaluate World Models?](#why-evaluate-world-models)
- [Evaluation Dimensions](#evaluation-dimensions)
- [🆕 2026 Papers at a Glance](#-2026-papers-at-a-glance)
- [Benchmarks by Modality](#benchmarks-by-modality)
  - [Language & Symbolic](#language--symbolic)
  - [Video / Pixel](#video--pixel)
  - [3D / 4D](#3d--4d)
  - [Driving](#driving)
  - [Embodied & Policy Evaluation](#embodied--policy-evaluation)
  - [Physics-Centric](#physics-centric)
  - [Other / Workshop](#other--workshop)
- [Metric Reference Tables](#metric-reference-tables)
  - [Common metrics](#common-metrics)
- [Evolution of Evaluation (diagrams)](EVOLUTION.md)
- [Contributing](#contributing)

---

## Why Evaluate World Models?

A recurring, independently-replicated finding across the 2025–2026 literature: **visual realism does not imply physical plausibility, geometric consistency, executability, or task success.** Models that top perceptual leaderboards (FID/FVD/VBench) routinely violate conservation laws, break under viewpoint changes, freeze when the camera looks away, or fail to drive a policy to its goal. Reported by [World-in-World](#video--pixel), [WorldArena](#embodied--policy-evaluation), [WorldLens](#driving), [RoboWM-Bench](#embodied--policy-evaluation), [CRONOS](#video--pixel), and [Out of Sight](#video--pixel), among others.

The frontier of evaluation is therefore moving **from "does it look right?" to "does it work?"** — toward functional, closed-loop, and causal tests.

---

## Evaluation Dimensions

Metrics across these benchmarks cluster into five families (lower rungs are the harder, more discriminative tests the field is moving toward):

| Dimension | What it measures | Typical metrics | How computed |
|---|---|---|---|
| **1. Visual fidelity** | Per-frame / clip realism | FID, FVD, IS, PSNR, SSIM, LPIPS, VBench | Automatic (pretrained nets) |
| **2. Consistency & persistence** | Coherence over time, views, memory | DINO/CLIP consistency, reprojection error, World Stability, rFID, InterStab | Automatic + specialist vision models |
| **3. Controllability & action fidelity** | Does output follow the action/instruction? | Camera-pose error (ATE/RPE), IEC, trajectory DTW/ADE/FDE, `1−LPIPS` | Automatic (SLAM, tracking) |
| **4. Physics & causality** | Physical-law adherence, counterfactuals | Physics-law scores, Physics-IQ, counterfactual sensitivity | VLM-as-judge + human |
| **5. Functional / closed-loop** | Real task usefulness | Task success rate, SPL, policy-eval correlation, OOD generalization | Closed-loop rollout |

Scoring comes in three flavors that strong benchmarks **validate against humans**: *automatic* (specialist models), *VLM-as-judge* (GPT-4o / Gemini / fine-tuned Qwen-VL), and *human study*.

---

## 🆕 2026 Papers at a Glance

A chronological index of 2026 entries; full descriptions and modality live in [Benchmarks by Modality](#benchmarks-by-modality).

| Paper | Date |
|---|---|
| [Wow, wo, val!](https://arxiv.org/abs/2601.04137) | Jan 2026 |
| [A Mechanistic View on Video Generation as World Models](https://arxiv.org/abs/2601.17067) | Jan 2026 |
| [DrivingGen](https://arxiv.org/abs/2601.01528) | ICLR 2026 (Jan) |
| [PhysicsMind](https://arxiv.org/abs/2601.16007) | Jan 2026 |
| [WorldBench](https://arxiv.org/abs/2601.21282) | Jan 2026 |
| [MIND](https://arxiv.org/abs/2602.08025) | Feb 2026 |
| [WorldArena](https://arxiv.org/abs/2602.08971) | Feb 2026 |
| [VisPhyWorld](https://arxiv.org/abs/2602.13294) | Feb 2026 |
| [The Trinity of Consistency (CoW-Bench)](https://arxiv.org/abs/2602.23152) | Feb 2026 |
| [Out of Sight, Out of Mind? (STEVO-Bench)](https://arxiv.org/abs/2603.13215) | Mar 2026 |
| [Physion-Eval](https://arxiv.org/abs/2603.19607) | Mar 2026 |
| [Omni-WorldBench](https://arxiv.org/abs/2603.22212) | Mar 2026 |
| [World Reasoning Arena](https://arxiv.org/abs/2603.25887) | Mar 2026 |
| [RoboWM-Bench](https://arxiv.org/abs/2604.19092) | Apr 2026 |
| [WorldMark](https://arxiv.org/abs/2604.21686) | Apr 2026 |
| [iWorld-Bench](https://arxiv.org/abs/2605.03941) | ICML 2026 (May) |
| [PhyScore (LoViF 2026)](https://arxiv.org/abs/2605.05187) | CVPR 2026 (ws, May) |
| [WorldReasonBench](https://arxiv.org/abs/2605.10434) | May 2026 |
| [PhyGround](https://arxiv.org/abs/2605.10806) | May 2026 |
| [Geometric-Consistency (PDI-Bench)](https://arxiv.org/abs/2605.15185) | May 2026 |
| [WorldArena 2.0](https://arxiv.org/abs/2605.17912) | May 2026 |
| [PhyWorld](https://arxiv.org/abs/2605.19242) | May 2026 |
| [stable-worldmodel](https://arxiv.org/abs/2605.21800) | May 2026 |
| [WMAttack](https://arxiv.org/abs/2605.23220) | May 2026 |
| [CRONOS](https://arxiv.org/abs/2605.23699) | May 2026 |
| [WBench](https://arxiv.org/abs/2605.25874) | May 2026 |
| [Do LLMs Build World Models From Text? (MentalMap)](https://arxiv.org/abs/2605.28277) | May 2026 |
| [WorldOlympiad](https://arxiv.org/abs/2606.11129) | Jun 2026 |
| [WorldLens](https://arxiv.org/abs/2512.10958) | CVPR 2026 (Oral; arXiv Dec 2025) |

---

## Benchmarks by Modality

> Format: **Name** — "Full title" — badges — *what it evaluates; key metrics.*

### Language & Symbolic

- **Implicit World Models** — "Evaluating the World Model Implicit in a Generative Model" [![arXiv](https://img.shields.io/badge/arXiv-2406.03689-b31b1b.svg)](https://arxiv.org/abs/2406.03689) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/keyonvafa/world-model-evaluation) — *Tests whether a generative model's implicit world model is coherent. Metrics: Myhill–Nerode-based Sequence Compression Precision, Sequence Distinction Precision/Recall.*
- **AutumnBench** — "Benchmarking World-Model Learning with Environment-Level Queries" [![arXiv](https://img.shields.io/badge/arXiv-2510.19788-b31b1b.svg)](https://arxiv.org/abs/2510.19788) — *Environment-level, counterfactual queries in 43 grid-worlds. Metrics: Masked Frame Prediction, Planning (binary success), Change Detection, normalized perplexity; humans ≫ 3 frontier models.*
- **WM-ABench** — "Do Vision-Language Models Have Internal World Models? Towards an Atomic Evaluation" [![arXiv](https://img.shields.io/badge/arXiv-2506.21876-b31b1b.svg)](https://arxiv.org/abs/2506.21876) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://wm-abench.maitrix.org/) — *23 atomic perception/prediction dimensions × 15 VLMs. Metrics: Accuracy, Standardized Relative Entanglement (s-RE).*
- **UNIVERSE** — "Adapting Vision-Language Models for Evaluating World Models" [![arXiv](https://img.shields.io/badge/arXiv-2506.17967-b31b1b.svg)](https://arxiv.org/abs/2506.17967) — *A VLM-based evaluator for action/character recognition. Metrics: Exact Match, ROUGE-F1, Graded Accuracy, Cohen's κ. (NeurIPS LAW 2025, Oral.)*
- **WorldPrediction** — "A Benchmark for High-level World Modeling and Long-horizon Procedural Planning" [![arXiv](https://img.shields.io/badge/arXiv-2506.04363-b31b1b.svg)](https://arxiv.org/abs/2506.04363) — *Discriminative MCQ with counterfactual distractors. Metrics: WP-WM / WP-PP accuracy (best VLM 57% / 38% vs ~100% human).*
- **AeroVerse** — "UAV-Agent Benchmark Suite … Aerospace Embodied World Models" [![arXiv](https://img.shields.io/badge/arXiv-2408.15511-b31b1b.svg)](https://arxiv.org/abs/2408.15511) — *UAV embodied tasks. Metrics: BLEU/CIDEr/SPICE + GPT-4 LLM-judge across scene/reasoning/planning.*
- **Text2World** — "Benchmarking Large Language Models for Symbolic World Model Generation" [![arXiv](https://img.shields.io/badge/arXiv-2502.13092-b31b1b.svg)](https://arxiv.org/abs/2502.13092) — *LLMs synthesize PDDL world models. Metrics: Executability + F1 on predicates/parameters/preconditions/effects.*
- 🆕 **WMAttack** — "Automated Attack Search for Adversarial Evaluation of World-Model Agents" [![arXiv](https://img.shields.io/badge/arXiv-2605.23220-b31b1b.svg)](https://arxiv.org/abs/2605.23220) — *Adversarial robustness of RL world-model agents. Metrics: Normalized Reward Degradation, Action Instability, combined Utility.*
- 🆕 **MentalMap** — "Do LLMs Build World Models From Text? A Multilingual Diagnostic of Spatial Reasoning" [![arXiv](https://img.shields.io/badge/arXiv-2605.28277-b31b1b.svg)](https://arxiv.org/abs/2605.28277) — *6-level (L0–L5) spatial-reasoning hierarchy, 8 languages. Finding: universal "L3 reasoning cliff." Metrics: strict/partial composite, counterfactual graph-F1, hallucination decomposition.*
- **ViSA** — "Probing the Effectiveness of World Models for Spatial Reasoning through Test-time Scaling" [![arXiv](https://img.shields.io/badge/arXiv-2512.05809-b31b1b.svg)](https://arxiv.org/abs/2512.05809) — *Evaluates world-model test-time verifiers (e.g. MindJourney) for VLM spatial reasoning; proposes Verification through Spatial Assertions. Metrics: SAT-Real / MMSI-Bench accuracy, answer-entropy reduction, calibration, evidence quality. (WM Workshop 2026.)*

### Video / Pixel

- **WorldModelBench** — "Judging Video Generation Models As World Models" [![arXiv](https://img.shields.io/badge/arXiv-2502.20694-b31b1b.svg)](https://arxiv.org/abs/2502.20694) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://worldmodelbench-team.github.io/) — *67K human labels + fine-tuned 2B judge. Metrics: Instruction Following (0–3), Physics Adherence (5 laws), Commonsense Quality (0–2).*
- **WorldSimBench** — "Towards Video Generation Models as World Simulators" [![arXiv](https://img.shields.io/badge/arXiv-2410.18072-b31b1b.svg)](https://arxiv.org/abs/2410.18072) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://iranqin.github.io/WorldSimBench.github.io/) — *Dual eval. Metrics: Explicit Perceptual (trained human-preference evaluator) + Implicit Manipulative (closed-loop success on Minecraft/CARLA/CALVIN).*
- **WorldScore** — "A Unified Evaluation Benchmark for World Generation" [![arXiv](https://img.shields.io/badge/arXiv-2504.00983-b31b1b.svg)](https://arxiv.org/abs/2504.00983) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://haoyi-duan.github.io/WorldScore/) — *3,000 examples, 19 models, 10 metrics in controllability/quality/dynamics. (ICCV 2025.)*
- **EWMBench** — "Evaluating Scene, Motion, and Semantic Quality in Embodied World Models" [![arXiv](https://img.shields.io/badge/arXiv-2505.09694-b31b1b.svg)](https://arxiv.org/abs/2505.09694) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/AgibotTech/EWMBench) — *Metrics: Scene Consistency (DINOv2), Hausdorff + nDTW (trajectory), Dynamic Consistency (Wasserstein), VLM-judged semantics.*
- **LoopNav** — "Benchmarking Spatial Consistency in World Models" [![arXiv](https://img.shields.io/badge/arXiv-2505.22976-b31b1b.svg)](https://arxiv.org/abs/2505.22976) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/Kevin-lkw/LoopNav) — *Loop navigation in Minecraft (250h/20M frames). Metrics: FVD, LPIPS, SSIM + qualitative.*
- **EVA** — "An Embodied World Model for Future Video Anticipation" [![arXiv](https://img.shields.io/badge/arXiv-2410.15461-b31b1b.svg)](https://arxiv.org/abs/2410.15461) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://sites.google.com/view/eva-publi) — *EVA-Bench. Composite EVA-Score fusing FVD/consistency + BLEU/CIDEr/SPICE + GPT-4o judge.*
- **Toward Stable World Models** — "Measuring and Addressing World Instability in Generative Environments" [![arXiv](https://img.shields.io/badge/arXiv-2503.08122-b31b1b.svg)](https://arxiv.org/abs/2503.08122) — *Introduces the World Stability (WS) score: consistency after an action and its inverse (LPIPS/MEt3R/DINO).*
- **SVIB** — "Imagine the Unseen World: A Benchmark for Systematic Generalization in Visual World Models" [![arXiv](https://img.shields.io/badge/arXiv-2311.09064-b31b1b.svg)](https://arxiv.org/abs/2311.09064) — *One-step transformation under latent dynamics; atomic/compositional generalization. (NeurIPS 2023.)*
- **World-in-World** — "World Models in a Closed-Loop World" [![arXiv](https://img.shields.io/badge/arXiv-2510.18135-b31b1b.svg)](https://arxiv.org/abs/2510.18135) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/World-In-World/world-in-world) — *Closed-loop, 4 tasks. Key result: Controllability (1−LPIPS) > visual fidelity; first embodied data-scaling laws.*
- 🆕 **WBench** — "A Comprehensive Multi-turn Benchmark for Interactive Video World Model Evaluation" [![arXiv](https://img.shields.io/badge/arXiv-2605.25874-b31b1b.svg)](https://arxiv.org/abs/2605.25874) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://meituan-longcat.github.io/WBench/) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/meituan-longcat/WBench) — *289 cases / 1,058 turns / 20 models; 22 automatic sub-metrics over Quality, Setting, Interaction, Consistency, Physics (human Spearman ≥0.94).*
- 🆕 **CRONOS** — "Benchmarking Counterfactual Physical Consistency in Video Models" [![arXiv](https://img.shields.io/badge/arXiv-2605.23699-b31b1b.svg)](https://arxiv.org/abs/2605.23699) — *Intervenes on viewpoint/scene/appearance/category while fixing the physical event. Metrics: Appearance/Background/3D-Shape Stability, Motion Similarity, Sensitivity to Interventions.*
- 🆕 **MIND** — "Benchmarking Memory Consistency and Action Control in World Models" [![arXiv](https://img.shields.io/badge/arXiv-2602.08025-b31b1b.svg)](https://arxiv.org/abs/2602.08025) — *Closed-loop, 1080p/24fps. Metrics: Long-Context Memory Consistency (MSE), forward-reverse Scene Consistency, RPE action accuracy, action-space generalization.*
- 🆕 **Omni-WorldBench** — "Towards a Comprehensive Interaction-Centric Evaluation for World Models" [![arXiv](https://img.shields.io/badge/arXiv-2603.22212-b31b1b.svg)](https://arxiv.org/abs/2603.22212) — *18 models. Metrics: InterStab-L/N, InterCov, InterOrder + agentic VLM AgenticScore.*
- 🆕 **World Reasoning Arena** [![arXiv](https://img.shields.io/badge/arXiv-2603.25887-b31b1b.svg)](https://arxiv.org/abs/2603.25887) — *Action-simulation fidelity + long-horizon forecasting + simulative reasoning/planning. No model >65% on long-horizon.*
- 🆕 **STEVO-Bench** — "Out of Sight, Out of Mind? Evaluating State Evolution in Video World Models" [![arXiv](https://img.shields.io/badge/arXiv-2603.13215-b31b1b.svg)](https://arxiv.org/abs/2603.13215) — *State evolution under occlusion/camera-lookaway; 225 tasks, 10 models. Five Gemini-3.1-Pro VLM verifiers; <10% success when unobserved.*
- 🆕 **WorldMark** — "A Unified Benchmark Suite for Interactive Video World Models" [![arXiv](https://img.shields.io/badge/arXiv-2604.21686-b31b1b.svg)](https://arxiv.org/abs/2604.21686) — *Unified action-mapping across 6 interactive models. Metrics: Visual Quality (LAION/MUSIQ), Control Alignment (DROID-SLAM translation/rotation/reprojection), World Consistency (VLM-judge).*
- 🆕 **PDI-Bench** — "Quantitative Video World Model Evaluation for Geometric-Consistency" [![arXiv](https://img.shields.io/badge/arXiv-2605.15185-b31b1b.svg)](https://arxiv.org/abs/2605.15185) — *Lifts tracked points to 3D and computes projective-geometry residuals: scale-depth alignment, 3D-motion consistency, structural rigidity.*
- 🆕 **The Trinity of Consistency (CoW-Bench)** — "A Defining Principle for General World Models" [![arXiv](https://img.shields.io/badge/arXiv-2602.23152-b31b1b.svg)](https://arxiv.org/abs/2602.23152) — *Posits Modal × Spatial × Temporal consistency; unified protocol over video and unified multimodal models.*
- 🆕 **A Mechanistic View on Video Generation as World Models** [![arXiv](https://img.shields.io/badge/arXiv-2601.17067-b31b1b.svg)](https://arxiv.org/abs/2601.17067) — *Survey/position. State Construction vs. Dynamics taxonomy; catalogs 17 metrics (WCS, rFID, Physics-IQ, …) and argues for functional benchmarks.*
- 🆕 **iWorld-Bench** — "A Benchmark for Interactive World Models with a Unified Action Generation Framework" [![arXiv](https://img.shields.io/badge/arXiv-2605.03941-b31b1b.svg)](https://arxiv.org/abs/2605.03941) — *14 models, 330K clips. Metrics: MUSIQ image quality, brightness/color/sharpness consistency, trajectory accuracy/tolerance (ViPE), memory symmetry. (ICML 2026.)*
- 🆕 **WorldReasonBench** — "Human-Aligned Stress Testing of Video Generators as Future World-State Predictors" [![arXiv](https://img.shields.io/badge/arXiv-2605.10434-b31b1b.svg)](https://arxiv.org/abs/2605.10434) — *436 QA cases over 4 reasoning dimensions + ~6K expert preference pairs. Metrics: binary QA accuracy, Reasoning Gap, composite ScorePR, human-Elo alignment (Spearman ρ).*
- 🆕 **WorldOlympiad** — "Can Your World Model Survive a Triathlon?" [![arXiv](https://img.shields.io/badge/arXiv-2606.11129-b31b1b.svg)](https://arxiv.org/abs/2606.11129) — *Three tracks across gaming/robotics/real video: Physical (segmentation + MLLM judge), Geometry (Gaussian-splatting 3D consistency), Interaction (action-prompt fidelity).*

### 3D / 4D

- **OmniWorld** — "A Multi-Domain and Multi-Modal Dataset for 4D World Modeling" [![arXiv](https://img.shields.io/badge/arXiv-2509.12201-b31b1b.svg)](https://arxiv.org/abs/2509.12201) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://yangzhou24.github.io/OmniWorld/) — *4D benchmark (96K sequences). Metrics: depth Abs Rel / δ<1.25, camera ATE/RPE, FVD, camera-motion consistency.*
- 🆕 **PhyScore (LoViF 2026 Challenge)** — "The First Challenge on Holistic Quality Assessment for 4D World Model" [![arXiv](https://img.shields.io/badge/arXiv-2605.05187-b31b1b.svg)](https://arxiv.org/abs/2605.05187) — *1,554 videos from 7 generators across text-2D / image-to-4D / video-to-4D. Dimensions: Video Quality, Physical Realism, Condition-Alignment, Temporal Consistency + anomaly localization (TimeStamp-IoU); SRCC/PLCC. (CVPR 2026 workshop.)*
- **4DWorldBench** — "A Comprehensive Evaluation Framework for 3D/4D World Generation Models" [![arXiv](https://img.shields.io/badge/arXiv-2511.19836-b31b1b.svg)](https://arxiv.org/abs/2511.19836) — *Unified eval across image-/video-/text-to-3D/4D. Four dimensions: Perceptual Quality, Condition-4D Alignment, Physical Realism, 4D Consistency — via LLM/MLLM-as-judge + traditional metrics + human study. (Nov 2025.)*
- *See also [WorldScore](#video--pixel) (3D/4D scene generation).*

### Driving

- **ACT-Bench** — "Towards Action Controllable World Models for Autonomous Driving" [![arXiv](https://img.shields.io/badge/arXiv-2412.05337-b31b1b.svg)](https://arxiv.org/abs/2412.05337) — *Action-instruction fidelity. Metrics: Instruction-Execution Consistency, ADE, FDE.*
- **Beyond Simulation** — "Benchmarking World Models for Planning and Causality in Autonomous Driving" [![arXiv](https://img.shields.io/badge/arXiv-2508.01922-b31b1b.svg)](https://arxiv.org/abs/2508.01922) — *Tests whether sim-agent metrics hold when world models are training environments. Metrics: NLL (9 dims), Realism Score, Delta Metametric, Confusion Rate. (ICRA 2025.)*
- **SimWorld** — "A Unified Benchmark for Simulator-Conditioned Scene Generation via World Model" [![arXiv](https://img.shields.io/badge/arXiv-2503.13952-b31b1b.svg)](https://arxiv.org/abs/2503.13952) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/Li-Zn-H/SimWorld) — *Generative quality + downstream utility. Metrics: FID, Pixel Diversity, detection mAP, segmentation mIoU.*
- 🆕 **WorldLens** — "Full-Spectrum Evaluations of Driving World Models in Real World" [![arXiv](https://img.shields.io/badge/arXiv-2512.10958-b31b1b.svg)](https://arxiv.org/abs/2512.10958) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://worldbench.github.io/worldlens) — *24 metrics across Generation / Reconstruction / Action-Following / Downstream / Human; visual realism vs. physics is a fundamental trade-off. (CVPR 2026, Oral.)*
- 🆕 **DrivingGen** — "A Comprehensive Benchmark for Generative Video World Models in Autonomous Driving" [![arXiv](https://img.shields.io/badge/arXiv-2601.01528-b31b1b.svg)](https://arxiv.org/abs/2601.01528) — *14 models. Metrics: FVD, Fréchet Trajectory Distance, CLIP-IQA+, trajectory comfort/curvature, agent-appearance consistency (YOLOv10+SAM2), Cosmos-Reason1 VLM judge. (ICLR 2026.)*

### Embodied & Policy Evaluation

- **WorldGym** — "World Model as An Environment for Policy Evaluation" [![arXiv](https://img.shields.io/badge/arXiv-2506.00613-b31b1b.svg)](https://arxiv.org/abs/2506.00613) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://world-model-eval.github.io) — *Evaluate robot policies inside a video world model via Monte-Carlo rollouts + GPT-4o reward. Metrics: MSE/SSIM/LPIPS, policy-ranking preservation, success-rate agreement.*
- **WorldEval** — "World Model as Real-World Robot Policies Evaluator" [![arXiv](https://img.shields.io/badge/arXiv-2505.19017-b31b1b.svg)](https://arxiv.org/abs/2505.19017) [![Website](https://img.shields.io/badge/Website-Link-blue)](https://worldeval.github.io) — *Policy2Vec turns video models into policy evaluators. Metrics: Pearson r (0.887–0.980), MMRV, FID.*
- 🆕 **stable-worldmodel** — "A Platform for Reproducible World Modeling Research and Evaluation" [![arXiv](https://img.shields.io/badge/arXiv-2605.21800-b31b1b.svg)](https://arxiv.org/abs/2605.21800) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/galilai-group/stable-worldmodel) — *Controllable visual/geometric/physical factors. Finding: prediction error does NOT correlate with success rate. Metrics: SR, Prediction MSE, OOD generalization.*
- 🆕 **Wow, wo, val!** — "A Comprehensive Embodied World Model Evaluation Turing Test" [![arXiv](https://img.shields.io/badge/arXiv-2601.04137-b31b1b.svg)](https://arxiv.org/abs/2601.04137) — *609 manipulation scenarios; 22 metrics + real-robot Inverse-Dynamics "Turing test." Human corr. >0.93.*
- 🆕 **WorldArena** — "A Unified Benchmark for Evaluating Perception and Functional Utility of Embodied World Models" [![arXiv](https://img.shields.io/badge/arXiv-2602.08971-b31b1b.svg)](https://arxiv.org/abs/2602.08971) — *16 perception + 3 functional metrics (data-engine / policy-evaluator / action-planner). EWMScore (r=0.825 to humans). Strong perception-functionality gap.*
- 🆕 **RoboWM-Bench** — "A Benchmark for Evaluating World Models in Robotic Manipulation" [![arXiv](https://img.shields.io/badge/arXiv-2604.19092-b31b1b.svg)](https://arxiv.org/abs/2604.19092) — *Converts generated videos into executable actions validated in simulation. Metrics: task/step-level executability, real-to-sim consistency.*
- 🆕 **WorldArena 2.0** — "Extending Embodied World Model Benchmarking on Modality, Functionality and Platform" [![arXiv](https://img.shields.io/badge/arXiv-2605.17912-b31b1b.svg)](https://arxiv.org/abs/2605.17912) — *Extends [WorldArena](#embodied--policy-evaluation) to visuotactile perception, interactive-RL environments, and real robots; 22 metrics incl. tactile PSNR/SSIM, JEPA similarity, closed-loop task/policy success.*
- *See also [EWMBench](#video--pixel) (embodied scene/motion/semantic).*

### Physics-Centric

- **VideoPhy-2** — "A Challenging Action-Centric Physical Commonsense Evaluation in Video Generation" [![arXiv](https://img.shields.io/badge/arXiv-2503.06800-b31b1b.svg)](https://arxiv.org/abs/2503.06800) — *3,940 prompts / 102K human labels + VideoPhy-AutoEval (7B). Metrics: Semantic Adherence, Physical Commonsense, Physical Rules, Joint (best 22% on hard).*
- 🆕 **PhyWorld** — "Physics-Faithful World Model for Video Generation" [![arXiv](https://img.shields.io/badge/arXiv-2605.19242-b31b1b.svg)](https://arxiv.org/abs/2605.19242) — *Physics-faithfulness benchmark over 7 event classes / 13 physics laws, scored by a fine-tuned Qwen3.5-9B judge; + VBench quality.*
- **PhyWorldBench** — "A Comprehensive Evaluation of Physical Realism in Text-to-Video Models" [![arXiv](https://img.shields.io/badge/arXiv-2507.13428-b31b1b.svg)](https://arxiv.org/abs/2507.13428) — *12 models / 1,050 prompts with an Anti-Physics category. Metrics: Semantic Adherence, Physical Commonsense, Context-Aware-Prompt (ROC-AUC). (ICLR 2026, Oral.)*
- **ScenePhys** — "Controllable Physics Videos for World-Model Evaluation" [![Workshop](https://img.shields.io/badge/NeurIPS_2025-EWM-purple)](https://neurips.cc/virtual/2025/loc/san-diego/123993) — *382 PhET-simulation clips, 1,146 expert Q/A. Metrics: deterministic numerical grading + rubricized dual-judge LLM scoring.*
- **Newton** — "A Small Benchmark for Interactive Foundation World Models" [![OpenReview](https://img.shields.io/badge/OpenReview-ICLR'25_WM-8c1b13)](https://openreview.net/forum?id=xlp6P6qaRW) — *Newton-OP (object permanence) + Newton-Physics (rigid-body interaction). Metrics: Object Permanence, Action Following, Physical Accuracy.*
- **Morpheus** — "Benchmarking Physical Reasoning of Video Generative Models with Real Physical Experiments" [![arXiv](https://img.shields.io/badge/arXiv-2504.02918-b31b1b.svg)](https://arxiv.org/abs/2504.02918) — *80 real-world videos of phenomena governed by conservation laws; fits the system's ODE and extracts physical measurements (velocity, acceleration). Metrics: conformance of generated dynamics to physical invariants (momentum/energy).*
- **Physics-IQ** — "Do generative video models understand physical principles?" [![arXiv](https://img.shields.io/badge/arXiv-2501.09038-b31b1b.svg)](https://arxiv.org/abs/2501.09038) — *Real test set spanning solid mechanics, fluids, optics, thermodynamics, magnetism; models predict the continuation of a physical event. Metric: composite Physics-IQ score (Spatial IoU, Spatiotemporal IoU, location + MSE) vs. real footage. Finding: physical understanding is largely uncorrelated with visual realism.*
- **PhysBench** — "Benchmarking and Enhancing Vision-Language Models for Physical World Understanding" [![arXiv](https://img.shields.io/badge/arXiv-2501.16411-b31b1b.svg)](https://arxiv.org/abs/2501.16411) — *10,002 interleaved video-image-text entries across 4 physical-understanding domains; also proposes the PhysAgent framework. Metric: VQA accuracy. (ICLR 2025.)*
- **PhyGenBench** — "Towards World Simulator: Crafting Physical Commonsense-Based Benchmark for Video Generation" [![arXiv](https://img.shields.io/badge/arXiv-2410.05363-b31b1b.svg)](https://arxiv.org/abs/2410.05363) — *160 prompts across 27 physical laws / 4 domains for text-to-video. Introduces PhyGenEval, a hierarchical VLM+LLM judge of physical commonsense.*
- 🆕 **Physion-Eval** — "Evaluating Physical Realism in Generated Video via Human Reasoning" [![arXiv](https://img.shields.io/badge/arXiv-2603.19607-b31b1b.svg)](https://arxiv.org/abs/2603.19607) — *10,990 expert reasoning traces over 5 generators (ego + exo views, each paired with a real reference). Metrics: temporal localization of glitches, 22 fine-grained failure categories, NL explanations; 83–94% of generated videos show ≥1 physical glitch.*
- 🆕 **PhyGround** — "Benchmarking Physical Reasoning in Generative World Models" [![arXiv](https://img.shields.io/badge/arXiv-2605.10806-b31b1b.svg)](https://arxiv.org/abs/2605.10806) — *250 prompts / 13 physical laws (mechanics, fluids, optics); 459 annotators + PhyJudge-9B judge. Metrics: per-law Likert physics scores, semantic alignment, temporal validity, persistence; no model >3.3/5.*
- 🆕 **VisPhyWorld** — "Probing Physical Reasoning via Code-Driven Video Reconstruction" [![arXiv](https://img.shields.io/badge/arXiv-2602.13294-b31b1b.svg)](https://arxiv.org/abs/2602.13294) — *Execution-based: MLLMs generate Python simulator code from video (VisPhyBench, 209 scenes / 108 templates). Metrics: reconstruction PSNR/SSIM/LPIPS + Physical-Parameter MAE (gravity/restitution/friction); gravity recovery ≈ 0 for all models.*
- 🆕 **WorldBench** — "Disambiguating Physics for Diagnostic Evaluation of World Models" [![arXiv](https://img.shields.io/badge/arXiv-2601.21282-b31b1b.svg)](https://arxiv.org/abs/2601.21282) — *Concept-disentangled physics diagnostics. Metrics: foreground mIoU (SAM2), background RMSE, automatic gravity/viscosity/friction parameter estimation.*
- 🆕 **PhysicsMind** — "Sim and Real Mechanics Benchmarking for Physical Reasoning and Prediction in Foundational VLMs and World Models" [![arXiv](https://img.shields.io/badge/arXiv-2601.16007-b31b1b.svg)](https://arxiv.org/abs/2601.16007) — *22 VLMs + 7 video/world models on Center-of-Mass, Lever Equilibrium, Newton's First Law (sim + real). Metrics: VQA accuracy, mask IoU/centroid, trajectory RMSE, speed/accel similarity.*

### Other / Workshop

- **OpenGVL** — "Benchmarking Visual Temporal Progress for Data Curation" [![arXiv](https://img.shields.io/badge/arXiv-2509.17321-b31b1b.svg)](https://arxiv.org/abs/2509.17321) [![Code](https://img.shields.io/badge/Code-GitHub-green)](https://github.com/budzianowski/opengvl) — *VLM temporal task-progress prediction for robot data curation. Metric: Value-Order Correlation (VOC). (CoRL 2025 workshop.)*
- **AetherVision-Bench** — "An Open-Vocabulary RGB-Infrared Benchmark for Multi-Angle Segmentation" [![arXiv](https://img.shields.io/badge/arXiv-2506.03709-b31b1b.svg)](https://arxiv.org/abs/2506.03709) — ⚠️ *Open-vocabulary **segmentation** benchmark (metric: mIoU); included because it appears in source world-model lists, but it is only tangential to world-model evaluation.*

---

## Metric Reference Tables

### Common metrics

General-purpose metrics reused across the benchmarks above, each with the paper that originally **defined** it and example users from this list.

| Metric | Measures | Defining paper | Used by (examples) |
|---|---|---|---|
| **FID** — Fréchet Inception Distance | Image-set distributional realism | [![arXiv](https://img.shields.io/badge/arXiv-1706.08500-b31b1b.svg)](https://arxiv.org/abs/1706.08500) | perceptual baseline; SimWorld, WorldEval |
| **IS** — Inception Score | Sample quality & diversity | [![arXiv](https://img.shields.io/badge/arXiv-1606.03498-b31b1b.svg)](https://arxiv.org/abs/1606.03498) | perceptual baseline |
| **FVD** — Fréchet Video Distance | Clip-level distributional realism | [![arXiv](https://img.shields.io/badge/arXiv-1812.01717-b31b1b.svg)](https://arxiv.org/abs/1812.01717) | EVA, LoopNav, OmniWorld, DrivingGen |
| **FVMD** — Fréchet Video Motion Distance | Motion / temporal consistency | [![arXiv](https://img.shields.io/badge/arXiv-2407.16124-b31b1b.svg)](https://arxiv.org/abs/2407.16124) | motion-consistency evaluation |
| **LPIPS** — Learned Perceptual Image Patch Similarity | Perceptual frame similarity | [![arXiv](https://img.shields.io/badge/arXiv-1801.03924-b31b1b.svg)](https://arxiv.org/abs/1801.03924) | World Stability, WorldGym, MIND |
| **SSIM** — Structural Similarity | Structural frame similarity | [![DOI](https://img.shields.io/badge/DOI-10.1109%2FTIP.2003.819861-blue.svg)](https://doi.org/10.1109/TIP.2003.819861) | WorldGym, LoopNav, MIND |
| **PSNR** — Peak Signal-to-Noise Ratio | Pixel-level fidelity | Classical (no canonical paper) | WorldGym, WorldArena 2.0 |
| **CLIP** — CLIP-based similarity | Image–text / feature alignment | [![arXiv](https://img.shields.io/badge/arXiv-2103.00020-b31b1b.svg)](https://arxiv.org/abs/2103.00020) | CLIP-consistency: EWMBench, CRONOS |
| **CLIPScore** | Reference-free text–image alignment | [![arXiv](https://img.shields.io/badge/arXiv-2104.08718-b31b1b.svg)](https://arxiv.org/abs/2104.08718) | caption / prompt alignment |
| **DINO / DINOv2 consistency** | Subject & background temporal stability | [![arXiv](https://img.shields.io/badge/arXiv-2304.07193-b31b1b.svg)](https://arxiv.org/abs/2304.07193) | EWMBench, CRONOS, WorldArena, WBench |
| **VBench** | Multi-axis perceptual quality | [![arXiv](https://img.shields.io/badge/arXiv-2311.17982-b31b1b.svg)](https://arxiv.org/abs/2311.17982) | WorldModelBench, PhyWorld, Omni-WorldBench |
| **VBench++** | Extended T2V / I2V perceptual quality | [![arXiv](https://img.shields.io/badge/arXiv-2411.13503-b31b1b.svg)](https://arxiv.org/abs/2411.13503) | perceptual-quality suite |
| **Camera-pose error (ATE / RPE)** | Action / camera controllability | SLAM-based (no single paper) | OmniWorld, MIND, WorldMark, WBench |
| **Reprojection / geometric residuals** | 3D structural coherence | Geometry-based (no single paper) | PDI-Bench, WorldScore, WBench, WorldLens |

### VLM-as-judge & human-validated metrics

| Approach | Example metric | Papers |
|---|---|---|
| Fine-tuned VLM judge | Physics-faithfulness, physical-rule scores | WorldModelBench, VideoPhy-2, PhyWorld, WBench |
| Frontier-VLM verifier | State-progress / plausibility / coherence | STEVO-Bench (Gemini-3.1-Pro), CRONOS, WorldArena |
| Human study (validated) | Spearman/Pearson alignment | WBench (≥0.94), Wow, wo, val! (>0.93), WorldMark (>0.9), WorldArena (0.825) |

### Functional / closed-loop metrics

| Metric | Measures | Papers |
|---|---|---|
| **Task Success Rate / SPL** | Real task completion | World-in-World, WorldSimBench, RoboWM-Bench |
| **Policy-eval correlation** | World model as policy evaluator | WorldGym, WorldEval, WorldArena |
| **OOD generalization** | Robustness to distribution shift | stable-worldmodel, WM-ABench |
| **IDM Turing test** | Predicted frames → real robot actions | Wow, wo, val! |

---

## Contributing

Contributions welcome! Please open a PR that adds an entry in this format:

```markdown
- **ShortName** — "Full Paper Title" [![arXiv](https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b.svg)](https://arxiv.org/abs/XXXX.XXXXX) [![Code](https://img.shields.io/badge/Code-GitHub-green)](LINK) — *one line: what it evaluates; key metrics.*
```