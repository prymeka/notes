# Learn by Building — A Project Companion to Both AI/ML Curricula

*For every section of the two curricula ("From Strong Baseline to the Frontier," Phases A–G; and "From Practitioner to Expert: Fraud Prevention," Phases H–P), this document gives a few concrete projects that turn the reading into understanding. The organizing conviction — matched to how you learn — is **implement from scratch first, reproduce a paper second, extend/contribute third**. A concept you have coded from first principles and then broken on purpose is a concept you own.*

## How to use this

Each project is one to three sentences: what to build and what it teaches. Pick by depth and goal using the tags:

- **[quick]** — hours to a day; a single idea made concrete.
- **[medium]** — several days; a real implementation or reproduction.
- **[deep]** — one to two+ weeks; a substantial build worth keeping.
- **[stack]** — connects directly to, or is reusable in, your PayPal fraud work.
- **[portfolio]** — a strong standalone artifact worth publishing internally or externally.

Within a section, projects are roughly ordered easiest-first. You do **not** need to do all of them — one from-scratch build plus one reproduction per section is enough to internalize it. The cross-cutting projects in Part 3 deliberately fuse the two curricula and are the highest-leverage things you can build given your role.

---

# Part 1 — Frontier AI/ML (Curriculum 1, Phases A–G)

## Phase A — Rigorous Mathematical Foundations

The math phases are proof-first, but every one of them has a computational shadow that makes the abstraction tangible. Build the shadow.

### A1 — Real Analysis
- **Counterexample zoo** — Implement and visualize the pathologies that motivate rigor: the Weierstrass function (continuous, nowhere differentiable), a sequence of functions converging pointwise but not uniformly, and a rearrangement of a conditionally convergent series that changes its sum. Seeing them removes the "why do we need epsilons" question permanently. [quick]
- **Completeness by its absence** — Construct a Cauchy sequence of rationals converging to √2 and watch it fail to converge *within* ℚ; then do it in ℝ. Makes completeness a fact you've felt, not memorized. [quick]
- **(Optional) Formalize in Lean 4** — Prove a handful of Rudin results (Bolzano–Weierstrass, or the intermediate value theorem) in a proof assistant. Forces total rigor and is excellent training for reading formal ML-theory papers. [medium]

### A2 — Linear Algebra & Matrix Analysis
- **SVD from scratch → image compression** — Implement SVD (via eigendecomposition of AᵀA, or Golub–Kahan bidiagonalization), then prove and empirically verify the Eckart–Young theorem by low-rank image compression, plotting reconstruction error vs. rank. This is the exact structure behind LoRA (D4) and PCA-based drift monitoring. [medium][stack]
- **Mini numerical-linear-algebra library** — Implement Gram–Schmidt vs. Householder QR, and power iteration for the top eigenpair; compare numerical stability. [medium]
- **Conditioning experiment** — Perturb a linear system and measure error amplification vs. the condition number; connect matrix norms to why some networks are hard to train. [quick]

### A3 — Measure-Theoretic Probability
- **Martingale simulator + optional stopping** — Simulate a fair-game martingale (gambler's fortune) and empirically test the optional stopping theorem; then break it with an unbounded stopping time to see the hypotheses bite. [quick]
- **σ-algebra on a finite space** — Build a small finite probability space, enumerate a σ-algebra, and implement conditional expectation as projection onto a sub-σ-algebra. Makes "measurability" and "conditioning" concrete objects. [quick]
- **Importance sampling and its failure** — Implement importance sampling, then show its variance explode when the proposal has thinner tails than the target. [medium]

### A4 — High-Dimensional Probability & Concentration
- **Tail-bound tightness map** — Sample means of bounded random variables and plot empirical deviation probabilities against Hoeffding and Bernstein bounds; find where each is tight vs. loose. Builds intuition for how many samples a bound really needs. [quick]
- **Johnson–Lindenstrauss random projection** — Implement random projection into lower dimension and verify pairwise-distance preservation on high-dimensional data; connect directly to why embeddings work. [medium]
- **Matrix Bernstein in action** — Sum random matrices and watch the spectral norm concentrate; relate to covariance estimation and the sample complexity of your fraud features (effective sample size = fraud count). [medium][stack]

### A5 — Optimization Theory
- **Rates, verified** — Implement gradient descent, heavy-ball momentum, and Nesterov acceleration on a strongly convex quadratic; verify the convergence rates match theory and visualize the trajectories. Then confirm Nesterov's provable speedup is real. [medium]
- **Mirror descent on the simplex** — Implement mirror descent with the entropy mirror map (multiplicative weights) and compare its geometry to projected GD; feel what changing the Bregman divergence buys you. [medium]
- **Non-convex landscape tour** — Optimize the Rosenbrock function and a 2-layer-net loss; observe saddle points, plateaus, and initialization sensitivity — the phenomena Phase E tries to explain. [quick]

### A6 — Functional Analysis + RKHS
- **Kernel ridge regression from scratch** — Implement KRR, visualize the effect of different kernels, and demonstrate the representer theorem (the solution lives in the span of the data). The RKHS becomes a concrete object. [medium]
- **Gaussian process → infinite-width preview** — Build a GP from scratch; then note its equivalence to an infinite-width network, setting up the NTK in Phase E. [medium]

### A7 — Information Theory
- **Build a compressor** — Implement Huffman or arithmetic coding and empirically confirm you can't beat the Shannon entropy bound; try to, and watch it fail. [medium]
- **ELBO on a toy latent model** — Derive and implement a variational bound on a small latent-variable model; this same KL-regularized structure reappears in DPO and RLHF (D3). [medium][stack]
- **Mutual information estimator** — Estimate MI between correlated variables and compare estimators; connect to feature selection and information bottleneck ideas. [quick]

## Phase B — Statistical Learning Theory

- **Fit random labels (the Zhang et al. experiment)** — Train a small MLP to 100% accuracy on randomly relabeled data while test accuracy stays at chance. The single cleanest demonstration that classical capacity bounds are vacuous for deep nets — do this early, it reframes everything. [medium][portfolio]
- **Estimate Rademacher complexity** — Empirically estimate the Rademacher complexity of linear predictors and compare it to the observed generalization gap; see where the bound is informative and where it isn't. [medium]
- **Shattering demo** — Implement a hypothesis class and show it shattering (and failing to shatter) point sets; compute the growth function to make VC dimension concrete. [quick]

## Phase C — Deep Learning Foundations

- **Micrograd → MLP** — Build a scalar reverse-mode autodiff engine from scratch, then an MLP on top; verify every gradient against finite differences. Backprop stops being magic. [medium]
- **Backprop a CNN by hand** — Implement convolution forward/backward without a framework and train on MNIST/CIFAR; you'll never misremember the chain rule again. [medium]
- **Initialization/normalization ablation** — Measure gradient variance across depth with Xavier vs. He init, and with/without BatchNorm and residual connections; reproduce the variance-preservation argument. [medium]
- **VAE, then a tiny DDPM** — Implement a variational autoencoder, then a minimal denoising diffusion model on MNIST; grounds the probabilistic/generative view before transformers. [deep]

## Phase D — Transformers & LLMs

### D1 — Architecture
- **Attention from scratch → nanoGPT** — Implement scaled dot-product and multi-head attention by hand, assemble a full GPT, and train a character-level model. The foundational build of the whole curriculum. [deep][portfolio]
- **Positional-encoding ablation** — Swap sinusoidal vs. learned vs. RoPE positional encodings in your GPT and measure the difference, including length extrapolation. [medium]
- **Architecture knobs** — Ablate pre-norm vs. post-norm and SwiGLU vs. ReLU MLPs; reproduce why the modern defaults won. [medium]

### D2 — Scaling & Pretraining
- **Mini-Chinchilla** — Train a family of tiny models across sizes and token budgets, fit a scaling law to the loss, and locate the compute-optimal frontier; test the ~20-tokens-per-parameter heuristic at small scale. [deep][portfolio]

### D3 — Post-training / Alignment
- **DPO from scratch** — Derive the DPO loss from the KL-regularized reward objective (using your A7 information theory), implement it, and fine-tune a small model on a preference set. [medium][portfolio]
- **Toy GRPO/PPO on a verifiable task** — Build a minimal RL-from-verifiable-rewards loop that trains a small model to do arithmetic, rewarding correct answers; the RLVR idea in miniature. [deep]

### D4 — Parameter-Efficient Fine-Tuning
- **LoRA from scratch** — Inject low-rank adapters into the linear layers of your nanoGPT, freeze the base, and compare quality vs. trainable-parameter count against full fine-tuning; then try a 4-bit quantized base (QLoRA-style). Uses your A2 low-rank intuition directly. [medium]

### D5 — Mixture-of-Experts
- **Sparse MoE layer** — Implement a top-k gated MoE layer with a load-balancing auxiliary loss; measure expert utilization and show what happens to balance when you remove the aux loss. [medium]

### D6 — Long-Context
- **RoPE scaling + needle-in-a-haystack** — Implement NTK-aware/YaRN RoPE scaling and evaluate context extrapolation on a synthetic long-context retrieval task; then implement a blockwise (ring-style) attention pass. [deep]

### D7 — Emergent Abilities (the debate)
- **Manufacture and erase "emergence"** — Take one capability, evaluate it across model sizes with a discontinuous metric (exact match) and a smooth surrogate, and show how the metric choice alone creates or removes the apparent emergent jump. Reproduces the Schaeffer et al. critique with your own hands — the best possible way to internalize how to read the field. [medium][portfolio]

## Phase E — ML / Deep Learning Theory

- **Empirical NTK** — Compute the empirical neural tangent kernel of a small net and track its drift during training; compare a very wide net (lazy/stable NTK) to a narrow one (feature learning). See exactly where the theory holds and where it breaks. [deep]
- **Double descent curve** — Sweep model width (or ridge parameter) and plot test error to reveal the interpolation-threshold peak and the second descent. A clean phase-transition experiment you can relate to statistical mechanics. [medium][portfolio]
- **Grokking on modular arithmetic** — Reproduce grokking: train far past overfitting on modular addition and watch validation accuracy suddenly jump; then probe the learned Fourier-feature circuit. [deep][portfolio]
- **Lottery ticket** — Implement iterative magnitude pruning, extract a winning ticket, and test the rewind-to-initialization claim vs. reinitialization. [medium]
- **Implicit bias of GD** — Train logistic regression on separable data and show gradient descent converges to the max-margin solution (compare against an SVM). One of the few genuinely settled explanations of implicit regularization. [medium]

## Phase F — Systems & Efficiency

### F1 — Kernels & Attention
- **Triton warmups → FlashAttention** — Write a fused softmax and a tiled matmul in Triton, then implement a FlashAttention forward pass; benchmark against naive PyTorch attention and place both on a roofline plot. The tiling/IO-awareness idea becomes concrete. [deep][portfolio]

### F2 — Parallelism & Large-Scale Training
- **Shard and parallelize by hand** — Shard a small model with FSDP/ZeRO, implement tensor parallelism for a single linear layer manually, and add gradient checkpointing; measure the memory/throughput trade-offs. [deep]

### F3 — Quantization & Inference
- **Quantize, cache, speculate** — Apply INT8 (with LLM.int8()-style outlier handling) and 4-bit quantization to a small model; implement a KV-cache; then build a toy speculative-decoding loop (draft model + verify) and measure the latency/throughput gains. [deep][portfolio]

## Phase G — Capstone: Reading & Contributing

- **End-to-end paper reproduction** — Pick one recent paper and reproduce its central claim from scratch, documenting every place your result diverges from the paper's. [deep][portfolio]
- **OSS contribution** — Contribute a kernel, bug fix, or test to a real repo (Hugging Face `transformers`/`trl`/`peft`, vLLM, or the CS336 assignment repos), starting from docs and tests. [deep][portfolio]
- **Paper-reading log** — Keep a running log where every paper gets its claims tagged [SETTLED] / empirical / spin via the three-pass protocol; the habit is the deliverable. [quick, ongoing]

---

# Part 2 — Fraud Prevention (Curriculum 2, Phases H–P)

## Phase H — The Fraud & Financial-Crime Domain

### H1 — The FDS, formalized
- **Your own fraud simulator** — Extend the handbook's generator into a configurable testbed with tunable base rate, drift, and label delay; you'll reuse it as the controlled environment for Phases I, K, L, and M. Building the data-generating process teaches you exactly which assumptions later methods depend on. [medium][stack]

### H2 — Typologies
- **Fraud taxonomy artifact + method map** — Write a structured taxonomy of platform fraud types (ATO, synthetic identity, first-party/friendly fraud, collusion, APP scams), noting per type: signals, cost asymmetry, label latency, and whether "is this the genuine user?" even helps. Then build a decision guide of which model class fits which fraud type. [quick][stack]

### H3 — Payments ecosystem & chargeback lifecycle
- **Chargeback lifecycle simulator** — Build a small event-driven simulator of authorization → clearing → settlement → dispute → representment, emitting labels at the (delayed, noisy) times they'd actually arrive. Directly sets up the delayed-label problem in Phase M. [medium][stack]

## Phase I — Rare-Event Statistics & Evaluation

### I1 — Metrics under imbalance
- **Curves from scratch** — Implement ROC and PR curves yourself, demonstrate why linear interpolation in PR space is wrong, and plot how ROC-AUC stays optimistic while PR-AUC collapses as the base rate → 0. Compute Precision@k to mirror a real review-queue budget. [medium][stack]

### I2 — Proper scoring rules
- **AUC is not proper** — Implement Brier score and log loss, then construct two models with identical AUC but very different calibration to show ranking metrics don't pin down probabilities. Draw the reliability diagrams. [quick]

### I3 — Calibration
- **Break and fix calibration** — Reproduce the posterior-probability shift that undersampling induces, then implement Dal Pozzolo's correction to recover calibrated scores; implement Platt scaling and isotonic regression from scratch and compare reliability diagrams before/after. [medium][stack]

### I4 — Cost-sensitive learning
- **Verify Elkan's theorem** — Empirically show that resampling + a 0.5 threshold is equivalent to no resampling + a cost-adjusted threshold (up to calibration). Then build an expected-cost Bayes decision rule with example-dependent (amount-weighted) costs and compare dollar loss against an F1-optimal threshold. [medium][stack][portfolio]

### I5 — The resampling debate
- **SMOTE bake-off** — On a GBM with a proper temporal split, compare SMOTE vs. class weights vs. cost-thresholds vs. undersample-and-correct; report calibration and Precision@k, and document the regimes where SMOTE actually hurts. Produces a defensible internal position on a widely-misapplied technique. [medium][stack][portfolio]

## Phase J — Adversarial Machine Learning

### J1 — Field & threat models
- **Threat models + real attacks** — Write threat models for two or three PayPal-relevant attacks (credential-stuffing ATO, collusion refund abuse), then implement a *semantically-constrained* evasion attack against a tree/linear model (not an ℓ_p perturbation) and a label-poisoning attack against an online learner. Makes the evasion/poisoning distinction concrete. [medium][stack]

### J2 — Transfer to fraud & security evaluation
- **SHAP as an attack map + security-evaluation harness** — Use TreeSHAP feature importances to construct business-legal evasions and estimate their cost to the attacker; then build a harness that measures model performance as adversarial manipulation increases. Finally, audit one published fraud paper against the Arp et al. "Dos and Don'ts" pitfalls (temporal snooping, base-rate fallacy). Reframes SHAP as an attack surface, not just an explanation. [medium][stack]

## Phase K — Graph & Network Methods

### K1 — Entity resolution
- **Probabilistic record linkage** — Implement Fellegi–Sunter matching, then build a device/identity entity-resolution pipeline with blocking plus fuzzy matching. The unglamorous prerequisite that determines how much signal your graphs carry. [medium][stack]

### K2 — GNN backbone
- **Message passing from scratch** — Implement GCN, GraphSAGE, and GAT by hand and do node classification, first on a citation graph, then on a fraud graph. Establishes the baseline before the fraud-specific fixes. [medium]

### K3 — GNNs for fraud (the flagship build)
- **Write a GNN for a fraud dataset, then defeat camouflage** — Build a message-passing GNN from scratch on a fraud graph (Amazon/YelpChi or Elliptic), then implement CARE-GNN's label-aware neighbor selection and PC-GNN's label-balanced sampler; reproduce feature and relation camouflage and show how they degrade a vanilla GNN. Implement BWGNN's band-pass filter and demonstrate the high-graph-frequency anomaly signal — a direct payoff from your signal-processing background. [deep][stack][portfolio]

### K4 — The honest bake-off (highest institutional value)
- **Do graphs actually beat your GBM?** — On a fraud graph with a proper temporal split, compare a GBM vs. graph-features-plus-GBM vs. an end-to-end GNN, reporting PR-AUC and entity-level precision; then engineer graph-derived features (PageRank, connected-component size, triangle counts on device/identity graphs) into your GBM and measure the lift. The honest empirical answer to the contested "GNNs beat XGBoost" claim is the deliverable. [deep][stack][portfolio]

## Phase L — Sequence, Temporal & Anomaly Methods

### L1 — Feature engineering for sequences
- **Velocity features with point-in-time correctness** — Build RFM-style and time-windowed aggregation features from raw transactions, enforcing point-in-time correctness to avoid leakage, and establish the strong GBM baseline everything else must beat. [medium][stack]

### L2 — Deep sequence models
- **Sequence vs. aggregation, honestly** — Implement an LSTM and a small transformer over transaction sequences and compare them to aggregation+GBM on a temporal split, reproducing the Jurgovsky comparison in spirit; report whether the sequence model earns its complexity. [medium][stack]

### L3 — Anomaly detection
- **Isolation Forest from scratch + anomaly-as-feature** — Implement Isolation Forest yourself and an autoencoder anomaly detector; fold the anomaly score in as a feature to the supervised model and test the lift specifically on a held-out *late* period to measure novel-attack coverage. [medium][stack]

## Phase M — Production Fraud Systems

### M1 — Concept drift
- **ADWIN + prequential evaluation** — Implement the ADWIN drift detector and a test-then-train (prequential) evaluation loop; inject drift and show a static model decaying while an adaptive one recovers. [medium][stack]

### M2 — Delayed & noisy labels (the fraud-defining build)
- **Two-classifier delayed-label pipeline** — Simulate verification latency with a fast investigator-feedback stream and a slow chargeback stream drawn from different distributions; implement the two-classifier aggregate (one on feedback, one on delayed labels) and quantify its lift over treating labels as immediate. Reproduces the core Dal Pozzolo result and is directly reusable at PayPal. [deep][stack][portfolio]

### M3 — Real-time architecture & feature stores
- **Minimal scoring service + a leakage bug you fix** — Build a small real-time scoring service backed by a feature store with online/offline parity; then deliberately introduce a point-in-time leakage bug, quantify the phantom AUC it produces, and fix it with point-in-time-correct aggregation. Instills the single most valuable production habit. [deep][stack]

### M4 — Monitoring & feedback loops
- **Selective-labels simulator + active learning** — Simulate the closed feedback loop where the model determines which transactions get labeled, demonstrate the bias it induces, and implement an active-learning strategy that spends a fixed investigator budget well. [medium][stack]

## Phase N — Explainability, Fairness & Model Risk Management

### N1 — Explainability
- **KernelSHAP and TreeSHAP from scratch → break them** — Implement KernelSHAP and the polynomial-time path-dependent TreeSHAP algorithm yourself and verify against the `shap` library; then construct a correlated-feature case where the attributions mislead, reproducing the Aas et al. and Kumar et al. critiques. Turns your daily tool into something you understand at the algorithm level and can defend. [deep][stack][portfolio]

### N2 — Reason codes & adverse action
- **Reason-code generator + stability stress test** — Build an adverse-action-style reason-code generator from SHAP values and stress-test the stability of the "principal reason" under feature correlation; map model features to specific, accurate reason strings. [medium][stack]

### N3 — Model Risk Management
- **A real SR-11-7 validation report** — Write a full model-validation report for one of your production models in SR 11-7 terms (conceptual soundness, outcomes analysis, ongoing monitoring, effective challenge) and distill it into a reusable validation template. Directly reusable at work, and a scarce artifact. [medium][stack][portfolio]

### N4 — The EU layer
- **Compliance matrix + disparate-impact audit** — Build a matrix mapping a fraud model to GDPR Art. 22, the EU AI Act (working through the fraud carve-out and the hybrid-system boundary), and PSD2/SCA; then implement an adverse-impact-ratio audit and compute the calibration-vs-equalized-error trade-off, making the impossibility results concrete. [medium][stack]

## Phase O — AML, Sanctions & Broader Financial Crime

### O1 — The AML modeling problem
- **Reproduce Weber et al. on Elliptic** — Run logistic regression, random forest, and a GCN on the Elliptic dataset with a temporal split, and write up honestly how the "unknown"-dominated labels limit what any result can claim. Your first contact with a label regime even harsher than fraud. [medium][stack]

### O2 — Typologies & graphs
- **Laundering-pattern detection as alert triage** — On synthetic AML data (AMLSim / IBM AMLworld), implement laundering-pattern detection via graph motifs/cycle-finding plus community detection, and frame the output as *alert prioritization* that reduces false positives on a rule baseline — what actually matters operationally. [deep][stack]

### O3 — Sanctions screening
- **Fuzzy name matcher under zero-tolerance** — Build a sanctions-screening matcher with transliteration handling, alias expansion, and edit-distance/phonetic similarity; tune it under a "never miss a true match" constraint and observe how the precision/recall frontier inverts relative to fraud. [medium][stack]

### O4 — Regulatory machine
- **Typology-to-detection map + SAR-narrative assistant** — Build a reference mapping placement/layering/integration to signals and methods, and mock up a SAR-narrative assistant (optionally LLM-backed) that summarizes an alert's evidence into a draft narrative. Bridges into Part 3. [medium][stack]

## Phase P — Capstone: Staying Expert

- **Pick one integrative project** from Part 3 and take it end to end. [deep][portfolio]
- **Paper-triage log** — Keep a running log applying the 5-question protocol (realistic data? temporal split / no leakage? operationally meaningful metric? adaptive adversary? would it survive MRM?) to tag each fraud/AML paper [leaderboard-artifact] vs. [production-real]. [quick, ongoing]
- **OSS contribution** — Extend the fraud-detection-handbook simulator, contribute a dependence-aware or cost-sensitive extension to `shap`, or add a fraud-GNN implementation to DGL/PyG. [deep][portfolio]

---

# Part 3 — Cross-Cutting Integrative Projects (bridging both curricula)

These fuse the frontier and fraud tracks. They are the projects that most distinguish someone who has read both curricula from someone who has read either alone, and several are genuinely publishable industry studies.

- **Deep-tabular vs. GBM for fraud, done rigorously** — Benchmark FT-Transformer / TabTransformer against your gradient-boosted baseline on realistic imbalanced, temporally-split, delayed-label fraud data, with calibration, example-dependent cost, and Precision@k. The honest answer to "should we deep-learn our tabular fraud models" is the deliverable. Bridges C/D + I + K/L. [deep][stack][portfolio]
- **LLM-for-fraud-investigation assistant** — Build a retrieval-augmented assistant that reasons over an alert's evidence (transaction history, graph neighborhood, prior cases) and drafts investigator notes or SAR narratives; evaluate it realistically rather than on vibes. Bridges D + N + O. [deep][stack][portfolio]
- **RLVR on a rule-checking task** — Train a small reasoning model with GRPO to verify whether a transaction pattern violates a set of compliance rules, rewarding correct verifiable judgments. Bridges D3 + J + O. [deep]
- **Systems for real-time fraud** — Apply quantization, KV-caching, and efficient-serving techniques to a low-latency fraud-scoring model, and roofline the whole pipeline to find the true bottleneck. Bridges F + M. [deep][stack]
- **Adversarial robustness meets interpretability** — Combine the SHAP-as-attack-map idea with a security-evaluation harness on a production-like model, and propose costly-to-fake feature hardening based on what the attack map reveals. Bridges E/N + J. [medium][stack][portfolio]
- **Concentration bounds for Precision@k stability** — Use the concentration inequalities from A4 to derive how many fraud examples you need before your Precision@k estimate is stable, then validate the bound empirically on your data. A small, elegant piece that connects rigorous probability directly to a metric you report weekly. Bridges A4 + I. [medium][stack]

---

## A note on sequencing and payoff

Work each section in the order **from scratch → reproduce → extend**, and resist skipping the from-scratch build even for concepts you use daily — that is precisely where the understanding hides. Across everything here, the highest-value artifacts for your situation are the **honest bake-offs and reusable templates** (I4, I5, K4, L2, M2, M3, N1, N3, and the deep-tabular study in Part 3), because they produce defensible, transferable conclusions and reusable tooling rather than another leaderboard number. Those are the projects that make you the person the room turns to.