# From Strong Baseline to the Frontier: A Rigorous, Proof-Based Curriculum for Reading and Contributing to SOTA AI/ML

## TL;DR
- This is a phased, proof-first curriculum built for an ML engineer with a theoretical-physics background: ~10–15 months full-time-equivalent through the whole program, or a ~4-month MVP that goes straight through rigorous math essentials → transformers → one frontier specialization.
- The four frontier targets (LLMs/post-training, ML theory, systems/efficiency, transformers as connective tissue) are anchored to seminal primary papers with verified citations and to Stanford CS336 (2025), which is the single best free capstone for hands-on frontier LM work.
- Almost every core text is legally free online (Boyd, Vershynin, Durrett, Shalev-Shwartz–Ben-David, MacKay, Goodfellow, Murphy, Prince, Zhang/D2L, ESL, Sutton–Barto, Telgarsky), so cost is not a barrier; the binding constraint is disciplined time on proofs and reproduction projects.

## Calibration note (read this first)
Throughout, claims are tagged **[SETTLED]**, **[CONTESTED]**, or **[HYPE/OVERSTATED]** so you can distinguish mathematics that actually explains practice from post-hoc rationalization. The single most important meta-fact: **deep-learning practice massively outstrips deep-learning theory.** Classical statistical learning theory (VC, Rademacher) is rigorous and settled but largely *fails to explain* why overparameterized nets generalize; NTK is rigorous but describes a "lazy" regime that real training partly escapes; double descent, grokking, and emergent abilities are empirically real but their explanations are actively contested. Keep this tension in mind — it is exactly where the frontier is.

---

## Curriculum-wide dependency map

```
A. Rigorous Math Foundations ──┬──> B. Statistical Learning Theory ──> E. ML/DL Theory
                               │
                               ├──> C. Deep Learning Foundations ──> D. Transformers & LLMs
                               │                                        │
                               └──> F. Systems & Efficiency <───────────┘
                                                                        │
                            (D + E + F) ──> G. Capstone: Reading & Contributing to SOTA
```

- A is the spine. B needs A (measure/probability, concentration, optimization). C needs linear algebra + optimization + probability. D needs C. E needs A + B + C. F needs C + D + engineering. G needs D+E+F.
- **MVP spine (time-compressed):** A-minimal → C → D → one of {E, F} → G.

---

# Phase A — Rigorous Mathematical Foundations (proof-based)

**Goals:** Achieve genuine fluency (able to prove, not just cite) in real analysis, linear/matrix analysis, measure-theoretic probability, high-dimensional probability & concentration, convex and non-convex optimization theory, functional-analysis basics, and information theory.

**Prerequisites:** Undergraduate calculus, linear algebra, and probability; mathematical maturity (your physics + MSc background covers this).

**Time estimate:** Full: 5–7 months FTE. MVP: 6–8 weeks (concentration + convex optimization + linear algebra refresh only).

### A1. Real Analysis
- **Primary:** Walter Rudin, *Principles of Mathematical Analysis*, 3rd ed., McGraw-Hill, 1976. **[PAID]** The canonical rigorous treatment; do Ch. 1–9.
- **Alternative/bridge:** Charles C. Pugh, *Real Mathematical Analysis*, 2nd ed., Springer, 2015 — more geometric intuition. **[PAID]**
- **Physics scaffold:** Metric-space completeness and compactness are the "why" behind existence/uniqueness theorems you already used in classical mechanics and PDEs.

### A2. Linear Algebra & Matrix Analysis
- **Primary:** Sheldon Axler, *Linear Algebra Done Right*, 4th ed., Springer, 2024 (open access — free PDF). **[FREE]** Determinant-free, operator-centric.
- **Primary (matrix analysis):** Roger A. Horn & Charles R. Johnson, *Matrix Analysis*, 2nd ed., Cambridge University Press, 2013. **[PAID]** SVD, perturbation theory, matrix norms — the backbone of numerics and NTK.
- **Supplementary:** Gilbert Strang, *Linear Algebra and Learning from Data*, Wellesley-Cambridge, 2019. **[PAID]**
- **Connection to your stack:** Low-rank structure (SVD) is the mathematical core of LoRA (Phase D) and of PCA-style drift monitoring.

### A3. Measure-Theoretic Probability
- **Primary:** Rick Durrett, *Probability: Theory and Examples*, 5th ed., Cambridge University Press, 2019 (free PDF on author's Duke site, sites.math.duke.edu/~rtd). **[FREE]**
- **Alternative:** David Williams, *Probability with Martingales*, Cambridge University Press, 1991 — short, elegant, martingale-first. **[PAID]** / Patrick Billingsley, *Probability and Measure*, Anniversary ed., Wiley, 2012. **[PAID]**
- **Physics scaffold:** Measure theory is the rigorous version of "summing over microstates"; martingales generalize the fair-game/random-walk intuition.

### A4. High-Dimensional Probability & Concentration
- **Primary:** Roman Vershynin, *High-Dimensional Probability: An Introduction with Applications in Data Science*, 2nd ed., Cambridge University Press, 2026; a free pre-publication PDF (dated Nov 28, 2025) is on the author's UC Irvine page (math.uci.edu/~rvershyn). **[FREE]** (1st ed., 2018, ISBN 978-1-108-41519-4, also fine.)
- **Supplementary:** Stéphane Boucheron, Gábor Lugosi & Pascal Massart, *Concentration Inequalities: A Nonasymptotic Theory of Independence*, Oxford University Press, 2013. **[PAID]**
- **Supplementary:** Martin J. Wainwright, *High-Dimensional Statistics: A Non-Asymptotic Viewpoint*, Cambridge University Press, 2019. **[PAID]**
- **Why this is the keystone for theory:** Hoeffding/Bernstein/matrix-Bernstein, sub-Gaussian/sub-exponential tails, and generic chaining are *exactly* the tools generalization bounds are built from. **[SETTLED]**
- **Physics scaffold:** Concentration of measure ≈ the thermodynamic limit — fluctuations vanish as dimension grows.

### A5. Optimization Theory (convex and non-convex)
- **Primary (convex):** Stephen Boyd & Lieven Vandenberghe, *Convex Optimization*, Cambridge University Press, 2004 (full PDF free on Boyd's Stanford page: web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf). **[FREE]**
- **Primary (first-order/complexity):** Yurii Nesterov, *Lectures on Convex Optimization*, 2nd ed., Springer, 2018. **[PAID]** Lower bounds, accelerated gradient — the rigorous "why" of momentum.
- **Primary (numerical):** Jorge Nocedal & Stephen J. Wright, *Numerical Optimization*, 2nd ed., Springer, 2006. **[PAID]**
- **Non-convex/ML-specific:** the optimization chapters of Telgarsky's notes (Phase E) and Sébastien Bubeck, *Convex Optimization: Algorithms and Complexity*, Foundations and Trends in ML, 2015 (free on arXiv:1405.4980). **[FREE]**
- **Physics scaffold:** Gradient flow = dissipative dynamics; momentum/Nesterov = a damped Hamiltonian system; mirror descent = a change of geometry (Bregman divergence) analogous to Lagrangian coordinate changes.

### A6. Functional Analysis (basics) + RKHS
- **Primary:** Erwin Kreyszig, *Introductory Functional Analysis with Applications*, Wiley, 1989. **[PAID]** Hilbert/Banach spaces, operators, spectral theorem.
- **ML target:** Reproducing Kernel Hilbert Spaces — the language of kernels and of the NTK. See Bernhard Schölkopf & Alexander Smola, *Learning with Kernels*, MIT Press, 2002. **[PAID]**

### A7. Information Theory
- **Primary:** Thomas M. Cover & Joy A. Thomas, *Elements of Information Theory*, 2nd ed., Wiley, 2006. **[PAID]**
- **Primary (free, idiosyncratic, brilliant):** David J. C. MacKay, *Information Theory, Inference, and Learning Algorithms*, Cambridge University Press, 2003 (free PDF on author's site, inference.org.uk/mackay/itila). **[FREE]**
- **Physics scaffold:** Entropy, free energy, and the variational principle recur directly in variational inference, the ELBO, and the DPO/RLHF objective (KL-regularized reward maximization).

**Phase A exercises/projects:**
1. Prove Hoeffding's and Bernstein's inequalities from scratch; then prove a finite-class generalization bound (bridge to Phase B).
2. Implement and prove convergence rates for GD and Nesterov's accelerated gradient on strongly convex quadratics; verify the rate empirically.
3. Derive the SVD and prove the Eckart–Young theorem; connect to low-rank adaptation.

**MVP for Phase A:** Vershynin Ch. 1–3 (concentration), Boyd Ch. 2–5 & 9 (convexity, duality, gradient methods), Axler for a linear-algebra refresh.

---

# Phase B — Statistical Learning Theory (the bridge from math to ML)

**Goals:** Rigorous PAC/agnostic-PAC learning, uniform convergence, VC theory, Rademacher complexity, covering numbers, margin bounds, and their limits.

**Prerequisites:** A3, A4, A5.

**Time:** Full 6–8 weeks; MVP 2 weeks (SSBD Part I).

- **Primary:** Shai Shalev-Shwartz & Shai Ben-David, *Understanding Machine Learning: From Theory to Algorithms*, Cambridge University Press, 2014 (free PDF on Shalev-Shwartz's HUJI page: cs.huji.ac.il/~shais/UnderstandingMachineLearning). **[FREE]** The best rigorous entry point; do Parts I–II in full.
- **Primary:** Mehryar Mohri, Afshin Rostamizadeh & Ameet Talwalkar, *Foundations of Machine Learning*, 2nd ed., MIT Press, 2018 (free PDF on mlbook.org). **[FREE]** Deeper on Rademacher complexity and margin theory.
- **Reference (statistical, encyclopedic):** Trevor Hastie, Robert Tibshirani & Jerome Friedman, *The Elements of Statistical Learning*, 2nd ed., Springer, 2009 (free PDF on Hastie's Stanford domain: hastie.su.domains/Papers/ESLII.pdf). **[FREE]**
- **Course:** Stanford CS229 (Andrew Ng / current staff) — free notes and lectures, for the statistical-ML backbone. **[FREE]**

**Calibration:**
- **[SETTLED]** VC dimension and Rademacher complexity give correct, distribution-free worst-case bounds for bounded-capacity classes; the fundamental theorem of PAC learning is airtight.
- **[CONTESTED/OVERSTATED]** These uniform-convergence bounds are *vacuous* for modern overparameterized nets (bounds ≫ 1). Chiyuan Zhang et al., "Understanding deep learning requires rethinking generalization" (ICLR 2017; arXiv:1611.03530) showed nets fit random labels, so capacity-based bounds cannot be the whole story. **This is the single cleanest demonstration that classical theory does not explain deep learning.**

**Connection to your stack:** Generalization bounds for gradient-boosted trees (finite VC/pseudo-dimension per tree, margin/AdaBoost theory) *do* apply meaningfully to your fraud models — a place where classical theory is genuinely predictive, unlike for deep nets.

**Exercises:** Prove the VC bound via growth function + Sauer–Shelah; compute Rademacher complexity of linear predictors; reproduce the random-label experiment on a small MLP and observe the vacuity of the bound.

---

# Phase C — Deep Learning Foundations (rigorous where possible)

**Goals:** Backprop as reverse-mode autodiff, initialization, normalization, optimization dynamics of SGD/Adam, regularization, CNNs/RNNs, and the probabilistic/variational view (VAEs, diffusion at a foundational level).

**Prerequisites:** A2, A5, A7, B.

**Time:** Full 6–8 weeks; MVP 3 weeks.

- **Primary (foundational, free):** Ian Goodfellow, Yoshua Bengio & Aaron Courville, *Deep Learning*, MIT Press, 2016 (free HTML at deeplearningbook.org). **[FREE]** Dated on architectures but excellent on fundamentals and optimization.
- **Primary (modern, free):** Simon J. D. Prince, *Understanding Deep Learning*, MIT Press, 2023 (free PDF at udlbook.com, CC-BY-NC-ND). **[FREE]** Best modern rigorous-but-readable text; covers transformers, double descent, grokking, lottery tickets.
- **Primary (modern, free):** Christopher M. Bishop & Hugh Bishop, *Deep Learning: Foundations and Concepts*, Springer, 2024 (free-to-use digital version at bishopbook.com). **[FREE]**
- **Primary (probabilistic, free):** Kevin P. Murphy, *Probabilistic Machine Learning: An Introduction* (2022) and *…Advanced Topics* (2023), MIT Press (free PDFs at probml.github.io/pml-book). **[FREE]**
- **Reference (classic, now free):** Christopher M. Bishop, *Pattern Recognition and Machine Learning*, Springer, 2006 (free PDF released by Microsoft on Bishop's page). **[FREE]**
- **Hands-on primary:** Aston Zhang, Zachary C. Lipton, Mu Li & Alexander J. Smola, *Dive into Deep Learning*, Cambridge University Press / d2l.ai (free, interactive). **[FREE]**
- **Course:** Stanford CS231n (vision-flavored but the best free deep-learning-mechanics course). **[FREE]**
- **Hands-on bridge:** Andrej Karpathy, "Neural Networks: Zero to Hero" + nanoGPT (free YouTube + GitHub). **[FREE]** *Secondary but outstanding* — build micrograd and a GPT from scratch. **[VERSION NOTE: track the repo; APIs evolve.]**

**Physics scaffold:** SGD as Langevin dynamics (noise ≈ temperature); the loss landscape as an energy surface; batch-norm/skip-connections as conditioning tricks with renormalization-group flavor.

**Exercises:** Implement reverse-mode autodiff; reproduce an initialization-variance analysis (Glorot/He) and confirm the variance-preservation derivation; train a small ResNet and a small Transformer from scratch.

---

# Phase D — Transformers & LLMs in Depth (the connective tissue)

**Goals:** Master the transformer end-to-end (attention variants, positional encodings, normalization placement), pretraining, tokenization, scaling laws, post-training (SFT/RLHF/DPO/RLVR), in-context learning, long-context, mixture-of-experts, and interpretability. Be able to read any current LM paper.

**Prerequisites:** C; helpful: A7 (info theory), A5 (optimization).

**Time:** Full 10–12 weeks; MVP 4 weeks (CS336 assignments 1–2 + the starred papers).

**Anchor course (do this):** Stanford **CS336: Language Modeling from Scratch**, Spring 2025 — lectures on YouTube, assignments and lecture code on GitHub (stanford-cs336). Builds tokenizer→transformer→training→systems→scaling→inference→alignment from scratch, minimal scaffolding. **[FREE]** A 3rd offering runs Spring 2026 (Mar 30–Jun 10, 2026); check cs336.stanford.edu for updated materials. **[VERSION NOTE]**

**NLP backbone course:** Stanford **CS224n** (free lectures/notes). **[FREE]**

### D1. Architecture (seminal papers) — all **[FREE]** on arXiv
- ★ Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser & Illia Polosukhin, "Attention Is All You Need," *NeurIPS* 2017, arXiv:1706.03762.
- Jacob Devlin, Ming-Wei Chang, Kenton Lee & Kristina Toutanova, "BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding," *NAACL-HLT* 2019, pp. 4171–4186, arXiv:1810.04805.
- Alec Radford et al., "Improving Language Understanding by Generative Pre-Training" (GPT-1, OpenAI tech report, 2018) and "Language Models are Unsupervised Multitask Learners" (GPT-2, 2019).
- Jianlin Su, Yu Lu, Shengfeng Pan, Ahmed Murtadha, Bo Wen & Yunfeng Liu, "RoFormer: Enhanced Transformer with Rotary Position Embedding," arXiv:2104.09864 (2021; *Neurocomputing* 568:127063, 2024). RoPE is now near-universal.
- Noam Shazeer, "GLU Variants Improve Transformer," arXiv:2002.05202 (2020) — SwiGLU.

### D2. Scaling & pretraining — **[FREE]**
- ★ Jared Kaplan, Sam McCandlish, Tom Henighan, Tom B. Brown, Benjamin Chess, Rewon Child, Scott Gray, Alec Radford, Jeffrey Wu & Dario Amodei, "Scaling Laws for Neural Language Models," arXiv:2001.08361 (2020).
- ★ Jordan Hoffmann et al., "Training Compute-Optimal Large Language Models" (Chinchilla), *NeurIPS* 2022, arXiv:2203.15556. The 70B Chinchilla was trained compute-optimally on 1.4T tokens = exactly **20 tokens per parameter**; the 20-to-1 heuristic is stated in the paper's Appendix C. **[SETTLED-ish as a heuristic]** but **[CONTESTED as a precise law]:** Besiroglu, Erdil, Barnett & You, "Chinchilla Scaling: A Replication Attempt" (Epoch AI, arXiv:2404.10102, 2024) reports that "we replicate Hoffmann et al.'s parametric scaling law estimates, finding issues" — wide confidence intervals and discrepancies between the paper's three estimation approaches — and provides "better-fitting estimates"; task/architecture dependence is documented in subsequent work.
- Tom B. Brown et al., "Language Models are Few-Shot Learners" (GPT-3), *NeurIPS* 2020, pp. 1877–1901, arXiv:2005.14165.

### D3. Post-training / alignment — **[FREE]**
- ★ Long Ouyang, Jeffrey Wu, Xu Jiang, Diogo Almeida, Carroll Wainwright et al., "Training Language Models to Follow Instructions with Human Feedback" (InstructGPT), *NeurIPS* 2022, pp. 27730–27744, arXiv:2203.02155.
- ★ Rafael Rafailov, Archit Sharma, Eric Mitchell, Stefano Ermon, Christopher D. Manning & Chelsea Finn, "Direct Preference Optimization: Your Language Model Is Secretly a Reward Model" (DPO), *NeurIPS* 2023, arXiv:2305.18290. Note the closed-form KL-regularized-reward derivation — this is where your Phase A information theory pays off.
- Yuntao Bai et al. (Anthropic), "Constitutional AI: Harmlessness from AI Feedback," arXiv:2212.08073 (2022).
- John Schulman, Filip Wolski, Prafulla Dhariwal, Alec Radford & Oleg Klimov, "Proximal Policy Optimization Algorithms," arXiv:1707.06347 (2017) — the RL workhorse behind RLHF.
- ★ Zhihong Shao et al., "DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models," arXiv:2402.03300 (2024) — introduces **GRPO (Group Relative Policy Optimization)**.
- ★ DeepSeek-AI (D. Guo, D. Yang, H. Zhang et al.), "DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning," arXiv:2501.12948 (2025). Peer-reviewed version: "DeepSeek-R1 incentivizes reasoning in LLMs through reinforcement learning," *Nature* 645(8081):633–638, published online 17 Sept 2025, DOI 10.1038/s41586-025-09422-z (Open Access, CC-BY 4.0) — reported by Nature as the first major open-weight LLM published after independent peer review. The canonical **RLVR** (RL from verifiable rewards) reasoning-model paper. **[CONTESTED]** How much pure-RL "reasoning" generalizes beyond verifiable domains (math/code) is open.
- Jason Wei et al., "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models," *NeurIPS* 2022, arXiv:2201.11903.

### D4. Parameter-efficient fine-tuning — **[FREE]**
- ★ Edward J. Hu, Yelong Shen, Phillip Wallis, Zeyuan Allen-Zhu, Yuanzhi Li, Shean Wang, Lu Wang & Weizhu Chen, "LoRA: Low-Rank Adaptation of Large Language Models," *ICLR* 2022, arXiv:2106.09685.
- Tim Dettmers, Artidoro Pagnoni, Ari Holtzman & Luke Zettlemoyer, "QLoRA: Efficient Finetuning of Quantized LLMs," *NeurIPS* 2023, arXiv:2305.14314 — 4-bit NF4 + double quantization + paged optimizers (finetune a 65B model on a single 48GB GPU).

### D5. Mixture-of-Experts — **[FREE]**
- Noam Shazeer et al., "Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer," *ICLR* 2017, arXiv:1701.06538.
- ★ William Fedus, Barret Zoph & Noam Shazeer, "Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity," *JMLR* 23(120):1–39, 2022, arXiv:2101.03961.
- DeepSeek-AI, "DeepSeek-V3 Technical Report," arXiv:2412.19437 (2024). Per the abstract: "a strong Mixture-of-Experts (MoE) language model with 671B total parameters with 37B activated for each token … adopts Multi-head Latent Attention (MLA) and DeepSeekMoE architectures"; pre-trained on 14.8T tokens using 2.788M H800 GPU-hours. The current open-weight frontier reference for MoE.

### D6. Long-context — **[FREE]**
- Bowen Peng, Jeffrey Quesnelle, Honglu Fan & Enrico Shippole, "YaRN: Efficient Context Window Extension of Large Language Models," *ICLR* 2024, arXiv:2309.00071.
- Hao Liu, Matei Zaharia & Pieter Abbeel, "Ring Attention with Blockwise Transformers for Near-Infinite Context," *ICLR* 2024, arXiv:2310.01889.

### D7. Emergent abilities — the debate (assign both) — **[FREE]**
- Jason Wei et al., "Emergent Abilities of Large Language Models," *TMLR* 2022, arXiv:2206.07682.
- ★ Rylan Schaeffer, Brando Miranda & Sanmi Koyejo, "Are Emergent Abilities of Large Language Models a Mirage?" *NeurIPS* 2023 (Outstanding Paper), arXiv:2304.15004. **[CONTESTED — this is the model for how to read the field]:** emergence is partly an artifact of discontinuous/nonlinear metrics; under smooth metrics many "emergent" jumps become predictable. Not fully settled either way.

**Connection to your stack:** Transformers for *tabular* fraud data mostly **do not** beat gradient-boosted trees; see Léo Grinsztajn, Edouard Oyallon & Gaël Varoquaux, "Why do tree-based models still outperform deep learning on typical tabular data?" *NeurIPS* 2022 (arXiv:2207.08815). Where deep learning *does* transfer: sequence/entity embeddings, text/behavioral signals, and large-scale representation learning. Treat this honestly — the frontier LLM stack is not a drop-in upgrade for your core tabular models.

**Exercises/projects:** Implement multi-head attention + a full GPT (nanoGPT-scale) from scratch; fine-tune with LoRA and with DPO on a small preference set; reproduce a scaling-law fit on tiny models; implement a toy GRPO loop on a verifiable task (e.g., arithmetic).

---

# Phase E — ML / Deep Learning Theory (what's settled vs open)

**Goals:** Understand the honest state of theory: optimization landscapes, implicit regularization/bias, NTK and feature learning, double descent, grokking, the lottery ticket hypothesis, and generalization in the overparameterized regime.

**Prerequisites:** A (all), B.

**Time:** Full 8–10 weeks; MVP 3 weeks (Telgarsky notes + the starred papers).

- **Primary (free lecture notes):** Matus Telgarsky, *Deep Learning Theory Lecture Notes*, Univ. of Illinois, 2021 (mjt.cs.illinois.edu/dlt). **[FREE]** The best rigorous single source; approximation, optimization, generalization.
- **Primary (free draft):** Sanjeev Arora et al., *Theory of Deep Learning* (book draft). **[FREE]**
- **Reference:** Roman Vershynin (A4) and Wainwright (A4) for the probabilistic machinery.

### Seminal papers — all **[FREE]**
- ★ Arthur Jacot, Franck Gabriel & Clément Hongler, "Neural Tangent Kernel: Convergence and Generalization in Neural Networks," *NeurIPS* 2018, arXiv:1806.07572. **[SETTLED as math, CONTESTED as explanation]:** exact in the infinite-width "lazy" limit; real finite nets do *feature learning* that the NTK misses.
- ★ Mikhail Belkin, Daniel Hsu, Siyuan Ma & Soumik Mandal, "Reconciling Modern Machine-Learning Practice and the Classical Bias–Variance Trade-off," *PNAS* 116(32):15849–15854, 2019. (Double descent, foundational.)
- ★ Preetum Nakkiran, Gal Kaplun, Yamini Bansal, Tristan Yang, Boaz Barak & Ilya Sutskever, "Deep Double Descent: Where Bigger Models and More Data Hurt," *ICLR* 2020 / *J. Stat. Mech.* 2021:124003, arXiv:1912.02292.
- ★ Alethea Power, Yuri Burda, Harri Edwards, Igor Babuschkin & Vedant Misra, "Grokking: Generalization Beyond Overfitting on Small Algorithmic Datasets," arXiv:2201.02177 (2022). Companion: Neel Nanda, Lawrence Chan, Tom Lieberum, Jess Smith & Jacob Steinhardt, "Progress Measures for Grokking via Mechanistic Interpretability," *ICLR* 2023, arXiv:2301.05217.
- ★ Jonathan Frankle & Michael Carbin, "The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks," *ICLR* 2019, arXiv:1803.03635.
- Chiyuan Zhang, Samy Bengio, Moritz Hardt, Benjamin Recht & Oriol Vinyals, "Understanding Deep Learning Requires Rethinking Generalization," *ICLR* 2017, arXiv:1611.03530.
- Daniel Soudry, Elad Hoffer, Mor Shpigel Nacson, Suriya Gunasekar & Nathan Srebro, "The Implicit Bias of Gradient Descent on Separable Data," *JMLR* 2018 — GD on separable data converges to the max-margin solution (a genuine, rigorous explanation of implicit regularization). **[SETTLED in its setting]**

**Physics scaffold (this is your comparative advantage):**
- Double descent and grokking are studied explicitly as **phase transitions**; several papers use statistical-mechanics (replica) methods. Belkin's curve is a bona fide phase-transition-like phenomenon.
- The **statistical-mechanics of learning** literature (Andreas Engel & Christian Van den Broeck, *Statistical Mechanics of Learning*, Cambridge, 2001 **[PAID]**) derives generalization curves via replica theory — directly readable with your background.
- NTK ↔ Gaussian processes ↔ the infinite-width limit is a mean-field/thermodynamic-limit statement.
- Andrea Montanari's "Six Lectures on Linearized Neural Networks" (arXiv:2308.13431) and the Krzakala–Zdeborová "Statistical Physics & Machine Learning" material (free on arXiv) are the ideal bridge for you.

**Calibration summary for Phase E:**
- **[SETTLED]:** implicit bias of GD toward max-margin on separable data; NTK dynamics in the strict infinite-width limit; double descent as an empirical phenomenon.
- **[CONTESTED]:** *why* real (finite-width, feature-learning) nets generalize; the mechanism of grokking (circuit efficiency vs. representation learning vs. weight-norm dynamics — multiple competing 2023–2026 accounts); whether NTK is the right model of practice (mostly not).
- **[HYPE/OVERSTATED]:** claims that any single current theory "explains deep learning." None does. Be skeptical of tidy narratives.

---

# Phase F — Systems & Efficiency (GPUs, kernels, parallelism, inference)

**Goals:** Understand and implement the systems that make frontier models feasible: GPU execution model, memory hierarchy, custom kernels (CUDA/Triton), FlashAttention, data/tensor/pipeline/sequence parallelism, ZeRO sharding, mixed precision, quantization, and inference optimization (KV-cache, paging, speculative decoding).

**Prerequisites:** C, D; comfort with C++/Python and computer-architecture basics.

**Time:** Full 8–10 weeks; MVP 4 weeks (CS336 systems lectures + a Triton kernel + FlashAttention paper).

**Anchor:** CS336 lectures 5–8 & 10 (GPUs, kernels/Triton, parallelism ×2, inference). **[FREE]**

### Kernels & attention — **[FREE]** on arXiv
- ★ Tri Dao, Daniel Y. Fu, Stefano Ermon, Atri Rudra & Christopher Ré, "FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness," *NeurIPS* 2022, arXiv:2205.14135.
- Tri Dao, "FlashAttention-2: Faster Attention with Better Parallelism and Work Partitioning," arXiv:2307.08691 (2023). (Baseline achieves only ~35% utilization on the H100.)
- ★ Jay Shah, Ganesh Bikshandi, Ying Zhang, Vijay Thakkar, Pradeep Ramani & Tri Dao, "FlashAttention-3: Fast and Accurate Attention with Asynchrony and Low-Precision," *NeurIPS* 2024, arXiv:2407.08608. Per the published abstract: speedup on H100 GPUs by 1.5–2.0×, with **BF16 reaching up to 840 TFLOPs/s (85% utilization)** and **FP8 reaching 1.3 PFLOPs/s** (note: these published figures supersede the earlier blog figures of 740 TFLOPs/75%/1.2 PFLOPs). **[VERSION NOTE: a FlashAttention-4 preprint (arXiv:2603.05451, 2026) has since appeared; check the FlashAttention repo for the current release before benchmarking.]**
- Philippe Tillet, H. T. Kung & David Cox, "Triton: An Intermediate Language and Compiler for Tiled Neural Network Computations," *MAPL @ PLDI* 2019, ACM, DOI:10.1145/3315508.3329973. **(No arXiv version.)** **[PAID via ACM; author copies circulate]**

### Parallelism & large-scale training — **[FREE]**
- ★ Mohammad Shoeybi, Mostofa Patwary, Raul Puri, Patrick LeGresley, Jared Casper & Bryan Catanzaro, "Megatron-LM: Training Multi-Billion Parameter Language Models Using Model Parallelism," arXiv:1909.08053 (2019). Tensor parallelism.
- ★ Samyam Rajbhandari, Jeff Rasley, Olatunji Ruwase & Yuxiong He, "ZeRO: Memory Optimizations Toward Training Trillion Parameter Models," *SC20* (IEEE), arXiv:1910.02054 (2020). The basis of DeepSpeed.
- Yanping Huang et al., "GPipe: Efficient Training of Giant Neural Networks Using Pipeline Parallelism," *NeurIPS* 2019, arXiv:1811.06965.
- Paulius Micikevicius et al., "Mixed Precision Training," *ICLR* 2018, arXiv:1710.03740.

### Quantization & inference — **[FREE]**
- Tim Dettmers, Mike Lewis, Younes Belkada & Luke Zettlemoyer, "LLM.int8(): 8-bit Matrix Multiplication for Transformers at Scale," *NeurIPS* 2022, arXiv:2208.07339.
- Elias Frantar, Saleh Ashkboos, Torsten Hoefler & Dan Alistarh, "GPTQ: Accurate Post-Training Quantization for Generative Pre-trained Transformers," *ICLR* 2023, arXiv:2210.17323.
- Ji Lin et al., "AWQ: Activation-aware Weight Quantization for LLM Compression and Acceleration," *MLSys* 2024 (Best Paper), arXiv:2306.00978.
- ★ Woosuk Kwon, Zhuohan Li, Siyuan Zhuang, Ying Sheng, Lianmin Zheng, Cody Hao Yu, Joseph E. Gonzalez, Hao Zhang & Ion Stoica, "Efficient Memory Management for Large Language Model Serving with PagedAttention" (vLLM), *SOSP* 2023, arXiv:2309.06180.
- Yaniv Leviathan, Matan Kalman & Yossi Matias, "Fast Inference from Transformers via Speculative Decoding," *ICML* 2023, arXiv:2211.17192; and Charlie Chen, Sebastian Borgeaud, Geoffrey Irving, Jean-Baptiste Lespiau, Laurent Sifre & John Jumper, "Accelerating Large Language Model Decoding with Speculative Sampling," arXiv:2302.01318 (2023).

**Learning resources (free):** the official NVIDIA CUDA C++ Programming Guide; the OpenAI Triton tutorials/docs; the GPU MODE (formerly CUDA MODE) lecture series and its "PMPP" reading group. **[VERSION NOTE: CUDA (currently 12.x/13.x), Triton, and PyTorch versions move fast; always confirm the version your target hardware/toolchain uses. Wen-mei W. Hwu, David B. Kirk & Izzat El Hajj, *Programming Massively Parallel Processors: A Hands-on Approach*, 4th ed., Morgan Kaufmann, 2022 is the canonical textbook — PAID.]**

**Physics scaffold:** Roofline analysis is dimensional analysis for compute — arithmetic intensity (FLOP/byte) vs. bandwidth is exactly the kind of scaling argument you already do. FlashAttention is a cache-blocking/tiling argument: minimize slow-memory traffic, recompute cheap quantities.

**Exercises/projects:** Write a fused softmax and a tiled matmul in Triton; implement a minimal FlashAttention forward pass; profile with Nsight; shard a small model with ZeRO/FSDP; implement a KV-cache and a toy speculative-decoding loop.

---

# Phase G — Capstone: Reading and Contributing to SOTA

**Goals:** Convert knowledge into contribution: read any new paper fast and critically, reproduce results, and make an open-source or research contribution.

**Prerequisites:** D + E + F (or one specialization at MVP level).

**Time:** Ongoing; initial 4–6 weeks to establish workflow.

**How to stay current (venues & tooling):**
- Top venues: **NeurIPS, ICML, ICLR** (core ML/DL); **ACL, EMNLP, NAACL** (NLP/LLMs); **MLSys** (systems); **COLT** (learning theory); journals **JMLR, TMLR**.
- Use **arXiv** (cs.LG, cs.CL, stat.ML) with alerts; **Papers with Code**; **Semantic Scholar**/**Connected Papers** for citation graphs; **OpenReview** to read reviews and rebuttals (learn what reviewers actually reward). Follow venue "Outstanding Paper" lists as a curated filter.
- **[VERSION NOTE: the SOTA frontier — reasoning models, RLVR variants, long-context, MoE, inference kernels — turns over every few months. Treat any specific model/result as a snapshot; re-verify before relying on it.]**

**How to read a paper (a concrete protocol):** three-pass method (Keshav): (1) title/abstract/figures/conclusions; (2) main method + key equations, mapping each to Phase A–F machinery; (3) reproduce the central claim mentally or in code, and list what you'd need to falsify it. Always ask: what's **[SETTLED]** here, what's an **empirical** claim, and what's **spin**?

**Capstone project options (pick one, aligned to a frontier target):**
1. **LLM/post-training:** reproduce a small DPO or GRPO result on an open model; write it up with an ablation.
2. **Theory:** take an open grokking/double-descent question and run a controlled phase-transition experiment; connect to statistical mechanics.
3. **Systems:** contribute a Triton kernel or a vLLM/DeepSpeed improvement; benchmark rigorously with roofline analysis.
4. **Your-stack bridge:** rigorously benchmark a modern tabular/deep hybrid (e.g., FT-Transformer, or LLM-derived entity embeddings) against your gradient-boosted baseline for fraud, with SHAP/TreeSHAP-based explainability and drift monitoring — a genuinely publishable industry study.

**Open-source on-ramps:** Hugging Face `transformers`/`trl`/`peft`, `vLLM`, DeepSpeed, `torch`, and the `stanford-cs336` assignment repos. Start with documentation and tests, then small fixes, then features.

---

# Reinforcement-learning supplement (for D3 depth)
Because post-training now lives on RL, add the canonical RL text as a reference:
- Richard S. Sutton & Andrew G. Barto, *Reinforcement Learning: An Introduction*, 2nd ed., MIT Press, 2018 (free author PDF at incompleteideas.net/book/the-book-2nd.html). **[FREE]** Read Ch. 1–6, 13 (policy gradients) as background for PPO/GRPO/DPO.

---

# Overall MVP (time-compressed, ~4 months FTE)
1. **Weeks 1–6 (Math-minimal, Phase A):** Vershynin Ch. 1–3; Boyd Ch. 2–5, 9; Axler refresh; MacKay selected chapters for info theory.
2. **Weeks 5–8 (overlap, Phase B):** SSBD Part I (PAC, uniform convergence, VC) + the "rethinking generalization" paper.
3. **Weeks 7–12 (Phase C→D):** Prince *Understanding Deep Learning* core chapters; Karpathy Zero-to-Hero + nanoGPT; CS336 assignments 1–2.
4. **Weeks 12–16 (one specialization + Phase G):** choose **D-deep** (post-training papers + a DPO/GRPO reproduction) *or* **F** (CS336 systems lectures + a Triton/FlashAttention project); start the three-pass reading habit and one capstone.

# Full-program time budget (FTE, sequential; overlaps compress this)
- A: 5–7 mo · B: 1.5–2 mo · C: 1.5–2 mo · D: 2.5–3 mo · E: 2–2.5 mo · F: 2–2.5 mo · G: ongoing. **Realistic part-time (10–15 h/week): ~2–3 years; full-time: ~10–15 months.**

# Benchmarks that should change your plan
- If you can prove a finite-class generalization bound and a GD convergence rate unaided → skip the rest of Phase A's remedial passes and accelerate to B/C.
- If you can implement nanoGPT + LoRA + a DPO loop from scratch → you've met Phase D's bar; commit to E or F as your specialization.
- If a Triton fused-attention kernel profiles within ~2× of FlashAttention on your GPU → you're ready for a real systems open-source contribution.
- If you can read a fresh arXiv paper and correctly tag its claims [SETTLED]/empirical/spin in one sitting → you've hit the capstone goal; shift effort to producing (reproductions, then original work).

## Caveats
- **Theory-practice gap is real and central:** treat every "explanation" of deep learning as provisional. The curriculum deliberately assigns competing papers (e.g., Wei vs. Schaeffer on emergence) so you form calibrated views rather than adopting a narrative.
- **Currency:** specific SOTA models, library versions (CUDA/Triton/PyTorch/FlashAttention), and "current best" methods change on a months timescale. All version-sensitive items are flagged; re-verify before production use. FlashAttention-4 (arXiv:2603.05451) and continued DeepSeek/Qwen releases already postdate several papers above.
- **Free-availability:** free status can change; author-hosted PDFs (Boyd, Durrett, Vershynin, SSBD, ESL, MacKay, Prince, Bishop, Sutton–Barto) were current as of research but confirm at point of use. Editions cited are the latest verified (e.g., Vershynin 2nd ed. 2026 with free pre-pub PDF; Durrett 5th ed. 2019).
- **Editions/citations:** arXiv IDs and venues were verified; a few papers have title/author variants between preprint and published versions (e.g., ZeRO's arXiv v1 title; RoFormer's author list; DeepSeek-R1's Nature title differs from the arXiv title). Two arXiv IDs (speculative decoding 2211.17192; chain-of-thought 2201.11903) are high-confidence but worth a 5-second spot-check.
- **Your stack:** the frontier LLM/transformer stack does **not** straightforwardly replace gradient-boosted trees for tabular fraud (Grinsztajn et al. 2022); the connections are value-adds and honest benchmarks, not a mandate to deep-learning-everything.