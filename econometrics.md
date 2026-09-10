# Econometrics: A Balanced Curriculum for a Machine Learner
### Theory + causal identification + the ML frontier · full time-series pillar · built on your stats foundations

**Orientation:** theory-forward, and balanced across the three areas you asked to weight equally — **econometric theory** (asymptotics, GMM), **causal inference / identification** (the credibility revolution), and the **econometrics↔ML frontier** (double ML, causal forests) — with **time-series as a full pillar**. This is built *on* your existing statistical and ML foundations: probability, linear algebra, regression, MLE, and asymptotics are assumed and reframed, not re-taught. A running **"new vs. ML"** flag marks what's genuinely novel relative to your training (mostly: identification and structure) versus what's a re-framing of what you know (mostly: estimation and inference).

**The spine of the whole field, and the thing that separates it from ML:** *identification is not estimation, and causation is not prediction.* ML excels at estimation and prediction and is largely silent on identification; econometrics is the discipline built around it. Every phase returns to this.

**Python note:** even in a theory-forward treatment, your native ecosystem is the natural companion — `statsmodels` and `linearmodels` (panel/IV), `arch` (GARCH), `statsmodels.tsa` (VAR/state-space), `EconML` (double ML, Python) and `grf` (causal forests, R via `rpy2`), and QuantEcon's Python time-series lectures. Flagged where relevant.

---

## Conventions

- **Calibration tags:** **[SETTLED]** (established method/result), **[CONTESTED]** (assumptions, interpretation, or the "right" estimator debated), **[HYPE]** (claims outrunning evidence), **[FRONTIER]** (active).
- **⊘ FREE** marks free resources — econometrics is exceptionally well-served (Hansen, Cunningham, Hernán–Robins, Train are all free and canonical).
- **⚡ new-vs-ML:** the field-specific bridge — since the whole subject overlaps your expertise, this flags what's *novel* (identification, structure) and what's a *re-framing* of ML you have.
- Each phase has an **MVP fast-path**; the assembled MVP spine is at the end.

---

## Your background as an accelerator (and where econometrics diverges)

You know estimation and inference cold. The mappings below are dense because the fields overlap heavily — but note the recurring theme: the *machinery* transfers, the *identification logic* is the new part.

1. **OLS = orthogonal projection; Frisch–Waugh–Lovell = residualization.** FWL (partialling out) is Gram–Schmidt orthogonalization — and it's the conceptual seed of double ML. → Phases 1, 10.
2. **M-estimation = empirical risk minimization.** The asymptotics of extremum estimators are the asymptotics of ERM; the sandwich variance is robustness under misspecification. → Phase 2.
3. **GMM = moment matching / estimating equations.** Optimal weighting is inverse-covariance (whitening); GMM nests OLS, IV, and MLE as special cases. → Phase 3.
4. **Kalman filter = recursive Bayesian filtering (linear-Gaussian LDS).** You already have this; econometrics uses it for unobserved-components and DSGE estimation. → Phase 8.
5. **Discrete-choice logit = softmax; GARCH = conditional heteroskedasticity; ARMA = LTI filters; unit root = random walk/diffusion; spectral analysis = Fourier/power spectra.** All re-framings of things you know. → Phases 6–9.
6. **Double ML = Neyman-orthogonal moments + cross-fitting.** Out-of-fold prediction + a debiasing correction — your toolkit, deployed for valid causal inference. Causal forests = random forests adapted for treatment effects. Dynamic discrete choice = estimating an MDP (inverse RL). MSM/indirect inference = simulation-based / likelihood-free inference (ABC). → Phases 9–10.
7. **The genuinely new part — identification.** Potential outcomes, the fundamental problem of causal inference, unconfoundedness, exclusion restrictions, and quasi-experimental designs (IV/DiD/RDD) have no real ML analogue. This is what to slow down for. → Phases 4–5.

---

## Prerequisites & co-requisites

**Assumed (you have it):** probability and distributions, LLN/CLT, linear algebra, linear regression, MLE, and the conceptual content of asymptotics. **Not re-taught.**

**Helpful co-reqs from the other tracks:** the micro track (structural econometrics estimates micro models — discrete choice, demand, dynamic choice); the macro track (its Phase 8 on VARs/local projections/identification overlaps this track's Phase 8, and DSGE estimation connects to state-space methods). This track is otherwise self-contained.

---

## Dependency map

```
        Phase 0  Prereqs (confirmation — light for you)
             │
        Phase 1  The econometric framework: regression reframed
             │
        Phase 2  Asymptotic theory (the math-stat spine)
             │
        Phase 3  MLE, GMM & the estimation frameworks
           /        │         \
   Phase 4        Phase 6       Phase 7
   Causal I:      Panel &       Time-series I:
   potential      nonlinear/    univariate &
   outcomes       LDV models    nonstationarity
      │                             │
   Phase 5                      Phase 8
   Causal II:                   Time-series II:
   IV/DiD/RDD/                  VAR/SVAR/GARCH/
   synthetic control           state-space
      │                             │
      └──────────► Phase 9  Structural econometrics ◄────┘
                        │
                   Phase 10  The econometrics↔ML frontier (capstone)
```

**Reading:** 0→1→2→3 is the theory spine (fast for you). Phase 3 (GMM) unlocks the three parallel branches — causal (4→5), micro-econometrics (6), and time-series (7→8). Structural (9) draws on GMM, discrete choice (6), and simulation. Phase 10 (the ML frontier) is the capstone and draws on causal (4–5) and high-dimensional theory. Fastest balanced route: 0→1→3→4→5→7→8→10.

---

# PHASE 0 — Prerequisites & Placement
*Light. Mostly confirming the econometric conventions on top of your stats.*

- **Goal:** align notation and conventions (econometric vs. ML/statistical), confirm the asymptotics and linear-algebra toolkit.
- **Primary:** skim the front matter of **Bruce Hansen, *Econometrics*** (⊘ FREE, ssc.wisc.edu/~bhansen) — the spine for the whole track.
- **⊘ FREE:** Hansen; QuantEcon Python lectures for the computational side.
- **Calibration:** **[SETTLED]** foundations.
- **⚡ new-vs-ML:** nothing new yet — this is your existing stats in econometric clothing.
- **Time:** 1–2 weeks (or skip).
- **MVP:** skip.

---

# PHASE 1 — The Econometric Framework: Regression Reframed
*Fast, but conceptually load-bearing — it installs the causation-vs-prediction distinction.*

- **Goal:** re-see regression through the econometric lens — the CEF, projection, robust inference — and internalize the "two cultures" split that organizes the field.
- **Prerequisites:** Phase 0.
- **Topics:** the **conditional expectation function** and OLS as its best linear approximation; **best linear predictor vs. best predictor**; the **Frisch–Waugh–Lovell theorem** (partialling out); the classical linear model, Gauss–Markov, and where its assumptions fail; **heteroskedasticity-robust and cluster-robust standard errors** (the modern default); Breiman's **"two cultures"** and how econometrics' goals (inference, causation) differ from ML's (prediction).
- **Primary:** **Hansen, *Econometrics*** (regression chapters); **Angrist & Pischke, *Mostly Harmless Econometrics*** (the causal-reframing classic — ch. 3 on regression); **Wooldridge, *Econometric Analysis of Cross Section and Panel Data*** (the comprehensive reference).
- **⊘ FREE:** Hansen; **Nick Huntington-Klein, *The Effect*** (theeffectbook.net) — excellent modern intro to regression-for-causality.
- **Calibration:** OLS/Gauss–Markov **[SETTLED]**; robust/clustered SEs **[SETTLED]** and now standard.
- **⚡ new-vs-ML:** FWL = residualization/Gram–Schmidt (familiar); the *new* idea is that a regression coefficient's *meaning* (predictive slope vs. causal effect) depends on assumptions outside the data — the prediction/causation split ML rarely forces you to confront.
- **Exercises:** prove FWL and use it to interpret a multivariate coefficient; derive the robust variance estimator; construct a case where the best linear predictor and the causal effect diverge.
- **Time:** 3–4 weeks.
- **MVP:** CEF + FWL + robust inference + the two-cultures framing; this phase is already near-minimal.

---

# PHASE 2 — Asymptotic Theory: The Mathematical-Statistics Spine
*Formalizes the asymptotics you use heuristically. Fast for a physicist.*

- **Goal:** the rigorous large-sample theory — the tools that prove estimators are consistent and asymptotically normal.
- **Prerequisites:** Phase 1.
- **Topics:** modes of convergence; **LLN, CLT, continuous mapping, the delta method**; **consistency and asymptotic normality**; **M-estimation / extremum estimators** (the unifying asymptotic framework); asymptotic efficiency; the **sandwich (robust) variance** under misspecification.
- **Primary:** **Hansen, *Econometrics*** (asymptotic-theory chapters); **Newey & McFadden, "Large Sample Estimation and Hypothesis Testing"** (Handbook of Econometrics — the definitive chapter); **van der Vaart, *Asymptotic Statistics*** (for full math-stat rigor — you'll appreciate it); White, *Asymptotic Theory for Econometricians*.
- **⊘ FREE:** Hansen; Newey–McFadden circulates freely.
- **Calibration:** **[SETTLED]**; the standing caveat is finite-sample vs. asymptotic behavior (addressed by the bootstrap and finite-sample corrections).
- **⚡ new-vs-ML:** M-estimation asymptotics = the asymptotics of ERM (you have this implicitly); delta method = error propagation (physics); the sandwich variance formalizes robustness-under-misspecification that ML treats loosely.
- **Exercises:** prove consistency and asymptotic normality of an M-estimator; derive the asymptotic variance of a nonlinear function via the delta method; show OLS is a special case.
- **Time:** 4–6 weeks (faster if the math-stat is already comfortable).
- **MVP:** the M-estimation consistency/normality results + the delta method + the sandwich variance; skip measure-theoretic depth.

---

# PHASE 3 — Maximum Likelihood, GMM & the Estimation Frameworks
*GMM is the unifying idea of graduate econometrics — it nests almost everything.*

- **Goal:** the two great estimation frameworks — likelihood and moments — and how GMM organizes the entire field.
- **Prerequisites:** Phase 2.
- **Topics:** **MLE** (econometric framing: information matrix, Cramér–Rao, the LR/Wald/LM test trilogy, **quasi-MLE** and robustness); the method of moments; **GMM** (Hansen 1982 — moment conditions, the optimal weighting matrix, **overidentification and the J-test**, efficiency, two-step vs. continuously-updated GMM); minimum-distance estimation; and how GMM **nests OLS, IV, and MLE** as special cases.
- **Primary:** **Hayashi, *Econometrics*** (the best GMM-centric graduate text — organizes everything around GMM); **Hansen, *Econometrics***; **Hansen (1982)** original GMM paper; Newey–McFadden.
- **⊘ FREE:** Hansen; lecture notes (e.g., MIT 14.382) circulate.
- **Calibration:** MLE and GMM **[SETTLED]**; GMM as *the* organizing framework **[SETTLED]** — it's the language modern econometrics is written in.
- **⚡ new-vs-ML:** GMM = moment matching / estimating equations (connects to moment-matching estimators and even GAN-style objectives); optimal weighting = inverse-covariance/whitening; the *new* part is using **economic-theory-implied moment conditions** (from equilibrium/optimality) as the estimating equations — the bridge to structural estimation (Phase 9).
- **Exercises:** derive the GMM estimator and its asymptotic variance; show OLS and 2SLS are GMM; compute and interpret the J-test; derive the LR/Wald/LM equivalence.
- **Time:** 5–6 weeks.
- **MVP:** GMM (moment conditions, optimal weighting, J-test) + MLE test trilogy; this is the theory you don't want to compress.

---

# PHASE 4 — Causal Inference I: Potential Outcomes & the Credibility Revolution
*The conceptual crown jewel — and the part ML training almost always skips. Slow down here.*

- **Goal:** the potential-outcomes framework and the logic of identification — what it takes to move from correlation to a credible causal claim.
- **Prerequisites:** Phase 1 (independent of the time-series branch).
- **Topics:** the **Rubin/Neyman potential-outcomes model**; the **fundamental problem of causal inference**; **selection bias**; estimands (ATE, ATT, LATE); **randomization and RCTs** as the benchmark; **regression and causality** (omitted-variable bias, "bad controls," collider bias); the **DAG / structural-causal-model** perspective (Pearl) alongside potential outcomes; **unconfoundedness/ignorability** (and why it's untestable); **matching, propensity scores, and doubly-robust estimation**.
- **Primary:** **Angrist & Pischke, *Mostly Harmless Econometrics***; **Cunningham, *Causal Inference: The Mixtape*** (⊘ FREE, causalinference.org, code-heavy); **Imbens & Rubin, *Causal Inference for Statistics, Social, and Biomedical Sciences*** (the rigorous potential-outcomes bible); **Hernán & Robins, *Causal Inference: What If*** (⊘ FREE, strong on DAGs); **Pearl, *Causality*** (the SCM/DAG view).
- **⊘ FREE:** Cunningham, Hernán–Robins, Huntington-Klein's *The Effect*.
- **Calibration:** the potential-outcomes framework **[SETTLED]**; **unconfoundedness is a strong, untestable assumption** — the crux of all selection-on-observables work; the **Pearl (DAGs) vs. Rubin (potential outcomes)** framing is often presented as a rivalry but is **largely complementary [CONTESTED presentation, reconcilable substance]**.
- **⚡ new-vs-ML (the big one):** identification ≠ estimation. Potential outcomes = counterfactuals; selection bias = the gap between observational and interventional distributions; the propensity score is a treatment-probability model you can fit with any ML method — *but valid inference requires orthogonalization*, which foreshadows Phase 10. This is the phase where your ML instincts must yield to identification logic.
- **Exercises:** decompose the naive difference-in-means into ATT + selection bias; draw DAGs that reveal a "bad control"; derive the doubly-robust estimator and show its double-robustness property.
- **Time:** 5–7 weeks.
- **MVP:** potential outcomes + selection bias + unconfoundedness + propensity scores/doubly-robust; defer the DAG formalism depth.

---

# PHASE 5 — Causal Inference II: The Quasi-Experimental Toolkit
*The workhorse designs — including the difference-in-differences revolution, a genuinely live frontier.*

- **Goal:** the four canonical identification strategies and how to deploy and critique each.
- **Prerequisites:** Phase 4.
- **Topics:**
  - **Instrumental variables:** 2SLS; the **LATE theorem** (Imbens–Angrist — relevance, exclusion, monotonicity); **weak instruments** (Stock–Yogo, the first-stage F); many-instrument problems; modern IV designs (judge/examiner, shift-share/Bartik).
  - **Difference-in-differences:** the canonical 2×2; **two-way fixed effects and its pitfalls** — the staggered-adoption / negative-weights problem (**Goodman-Bacon** decomposition), and the new robust estimators (**Callaway–Sant'Anna, de Chaisemartin–D'Haultfœuille, Sun–Abraham**); event-study designs and parallel-trends testing.
  - **Regression discontinuity:** sharp and fuzzy; **local polynomial estimation** and bandwidth choice; **robust bias-correction** (Calonico–Cattaneo–Titiunik); RD as a design; the McCrary density test.
  - **Synthetic control:** Abadie–Diamond–Hainmueller; **synthetic difference-in-differences** (Arkhangelsky et al.).
- **Primary:** **Angrist & Pischke**; **Cunningham, *The Mixtape***; **Roth, Sant'Anna, Bilinski & Poe (2023), "What's Trending in Difference-in-Differences?"** (the survey of the DiD revolution); **Cattaneo, Idrobo & Titiunik** RD monographs. Python: `linearmodels`, and the DiD/RD packages (`differences`, `rdrobust`).
- **⊘ FREE:** Cunningham, Huntington-Klein; the DiD/RD methods papers are working papers.
- **Key original readings:** Imbens–Angrist (1994) LATE; Card–Krueger (1994) minimum wage (the DiD classic); Goodman-Bacon (2021); Callaway–Sant'Anna (2021); Calonico–Cattaneo–Titiunik (2014); Abadie–Diamond–Hainmueller (2010).
- **Calibration:** IV/2SLS **[SETTLED]** but the LATE interpretation and weak-instrument fragility are **[CONTESTED in practice]** (what population does your estimate describe?); **the DiD literature is genuinely [FRONTIER]** — the TWFE pitfalls were only widely recognized around 2018–2021 and the "correct" estimator is actively evolving, so anything relying on staggered-adoption TWFE needs the modern correction; RD **[SETTLED]** as a design with settled bias-correction; synthetic control **[SETTLED→FRONTIER]**, still developing.
- **⚡ new-vs-ML:** these designs have *no ML analogue* — they exploit exogenous variation (an instrument, a discontinuity, a policy timing) to identify effects. IV = isolating a causal channel via an exogenous perturbation; RD = local randomization at a threshold; DiD = differencing out fixed confounders. This is the toolkit that makes you dangerous in a way pure ML doesn't.
- **Exercises:** derive 2SLS as IV-GMM and interpret the LATE; run a Goodman-Bacon decomposition and see why naive TWFE misleads under staggered adoption; estimate a sharp RD with robust bias-correction; build a synthetic control for a case study.
- **Time:** 7–9 weeks (the biggest causal phase).
- **MVP:** IV + LATE, modern DiD (the TWFE problem + one robust estimator), and RD with bias-correction; defer synthetic control and shift-share.

---

# PHASE 6 — Panel Data & Nonlinear / Limited-Dependent-Variable Models
*Micro-econometrics staples — several directly relevant to fraud (duration, counts, rare events).*

- **Goal:** the estimation of panel and nonlinear/limited-dependent-variable models.
- **Prerequisites:** Phase 3 (GMM for dynamic panels).
- **Topics:** **panel data** (fixed vs. random effects; within/between/first-difference; **dynamic panels** — Arellano–Bond, Blundell–Bond system GMM; clustering and inference); **binary choice** (logit/probit — the ML side you know, re-derived from latent-variable and random-utility foundations); **multinomial and ordered** models; **count data** (Poisson, negative binomial, QMLE); **censoring/truncation** (Tobit); **sample selection** (Heckman); **duration/hazard models** (relevant to time-to-event problems like fraud and churn).
- **Primary:** **Wooldridge, *Econometric Analysis of Cross Section and Panel Data*** (THE reference); **Cameron & Trivedi, *Microeconometrics: Methods and Applications*** (comprehensive, strong on counts and panels); Arellano, *Panel Data Econometrics*. Python: `linearmodels` (panel), `statsmodels` (GLM/duration).
- **⊘ FREE:** lecture notes; Wooldridge's problem sets circulate.
- **Key original readings:** Arellano–Bond (1991); Blundell–Bond (1998); Heckman (1979).
- **Calibration:** panel FE/RE **[SETTLED]**; dynamic-panel GMM **[SETTLED]** but with finite-sample/weak-instrument concerns; **Heckman selection is [SETTLED but identification-fragile]** — it leans on exclusion restrictions that are often thin.
- **⚡ new-vs-ML:** logit/Poisson = your GLM/softmax knowledge re-derived from random-utility/latent-variable foundations; **hazard models = survival analysis** (directly useful for fraud/time-to-event); QMLE = robustness under distributional misspecification; the *new* part is the fixed-effects logic for removing unobserved confounders in panels.
- **Exercises:** derive the within estimator and show it removes unit fixed effects; set up Arellano–Bond for a dynamic panel; derive the Heckman two-step and identify what makes it work; fit a proportional-hazards model to a duration outcome.
- **Time:** 5–7 weeks.
- **MVP:** panel FE + dynamic-panel GMM + logit/probit foundations + hazard models; defer Tobit and multinomial depth.

---

# PHASE 7 — Time-Series I: Univariate Models & Nonstationarity
*(Full pillar, part 1.) The foundations, including the traps unique to time series.*

- **Goal:** stationary time-series modeling and the theory of nonstationarity, unit roots, and cointegration.
- **Prerequisites:** Phase 2 (independent of the causal branch).
- **Topics:** **stationarity and ergodicity**; **ARMA/ARIMA** modeling and the Wold decomposition; **autocovariance and spectral analysis**; **forecasting** and forecast evaluation (Diebold–Mariano); **nonstationarity** — **unit roots** (Dickey–Fuller, ADF, Phillips–Perron, KPSS) and their low power; **spurious regression** (Granger–Newbold); deterministic vs. stochastic trends; **cointegration** (Engle–Granger two-step, error-correction models) with the multivariate Johansen approach set up for Phase 8.
- **Primary:** **Hamilton, *Time Series Analysis*** (the graduate bible — your spine for both time-series phases); **Enders, *Applied Econometric Time Series*** (more applied). Python: `statsmodels.tsa`, `arch`; QuantEcon time-series lectures.
- **⊘ FREE:** QuantEcon; lecture notes.
- **Key original readings:** Dickey–Fuller (1979); Granger–Newbold (1974) spurious regression; Engle–Granger (1987) cointegration.
- **Calibration:** ARMA/stationarity **[SETTLED]**; **unit-root tests are [SETTLED but low-power]** (hard to distinguish a near-unit-root from a unit root); cointegration **[SETTLED]**.
- **⚡ new-vs-ML:** spectral analysis = Fourier/power spectra (physics); ARMA = LTI linear filters; unit root = random walk / diffusion (a nonstationary process); the Wold decomposition = representing any stationary process as filtered white noise. The *new* econometric emphasis: nonstationarity breaks standard inference (spurious regression), which ML time-series often ignores.
- **Exercises:** derive the ARMA autocovariance and forecast; demonstrate spurious regression by simulation; run and interpret an ADF test; estimate an error-correction model for two cointegrated series.
- **Time:** 5–7 weeks.
- **MVP:** ARMA + forecasting + unit roots (ADF) + spurious regression + Engle–Granger cointegration; defer spectral depth.

---

# PHASE 8 — Time-Series II: Multivariate, Volatility & State-Space
*(Full pillar, part 2.) VARs, structural identification, GARCH, and the Kalman filter you already know.*

- **Goal:** multivariate dynamics, structural identification in time series, volatility modeling, and state-space methods.
- **Prerequisites:** Phase 7.
- **Topics:** **VARs** (estimation, lag selection, **Granger causality**, **impulse-response functions**, forecast-error variance decomposition); **structural VARs** — the identification problem and its solutions (recursive/**Cholesky**, short- and **long-run (Blanchard–Quah)** restrictions, **sign restrictions**, **external-instrument / proxy SVARs**); **multivariate cointegration** (Johansen VECM); **local projections** (Jordà — the modern alternative to VARs for impulse responses, and a bridge to the causal toolkit and the macro track's Phase 8); **volatility** (ARCH/GARCH — Engle, Bollerslev; EGARCH/GJR; stochastic volatility; realized volatility; multivariate GARCH/DCC); **state-space models and the Kalman filter** (linear-Gaussian state-space, unobserved-components models, the Kalman filter/smoother, and the link to DSGE estimation from the macro track).
- **Primary:** **Hamilton, *Time Series Analysis*** (VARs, Kalman, GARCH); **Lütkepohl, *New Introduction to Multiple Time Series Analysis*** (the definitive VAR/multivariate reference); **Kilian & Lütkepohl, *Structural Vector Autoregressive Analysis*** (the definitive SVAR text). Python: `statsmodels` (VAR, state-space), `arch` (GARCH).
- **⊘ FREE:** QuantEcon (Kalman, linear state-space); working-paper versions of the SVAR literature.
- **Key original readings:** Sims (1980) "Macroeconomics and Reality" (VARs); Blanchard–Quah (1989) long-run restrictions; Jordà (2005) local projections; Engle (1982) ARCH; Bollerslev (1986) GARCH.
- **Calibration:** VARs **[SETTLED]**; **SVAR identification is [CONTESTED]** — the identifying restrictions are assumptions, not data (the same "identification is where the action is" lesson as the causal phases, in time-series form); GARCH and Kalman/state-space **[SETTLED]**; **local projections vs. VARs is a live [methods debate]**, both valid with different trade-offs.
- **⚡ new-vs-ML:** the Kalman filter = recursive Bayesian filtering / linear dynamical systems (you have this); VAR = multivariate linear autoregression; GARCH = conditional-variance modeling (volatility clustering = heteroskedastic dynamics); state-space = hidden-state models (HMM/LDS). The *new* part is **structural identification of impulse responses** — extracting causal dynamics from the reduced-form VAR requires exactly the identification thinking from Phase 5.
- **Exercises:** estimate a VAR and compute IRFs with a Cholesky identification; contrast a Blanchard–Quah long-run identification; estimate a GARCH(1,1) and interpret volatility persistence; run the Kalman filter on an unobserved-components model.
- **Time:** 7–9 weeks (the biggest time-series phase).
- **MVP:** VARs + IRFs + one SVAR identification + GARCH(1,1) + the Kalman filter; defer sign-restrictions and multivariate GARCH.

---

# PHASE 9 — Structural Econometrics & Simulation-Based Estimation
*Where economic theory becomes the estimating equations — and where your simulation/RL skills transfer.*

- **Goal:** the structural approach — estimating the parameters of an economic model — and the simulation methods that make it feasible.
- **Prerequisites:** Phase 3 (GMM), Phase 6 (discrete choice).
- **Topics:** the **structural vs. reduced-form debate** (the Lucas-critique motivation — recap from macro; the experimentalist-vs-structuralist divide); **discrete-choice demand** (random-utility foundations; multinomial/nested/**mixed logit**; **BLP** — Berry–Levinsohn–Pakes, the workhorse of structural IO); **simulation-based estimation** (**method of simulated moments** — McFadden/Pakes–Pollard; **indirect inference** — Gouriéroux–Monfort; simulated MLE); **dynamic structural models** (**dynamic discrete choice** — Rust's nested fixed-point; **CCP estimation** — Hotz–Miller; estimating dynamic games).
- **Primary:** **Train, *Discrete Choice Methods with Simulation*** (⊘ FREE, eml.berkeley.edu/books/choice2.html — the definitive discrete-choice text); the **BLP (1995)** paper; **Rust (1987)**; the structural-econometrics Handbook chapters (Reiss–Wolak; Aguirregabiria–Mira for dynamics). Python: `pyblp` (BLP), and your own simulation code.
- **⊘ FREE:** Train; QuantEcon (dynamic programming, which underlies dynamic discrete choice).
- **Key original readings:** Berry–Levinsohn–Pakes (1995); Rust (1987); Hotz–Miller (1993); McFadden (1989) MSM.
- **Calibration:** discrete choice **[SETTLED]**; **BLP is [SETTLED] as the IO workhorse** but with well-known numerical and identification difficulties; **the structural-vs-experimental debate is [CONTESTED]** — a genuine, unresolved methodological divide (Angrist–Pischke experimentalists prize credible identification; structuralists prize counterfactual/policy portability), and both have real merit; dynamic structural estimation **[SETTLED methods, computationally heavy]**.
- **⚡ new-vs-ML (strong transfer):** discrete-choice logit = softmax (recurring); **MSM/indirect inference = simulation-based / likelihood-free inference** (ABC — you can map this to modern simulation-based inference in ML); **dynamic discrete choice = estimating an MDP = inverse reinforcement learning** (Rust's problem is "recover the reward/utility from observed optimal behavior" — precisely inverse RL). This phase is where your computational and RL background pays off directly.
- **Exercises:** estimate a mixed logit by simulated maximum likelihood; set up BLP's contraction mapping and moment conditions; implement Rust's nested-fixed-point for a simple dynamic discrete-choice problem and connect it to inverse RL.
- **Time:** 5–7 weeks.
- **MVP:** mixed logit + BLP overview + Rust's dynamic discrete choice (with the inverse-RL framing); defer indirect inference and dynamic games.

---

# PHASE 10 — The Econometrics↔ML Frontier
*(The third balanced pillar, as capstone.) Your exact sweet spot — using ML for valid causal inference.*

- **Goal:** the modern fusion of ML and econometrics — high-dimensional inference, double/debiased ML, and heterogeneous treatment effects — done correctly.
- **Prerequisites:** Phases 4–5 (causal), Phase 2 (theory).
- **Topics:**
  - **High-dimensional econometrics:** LASSO/ridge/elastic-net in an inference context; **why naive post-selection inference is invalid**; **post-double-selection** (Belloni–Chernozhukov–Hansen).
  - **Double/debiased machine learning:** **Chernozhukov et al. (2018)** — **Neyman orthogonality** and **cross-fitting**, and how they let you use arbitrary ML for the nuisance functions while getting √n-valid inference on the causal parameter.
  - **Heterogeneous treatment effects:** **causal forests** (Wager–Athey); **generalized random forests** (Athey–Tibshirani–Wager); the `grf`/`EconML` tooling.
  - **Panel/causal via ML:** matrix completion for causal panel data (Athey et al.).
  - **Policy learning:** optimal treatment rules (Athey–Wager; Kitagawa–Tetenov); the **prediction-policy problem** (Kleinberg et al.); **prediction vs. causation** (Mullainathan–Spiess).
  - **Text as data** (Gentzkow–Kelly–Taddy) and other modern applications.
- **Primary:** **Chernozhukov et al. (2018), "Double/Debiased Machine Learning for Treatment and Structural Parameters"**; **Athey & Imbens (2019), "Machine Learning Methods That Economists Should Know About"** (Annual Review of Economics — the map); **Mullainathan & Spiess (2017), "Machine Learning: An Applied Econometric Approach"** (JEP); Belloni–Chernozhukov–Hansen (2014). Python/R: **`EconML`** (Microsoft, Python — your language), **`grf`** and **`DoubleML`**.
- **⊘ FREE:** all the above are freely available papers; `EconML` and `grf` documentation are excellent free tutorials.
- **Key original readings:** Belloni–Chernozhukov–Hansen (2014); Chernozhukov et al. (2018); Wager–Athey (2018); Athey–Tibshirani–Wager (2019); Kleinberg–Ludwig–Mullainathan–Obermeyer (2015).
- **Calibration:** genuinely **[FRONTIER]** and fast-moving, but the core methods (double ML, causal forests) are increasingly **[SETTLED]** as of the early 2020s. The one **[SETTLED]** headline to carry away: **naive ML plugged into causal estimation gives invalid inference** — you must orthogonalize and cross-fit. Beware **[HYPE]** in "just throw a neural net at it" causal claims that skip the orthogonalization.
- **⚡ new-vs-ML (the payoff):** this whole phase is your home turf. Double ML = Neyman-orthogonal moment conditions + cross-fitting = a debiasing correction + out-of-fold prediction (both of which you know); causal forests = random forests adapted to estimate treatment effects with valid confidence intervals; policy learning = treating optimal-treatment-rule estimation as a learning problem. The synthesis is: *your ML toolkit is the engine for the nuisance functions, and econometric identification + orthogonalization is the steering.*
- **Exercises:** implement double ML for a partially-linear model with cross-fitting in `EconML` and show the bias without orthogonalization; fit a causal forest and interpret heterogeneous effects with valid CIs; contrast a prediction-policy problem with a causal-effect problem.
- **Time:** 5–7 weeks.
- **MVP:** post-double-selection + double ML (orthogonality + cross-fitting) + causal forests; defer policy learning and text-as-data. **Worth keeping in any MVP** — it's the phase that unifies this track with your existing expertise.

---

## The MVP fast-path (balanced core, ~4–6 months)

A route that keeps all three balanced areas plus core time-series, skipping Phases 0, 2 (you have the asymptotics), 6, and 9:

1. **Phase 1 MVP** — CEF + FWL + robust inference + two cultures. *(~3 wk)*
2. **Phase 3 MVP** — GMM (moment conditions, weighting, J-test) + MLE tests. *(~4 wk)*
3. **Phase 4 MVP** — potential outcomes + selection + unconfoundedness + doubly-robust. *(~4 wk)*
4. **Phase 5 MVP** — IV/LATE + modern DiD + RD with bias-correction. *(~6 wk)*
5. **Time-series core** (Phases 7–8 MVP) — ARMA + unit roots + cointegration + VAR/IRF + GARCH + Kalman. *(~7 wk)*
6. **Phase 10 MVP** — post-double-selection + double ML + causal forests. *(~5 wk)*

This hits theory (GMM), causal (potential outcomes + the quasi-experimental toolkit), time-series (the full core), and the ML frontier — the balance you asked for. It defers the full asymptotic-theory proofs, nonlinear/panel micro-econometrics, and structural estimation.

---

## Total timeline

| Route | Pace | Duration |
|---|---|---|
| **Full program** (Phases 0–10) | 8–12 hrs/wk | **~14–19 months** |
| **Balanced MVP** (above) | 8–12 hrs/wk | **~4–6 months** |

The largest track by phase count, but your background compresses Phases 0–3 substantially (you already own the statistical foundations). Phases 4–5, 7–8, and 9 run as three parallel branches after Phase 3. The one branch not to compress is causal (4–5) — it's the novel content.

---

## Editions & currency

The graduate canon is stable: **Wooldridge (2010), Hayashi (2000), Hamilton (1994), Lütkepohl (2005), Cameron–Trivedi (2005), Imbens–Rubin (2015), Angrist–Pischke (2009)** — all current standards. **Bruce Hansen's *Econometrics*** (free PDF, revised continually; print 2022) is the freshest rigorous spine — always grab the latest version. **Two areas move fast and live in journals/working papers:** the **difference-in-differences revolution** (2018–present — anything relying on staggered TWFE needs the modern estimators) and the **econometrics↔ML frontier** (double ML, causal forests, policy learning). Track those in recent issues and in the `EconML`/`grf`/`DoubleML` release notes.

---

## What I can build next

- The **combined economics study plan** sequencing all seven tracks into one coherent multi-year program — this is the natural capstone, and the tracks now cross-reference each other deliberately (micro is macro's co-req; behavioral deepens micro Phase 4; game theory discharges micro/behavioral spin-offs; this econometrics track is the empirical spine that macro Phase 8 and micro structural estimation both lean on).
- A **week-by-week reading schedule** across Phases 0–10 against your hrs/week.
- A **problem-set companion** with the ML-mapped derivations worked in full (GMM as moment-matching, double ML as orthogonalized cross-fitting, dynamic discrete choice as inverse RL, Kalman as recursive Bayesian filtering).
- A **causal-inference-only deep track** (potential outcomes → the full quasi-experimental toolkit → double ML/causal forests) if the identification apparatus is your real target — it's the highest-value corner for someone with your background.
- A **fraud-relevant applied-econometrics dossier** — the subset most directly usable in your work (causal impact evaluation, DiD/synthetic-control for policy changes, duration/hazard models, double ML for treatment effects at scale), mapped to your PayPal context.