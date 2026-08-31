# Reading List — Data Drift & Model Drift for Transactional Data

> Scope: balanced theory + applied, full detection-method scope (statistical, model-based, streaming/online), with emphasis on delayed-label and unsupervised settings. Brief adversarial coverage. Fraud-specific material flagged as supplementary.
>
> Estimated total runtime: ~44 hours across 8 weeks at ~5 hrs/week.
> ★ marks must-reads.

---

## Phase 1 — Taxonomy & theory of drift (week 1, ~10 hrs)

The vocabulary that lets the rest of the literature make sense. Read in order.

- ★ **Moreno-Torres, Raeder, Alaiz-Rodríguez, Chawla & Herrera (2012).** "A unifying view on dataset shift in classification." *Pattern Recognition* 45(1), 521–530. *(~1 hr)*
  The clearest formal split between covariate shift, prior probability shift, concept shift, and dataset shift. Anchor reference.

- ★ **Gama, Žliobaitė, Bifet, Pechenizkiy & Bouchachia (2014).** "A survey on concept drift adaptation." *ACM Computing Surveys* 46(4). *(~4–5 hrs)*
  The canonical survey. Long but every later paper references it.

- **Webb, Hyde, Cao, Nguyen & Petitjean (2016).** "Characterizing concept drift." *Data Mining and Knowledge Discovery* 30(4), 964–994. *(~2 hrs)*
  Formalizes drift typology (abrupt / incremental / gradual / recurring) and gives quantitative drift measures.

- **Lu, Liu, Dong, Gu, Gama & Zhang (2018).** "Learning under concept drift: A review." *IEEE TKDE* 31(12), 2346–2363. *(~3 hrs)*
  Updates Gama with stronger emphasis on detection methods. If short on time, read this *instead of* Gama.

---

## Phase 2 — Supervised streaming detectors (week 2, ~6 hrs)

Classical online detectors that monitor error rates. Pay attention to assumptions (Bernoulli error, i.i.d. within windows, etc.) — they break in fraud.

- **Gama, Medas, Castillo & Rodrigues (2004).** "Learning with drift detection." *Brazilian Symposium on AI (SBIA)*. *(~45 min)* — **DDM**.
- **Baena-García et al. (2006).** "Early drift detection method." *4th ECML PKDD Workshop on KDDS*. *(~45 min)* — **EDDM**, fixes DDM's sluggishness on gradual drift.
- ★ **Bifet & Gavaldà (2007).** "Learning from time-changing data with adaptive windowing." *SIAM SDM*. *(~1.5 hrs)* — **ADWIN**. Cleanest statistical guarantees; window size is automatic.
- **Frías-Blanco et al. (2014).** "Online and non-parametric drift detection methods based on Hoeffding's bounds." *IEEE TKDE* 27(3). *(~1.5 hrs)* — **HDDM-A/HDDM-W**.
- **Raab, Heusinger & Schleif (2020).** "Reactive Soft Prototype Computing for Concept Drift Streams." *Neurocomputing* 416. *(~1 hr)* — **KSWIN** introduced and benchmarked.
- **Page (1954).** "Continuous inspection schemes." *Biometrika* 41. *(~30 min)* — **Page–Hinkley**, the change-point statistic underneath much of the above. Short, classic.

---

## Phase 3 — Two-sample tests for input drift (week 3, ~7 hrs)

Drift as a hypothesis-testing problem. This is where most production tabular monitoring lives.

- ★ **Gretton, Borgwardt, Rasch, Schölkopf & Smola (2012).** "A kernel two-sample test." *JMLR* 13, 723–773. *(~3 hrs)*
  **MMD**. Heavy but worth it; the RKHS framing should land cleanly given your physics background, and MMD underlies most modern embedding-space drift detectors.

- **Sugiyama, Suzuki & Kanamori (2012).** *Density Ratio Estimation in Machine Learning.* Cambridge UP. *(~3 hrs, chapters 2–3)*
  KLIEP, uLSIF; reframes covariate shift as a density-ratio estimation problem.

- **Kifer, Ben-David & Gehrke (2004).** "Detecting change in data streams." *VLDB*. *(~1 hr)*
  Theoretical foundations for window-based two-sample testing on streams.

- **Yurdakul (2018).** *Statistical properties of population stability index.* MSc thesis, Western Michigan University. *(~1 hr)*
  No canonical PSI paper exists; this is the best reference for its actual distribution. Worth reading because PSI is what every fraud/credit shop uses, and most people don't know its statistical properties.

---

## Phase 4 — Unsupervised / label-free detection (week 4, ~7 hrs)

The realistic fraud setting outside of chargeback batches.

- **dos Reis, Flach, Matwin & Batista (2016).** "Fast unsupervised online drift detection using incremental Kolmogorov–Smirnov test." *KDD '16*. *(~1 hr)*
  Incremental KS, very practical baseline.

- **Sethi & Kantardzic (2017).** "On the reliable detection of concept drift from streaming unlabeled data." *Expert Systems with Applications* 82. *(~1.5 hrs)*
  Margin-density-based detection (MD3).

- ★ **Rabanser, Günnemann & Lipton (2019).** "Failing loudly: An empirical study of methods for detecting dataset shift." *NeurIPS*. *(~2 hrs)*
  The cornerstone empirical paper. Benchmarks univariate vs multivariate tests, dimensionality reduction strategies, classifier-based detection. Treat as your practical playbook.

- **Lipton, Wang & Smola (2018).** "Detecting and correcting for label shift with black box predictors." *ICML*. *(~1.5 hrs)*
  **BBSD.** Uses softmax outputs alone to detect label-distribution shift — directly relevant when fraud prevalence drifts.

- **Cerqueira, Gomes, Bifet & Torgo (2023).** "STUDD: A student–teacher method for unsupervised concept drift detection." *Machine Learning* 112(11), 4351–4378. arXiv:2103.00903. *(~1.5 hrs)*
  Mimicking-loss as drift proxy.

---

## Phase 5 — Tree ensembles & feature-importance drift (week 5, ~8 hrs)

Two threads. (A) Tree ensembles redesigned to adapt to drift natively. (B) Using feature importance / attributions themselves as a drift signal — directly relevant to your XAI work, since the same SHAP infrastructure becomes a monitoring substrate.

### 5A — Drift-aware tree ensembles

- **Bifet & Gavaldà (2009).** "Adaptive learning from evolving data streams." *IDA 2009.* *(~1.5 hrs)*
  **Hoeffding Adaptive Tree (HAT)** — pairs Hoeffding tree growth with ADWIN-monitored alternate subtrees. Each subtree carries its own change detector. Foundational for everything below.

- ★ **Gomes, Bifet, Read, Barddal, Enembreck, Pfahringer, Holmes & Abdessalem (2017).** "Adaptive random forests for evolving data stream classification." *Machine Learning* 106(9–10), 1469–1495. *(~2 hrs)*
  **ARF.** Online bagging + per-tree drift detectors (warning + drift levels) + background trees grown in parallel that swap in on confirmed drift. Pragmatic and strong baseline; cleanly implemented in River.

- **Gomes, Read & Bifet (2019).** "Streaming random patches for evolving data stream classification." *ICDM*. *(~1 hr)*
  **SRP** — random subsets of both instances and features per learner. Often outperforms ARF in high-dimensional settings; relevant when fraud features explode.

- **Montiel, Mitchell, Frank, Pfahringer, Abdessalem & Bifet (2020).** "Adaptive XGBoost for evolving data streams." *IJCNN*. *(~1 hr)*
  Push/replace strategies for boosted trees under drift. Closest streaming analogue to the gradient-boosted models you likely have in production.

- **Gunasekara, Pfahringer, Gomes & Bifet (2024).** "Streaming gradient boosted trees." *Machine Learning.* *(~1.5 hrs)*
  More recent, more rigorous treatment of streaming gradient boosting — uses XGBoost's weighted squared loss with explicit tree-replacement on drift detection. State of the art for the GBT-under-drift question as of writing.

### 5B — Feature importance as a drift signal

- ★ **Demšar & Bosnić (2018).** "Detecting concept drift in data streams using model explanation." *Expert Systems with Applications* 92, 546–559. *(~1.5 hrs)*
  **ExStream.** Computes per-instance attribute contributions via the EXPLAIN / IME methodology (precursor to SHAP), then monitors them with Page–Hinkley / SPC at three granularities: full attribution vector, per-feature streams, and per-(attribute, value) cells. The first principled paper on this idea.

- **Haug, Pawelczyk, Broelemann & Kasneci (2020).** "Leveraging model inherent variable importance for stable online feature selection." *KDD*. *(~1.5 hrs)*
  **FIRES.** Online feature selection from streaming Bayesian inference over model parameters — variable importance gets a posterior, which then becomes a natural drift-detection substrate.

- **Haug & Kasneci (2021).** "Learning parameter distributions to detect concept drift in data streams." *ICPR*. *(~1 hr)*
  **ERICS.** Posterior over model parameters → KL-divergence between time-adjacent posteriors as drift score. Lets you separate "the model parameters changed" from "the inputs changed" — useful when triangulating root cause.

- **Haug, Braun, Zürn & Kasneci (2022).** "Change detection for local explainability in evolving data streams." *CIKM*. arXiv:2209.02764. *(~1.5 hrs)*
  **CDLEEDS.** Detects when local feature attributions become stale and flags both local and global drift. Practical: a model-agnostic wrapper around SHAP/LIME for streams.

- **Lundberg, Erion, Chen, DeGrave, Prutkin, Nair, Katz, Himmelfarb, Bansal & Lee (2020).** "From local explanations to global understanding with explainable AI for trees." *Nature Machine Intelligence* 2(1), 56–67. *(~1.5 hrs)*
  Background reference: **TreeSHAP**'s polynomial-time algorithm is what makes SHAP-on-trees tractable at fraud-scale and is therefore the precondition for any of the SHAP-based monitoring schemes above. You may have read this already given your XAI work; if so, skim section 3.

#### A note on how to use 5B in practice

Three monitoring substrates emerge from 5B, in increasing operational ambition:

1. **Global feature-importance vectors over rolling windows.** Compute SHAP-aggregated feature importance per day (or per million transactions), then run any Phase 3 two-sample test on the importance vectors. Cheap, robust, often catches drift that input-distribution monitors miss because feature *interactions* shifted.

2. **Per-feature attribution distributions.** For each feature, monitor the distribution of its SHAP values (not the raw feature value) with PSI / KS. Catches cases where a feature's *role* changed even though its marginal distribution looks identical.

3. **Local-attribution drift** (CDLEEDS-style). Monitor cosine distance between current local attributions and a reference set. Most expensive but most sensitive; useful for triaging which transaction clusters are drifting.

In adversarial fraud, (2) tends to be the highest-signal-to-noise: attackers move attack volume across features faster than they move feature marginals, so SHAP-value-distribution shifts often lead input-distribution shifts by days or weeks.

### 5C — Feature importance for monitoring prioritization

A distinct use of importance: rather than treating attributions as the drift signal (5B), use them to *decide which features get a Phase 3 detector at all*. Top-K monitoring is the default in nearly every production fraud system, for three reasons.

**Why the pattern is valid.**

1. **Multiple-testing arithmetic.** With 500 features and PSI thresholds calibrated at single-feature significance, you'll see a parade of spurious alarms by construction (binomial expectation alone gives ~25 false positives per check at α = 0.05). Restricting to the top-K — say, top 20 features by cumulative mean |SHAP|, or features covering 80% of total importance mass — collapses the alert volume by orders of magnitude with minimal information loss.

2. **Performance relevance.** Drift in a feature with near-zero SHAP impact cannot move performance much. The whole point of monitoring is to predict performance change, and features the model relies on are the ones whose drift translates.

3. **Operational throughput.** Alerts on 20 features are triageable; alerts on 500 features are noise that trains the on-call to ignore them.

This pattern sits between two extremes. The maximally permissive end is "monitor every feature with FDR correction" — statistically clean but operationally dead. The maximally compressed end is **BBSD** (Lipton, Wang & Smola 2018, already in Phase 4): monitor only the softmax output, the model's own importance-weighted compression of everything. Top-K importance monitoring is the middle ground that keeps interpretability — "which feature drifted?" — while controlling alert volume.

**Practical design choices.**

- *Importance source.* Use SHAP global aggregates (mean |SHAP|) computed on a fixed reference window. Avoid scikit-learn's default Gini / MDI for monitoring purposes — it's biased toward high-cardinality and continuous features. Permutation importance is acceptable; SHAP is preferable because the same infrastructure powers your XAI deliverables.

- *Top-K selection rule.* Either fixed K (e.g. 20) or cumulative-importance threshold (features covering 80% of total |SHAP| mass). The latter adapts to models with different importance concentration; the former is operationally simpler. Pick one, document it, don't change without versioning the monitor.

- *Periodic re-ranking.* Recompute importance on retraining. Track the ranking itself as a separate signal — if your top-20 changes meaningfully between retrains, that *is* a drift signal (the model has discovered features that newly matter, or stopped relying on features it used to).

- *Sentinel multivariate monitor.* Always pair top-K univariate monitoring with a low-cost multivariate detector over the full feature space — MMD on a fixed embedding, classifier-based drift, or PCA-reconstruction-error as in NannyML's multivariate drift module. The sentinel catches the failure mode top-K monitoring is structurally blind to: drift in a currently-unimportant feature that signals an upcoming concept change. In adversarial fraud this matters specifically because attackers probe blind spots, and the blind spots are exactly the features you've stopped monitoring closely.

- *Importance-weighted aggregation* (softer variant). Monitor all features, but weight per-feature drift scores by normalized SHAP importance when aggregating to a single "feature drift" KPI. This is what Fiddler and Evidently do under the hood for their "feature drift impact on prediction" displays — useful as a single executive-dashboard number alongside the per-feature alerts.

**A fraud-specific caveat.** In fraud the correlation between model importance and adversarial value-of-attack is strong — attackers target what the model relies on, so top-K monitoring captures most of the adversarial drift surface for free. But the same logic implies attackers will deliberately probe low-importance dimensions to find blind spots. The multivariate sentinel is therefore non-optional in adversarial settings, regardless of how clean your top-K monitor looks on a given day.

**Production references.**

- ★ **Breck, Zinkevich, Polyzotis, Whang & Roy (2019).** "Data validation for machine learning." *MLSys.* *(~1.5 hrs)*
  Google's TFX data validation paper. The most rigorous treatment of feature-prioritized monitoring at production scale; describes Google's actual schema-based monitoring system. Covers training-serving skew, data drift, and the operational case for importance-prioritized alerting. Most directly relevant paper for this pattern.

- **Caveness, Suganthan, Peng, Polyzotis, Roy & Zinkevich (2020).** "TensorFlow data validation: Data analysis and validation in continuous ML pipelines." *SIGMOD.* *(~1 hr)*
  Continuation of Breck et al. with explicit focus on continuous monitoring patterns; useful complement.

- **Schelter, Lange, Schmidt, Celikel, Biessmann & Grafberger (2018).** "Automating large-scale data quality verification." *VLDB* 11(12), 1781–1794. *(~1 hr)*
  **Amazon Deequ.** Sister system to TFX from the Amazon side — declarative data-quality constraints over Spark, similar prioritized-monitoring philosophy. Good for seeing two independent industrial designs converging on the same pattern.

For the BBSD-as-extreme-case reference, see Lipton, Wang & Smola (2018) already in Phase 4.

---

## Phase 6 — Delayed labels & performance estimation without ground truth (week 6, ~8 hrs)

Operationally the most important section for fraud chargebacks (60–120 day lag).

- **Žliobaitė (2010).** "Change with delayed labelling: When is it detectable?" *ICDM Workshops*. *(~45 min)* — Theoretical limits; read first.
- **Grzenda, Gomes & Bifet (2020).** "Delayed labelling evaluation for data streams." *Data Mining and Knowledge Discovery* 34(5). *(~1.5 hrs)* — How to evaluate honestly under verification latency; read before designing your monitoring.
- **Plasse & Adams (2016).** "Handling delayed labels in temporally evolving data streams." *IEEE Big Data*. *(~1 hr)*
- ★ **Garg, Balakrishnan, Lipton, Neyshabur & Sedghi (2022).** "Leveraging unlabeled data to predict out-of-distribution performance." *ICLR*. *(~1.5 hrs)* — **ATC** (Average Thresholded Confidence). Single-threshold trick that frequently outperforms more elaborate schemes.
- **NannyML technical deep-dive on CBPE and DLE:** [nannyml.readthedocs.io/en/main/how_it_works/performance_estimation.html](https://nannyml.readthedocs.io/en/main/how_it_works/performance_estimation.html). *(~2 hrs)* — Read alongside Garg. CBPE assumes calibrated probabilities; DLE trains a child model to predict per-instance loss. Both deployable, both have clear failure modes worth understanding before you trust them.
- **Chen, Liu, Wu, Kailkhura, Ding & Cheng (2021).** "Detecting errors and estimating accuracy on unlabeled data with self-training ensembles." *NeurIPS*. *(~1 hr)* — Ensemble disagreement as performance signal.

---

## Phase 7 — Brief adversarial drift (week 7, ~2 hrs)

Per your scoping; just enough to know it's its own beast.

- **Sethi & Kantardzic (2018).** "Handling adversarial concept drift in streaming data." *Expert Systems with Applications* 97. *(~1 hr)*
- **Kantchelian, Tygar & Joseph (2016).** "Evasion and hardening of tree ensemble classifiers." *ICML*. *(~1 hr)* — Useful background on how attackers cause apparent drift.

---

## Supplementary — Fraud-specific applications

All from the ULB/Worldline line (Bontempi group), the canonical academic-industrial body of work on credit card fraud under drift.

- ★ **Dal Pozzolo, Boracchi, Caelen, Alippi & Bontempi (2018).** "Credit card fraud detection: A realistic modeling and a novel learning strategy." *IEEE TNNLS* 29(8), 3784–3797. *(~2 hrs)*
  Explicitly models verification latency, sample selection bias, and concept drift. **Most important single paper on this list for your work.**

- **Dal Pozzolo (2015).** *Adaptive machine learning for credit card fraud detection.* PhD thesis, ULB. *(~2 hrs, chapters 4–5, 7)*
  Deepest treatment of drift in fraud; thesis chapters expand on what the journal paper compresses.

- **Carcillo, Le Borgne, Caelen, Kessaci, Oblé & Bontempi (2021).** "Combining unsupervised and supervised learning in credit card fraud detection." *Information Sciences* 557. *(~1.5 hrs)*

- **Lebichot, Paldino, Siblini, He-Guelton, Oblé & Bontempi (2021).** "Incremental learning strategies for credit card fraud detection." *International Journal of Data Science and Analytics* 12. *(~1.5 hrs)*
  50M+ real transactions, batch vs incremental under drift.

- **Lebichot, Siblini, Paldino, Le Borgne, Oblé & Bontempi (2024).** "Assessment of catastrophic forgetting in continual credit card fraud detection." *Expert Systems with Applications* 249. *(~1 hr)*
  Stability/plasticity tradeoff for fraud models.

---

## Tooling — to run alongside the reading

- **River** — [riverml.xyz](https://riverml.xyz). Cleanest Python API for streaming detectors (ADWIN, DDM, EDDM, HDDM, KSWIN, Page–Hinkley) *and* drift-aware tree ensembles (HAT, ARF, SRP). Spend an evening implementing each Phase 2 detector here; the mechanism stops being abstract immediately. Pair Phase 5A reading with the corresponding River classes.
- **Alibi Detect** (Seldon) — MMD, KS, LSDD, classifier-based, ChiSquared. Production-oriented, with clear "when to use which" docs. Implements much of Phase 3 and 4.
- **NannyML** — CBPE, DLE, multivariate drift (PCA reconstruction error, domain classifier), univariate drift. Strongest tool for Phase 6; read the deep-dive docs as primary literature.
- **Evidently AI** — ad-hoc reports; weaker for streaming but good as a metric reference.
- **SHAP** — `shap.TreeExplainer` for TreeSHAP. The substrate for any Phase 5B feature-importance monitoring you'd actually deploy.
- **Bifet, Gama, Holmes & Pfahringer (2018).** *Machine Learning for Data Streams with Practical Examples in MOA.* MIT Press. Chapters 3–5 cover Phase 2 material textbook-style; chapter 7 covers tree ensembles. Read concurrently with Phases 2 and 5A if you want consolidated depth.

---

## Sequencing notes

- Within Phase 6, read Žliobaitė → Grzenda → Plasse before the performance-estimation work — the theoretical limits paper saves you from over-trusting the methods that follow.
- **Gretton MMD** (Phase 3) is the one most worth slowing down on. It pays compounding returns: MMD shows up inside Alibi Detect, *Failing Loudly*, much of the embedding-drift literature, and many adversarial-drift papers.
- Phase 5B is the section that pulls double duty for you given the upcoming XAI / SHAP work. Read it carefully: the same TreeSHAP infrastructure you build for explainability becomes a monitoring substrate at near-zero marginal cost.
- Phase 5C is the one most likely to match how your production monitoring is actually shaped today; Breck et al. is the reference to read first if you want to formalize what you're already doing.
- If you only had two weekends, the irreducible core would be: Moreno-Torres + Gama survey + Bifet–Gavaldà ADWIN + Gomes ARF + Rabanser *Failing Loudly* + Demšar & Bosnić ExStream + Breck *Data Validation for ML* + Garg ATC + Dal Pozzolo 2018. Nine papers, ~19 hours, defensible mental model.

---

*Last revised: 2026-05-21.*