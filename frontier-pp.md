# From Practitioner to Expert: A Curriculum for AI/ML in Payments Fraud Prevention

*Companion to "From Strong Baseline to the Frontier." That curriculum built rigorous mathematical and frontier-ML depth (transformers, LLMs, ML theory, systems). This one builds the intersecting expertise that makes an ML engineer an authority on **fraud prevention specifically**: the adversarial-ML discipline, rare-event statistics done rigorously, graph and sequence methods for financial crime, production fraud systems, and the regulatory machinery that constrains all of it. Where the two overlap, this document points back rather than repeating.*

---

## TL;DR
- Fraud ML is a distinct discipline, not "classification applied to money." Its four defining features — an **adaptive adversary**, **extreme class imbalance**, **delayed and noisy labels** (verification latency), and **hard regulatory constraints** — each break assumptions that ordinary supervised learning takes for granted. This curriculum is organized around mastering exactly those four breakages plus the systems and domain knowledge around them.
- Balance is deliberately **50/50 modeling ↔ domain+systems+regulatory**, and **50/50 applied ↔ proof-based**: rigorous where rigor pays (rare-event estimation, calibration under imbalance, cost-sensitive decision theory, proper scoring rules), applied where the frontier is empirical (feature engineering, graph camouflage, production monitoring).
- The single best free anchor is the **Le Borgne–Bontempi handbook** (Université Libre de Bruxelles / Worldline, 2022) — a full reproducible Jupyter-book fraud-detection course. Almost every other core reference is a freely available paper or a public regulatory document, so cost is again not the binding constraint; disciplined reproduction on realistic (imbalanced, drifting, delayed-label) data is.
- **Full program: ~6–9 months FTE. MVP spine: ~5–6 weeks** (handbook → imbalance/calibration/cost → drift & delayed labels → one of {graphs, sequences} → the regulatory core).

## How this connects to your world
You already live in production fraud ML at PayPal with gradient-boosted trees and TreeSHAP. That means Phases on production systems and explainability will partly formalize what you do daily — the value there is in the *theory underneath the practice* (why undersampling distorts probabilities, what SR 11-7 validation actually demands, where the EU AI Act does and doesn't bite). The genuinely new depth for most tree-based practitioners is in **adversarial ML as a formal discipline**, **graph methods for rings/collusion**, **rigorous rare-event statistics**, and the **AML/sanctions** modeling tradition, which has its own regulatory physics.

---

## Calibration note (read this first)
As before, claims are tagged **[SETTLED]**, **[CONTESTED]**, or **[HYPE/OVERSTATED]**. The meta-fact specific to *this* field: **fraud ML is where academic benchmarks and production reality diverge most.** Public datasets are tiny, stale, and stripped of the operational structure (delayed labels, investigator feedback loops, adversarial adaptation, cost asymmetry) that dominates real systems. A method that wins on the Kaggle credit-card dataset or on Yelp/Amazon review graphs may be irrelevant or actively misleading in production. Treat leaderboard SOTA with more suspicion here than in any area of the first curriculum, and weight practitioner literature (Dal Pozzolo et al.'s "lessons learned," the ULB/Worldline line of work) accordingly.

---

## Curriculum-wide dependency map

```
                    ┌─────────────────────────────────────────────┐
                    │  Prereqs from Curriculum 1 (as needed):     │
                    │  probability/concentration, stat. learning, │
                    │  optimization, deep learning, GNN basics    │
                    └──────────────────────┬──────────────────────┘
                                           │
  H. Fraud & Financial-Crime Domain ──────>│
                                           v
  I. Rare-Event Statistics & Evaluation ──> J. Adversarial ML ──> (core modeling)
        │                                        │
        ├──> K. Graph & Network Methods <────────┤
        ├──> L. Sequence / Temporal & Anomaly ───┤
        │                                        v
        └──> M. Production Fraud Systems ──> N. Explainability, Fairness & MRM
                                                 │
                              (H+I+…+N) ──> O. AML, Sanctions & Broader Financial Crime
                                                 │
                                                 v
                                          P. Capstone: Staying Expert
```

- **H** (domain) and **I** (rare-event stats/eval) are the twin spine — do them first and largely in parallel.
- **J** (adversarial ML) reframes everything downstream; it gates the *mindset* for K, L, M.
- **K/L** are the two big modeling pillars (structure vs. time); **M** is production; **N** is the regulatory/ethical layer that in this domain is not optional.
- **O** (AML/sanctions) is a semi-independent capstone discipline that reuses H–N but adds its own typologies and heavier compliance machinery.
- **MVP spine:** H-minimal → I → drift/delayed-labels (in M) → one of {K, L} → N-core.

---

# Phase H — The Fraud & Financial-Crime Domain

**Goals:** Build a precise mental taxonomy of fraud and financial crime on a two-sided payments platform; understand the payments rails, the chargeback/dispute lifecycle, and the operational shape of a fraud-detection system (FDS) with its layers of control and investigator feedback loop. Without this, modeling choices are unmoored from what actually matters (cost asymmetries, latency budgets, which errors are catastrophic).

**Prerequisites:** None beyond general ML literacy.

**Time:** Full 2–3 weeks; MVP 4–5 days (handbook Ch. 1–2 + a payments primer).

### H1. The fraud-detection problem, formalized
- **Primary (free, the anchor for the whole curriculum):** Yann-Aël Le Borgne, Wissam Siblini, Bertrand Lebichot & Gianluca Bontempi, *Reproducible Machine Learning for Credit Card Fraud Detection — Practical Handbook*, Université Libre de Bruxelles, 2022. Full Jupyter book: https://fraud-detection-handbook.github.io/fraud-detection-handbook. **[FREE]** Chapter 1 (problem definition, why fraud ML is hard) and Chapter 2 (the simulator; understand its transaction/label-generation model before trusting any experiment).
- **Primary (free, practitioner ground truth):** Andrea Dal Pozzolo, Olivier Caelen, Yann-Aël Le Borgne, Serge Waterschoot & Gianluca Bontempi, "Learned lessons in credit card fraud detection from a practitioner perspective," *Expert Systems with Applications* 41(10):4915–4928, 2014. The paper that names the operational realities (imbalance, drift, feedback, precision-of-alerts as the metric that matters). **[PAID; author preprints circulate]**
- **Reference (the realistic-modeling paper — you'll return to it in I and M):** Andrea Dal Pozzolo, Giacomo Boracchi, Olivier Caelen, Cesare Alippi & Gianluca Bontempi, "Credit Card Fraud Detection: A Realistic Modeling and a Novel Learning Strategy," *IEEE Transactions on Neural Networks and Learning Systems* 29(8):3784–3797, 2018. Free PDF via Politecnico di Milano (re.public.polimi.it/…/08038008.pdf). **[FREE]** Introduces the FDS "layers of control" and the alert–feedback interaction; **[SETTLED]** as the canonical formalization.

### H2. Fraud typologies on a two-sided platform
Build (as a written artifact for yourself) a taxonomy covering: card/transaction fraud, **account takeover (ATO)**, **new-account / synthetic-identity fraud**, **friendly fraud / first-party fraud / chargeback abuse**, **collusion & seller fraud** (critical on a marketplace like PayPal), promotion/refund abuse, **scams / authorized push payment (APP) fraud** (the victim authorizes — a category that defeats most "was this the real user?" signals), and money-laundering typologies (deferred to Phase O). There is no single canonical academic text; assemble from:
- Industry taxonomy references (e.g., the **Merchant Risk Council** and **European Payments Council** fraud taxonomies) — **[VERSION NOTE: taxonomies and especially APP-fraud liability rules change yearly; check current-year sources.]**
- **Free survey:** Clifton Phua, Vincent Lee, Kate Smith & Ross Gayler, "A Comprehensive Survey of Data Mining-based Fraud Detection Research," arXiv:1009.6119 (2010). Dated on methods but still the best structured overview of fraud *types* and detection framings. **[FREE]**

### H3. Payments ecosystem & the chargeback/dispute lifecycle
Understand the rails and the money/liability flow — modeling decisions (what's reversible, who bears loss, what the latency budget is) follow directly from this plumbing.
- **Primary (reference text):** Glenbrook Partners, *Payments Systems in the U.S.: A Guide for the Payments Professional*, 3rd ed., 2016 (or current). **[PAID]** The standard practitioner primer on card networks, ACH, issuers/acquirers, interchange, and dispute flows. For EU rails, supplement with European Central Bank / European Payments Council materials on SEPA and card schemes. **[VERSION NOTE: check for the latest edition and for post-PSD2/PSD3 changes.]**
- Learn the **chargeback lifecycle** and reason-code taxonomy concretely (authorization → clearing → settlement → dispute → representment → arbitration) from the card-scheme dispute-resolution documentation (Visa/Mastercard rules summaries). **[VERSION NOTE: scheme rules and reason codes are revised frequently.]**

**Physics scaffold:** Think of the FDS as a **multi-stage filter / control system** with different time constants at each layer (real-time scoring in milliseconds; investigator feedback in hours; customer-reported chargebacks in days–weeks). The mismatch of time constants is the source of the delayed-label problem you'll formalize in Phase M — analogous to a system probed at multiple, widely separated timescales where the slow modes dominate long-run behavior.

**Phase H exercises:**
1. Write a 3–5 page taxonomy of fraud types relevant to a two-sided payments platform, and for each note: typical signals, cost asymmetry, label latency, and whether "is this the genuine account holder?" even helps (it doesn't, for APP scams and first-party fraud — a distinction most models ignore).
2. Diagram the chargeback lifecycle with timelines; mark where a label becomes available and how noisy it is at each stage.

**MVP for Phase H:** Handbook Ch. 1–2 + the 2018 "Realistic Modeling" paper's problem formalization + your own typology artifact.

---

# Phase I — Rare-Event Statistics & Evaluation (proof-based core)

**Goals:** Master, rigorously, the statistics that fraud's extreme class imbalance forces: proper scoring rules, calibration (and how resampling destroys it), cost-sensitive decision theory, and the correct threshold-free and threshold-based metrics. This is the most proof-heavy phase and the one that most sharply separates experts from practitioners who reach for SMOTE reflexively.

**Prerequisites:** Curriculum 1 Phases A3–A4 (probability, concentration) and B (statistical learning) help but aren't strictly required.

**Time:** Full 3–4 weeks; MVP 1.5 weeks (calibration + cost + PR-curve papers).

### I1. Metrics under extreme imbalance
- **Primary (free):** Jesse Davis & Mark Goadrich, "The Relationship Between Precision-Recall and ROC Curves," *Proc. 23rd ICML*, pp. 233–240, 2006. Free PDF (ftp.cs.wisc.edu/machine-learning/shavlik-group/davis.icml06.pdf). **[FREE]** Proves a curve dominates in ROC space iff it dominates in PR space, and that **linear interpolation in PR space is incorrect** — a subtlety many practitioners get wrong. **[SETTLED]**
- **Primary:** Takaya Saito & Marc Rehmsmeier, "The Precision-Recall Plot Is More Informative than the ROC Plot When Evaluating Binary Classifiers on Imbalanced Datasets," *PLoS ONE* 10(3):e0118432, 2015. **[FREE]** The empirical case that **ROC-AUC is misleadingly optimistic under heavy imbalance**; PR-AUC (average precision) is the better summary. **[SETTLED for imbalanced regimes]**
- **Domain-specific metric [CONTESTED but important]:** Dal Pozzolo et al. (2018, Phase H) argue that in a real FDS the operationally meaningful metric is **precision within the small set of alerts investigators can actually check** (e.g., Precision@k / card-level precision in a daily budget), not global AUC. Internalize this: your metric should mirror the review-queue economics, not a benchmark convention.
- **Reference (point estimates & CIs for PR-AUC):** Kendrick Boyd, Kevin H. Eng & C. David Page, "Area Under the Precision-Recall Curve: Point Estimates and Confidence Intervals," *ECML PKDD* 2013, LNCS 8190, pp. 451–466, Springer. **[PAID]**

### I2. Proper scoring rules & why "just optimize AUC" is incomplete
- **Primary (free):** Tilmann Gneiting & Adrian E. Raftery, "Strictly Proper Scoring Rules, Prediction, and Estimation," *Journal of the American Statistical Association* 102(477):359–378, 2007. Free preprint via U. Washington stat (stat.washington.edu). **[FREE]** The rigorous foundation: log loss and Brier score are strictly proper; ranking metrics (AUC) are not proper scoring rules and don't by themselves yield well-calibrated probabilities. Ground your decisioning in proper scores, then threshold. **[SETTLED]**

### I3. Calibration — and how imbalance/resampling breaks it
This is the crux where fraud practice most often goes wrong.
- **Primary (free), the fraud-specific result:** Andrea Dal Pozzolo, Olivier Caelen, Reid A. Johnson & Gianluca Bontempi, "Calibrating Probability with Undersampling for Unbalanced Classification," *IEEE SSCI/CIDM* 2015, pp. 159–166. **[PAID; ULB preprint free]** Proves and quantifies how **undersampling shifts posterior probabilities** and gives the correction formula to recover calibrated probabilities. **[SETTLED]** — this single result should change how you resample.
- **Primary (classical calibration methods):** John Platt, "Probabilistic Outputs for Support Vector Machines and Comparisons to Regularized Likelihood Methods," in *Advances in Large Margin Classifiers*, MIT Press, 1999 (Platt scaling); and Bianca Zadrozny & Charles Elkan, "Transforming Classifier Scores into Accurate Multiclass Probability Estimates," *KDD* 2002 (isotonic regression). **[FREE via author pages]**
- **Modern [CONTESTED]:** Chuan Guo, Geoff Pleiss, Yu Sun & Kilian Q. Weinberger, "On Calibration of Modern Neural Networks," *ICML* 2017, arXiv:1706.04599. Shows modern nets are miscalibrated and introduces temperature scaling. **[SETTLED that nets miscalibrate; CONTESTED which fix is best]** Relevant if you move beyond trees; less so for well-calibrated GBMs.

### I4. Cost-sensitive learning & the decision-theoretic frame
Fraud is economically asymmetric; the right object is expected cost, not accuracy.
- **Primary (free):** Charles Elkan, "The Foundations of Cost-Sensitive Learning," *Proc. 17th IJCAI*, vol. 2, pp. 973–978, 2001. Free PDF (cseweb.ucsd.edu/~elkan/rescale.pdf). **[FREE]** The theorem you should know cold: **rebalancing the training distribution is equivalent (for probabilistic classifiers) to changing the decision threshold via the cost ratio** — so the principled recipe is *learn calibrated probabilities, then make optimal Bayes-cost decisions explicitly*, rather than resampling and hoping. **[SETTLED]**
- **Primary (costs & probabilities both unknown):** Bianca Zadrozny & Charles Elkan, "Learning and Making Decisions When Costs and Probabilities Are Both Unknown," *KDD* 2001, pp. 204–213. **[PAID; preprint free]**
- **Fraud-specific example-dependent costs:** Alejandro Correa Bahnsen, Djamila Aouada & Björn Ottersten, "Example-Dependent Cost-Sensitive Decision Trees," *Expert Systems with Applications* 42(19):6609–6619, 2015; and their "Feature Engineering Strategies for Credit Card Fraud Detection," *ESWA* 51:134–142, 2016. **[PAID; preprints on Bahnsen's site]** Each transaction has its *own* cost (the amount), which standard cost-sensitive methods (uniform cost matrix) don't capture. **[SETTLED as a framing; method choice CONTESTED.]**

### I5. The resampling debate (SETTLED vs HYPE)
- **The canonical method:** Nitesh V. Chawla, Kevin W. Bowyer, Lawrence O. Hall & W. Philip Kegelmeyer, "SMOTE: Synthetic Minority Over-sampling Technique," *JAIR* 16:321–357, 2002. **[FREE]** Foundational and worth reading — but read it *against* its critics.
- **[HYPE/OVERSTATED — important corrective]:** A growing body of work shows SMOTE and aggressive resampling often **do not help, and can hurt calibration and real-world precision**, especially with strong learners (GBMs) and proper evaluation. See the undersampling-calibration result (I3), Elkan's theorem (I4), and the practitioner consensus in the ULB line of work. The expert position: **prefer calibrated probabilities + cost-based thresholds + class weights over synthetic oversampling; if you resample, correct the probabilities and validate on realistic time-split data.** State this explicitly — it's a place where common practice lags the settled theory.
- **When undersampling *is* justified [SETTLED]:** Andrea Dal Pozzolo, Olivier Caelen & Gianluca Bontempi, "When Is Undersampling Effective in Unbalanced Classification Tasks?" *ECML PKDD* 2015, LNCS 9284, Springer. **[PAID; ULB preprint free]**

**Physics scaffold:** Rare-event detection is formally the **large-deviations / tail regime**. The base rate is a small parameter ε; many quantities you care about (precision at fixed recall, variance of AUC estimates) have leading-order behavior in ε that differs qualitatively from the balanced case — treat it as a singular perturbation, not a smooth one. Concentration inequalities (Curriculum 1, A4) govern how many fraud examples you need before an estimate stabilizes; with ε ~ 10⁻³ the effective sample size is the *fraud count*, not the row count.

**Phase I exercises (do these on the handbook simulator or a realistic time-split of a public set):**
1. Prove Elkan's rebalancing↔threshold equivalence for a two-class probabilistic classifier; then verify empirically that resampling + threshold-at-0.5 ≈ no-resampling + cost-adjusted threshold, up to calibration.
2. Reproduce the undersampling probability-shift and apply the correction; show the reliability diagram before/after.
3. Build an expected-cost decision rule using example-dependent (amount-weighted) costs; compare its dollar loss to an F1-optimal threshold. Connect to your PayPal review-queue economics.

**MVP for Phase I:** Elkan 2001 + the undersampling-calibration paper + Davis–Goadrich + Saito–Rehmsmeier; internalize "calibrate then decide," and the SMOTE corrective.

---

# Phase J — Adversarial Machine Learning (the defining discipline)

**Goals:** Treat fraud as the security problem it is: a non-stationary game against an adaptive adversary who observes your defenses and adapts. Master the threat-model vocabulary (evasion vs. poisoning, white/black-box, attacker knowledge/goal), understand where adversarial-ML theory transfers to tabular fraud (and where the famous image-perturbation results *don't*), and adopt the "security evaluation" mindset for your own models.

**Prerequisites:** Phase I; Curriculum 1 Phase C (deep learning) helps for the neural-attack literature.

**Time:** Full 2–3 weeks; MVP 1 week (Biggio–Roli + the security-eval framing + one poisoning paper).

### J1. The field and its threat models
- **Primary (free), the survey to internalize:** Battista Biggio & Fabio Roli, "Wild Patterns: Ten Years After the Rise of Adversarial Machine Learning," *Pattern Recognition* 84:317–331, 2018. arXiv:1712.03141. **[FREE]** The historical arc and — most useful for you — the **threat-model taxonomy** (attacker's goal, knowledge, capability; evasion vs. poisoning; error-generic vs. error-specific). Note the origin story: adversarial ML began with **spam filtering and malware**, i.e., exactly the security/fraud lineage, *before* the image-perturbation era. **[SETTLED as framing.]**
- **Primary (evasion, the foundational attack):** Battista Biggio, Igino Corona, Davide Maiorca, Blaine Nelson, Nedim Šrndić, Pavel Laskov, Giorgio Giacinto & Fabio Roli, "Evasion Attacks Against Machine Learning at Test Time," *ECML PKDD* 2013, LNCS 8190, Springer. arXiv:1708.06131. **[FREE]**
- **Primary (poisoning):** Battista Biggio, Blaine Nelson & Pavel Laskov, "Poisoning Attacks Against Support Vector Machines," *ICML* 2012, arXiv:1206.6389. **[FREE]** Fraud systems that learn online from investigator feedback are *poisonable* — adversaries can try to shape your training data. **[SETTLED that the threat is real; magnitude in production CONTESTED.]**
- **The image-era classics (know them, but calibrate transfer):** Ian J. Goodfellow, Jonathon Shlens & Christian Szegedy, "Explaining and Harnessing Adversarial Examples," *ICLR* 2015, arXiv:1412.6572; and Aleksander Mądry, Aleksandar Makelov, Ludwig Schmidt, Dimitris Tsipras & Adrian Vladu, "Towards Deep Learning Models Resistant to Adversarial Attacks" (PGD/adversarial training), *ICLR* 2018, arXiv:1706.06083. **[FREE]**

### J2. Calibration on transfer to tabular fraud (SETTLED vs OVERSTATED)
- **[OVERSTATED for fraud]:** The ℓ_p-bounded imperceptible-perturbation formulation (pixels) does **not** map cleanly to fraud. Fraud "perturbations" are **discrete, semantically constrained, and cost-bearing** (an attacker can't set an arbitrary feature vector; they must transact in ways that pass business logic and cost them money/time). Importing image-adversarial defenses wholesale is a known failure mode.
- **[SETTLED and transferable]:** The *mindset* transfers completely — assume feature values are attacker-controllable, expect **feature and relation camouflage** (Phase K), evaluate under adaptive attack rather than a fixed test set, and prefer signals that are **costly for the adversary to fake** (device/hardware, funding-instrument history, network position) over cheap, spoofable ones.
- **Security-evaluation practice:** Battista Biggio, Giorgio Fumera & Fabio Roli, "Security Evaluation of Pattern Classifiers Under Attack," *IEEE TKDE* 26(4):984–996, 2014. **[PAID; preprint free]** How to build attacker models into your evaluation. Complement with the methodological warnings in Daniel Arp et al., "Dos and Don'ts of Machine Learning in Computer Security," *USENIX Security* 2022, arXiv:2010.09470 **[FREE]** — a checklist of evaluation pitfalls (temporal snooping, spatial bias, base-rate fallacy) that recur constantly in fraud papers.

**Physics scaffold:** This is a **non-stationary, adversarial game**, not a fixed distribution. The right frame is closer to game theory / evolutionary dynamics than to i.i.d. statistics: you and the adversary co-evolve, so any static equilibrium (a "solved" model) is temporary. Expect **arms-race dynamics** and design for continuous re-training and monitoring (Phase M) as a first-class requirement, not an afterthought.

**Phase J exercises:**
1. Write the threat model for one PayPal-relevant attack (e.g., ATO via credential stuffing, or seller-collusion refund abuse): attacker goal, knowledge, capability, and which of your features are cheap vs. costly to manipulate.
2. Red-team a tree-based model: given feature importances (you have TreeSHAP), construct a plausible *business-legal* evasion (not an ℓ_p perturbation) and estimate its cost to the attacker. This reframes SHAP as an attack-surface map, not just an explanation tool.

**MVP for Phase J:** Biggio–Roli survey + the security-evaluation framing + the "Dos and Don'ts" pitfalls list.

---

# Phase K — Graph & Network Methods (structure: rings, collusion, shared identity)

**Goals:** Model fraud as relational, not row-independent. Master entity resolution, graph construction from transactions/devices/identities, and GNNs adapted to the two hard properties of fraud graphs — **class imbalance** and **heterophily/camouflage**. This is the highest-value genuinely-new modeling pillar for a tree-based practitioner and connects directly to your existing GNN learning path.

**Prerequisites:** Curriculum 1 GNN foundations (graph theory, message passing, GCN/GraphSAGE/GAT); Phases I and J of this curriculum.

**Time:** Full 3–4 weeks; MVP 1.5 weeks (GCN + CARE-GNN + PC-GNN + one survey).

### K1. Entity resolution / record linkage (the unglamorous prerequisite)
Graphs are only as good as the entities you resolve; linking accounts, devices, cards, and identities is where much fraud signal lives.
- **Primary (foundational theory):** Ivan P. Fellegi & Alan B. Sunter, "A Theory for Record Linkage," *JASA* 64(328):1183–1210, 1969. **[PAID]** The probabilistic-matching foundation. **[SETTLED]**
- **Primary (modern reference):** Peter Christen, *Data Matching: Concepts and Techniques for Record Linkage, Entity Resolution, and Duplicate Detection*, Springer, 2012. **[PAID]** The standard modern text.

### K2. GNN backbone (bridge from Curriculum 1)
- Recap the message-passing canon you already have: Kipf & Welling (GCN, arXiv:1609.02907), Hamilton et al. (GraphSAGE, arXiv:1706.02216), Veličković et al. (GAT, arXiv:1710.10903), Xu et al. (GIN / expressiveness, arXiv:1810.00826). **[FREE]** For dynamic transaction graphs, add Pareja et al., "EvolveGCN: Evolving Graph Convolutional Networks for Dynamic Graphs," *AAAI* 2020, arXiv:1902.10191. **[FREE]**

### K3. GNNs adapted for fraud — imbalance, heterophily, camouflage
The core insight: **standard GNNs assume homophily** (connected nodes are similar), but fraudsters deliberately connect to benign nodes to hide — *relation camouflage* — and mimic benign features — *feature camouflage*. Plain message passing then **dilutes** the fraud signal. The fraud-GNN literature is essentially a sequence of fixes for this.
- **Primary (camouflage-resistant):** Yingtong Dou, Zhiwei Liu, Li Sun, Yutong Deng, Hao Peng & Philip S. Yu, "Enhancing Graph Neural Network-based Fraud Detectors against Camouflaged Fraudsters" (**CARE-GNN**), *CIKM* 2020, arXiv:2008.08692. Code: github.com/YingtongDou/CARE-GNN. **[FREE]** Label-aware neighbor selection + RL-chosen neighbor budgets. **[SETTLED as a landmark; superseded on benchmarks.]**
- **Primary (imbalance-aware):** Yang Liu, Xiang Ao, Zidi Qin, Jianfeng Chi, Jinghua Feng, Hao Yang & Qing He, "Pick and Choose: A GNN-based Imbalanced Learning Approach for Fraud Detection" (**PC-GNN**), *TheWebConf (WWW)* 2021. **[FREE]** Label-balanced sampler + neighbor selection (Pick–Choose–Aggregate). **[SETTLED as a landmark.]**
- **Primary (spectral view of anomaly):** Jianheng Tang, Jiajin Li, Ziqi Gao & Jia Li, "Rethinking Graph Neural Networks for Anomaly Detection" (**BWGNN**, Beta Wavelet GNN), *ICML* 2022, arXiv:2205.15508. **[FREE]** Shows anomalies induce a **'right-shift' to higher graph frequencies** that low-pass GNNs smooth away, motivating band-pass filters. A rare place where fraud-GNN work has clean theory. **[SETTLED for the spectral observation.]**
- **Supplementary (heterophily/consistency):** Zhiwei Liu et al., "Alleviating the Inconsistency Problem of Applying Graph Neural Network to Fraud Detection" (**GraphConsis**), *SIGIR* 2020, arXiv:2005.00625; and the credit-card semi-supervised attribute-graph line, e.g., Xiang et al., "Semi-supervised Credit Card Fraud Detection via Attribute-driven Graph Representation" (**GTAN**), *AAAI* 2023. **[FREE]**
- **Survey (free, current):** a good entry survey is Xiaoxiao Ma et al., "A Comprehensive Survey on Graph Anomaly Detection with Deep Learning," *IEEE TKDE*, 2021, arXiv:2106.07178. **[FREE]** For the fraud-specific slice, use the recent GNN-fraud surveys (2024–2026) but read their headline numbers critically — see the caveat below.

### K4. Calibration on graph methods (SETTLED vs CONTESTED)
- **[CONTESTED / likely OVERSTATED]:** Survey claims that GNNs beat XGBoost by "12–25% AUROC" on fraud are dataset- and setup-dependent and frequently rest on the same tiny public graphs (Yelp/Amazon reviews, small transaction sets) with optimistic splits. On **tabular** fraud features, strong GBMs remain extremely hard to beat (cf. Grinsztajn et al. 2022 from Curriculum 1). The honest expert take: **graphs add the most value where the signal is genuinely relational** — rings, shared devices/identities, collusion — and as a *complementary* feature source (graph-derived features feeding your GBM, or a GNN ensembled with trees), not as a wholesale replacement. **[SETTLED that relational signal helps; CONTESTED that end-to-end GNNs dominate in production.]**
- **[SETTLED]:** Scalability and latency are real constraints — billion-edge graphs and <100ms scoring push toward precomputed graph features, neighbor sampling, or offline ring-detection rather than full online GNN inference.

**Physics scaffold:** Message passing is diffusion on a graph; the BWGNN result is literally a **spectral/Fourier** statement (anomalies live in high graph-frequency modes; low-pass aggregation is a smoothing operator that damps them). Your signal-processing/MIR background (spectral filters, band-pass design) transfers directly — a fraud-detection GNN is a filter-design problem on the graph Laplacian's spectrum.

**Phase K exercises:**
1. On the **Elliptic** dataset (Phase O) or a public fraud graph, reproduce GCN vs. CARE-GNN vs. PC-GNN vs. a GBM-on-graph-features baseline; report PR-AUC and card/entity-level precision, with a proper temporal split. Confirm or refute the "GNNs beat GBM" claim honestly.
2. Engineer graph-derived features (degree, triangle counts, connected-component size, PageRank on device/identity graphs) and feed them to your GBM; measure lift over transaction-only features. This is the highest-ROI, production-realistic version of "using graphs."

**MVP for Phase K:** GCN recap + CARE-GNN + PC-GNN + BWGNN's spectral insight + the "graph features → GBM" experiment.

---

# Phase L — Sequence, Temporal & Anomaly Methods (time & the unlabeled)

**Goals:** Model the *temporal* structure fraud lives in (velocity, sessionization, behavioral sequences) and handle the reality that novel attacks arrive **without labels**, requiring unsupervised/semi-supervised anomaly detection to catch what supervised models have never seen.

**Prerequisites:** Curriculum 1 Phases C–D (sequence models, transformers); Phases H–I here.

**Time:** Full 2–3 weeks; MVP 1 week (feature-aggregation section of the handbook + one anomaly survey + one deep-sequence fraud paper).

### L1. Feature engineering for transaction sequences (still the workhorse)
- **Primary (free):** Le Borgne–Bontempi handbook, the **feature-transformation / aggregation** chapter — RFM-style aggregates, time-windowed velocity features, and the periodic/temporal encodings that make tabular models work on streams. **[FREE]** For most production fraud systems, **well-designed aggregation features on a GBM remain the strongest baseline** — establish this before reaching for deep sequence models. **[SETTLED.]**
- **Primary (the "transaction as sequence" framing):** Johannes Jurgovsky, Michael Granitzer, Konstantin Ziegler, Sylvie Calabretto, Pierre-Edouard Portier, Liyun He-Guelton & Olivier Caelen, "Sequence Classification for Credit-Card Fraud Detection," *Expert Systems with Applications* 100:234–245, 2018. **[PAID; preprint free]** LSTM vs. feature-aggregation comparison on real card data — a clean, honest baseline study. **[SETTLED as a reference comparison.]**

### L2. Deep sequence & spatio-temporal models
- **Primary (attention/transformer over transactions):** the spatio-temporal-aware graph/transformer line, e.g., "Transaction Fraud Detection via Spatial-Temporal-Aware Graph Transformer," arXiv:2307.05121 (2023); and attentional spatio-temporal GNNs for transactions (2024–2025). **[FREE]** **[CONTESTED]:** gains over strong aggregation+GBM baselines are often modest and dataset-dependent; adopt where you have rich, long behavioral sequences and the latency budget for it.
- **Connection back to Curriculum 1:** everything you learned about attention, positional encodings, and long-context applies here; the open question is whether sequence structure in *your* data carries signal beyond aggregation features. Test, don't assume.

### L3. Anomaly / novelty detection (for the unlabeled frontier)
Supervised models catch known fraud; anomaly detection is your net for **novel** attacks and cold-start.
- **Primary (foundational survey, free):** Varun Chandola, Arindam Banerjee & Vipin Kumar, "Anomaly Detection: A Survey," *ACM Computing Surveys* 41(3):1–58, 2009. **[FREE via UMN]** The canonical taxonomy (point/contextual/collective anomalies). **[SETTLED.]**
- **Primary (the practical workhorse):** Fei Tony Liu, Kai Ming Ting & Zhi-Hua Zhou, "Isolation Forest," *ICDM* 2008, pp. 413–422. **[PAID; widely available]** Fast, effective, tree-based (fits your stack). **[SETTLED.]**
- **Primary (deep, and its honest limits):** Lukas Ruff, Jacob R. Kauffmann, Robert A. Vandermeulen, Grégoire Montavon, Wojciech Samek, Marius Kloft, Thomas G. Dietterich & Klaus-Robert Müller, "A Unifying Review of Deep and Shallow Anomaly Detection," *Proceedings of the IEEE* 109(5):756–795, 2021, arXiv:2009.11732. **[FREE]** Places deep methods against classical ones and is refreshingly clear that **deep anomaly detection does not uniformly beat shallow methods** — especially on tabular data. Complement with Guansong Pang, Chunhua Shen, Longbing Cao & Anton van den Hengel, "Deep Learning for Anomaly Detection: A Review," *ACM Computing Surveys* 54(2):1–38, 2021, arXiv:2007.02500. **[FREE]**
- **Combining supervised + unsupervised (fraud-specific):** Fabrizio Carcillo, Yann-Aël Le Borgne, Olivier Caelen, Yacine Kessaci, Frédéric Oblé & Gianluca Bontempi, "Combining Unsupervised and Supervised Learning in Credit Card Fraud Detection," *Information Sciences* 557:317–331, 2021. **[PAID; ULB preprint free]** How anomaly scores become features for supervised models. **[SETTLED as a practical pattern.]**

**Physics scaffold:** Anomaly detection is density estimation in the tail — you're modeling the support of "normal" and flagging low-density regions, a problem that gets exponentially harder in high dimensions (curse of dimensionality). Contextual anomalies (normal globally, abnormal for *this* user at *this* time) are the analog of fluctuations that are only anomalous relative to a local baseline — the same conditioning logic as in your rare-event statistics (Phase I).

**Phase L exercises:**
1. Reproduce the Jurgovsky LSTM-vs-aggregation comparison in spirit: build strong velocity/aggregation features + GBM, then a sequence model, on a time-split; report whether the sequence model earns its complexity.
2. Add an isolation-forest (or autoencoder) anomaly score as a feature to your supervised model; measure lift on *recently emerged* fraud patterns specifically (hold out a late time period). This directly tests novel-attack coverage.

**MVP for Phase L:** Handbook aggregation chapter + Chandola survey + Isolation Forest + the "anomaly-score-as-feature" experiment.

---

# Phase M — Production Fraud Systems (real-time, drifting, delayed-label)

**Goals:** Master the systems and lifecycle problems that dominate real fraud ML: low-latency real-time scoring, feature stores and streaming, and — the two most under-appreciated and most fraud-defining — **concept drift** and **delayed/noisy labels (verification latency)** with investigator feedback loops. This phase formalizes much of your day job.

**Prerequisites:** Phases H–I; general MLOps familiarity.

**Time:** Full 3–4 weeks; MVP 1.5 weeks (drift + delayed-label papers + one MLOps reference).

### M1. Concept drift (the adversary and the world both move)
- **Primary (free, the canonical survey):** João Gama, Indrė Žliobaitė, Albert Bifet, Mykola Pechenizkiy & Abdelhamid Bouchachia, "A Survey on Concept Drift Adaptation," *ACM Computing Surveys* 46(4):1–37, 2014. **[FREE]** The reference taxonomy (sudden/gradual/incremental/recurring drift; detection, forgetting, ensembles). **[SETTLED.]**
- **Primary (streaming foundations):** Albert Bifet, Ricard Gavaldà, Geoff Holmes & Bernhard Pfahringer, *Machine Learning for Data Streams, with Practical Examples in MOA*, MIT Press, 2018. **[PAID]** For adaptive windowing (ADWIN) and streaming evaluation (prequential/interleaved test-then-train). **[SETTLED.]**

### M2. Delayed & noisy labels / verification latency (THE fraud-specific systems problem)
This is where fraud ML most sharply departs from textbook supervised learning, and where most engineers underinvest.
- **Primary (free, essential):** Andrea Dal Pozzolo, Giacomo Boracchi, Olivier Caelen, Cesare Alippi & Gianluca Bontempi, "Credit Card Fraud Detection and Concept-Drift Adaptation with Delayed Supervised Information," *IJCNN* 2015, pp. 1–8. Free PDF (boracchi.faculty.polimi.it/docs/2015_04_...pdf). **[FREE]** Formalizes **verification latency**: a small set of investigator-checked labels arrives *fast* (feedbacks), while the vast majority of labels arrive *days later* via customer chargebacks (delayed) — and these are *different distributions*. The **[SETTLED]** result: train **two separate classifiers** (one on recent feedbacks, one on delayed labels) and aggregate, rather than pretending labels are i.i.d. and immediate. Internalizing this changes your training pipeline design.
- **Reference (the full treatment):** the 2018 *IEEE TNNLS* "Realistic Modeling" paper (Phase H) develops the alert–feedback interaction and the two-timescale label problem in depth. **[FREE]**
- **Related learning setting (positive-unlabeled):** because "not-yet-charged-back" ≠ "genuine," fraud labeling is closer to **PU learning** than clean binary labels. Jessa Bekker & Jesse Davis, "Learning from Positive and Unlabeled Data: A Survey," *Machine Learning* 109:719–760, 2020, arXiv:1811.04820. **[FREE]** **[SETTLED framing; underused in practice.]**

### M3. Real-time architecture, feature stores & streaming
- **Primary (the ML-systems text):** Chip Huyen, *Designing Machine Learning Systems*, O'Reilly, 2022. **[PAID]** The best current treatment of feature stores, online/offline skew, real-time serving, and monitoring — read the streaming and monitoring chapters through a fraud lens (millisecond budgets, point-in-time-correct features to avoid label leakage). **[VERSION NOTE: tooling — Feast, Tecton, Flink, Kafka, and the current feature-store landscape — moves fast; check current versions and PayPal's internal stack.]**
- **Foundations to know by name:** the **feature store** concept (Uber Michelangelo; the open-source Feast project); streaming architectures (Kafka/Flink; the Kappa architecture). Emphasis: **point-in-time correctness** — training on features that wouldn't have been available at scoring time is the most common silent leakage in fraud ML. **[SETTLED as the cardinal sin to avoid.]**
- **Fraud-specific scalable pipeline:** Fabrizio Carcillo, Andrea Dal Pozzolo, Yann-Aël Le Borgne, Olivier Caelen, Yannis Mazzer & Gianluca Bontempi, "SCARFF: A Scalable Framework for Streaming Credit Card Fraud Detection with Spark," *Information Fusion* 41:182–194, 2018. **[PAID; preprint free]**

### M4. Monitoring, feedback loops & the review queue
- Monitoring under drift + the **feedback-loop pathology**: your model determines which transactions get blocked/reviewed, which determines which labels you observe, which biases your next model. This selective-labels problem is subtle and important. See Himabindu Lakkaraju, Jon Kleinberg, Jure Leskovec, Jens Ludwig & Sendhil Mullainathan, "The Selective Labels Problem: Evaluating Algorithmic Predictions in the Presence of Unobservables," *KDD* 2017. **[FREE]** **[SETTLED that the bias exists; correcting it in production is CONTESTED.]**
- **Active learning to spend the scarce investigator budget:** Fabrizio Carcillo, Yann-Aël Le Borgne, Olivier Caelen & Gianluca Bontempi, "Streaming Active Learning Strategies for Real-Life Credit Card Fraud Detection," *International Journal of Data Science and Analytics* 5(4):285–300, 2018. **[PAID; preprint free]**

**Physics scaffold:** The two-timescale label problem is explicitly a **separation-of-timescales** system: fast feedback labels vs. slow chargeback labels, with the slow channel carrying different (and drifting) statistics. Analyze it the way you'd analyze a system with fast and slow modes — you can't average them into one "label" without losing the dominant slow dynamics. The feedback loop is a **closed control loop** with the model in the loop, so stability/observability intuitions (you only observe the part of state your policy exposes) apply.

**Phase M exercises:**
1. Simulate verification latency on the handbook data: split labels into fast "feedback" and delayed "chargeback" streams; compare a single-classifier baseline to the two-classifier aggregate. Reproduce the Dal Pozzolo result.
2. Build a prequential (test-then-train) evaluation with an ADWIN-style drift detector; show how a static model degrades and an adaptive one recovers.
3. Construct a deliberately leaky feature (uses future information) and quantify the phantom AUC it produces; then fix it with point-in-time-correct aggregation. This is the single most valuable habit to instill.

**MVP for Phase M:** Gama drift survey + the delayed-supervised-information paper + Huyen's monitoring/streaming chapters + the point-in-time-leakage exercise.

---

# Phase N — Explainability, Fairness & Model Risk Management (the regulatory layer)

**Goals:** Make models that are explainable, fair, and governable *because the law and regulators require it* — not as a nicety. Master SHAP/TreeSHAP rigorously (your wheelhouse, formalized), reason-code generation for adverse-action-style requirements, fairness/disparate-impact testing, and the model-risk-management (SR 11-7) and EU (GDPR Art. 22, EU AI Act, DORA, PSD2/SCA) regimes that govern fraud models — including the important nuances about what does and doesn't apply.

**Prerequisites:** Phases H–M; Curriculum 1 not required.

**Time:** Full 3–4 weeks; MVP 1.5 weeks (SHAP papers + SR 11-7 + the EU-AI-Act fraud-carveout nuance + one fairness reference).

### N1. Explainability, done rigorously
- **Primary (free, the unified theory):** Scott M. Lundberg & Su-In Lee, "A Unified Approach to Interpreting Model Predictions" (SHAP), *NeurIPS* 30, pp. 4765–4774, 2017, arXiv:1705.07874. **[FREE]** SHAP values as the unique additive feature-attribution satisfying the Shapley axioms (local accuracy, missingness, consistency). Know the axioms and what uniqueness does and doesn't buy you. **[SETTLED as a theory of attribution.]**
- **Primary (free, your daily tool formalized):** Scott M. Lundberg, Gabriel Erion, Hugh Chen, Alex DeGrave, Jordan M. Prutkin, Bala Nair, Ronit Katz, Jonathan Himmelfarb, Nisha Bansal & Su-In Lee, "From Local Explanations to Global Understanding with Explainable AI for Trees" (**TreeSHAP**), *Nature Machine Intelligence* 2(1):56–67, 2020. arXiv:1905.04610. **[FREE]** The exact-and-fast tree algorithm you already use — read it for the algorithm and its interaction values, and for its honest limitations. **[SETTLED for the algorithm.]**
- **[CONTESTED — essential epistemics]:** SHAP is widely misused. Read the critiques so you can defend or qualify your explanations: I. Elizabeth Kumar, Suresh Venkatasubramanian, Carlos Scheidegger & Sorelle Friedler, "Problems with Shapley-value-based Explanations as Feature Importance Measures," *ICML* 2020, arXiv:2002.11097 **[FREE]**; and the correlated-feature issue in Kjersti Aas, Martin Jullum & Anders Løland, "Explaining Individual Predictions When Features Are Dependent," *Artificial Intelligence* 298:103502, 2021, arXiv:1903.10464. **[FREE]** Key point: **feature dependence (rife in fraud data) breaks the interventional/observational distinction** and can make SHAP attributions misleading. **[SETTLED that the pitfalls are real.]**
- **Fraud-specific extension (connects your stack):** Miloš Kopanja et al., "Cost-sensitive TreeSHAP for explaining cost-sensitive tree-based models," *Computational Intelligence* 40(3):e12651, 2024. **[PAID]** Directly relevant: explaining *cost-sensitive* fraud models correctly.

### N2. Reason codes, adverse action & fair lending (US)
Even though *fraud* decisions differ from *credit* decisions, the reason-code discipline and the fair-lending machinery shape how financial institutions deploy models, and hybrid fraud/credit decisions can trigger them.
- **Primary (regulatory, free):** CFPB **Circular 2022-03**, "Adverse Action Notification Requirements in Connection with Credit Decisions Based on Complex Algorithms" (May 2022), and **Circular 2023-03**, "Adverse Action Notification Requirements and the Proper Use of the CFPB's Sample Forms" (Sept 2023). consumerfinance.gov. **[FREE]** The settled position: **ECOA/Regulation B require specific, accurate principal reasons regardless of model complexity — "the model is a black box" is not a defense**, and the sample-form checklists don't suffice if they're not specific/accurate. **[SETTLED law.]** This is why reason-code generation (often SHAP-derived) is load-bearing in regulated deployments — but note the SHAP-misuse caveats above: a reason code must be *accurate*, not merely plausible.
- **Fairness/disparate impact (technical):** the fair-ML canon — Solon Barocas, Moritz Hardt & Arvind Narayanan, *Fairness and Machine Learning: Limitations and Opportunities*, MIT Press, 2023 (free at fairmlbook.org) **[FREE]**; Moritz Hardt, Eric Price & Nathan Srebro, "Equality of Opportunity in Supervised Learning," *NeurIPS* 2016, arXiv:1610.02413 **[FREE]**; and the **impossibility results** (Kleinberg, Mullainathan & Raghavan, "Inherent Trade-Offs in the Fair Determination of Risk Scores," *ITCS* 2017, arXiv:1609.05807; Chouldechova, *Big Data* 2017, arXiv:1703.00056). **[FREE]** **[SETTLED]:** you generally cannot satisfy all fairness criteria at once — calibration and equalized error rates conflict except in degenerate cases. Fraud adds a wrinkle: **fairness in fraud is under-theorized** relative to lending, and the harms (wrongful account freezes, financial exclusion) are real but the legal framework is less settled. **[CONTESTED.]**

### N3. Model Risk Management — SR 11-7 and successors (US)
- **Primary (regulatory, free):** Board of Governors of the Federal Reserve System & OCC, **SR 11-7 / OCC Bulletin 2011-12, "Supervisory Guidance on Model Risk Management,"** April 4, 2011. federalreserve.gov/supervisionreg/srletters/sr1107.htm. **[FREE]** The tri-pillar framework you must know: **(1)** robust model development/implementation/use, **(2)** **independent validation** (effective challenge), **(3)** governance/policies/controls (model inventory, documentation). The doctrine of **"effective challenge"** and the "all models are wrong, some are useful" stance are the load-bearing ideas. **[SETTLED — the defining US MRM framework.]**
- **[VERSION NOTE / CURRENCY]:** The Fed and OCC issued **revised model-risk guidance (SR 26-2 / an updated interagency statement)** in early 2026, reflecting ~15 years of experience and AI/ML developments; SR 11-7's principles carry forward but **check the current version** (federalreserve.gov/supervisionreg/srletters/) before citing specifics. Also note the 2021 interagency statement on model risk management **for BSA/AML compliance** (relevant to Phase O).
- **Adjacent frameworks to know by name:** the **NIST AI Risk Management Framework (AI RMF 1.0, 2023)** for a voluntary, broadly-applicable structure; and **SS1/23** (Bank of England/PRA model risk management principles, effective 2024) for the UK analog. **[FREE]**

### N4. The EU layer (directly relevant to your Frankfurt/EU context) — with the key nuances
- **GDPR Article 22 [SETTLED, and it *does* apply to fraud]:** restricts solely-automated decisions producing legal/similarly-significant effects (e.g., blocking payments, freezing accounts) and grants rights to meaningful information, human review, and contestation. Regulation (EU) 2016/679. **[FREE]** Fraud systems that auto-block are squarely in scope.
- **EU AI Act [SETTLED framework, with a crucial fraud carve-out]:** Regulation (EU) 2024/1689. **The important, non-obvious nuance:** Annex III, point 5(b) classifies **creditworthiness / credit-scoring** AI as **high-risk**, but **explicitly carves out AI used to detect financial fraud**. So a *pure* fraud-detection model is generally **not** high-risk under the Act — **but** (a) GDPR Art. 22, PSD2, and DORA still apply in full, and (b) **hybrid** systems that also drive credit or access-to-service decisions can be pulled back into high-risk and require individual scope assessment. High-risk obligations phase in around **August 2, 2026** (with creditworthiness-specific timing debated in the "Digital Omnibus" process). **[SETTLED that fraud is carved out; CONTESTED/evolving at the hybrid boundary and on exact dates — VERSION NOTE: verify current text and timelines.]**
- **PSD2 / Strong Customer Authentication [SETTLED, operationally central]:** the PSD2 RTS on SCA (and **Transaction Risk Analysis** exemptions tied to fraud-rate thresholds) directly shape real-time fraud decisioning in the EU — your risk engine's output can determine whether SCA is required or exempted. **[VERSION NOTE: PSD3 / PSR are in progress and will change this; track them.]**
- **DORA (Digital Operational Resilience Act):** ICT/operational-resilience obligations that increasingly wrap ML systems in EU financial institutions. **[FREE]**

**Physics scaffold:** Treat the regulatory constraints as **boundary conditions** on the optimization, not as afterthoughts — the feasible model space is the intersection of "accurate," "explainable," "fair," "auditable," and "resilient." Much of applied fraud-ML expertise is finding good solutions *inside* that constrained region, exactly as physical systems are optimized subject to conservation laws and boundary conditions rather than in free space.

**Phase N exercises:**
1. Generate adverse-action-style reason codes from a TreeSHAP model, then stress-test them against the Kumar et al. and Aas et al. critiques on a case with correlated features — where does the "principal reason" become unstable, and how would you defend it to a validator?
2. Run a disparate-impact analysis (e.g., adverse-impact ratio across proxy groups) on a fraud model; compute calibration vs. equalized-error trade-offs and articulate which you'd choose and why, given the impossibility results.
3. Write a mini model-validation report for one of your models in SR 11-7 terms: conceptual soundness, outcomes analysis, ongoing monitoring, and effective challenge. This is directly reusable at work.

**MVP for Phase N:** SHAP + TreeSHAP papers (+ the two critiques) + SR 11-7 (+ currency check) + the EU-AI-Act fraud-carveout nuance + GDPR Art. 22 + one fairness-impossibility result.

---

# Phase O — AML, Sanctions & Broader Financial Crime

**Goals:** Extend from fraud into the adjacent, heavily-regulated disciplines of anti-money-laundering and sanctions screening. These reuse the modeling toolkit (graphs, anomaly detection, imbalance) but add distinct typologies, a different label regime (SARs, investigations, near-total absence of ground truth), and much heavier compliance machinery (BSA/FinCEN, OFAC, FATF, EU AMLD/AMLR).

**Prerequisites:** Phases H–N (especially K graphs, L anomaly, N regulatory).

**Time:** Full 3–4 weeks; MVP 1.5 weeks (Elliptic + one AML-ML survey + the BSA/OFAC/FATF primers).

### O1. The AML modeling problem & why it's harder than fraud
- **Primary (free, the anchor dataset & paper):** Mark Weber, Giacomo Domeniconi, Jie Chen, Daniel Karl I. Weidele, Claudio Bellei, Tom Robinson & Charles E. Leiserson, "Anti-Money Laundering in Bitcoin: Experimenting with Graph Convolutional Networks for Financial Forensics," *KDD 2019 Workshop on Anomaly Detection in Finance*, arXiv:1908.02591. **[FREE]** Introduces the **Elliptic dataset** (~203k Bitcoin-transaction nodes, 234k edges, 166 features, licit/illicit/unknown) — the most-used public AML graph benchmark, and your reproduction target for K and O. **[SETTLED as the benchmark; note its limits — crypto ≠ fiat rails, and "unknown" labels dominate.]**
- **Primary (statistics/ML survey, free):** Rasmus Jensen & Alexandros Iosifidis, "Fighting Money Laundering with Statistics and Machine Learning," *IEEE Access* 2023, arXiv:2201.04207. **[FREE]** A clear survey of the AML-ML problem structure (transaction monitoring, alert prioritization, the crushing false-positive rates of legacy rule systems). **[SETTLED overview.]**
- **The label reality [SETTLED, and sobering]:** AML has **almost no ground truth** — a Suspicious Activity Report (SAR) is a *suspicion*, not a confirmed label, and confirmed laundering is rarely fed back. This makes supervised AML far shakier than supervised fraud; unsupervised/graph/typology methods and alert-prioritization (reducing false positives on rule-based alerts) dominate. Frame AML ML as **alert triage and network discovery**, not clean classification.

### O2. Typologies, graphs & the money-laundering process
- Learn the three-stage model (**placement, layering, integration**) and concrete typologies (smurfing/structuring, mule networks, trade-based laundering, layering through shell entities). Graphs are natural here — laundering *is* a network phenomenon — so Phase K methods (community detection, motif/cycle finding, GNNs) apply, plus dynamic-graph methods (EvolveGCN) for evolving flows.
- **Synthetic data for scale (since real AML data is locked up):** the **AMLSim** / IBM synthetic AML transaction generators and the **AMLworld / IBM Transactions for AML** datasets (Kaggle) let you build realistic laundering-pattern graphs. **[FREE; VERSION NOTE: check current releases.]**

### O3. Sanctions screening (a different problem: matching, not prediction)
- Sanctions screening is primarily **fuzzy name/entity matching** against watchlists (OFAC SDN, EU consolidated list, UN) — a **record-linkage / string-similarity** problem (Phase K1 entity resolution), not a predictive-modeling one, though ML helps reduce false positives from transliteration, aliases, and name variants. Know the distinction: **screening is deterministic-matching-with-fuzz under zero-tolerance regulatory pressure**, so precision/recall trade-offs are dominated by "never miss a true match," inverting the usual cost calculus. **[SETTLED.]**

### O4. The AML/sanctions regulatory machine
- **US:** the **Bank Secrecy Act (BSA)**, **FinCEN** SAR/CTR requirements, and the **FFIEC BSA/AML Examination Manual** (the operational bible — ffiec.gov). Note the 2021 interagency statement on **model risk management for BSA/AML** (ties Phase N's SR 11-7 to AML models). **[FREE]**
- **Sanctions:** **OFAC** (SDN list, 50% rule, strict liability). **[FREE]**
- **International/EU:** the **FATF Recommendations** (the global standard-setter); the EU's **AMLD** framework moving to the directly-applicable **AML Regulation (AMLR)** and the new **AMLA** (Anti-Money Laundering Authority, based in Frankfurt — directly relevant to you). **[FREE; VERSION NOTE: the EU AML package is new and phasing in — check current status.]**

**Physics scaffold:** Money laundering is a **flow/transport problem on a network** with conservation-like constraints (funds are conserved as they move; laundering obscures the source–sink mapping). Layering is deliberate mixing to maximize entropy of the flow's apparent origin — you're trying to invert a diffusion/mixing process to recover the source, which is exactly an ill-posed inverse problem, and explains why single-transaction features fail and network/temporal structure is essential.

**Phase O exercises:**
1. Reproduce the Weber et al. Elliptic experiment (logistic regression / random forest / GCN); report on the temporal split and honestly assess how the "unknown"-dominated labels limit conclusions.
2. On synthetic AML data (AMLSim/AMLworld), implement a laundering-pattern detector using graph motifs/community detection + an anomaly score; frame the output as *alert prioritization* (reduce false positives on a rule baseline), which is what actually matters operationally.
3. Build a toy sanctions-screening matcher (fuzzy name matching with transliteration handling) and tune it under a "never miss a true match" constraint; observe how the precision/recall frontier differs from fraud.

**MVP for Phase O:** Elliptic paper + the AML-ML survey + BSA/OFAC/FATF primers + one graph-based laundering-detection reproduction.

---

# Phase P — Capstone: Becoming and Staying an Expert

**Goals:** Convert the above into durable, current expertise — an integrated view, a habit of reading the right venues critically, and one or more original contributions grounded in your PayPal work.

**Prerequisites:** H–O (or the MVP spine + one deep pillar).

**Time:** Ongoing; initial 3–4 weeks to establish workflow.

### How to stay current (venues & sources)
- **Academic:** *KDD* and its **Anomaly Detection in Finance** workshop, *AAAI*, *ICDM*, *TheWebConf (WWW)*, *CIKM*, *SIGIR* (for the graph/opinion-fraud line), and *NeurIPS/ICML/ICLR* for methods that later diffuse into fraud. **[FREE via arXiv / proceedings.]**
- **Practitioner & industry:** the ULB Machine Learning Group / Worldline line of work (the most reliable academic-practitioner bridge); vendor and payment-network fraud reports (read critically — marketing-adjacent); central-bank and scheme fraud statistics (ECB, UK Finance) for ground-truth trends. **[VERSION NOTE: threat landscape and especially scam/APP-fraud and GenAI-enabled fraud shift yearly.]**
- **Regulatory:** monitor CFPB, Fed/OCC (SR letters), EU (AI Act guidance, PSD3/PSR, the AML package & AMLA), FinCEN/OFAC, and FATF. In this field, **regulatory change is as important as methodological change**, and it moves on its own clock.
- **Emerging frontier [CONTESTED, watch closely]:** GenAI/LLMs cut both ways — adversaries use them for scaled social-engineering and synthetic identities; defenders explore LLMs for investigator assistance, narrative/SAR drafting, and reasoning over alerts. This is where your *first* curriculum (LLMs, RLVR, systems) meets your *second*. Treat vendor claims skeptically and demand realistic evaluation.

### How to read a fraud/AML paper critically (a protocol)
For every paper ask: **(1)** Is the dataset realistic (size, recency, and does it preserve delayed labels, imbalance, temporal order)? **(2)** Is the evaluation temporally split and free of leakage (the Arp et al. pitfalls)? **(3)** Is the metric operationally meaningful (Precision@k / card-level precision, dollar loss) or a benchmark convenience (global AUC)? **(4)** Is there an *adaptive*-adversary consideration or is it a static test set? **(5)** Would it survive your MRM/validation and regulatory constraints? A method that fails 1–5 is a leaderboard artifact, however high its AUROC.

### Capstone project options (pick one, aligned to your role)
1. **Rigorous baseline audit (highest institutional value):** on realistic time-split data, rigorously compare your production GBM against graph-feature-augmented GBMs and end-to-end GNNs, with proper calibration, example-dependent cost, delayed-label simulation, and Precision@k — and publish (internally or externally) an honest account of what actually helps. This directly tests the CONTESTED claims in Phases K/L.
2. **Delayed-label pipeline:** implement and evaluate the two-classifier (feedback + delayed) architecture on your data; quantify the lift over treating labels as immediate. Reusable at PayPal.
3. **Adversarial robustness study:** red-team a production model with *business-realistic* (not ℓ_p) evasions using SHAP as an attack map; propose costly-to-fake feature hardening.
4. **AML/graph contribution:** reproduce and extend an Elliptic/AMLSim result with a focus on alert-prioritization and honest label-limitation reporting.
5. **Regulatory-ML bridge:** build a reusable model-validation + reason-code + fairness-audit toolkit for fraud models that satisfies SR 11-7 (and its 2026 successor) and GDPR Art. 22 — a genuinely scarce, high-value artifact.

**Open-source / tooling on-ramps:** the fraud-detection-handbook repo (extend the simulator/experiments); DGL / PyTorch Geometric (graph methods, including CARE-GNN/PC-GNN implementations); the `shap` library (contribute cost-sensitive or dependence-aware extensions); imbalanced-learn (with a critical eye, per Phase I). **[VERSION NOTE: check current versions.]**

---

# Overall MVP (time-compressed, ~5–6 weeks FTE)
1. **Week 1 (H + start I):** Handbook Ch. 1–2 + the 2018 "Realistic Modeling" formalization + your fraud typology artifact. Begin rare-event stats.
2. **Week 2 (I):** Elkan 2001 (cost = threshold), the undersampling-calibration correction, Davis–Goadrich, Saito–Rehmsmeier. Lock in "calibrate then decide" and the SMOTE corrective.
3. **Week 3 (J + M-core):** Biggio–Roli threat models + the "Dos and Don'ts" pitfalls; then the delayed-supervised-information paper and the Gama drift survey. Do the point-in-time-leakage exercise.
4. **Week 4 (one modeling pillar):** choose **K** (CARE-GNN + PC-GNN + BWGNN + the "graph-features→GBM" experiment) *or* **L** (aggregation-vs-sequence comparison + anomaly-score-as-feature).
5. **Weeks 5–6 (N-core + a taste of O):** SHAP/TreeSHAP + the two critiques + SR 11-7 (+ currency check) + GDPR Art. 22 + the EU-AI-Act fraud carve-out; skim the Elliptic paper for the AML framing. Start one capstone.

# Full-program time budget (FTE, sequential; overlaps compress this)
- H: 2–3 wk · I: 3–4 wk · J: 2–3 wk · K: 3–4 wk · L: 2–3 wk · M: 3–4 wk · N: 3–4 wk · O: 3–4 wk · P: ongoing. **Realistic part-time (10–15 h/week): ~15–20 months; full-time: ~6–9 months.**

# Benchmarks that should change your plan
- If you can state and prove Elkan's rebalancing↔threshold theorem and derive the undersampling probability-correction → skip the rest of Phase I's remedial passes.
- If you can articulate, unprompted, why ℓ_p adversarial results don't transfer to fraud but the security-evaluation mindset does → Phase J is internalized.
- If you can reproduce CARE-GNN/PC-GNN *and* show whether graph features beat a GBM on a proper temporal split → you've met Phase K's bar; the honest empirical answer is the deliverable.
- If you can implement the two-classifier delayed-label architecture and quantify its lift → Phase M is yours.
- If you can write a SR-11-7-shaped validation report and defend TreeSHAP reason codes against the dependence critiques → Phase N is yours, and it's directly reusable at work.
- If you can read a new fraud/AML paper and correctly tag it [leaderboard-artifact] vs. [production-real] via the 5-question protocol → you've hit the capstone goal; shift to producing.

## Caveats
- **Benchmark–reality gap is the field's defining hazard.** Public fraud/AML datasets are tiny, stale, and stripped of operational structure. Weight practitioner literature and *your own realistic experiments* over leaderboard SOTA more heavily than in any area of Curriculum 1.
- **"GNNs/deep learning beat GBMs for fraud" is CONTESTED and often OVERSTATED.** The settled, defensible position: relational and temporal signal genuinely helps, best captured as complementary features to strong calibrated tree models, or via careful ensembling — not as a wholesale replacement. Prove it on your data before believing it.
- **Regulatory currency:** SR 11-7 has a 2026 successor (verify SR 26-2 / the interagency update); the EU AI Act's fraud carve-out is real but the hybrid-system boundary and exact timelines are evolving (Digital Omnibus); PSD2 is moving to PSD3/PSR; the EU AML package (AMLR/AMLA, Frankfurt-based) is phasing in. **Re-verify every regulatory specific before relying on it**; all such items are flagged.
- **Free-availability:** author/regulator PDFs (the handbook, Elkan, Davis–Goadrich, Dal Pozzolo papers via ULB/Politecnico, SHAP/TreeSHAP, SR 11-7, CFPB circulars, Weber et al., the AML survey, fairmlbook) were free as of research; confirm at point of use. Several key method papers (Bahnsen cost-sensitive work, Jurgovsky sequences, SCARFF, calibration-under-undersampling) are paywalled at the venue but have free author preprints.
- **Citations/editions:** arXiv IDs and venues were verified where possible; a few have preprint↔published discrepancies (e.g., Biggio–Roli 1712.03141 vs. the ACM CCS version; Weber et al. is a KDD *workshop* paper, arXiv:1908.02591). Two version-sensitive items to spot-check before formal citation: the exact SR 11-7 successor number/date, and the EU AI Act creditworthiness timeline.
- **Your stack, honestly:** most of what makes fraud ML hard is *not* model architecture — it's imbalance, delayed/noisy labels, drift, adversarial adaptation, and regulation. An expert's edge is disproportionately in Phases I, J, M, and N, which is where tree-based practitioners most often have the least formal grounding despite the most daily exposure.