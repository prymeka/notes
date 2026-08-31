# A 24-Month Curriculum: Mathematics, Classical ML, and the History of AI

*A three-track self-study plan at ~5 hrs/week (≈480 hrs total), designed for a working ML engineer with a theoretical physics background who wants to (a) rebuild mathematical foundations from the ground up, (b) master the pre-deep-learning canon of machine learning end-to-end, and (c) gain a historically grounded understanding of AI as a field.*

---

## Preface

### Goals

By the end of the 24 months you should be able to:

1. Read modern theoretical ML/DL papers — including generalization bounds, kernel theory, variational inference, optimization theory, and information-geometric approaches — without the mathematics being a bottleneck.
2. Derive, implement, and reason rigorously about every major classical (pre-deep-learning) ML method, from CART and gradient boosting through SVMs, Gaussian processes, graphical models, HMMs, and anomaly detection.
3. Situate any modern AI development in its proper historical lineage: the symbolic / connectionist / statistical learning trajectories, the AI winters, and the conceptual debts modern AI owes to GOFAI.

### Assumed background

This curriculum assumes:

- Undergraduate physics-level fluency with multivariable calculus, ODEs/PDEs at a working level, vector calculus, and complex variables.
- Working linear algebra (matrices, determinants, eigendecomposition, change of basis) but not necessarily the abstract operator-theoretic view.
- Real analysis at the level of Rudin's *Principles* (epsilon-delta, convergence, compactness, continuity in metric spaces), with potential gaps.
- Probability at the level of a good undergraduate course, but not measure-theoretic.
- Working Python and applied ML experience (you are an ML engineer); no separate coding track is included.

### Reading conventions

Every reading is annotated and tagged. Tags used throughout:

- **[Primary]** — the spine of the phase. Read in full or to the depth specified.
- **[Supplementary]** — read selectively, use as reference, or substitute for the primary if it doesn't suit you.
- **[Historical]** — primary-source paper or text, read for the ideas in their original form.
- **[Free]** — legally free PDF available from the author or publisher.
- **[MVP]** — included in the minimum viable path if you fall behind.

Citations are full: author(s), title, edition where relevant, publisher, year. Where a translator matters, it's noted.

### Time budget

- 24 months × ~5 hrs/week ≈ 480 hrs total.
- Suggested per-week split: **Math 2.5 hrs · Classical ML 2 hrs · History 0.5 hrs.**
- The math track is the most ambitious. If you slip, slow math first; the ML reading will signal when more math is needed.

### How to use this document

Each phase is structured identically:

1. **Goal** — what you should be able to do after.
2. **Prerequisites** — which earlier phases (in any track) it depends on.
3. **Primary readings** — the spine, in suggested order.
4. **Supplementary readings** — additional or alternative.
5. **Papers** — primary literature where relevant.
6. **Exercises and implementation work** — what to actually do beyond reading.
7. **Minimum viable path** — what to keep if you have to cut.
8. **Time estimate**.

The 24-month calendar at the end of this document interleaves all three tracks. Use it as a default and adjust to your pace.

---

## Sequencing rationale

Three principles drive the ordering:

1. **Math leads ML.** Each math phase finishes ahead of the ML phase that needs it: measure theory before probabilistic ML; convex optimization before SVMs; functional analysis before kernel methods and Gaussian processes.
2. **ML moves from the geometric/algorithmic to the probabilistic/inferential.** Start with the data-centric, easily visualized ESL/trees worldview; build to the more abstract probabilistic and Bayesian view; finish with unsupervised and sequential models, which depend on both.
3. **History runs throughout as a slow background thread.** Nilsson early to anchor the timeline; primary sources interleaved with the technical material they illuminate (Vapnik during SVMs, Pearl during graphical models, the PDP volumes during the connectionist sections).

---

# Track 1 — Mathematics

A five-phase rebuild from foundations through statistical learning theory math. The Phase M1 → M5 ordering is strict; later phases assume earlier ones.

## Phase M1 — Linear algebra and analysis foundations

**Time: ~2 months (≈20–22 hrs)**

### Goal

Achieve operator-theoretic fluency with finite-dimensional vector spaces — inner products, dual spaces, adjoints, spectral theorem, singular value decomposition — and refresh the analysis machinery (metric spaces, modes of convergence, compactness, continuity) that downstream phases will assume.

### Prerequisites

Undergraduate linear algebra and real analysis. No earlier phases.

### Primary readings

- **[Primary] [Free] [MVP]** Sheldon Axler, *Linear Algebra Done Right*, 4th ed., Springer (Undergraduate Texts in Mathematics), 2024.
  *Strict avoidance of determinants until the end; clean abstract treatment of operators, inner product spaces, and the spectral theorem. The 4th edition (open access) is the version to use.*
  Target chapters: 1–7 in full, 8–9 for context.

### Supplementary readings

- **[Supplementary] [Free]** Sergei Treil, *Linear Algebra Done Wrong*, self-published, latest revision available on Treil's homepage (Brown University).
  *Determinant-friendly companion to Axler; useful if Axler's determinant-late approach feels artificial after physics.*

- **[Supplementary]** Paul R. Halmos, *Finite-Dimensional Vector Spaces*, 2nd ed., Springer (Undergraduate Texts in Mathematics), 1974 (orig. Van Nostrand, 1958).
  *The original abstract-operator treatment. Concise, opinionated, still excellent.*

- **[Supplementary]** Lloyd N. Trefethen and David Bau III, *Numerical Linear Algebra*, SIAM, 1997.
  *The numerical perspective: conditioning, stability, QR, SVD as computational objects. Lectures 1–10 are essential reading for anyone doing applied ML.*

- **[Supplementary]** Walter Rudin, *Principles of Mathematical Analysis*, 3rd ed., McGraw-Hill, 1976.
  *Reference only. Re-read Chapters 2–4 (metric spaces, compactness, continuity) and Chapter 7 (sequences and series of functions) if your analysis is rusty.*

### Exercises and implementation work

- Axler's exercises are good but not numerous; do at least one-third of the exercises in Chapters 5–7.
- Implement SVD from scratch in Python (one-sided Jacobi or Golub–Kahan) and verify against `numpy.linalg.svd`.

### Minimum viable path

Axler chapters 1–7 + Trefethen & Bau lectures 1–10.

---

## Phase M2 — Measure-theoretic probability and mathematical statistics

**Time: ~3 months (≈32–34 hrs)**

### Goal

Develop a working understanding of measure-theoretic probability sufficient to read modern ML theory: σ-algebras, measurable functions, Lebesgue integration as expectation, modes of convergence (a.s., in probability, in distribution, in Lᵖ), the law of large numbers and central limit theorem from a measure-theoretic standpoint, and conditional expectation. Plus a thorough refresh of inference: estimators, sufficiency, consistency, asymptotic normality, hypothesis testing, and Bayesian basics.

### Prerequisites

M1 (especially analysis refresh).

### Primary readings

- **[Primary] [MVP]** David Williams, *Probability with Martingales*, Cambridge University Press (Cambridge Mathematical Textbooks), 1991.
  *The compact, elegant introduction. Williams gets to martingales (which you will not use heavily here but which make conditional expectation click) in under 200 pages. Chapters 1–9 are core; 10–14 are bonus.*

- **[Primary]** Larry Wasserman, *All of Statistics: A Concise Course in Statistical Inference*, Springer (Springer Texts in Statistics), 2004.
  *Fast, broad, ML-oriented overview of inference. Use as the inference spine.*

### Supplementary readings

- **[Supplementary]** Rick Durrett, *Probability: Theory and Examples*, 5th ed., Cambridge University Press (Cambridge Series in Statistical and Probabilistic Mathematics), 2019. Free PDF on the author's Duke homepage.
  *More extensive than Williams; the standard graduate American text. Use as a backup reference, especially for the LLN/CLT chapters.*

- **[Supplementary]** Patrick Billingsley, *Probability and Measure*, 3rd ed. (anniversary edition), Wiley (Wiley Series in Probability and Statistics), 1995.
  *Older, gentler than Durrett. Excellent if you want to take the measure-theoretic plumbing very slowly.*

- **[Supplementary]** George Casella and Roger L. Berger, *Statistical Inference*, 2nd ed., Duxbury (now Cengage), 2002.
  *More leisurely than Wasserman. Use if Wasserman's brevity bites; particularly strong on sufficiency and exponential families.*

- **[Supplementary]** Erich L. Lehmann and George Casella, *Theory of Point Estimation*, 2nd ed., Springer (Springer Texts in Statistics), 1998.
  *Reference-grade. Don't read cover-to-cover; consult for UMVU, Cramér–Rao, asymptotic theory of estimators.*

- **[Primary]** Thomas M. Cover and Joy A. Thomas, *Elements of Information Theory*, 2nd ed., Wiley (Wiley Series in Telecommunications and Signal Processing), 2006.
  *Promoted to primary because entropy, mutual information, KL divergence, the data-processing inequality, and Fano's inequality recur across every later phase. Chapters 1–4, 7–8 minimum.*

### Exercises and implementation work

- Wasserman has compact problem sets; do at least Ch. 5–11 odd-numbered problems.
- Simulate the LLN and CLT in Python for a few distributions (e.g., Cauchy to see what *fails*).
- Compute KL divergences between common parametric families analytically and verify numerically.

### Minimum viable path

Williams chapters 1–9 + Wasserman chapters 1–14 + Cover & Thomas chapters 1–4.

---

## Phase M3 — Optimization

**Time: ~2 months (≈22 hrs)**

### Goal

Convex analysis to working depth (convex sets, convex functions, dual cones, conjugate functions, Lagrangian duality, KKT conditions); convex optimization algorithms (gradient methods, Newton, interior-point, proximal); a working overview of non-convex methods (line search, trust region, stochastic gradient methods).

### Prerequisites

M1.

### Primary readings

- **[Primary] [Free] [MVP]** Stephen Boyd and Lieven Vandenberghe, *Convex Optimization*, Cambridge University Press, 2004. Free PDF on Boyd's Stanford homepage.
  *The standard. Chapters 1–5 (theory: convex sets, convex functions, problems, duality) are non-negotiable. Chapters 9–11 (unconstrained, equality-constrained, interior-point methods) cover the algorithms ML actually uses. Skim 6–8 for applications and skip 12 unless interested.*

- **[Primary]** Jorge Nocedal and Stephen J. Wright, *Numerical Optimization*, 2nd ed., Springer (Springer Series in Operations Research and Financial Engineering), 2006.
  *The non-convex / large-scale companion. Chapters 2–6 (line search, trust region, conjugate gradient, quasi-Newton) and Chapter 7 (large-scale unconstrained) are the relevant parts for ML.*

### Supplementary readings

- **[Supplementary] [Free]** Sébastien Bubeck, *Convex Optimization: Algorithms and Complexity*, Foundations and Trends in Machine Learning, vol. 8, no. 3–4, 2015. arXiv:1405.4980.
  *Modern, compact, complexity-aware. Read after Boyd & Vandenberghe's algorithmic chapters as a contemporary lens.*

- **[Supplementary]** R. Tyrrell Rockafellar, *Convex Analysis*, Princeton University Press (Princeton Mathematical Series), 1970.
  *The classical reference. Read selectively if you want the deepest convex-analytic foundations; otherwise leave on the shelf.*

- **[Supplementary]** Dimitri P. Bertsekas, *Nonlinear Programming*, 3rd ed., Athena Scientific, 2016.
  *An alternative non-convex reference; pick this over Nocedal & Wright only if you prefer Bertsekas's exposition style.*

### Exercises and implementation work

- Implement gradient descent, Newton's method, BFGS, and ADMM from scratch on quadratic and logistic regression problems.
- Solve a small SOCP by hand using KKT conditions before phase C3.

### Minimum viable path

Boyd & Vandenberghe chapters 1–5 + 9–10 + Nocedal & Wright chapters 2–3.

---

## Phase M4 — Functional analysis and geometry

**Time: ~3 months (≈32 hrs)**

### Goal

Hilbert and Banach spaces, bounded linear operators, dual spaces, spectral theory of compact operators, and reproducing kernel Hilbert spaces. Plus an entry-level treatment of smooth manifolds and information geometry for the geometric view of statistical models.

### Prerequisites

M1 thoroughly; M2 (for the probabilistic side of RKHS); M3 (helpful for variational viewpoints).

### Primary readings

- **[Primary] [MVP]** Erwin Kreyszig, *Introductory Functional Analysis with Applications*, Wiley (Wiley Classics Library), 1989 (orig. 1978).
  *The gentlest serious entry into functional analysis. Chapters 1–4 (metric, normed, Banach, inner product, Hilbert spaces) and 9–10 (linear operators, spectral theory in normed spaces) are core.*

- **[Primary]** Alain Berlinet and Christine Thomas-Agnan, *Reproducing Kernel Hilbert Spaces in Probability and Statistics*, Kluwer Academic Publishers, 2004.
  *The reference work specifically on RKHS. Chapters 1–3 give the foundations needed for kernel methods, Gaussian processes, and modern non-parametric inference.*

### Supplementary readings

- **[Supplementary]** Michael Reed and Barry Simon, *Methods of Modern Mathematical Physics, Volume I: Functional Analysis*, rev. and enlarged ed., Academic Press, 1980.
  *Physics-friendly functional analysis at a higher level than Kreyszig. Recommended specifically because of your physics background: the operator-theoretic intuition from quantum mechanics translates directly.*

- **[Supplementary]** Haïm Brezis, *Functional Analysis, Sobolev Spaces and Partial Differential Equations*, Springer (Universitext), 2011.
  *The more rigorous modern reference. Substitute for Kreyszig only if you want full rigor and don't mind a steeper climb.*

- **[Supplementary]** John B. Conway, *A Course in Functional Analysis*, 2nd ed., Springer (Graduate Texts in Mathematics 96), 1990.
  *Another standard. Particularly clear on operator theory.*

- **[Supplementary]** Loring W. Tu, *An Introduction to Manifolds*, 2nd ed., Springer (Universitext), 2011.
  *The gentlest path into smooth manifolds. Chapters 1–11 are enough for information-geometry purposes.*

- **[Supplementary]** John M. Lee, *Introduction to Smooth Manifolds*, 2nd ed., Springer (Graduate Texts in Mathematics 218), 2013.
  *The more thorough modern reference if Tu feels too compressed. Pick one; do not read both.*

- **[Supplementary]** Shun-ichi Amari, *Information Geometry and Its Applications*, Springer (Applied Mathematical Sciences 194), 2016.
  *The book on natural gradient and statistical manifolds. Chapters 1–6 (foundations) and the chapters on the natural gradient are the relevant ML connection.*

### Exercises and implementation work

- Verify the reproducing property for the Gaussian and polynomial kernels by hand.
- Implement kernel ridge regression from scratch using only NumPy.
- Compute the Fisher information matrix for a logistic regression model and verify the natural gradient update for one step.

### Minimum viable path

Kreyszig chapters 1–4, 9–10 + Berlinet & Thomas-Agnan chapters 1–2.

---

## Phase M5 — Statistical learning theory mathematics

**Time: ~2 months (≈22 hrs)**

### Goal

The mathematical machinery of generalization: concentration of measure (Hoeffding, Bernstein, McDiarmid, Talagrand), uniform convergence, VC theory, Rademacher complexity, covering numbers, PAC-Bayes. By the end, you should be able to read a paper proving an excess-risk bound and understand each step.

### Prerequisites

M1, M2, M3, M4.

### Primary readings

- **[Primary]** Stéphane Boucheron, Gábor Lugosi, and Pascal Massart, *Concentration Inequalities: A Nonasymptotic Theory of Independence*, Oxford University Press, 2013.
  *The reference on the mathematical machinery itself. Chapters 1–6 cover essentially every concentration inequality you will encounter.*

- **[Primary] [MVP]** Mehryar Mohri, Afshin Rostamizadeh, and Ameet Talwalkar, *Foundations of Machine Learning*, 2nd ed., MIT Press (Adaptive Computation and Machine Learning), 2018.
  *The cleanest bridge from the math of concentration to PAC learning, VC theory, Rademacher complexity, and applications. Chapters 1–6 are core.*

### Supplementary readings

- **[Supplementary] [Free]** Shai Shalev-Shwartz and Shai Ben-David, *Understanding Machine Learning: From Theory to Algorithms*, Cambridge University Press, 2014. Free PDF on Shalev-Shwartz's homepage.
  *A more pedagogical alternative to Mohri et al. — pick one as primary and use the other for cross-reading.*

- **[Supplementary]** Roman Vershynin, *High-Dimensional Probability: An Introduction with Applications in Data Science*, Cambridge University Press (Cambridge Series in Statistical and Probabilistic Mathematics 47), 2018. Author's free pre-publication PDF on his homepage.
  *Concentration in high dimensions, sub-Gaussian random variables, random matrices. Selective reading; Chapters 2–3, 5 are the most useful.*

- **[Supplementary]** Martin J. Wainwright, *High-Dimensional Statistics: A Non-Asymptotic Viewpoint*, Cambridge University Press, 2019.
  *Companion volume to Vershynin in spirit; focus is on statistical estimation in high dimensions.*

- **[Supplementary]** Vladimir N. Vapnik, *Statistical Learning Theory*, Wiley (Adaptive and Learning Systems for Signal Processing, Communications, and Control), 1998.
  *Vapnik's own book — historically essential and dense. Read after Mohri et al. for the original formulation of VC theory.*

- **[Supplementary]** Aad W. van der Vaart, *Asymptotic Statistics*, Cambridge University Press (Cambridge Series in Statistical and Probabilistic Mathematics 3), 1998.
  *Reference for asymptotic theory, useful when comparing classical and learning-theoretic bounds.*

### Exercises and implementation work

- Re-prove Hoeffding's inequality from the moment generating function bound.
- Derive a generalization bound for the linear classifier class via Rademacher complexity.
- Numerically estimate the Rademacher complexity of a small function class on synthetic data.

### Minimum viable path

Mohri, Rostamizadeh, Talwalkar chapters 1–6 + Boucheron, Lugosi, Massart chapters 1–3.

---

# Track 2 — Classical (Pre-Deep-Learning) Machine Learning

A six-phase comprehensive treatment, from the supervised-learning foundations through trees, kernel methods, probabilistic and graphical models, sequential models, and unsupervised methods including anomaly detection.

## Phase C1 — Statistical learning foundations

**Time: ~2 months (≈22 hrs)**

### Goal

Build the conceptual map of the field: the supervised learning setup, linear and generalized linear models, regularization (ridge, lasso, elastic net), basis expansions and splines, bias-variance, cross-validation, model assessment.

### Prerequisites

M1; M2 in progress in parallel.

### Primary readings

- **[Primary] [Free] [MVP]** Trevor Hastie, Robert Tibshirani, and Jerome Friedman, *The Elements of Statistical Learning: Data Mining, Inference, and Prediction*, 2nd ed. (corrected 12th printing), Springer (Springer Series in Statistics), 2009. Free PDF on Tibshirani's Stanford homepage.
  *The anchor textbook for the classical-ML half of this curriculum. Chapters 1–7 (introduction, supervised learning overview, linear methods for regression, linear methods for classification, basis expansions and regularization, kernel smoothing, model assessment and selection) in full.*

### Supplementary readings

- **[Supplementary] [Free]** Gareth James, Daniela Witten, Trevor Hastie, and Robert Tibshirani, *An Introduction to Statistical Learning: with Applications in Python*, Springer (Springer Texts in Statistics), 2023. Also Python edition free PDF, plus the original R edition (2nd ed., 2021).
  *A gentler on-ramp to ESL. Use if any ESL chapter is opaque.*

- **[Supplementary] [Free]** Trevor Hastie, Robert Tibshirani, and Martin Wainwright, *Statistical Learning with Sparsity: The Lasso and Generalizations*, CRC Press (Chapman & Hall/CRC Monographs on Statistics and Applied Probability 143), 2015. Free PDF on Hastie's homepage.
  *Deep dive on regularization. Chapters 1–4 alongside ESL chapter 3.*

### Exercises and implementation work

- Implement from scratch in NumPy: OLS, ridge regression, lasso (coordinate descent), logistic regression (Newton-Raphson), LDA and QDA.
- Reproduce the bias-variance decomposition empirically using a simulated dataset.
- Implement K-fold cross-validation and confirm it produces unbiased risk estimates on synthetic data.

### Minimum viable path

ESL chapters 1–7.

---

## Phase C2 — Trees, forests, and gradient boosting

**Time: ~1.5 months (≈16 hrs)**

### Goal

Master the family of tree-based methods that dominate tabular ML and that you already use professionally: CART, bagging, random forests, AdaBoost, gradient boosting, and the modern implementations (XGBoost, LightGBM, CatBoost). Be able to derive split criteria, implement CART and a basic gradient booster from scratch, and explain rigorously what XGBoost's regularization, sparsity-aware split finding, and approximate quantile sketch contribute.

### Prerequisites

C1; M1.

### Primary readings

- **[Primary] [Historical]** Leo Breiman, Jerome Friedman, Richard Olshen, and Charles Stone, *Classification and Regression Trees*, Wadsworth, 1984.
  *The foundational text. Chapters 1–4 (introduction, the tree-growing procedure, splitting rules, pruning) and Chapter 8 (regression trees) are core.*

- **[Primary]** ESL chapters 9 (additive models, trees, MARS), 10 (boosting), 15 (random forests). Read alongside the papers below.

### Supplementary readings

- **[Supplementary] [Historical]** J. Ross Quinlan, *C4.5: Programs for Machine Learning*, Morgan Kaufmann (Morgan Kaufmann Series in Machine Learning), 1993.
  *The other classical tree algorithm. Read selectively; useful for the information-gain / gain-ratio perspective and historical contrast with CART.*

### Papers (in suggested reading order)

- **[Historical]** Leo Breiman, "Bagging Predictors," *Machine Learning* 24 (2): 123–140, 1996.
- **[Historical]** Yoav Freund and Robert E. Schapire, "A Decision-Theoretic Generalization of On-Line Learning and an Application to Boosting," *Journal of Computer and System Sciences* 55 (1): 119–139, 1997. (AdaBoost.)
- **[Historical]** Leo Breiman, "Random Forests," *Machine Learning* 45 (1): 5–32, 2001.
- **[Historical]** Jerome H. Friedman, "Greedy Function Approximation: A Gradient Boosting Machine," *Annals of Statistics* 29 (5): 1189–1232, 2001.
- **[Historical]** Jerome H. Friedman, "Stochastic Gradient Boosting," *Computational Statistics & Data Analysis* 38 (4): 367–378, 2002.
- Tianqi Chen and Carlos Guestrin, "XGBoost: A Scalable Tree Boosting System," *KDD '16*, pp. 785–794, 2016.
- Guolin Ke et al., "LightGBM: A Highly Efficient Gradient Boosting Decision Tree," *NeurIPS 2017*.
- Liudmila Prokhorenkova et al., "CatBoost: Unbiased Boosting with Categorical Features," *NeurIPS 2018*.
- **[Historical]** Leo Breiman, "Statistical Modeling: The Two Cultures," *Statistical Science* 16 (3): 199–231, 2001. (Read this once before or after the rest — it's the cultural manifesto of the tree/forest school.)

### Exercises and implementation work

- Implement CART from scratch in Python for both regression and classification, including pruning.
- Implement a basic gradient boosting machine on top of your CART, using squared-error loss and then log-loss.
- Reproduce one of the XGBoost benchmark experiments on a UCI dataset and compare to your implementation; understand where the speedup and accuracy gap come from.

### Minimum viable path

ESL chapters 9, 10, 15 + Breiman 2001 (RF) + Friedman 2001 (GBM) + Chen & Guestrin 2016 (XGBoost).

---

## Phase C3 — Kernel methods and support vector machines

**Time: ~2 months (≈22 hrs)**

### Goal

Understand kernels as inner products in feature spaces (Mercer's theorem, RKHS perspective from M4), the SVM optimization problem in primal and dual form, the kernel trick, kernel ridge regression, and the broader family of regularized risk minimization in RKHS.

### Prerequisites

M3 (duality, KKT); M4 (Hilbert spaces, RKHS); C1.

### Primary readings

- **[Primary] [MVP]** Bernhard Schölkopf and Alexander J. Smola, *Learning with Kernels: Support Vector Machines, Regularization, Optimization, and Beyond*, MIT Press (Adaptive Computation and Machine Learning), 2002.
  *The canonical kernel-methods textbook. Chapters 1–7 are core; 11–12 cover SVM regression and one-class SVM.*

- **[Primary]** ESL chapter 12 (Support Vector Machines and Flexible Discriminants).

### Supplementary readings

- **[Supplementary]** Ingo Steinwart and Andreas Christmann, *Support Vector Machines*, Springer (Information Science and Statistics), 2008.
  *The more mathematically rigorous treatment, with full RKHS development. Use this if Schölkopf & Smola feels under-rigorous for your taste.*

- **[Supplementary]** Bernhard Schölkopf, Alexander J. Smola, and Klaus-Robert Müller, "Nonlinear Component Analysis as a Kernel Eigenvalue Problem," *Neural Computation* 10 (5): 1299–1319, 1998. (Kernel PCA — read before unsupervised methods in C6.)

### Papers (in suggested reading order)

- **[Historical]** Bernhard E. Boser, Isabelle M. Guyon, and Vladimir N. Vapnik, "A Training Algorithm for Optimal Margin Classifiers," *COLT '92*, 1992. (The original kernel-SVM paper.)
- **[Historical]** Corinna Cortes and Vladimir Vapnik, "Support-Vector Networks," *Machine Learning* 20 (3): 273–297, 1995.
- Christopher J. C. Burges, "A Tutorial on Support Vector Machines for Pattern Recognition," *Data Mining and Knowledge Discovery* 2 (2): 121–167, 1998.
- Thomas Hofmann, Bernhard Schölkopf, and Alexander J. Smola, "Kernel Methods in Machine Learning," *Annals of Statistics* 36 (3): 1171–1220, 2008.

### Exercises and implementation work

- Derive the SVM dual from scratch, including the KKT conditions for the soft-margin version.
- Implement a small SMO-style SVM solver in Python.
- Implement kernel ridge regression and reproduce a regression problem from ESL.
- Implement kernel PCA on a non-linearly separable synthetic dataset.

### Minimum viable path

Schölkopf & Smola chapters 1–7 + ESL chapter 12 + Cortes & Vapnik 1995.

---

## Phase C4 — Probabilistic machine learning and graphical models

**Time: ~3 months (≈32 hrs)**

### Goal

The probabilistic/Bayesian view of ML: naive Bayes, generative vs. discriminative classifiers, mixture models and EM, Bayesian linear regression, Gaussian processes, Bayesian networks, Markov random fields, exact and approximate inference (variable elimination, junction trees, loopy BP, variational methods, MCMC).

### Prerequisites

M2 thoroughly; C1.

### Primary readings

- **[Primary] [Free] [MVP]** Christopher M. Bishop, *Pattern Recognition and Machine Learning*, Springer (Information Science and Statistics), 2006. Free PDF released by Microsoft Research in 2024.
  *The other anchor textbook of this curriculum. The probabilistic spine of the phase. Chapters 1–4 (introduction, probability, linear models for regression, linear models for classification), 8 (graphical models), 9 (mixture models and EM), 10 (variational inference), 11 (sampling), 13 (HMMs and linear dynamical systems).*

- **[Primary] [Free]** Kevin P. Murphy, *Probabilistic Machine Learning: An Introduction*, MIT Press (Adaptive Computation and Machine Learning), 2022.
  *Modern, comprehensive, and the natural companion / successor to Bishop. Free PDF on Murphy's homepage. Use as cross-reference and for any topic where you find Bishop dated.*

- **[Primary] [Free]** Kevin P. Murphy, *Probabilistic Machine Learning: Advanced Topics*, MIT Press (Adaptive Computation and Machine Learning), 2023.
  *Advanced companion. Selective reading; particularly Chapters 1–7 for graphical-model inference at modern depth.*

### Supplementary readings

- **[Supplementary] [Free]** David J. C. MacKay, *Information Theory, Inference, and Learning Algorithms*, Cambridge University Press, 2003. Free PDF on MacKay's homepage.
  *Idiosyncratic, brilliant, and the bridge between information theory and Bayesian ML. Read Parts II (probability and inference) and IV (probabilistic data modelling) at minimum.*

- **[Supplementary] [Free]** David Barber, *Bayesian Reasoning and Machine Learning*, Cambridge University Press, 2012. Free PDF on Barber's UCL homepage.
  *Alternative comprehensive probabilistic ML textbook. Use as a third opinion when Bishop and Murphy disagree.*

- **[Supplementary]** Daphne Koller and Nir Friedman, *Probabilistic Graphical Models: Principles and Techniques*, MIT Press (Adaptive Computation and Machine Learning), 2009.
  *The PGM reference. Read selectively — Chapters 3 (Bayesian networks), 4 (undirected models), 9 (variable elimination), 11 (cluster graphs and belief propagation).*

- **[Supplementary] [Free]** Carl Edward Rasmussen and Christopher K. I. Williams, *Gaussian Processes for Machine Learning*, MIT Press (Adaptive Computation and Machine Learning), 2006. Free PDF on the book's homepage.
  *The GP reference. Read Chapters 1–5 alongside Bishop's chapter 6.*

- **[Supplementary] [Free]** Martin J. Wainwright and Michael I. Jordan, "Graphical Models, Exponential Families, and Variational Inference," *Foundations and Trends in Machine Learning* 1 (1–2): 1–305, 2008.
  *The monograph on exponential-family graphical models and variational inference. Dense but excellent once Bishop chapter 10 has primed you.*

- **[Supplementary] [Historical]** Judea Pearl, *Probabilistic Reasoning in Intelligent Systems: Networks of Plausible Inference*, Morgan Kaufmann (Morgan Kaufmann Series in Representation and Reasoning), 1988.
  *The book that introduced Bayesian networks. Read at least Chapters 1–4 for the original formulation. Doubles as a Track 3 reading.*

### Exercises and implementation work

- Implement naive Bayes (Gaussian and multinomial) from scratch.
- Implement EM for Gaussian mixture models and verify on a 2D synthetic dataset.
- Implement Bayesian linear regression with full posterior computation and predictive distributions.
- Implement Gaussian process regression on a small dataset; hand-derive the marginal likelihood.
- Implement variable elimination on a small Bayesian network by hand and in code.
- Implement a basic mean-field variational inference algorithm for a Gaussian mixture model.

### Minimum viable path

Bishop chapters 1–4, 8, 9, 10, 13 + Murphy (PML 1) chapters cross-referenced.

---

## Phase C5 — Time series and sequential models

**Time: ~1.5 months (≈16 hrs)**

### Goal

Classical time series: stationarity, ARIMA, state-space models, Kalman filtering and smoothing. Hidden Markov models from first principles: forward-backward, Viterbi, Baum-Welch (HMM-EM). Particle filtering basics.

### Prerequisites

M2; C4 (specifically, HMMs build on the EM and graphical-model material).

### Primary readings

- **[Primary] [MVP]** Peter J. Brockwell and Richard A. Davis, *Introduction to Time Series and Forecasting*, 3rd ed., Springer (Springer Texts in Statistics), 2016.
  *The gentlest serious time series text. Chapters 1–6 cover stationarity, ARMA models, forecasting, model identification, and state-space basics.*

- **[Primary] [Free]** Simo Särkkä, *Bayesian Filtering and Smoothing*, Cambridge University Press (Institute of Mathematical Statistics Textbooks 3), 2013. Free PDF on Särkkä's Aalto homepage.
  *The clearest modern treatment of Kalman, extended Kalman, unscented, and particle filters from a unified Bayesian perspective. Chapters 1–7 are core.*

### Supplementary readings

- **[Supplementary]** James D. Hamilton, *Time Series Analysis*, Princeton University Press, 1994.
  *The econometric/statistical classic. Dense; consult selectively for state-space models (chapter 13) and vector autoregressions (chapter 11).*

- **[Supplementary] [Free]** Robert H. Shumway and David S. Stoffer, *Time Series Analysis and Its Applications: With R Examples*, 4th ed., Springer (Springer Texts in Statistics), 2017. Free PDF (EZ edition) on Stoffer's Pitt homepage.
  *More applied than Brockwell & Davis; use as a third reference.*

- **[Supplementary] [Free]** Rob J. Hyndman and George Athanasopoulos, *Forecasting: Principles and Practice*, 3rd ed., OTexts, 2021. Free at otexts.com/fpp3.
  *Applied forecasting. Read if you want the most direct production-oriented treatment.*

### Papers

- **[Historical]** Lawrence R. Rabiner, "A Tutorial on Hidden Markov Models and Selected Applications in Speech Recognition," *Proceedings of the IEEE* 77 (2): 257–286, 1989.
  *The HMM reference paper. Section II and III are essential.*

### Exercises and implementation work

- Implement an ARIMA model from scratch (parameter estimation by MLE; forecasting by recursion).
- Implement a Kalman filter and smoother on a 1D tracking problem.
- Implement the forward-backward algorithm, Viterbi, and Baum-Welch for an HMM with discrete observations from scratch.

### Minimum viable path

Brockwell & Davis chapters 1–6 + Särkkä chapters 1–4 + Rabiner 1989.

---

## Phase C6 — Unsupervised learning: clustering, dimensionality reduction, anomaly detection

**Time: ~2 months (≈22 hrs)**

### Goal

K-means and its variants; hierarchical and spectral clustering; PCA and its extensions (probabilistic PCA, kernel PCA, ICA); manifold learning (Isomap, LLE, t-SNE, UMAP); anomaly detection (statistical methods, isolation forest, one-class SVM, density-based methods, autoencoder-based methods at the conceptual level).

### Prerequisites

M1, M4 (kernel PCA, manifold methods); C3 (one-class SVM); C4 (probabilistic PCA, mixture-based clustering).

### Primary readings

- **[Primary]** ESL chapter 14 (Unsupervised Learning) — the spine. Read in full.

- **[Primary] [MVP]** I. T. Jolliffe, *Principal Component Analysis*, 2nd ed., Springer (Springer Series in Statistics), 2002.
  *The PCA reference. Read selectively — Chapters 1–4, 6, 9, 10 cover the standard material plus probabilistic extensions and robust variants.*

- **[Primary]** Charu C. Aggarwal, *Outlier Analysis*, 2nd ed., Springer, 2017.
  *The comprehensive textbook on anomaly detection. Chapters 1–8 cover statistical, proximity, linear, high-dimensional, and ensemble-based methods. Directly relevant to your fraud work.*

### Supplementary readings

- **[Supplementary]** Christopher M. Bishop, *Pattern Recognition and Machine Learning*, chapter 12 (continuous latent variables — probabilistic PCA, factor analysis, ICA, kernel PCA).

### Papers (in suggested reading order)

- **[Historical]** Joshua B. Tenenbaum, Vin de Silva, and John C. Langford, "A Global Geometric Framework for Nonlinear Dimensionality Reduction," *Science* 290 (5500): 2319–2323, 2000. (Isomap.)
- **[Historical]** Sam T. Roweis and Lawrence K. Saul, "Nonlinear Dimensionality Reduction by Locally Linear Embedding," *Science* 290 (5500): 2323–2326, 2000. (LLE.)
- **[Historical]** Laurens van der Maaten and Geoffrey Hinton, "Visualizing Data using t-SNE," *Journal of Machine Learning Research* 9: 2579–2605, 2008.
- Leland McInnes, John Healy, and James Melville, "UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction," arXiv:1802.03426, 2018.
- **[Historical]** Bernhard Schölkopf, John C. Platt, John Shawe-Taylor, Alex J. Smola, and Robert C. Williamson, "Estimating the Support of a High-Dimensional Distribution," *Neural Computation* 13 (7): 1443–1471, 2001. (One-class SVM.)
- **[Historical]** Fei Tony Liu, Kai Ming Ting, and Zhi-Hua Zhou, "Isolation Forest," *ICDM 2008*, pp. 413–422, 2008.
- Varun Chandola, Arindam Banerjee, and Vipin Kumar, "Anomaly Detection: A Survey," *ACM Computing Surveys* 41 (3), article 15, 2009.
  *Read this survey first as a structural map of the field — extremely relevant to fraud detection.*

### Exercises and implementation work

- Implement K-means (Lloyd's algorithm) and K-means++ initialization from scratch.
- Implement PCA from scratch via the SVD and via the eigendecomposition of the covariance matrix; compare numerical behavior.
- Implement isolation forest from scratch on a fraud-style benchmark (e.g., UCI Credit Card Fraud).
- Compare one-class SVM, isolation forest, and a simple autoencoder-based anomaly score on the same benchmark.

### Minimum viable path

ESL chapter 14 + Chandola, Banerjee, Kumar 2009 + Liu et al. 2008 + Schölkopf et al. 2001.

---

# Track 3 — History and the GOFAI Tradition

A four-phase parallel reading thread at ~0.5 hrs/week. The point is contextual understanding, not implementation; treat these as books to read on the train or in the evening rather than at a desk.

## Phase H1 — Big-picture histories

**Time: ~1 month at 0.5 hrs/week**

### Goal

Get the timeline straight: from the Dartmouth conference through the early symbolic systems, the perceptron and its critique, the first AI winter, expert systems and the second winter, the statistical learning turn, and the lead-up to deep learning.

### Primary readings

- **[Primary] [Free] [MVP]** Nils J. Nilsson, *The Quest for Artificial Intelligence: A History of Ideas and Achievements*, Cambridge University Press, 2010. Free PDF on Stanford CS.
  *Written by a major participant in the symbolic-AI era. The single best historical overview.*

### Supplementary readings

- **[Supplementary]** Pamela McCorduck, *Machines Who Think: A Personal Inquiry into the History and Prospects of Artificial Intelligence*, 2nd ed., A K Peters, 2004 (orig. W. H. Freeman, 1979).
  *More cultural and journalistic; many first-hand interviews. Excellent complement to Nilsson.*

- **[Supplementary]** Daniel Crevier, *AI: The Tumultuous History of the Search for Artificial Intelligence*, Basic Books, 1993.
  *Older but useful for the 1980s-perspective on early AI history.*

- **[Supplementary]** Margaret A. Boden, *Mind as Machine: A History of Cognitive Science*, 2 vols., Oxford University Press, 2006.
  *The most thorough scholarly history of cognitive science (which contains AI as a major thread). Reference only; very long.*

- **[Supplementary]** Michael Wooldridge, *A Brief History of Artificial Intelligence: What It Is, Where We Are, and Where We Are Going*, Flatiron Books, 2021.
  *Modern, brief, popular. Useful as a one-week overview before Nilsson.*

### Minimum viable path

Nilsson, *The Quest for Artificial Intelligence*.

---

## Phase H2 — Foundational papers

**Time: ~1.5 months at 0.5 hrs/week**

### Goal

Read the primary sources of the field's founding generation.

### Primary readings (all [Historical])

- Alan M. Turing, "Computing Machinery and Intelligence," *Mind* 59 (236): 433–460, 1950.
- John McCarthy, Marvin L. Minsky, Nathaniel Rochester, and Claude E. Shannon, "A Proposal for the Dartmouth Summer Research Project on Artificial Intelligence," August 31, 1955. (The Dartmouth proposal.)
- Allen Newell and Herbert A. Simon, "The Logic Theory Machine: A Complex Information Processing System," *IRE Transactions on Information Theory* IT-2 (3): 61–79, 1956.
- Allen Newell, J. C. Shaw, and Herbert A. Simon, "Report on a General Problem-Solving Program," *Proceedings of the International Conference on Information Processing*, UNESCO House, pp. 256–264, 1959. (GPS.)
- John McCarthy, "Programs with Common Sense," in *Proceedings of the Teddington Conference on the Mechanization of Thought Processes*, HMSO, 1959.
- Marvin Minsky, "Steps Toward Artificial Intelligence," *Proceedings of the IRE* 49 (1): 8–30, 1961.
- Frank Rosenblatt, "The Perceptron: A Probabilistic Model for Information Storage and Organization in the Brain," *Psychological Review* 65 (6): 386–408, 1958.
- Marvin Minsky and Seymour Papert, *Perceptrons: An Introduction to Computational Geometry*, MIT Press, 1969 (expanded edition 1988). (Selective; read the introduction and the conclusion.)

### Supplementary readings

- **[Supplementary]** Martin Davis, *The Universal Computer: The Road from Leibniz to Turing*, W. W. Norton, 2000.
  *The pre-AI mathematical logic backstory: Leibniz, Frege, Cantor, Hilbert, Gödel, Turing. Essential context.*

### Minimum viable path

Turing 1950 + Dartmouth proposal + Newell & Simon 1956 + Minsky 1961 + Rosenblatt 1958 + Minsky & Papert 1969 (intro + conclusion).

---

## Phase H3 — GOFAI: search, planning, knowledge representation, classical probabilistic reasoning

**Time: ~1.5 months at 0.5 hrs/week**

### Goal

Understand the core of "good old-fashioned AI" — symbolic search and planning, formal knowledge representation, the move from logical AI to probabilistic reasoning that culminates in Pearl's Bayesian-network synthesis.

### Primary readings

- **[Primary] [MVP]** Stuart Russell and Peter Norvig, *Artificial Intelligence: A Modern Approach*, 4th ed., Pearson, 2020.
  *Read selectively. Chapters 3–5 (search), 7–10 (logical agents, first-order logic, inference, knowledge representation), 11 (automated planning), 12–13 (quantifying uncertainty, probabilistic reasoning). This is the textbook view — supplement it with Pearl below for the historical depth.*

- **[Primary]** Judea Pearl, *Probabilistic Reasoning in Intelligent Systems: Networks of Plausible Inference*, Morgan Kaufmann, 1988.
  *The book that effectively ended the "logic vs. probability" debate inside AI. Chapters 1–4 are required; the rest is reference. Doubles as a Track 2 reading.*

### Supplementary readings

- **[Supplementary] [Historical]** Judea Pearl, *Heuristics: Intelligent Search Strategies for Computer Problem Solving*, Addison-Wesley (Addison-Wesley Series in Artificial Intelligence), 1984.
  *Pearl on search. The state-of-the-art search treatment of its era.*

- **[Supplementary]** Ronald J. Brachman and Hector J. Levesque, *Knowledge Representation and Reasoning*, Morgan Kaufmann (Morgan Kaufmann Series in Artificial Intelligence), 2004.
  *The KR reference textbook. Selective reading.*

- **[Supplementary] [Historical]** John Haugeland, *Artificial Intelligence: The Very Idea*, MIT Press (Bradford Books), 1985.
  *The book that coined "GOFAI." Philosophy-of-AI more than technical. Read for the conceptual framing of the symbolic paradigm.*

### Minimum viable path

Russell & Norvig chapters 3–5, 7, 12–13 + Pearl 1988 chapters 1–4.

---

## Phase H4 — The shift from symbolic to statistical AI

**Time: ~1 month at 0.5 hrs/week**

### Goal

Understand the connectionist revival of the 1980s, the rise of expert systems and their commercial collapse, and the emergence of statistical learning theory as the dominant paradigm of the 1990s. End the curriculum positioned to read modern deep-learning history with the right framing.

### Primary readings

- **[Primary] [Historical] [MVP]** David E. Rumelhart and James L. McClelland (eds.), *Parallel Distributed Processing: Explorations in the Microstructure of Cognition*, 2 vols., MIT Press, 1986.
  *Read at minimum: Vol. 1, Chapter 1 (the general framework), Chapter 8 (backpropagation by Rumelhart, Hinton, and Williams). The book that reignited connectionism.*

- **[Primary] [Historical]** Vladimir N. Vapnik, "An Overview of Statistical Learning Theory," *IEEE Transactions on Neural Networks* 10 (5): 988–999, 1999.
  *Vapnik's own retrospective on the paradigm shift. Read this after C3.*

### Supplementary readings

- **[Supplementary]** Selected expert-systems papers:
  - Bruce G. Buchanan and Edward A. Feigenbaum, "DENDRAL and Meta-DENDRAL: Their Applications Dimension," *Artificial Intelligence* 11 (1–2): 5–24, 1978.
  - Edward H. Shortliffe, *Computer-Based Medical Consultations: MYCIN*, Elsevier, 1976. (Reference; do not read in full.)

- **[Supplementary] [Historical]** Douglas B. Lenat and R. V. Guha, *Building Large Knowledge-Based Systems: Representation and Inference in the Cyc Project*, Addison-Wesley, 1989. (Skim; read for the Cyc framing and its eventual failure modes.)

- **[Supplementary]** Yann LeCun, Yoshua Bengio, and Geoffrey Hinton, "Deep Learning," *Nature* 521 (7553): 436–444, 2015.
  *The retrospective that closes the pre-deep-learning era. Read last in the curriculum.*

### Minimum viable path

PDP Vol. 1 chapters 1 and 8 + Vapnik 1999 + LeCun, Bengio, Hinton 2015.

---

# Inter-track dependency map

| Math phase ends | Enables ML phase |
|---|---|
| M1 (linear algebra) | C1, C2 (basic linear algebra throughout); C6 (PCA, SVD) |
| M2 (measure-theoretic probability) | C4 (probabilistic ML); C5 (time series, HMMs) |
| M3 (convex optimization) | C2 (gradient boosting; numerical optimization); C3 (SVM duality and KKT) |
| M4 (functional analysis, RKHS) | C3 (kernel methods, RKHS); C4 (Gaussian processes); C6 (kernel PCA, manifold learning) |
| M5 (statistical learning theory math) | Post-curriculum: reading theoretical ML/DL papers |

| History phase | Pairs technically with |
|---|---|
| H1 (big-picture history) | C1 (sets the stage for ESL) |
| H2 (foundational papers) | C1, C2 (perceptrons, statistical-modeling debate) |
| H3 (GOFAI + Pearl) | C4 (probabilistic graphical models — Pearl is the bridge) |
| H4 (shift to statistical AI) | C3 (Vapnik's retrospective); end-of-curriculum reflection |

---

# Month-by-month calendar (24 months at ~5 hrs/week)

| Month | Math | Classical ML | History |
|---|---|---|---|
| 1 | M1 — Axler 1–4 | C1 — ESL 1–3 (in parallel) | H1 — Nilsson part I |
| 2 | M1 — Axler 5–7; Trefethen & Bau selected | C1 — ESL 3–4 | H1 — Nilsson part II |
| 3 | M2 — Williams 1–4 | C1 — ESL 5–7 | H1 — Nilsson part III; McCorduck (optional) |
| 4 | M2 — Williams 5–9; Cover & Thomas 1–2 | C2 — CART (Breiman et al.); ESL 9 | H2 — Turing 1950; Dartmouth |
| 5 | M2 — Wasserman 1–7 | C2 — RF, AdaBoost, GBM papers; ESL 10, 15 | H2 — Newell & Simon; Minsky 1961 |
| 6 | M2 — Wasserman 8–14; Cover & Thomas 3–4 | C2 — XGBoost, LightGBM, CatBoost; implementation | H2 — Rosenblatt; Minsky & Papert |
| 7 | M3 — Boyd & Vandenberghe 1–3 | C3 — Schölkopf & Smola 1–3; ESL 12 | H2 — Davis (background) |
| 8 | M3 — Boyd & Vandenberghe 4–5, 9 | C3 — Schölkopf & Smola 4–5; Cortes & Vapnik | H3 — Russell & Norvig 3–5 |
| 9 | M3 — Boyd & Vandenberghe 10; Nocedal & Wright 2–3 | C3 — Schölkopf & Smola 6–7; Burges tutorial | H3 — Russell & Norvig 7, 9–10 |
| 10 | M4 — Kreyszig 1–2 | C4 — Bishop 1–2 (in parallel) | H3 — Russell & Norvig 11–13 |
| 11 | M4 — Kreyszig 3–4 | C4 — Bishop 3–4 | H3 — Pearl 1988 (chapters 1–2) |
| 12 | M4 — Kreyszig 9–10 | C4 — Bishop 8 (graphical models); Pearl 1988 | H3 — Pearl 1988 (chapters 3–4) |
| 13 | M4 — Berlinet & Thomas-Agnan 1–2 | C4 — Bishop 9 (mixture models, EM); Murphy I cross-ref | H3 — Brachman & Levesque (selective) |
| 14 | M4 — Berlinet & Thomas-Agnan 3; Tu 1–5 | C4 — Bishop 10 (variational); Wainwright & Jordan | H4 — PDP Vol. 1, Ch. 1 |
| 15 | M4 — Tu 6–11; Amari 1–3 | C4 — Bishop 11 (sampling); Murphy II selected | H4 — PDP Vol. 1, Ch. 8 |
| 16 | M4 — Amari 4–6 | C4 — Bishop 13 (HMMs, LDS); Rasmussen & Williams 1–3 | H4 — DENDRAL/MYCIN papers |
| 17 | M5 — Mohri, Rostamizadeh, Talwalkar 1–3 | C5 — Brockwell & Davis 1–3 | H4 — Vapnik 1999 |
| 18 | M5 — Mohri et al. 4–6 | C5 — Brockwell & Davis 4–6; Särkkä 1–4 | H4 — LeCun, Bengio, Hinton 2015 |
| 19 | M5 — Boucheron, Lugosi, Massart 1–3 | C5 — Rabiner 1989; Särkkä 5–7 | Slack / reread Nilsson selectively |
| 20 | M5 — Boucheron, Lugosi, Massart 4–6 | C6 — ESL 14; Jolliffe 1–4 | Slack |
| 21 | M5 — Shalev-Shwartz & Ben-David (cross-reading) | C6 — Bishop 12; Tenenbaum/Roweis 2000 | Slack |
| 22 | M5 — Vershynin selected | C6 — t-SNE, UMAP | Slack / additional Pearl reading |
| 23 | Buffer / Wainwright selected | C6 — Aggarwal 1–5 | Slack |
| 24 | Buffer / Vapnik 1998 selected | C6 — Aggarwal 6–8; Chandola survey; isolation forest; one-class SVM | Slack / read deep-learning history retrospectives |

---

# Pacing notes, recovery, and what to cut first

Some honest realities to plan around:

- **24 months at 5 hrs/week is aggressive but feasible as a sustained habit.** Slipping to 30 months is normal and acceptable. The schedule above is the default, not a target.
- **Don't read every textbook cover to cover.** ESL, Bishop, Murphy, and Russell & Norvig should all live on your shelf and be consulted; the phase structure tells you what to look up.
- **Implement as you go.** ESL, kernel methods, trees, and graphical models all benefit enormously from from-scratch implementations. The exercises in each phase are recommendations, not optional homework.
- **Bishop and Murphy partially overlap with ESL.** Pick one as your primary text per phase and sample from the others.
- **If you fall behind, slow math first.** The ML reading will tell you what math you actually need next, and you can backfill specific math topics on demand once the broad foundations of M1–M3 are in place.
- **Cut order if behind**, from first-to-cut to last-to-cut: H1 supplementary → M4 manifold/info-geometry section (do without it) → C5 supplementary time-series texts → M5 Boucheron, Lugosi, Massart (read only Mohri et al. for SLT) → C2 LightGBM/CatBoost papers (XGBoost alone is enough). Do not cut: ESL, Bishop chapters 1–4 and 8–10, Boyd & Vandenberghe chapters 1–5, the M1 linear algebra phase, or Williams chapters 1–9.
- **Don't cut history entirely if pressed for time.** Even one chapter of Nilsson per month is more than most ML engineers ever read, and the payoff for situating modern AI in its lineage is large.

---

# After the curriculum

Once you finish, the following are natural next steps depending on which direction you want to push:

- **Deep learning, well-founded.** Goodfellow, Bengio, Courville, *Deep Learning* (MIT Press, 2016, free online) as the bridge, then move to modern theoretical work — implicit regularization, neural tangent kernel, double descent.
- **Causal inference.** Pearl, *Causality* (2nd ed., Cambridge, 2009); Hernán & Robins, *Causal Inference: What If* (free PDF).
- **Reinforcement learning.** Sutton & Barto, *Reinforcement Learning: An Introduction* (2nd ed., MIT Press, 2018, free PDF) as the canonical text.
- **Probabilistic programming and modern Bayesian computation.** Gelman et al., *Bayesian Data Analysis* (3rd ed., CRC, 2013); McElreath, *Statistical Rethinking* (2nd ed., CRC, 2020).
- **Theoretical machine learning research.** With M5 in place, you can read JMLR, NeurIPS theory track, COLT papers directly.

By that point, the foundations will support any of these without further backfilling.