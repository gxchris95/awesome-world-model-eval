# Metrics — Quick Reference

> One line per metric for every benchmark in [`README.md`](./README.md#benchmarks-by-modality). Full computation + worked examples in [`METRICS.md`](./METRICS.md). Benchmarks here are grouped by **domain/modality**; for the metric *taxonomy* (the five evaluation dimensions × scoring methods) see the [README](./README.md#evaluation-dimensions).

> Metrics are **ranked by importance**: ⭐ **Primary** (the headline metric the benchmark is judged on) · ● **Secondary** (important supporting) · ○ **Supporting** (auxiliary / diagnostic / reliability). Citation counts via Semantic Scholar (snapshot 2026-06).

_63 benchmarks · 564 metrics._

## Contents

- [Language & Symbolic](#language-symbolic)
- [Video / Pixel](#video-pixel)
- [3D / 4D](#3d-4d)
- [Driving](#driving)
- [Embodied & Policy Evaluation](#embodied-policy-evaluation)
- [Physics-Centric](#physics-centric)
- [Other / Workshop](#other-workshop)

---

## Language & Symbolic

**[Implicit World Models](https://arxiv.org/abs/2406.03689)** · 📑 117 — The paper proposes that neural networks can learn implicit world models by learning to recognize when sequences lead to equivalent states (compression) and when they lead to different states (distinction), measured through Myhill-Nerode boundary analysis rather than task accuracy alone.
- ⭐ **Sequence Compression Precision** — Whether a model recognizes that multiple distinct sequences arriving at the same world state should permit identical continuations.
- ⭐ **Sequence Distinction Precision** — Whether a model correctly identifies sequences leading to different DFA states as requiring distinct continuations.
- ⭐ **Sequence Distinction Recall** — What fraction of true distinguishing sequences (Myhill-Nerode boundary) the model actually identifies.
- ● **Next-Token Test Accuracy** — Percentage of greedy-decoded predictions that represent valid next tokens under the true world model.
- ● **Current-State Probe Accuracy** — How well a linear classifier can predict the current DFA state from the model's learned representations, measuring whether the model's hidden layers encode state information.
- ● **Distinction Recall (Logic Puzzles Domain)** — On logic puzzles, fraction of true minimal distinguishing sequences (Myhill-Nerode boundaries separating different valid states) that the model identifies.
- ● **Compression Precision (Logic Puzzles Domain)** — On logic puzzle constraint satisfaction, whether the model recognizes that different permutations of partial assignments that are logically equivalent should yield identical continuations.
- ● **Compression Precision (Othello Domain)** — On Othello game playing, whether the model recognizes board positions that should yield identical game continuations (compression of equivalent game states).
- ● **Task Accuracy (Logic Puzzles Domain)** — Fraction of seating arrangement logic puzzles solved correctly, measured as identifying the correct full arrangement that satisfies all constraints.
- ○ **Route Planning Accuracy (Maps Domain)** — Fraction of greedy-decoded traversals between test origin-destination pairs that match true shortest paths in the underlying graph.
- ○ **Valid Traversal Rate (Maps Domain)** — Fraction of greedy-decoded sequences that represent topologically valid paths in the true street network (no impossible transitions).
- ○ **Detour Robustness (Random & Adversarial)** — Whether models maintain valid traversals when path sequences are perturbed by random or adversarial token substitutions at varying corruption rates, testing robustness of internal world understanding.

**[AutumnBench](https://arxiv.org/abs/2510.19788)** · 📑 2 — AutumnBench evaluates whether AI agents can learn world models that support environment-level reasoning by assessing their performance across three task families (masked frame prediction, planning, change detection) in grid-world environments, using both automatic task success metrics and behavioral metrics that measure the quality of exploration and learning trajectories.
- ⭐ **Masked Frame Prediction (MFP) Accuracy** — Agent's ability to predict unobserved regions in grid frames after observing a partial trajectory.
- ⭐ **Planning Task Success** — Agent's ability to generate action sequences that reach a specified goal state.
- ● **Change Detection (CD) Accuracy** — Agent's ability to detect when environment dynamics have deviated from previously learned rules.
- ● **Normalized Perplexity** — Action predictability and behavioral focus during exploration.
- ● **Area Under Curve (AUC) of Normalized Perplexity** — Overall learning trajectory quality.
- ○ **Final Normalized Perplexity** — Degree of behavioral focus and targeting at the conclusion of exploration.
- ○ **Human Baseline (80th Percentile Aggregate Score)** — Representative human performance on benchmark tasks, computed as the 80th percentile of individual task scores across 20 independent human attempts.
- ○ **Action Category Distribution** — Composition of agent exploration strategies, capturing the proportion of unique actions across categories (clicks, directional inputs, resets, no-ops).

**[WM-ABench](https://arxiv.org/abs/2506.21876)** · 📑 28 — WM-ABench measures whether vision-language models possess human-like world models by evaluating perception and prediction across controlled simulated environments with 23 fine-grained dimensions.
- ⭐ **Accuracy (Perception & Prediction)** — Correctness of model outputs on individual tasks.
- ⭐ **Standardized Relative Entanglement (s-RE)** — Degree to which a model's internal representations incorrectly couple orthogonal world attributes.
- ● **Per-Dimension Accuracy (23 Dimensions)** — Task-specific accuracy for each of the 23 fine-grained evaluation dimensions (e.g., spatial positioning, motion direction, discrete quantity, collision prediction, transitive inference).
- ● **Task-Category Accuracy (Perception vs. Prediction)** — Separates and compares performance on perception tasks (visual recognition, spatial/temporal/quantitative understanding) versus prediction tasks (mechanistic simulation, transitive/compositional inference).
- ○ **Fleiss' Kappa (κ) for Human Agreement** — Inter-rater reliability of human annotators on benchmark tasks.
- ○ **Environment-Specific Accuracy** — Model performance within each of the 6 simulated environments (ThreeDWorld, ManiSkill, Habitat, Physion, CARLA, Real-world), revealing whether limitations are environment-dependent or systematic across domains.

**[UNIVERSE](https://arxiv.org/abs/2506.17967)** · 📑 2 — UNIVERSE evaluates video world models by using a vision-language model as a judge to assess whether generated video rollouts correctly represent agent actions and maintain character consistency over time.
- ⭐ **Action Recognition (AR) Accuracy** — Proportion of video sequences where UNIVERSE correctly identifies or describes the agent's action(s) at each timestep, across three question formats (binary yes/no, multiple-choice with 4 options, open-ended description).
- ⭐ **Character Recognition (CR) Accuracy** — Proportion of timestep-pairs where UNIVERSE correctly assesses semantic consistency and identity of entities (characters, objects) across temporal sequences in video rollouts, across the same three question formats.
- ● **Cross-Environment Generalization (AR Accuracy Spread)** — Range and consistency of Action Recognition accuracy across seven diverse visual environments, assessing whether UNIVERSE generalizes beyond the training environment or degrades on unseen settings.
- ● **Graded Accuracy (Ordinal Four-Point Scale)** — Human judgments of prediction quality across four categorical levels: Correct (full credit), Partially Correct (some understanding but incomplete/flawed), Incorrect (fundamentally wrong), and Unclear (indecipherable response).
- ● **ROUGE-F1 (ROUGE)** — Semantic similarity between predicted and reference answers by computing overlap of word n-grams, capturing both lexical matching and semantic alignment beyond exact string matches.
- ● **Exact Match (EM)** — Binary assessment of whether a predicted text answer (e.g., description of an action or character property) precisely matches the reference ground-truth answer, character-for-character.
- ○ **Cohen's Kappa (κ) Inter-Annotator Agreement** — Statistical reliability of agreement between two independent human raters assigning ordinal grades, accounting for chance agreement.
- ○ **Parameter Efficiency Ratio** — Proportion of the total VLM's trainable parameters that UNIVERSE updates during fine-tuning, reflecting computational and memory efficiency of the adaptation approach.
- ○ **Sample Efficiency (Few-Shot Convergence)** — Performance achieved with a minimal subset of training samples, demonstrating how quickly UNIVERSE learns from limited data, reported as accuracy reached after processing a small fraction of training data.

**[WorldPrediction](https://arxiv.org/abs/2506.04363)** · 📑 12 — The benchmark evaluates whether frontier AI models can perform high-level semantic action understanding and procedural reasoning in video.
- ⭐ **Accuracy (WorldPrediction-WM)** — Percentage of correct action selections: given an initial video frame, final video frame, and a set of candidate actions (one correct, others distractors), the model must identify which single action would causally produce the state transition from initial to final.
- ⭐ **Accuracy (WorldPrediction-PP)** — Percentage of correctly ordered action sequence selections: given an initial frame and final frame spanning multiple actions, the model must identify the proper temporal order of a sequence of actions (e.g., [Grasp, Lift, Place]) from distractor sequences that violate causal order or include wrong actions.
- ● **Inter-Annotator Agreement (IAA)** — Consistency metric quantifying human disagreement: proportion of test samples where two independent human annotators selected identical correct answers, establishing ceiling performance for the benchmark itself.
- ○ **Parseability Rate** — Percentage of model outputs that are successfully formatted and parseable as valid action or sequence selections (versus malformed, gibberish, or unparseable responses).
- ○ **Feature Distance (Observability Filtering)** — Euclidean distance in embedding space between initial and final state observations, used to filter out samples where visual changes are so extreme that causal action inference becomes ambiguous or ill-defined.

**[AeroVerse](https://arxiv.org/abs/2408.15511)** · 📑 26 — AeroVerse evaluates aerial embodied AI systems across five downstream tasks (scene awareness, spatial reasoning, navigation, planning, motion decision) using both traditional reference-based metrics and modern GPT-4-based task-specific judges to assess UAV-agent visual-language models.
- ⭐ **LLM-Judge-Scene** — Multi-perspective scene awareness: description granularity (detail level of objects, spatial relationships, attributes) and directional accuracy (correctness of object locations relative to specified viewpoint/direction).
- ⭐ **LLM-Judge-Reason&Nav (Reasoning and Navigation)** — Spatial reasoning: correlation between model reasoning and reference answers.
- ⭐ **LLM-Judge-Nav (Navigation Exploration)** — Navigational path quality: description coherence of explored route, relevance of landmark observations, correctness of directional transitions during exploration.
- ⭐ **LLM-Judge-Plan (Path Planning)** — Two components: (1) key action sequence alignment.
- ● **SPICE (Semantic Propositional Image Caption Evaluation)** — Scene graph semantic content: objects present, attributes (color, size), and relationships (spatial, action).
- ● **CIDEr (Consensus-based Image Description Evaluation)** — Semantic consistency: treats each description as a document and measures how well the model's description aligns with reference descriptions using TF-IDF weighted n-gram similarity.
- ○ **BLEU (Bilingual Evaluation Understudy)** — N-gram overlap between model-generated descriptions and reference descriptions.

**[Text2World](https://arxiv.org/abs/2502.13092)** · 📑 23 — Text2World measures the quality of AI-generated PDDL (planning) domain models from natural language descriptions by evaluating whether models are syntactically valid, structurally similar to ground truth, and correctly specify planning components (predicates, parameters, preconditions, effects).
- ⭐ **Executability (Exec.)** — Whether the generated PDDL domain file can be successfully parsed and validated without syntax errors by standard PDDL validators, indicating basic syntactic correctness.
- ⭐ **F1precond (Precondition F1)** — Precision and recall of action preconditions.
- ⭐ **F1eff (Effect F1)** — Precision and recall of action effects.
- ● **F1pred (Predicate F1)** — Precision and recall of correctly identified predicates (e.g., 'on', 'clear', 'holding') by comparing sets of predicates in generated vs.
- ● **F1param (Parameter F1)** — Precision and recall of correctly specified parameters in PDDL action/predicate signatures (e.g., 'block1', 'block2', and their types).
- ○ **Structural Similarity (Sim.)** — Character-level textual similarity between the generated PDDL and the ground-truth reference PDDL, quantifying how closely the output matches the expected domain specification.

**[WMAttack](https://arxiv.org/abs/2605.23220)** · 📑 1 — Automated search framework for finding adversarial attacks against reinforcement learning agents with learned world models, balancing attack effectiveness, action perturbations, and computational cost.
- ⭐ **Normalized Reward Degradation (D_τ)** — How severely the discovered attack reduces the agent's episodic return compared to clean execution.
- ⭐ **Scalarized Utility Function (U_τ)** — Combined score balancing attack strength (reward degradation + action changes) against computational cost and reliability, enabling single-objective optimization over the attack space.
- ● **Action Instability (F_τ)** — How often the adversarial perturbations cause the agent to change its decision.
- ● **Hit Rate (% reaching 90% of final utility)** — Search efficiency: percentage of task-attack pairs where the algorithm discovers a configuration achieving at least 90% of the best utility found within the evaluation budget, indicating convergence reliability.
- ● **Best-So-Far Utility (convergence tracking)** — Progressive quality of the best attack found up to any evaluation step, showing whether the search algorithm steadily improves or stagnates early.
- ○ **Runtime Cost (T_τ)** — Wall-clock time required to evaluate a candidate attack configuration, penalizing computationally expensive attacks through logarithmic scaling to avoid wasting budget on slow perturbations.
- ○ **Rollout Variability (V_τ)** — Consistency of attack effects across multiple evaluation runs.

**[MentalMap](https://arxiv.org/abs/2605.28277)** · 📑 0 — This benchmark measures whether language models can build coherent world models of spatial environments through multi-level reasoning tasks, from atomic spatial facts to generative graph construction, revealing a "reasoning cliff" where performance collapses as complexity increases.
- ⭐ **Strict Composite (L0–L4 Unweighted Macro-Average)** — Overall model performance across difficulty levels L0 through L4, computed as the unweighted macro-average of task-level pass rates.
- ⭐ **L3/L0 Ratio (Reasoning Cliff Diagnostic)** — The degree to which a model's performance degradation on viewpoint-reasoning tasks (L3) compares to its atomic-fact accuracy (L0).
- ⭐ **Pass Rate (L0–L4)** — Binary correctness of model outputs after canonical normalization at each difficulty level, from atomic spatial facts (L0) through viewpoint reasoning (L3) to action-state transitions (L4).
- ● **Graph F1 (L5) — Node and Edge F1** — Set-based F1 score measuring the harmonic mean of precision and recall on predicted world-graph nodes and containment edges.
- ● **Partial-Credit Composite (L5 Weighted Score)** — Holistic scoring of generative graph construction combining JSON validity, node accuracy, edge accuracy, relation correctness, and task-specific components into a single composite score.
- ● **Event Precision & Recall (L4)** — Precision and recall of the model's predicted action-state transitions against a gold action-state transition log.
- ● **Counterfactual Delta F1 (L5c)** — Graph F1 restricted only to nodes and edges that changed between the before and after states.
- ○ **Hallucination Decomposition (L5)** — Specific failure mode breakdown: hallucinated nodes (entities predicted but not in gold), missing nodes (entities in gold but not predicted), hallucinated edges (spatial relations predicted but not gold), and relation flips (correct entity pair but wrong relation type).
- ○ **Reasoning-Prompt Delta (CoT Effect)** — Percentage-point change in performance when a chain-of-thought (reasoning) prompt is used versus a direct prompt.
- ○ **Language-Specific Pass Rate (Script Groups)** — Pass rates aggregated by linguistic script/typology: Latin (English, Spanish, German), CJK (Chinese, Japanese, Korean), Arabic, Thai.
- ○ **Kendall's Tau (Rank Correlation)** — Stability of model ranking across different difficulty levels and languages.

**[ViSA](https://arxiv.org/abs/2512.05809)** · 📑 0 — The paper measures how well large vision-language models can reason about spatial relationships when augmented with test-time scaling via world-model-generated frames and claim-based verification, using accuracy on spatial reasoning benchmarks combined with evidence quality and confidence metrics.
- ⭐ **Spatial Reasoning Accuracy** — Percentage of correct answers selected by the model on multiple-choice spatial reasoning questions (e.g., ego-motion, object tracking, goal estimation, perspective reasoning).
- ● **Evidence Quality (EQ) Score** — Frame-level score quantifying how well a generated world-model frame provides verifiable evidence for answering a spatial reasoning question.
- ○ **Answer-Level Entropy (Model Confidence / Uncertainty)** — Shannon entropy of the model's predicted probability distribution over answer choices, quantifying prediction confidence and calibration.
- ○ **Claim Verification Verdict Categories** — Classification of each extracted micro-claim into one of three categories: ENTAILED (evidence supports the claim), CONTRADICTED (evidence opposes the claim), or INSUFFICIENT (insufficient evidence to decide).
- ○ **Perceptual Quality (LAION Aesthetic Score)** — Visual fidelity and aesthetic quality of the generated frames from the world model, assessing how photorealistic and clear the synthetic frames are.

---

## Video / Pixel

**[WorldModelBench](https://arxiv.org/abs/2502.20694)** · 📑 78 — WorldModelBench measures how well video generation models adhere to physical laws, follow instructions, and maintain visual quality.
- ⭐ **Combined Grading Score (0–10 points)** — Overall quality of generated video as the sum of instruction following, physics adherence, and visual quality dimensions.
- ⭐ **Instruction Following Score (0–3 points)** — Whether generated video correctly executes the text/image-based instruction.
- ⭐ **Physics Adherence Score (0–5 points)** — Violations of five fundamental physical laws: Newton's First Law (motion without external forces), Conservation of Mass/Solid Mechanics (irregular deformation), Fluid Mechanics (unnatural liquid flow), Impenetrability (objects passing through), and Gravitation (floating objects).
- ● **Commonsense / Visual Quality Score (0–2 points)** — General video generation quality independent of task instruction: frame-wise visual appeal and temporal coherence (flickering, motion smoothness, object persistence).
- ○ **Automatic Judger Prediction Error (≤4.1% mean error)** — How accurately a fine-tuned visual language model (VILA-2B with 2B parameters) predicts human-assigned scores without requiring human raters.

**[WorldSimBench](https://arxiv.org/abs/2410.18072)** · 📑 1116 — WorldSimBench evaluates video generation models' ability to produce realistic embodied interactions across three representative scenarios (open-ended environments, autonomous driving, robot manipulation) by combining human-aligned perception judgments with automatic task-specific success metrics.
- ⭐ **Human Preference Evaluator (HPE) — Open-Ended (OE) Accuracy** — Whether a fine-tuned VideoLLM agrees with human preference judgments on Minecraft video quality, measuring alignment with human perception across visual and embodiment dimensions.
- ⭐ **Human Preference Evaluator (HPE) — Autonomous Driving (AD) Pearson Linear Correlation Coefficient (PLCC)** — How well the HPE's predicted scores correlate with human preference ratings on autonomous driving video quality across multiple rating scenarios on a 1-5 scale.
- ⭐ **Human Preference Evaluator (HPE) — Robot Manipulation (RM) Pearson Linear Correlation Coefficient (PLCC)** — Correlation between HPE-predicted ratings and human judgments on robot manipulation video quality on a 1-5 scale, across seven evaluation dimensions (Aesthetics, Background Consistency, Foreground Consistency, Instruction Alignment, Trajectory, Perspectivity, Embodied Interaction).
- ● **Autonomous Driving (AD) — Route Completion (RC), Driving Score (DS), and Collision Metrics** — Percentage of planned driving route completed, overall quality of driving behavior, and counts of violations (collisions with vehicles/pedestrians/scenery, red-light violations, off-road driving).
- ● **Robot Manipulation (RM) — Success Rate** — Percentage of task completion across 20 trials in a skill composition scenario.
- ● **Open-Ended Environment (OE) — Programmatic Task Metrics (Travel Distance, Dig Depth, Early-Game Inventory)** — Automatic measures of agent progress in Minecraft tasks: maximum displacement from spawn (Travel Distance on X-Z plane), maximum vertical displacement (Dig Depth), and maximum items collected (logs, seeds, dirt count).
- ○ **Multi-Dimensional Human Ratings — Seven Visual & Embodiment Dimensions** — Structured evaluation across specific perceptual and physical plausibility criteria: Aesthetics (composition, color, lighting), Background Consistency, Foreground Consistency, Instruction Alignment, Scenario Alignment, Trajectory (object movement rationality), Perspectivity (3D depth/lighting logic), Velocity, Key Elements, Safety, Embodied Interaction.

**[WorldScore](https://arxiv.org/abs/2504.00983)** · 📑 102 — WorldScore measures the quality, controllability, and realism of AI-generated 3D video sequences by combining automatic metrics (SLAM, optical flow, CLIP) into a unified benchmark across static and dynamic scenes.
- ⭐ **Content Alignment** — How well the entire generated scene matches the full text description.
- ⭐ **Camera Controllability** — How accurately generated camera motion matches a specified trajectory (rotation and translation).
- ⭐ **3D Consistency** — Geometric stability of the 3D scene across frames.
- ⭐ **Object Controllability** — Whether specified objects from the text prompt actually appear in the generated scene.
- ● **Motion Accuracy** — Whether specified motion occurs in the correct spatial regions and not elsewhere.
- ● **Motion Smoothness** — Temporal consistency of motion across frames.
- ● **Photometric Consistency** — Texture and lighting stability across frames.
- ● **Motion Magnitude** — Ability to generate substantial, visible motion.
- ○ **Style Consistency** — Visual style preservation throughout the video.
- ○ **Subjective Quality** — Perceptual visual quality and aesthetic appeal of generated video.

**[EWMBench](https://arxiv.org/abs/2505.09694)** · 📑 26 — EWMBench measures how well embodied video generation models produce videos that are visually consistent, follow realistic motion dynamics, execute multi-step tasks semantically, and maintain diversity across outputs.
- ⭐ **Scene Consistency (SceneC)** — Visual stability of the 3D scene layout across frames.
- ⭐ **Symmetric Hausdorff Distance (HSD)** — Maximum spatial deviation between the generated robot trajectory and the ground-truth trajectory.
- ⭐ **Normalized Dynamic Time Warping (nDTW)** — Temporal and spatial alignment of trajectories accounting for timing variations.
- ⭐ **Dynamic Consistency (DYN)** — Physical realism of motion.
- ● **Global Caption Alignment** — Whether the overall task goal shown in the generated video matches the language instruction.
- ● **Step-Level Semantic Alignment** — Fine-grained task understanding.
- ○ **Logical Error Punishment** — Absence of commonsense violations.
- ○ **Semantic Diversity** — Whether a model can generate multiple plausible variations of the same task rather than producing near-identical videos.

**[LoopNav](https://arxiv.org/abs/2505.22976)** · 📑 4 — The benchmark evaluates video world models' ability to reconstruct previously visited spatial locations during looped navigation trajectories (A→B→A patterns), measuring whether models can maintain consistent spatial geometry and visual coherence over extended rollouts in a Minecraft environment.
- ⭐ **Learned Perceptual Image Patch Similarity (LPIPS)** — Perceptual similarity between individual generated and ground-truth frames, measuring whether objects, layouts, and structural elements appear plausible to a pretrained perceptual network.
- ⭐ **Fréchet Video Distance (FVD)** — Distributional distance between real and generated video features, capturing both spatial and temporal statistics at a high level.
- ● **Structural Similarity Index Measure (SSIM)** — Structural fidelity and luminance similarity between generated and reference frames.

**[EVA](https://arxiv.org/abs/2410.15461)** · 📑 24 — The paper benchmarks embodied video prediction and understanding by combining language understanding metrics with video generation quality metrics to comprehensively assess world models across four tasks: Action-Description, Finish-Thinking, How-To, and Next-Step.
- ⭐ **Task Success Rate on RT-1 (Real-World Robot Tasks)** — Percentage of robot task completions when model-predicted actions/videos are executed.
- ⭐ **Task Success Rate on CALVIN Simulation** — Percentage of complex multi-step tasks completed in simulation.
- ⭐ **EVA-Video-Score (composite video metrics)** — Unified video quality combining Subject Consistency, Background Consistency, Motion Smoothness, Goal Completion Estimation, and Fréchet Video Distance.
- ⭐ **EVA-Score (composite language metric)** — Unified text quality combining BLEU, METEOR, ROUGE-L, CIDEr, SPICE, CLIP, and GPT-4o.
- ● **Goal Completion Estimation (GCE)** — Success of task execution by comparing final frame visual content with ground truth.
- ● **Fréchet Video Distance (FVD)** — Overall video quality and realism.
- ● **Subject Consistency (SC)** — Alignment between the subject/main object in the input image and the subject in generated video.
- ● **Motion Smoothness (MS)** — Physical plausibility of motion.
- ● **Background Consistency (BC)** — Coherence between input background and generated video background.
- ○ **SPICE (Semantic Propositional Image Caption Evaluation)** — Semantic content via scene graph parsing.
- ○ **GPT-4o as Judge** — Semantic understanding of generated text through comprehensive evaluation on four key criteria: object accuracy, action type correctness, location accuracy, and attribute correctness.
- ○ **CIDEr (Consensus-based Image Description Evaluation)** — Image description quality using TF-IDF weighted n-gram similarity.
- ○ **METEOR (Metric for Evaluation of Translation with Explicit Ordering)** — Translation quality beyond exact matches by accounting for stemming, synonyms, word order, precision, recall, and penalties for sentence length.
- ○ **ROUGE-L (Recall-Oriented Understudy for Gisting Evaluation - Longest Common Subsequence)** — Longest common subsequence between generated and reference text.
- ○ **CLIP Score (Contrastive Language-Image Pre-training score)** — Image-caption alignment without reference dependence.
- ○ **BLEU (Bilingual Evaluation Understudy)** — Text similarity between generated and reference descriptions using 1-gram and 2-gram overlap.

**[Toward Stable World Models](https://arxiv.org/abs/2503.08122)** · 📑 3 — The benchmark measures the stability and consistency of learned world models by testing whether they can accurately reverse the effects of actions, assessing both the fidelity of frame predictions and the long-horizon coherence of video generation in complex visual environments.
- ⭐ **World Stability (WS) Score with LPIPS Distance** — The consistency and accuracy of a world model when performing an action followed by its inverse action.
- ⭐ **World Stability (WS) Score with MEt3R Distance** — Variant of WS score using MEt3R (multi-view consistent image warping), which evaluates stability by measuring geometric consistency and multi-view alignment.
- ⭐ **World Stability (WS) Score with DINO Distance** — WS metric using DINO v2 features, which captures semantic and structural consistency at a high level.
- ● **Fréchet Video Distance (FVD)** — Overall quality of generated video sequences by comparing the distributional distance between feature representations of real and model-generated videos.
- ○ **Peak Signal-to-Noise Ratio (PSNR)** — Frame-level pixel-level reconstruction quality, expressed in decibels.
- ○ **Structural Similarity Index (SSIM)** — Frame-level structural and perceptual quality by comparing luminance, contrast, and structure between generated and ground-truth frames.

**[SVIB](https://arxiv.org/abs/2311.09064)** · 📑 10 — Measures how well visual world models generalize to unseen factor combinations by evaluating their ability to perform one-step image-to-image transformations with controllable compositional complexity.
- ⭐ **Systematic Generalization Gap** — The degree of performance degradation when transitioning from training factor combinations to unseen combinations.
- ⭐ **Learned Perceptual Image Patch Similarity (LPIPS)** — Perceptual quality of generated images as perceived by humans, rather than pixel-level accuracy.
- ● **Mean Squared Error (MSE)** — Pixel-level reconstruction accuracy between model-predicted and ground-truth target images.
- ○ **Difficulty Level (Alpha Parameter α)** — Degree of compositional complexity in training data, reflecting the fraction of possible factor combinations shown during training.
- ○ **Transformation Type Category (Atomic vs. Non-Atomic)** — Compositional complexity of the underlying visual transformation rule.

**[World-in-World](https://arxiv.org/abs/2510.18135)** · 📑 29 — The paper evaluates world models' ability to plan in embodied AI tasks by measuring task success rate, planning efficiency, and trajectory quality across four vision-based control domains (active recognition, image-goal navigation, embodied question answering, and manipulation).
- ⭐ **Success Rate (SR)** — The percentage of episodes where the agent successfully completes the task within the action budget.
- ⭐ **Success weighted by Path Length (SPL)** — Combines success rate and path efficiency into a single metric that rewards both reaching the goal and doing so near-optimally.
- ⭐ **Controllability (1 - LPIPS)** — The inverse of LPIPS (Learned Perceptual Image Patch Similarity), capturing fine-grained spatial control precision of the world model's predictions.
- ⭐ **Answer Score (A-EQA)** — The accuracy or correctness of answers provided by the embodied QA agent after active exploration.
- ● **Mean Trajectory Length** — The average number of actions (navigation steps or manipulation primitives) executed per episode before reaching task completion or step budget exhaustion.
- ● **Inference-Time Scaling (SR vs. Average Inferences per Episode)** — The effect of increased computational budget (more world model forward passes per planning step) on task success.
- ● **Data Scaling Efficiency (SR vs. Training Data Size)** — How rapidly task success rate improves as post-training data volume increases.
- ○ **Input Conditioning Format Comparison (Panoramic vs. Front-View)** — Task performance difference when the world model is conditioned on panoramic (360° scene) versus front-facing (narrow FOV) visual context.

**[WBench](https://arxiv.org/abs/2605.25874)** · 📑 1 — WBench proposes a comprehensive 22-metric evaluation framework for assessing AI-generated videos across five dimensions.
- ⭐ **Causal Fidelity** — Assesses physical plausibility of cause-and-effect relationships (e.g., collisions, object deformation, wind effects, human motion).
- ⭐ **Scene Adherence** — Verifies that the generated video maintains consistency with the input scene description, including both visible and offscreen elements.
- ⭐ **Subject Adherence** — Validates that character appearance attributes (clothing, coloring, features) and motion characteristics (gait, agility) match the input specification throughout generation.
- ⭐ **Subject Action Adherence** — Assesses whether generated subject interactions (locomotion, manipulation, gestures) match the input action specification.
- ⭐ **Event Editing Adherence** — Evaluates whether edited events (e.g., 'add explosion at frame 120') occur at correct timing with correct details and no anomalies.
- ⭐ **Navigation Score** — Measures camera pose estimation accuracy and consistency when responding to navigation commands (pan, rotate, zoom).
- ⭐ **Spatial Consistency** — For roundtrip camera trajectories (e.g., pan left then back), verifies that the return frame closely matches the initial viewpoint using perceptual similarity.
- ⭐ **Perspective Consistency** — Tracks subject location and verifies that the character stays geometrically stable and doesn't jump around unexpectedly.
- ⭐ **Geometric Consistency** — Verifies 3D structural coherence by measuring consistency of depth estimates across frames when reprojected.
- ⭐ **Photometric Consistency** — Measures appearance stability by comparing pixel-level intensity/color consistency between reprojected frame pairs.
- ● **Subject Consistency** — Verifies that a character's appearance remains stable across frames, detecting both local flicker and global drift.
- ● **Background Consistency** — Measures temporal stability of non-subject scene elements by tracking appearance across consecutive frames.
- ● **Gated Spatial Consistency** — Extended spatial consistency that samples intermediate frames and penalizes inflated scores from static scenes by taking minimum similarity.
- ● **Segment Continuity** — Detects unexpected hard cuts or discontinuities within a video segment that should be temporally continuous.
- ● **Perspective Switching Adherence** — Validates correctness of viewpoint transitions (e.g., first-person to third-person, or camera cuts).
- ● **Visual Plausibility** — Detects low-level physical artifacts such as geometric distortion, object penetration, unnatural deformation, and other rendering errors.
- ● **Motion Smoothness** — Assesses temporal coherence and fluidity of movement transitions between frames.
- ○ **Aesthetic Quality** — Visual appeal, composition, and professional presentation of the generated video frames.
- ○ **Imaging Quality** — Technical image properties including clarity, sharpness, color fidelity, and absence of noise/compression artifacts.
- ○ **Temporal Flickering** — Detects unwanted frame-to-frame flicker artifacts that degrade visual continuity and viewing experience.
- ○ **Dynamic Degree** — Quantifies motion intensity and scene activity levels.
- ○ **HPSv3-Norm** — Percentile-normalized human-preference reward score that combines aesthetic and visual quality judgments.

**[CRONOS](https://arxiv.org/abs/2605.23699)** · 📑 0 — CRONOS measures the ability of video generation models to maintain visual and physical consistency when objects or scenes undergo counterfactual interventions (viewpoint changes, object appearance modifications, scene changes).
- ⭐ **Physical Plausibility** — Adherence to real-world physics constraints and event realism.
- ⭐ **Intervention Sensitivity** — Consistency of model output quality under different types of counterfactual changes.
- ⭐ **Success Rate (Binary)** — Holistic pass/fail determination.
- ● **Motion Similarity** — Fidelity of object motion relative to reference video.
- ● **3D Shape Stability** — Geometric consistency of objects.
- ○ **Appearance Stability** — Visual consistency of objects across frames.
- ○ **Background Stability** — Absence of unwanted visual artifacts in the background such as morphing, texture warping, or camera drift.
- ○ **Human Annotation Correlation** — Validity of automatic metrics against human judgment.

**[MIND](https://arxiv.org/abs/2602.08025)** · 📑 9 — MIND benchmarks world models on their ability to maintain temporal and geometric consistency while predicting future frames under various actions, measuring both memory coherence and zero-shot action generalization.
- ⭐ **Long Context Memory Consistency (LCM)** — Reconstruction fidelity of previously observed content.
- ⭐ **Generated Scene Consistency (GSC)** — Geometric stability under symmetric motion.
- ⭐ **Action Accuracy (Relative Pose Error / RPE)** — Accuracy of the model in executing specified actions.
- ● **Action Space Generalization** — Zero-shot transfer of learned action control to new action configurations.
- ○ **Aesthetic Quality Assessment** — Visual pleasantness and composition of generated frames.
- ○ **Image Quality Assessment (via MUSIQ)** — Technical image quality.

**[Omni-WorldBench](https://arxiv.org/abs/2603.22212)** · 📑 3 — Quantifies world modeling capabilities by measuring how well AI-generated videos simulate interactions and state transitions, evaluating visual quality, scene control, and physical plausibility of causal effects.
- ⭐ **AgenticScore (Final Aggregated Score)** — Holistic world model performance: weighted aggregate of all three evaluation dimensions (interaction fidelity, video quality, controllability), with weights adapted per-prompt.
- ⭐ **InterCov (Interaction Semantic Consistency)** — Causal plausibility: whether objects that interact semantically respond in physically consistent ways (e.g., pushed object moves, not floats away).
- ⭐ **InterOrder (Temporal Event Precedence)** — Causal sequence validity: whether the temporal order of cause-and-effect events is physically plausible (causes precede effects).
- ⭐ **Object Control** — Success of object placement and presence: the proportion of objects specified in the prompt that are visually present and grounded in the generated video frames.
- ● **Camera Control** — Accuracy of camera trajectory alignment: how well the generated video's camera movements match the specified camera control commands (separated into rotational and translational components).
- ● **InterStab-L (Long-horizon Stability)** — Structural consistency over long timeframes: whether non-interacted regions remain visually and semantically stable when a video revisits them (e.g., background unchanged after 50 frames).
- ● **InterStab-N (Non-target Stability)** — Motion isolation: how well non-interacted objects remain still, measuring unwanted motion energy in off-target regions.
- ○ **Transitions Detect** — Scene continuity: whether unwanted scene cuts or abrupt visual transitions occur during video generation.

**[World Reasoning Arena](https://arxiv.org/abs/2603.25887)** · 📑 1 — A benchmark measuring how well vision-language models can simulate physical worlds, predict multi-step action sequences, and reason about counterfactual futures for planning.
- ⭐ **Action Faithfulness** — Whether the model generates action sequences that reasonably follow the intended control instruction without deviating from the specified behavior.
- ⭐ **Trajectory-Level Task Success (Planning)** — Whether multi-step simulated rollouts help select actions that actually achieve stated goals (e.g., move a cup to a location), compared to pure vision-language baseline agents.
- ⭐ **Step-Wise Simulation Accuracy** — Ability to correctly predict the immediate consequence of a single action from a given state, selecting the correct outcome from distractor options.
- ● **Multi-Round Smoothness (MRS)** — Quality of smooth, jerk-free transitions across action sequences in multi-step rollouts, penalizing abrupt changes in motion.
- ● **Action Precision (Environment Simulation)** — How accurately the model predicts visually verifiable scene-level changes with predictable downstream effects from a given action.
- ○ **Generation Consistency (across rounds)** — How well the model maintains coherent identity and style of key elements over multiple sequential generation rounds, penalizing progressive degradation.

**[STEVO-Bench](https://arxiv.org/abs/2603.13215)** · 📑 3 — STEVO-Bench measures video world models' ability to generate plausible unseen state changes in occluded scenarios, decoupling true physical evolution from mere observation tricks.
- ⭐ **Task Success Rate (Overall)** — Compound binary metric: whether a video world model successfully generates a plausible hidden state evolution.
- ⭐ **State Progress Rate** — During the hidden/unobserved period, whether the intended state change actually progresses.
- ● **Control Success Rate** — Whether prerequisite conditions for evaluation are met: both observation control (scene was obstructed/hidden consistently) AND action control (the requested action both occurred and had correct physical effects).
- ● **Physical Plausibility Rate** — Whether the generated world evolution contains egregious physics violations.
- ● **Coherence Rate** — Whether the evolved scene maintains visual and temporal coherence.
- ○ **Verifier-Human Accuracy** — Agreement between automated VLM verifier binary labels and human rater binary labels.
- ○ **ROC-AUC (Receiver Operating Characteristic Area Under Curve)** — Balanced diagnostic performance of verifier judgment accounting for class imbalance in binary pass/fail labels.
- ○ **Model Ranking Agreement (MRA)** — Whether verifiers and human raters agree on the relative ranking of models.

**[WorldMark](https://arxiv.org/abs/2604.21686)** · 📑 4 — WorldMark measures whether AI video generation models can faithfully execute camera movements while maintaining visual quality, world consistency, and stable object behavior across extended video sequences.
- ⭐ **Translation Error** — Spatial consistency between generated video and ground-truth camera trajectory, measured as scale-invariant Euclidean distance of camera position.
- ⭐ **Rotation Error** — Orientational consistency between generated video and ground-truth camera rotation, measured as geodesic angular deviation between rotation matrices.
- ⭐ **Reprojection Error** — 3D spatial coherence and world stability by detecting scene drift, morphing, structural collapse, and geometric inconsistencies via 2D pixel reprojection from 3D reconstruction.
- ● **State Consistency** — Spatiotemporal stability of objects within the world: whether object shape, texture, and motion remain continuous and believable across frames, free from abrupt mutations.
- ● **Content Consistency** — Presence of hallucinated objects, 'popping effects' (sudden appearance/disappearance), and other spatiotemporal hallucinations where scene content violates physical continuity.
- ● **Aesthetic Quality** — Human-perceived aesthetic appeal of generated frames, capturing layout harmony, color balance, lighting coherence, and overall photo-realism.
- ● **Imaging Quality** — Low-level image degradations including noise, blur, over-exposure, compression artifacts, and focus inconsistencies within individual frames.
- ○ **Style Consistency** — Global aesthetic uniformity and lighting coherence: whether color palette, lighting tone, stylistic treatment remain stable across frames without unexplained shifts.

**[PDI-Bench](https://arxiv.org/abs/2605.15185)** · 📑 0 — PDI-Bench quantifies geometric coherence failures in AI-generated videos by measuring three dimensions of 3D consistency violations that perceptual metrics typically miss.
- ⭐ **Scale-Depth Alignment Error (εs)** — Whether object scaling in video frames correctly corresponds to depth positioning in 3D space.
- ⭐ **3D Motion Consistency Error (εt)** — Whether tracked object point trajectories remain physically plausible in 3D space across frames.
- ⭐ **3D Structural Rigidity Error (εr)** — Whether rigid objects maintain consistent geometric relationships between parts across frames.
- ● **PDI Score (Perspective Distortion Index)** — Aggregated geometric consistency quality combining all three failure dimensions.

**[CoW-Bench (Trinity of Consistency)](https://arxiv.org/abs/2602.23152)** · 📑 3 — CoW-Bench assesses whether world models (video generators and multimodal systems) maintain consistency across three dimensions.
- ⭐ **Worldline (Temporal Consistency) Metric Family (T1)** — Whether a multi-frame video maintains consistent object identity, attributes, and physics over time.
- ⭐ **Subject-Attribute (Subj-Attr) Metric Family (M1)** — Whether a generated image or video preserves the identity and attributes of specified subjects (e.g., the same person remains the same across edits, not replaced by someone else).
- ⭐ **Local-Edit (Local-Edit) Metric Family (M2)** — Whether the model makes only the specified local edit to an image or scene without diffusing changes globally.
- ⭐ **Multi-Constraint (Multi-Const) Metric Family (M3)** — Whether the model satisfies multiple overlapping constraints in a single generation (e.g., 'render a red car on a sunny road with a dog nearby').
- ● **Average Score (AVG / Leaderboard Ranking)** — A normalized aggregate score across all metric families (M1, M2, M3, T1) and atomic checks, rescaled to a 0–100 percentage scale for leaderboard ranking.
- ○ **Identity Drift Atomic Check** — A specific failure mode within Subject Consistency (T1.Subj-cons): does an object's or character's fundamental identity persist across frames, or does the model substitute a different entity frame-to-frame while plausibly maintaining motion?
- ○ **Boundary Leakage (LEAK) Atomic Check** — A specific failure mode within Local-Edit (M2.Leakage): when a local edit is requested, does the model unintentionally apply changes beyond the target region (e.g., changing a wall color also shifts the sofa's hue, or editing an object's expression affects unrelated background details)?
- ○ **Attribute Rebinding (MNCH / Mismatch) Atomic Check** — A specific failure mode within Subject-Attribute (M1.Dominance or M3.Attr-corr): when multiple subjects/objects are present, does the model bind attributes to the correct entity, or does it mix them up (e.g., 'a red car and a blue bike' becomes 'red bike and blue car')?

**[A Mechanistic View on Video Generation as World Models](https://arxiv.org/abs/2601.17067)** · 📑 2
- ⭐ **World Consistency Score (WCS)** — Internal logical integrity of generated long-horizon videos by checking object permanence, relation stability between objects, and causal rule compliance.
- ⭐ **Reconstruction FID (rFID)** — Scene re-visitation accuracy: whether the model can correctly retrieve the internal latent state when returning to a previously-seen viewpoint or scene configuration.
- ⭐ **Physics-IQ Test Suite (Spatial IoU, Spatio-temporal IoU, Weighted Spatial IoU, Pixel-wise MSE)** — Physical plausibility across four dimensions: (1) action localization accuracy (where does the object move?), (2) timing and location of movement (when and where?), (3) movement magnitude fidelity (how far/fast?), (4) pixel-level alignment of physical outcomes.
- ⭐ **Success Rate (SR) and Normalized Regret** — Functional task performance: (1) Success Rate = percentage of navigation/manipulation tasks completed correctly within generated worlds.
- ⭐ **Controllability Score** — How well model-predicted observations match real-world ground-truth outcomes when given the same action sequence, capturing alignment between simulated and actual physics.
- ⭐ **ChronoMagic-Bench (Metamorphic Progression Score, Temporal Coherence Score)** — Temporal reasoning and semantic monotonicity: (1) Metamorphic Progression = realism of monotonic temporal transformations (e.g., object aging, person getting older).
- ● **Long-Horizon Frame Coherence (600+ frames / 1800+ frames)** — Ability to generate coherent video content over extended sequences, tracking scene stability, object consistency, and absence of quality collapse.
- ● **Fréchet Video Distance (FVD)** — Spatiotemporal consistency in short video clips by extending FID to capture motion patterns and temporal coherence across consecutive frames.
- ● **Fréchet Video Motion Distance (FVMD)** — Optical flow-based temporal smoothness and naturalness of motion, penalizing jerky or unnatural transitions between frames.
- ○ **Fréchet Inception Distance (FID)** — Per-frame visual quality and realism by comparing feature distributions between generated and real video frames using a pretrained Inception classifier.
- ○ **VBench / VBench++** — Hierarchical decomposition of video quality into motion smoothness, subject identity consistency, spatial relationship preservation, and (in VBench++) trustworthiness and text-semantic alignment.

**[iWorld-Bench](https://arxiv.org/abs/2605.03941)** · 📑 2 — Assesses world models' ability to generate coherent video sequences that respect physical laws, follow user commands, and maintain spatial/temporal consistency across visual generation, camera trajectory control, and geometric memory tasks.
- ⭐ **Trajectory Accuracy** — Precision and fidelity of model adherence to user-specified camera control commands, measuring instruction-level controllability in motion tangent space.
- ⭐ **Memory Symmetry** — Logical loop-closure consistency in reciprocal tasks.
- ⭐ **Trajectory Alignment** — Spatial topological consistency of camera movements in return-trip scenarios, validating that reciprocal displacements cancel geometrically.
- ● **Trajectory Tolerance** — Robustness and physical execution fidelity of camera motion under ideal constraint conditions, validating that generated videos are geometrically feasible.
- ● **Motion Smoothness** — Naturalness and continuity of motion, detecting jitters, unnatural accelerations, and physical inconsistencies in the video flow.
- ● **Sharpness Retention** — Edge clarity and texture stability versus high-frequency artifacts and visual collapse, distinguishing genuine texture preservation from noise/aliasing.
- ○ **Image Quality (MUSIQ-based)** — Low-level visual distortions and fundamental rendering fidelity, detecting artifacts, blurriness, and perceptual degradation across generated frames.
- ○ **Brightness Consistency** — Temporal stability of brightness distribution between consecutive frames and relative to the initial frame, penalizing abrupt lighting shifts and inter-frame flicker.
- ○ **Color Temperature Constraint** — Global color temperature stability and hue consistency across the temporal sequence, penalizing color drift and unnatural tint shifts in HSV space.

**[WorldReasonBench](https://arxiv.org/abs/2605.10434)** · 📑 0 — Evaluates video-generation models' ability to reason about world dynamics by measuring both outcome accuracy and reasoning consistency, including temporal/causal correctness and detection of "outcome hacking" (visually plausible but physically incorrect videos).
- ⭐ **ScorePR (Process-aware Score)** — Headline metric balancing QA accuracy with process fidelity, penalizing models that achieve high accuracy only by 'cheating' on static/visual reasoning without understanding dynamics.
- ⭐ **Reasoning Gap (ΔRG)** — Discrepancy between static (outcome) and dynamic (process) reasoning accuracy, detecting 'outcome hacking'.
- ⭐ **AccQA (QA Accuracy)** — Overall correctness of answers to structured questions about video content, measuring whether a model correctly answers what happened, when it happened, and why it happened in generated videos.
- ● **Phase Scores (s_state, s_proc, s_fidel, s_mech)** — Granular breakdown of reasoning: s_state captures initial/final state understanding (static facts), s_proc captures temporal sequencing (event ordering), s_fidel captures fine-grained detail verification, and s_mech captures causal/physical mechanism reasoning.
- ● **Process-completeness Ratio** — Ratio of dynamic reasoning accuracy to overall accuracy, indicating the proportion of correct answers that stem from understanding temporal/causal processes versus static facts.
- ● **S(v) (Aggregate Video Score)** — Holistic quality score combining reasoning correctness, temporal consistency, and visual aesthetics into a single value for reward-model training.
- ● **Spearman ρ (Rank Correlation)** — Consistency of a judge's ranking of videos against rankings derived from human Elo ratings, capturing whether the judge preserves the correct relative order of video quality.
- ● **Pairwise Agreement (with/without ties)** — Alignment between a reward model or human judge and expert human preferences on pairwise video comparisons, indicating how consistently the judge predicts which video is better.
- ○ **Induced Pairwise Accuracy** — Accuracy of preference predictions derived from point-wise (single-video) scores, measuring how well pairwise preferences can be inferred from independent video ratings.
- ○ **Bootstrap Confidence Intervals (95%)** — Uncertainty bounds on primary metrics (ScorePR, AccQA, S(v)), quantifying the range within which the true population metric likely lies given sampling variability.
- ○ **Difficulty-weighted Score** — Auxiliary metric that emphasizes harder/more discriminative questions, upweighting questions that fewer models answer correctly.
- ○ **Bottleneck Composite Score** — Performance on the most challenging dimensions, aggregating accuracy on the hardest questions/categories to identify remaining model weaknesses.

**[WorldOlympiad](https://arxiv.org/abs/2606.11129)** · 📑 0 — WorldOlympiad measures whether video-generating world models can reliably simulate realistic physics, preserve 3D spatial coherence, and respond correctly to action prompts over extended sequences.
- ⭐ **Composite Overall Score (S_all)** — Single aggregate metric combining all three dimensions equally to rank models on overall world-model capability.
- ● **Physical Faithfulness (S_phys)** — Whether generated videos obey interpretable physical rules across mechanics (gravity, buoyancy, compression, impact), thermodynamics (phase transitions: melting, vaporization, condensation, etc.), and material properties (color mixing, solubility, hardness, combustibility).
- ● **3D Consistency (S_3D)** — Whether generated video frames preserve coherent three-dimensional structure, spatial layout, and camera consistency.
- ● **Interaction Fidelity (S_interact)** — Whether generated video sequences faithfully execute action prompts, maintain semantic coherence with natural-language descriptions, and preserve smooth visual continuity across consecutive video chunks.

---

## 3D / 4D

**[OmniWorld](https://arxiv.org/abs/2509.12201)** · 📑 30 — OmniWorld benchmarks vision and video generation models across diverse visual domains (synthetic and real-world), measuring their ability to understand 3D scene geometry, camera pose, and generate dynamic video content in response to camera control commands.
- ⭐ **Absolute Relative Error (Abs Rel) - Depth Estimation** — Scale-invariant error in monocular or video depth estimation.
- ⭐ **Threshold Accuracy (δ<1.25) - Depth Estimation** — Percentage of depth predictions that fall within an acceptable relative error threshold.
- ⭐ **Absolute Trajectory Error (ATE) - Camera Pose Estimation** — Overall accuracy of estimated camera trajectory compared to ground truth.
- ● **Camera Motion Consistency (CamMC) - Combined Camera Control** — Overall accuracy of camera control adherence, combining translation and rotation fidelity.
- ● **Relative Pose Error (RPE) - Translation and Rotation** — Frame-to-frame consistency of pose estimation.
- ● **Translation Error (TransErr) - Video Generation Camera Control** — Accuracy of camera translation (x, y, z movement) commands in generated video.
- ● **Rotation Error (RotErr) - Video Generation Camera Control** — Accuracy of camera rotation (pitch, yaw, roll) commands in generated video.
- ○ **Fréchet Video Distance (FVD) - Video Perceptual Quality** — Perceptual realism and quality of generated video content.
- ○ **AUC@5, @10, @20 - Dynamic Pose Localization** — Area Under Curve of pose accuracy at rotation/translation error thresholds.

**[PhyScore (LoViF 2026 Challenge)](https://arxiv.org/abs/2605.05187)** · 📑 2 — PhyScore evaluates AI-generated video quality across physics realism and alignment dimensions, combining anomaly detection accuracy with correlation-based scoring to benchmark generative models on their ability to produce physically plausible dynamic content.
- ⭐ **Physical Realism Score (1-10 scale)** — Adherence to physical laws and plausibility of dynamics in generated videos.
- ⭐ **Condition-Video Alignment Score (1-10 scale)** — Consistency between input conditions (text prompts, reference images, or source videos) and the generated output.
- ⭐ **TimeStamp_IOU (Temporal Intersection-over-Union)** — Accuracy of fine-grained anomaly localization.
- ● **Spatial-Temporal Consistency Score (1-10 scale)** — Coherence of video frames across space and time.
- ● **Video Quality Score (1-10 scale)** — Visual fidelity and perceptual quality of generated videos as rated by human annotators on a 1-10 ordinal scale.
- ● **Final_Score (Composite Ranking)** — Overall challenge ranking combining anomaly detection precision with general prediction accuracy.
- ○ **SRCC (Spearman Rank Correlation Coefficient)** — Monotonic rank correlation between predicted quality scores and ground-truth scores.
- ○ **PLCC (Pearson Linear Correlation Coefficient)** — Linear correlation strength between predicted scores and ground-truth scores.

**[4DWorldBench](https://arxiv.org/abs/2511.19836)** · 📑 6 — Benchmark that comprehensively evaluates 4D world generation systems (video synthesis with spatial-temporal coherence) across perceptual quality, semantic alignment to input conditions, adherence to physical laws, and spatial-temporal stability.
- ⭐ **Condition-4D Alignment (Aggregate)** — Overall alignment between input text conditions and generated 4D video across all semantic dimensions (event, scene, attribute, motion).
- ⭐ **4D Consistency (Aggregate)** — Overall spatial-temporal stability across 3D viewpoint consistency, motion coherence, and style stability.
- ⭐ **Physical Realism (Aggregate)** — Overall adherence to physical laws across dynamics, optics, and thermal phenomena.
- ⭐ **Perceptual Quality (Aggregate)** — Overall visual fidelity, temporal smoothness, and texture realism of generated video.
- ● **Event Control (Condition-4D Alignment sub-metric)** — Whether the generated video correctly depicts the plot and character actions in the intended chronological order when given a text condition specifying story events.
- ● **Scene Control (Condition-4D Alignment sub-metric)** — Accuracy of landscape, environment, and spatial layout details (objects, colors, structures, locations) matching the input text condition.
- ● **Attribute Relationship Control (Condition-4D Alignment sub-metric)** — Correctness of spatial relationships between objects (relative positions, distances, orientations) as specified in the input condition.
- ● **Motion Control (Condition-4D Alignment sub-metric)** — Temporal ordering of motions and dynamic events.
- ● **Dynamics (Physical Realism sub-metric)** — Adherence to physical laws governing force, motion, and mechanical interactions (e.g., objects fall with gravity, friction slows motion, collisions behave realistically).
- ● **Optics (Physical Realism sub-metric)** — Correctness of light behavior: refraction, reflection, shadow casting, transparency, and other optical phenomena.
- ● **Thermal (Physical Realism sub-metric)** — Plausibility of thermal phenomena: heating effects, phase transitions (melting, boiling), temperature-dependent behavior.
- ● **3D Consistency via Reprojection Error (4D Consistency sub-metric)** — Spatial consistency across different viewpoints.
- ● **Motion Consistency (4D Consistency sub-metric)** — Temporal coherence of motion.
- ● **Style Consistency (4D Consistency sub-metric)** — Visual style stability.
- ● **Spatial Quality (via CLIPIQA+ and CLIP-Aesthetic)** — Visual fidelity and technical quality of individual frames, plus human aesthetic preferences.
- ● **Temporal Quality (via FastVQA)** — Temporal coherence and visual stability across video frames.
- ● **3D Texture Quality (via mPLUG-Owl3)** — Realism and physical plausibility of surface textures, materials, and visual details in 3D objects.
- ○ **PLCC (Pearson Correlation with Human Judgment)** — Linear correlation strength between automated metric scores and human judgments.
- ○ **SRCC (Spearman Rank Correlation with Human Judgment)** — Rank-order correlation between automated scores and human rankings.

---

## Driving

**[ACT-Bench](https://arxiv.org/abs/2412.05337)** · 📑 8 — ACT-Bench evaluates whether world models for autonomous driving can faithfully execute high-level action instructions when generating future video frames, measuring both semantic instruction adherence and spatial trajectory accuracy.
- ⭐ **Final Displacement Error (FDE)** — Spatial accuracy at the end of the trajectory.
- ⭐ **Average Displacement Error (ADE)** — Spatial accuracy of the generated vehicle trajectory.
- ● **Instruction-Execution Consistency (IEC)** — Whether the high-level driving action performed in a generated video matches the action that was instructed.
- ○ **High-level Action Classification Accuracy** — How reliably the ACT-Estimator can infer the correct driving action from video frames.

**[Beyond Simulation](https://arxiv.org/abs/2508.01922)** · 📑 1 — Evaluates world models for autonomous driving by measuring both prediction accuracy under standard conditions and robustness when ego agents are constrained to replay ground-truth trajectories, exposing whether models rely on unrealistic agent interdependencies.
- ⭐ **Realism Score (ℳ)** — Aggregate performance across all nine NLL metrics, combining them into a single weighted summary score.
- ⭐ **Policy-Aware Delta Metric (ΔℳI)** — How much world model performance degrades when the ego vehicle is forced to replay its ground-truth trajectory instead of using its learned policy.
- ⭐ **Simulation Delta Metric (ΔℳI^sim)** — Performance change for non-ego agents only when ego replays ground truth.
- ● **Simulation Confusion Rate (Cs)** — Percentage of scenarios where the traffic simulation significantly fails when dealing with uncontrollable agents (ego vehicle constrained to replay ground truth).
- ● **Policy Confusion Rate (Cp)** — Percentage of scenarios where forcing the ego vehicle to replay ground truth actually improves model performance, suggesting the model normally makes wrong assumptions about ego behavior.
- ● **Aggregated Delta Metric (Δℳ, Δℳ^sim)** — Overall sensitivity to uncontrollable objects across the entire evaluation set.
- ○ **Negative Log-Likelihood (NLL)** — Quality of world model predictions for nine driving-relevant attributes: speed, acceleration, angular speed, angular acceleration, distance to nearest object, collisions, time-to-collision, distance to road edge, and road departures.
- ○ **Minimum Average Displacement Error (minADE)** — Minimum trajectory prediction error across all predictions, measuring planning-relevant trajectory accuracy.

**[SimWorld](https://arxiv.org/abs/2503.13952)** · 📑 4 — SimWorld evaluates a generative world model for autonomous driving by measuring both the distributional quality of generated images and the downstream task performance (object detection and segmentation) when models are pre-trained on synthetic data.
- ⭐ **Mean Average Precision (mAP) — Object Detection** — The accuracy of object detection models trained on synthetic data.
- ⭐ **Mean Intersection over Union (mIoU) — Semantic Segmentation** — The pixel-level segmentation accuracy across all classes.
- ⭐ **Fréchet Inception Distance (FID)** — The distributional distance between generated and real images.
- ● **Pixel Diversity (D_pix)** — The stylistic and chromatic consistency of generated images, quantified as the standard deviation of pixel values across a batch.

**[WorldLens](https://arxiv.org/abs/2512.10958)** · 📑 20 — WorldLens evaluates generative 4D driving world models on whether generated environments preserve geometric consistency, obey physics, and support reliable agent control.
- ⭐ **Photometric Error (R.1)** — Reconstruction accuracy.
- ⭐ **Geometric Discrepancy (R.2)** — Depth reconstruction accuracy.
- ⭐ **Temporal Consistency (G.5)** — Global frame smoothness.
- ⭐ **Subject Coherence (G.2)** — Temporal identity stability.
- ⭐ **Depth Discrepancy (G.4)** — Geometric coherence.
- ⭐ **Closed-Loop Adherence (A.4)** — Closed-loop driving capability.
- ● **Behavioral Safety (H.4)** — Traffic safety.
- ● **Novel-View Quality (R.3)** — Unseen viewpoint rendering quality.
- ● **Cross-View Consistency (G.8)** — Multi-camera alignment.
- ● **3D & 4D Consistency (H.3)** — Spatial-temporal coherence.
- ● **Subject Consistency (G.3)** — Fine-grained texture and geometry stability.
- ● **Semantic Consistency (G.6)** — Scene layout stability.
- ● **Route Completion (A.3)** — Navigation success.
- ● **World Realism (H.1)** — Overall visual authenticity and physical plausibility as judged by human raters.
- ○ **Novel-View Discrepancy (R.4)** — Novel-view consistency.
- ○ **Perceptual Discrepancy (G.7)** — Appearance consistency.
- ○ **Physical Plausibility (H.2)** — Physics coherence.
- ○ **Displacement Error (A.1)** — Trajectory prediction accuracy.
- ○ **Open-Loop Adherence (A.2)** — Driving behavior realism.
- ○ **3D Object Detection (D.2)** — Geometric perception.
- ○ **3D Object Tracking (D.3)** — Motion consistency.
- ○ **Map Segmentation (D.1)** — BEV mapping accuracy.
- ○ **Occupancy Prediction (D.4)** — 3D spatial reconstruction.
- ○ **Subject Fidelity (G.1)** — Object instance realism.

**[DrivingGen](https://arxiv.org/abs/2601.01528)** · 📑 10 — DrivingGen proposes a comprehensive benchmark to evaluate autonomous driving video generation systems across four dimensions.
- ⭐ **Fréchet Video Distance (FVD)** — Distributional similarity between generated and real driving videos in feature space.
- ⭐ **Fréchet Trajectory Distance (FTD)** — Distributional similarity of agent trajectories (paths through space over time) between generated and real scenarios.
- ⭐ **Trajectory Quality (Comfort × Motion × Curvature)** — Physical realism of agent motion.
- ● **CLIP-IQA+ (Subjective Image Quality)** — Perceptual image quality aligned with human judgment.
- ● **Video Consistency (DINOv3 Feature Similarity)** — Temporal consistency of visual appearance across frames.
- ● **Average Displacement Error (ADE)** — Step-by-step trajectory alignment.
- ● **Dynamic Time Warping (DTW)** — Path-shape similarity independent of speed.
- ○ **Modulation Mitigation Probability (MMP)** — Objective image quality against PWM (pulse-width modulation) induced flicker.
- ○ **Agent Appearance Consistency** — Visual consistency of agents (pedestrians, vehicles, obstacles) across frames.
- ○ **Trajectory Consistency (Speed & Acceleration Dispersion)** — Smooth, realistic kinematics over the full trajectory.
- ○ **Agent Abnormal Disappearance Rate** — Absence of unrealistic agent occlusion.

---

## Embodied & Policy Evaluation

**[WorldGym](https://arxiv.org/abs/2506.00613)** · 📑 26 — WorldGym measures how accurately a world model (VLM-guided video prediction) captures robot dynamics and can predict task success, by comparing generated rollouts against ground-truth simulator outcomes and human visual assessment.
- ⭐ **Policy Value Estimation (ρ̂(π))** — Whether the world model accurately estimates a policy's success rate by rolling out the policy forward and measuring task completion, compared to ground-truth success rates in the real simulator.
- ⭐ **Policy Ranking Preservation** — Whether the relative ordering of multiple policies by success rate in the world model matches their true ordering in the real simulator.
- ⭐ **VLM Reward Accuracy (TP, FP, TN, FN)** — Whether a vision-language model correctly predicts task success/failure by comparing its binary predictions against ground-truth task outcomes (success or failure in the simulator).
- ● **LPIPS (Learned Perceptual Image Patch Similarity)** — Perceptual similarity using deep neural network features, capturing whether predicted frames 'look right' to human observers rather than matching pixel-for-pixel.
- ● **Semantic MSE (Arm and Object)** — Pixel-wise prediction error isolated to semantic regions (robot arm or manipulated object) rather than the entire frame, to identify where generation errors concentrate.
- ● **SSIM (Structural Similarity Index)** — Whether the generated video preserves structural patterns and spatial relationships (luminance, contrast, structure) rather than just pixel-level accuracy, correlating with human perception of visual quality.
- ● **Mean Squared Error (MSE)** — Pixel-wise visual fidelity of generated video frames versus ground truth by computing the average squared difference in pixel values across all frames.
- ○ **Out-of-Distribution Action Robustness** — How well the world model generalizes to noisy or perturbed actions outside its training distribution by adding Gaussian noise to policy actions and measuring prediction error or overestimation.
- ○ **Context and Horizon Length Optimization (Arm MSE)** — How the world model's ability to predict robot arm pose depends on the length of conditioning context (input frames) and prediction horizon (how many frames ahead to predict).
- ○ **Generalization to Novel Tasks (Qualitative Visual Assessment)** — Whether the world model can predict robot behavior on previously unseen task types and environments given only the initial frame, by visual inspection of predicted vs.

**[WorldEval](https://arxiv.org/abs/2505.19017)** · 📑 44 — WorldEval measures how accurately a world model can predict robot policy performance in generated videos, validating that simulated performance rankings correlate with real-world task success to enable efficient policy evaluation without physical trials.
- ⭐ **Pearson Correlation Coefficient (Pearson r)** — The linear relationship between simulated policy performance scores (generated by WorldEval's video evaluation) and real-world policy success rates.
- ⭐ **Mean Maximum Rank Violation (MMRV)** — The consistency of policy rankings between WorldEval predictions and real-world outcomes.
- ● **Task Success Classification (VLM-based)** — Binary success/failure classification for each generated video trajectory, determined by a vision-language model answering task-specific questions.
- ● **Generalization Performance (MMRV across novel environments)** — Whether policy rankings remain consistent when the world model is deployed in unseen environmental contexts (different rooms, novel objects, new tasks), indicating the proxy's robustness and transferability.
- ○ **Fréchet Inception Distance (FID)** — The quality and realism of generated robot videos by measuring the distance between feature distributions of generated and real robot video frames.

**[stable-worldmodel](https://arxiv.org/abs/2605.21800)** · 📑 2 — The benchmark measures how well world model planning systems generalize across in-distribution control tasks and remain robust under controlled visual and physical distribution shifts, capturing both prediction accuracy and goal-reaching capability.
- ⭐ **Success Rate (SR)** — The proportion of episodes in which a world model-based planner successfully achieves the task goal within the episode's maximum step limit.
- ⭐ **In-Distribution Performance (Environment-Specific SR)** — Success rate on the canonical in-distribution test set for each environment (Push-T, OGB-Cube, etc.), evaluated on held-out expert or random-policy trajectories following the same visual/physical distribution as training data.
- ● **Success Rate Under Visual Factor Perturbations** — Planning success rate when one visual attribute of the environment is systematically modified (e.g., agent color, block color, canvas color, object size, lighting, textures, occlusions).
- ● **Success Rate Under Physical Factor Perturbations** — Planning success rate when physical simulation parameters are modified (mass, friction, gravity, density).
- ● **Trajectory-level Prediction MSE** — Mean Squared Error of the world model's predicted state trajectories compared to ground truth, computed over full episode trajectories.
- ○ **Distractor Robustness (Visual Clutter)** — Success rate as the number of visual distractor squares placed randomly in the scene increases.
- ○ **Data Loading Throughput** — Number of samples (video frames or trajectories) loaded per second from different storage formats during training and evaluation.

**[Wow, wo, val!](https://arxiv.org/abs/2601.04137)** · 📑 6 — A comprehensive benchmark assessing video generation models' ability to follow complex manipulation instructions while maintaining physical consistency, semantic fidelity, and real-world executability across 22 distinct evaluation dimensions.
- ⭐ **IDM Turing Test (Real-World Execution Success Rate, %)** — Whether a Gripper-Centric Inverse Dynamics Model can successfully interpret generated video into real-world robot actions, indicating practical executability on actual hardware.
- ⭐ **Planning DAG Score (Node Correctness + Task Completion, max 100)** — Correctness of long-horizon planning: whether the video successfully executes all required sub-tasks with correct arguments, measured via nodes in an action DAG.
- ⭐ **Sequence Match Score (0-1 Scale)** — Correctness of action ordering, evaluating whether action-object pairs occur in the sequence specified by the instruction.
- ● **Caption Score (1-5 Scale)** — Whether the generated video matches the semantic content of the instruction by comparing extracted descriptions of generated versus ground-truth videos.
- ● **Execution Quality Score (1-5 Scale)** — Correctness of individual action-object pairs themselves, not their ordering, assessing whether each action targets the right object appropriately.
- ● **DreamSim (Human-Aligned Perceptual Similarity)** — Perceptual similarity calibrated to human preferences, trained from human triplet judgments of which video pair looks more similar.
- ● **Physical Common Sense (6-Dimensional Score, 1-5 Scale)** — Physical realism across six dimensions: object interaction correctness, object properties preservation, temporal consistency of physics, lighting/shading coherence, fluid dynamics realism, and absence of physical anomalies.
- ● **Trajectory Consistency (MED, DTW, Fréchet Distance)** — Temporal smoothness of end-effector and object motion, ensuring trajectories are physically plausible and continuous across frames.
- ○ **DINO (Semantic/Instance Alignment)** — Semantic and instance-level correctness, detecting whether semantic entities (objects, actors) are aligned between generated and reference frames.
- ○ **Mask-Guided Regional Consistency** — Temporal consistency of specific regions (robot arm, manipulated object, background) separately, ensuring each region maintains coherence across frames.
- ○ **SSIM (Structural Similarity Index)** — Structural consistency beyond pixel values, capturing luminance, contrast, and structural alignment between generated and ground-truth video frames.
- ○ **FVD (Fréchet Video Distance)** — Video quality at the distribution level, measuring perceptual similarity between generated and real video embeddings in feature space rather than pixel space.
- ○ **PSNR (Peak Signal-to-Noise Ratio)** — Pixel-level fidelity by comparing maximum signal intensity to pixel-wise reconstruction error between generated and reference frames.
- ○ **Human Preference Correlation (Pearson r, Spearman ρ)** — Validity of the overall benchmark score, confirming it aligns with human expert judgment of video quality and instruction-following correctness.
- ○ **Human Deceive Ratio Correlation** — Correlation between how well generated videos fool human evaluators and the overall benchmark score, indicating whether benchmark captures deceptiveness.

**[WorldArena](https://arxiv.org/abs/2602.08971)** · 📑 19 — WorldArena measures embodied world model quality across three dimensions.
- ⭐ **Data Engine Task (Policy Gain π₀.₅)** — Downstream utility: how much does a reinforcement learning policy improve when trained on synthetic world-model-generated trajectories versus random baseline.
- ⭐ **Policy Evaluator Task (Simulator Correlation)** — Measures whether world model evaluation correlates with real downstream policy performance, validating the benchmark's predictive validity.
- ⭐ **Action Planner Task (Direct Success Rate)** — Closed-loop robot task completion.
- ● **Human Evaluation (1-5 Scale, Converted to 0-100)** — Direct human assessment of overall video quality, instruction following fidelity, and physics plausibility by expert annotators.
- ● **EWMScore (Unified Video Quality Metric)** — Aggregates all 16 video-based metrics into a single 0-100 interpretable score, representing overall embodied world model video quality.
- ○ **Instruction Following (VLM Text Alignment)** — Verifies that generated videos execute the intended action, target object, and outcome state as specified in text instructions.
- ○ **Image Quality (MUSIQ)** — Detects visual distortions and artifacts in generated frames using a learned distortion model.
- ○ **Dynamic Degree** — Quantifies motion intensity by measuring optical flow magnitude in the most motion-rich pixels, capturing scene dynamism.
- ○ **Subject Consistency (DINO Features)** — Verifies that the main object (e.g., robot gripper) maintains visual identity and appearance across frames.
- ○ **Background Consistency (CLIP Features)** — Assesses scene stability by measuring how much the background and non-manipulated context remain unchanged across frames.
- ○ **Photometric Consistency** — Verifies that pixel-level alignment holds under motion, detecting geometric distortions or unrealistic warping.
- ○ **Interaction Quality (VLM-based Physics)** — Judges whether object interactions follow real physics.
- ○ **Trajectory Accuracy (DTW-based Bounding Box)** — Verifies that tracked objects follow spatially correct paths.
- ○ **Depth Accuracy (Monocular Depth Estimation)** — Assesses 3D spatial consistency by comparing estimated depth maps (from single-frame prediction) between generated and reference videos.
- ○ **Semantic Alignment (CLIP Text-Video)** — Measures how well the visual content matches descriptions of the reference video, at a semantic level independent of exact pixel matching.
- ○ **Action Following (Diversity Across Instructions)** — For different action instructions applied to the same scene, measures whether the model produces meaningfully different outputs rather than ignoring instructions.

**[RoboWM-Bench](https://arxiv.org/abs/2604.19092)** · 📑 2 — RoboWM-Bench evaluates whether world models can predict physically executable manipulation behaviors that succeed in real robotic tasks, beyond just visual plausibility.
- ⭐ **Task-Level Embodied Success Rate** — Whether a world model's predicted manipulation sequence accomplishes the intended task objective when extracted actions are executed on a real robot in a reconstructed sim-to-real environment.
- ⭐ **Step-Level Action Node Satisfaction** — Whether predicted behaviors satisfy physical and interaction constraints at semantically meaningful interaction milestones (e.g., gripper-object contact, lift clearance, stable placement).
- ⭐ **Inverse Dynamics Model (IDM) Execution Fidelity** — Whether actions extracted from video demonstrations via inverse dynamics.
- ● **Real-to-Sim Consistency** — Whether identical manipulation trajectories yield consistent outcomes (success or failure) across real-world execution and simulation environments with reconstructed scenes.
- ● **Task Success Variance by Embodiment Type** — Performance differential between world models on human-hand vs.
- ○ **Comparison with Visual Plausibility Baseline (PAI-Bench Domain Score)** — How RoboWM-Bench execution accuracy compares to perceptual plausibility scores from PAI-Bench (a vision-only metric assessing visual quality).

**[WorldArena 2.0](https://arxiv.org/abs/2605.17912)** · 📑 0 — WorldArena 2.0 comprehensively evaluates embodied world models across three dimensions.
- ⭐ **Task Success Rate (Visuotactile Downstream)** — Percentage of manipulation tasks successfully completed using tactile predictions from the world model.
- ⭐ **Policy Success Rate (RL as Environment)** — Percentage of task episodes where a reinforcement learning policy trained with a world model as environment achieves the goal on real-world or simulated robot platforms.
- ⭐ **Task Success Rate: Data Engine** — Percentage of successful task completions when world model generates synthetic trajectories for downstream policy training.
- ⭐ **Task Success Rate: Action Planner** — Percentage of successful task completions when world model is used as an action planning environment (model-based planning via imagination rollouts).
- ⭐ **PSNR (Peak Signal-to-Noise Ratio)** — Pixel-level fidelity of predicted tactile deformation maps compared to ground-truth tactile sensor readings.
- ⭐ **SSIM (Structural Similarity Index)** — Perceptual structural consistency between predicted and ground-truth tactile observations.
- ● **Policy Training Convergence (Environment Steps)** — Number of world-model environment interaction steps required for a policy trained on world-model rollouts to reach a target success rate.
- ● **Reward Model Variant Performance** — Compares three reward function designs (proxy-based, VLM-based, similarity-based) for their impact on policy success in the RL pipeline.
- ● **Cross-Platform Correlation (Pearson r)** — Consistency of metric rankings across different platforms (RoboTwin simulator, LIBERO simulator, real-world AgilexX).
- ○ **Video Quality: Interaction Quality** — Realism and physical plausibility of hand-object or object-object interactions shown in predicted video.
- ○ **Video Quality: Trajectory Accuracy** — Accuracy of object or end-effector path prediction over time.
- ○ **Video Quality: Motion Smoothness** — Temporal consistency of motion across consecutive frames.
- ○ **Video Quality: Subject Consistency** — Whether predicted video maintains visual identity and continuity of objects across frames.
- ○ **Video Quality: Flow Score** — Smoothness and physical plausibility of optical flow in predictions.
- ○ **Video Quality: Image Quality (JEPA Similarity)** — Semantic visual quality of generated video frames via JEPA embeddings.
- ○ **Video Quality: Depth Accuracy** — Correctness of 3D spatial layout and depth relationships in predicted frames.
- ○ **Video Quality: Aesthetic Quality** — Overall visual pleasing appearance and absence of artifacts (blur, noise, distortion) in generated frames.
- ○ **Video Quality: Instruction Following (Controllability)** — Whether predicted video obeys task-specific instructions or actions provided as input (e.g., 'Click the bell').
- ○ **Video Quality: Photometric Consistency** — Stability of lighting, color, and brightness across frames.
- ○ **Video Quality: Dynamic Degree** — Magnitude and frequency of motion content in video.
- ○ **Video Quality: Background Consistency** — Preservation of static background elements (walls, table surfaces) across predicted frames.
- ○ **Video Quality: Perspectivity** — Correctness of perspective geometry and vanishing points in predicted frames.
- ○ **Video Quality: Semantic Alignment** — Consistency between predicted video content and semantic object/action labels.
- ○ **Video Quality: Action Response Sensitivity** — Sensitivity of predicted video to action/control inputs.

---

## Physics-Centric

**[VideoPhy-2](https://arxiv.org/abs/2503.06800)** · 📑 90 — VideoPhy-2 measures how well video generation models produce videos that satisfy two independent but jointly difficult constraints: accurately depicting text-prompt semantics while obeying real-world physics laws.
- ⭐ **Joint Performance (SA≥4 ∩ PC≥4)** — Percentage of videos achieving high semantic adherence AND high physical commonsense simultaneously.
- ⭐ **Semantic Adherence (SA)** — Whether entities, actions, and spatial relationships specified in the text prompt are correctly depicted in the generated video.
- ⭐ **Physical Commonsense (PC)** — Whether generated videos respect real-world physics laws and intuitive physical behavior, independent of prompt semantics.
- ● **Physical Rules Violation (PR)** — Fine-grained binary detection of whether specific physical laws (e.g., conservation of mass, momentum, reflection, buoyancy) are violated or respected in individual videos.
- ○ **VideoPhy-2-AutoEval (Automatic Evaluator Pearson Correlation)** — How well an automatic VLM-based evaluator correlates with human annotation judgments.

**[PhyWorld](https://arxiv.org/abs/2605.19242)** · 📑 0 — PhyWorld benchmarks video generation models on their ability to simulate realistic physics and coherent visual dynamics.
- ⭐ **Physical-Temporal Validity (PTV)** — Adherence to realistic physical dynamics and temporal causality.
- ⭐ **Overall Physics Benchmark Score** — Composite score combining general quality dimensions and physics-specific adherence across seven physical-law categories.
- ⭐ **Semantic Alignment (SA)** — How well the generated video content matches the semantic intent and description in the input prompt.
- ⭐ **Solid-Body Physics** — Correctness of rigid object interactions.
- ⭐ **Fluid Dynamics** — Correctness of liquid behavior.
- ⭐ **Optical Phenomena** — Accuracy of shadows and reflections.
- ● **Motion Smoothness (VBench)** — Fluidity and continuity of motion transitions between frames.
- ● **Persistence** — Retention of visual attributes and coherent motion.
- ● **Subject Consistency (VBench)** — How stably and consistently main objects/subjects remain identifiable and maintain their visual appearance across all frames of the generated video.
- ● **Background Consistency (VBench)** — Stability and coherence of the environmental/background elements in the scene, ensuring the backdrop does not flicker, shift unexpectedly, or violate spatial continuity.
- ○ **Imaging Quality (VBench)** — Technical video quality including resolution clarity, absence of artifacts, blur, noise, or compression distortions.
- ○ **Dynamic Degree (VBench)** — Quantifies the overall activity level and temporal variation in the generated scene.
- ○ **Aesthetic Quality (VBench)** — Visual appeal, composition, lighting, and overall artistic quality of the generated video.
- ○ **VBench Composite Score** — Average of all six VBench video quality dimensions.

**[PhyWorldBench](https://arxiv.org/abs/2507.13428)** · 📑 14 — PhyWorldBench evaluates whether AI text-to-video models generate videos that respect real-world physics and semantic content, combining human judgment with automated multimodal LLM evaluation to measure physical realism in generated videos.
- ⭐ **Semantic Adherence (SA)** — Whether generated videos correctly depict the objects and actions described in the prompt.
- ⭐ **Physical Commonsense (PC)** — Whether generated videos obey real-world physics laws and exhibit key physical phenomena that should naturally occur in the real scenario (e.g., objects fall due to gravity, friction slows motion, collisions produce realistic responses).
- ⭐ **Both (SA ∧ PC)** — Joint satisfaction of both semantic adherence AND physical commonsense simultaneously.
- ● **Context-Aware Prompt (CAP) Evaluation** — Automated zero-shot assessment of whether a video exhibits correct semantics and physics, using a multimodal LLM as a judge instead of humans.
- ● **ROC-AUC (Receiver Operating Characteristic Area Under Curve)** — How well an automated evaluator (CAP) distinguishes between videos that satisfy the criterion (SA or PC) versus those that don't, compared to human judgments.
- ○ **Precision and Recall** — False positive and false negative rates of automated evaluation.

**[ScenePhys](https://neurips.cc/virtual/2025/loc/san-diego/123993)** · 📑 n/a — The benchmark measures whether video understanding models can demonstrate genuine physics reasoning across diverse domains (mechanics, optics, electromagnetism, quantum mechanics) rather than relying on surface-level visual pattern matching.
- ⭐ **Numerical Score (Deterministic Grading)** — Accuracy of extracting and calculating quantitative physics values from video frames.
- ⭐ **Conceptual Score (LLM-Judged Rubric, 1-5 Scale)** — Understanding of qualitative physics principles, causal reasoning, and conceptual knowledge.
- ● **Error-Detection Score (LLM-Judged Rubric, 1-5 Scale)** — Ability to identify physics violations and misconceptions in video scenarios.
- ○ **Domain-Specific Weak Classifier Sanity Check** — Whether question categories (mechanics, optics, electromagnetism, quantum) form distinct clusters in feature space.

**[Newton](https://openreview.net/forum?id=xlp6P6qaRW)** · 📑 n/a — Newton evaluates foundation world models' ability to understand interactive environments through object permanence (via occlusion and viewpoint changes) and physical dynamics (via rigid body interactions), measuring both long-context memory retention and physics simulation accuracy.
- ⭐ **Trajectory RMSE - Motion Path Accuracy** — How accurately a world model predicts an object's motion trajectory over time in physics simulations.
- ⭐ **Final Position Error (FPE) - End-State Accuracy** — Whether a model correctly predicts where an object ends up after a physics interaction completes.
- ⭐ **Mask Intersection-over-Union (mIoU) - Object Detection** — How accurately a world model predicts object locations and boundaries in occluded and rotated scenarios.
- ● **Action Following Accuracy - Instruction Compliance** — Whether a world model correctly executes and simulates the consequences of specified actions (e.g., applying force, rotating objects).
- ● **Physics Plausibility Rating - Realism Score** — Subjective or automated assessment of whether predicted physics behaviors are realistic and follow natural laws (no unphysical artifacts like objects moving without force, intersecting, or defying gravity).
- ● **Gravity Estimation Accuracy - Physical Law Discovery** — Whether a model implicitly learns and applies Newtonian gravity constants.
- ○ **Mask Centroid Distance - Center of Mass Accuracy** — How precisely a model locates the center point of objects in 3D space despite occlusion.
- ○ **Object Permanence Success Rate - Occlusion Recall** — Percentage of test cases where a model correctly recalls and maintains object identity/position despite prolonged occlusion or camera rotation.
- ○ **Background RMSE - Environmental Consistency** — How well a model preserves static background elements across predicted frames.

**[Morpheus](https://arxiv.org/abs/2504.02918)** · 📑 36 — Morpheus evaluates whether video generation models can generate physically plausible videos that obey conservation laws and governing equations of motion, identifying a critical gap between aesthetic quality and physical reasoning in current VGMs.
- ⭐ **Dynamical Score** — Overall adherence to the equations of motion governing the physical system.
- ⭐ **Physical Invariance Score** — Preservation of system-specific conserved quantities (energy, momentum, angular displacement, acceleration) that should remain constant over the entire video sequence according to conservation laws.
- ● **Discard Rate (DR)** — The fraction of generated videos that fail basic validity checks and cannot be reliably analyzed.
- ● **Energy Conservation (Specific Invariant)** — Whether total mechanical energy E = ½m(vₓ² + vᵧ²) + mgy remains constant throughout the sequence, as required by physics for isolated systems.
- ● **Momentum Conservation (Specific Invariant)** — Whether linear momentum components (pₓ and pᵧ) or total momentum remain constant over time, as required for closed systems without external net force.
- ○ **Acceleration Uniformity (Specific Invariant)** — Whether acceleration of an object remains constant as required by physics, e.g., a_y = g (gravitational acceleration) for freely falling objects in uniform gravity.

**[Physics-IQ](https://arxiv.org/abs/2501.09038)** · 📑 110 — Physics-IQ measures how well video generation models understand physical principles by evaluating whether generated videos correctly depict the spatial location, timing, intensity, and pixel-level fidelity of physical phenomena across domains like fluid dynamics, optics, and mechanics.
- ⭐ **Physics-IQ Score (Composite)** — Holistic physical understanding by combining spatial accuracy, temporal alignment, motion intensity, and pixel fidelity into a single normalized score.
- ⭐ **Spatiotemporal IoU** — Whether physical action happens at both the correct spatial locations AND correct times.
- ● **Weighted Spatial IoU** — Both the location and intensity/duration of motion patterns.
- ● **Spatial IoU (Intersection over Union)** — Whether physical action occurs in the correct spatial locations, independent of when it happens.
- ● **Mean Squared Error (MSE)** — Pixel-level visual fidelity and physical plausibility of object appearance.
- ○ **MLLM Evaluation (Gemini 1.5 Pro as Judge)** — Visual realism and perceptual quality, independent of physics.

**[PhysBench](https://arxiv.org/abs/2501.16411)** · 📑 119 — PhysBench measures vision-language models' ability to understand physical properties, relationships, scene dynamics, and physics-based reasoning through multiple-choice questions on video and image data.
- ⭐ **Overall Accuracy** — Percentage of correct answers on multiple-choice questions (4 options per question) across the full 10,002-entry test set.
- ⭐ **Category-Specific Accuracy (Property, Relationships, Scene, Dynamics)** — Accuracy broken down by four major physical understanding domains: (1) Physical Object Properties (mass, density, friction, etc.), (2) Object Relationships (spatial positions, movements), (3) Physical Scene Understanding (multi-object interactions), (4) Physics-Based Dynamics (motion prediction, physics simulation outcomes).
- ● **Embodied Task Success Rate (Robotic Manipulation)** — Percentage of successfully completed physical manipulation tasks in MuJoCo simulation when using model predictions (with and without fine-tuning on PhysBench data).
- ● **Capability Dimension Performance (8 Distinct Dimensions)** — Accuracy across 8 capability dimensions capturing different reasoning types (e.g., single-object reasoning, multi-object reasoning, temporal reasoning, causal reasoning).
- ● **Sub-task Performance (19 Subclasses)** — Accuracy on 19 distinct sub-categories nested within the four major domains (examples: 'object mass estimation', 'friction prediction', 'collision outcomes').
- ● **Prompting Strategy Improvement (Accuracy Delta)** — Absolute accuracy improvement when applying reasoning-enhancement prompts (Chain of Thought, Descriptive CoT, Pure Language Reasoning) compared to baseline direct prediction.
- ○ **Error Type Classification Distribution (6 Categories)** — Proportion of model errors falling into six human-identified categories: Perception errors (misidentifying visual features), Reasoning errors (logical mistakes), Knowledge gaps (missing physical understanding), Refusal to answer, Instruction-following failures, and Annotation errors in dataset.
- ○ **Correlation with Other Benchmarks** — Spearman or Pearson correlation coefficient between model's PhysBench performance and performance on 15 other vision-language benchmarks (e.g., MMVP, MMBench).
- ○ **Scaling Analysis (Model Size / Data Quantity / Frame Count Effects)** — How performance changes with model size (parameters), amount of training data (PhysBench sample count), and video frame density (number of frames per video sample).

**[PhyGenBench](https://arxiv.org/abs/2410.05363)** · 📑 128 — PhyGenBench measures whether generated videos faithfully depict physical phenomena with correct semantics and realistic commonsense physics, using a three-stage hierarchical framework that combines VLM-based evaluation with human validation.
- ⭐ **Physical Commonsense Alignment (PCA) - Composite 4-Point Score** — Integrated measure of physical correctness combining all three stages (key phenomena detection, temporal ordering, and naturalness) into a single 0-3 scale score representing overall physical commonsense quality.
- ⭐ **Key Physical Phenomena Detection (Stage 1 of PCA)** — Whether the video successfully depicts the critical physical phenomena that are central to the prompt.
- ⭐ **Physics Order Verification (Stage 2 of PCA)** — Whether physical events occur in the correct causal and temporal sequence.
- ⭐ **Overall Naturalness Evaluation (Stage 3 of PCA)** — Whether the physical progression of the entire video aligns with realistic real-world physics and natural motion dynamics, independent of specific keyframes.
- ● **Semantic Alignment (SA)** — Whether generated videos contain the correct objects and actions described in the input prompt.
- ● **Physics Domain-Specific PCA Scores (Mechanics, Optics, Thermal, Material Properties)** — Physical commonsense alignment broken down by physics category to identify which physical domains models struggle with most.
- ○ **Kendall's Tau (τ) Correlation with Human Judgment** — Statistical rank-order agreement between automated PhyGenEval scores and human expert evaluation.
- ○ **Spearman's Rho (ρ) Correlation with Human Judgment** — Statistical monotonic rank-order agreement between automated PhyGenEval scores and human evaluation.

**[Physion-Eval](https://arxiv.org/abs/2603.19607)** · 📑 2 — Quantifying human-detectable physical plausibility gaps in AI-generated videos by measuring perception, explicit violations, and machine critic reliability across perceptual and annotation-based dimensions.
- ⭐ **Failure Rate** — The proportion of generated videos that contain at least one human-identifiable physical glitch (unrealistic violation) detectable by experts.
- ⭐ **Glitch Density** — The average count of distinct physical violations per generated video, capturing how dense or frequent failures are within a single clip.
- ⭐ **Glitch Classification (Taxonomy-based)** — Categorization of failure types into a structured taxonomy, identifying which classes of physical laws are most frequently violated (e.g., contact violations, object permanence, causal logic).
- ⭐ **Youden's J Statistic (JG)** — The perceptual degradation gap: how much less realistic AI-generated videos appear compared to real videos, as judged by human viewers on a perceived realism scale.
- ● **Glitch Severity** — The subjective magnitude or severity of individual physical violations, rated on a structured scale from minor (barely noticeable) to major (obviously impossible).
- ● **Binary Realism Detection (MLLM Critic)** — Whether a multimodal large language model (MLLM) can correctly classify a video as 'REALISTIC' or 'UNREALISTIC' when compared to human ground truth judgments.
- ● **Physical Intensity Score** — The magnitude or energy level of the dominant physical process(es) in a video, ranging from low (stationary objects) to high (violent collisions, rapid motion).
- ● **Dynamics Score** — The temporal activity or rate of change within a video, capturing whether the scene is quasi-static (little motion) or highly dynamic (rapid, continuous change).
- ○ **Temporal Glitch Localization** — The precise timing or frame range within the video where a physical violation occurs, enabling granular failure analysis.
- ○ **Temporal Mislocalization Error (MLLM Critic)** — The disagreement between MLLM-predicted failure timestamps and human-verified ground-truth timestamps, indicating whether the model can pinpoint when violations occur.
- ○ **Reasoning Accuracy (MLLM Critic)** — The validity and causal soundness of the explanations MLLMs provide for why a glitch occurred, assessed by expert comparison.

**[PhyGround](https://arxiv.org/abs/2605.10806)** · 📑 0 — A benchmark for evaluating whether text-to-video generation models produce videos that obey physics laws across solid-body mechanics, fluid dynamics, and optical domains, using human annotations with both expert review and automated VLM judging.
- ⭐ **Per-Law Physics Score (Likert 1-5)** — How well individual physics laws (13 total: 6 solid-body, 5 fluid, 2 optical) are obeyed in generated videos.
- ⭐ **Overall Composite Score** — Blended summary metric combining general physical adherence dimensions (SA, PTV, persistence) and domain-specific physics laws.
- ⭐ **Semantic Alignment (SA)** — Whether video content actually matches the text prompt provided to the generative model.
- ⭐ **Physical Temporal Validity (PTV)** — Whether the sequence of physical events unfolds plausibly in time.
- ⭐ **Object Persistence** — Consistency of objects' visual appearance, shape, and continued existence throughout the video.
- ● **Domain Aggregation Score (Solid-Body, Fluid, Optical)** — Overall physics plausibility within each major physics domain by averaging applicable domain-specific laws.
- ● **Aggregate Relative Bias (VLM Judge Accuracy)** — Accuracy of an automated Vision-Language Model judge (PhyJudge-9B) compared to human mean scores.
- ● **Signed Relative Bias (VLM Judge Directionality)** — Systematic direction of judge error: whether an automated judge tends to overestimate or underestimate physics plausibility relative to humans.
- ○ **Split-Half Ranking Correlation (Spearman ρ, Kendall τ-b)** — Stability and reliability of model rankings: whether splitting the 352 annotators into random halves produces consistent model orderings, indicating the benchmark is not noisy or unstable.
- ○ **Pairwise Preference Agreement** — Inter-annotator consistency on relative model comparisons: how often two annotators agree on which of two models produces a better video.
- ○ **Peer Mean Absolute Error (MAE)** — Average magnitude of disagreement between individual annotators and the mean annotator score.
- ○ **Score Constancy Filter (Annotator Quality Control)** — Whether an annotator discriminates between videos/dimensions or gives repetitive responses.
- ○ **Per-Video Copy-Paste Rate (Annotator Quality Control)** — Detection of annotators assigning identical scores across all dimensions for the same video.
- ○ **Annotator Subsampling Stability (Robustness to Pool Size)** — How much score variance decreases when more annotators are included.

**[VisPhyWorld](https://arxiv.org/abs/2602.13294)** · 📑 1 — VisPhyWorld evaluates whether large multimodal language models can jointly reconstruct plausible 3D scene geometry and simulate physically accurate dynamics from single images, combining pixel-level reconstruction quality, semantic consistency, motion fidelity, and holistic perceptual plausibility judgments.
- ⭐ **Gemini Judge (Gemini-2.5-Pro Video Evaluator)** — Holistic perceptual and physical plausibility judgment by a vision-language model, assessing visual quality, motion realism, collision consistency, and contact dynamics on a 1–10 scale.
- ⭐ **RAFT-EPE (Optical Flow End-Point Error)** — Optical flow discrepancy between reconstructed and ground-truth motion, quantifying how accurately the model simulates frame-to-frame object motion.
- ⭐ **LPIPS (Learned Perceptual Image Patch Similarity)** — Perceptual distance between images using deep learned features, capturing human-perceived visual quality rather than pixel-level metrics.
- ⭐ **PSNR (Peak Signal-to-Noise Ratio)** — Frame-by-frame pixel-level fidelity between reconstructed video frames and ground truth, measuring how closely the reconstructed color values match the original.
- ⭐ **SSIM (Structural Similarity Index)** — Local structural similarity between reconstructed and ground-truth frames, capturing luminance, contrast, and structure preservation better than raw pixel differences.
- ● **Temporal Offset Estimation & Frame Alignment** — Automatic detection and correction of synchronization misalignment between reconstructed and ground-truth videos, ensuring fair flow metric comparison when timing differs.
- ● **CLIP-Img (CLIP Image-to-Image Similarity)** — Semantic and visual consistency between reconstructed frames and ground truth using CLIP's pre-trained vision encoder, ensuring objects and scene layout are recognized similarly.
- ● **DINO (Self-Supervised Vision Transformer Features)** — Object identity and visual correspondence preservation using self-supervised features, detecting whether the same objects in the scene remain recognizable in reconstructions.
- ○ **BERTScore-F1 (Semantic Similarity of Text Analysis)** — Semantic similarity between the model's generated motion analysis and reference descriptions, using contextual embeddings to detect paraphrases and synonym use.
- ○ **CLIP-Cap (Text-to-Image Consistency via CLIP)** — Alignment between the model's generated motion analysis description and the actual reconstructed video frames, ensuring semantic descriptions match observed motion.
- ○ **ROUGE-L F1 (Lexical Overlap in Text Analysis)** — Lexical and structural overlap between the model's generated motion analysis text and reference descriptions, capturing word-level agreement.
- ○ **Pipeline Success Rate / Code Validity** — Percentage of benchmark samples for which the model's generated code successfully produces valid reconstructed videos without runtime errors or fallback.

**[WorldBench](https://arxiv.org/abs/2601.21282)** · 📑 5 — Assesses how accurately world models predict physical object dynamics and understand physics laws by measuring both intuitive physics concepts (object permanence, support relations) and low-level physical parameters (gravity, friction, viscosity).
- ⭐ **Foreground mIoU (Mean Intersection over Union)** — Accuracy of predicted object segmentation and dynamics.
- ⭐ **Motion Physics Concept Score (mIoU aggregated)** — Performance specifically on scenarios involving forces, kinematics, and dynamics (gravity, friction effects on trajectories).
- ● **Background RMSE (Root Mean Squared Error)** — Consistency of static scene background.
- ● **Object Permanence Concept Score (mIoU aggregated)** — Performance on tasks where objects are occluded or hidden, testing whether the model understands objects continue to exist out-of-view.
- ● **Support Relations Concept Score (mIoU aggregated)** — Performance on tasks requiring understanding of physical support, stability, and contact forces (e.g., which objects can stack, what happens when support is removed).
- ● **Scale/Perspective Relations Concept Score (mIoU aggregated)** — Performance on tasks requiring understanding of camera viewpoint effects: objects appear larger when close, smaller when far.
- ○ **Gravitational Acceleration Estimation (m/s²)** — Accuracy of inferred gravitational acceleration from object motion trajectories.
- ○ **Friction Coefficient Estimation** — Accuracy of inferred friction μ from object sliding down ramps.
- ○ **Fluid Viscosity Estimation (Pa·s)** — Accuracy of inferred fluid viscosity from object terminal velocity in viscous medium.
- ○ **Language QA Accuracy (%)** — Physics reasoning capability via natural language.

**[PhysicsMind](https://arxiv.org/abs/2601.16007)** · 📑 1 — PhysicsMind measures whether AI models can reason about and predict outcomes of basic physics scenarios (center of mass, lever equilibrium, Newton's first law) via video understanding and generation tasks.
- ⭐ **VQA Exact-Match Accuracy** — Binary accuracy of model predictions in video question-answering tasks, where the model must select the correct answer from ground-truth options about physical quantities or outcomes.
- ⭐ **Lever Equilibrium Final State Accuracy** — Whether the generated video sequence converges to the physically correct lever outcome (balanced, left-heavy, or right-heavy) implied by torque balance equations.
- ⭐ **Trajectory RMSE (Newton's First Law)** — Deviation of predicted motion trajectory from ground-truth, normalized by trajectory scale, capturing overall path accuracy.
- ⭐ **Final Position Error (FPE)** — Endpoint accuracy in video generation, measuring absolute distance between predicted final position and ground-truth final position.
- ⭐ **Segmentation Mask IoU (Video Generation)** — Geometric fidelity of generated video frames, measuring overlap between predicted object masks and ground-truth masks.
- ● **Category-wise Accuracy** — Performance breakdown by physics law subcategories, revealing which specific physical principles the model masters or struggles with.
- ● **Experiment-wise Accuracy** — Aggregated accuracy across different physical setups and configurations, identifying which experimental conditions are easier or harder for the model.
- ● **Speed Similarity** — Consistency of velocity magnitude in generated motion, ensuring predicted speeds match ground-truth speed profile over time.
- ● **Acceleration Similarity** — Accuracy of acceleration profile in generated motion, ensuring predicted accelerations match ground-truth (e.g., zero acceleration for uniform motion, constant negative for friction-induced deceleration).
- ● **Directional Consistency** — Preservation of velocity direction in generated motion, ensuring the model maintains correct heading/trajectory direction throughout the sequence.
- ○ **Variant-wise Accuracy** — Robustness testing by varying object appearance (colors, textures, materials), mass distributions, and motion profiles, ensuring model generalizes beyond training visual patterns.
- ○ **Segmentation Mask Center Distance** — Accuracy of the object's center-of-mass position in generated frames, measuring distance between predicted and ground-truth mask centroids.

---

## Other / Workshop

**[OpenGVL](https://arxiv.org/abs/2509.17321)** · 📑 3 — OpenGVL benchmarks vision-language models' ability to predict task progress in robotic manipulation by assessing whether their numerical completion estimates respect the true temporal order of frames presented out-of-sequence.
- ⭐ **Value-Order Correlation (VOC)** — How well a model's predicted task completion scores align with the true temporal order of video frames.
- ⭐ **Model Scaling Analysis (Parameter Count Sensitivity)** — How task progress prediction improves with model size.
- ⭐ **Hidden Evaluation Task Performance (Sub-millimeter Precision Assembly)** — Model robustness on novel, out-of-distribution tasks requiring precision-critical predictions.
- ● **Conditioning Scenario Ablation (Zero-shot vs. Two-shot)** — Whether models improve with task context examples, and by how much.
- ● **Dataset-Level Performance Variance** — How model performance generalizes across distinct robotic manipulation tasks with different embodiments and visual characteristics.
- ○ **Open-source vs. Closed-source Performance Ratio** — The relative competitive gap between open-source VLMs (Gemma, Qwen, MiMo) and proprietary models (GPT-4o, Gemini-2.5-Pro).

**[AetherVision-Bench](https://arxiv.org/abs/2506.03709)** · 📑 1 — The benchmark measures the robustness of open-vocabulary semantic segmentation models across multiple challenging real-world conditions (viewing angles, sensor modalities) to assess whether models generalize for embodied AI applications in autonomous navigation systems.
- ⭐ **Mean Intersection over Union (mIoU)** — The average pixel-level segmentation accuracy across all semantic classes.
- ● **Viewing Angle Generalization Performance** — The segmentation accuracy when models trained on one viewing perspective are evaluated on different viewing angles (bird's-eye, slant-angle, ground-level).
- ● **Cross-Modal Performance Gap (RGB vs. Infrared)** — The relative degradation in segmentation accuracy when models are evaluated on infrared imagery compared to RGB imagery under identical training and testing conditions.
- ○ **Domain Shift Robustness (Training Dataset Impact)** — The relative performance consistency when models trained on standard large-scale datasets (COCO-Stuff) are evaluated on smaller, specialized datasets compared to evaluation on the training distribution.

---
