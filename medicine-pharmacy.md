# A Multi-Year Autodidact Curriculum in Medicine & Pharmacy

## TL;DR
- **This is a ~3–4 year, part-time (≈10 hrs/week) standalone program in 8 phases** that builds clinical medicine and pharmacology in equal measure from molecular foundations up to critical reading of RCTs and guidelines; a compressed **~12-month MVP fast-path** gets you to literacy + literature-reading competence. All flagship textbook editions below are verified current as of September 2026.
- **The quantitative strands (biostatistics/epidemiology, PK/PD & pharmacometrics) can run in parallel from day one** and are where your physics/ML background gives you the biggest acceleration — PK is literally coupled mass-balance ODEs, dose–response is Hill/receptor-occupancy kinetics, trial power is Monte Carlo, and epidemic models are the SIR/SEIR ODE systems you already know.
- **Anchor texts (verified current editions):** Boron & Boulpaep *Medical Physiology* 4e (2022); Guyton & Hall 15e (2025); Robbins & Cotran *Pathologic Basis of Disease* 11e (2025); Harrison's *Principles of Internal Medicine* 22e (2025); Janeway's *Immunobiology* 10e (2022); Goodman & Gilman 14e (2023); Katzung 16e (2024); Rang & Dale 10e (2024); Rowland & Tozer 5e (2019); plus the FREE Hernán & Robins *Causal Inference: What If* (2020, 2025 revision).

---

## Key Findings

**1. The canonical spines are stable and current.** Both the medicine and pharmacy sides have well-defined "bibles" with recently updated editions. Most flagship texts were refreshed in 2021–2025, so you are buying into a curriculum that will remain edition-current for years.

**2. Your quantitative background is a genuine accelerant, not a decoration.** Pharmacokinetics is a system of linear ODEs solved by the same Laplace/eigenvalue methods you used in physics; population PK is hierarchical Bayesian/mixed-effects modeling; pharmacodynamics is receptor-occupancy statistical mechanics (the Hill equation is the Langmuir isotherm); survival analysis and epidemic modeling are directly in your wheelhouse. You can compress the quantitative strands to a fraction of the time a typical med/pharm student needs.

**3. The mechanistic/clinical strand is the true rate-limiter.** Physiology → biochemistry → pathophysiology → pharmacology → internal medicine is a strict dependency chain that cannot be rushed, because clinical pharmacology only makes sense once you understand the disease it treats. This is where most of the calendar time goes.

**4. Excellent free/open resources exist and are verified**: Hernán & Robins *Causal Inference: What If* (full PDF free); NCBI Bookshelf / StatPearls; OpenStax Anatomy & Physiology and LibreTexts; PubMed Central; the EQUATOR Network for reporting guidelines; and openly published clinical guidelines (ESC, NICE, KDIGO, GOLD, GINA, ADA Standards of Care). These let you build most of the literature-reading and guideline strands at zero cost.

**5. Guidelines and drug-safety content are the only genuinely time-sensitive elements** and must be re-verified at the moment of study — they change annually or faster.

---

## Details: The Phased Curriculum (Full Arc)

**Assumptions & conventions.** Effort is calibrated to a working ML engineer studying seriously ~8–12 hrs/week. Time estimates assume that pace. Calibration tags: **SETTLED** (established consensus), **CONTESTED** (evolving/debated), **OPEN** (genuinely unresolved), **HYPE-WATCH** (overclaimed). Free = openly/legally free; Paywalled = purchase/subscription. Editions marked "verified" were confirmed against publisher pages in Sept 2026.

---

### PHASE 0 — Orientation & the Quantitative On-Ramp (parallel, ongoing)
**Goal:** Stand up your toolkit and the vocabulary of evidence before diving into biology. Establish the two parallel quantitative strands that will run through the whole program.
**Prerequisites:** None (leverages your existing math/Python).

**Primary readings:**
- Hernán MA & Robins JM, *Causal Inference: What If* (Chapman & Hall/CRC, 2020; 2025 online revision). **FREE PDF** (miguelhernan.org/whatifbook). **SETTLED** as the modern causal-inference reference; Part I is essential for reading any observational study. This is your single highest-leverage early read.
- Rothman KJ, Huybrechts KF & Murray EJ, *Epidemiology: An Introduction*, **3rd ed. (Oxford University Press, 2024; ISBN 9780197751541)** — verified. A demanding but concise conceptual primer that deliberately teaches epidemiologic reasoning over mere applied statistics. **SETTLED.**
- Reporting-guideline checklists from the **EQUATOR Network** (free, equator-network.org): **CONSORT 2025** (RCTs — a 30-item checklist published April 14, 2025 simultaneously in *The BMJ*, *JAMA*, *The Lancet*, *Nature Medicine* and *PLOS Medicine*, lead author Sally Hopewell; it **supersedes CONSORT 2010, which should no longer be used**); **SPIRIT 2025** (protocols); **PRISMA 2020** (systematic reviews/meta-analyses); **STROBE** (observational). Read the checklists directly. **SETTLED.**

**Supplementary:** Guyatt et al., *Users' Guides to the Medical Literature* (JAMA/McGraw Hill) for EBM appraisal; the GRADE Handbook (free online) for evidence-grading. StatPearls "Number Needed to Treat," "Hazard Ratio," etc. (free, NCBI Bookshelf).

**Build/lab project (Python):**
1. *Estimation vs. testing:* simulate a two-arm trial in NumPy; compute risk difference, relative risk, odds ratio, NNT, and 95% CIs; plot a p-value function (Rothman's device) to internalize why estimation beats dichotomized significance.
2. *Monte-Carlo power:* write a function that computes power for a two-proportion trial by simulation and compare to the analytic formula; produce a power-vs-sample-size curve.
**Time:** 4–6 weeks to a working baseline; then it runs in the background.
**Currency notes:** CONSORT/SPIRIT are the 2025 versions — confirm you are using CONSORT 2025, not the retired 2010 statement. Causal Inference has periodic online revisions; always pull the current PDF.

---

### PHASE 1 — Molecular & Cellular Foundations (self-contained core)
**Goal:** Acquire exactly the cell/molecular biology and biochemistry a physician-level understanding of disease and drugs requires — no more.
**Prerequisites:** Phase 0 optional.

**Primary readings:**
- Alberts B, Heald R, Johnson A, Morgan D, Raff M, Roberts K, Walter P, *Molecular Biology of the Cell*, **7th ed. (W. W. Norton, 2022)** — verified. Read selectively: membranes & transport, signaling, gene expression, cell cycle, cell death. **SETTLED.**
- Nelson DL & Cox MM, *Lehninger Principles of Biochemistry*, **8th ed. (Macmillan/W. H. Freeman, 2021)** — verified. Focus: enzyme kinetics (primes you for PK/PD), metabolism, bioenergetics. **SETTLED.**

**Supplementary / FREE:** OpenStax *Biology 2e* and LibreTexts biochemistry for gap-filling; NCBI Bookshelf *Molecular Biology of the Cell* legacy chapters.

**Build/lab project (Python):** Implement Michaelis–Menten kinetics; fit Vmax/Km to simulated substrate–velocity data with SciPy `curve_fit`; then implement competitive vs. non-competitive inhibition and show how each transforms a Lineweaver–Burk plot. *This is the conceptual bridge to receptor pharmacology.*
**Time:** 3–4 months (selective reading).
**Currency notes:** Both editions current; no time-sensitive content.

---

### PHASE 2 — Human Physiology by Organ System (the spine of the medicine half)
**Goal:** Deep, mechanistic mastery of normal organ-system function — the substrate on which all pathophysiology and pharmacology is built.
**Prerequisites:** Phase 1.

**Primary readings (choose one anchor + one reference):**
- Boron WF & Boulpaep EL, *Medical Physiology*, **4th ed. (Elsevier, 2022; ISBN 9780323794862)** — verified. The molecular/quantitative-leaning choice; best fit for your background. **SETTLED.**
- Hall JE & Hall ME, *Guyton and Hall Textbook of Medical Physiology*, **15th ed. (Elsevier, 2025; ISBN 9780443111013)** — verified. Clearer single-voice narrative; excellent for cardiovascular/renal. Use as the readable complement. **SETTLED.**

**Supplementary / FREE:** OpenStax *Anatomy & Physiology 2e* (free) for anatomy context; Costanzo *Physiology* for a lighter pass.

**Build/lab projects (Python):**
1. *Cardiovascular:* model the Frank–Starling relationship and a two-element Windkessel as an ODE; simulate arterial pressure decay.
2. *Renal/acid–base:* implement the Henderson–Hasselbalch buffer system; simulate compensation for a metabolic acidosis.
3. *Neuro:* implement the Hodgkin–Huxley action-potential model (coupled nonlinear ODEs) — directly leverages your ODE/numerical-methods skill.
**Time:** 6–8 months (this is a large, central phase).
**Currency notes:** Editions current and stable.

---

### PHASE 3 — Principles of Pharmacology + PK/PD & Pharmacometrics (the spine of the pharmacy half; runs partly parallel to Phase 2)
**Goal:** Master the general principles that govern *every* drug — ADME, receptor theory, dose–response — and build the quantitative PK/PD engine. This is your comparative-advantage phase.
**Prerequisites:** Phase 1 (enzyme kinetics); Phase 2 cardiovascular/renal helpful but can overlap.

**Primary readings:**
- Rang & Dale's *Pharmacology*, **10th ed. (Elsevier, 2024; Ritter, Flower, Henderson, Loke, MacEwan, Robinson, Fullerton; ISBN 9780323873956)** — verified. Best "how drugs work" conceptual foundation. **SETTLED.**
- Rowland M & Tozer TN (Derendorf H & Schmidt S, eds.), *Rowland and Tozer's Clinical Pharmacokinetics and Pharmacodynamics: Concepts and Applications*, **5th ed. (Wolters Kluwer, 2019; ISBN 9781496385048)** — verified. Your PK/PD anchor. **SETTLED.**
- For the modeling layer: Owen JS & Fiedler-Kelly J, *Introduction to Population Pharmacokinetic/Pharmacodynamic Analysis with Nonlinear Mixed Effects Models* (Wiley, **1st and only ed., 2014; ISBN 9780470582299**). **SETTLED** as the standard NONMEM-oriented intro.

**Supplementary / FREE:** Rosenbaum SE, *Basic Pharmacokinetics and Pharmacodynamics*, 2nd ed. (Wiley-Blackwell, 2016/2017; ISBN 9781119143154) with its **free online interactive simulations**; Gabrielsson J & Weiner D, *Pharmacokinetic and Pharmacodynamic Data Analysis: Concepts and Applications*, 5th ed. (Swedish Pharmaceutical Press, 2016; ISBN 9789198299106); Bonate PL, *Pharmacokinetic-Pharmacodynamic Modeling and Simulation*, 2nd ed. (Springer, 2011). Open tooling: **nlmixr2** (R, on CRAN) and **Pumas** (Julia, tutorials.pumas.ai) — both free. Key journal: *CPT: Pharmacometrics & Systems Pharmacology* (much is open access).

**Build/lab projects (Python) — your flagship quantitative work:**
1. Implement one-, two-, and three-compartment PK models as ODE systems in SciPy (`solve_ivp`); derive the analytic solutions via eigen-decomposition and confirm numerically. Fit parameters to simulated plasma-concentration data.
2. Fit a Hill/Emax dose–response curve; connect it explicitly to receptor-occupancy theory (Langmuir isotherm) and derive EC50/Hill coefficient.
3. Build a simple population-PK simulation: add inter-individual variability as random effects; simulate concentration–time profiles across a virtual population (Monte Carlo) and construct a visual predictive check.
4. Model an oral-dosing regimen to steady state; compute accumulation ratio and design a loading dose.
**Time:** 4–6 months; the quantitative pieces move fast for you.
**Currency notes:** Texts current; PK/PD principles are SETTLED. Population-PK *software* evolves — verify tool versions. Note: Owen & Fiedler-Kelly has only one edition (2014); Bonate's "2014" listing is a paperback reprint of the 2011 2nd edition, not a 3rd edition.

---

### PHASE 4 — Pathophysiology / Mechanisms of Disease (the hinge phase)
**Goal:** Understand how normal physiology breaks — the mechanistic basis of disease that connects Phase 2 to clinical medicine and rational therapeutics.
**Prerequisites:** Phases 1–2 (hard); Phase 3 helpful.

**Primary readings:**
- Kumar V, Abbas AK, Aster JC, Debnath J, Das A (eds.), *Robbins & Cotran Pathologic Basis of Disease*, **11th ed. (Elsevier, May 2025; ISBN 9780443264528)** — verified. The definitive mechanisms-of-disease text. **SETTLED.**

**Supplementary:** Hammer & McPhee, *Pathophysiology of Disease: An Introduction to Clinical Medicine* (a mechanisms-focused, more concise alternative/complement); StatPearls disease articles (free) for quick mechanistic refreshers.

**Build/practical project (non-coding):** For three high-prevalence diseases (e.g., atherosclerosis, type 2 diabetes, heart failure), build a one-page "mechanism map" linking molecular lesion → cellular dysfunction → organ pathophysiology → clinical signs → drug target. These maps become the connective tissue for Phases 5–6.
**Time:** 5–7 months.
**Currency notes:** 11th ed. (2025) is current; disease classifications (e.g., tumor nomenclature) update — cross-check against current WHO classifications when relevant.

---

### PHASE 5 — Immunology, Microbiology & Infectious Disease, Medical Genetics (parallel-capable)
**Goal:** Master the immune system (essential for modern therapeutics — biologics, checkpoint inhibitors, vaccines), host–pathogen interaction and antimicrobials, and the genetics underlying disease and pharmacogenomics.
**Prerequisites:** Phases 1–2; Phase 4 concurrent.

**Primary readings:**
- Murphy K, Weaver C, Berg L, *Janeway's Immunobiology*, **10th ed. (W. W. Norton, 2022; ISBN 9780393884890)** — verified. **SETTLED** as the graduate immunology reference.
- Medical microbiology: a current standard reference (e.g., *Jawetz, Melnick & Adelberg's Medical Microbiology* or *Murray's Medical Microbiology*) — verify latest edition at purchase. **SETTLED.**

**Supplementary / FREE:** NCBI Bookshelf hosts free immunology and microbiology references; StatPearls antimicrobial articles.

**Build/practical projects:**
1. (Python) Extend your Phase 0 epidemic model: implement SIR and SEIR as coupled ODEs; add a vaccination compartment; estimate R0 and the critical vaccination threshold. Directly leverages your ODE/dynamics background.
2. (Non-coding) Build an antimicrobial-spectrum grid (drug class × organism) and a resistance-mechanism map.
**Time:** 4–6 months.
**Currency notes:** Immunotherapy and vaccine content evolve fast — cross-check therapeutic claims against current guidelines. **HYPE-WATCH:** microbiome-based therapeutics claims often outrun evidence.

---

### PHASE 6 — Systematic Pharmacology + Clinical Pharmacology & Therapeutics
**Goal:** Drug class by drug class, organ system by organ system — mechanisms, uses, interactions, adverse effects, and rational prescribing. Integrate with the pathophysiology from Phase 4.
**Prerequisites:** Phases 3 and 4 (hard); Phase 5 for anti-infectives/immunomodulators.

**Primary readings:**
- Brunton LL & Knollmann BC (eds.), *Goodman & Gilman's The Pharmacological Basis of Therapeutics*, **14th ed. (McGraw Hill, 2023; ISBN 9781264258079)** — verified. The definitive reference; new chapters on pharmacovigilance, the blood–brain barrier, cannabis, and biologics (antibodies, checkpoint inhibitors, CAR-T). **SETTLED.**
- Vanderah TW (ed.), *Katzung's Basic & Clinical Pharmacology*, **16th ed. (McGraw Hill, 2024; ISBN 9781260463309)** — verified. The more teachable, case-based systematic pass; use as primary study text with G&G as reference. **SETTLED.**

**Supplementary / FREE:** British National Formulary (BNF) for prescribing detail (UK); AccessPharmacy (paywalled) hosts both G&G and Katzung; StatPearls drug monographs (free). Special-population pharmacology (pediatric, geriatric, pregnancy/lactation, renal & hepatic impairment) is covered within both texts — supplement with current product labels.

**Build/practical projects:**
1. (Non-coding) Build drug-class mechanism maps for the major systems (autonomic, cardiovascular, CNS, endocrine, antimicrobial, chemotherapy), each tying receptor/enzyme target → downstream effect → clinical indication → key adverse effects → major drug–drug interactions (CYP450 focus).
2. (Python) Model a clinically important CYP-mediated drug–drug interaction as a change in clearance in your Phase 3 PK model; quantify the AUC change and the dose adjustment needed.
**Time:** 7–9 months (large phase; the heart of the pharmacy half).
**Currency notes:** **TIME-SENSITIVE** — new drug approvals, boxed warnings, and interaction data change continuously. Always re-verify specific drug facts against current FDA/EMA labels and safety communications at time of study.

---

### PHASE 7 — Clinical/Internal Medicine, Diagnostics & Clinical Reasoning + Landmark-Trial Literature Immersion
**Goal:** Integrate everything into how disease presents, is diagnosed, and is managed; achieve fluency in reading the primary clinical literature and guidelines. This is where endpoints (a), (b), (c) converge.
**Prerequisites:** Phases 2, 4, 5, 6.

**Primary readings:**
- Loscalzo J, Fauci A, Kasper D, Hauser S, Longo D, Jameson JL, et al. (eds.), *Harrison's Principles of Internal Medicine*, **22nd ed. (McGraw Hill, 2025; ISBN 9781265979317)** — verified (released Aug 2025). The authoritative applied-pathophysiology + clinical-medicine reference. **SETTLED.**
- *Kumar & Clark's Clinical Medicine* (verify latest edition) as a more concise, readable European-context complement. **SETTLED.**

**Landmark trials to read in full (verified citations) — read these as primary literature, appraising each with your Phase 0 toolkit:**
- **ISIS-2** (ISIS-2 Collaborative Group, aspirin/streptokinase in acute MI), *Lancet* 1988;332:349–360. **SETTLED** classic.
- **4S / Scandinavian Simvastatin Survival Study** (statin secondary prevention), *Lancet* 1994. **SETTLED.**
- **UKPDS** (glycemic/BP control in type 2 diabetes; e.g., UKPDS 33 & 38), *Lancet*/*BMJ* 1998. **SETTLED.**
- **PARADIGM-HF** (McMurray JJV et al., sacubitril/valsartan vs enalapril in HFrEF), *NEJM* 2014;371:993–1004. **SETTLED.**
- **EMPA-REG OUTCOME** (Zinman B et al., empagliflozin CV outcomes in T2DM), *NEJM* 2015;373:2117–2128. **SETTLED** — launched the SGLT2-inhibitor era.
- **SPRINT** (SPRINT Research Group / Wright JT Jr, intensive vs standard BP control), *NEJM* 2015;373:2103–2116; final report *NEJM* 2021;384:1921–1930. **CONTESTED** — BP targets remain debated across guidelines.
- **DAPA-HF** (McMurray JJV et al., dapagliflozin in HFrEF), *NEJM* 2019;381:1995–2008. **SETTLED.**
- **RECOVERY** (RECOVERY Collaborative Group / Horby P et al., dexamethasone in COVID-19), *NEJM* 2021;384:693–704. **SETTLED** — model of a large pragmatic platform trial.
- **KEYNOTE-189** (Gandhi L et al., pembrolizumab + chemo in metastatic non-squamous NSCLC), *NEJM* 2018;378:2078–2092. **SETTLED** mechanism; **CONTESTED**/evolving on sequencing/biomarkers.
- **SELECT** (Lincoff AM et al., semaglutide CV outcomes in obesity without diabetes), *NEJM* 2023;389:2221–2232. **CONTESTED**/evolving — reshaping obesity medicine. **HYPE-WATCH** on GLP-1 "cure-all" claims.

**Curated free trial-summary resources** (use as an index, then read the primary paper): WikiJournalClub and 2 Minute Medicine's "Classics in Medicine" directory.

**Where to find current authoritative guidelines (free, verified official portals) — re-verify at time of study:**
- **US:** ACC/AHA (acc.org; published in *Circulation*/*JACC*, rolling topic-by-topic updates); IDSA (idsociety.org; *Clinical Infectious Diseases*; uses GRADE); ADA **Standards of Care in Diabetes** — updated **annually every January**; the **2026 edition was released Dec 8, 2025** as a supplement to *Diabetes Care* Vol 49, Suppl 1 (Summary of Revisions doi:10.2337/dc26-SREV, S6–S12; PPC co-chaired by Mandeep Bajaj and Rozalina McCoy); KDIGO (kdigo.org; *Kidney International*).
- **Europe:** ESC (escardio.org; new guidelines released each year timed to the ESC Congress, full texts free in *European Heart Journal*); NICE (nice.org.uk; continuously updated); EASL (easl.eu; *Journal of Hepatology*); EMA product information.
- **Respiratory (global annual reports):** **GOLD 2026 Report** (goldcopd.org; v1.3 dated Dec 8, 2025, released Nov 2025 at the 10th annual COPD International Conference; adds mepolizumab as a biologic option and a new AI chapter) for COPD; **GINA 2026 Strategy Report** (ginasthma.org; released May 5, 2026; adds four acute-asthma flowcharts and AIR/ICS-SABA therapy at Step 1) for asthma.

**Build/practical projects (Python + non-coding):**
1. *Reproduce a meta-analysis:* pull summary data from a published systematic review and reproduce the forest plot and pooled effect (fixed + random effects) in Python; compute heterogeneity (I²).
2. *Survival analysis:* on a public dataset (e.g., a lung-cancer survival set), fit Kaplan–Meier curves, run a log-rank test, and fit a Cox proportional-hazards model with `lifelines`; interpret hazard ratios and check the proportional-hazards assumption.
3. *Structured critical appraisal:* write a formal appraisal of two of the landmark trials above using CONSORT 2025 + a risk-of-bias framework, ending with a GRADE-style certainty judgment.
**Time:** 8–10 months.
**Currency notes:** **HIGHLY TIME-SENSITIVE** — guidelines, drug approvals, and trial updates change constantly; treat every guideline recommendation as "verify current version."

---

### PHASE 8 — Specialized & Applied Strands (elective, choose by interest)
**Goal:** Round out the "pharmacy craft" and drug-lifecycle knowledge; deepen selected areas.
**Prerequisites:** Phases 3, 6.

**Primary readings:**
- Klaassen CD (ed.), *Casarett & Doull's Toxicology: The Basic Science of Poisons* — current in-print edition is the **9th (McGraw Hill, 2018)**; a **10th edition is announced (copyright 2027, ISBN 9781265492175)** — verify availability at time of study. **SETTLED.**
- Taylor KMG & Aulton ME (eds.), *Aulton's Pharmaceutics: The Design and Manufacture of Medicines* — **6th ed. (Elsevier, 2021; ISBN 9780702081545)** verified; a **7th ed. is announced (2025, ISBN 9780443287824)** — verify at purchase. The "pharmacy craft" of formulation and drug delivery. **SETTLED.**
- Medicinal chemistry essentials: Patrick GL, *An Introduction to Medicinal Chemistry* (Oxford) — verify latest edition; keep to structure–activity relationships and drug-design basics since you have a separate chemistry track. **SETTLED.**

**Drug development & regulation strand (free/primary sources):** FDA and EMA websites for the preclinical → Phase I–IV → approval → post-marketing (pharmacovigilance) lifecycle; ICH GxP guidelines; the G&G 14e pharmacovigilance chapter. **SETTLED** framework; **CONTESTED** areas include accelerated-approval and surrogate-endpoint policy.

**Build/practical projects (Python):**
1. Simulate a Phase II dose-finding trial: combine your Emax PD model with a trial simulation; use Monte Carlo to compare adaptive vs fixed designs on power and expected sample size.
2. Build an exposure–response analysis linking your Phase 3 PK model output to a simulated efficacy/toxicity endpoint.
**Time:** 3–6 months depending on breadth.
**Currency notes:** Casarett & Doull and Aulton both have newer editions imminent — verify. Regulatory policy is **TIME-SENSITIVE**.

---

## The MVP Fast-Path (~12 months, ~10 hrs/week)

The shortest route to (a) informed-reader fluency, (b) literature-reading competence, and a working (if not exhaustive) mechanistic base:

1. **Months 1–2 — Evidence toolkit (Phase 0):** Hernán & Robins Part I (free); Rothman *Epidemiology: An Introduction* 3e; EQUATOR checklists (CONSORT 2025 etc.). Do the Monte-Carlo power + estimation Python labs. → *Enables literature reading immediately.*
2. **Months 2–5 — Core physiology + disease (compressed Phases 2 & 4):** Guyton & Hall 15e (the readable single-voice text) for cardiovascular, renal, respiratory, endocrine, neuro; then the corresponding Robbins 11e chapters. Do the CV/renal/HH Python labs. Skip the exhaustive Boron reference read.
3. **Months 4–7 — Pharmacology principles + PK/PD (Phase 3):** Rang & Dale 10e + Rowland & Tozer 5e. Do the compartmental-PK and Hill-curve labs — fast for you.
4. **Months 6–10 — Systematic pharmacology (compressed Phase 6):** Katzung 16e (skip G&G as cover-to-cover; use as reference). Build drug-class mechanism maps for the major systems.
5. **Months 9–12 — Clinical integration + trials (compressed Phase 7):** Use Harrison's 22e as a reference (not cover-to-cover); read the 10 landmark trials above; reproduce a meta-analysis and run the survival-analysis lab. Learn to navigate ESC/NICE/ADA guideline portals.

**MVP outcome:** You will follow medical/pharma news fluently, hold substantive conversations with clinicians and pharmacists, and critically appraise most RCTs, meta-analyses, and guidelines — with solid (not comprehensive) mechanistic depth. The full arc then deepens immunology/micro, toxicology, pharmaceutics, and the long tail of internal medicine.

---

## Dependency Map

```
PHASE 0 (Evidence/quant toolkit) ─── runs in PARALLEL throughout ──────────────┐
                                                                               │
PHASE 1 (Cell/molecular + biochem)                                             │
   │                                                                           │
   ├──> PHASE 2 (Physiology) ──┬──> PHASE 4 (Pathophysiology) ──┐              │
   │                           │                                │              │
   └──> PHASE 3 (Pharm principles + PK/PD) ──────┐             │              │
        (can start alongside late Phase 2)       │             │              │
                                                 ▼             ▼              │
   PHASE 5 (Immuno/Micro/Genetics) ────────> PHASE 6 (Systematic + clinical    │
        (parallel with 4)                         pharmacology) ──┐            │
                                                                  ▼            ▼
                                             PHASE 7 (Internal medicine + literature/guidelines)
                                                                  │
                                                                  ▼
                                             PHASE 8 (Toxicology, pharmaceutics, med-chem, drug dev — elective)
```

**Strands that run in parallel:** (i) the **biostatistics/epidemiology** strand (Phase 0) should run continuously from day one; (ii) the **PK/PD & pharmacometrics** strand (Phase 3) can begin as soon as you have enzyme kinetics (Phase 1) and can proceed alongside physiology; (iii) **immunology/micro/genetics** (Phase 5) can run in parallel with pathophysiology (Phase 4). The strict serial core is **1 → 2 → 4 → 6 → 7**.

---

## Overall Timeline & Effort

- **Full arc:** ~**42–52 months** (3.5–4.5 years) at ~8–12 hrs/week, i.e., roughly **1,800–2,400 hours** total. Phases 2, 4, 6, and 7 dominate the calendar.
- **MVP fast-path:** ~**12 months** at ~10 hrs/week (~500 hours).
- If you can invest 15–20 hrs/week, compress the full arc toward ~3 years.

---

## Recommendations (staged, with decision thresholds)

**Stage 1 (Months 0–2): Start two things at once.** Begin Phase 0 (free Causal Inference + EQUATOR checklists + Python stats labs) *and* the first physiology chapters (Phase 2). Rationale: the evidence toolkit is where your existing skills give an instant win and immediately unlocks literature reading — one of your three explicit endpoints. **Threshold to proceed:** you can independently appraise a simple RCT and compute NNT/HR with CIs.

**Stage 2 (Months 2–8): Commit to the serial core.** Drive physiology (Phase 2) to reasonable depth, then start pathophysiology (Phase 4), while spinning up PK/PD (Phase 3) in parallel — this is your comparative advantage and keeps motivation high. **Threshold:** you can draw a mechanism map for atherosclerosis, T2D, and heart failure unaided, and you have working 1–3 compartment PK models in SciPy.

**Stage 3 (Months 8–20): Systematic pharmacology + clinical integration.** Katzung → Goodman & Gilman as reference; begin reading landmark trials in full. **Threshold to declare "literature-competent":** you can read a new NEJM/Lancet RCT and a Cochrane review and produce a structured CONSORT/GRADE appraisal in under two hours.

**Stage 4 (Months 20+): Depth and electives.** Harrison's as reference across internal medicine; add immunology/micro depth, then Phase 8 electives by interest (pharmacometrics if you want to go deepest where your skills transfer; toxicology/pharmaceutics/drug development for breadth).

**Ongoing:** Subscribe to NEJM, *The Lancet*, JAMA, and BMJ tables of contents; for the pharmacology endpoint add *Clinical Pharmacology & Therapeutics*, *British Journal of Clinical Pharmacology*, and *CPT: Pharmacometrics & Systems Pharmacology*. Re-verify any guideline or drug-safety fact at the moment you rely on it.

**What would change this plan:** If your goal narrows to (b) literature-reading only, stop after the MVP. If you later want a data-science/clinical-ML layer (explicitly excluded now), it would attach after Phase 7. If a target textbook's newer edition ships mid-study (Aulton 7e, Casarett & Doull 10e), switch at a natural phase boundary rather than mid-phase.

---

## Caveats

- **Editions verified vs. not:** Verified current against publisher pages (Sept 2026): Boron & Boulpaep 4e (2022), Guyton & Hall 15e (2025), Robbins 11e (2025), Harrison's 22e (2025), Janeway 10e (2022), Goodman & Gilman 14e (2023), Katzung 16e (2024), Rang & Dale 10e (2024), Rowland & Tozer 5e (2019), MBoC 7e (2022), Lehninger 8e (2021), Rothman *Epidemiology: An Introduction* 3e (2024), Owen & Fiedler-Kelly (2014, sole edition), Aulton 6e (2021), Casarett & Doull 9e (2018), Hernán & Robins (2020/2025). **Announced-but-verify-at-purchase:** Aulton's Pharmaceutics 7e (2025); Casarett & Doull 10e (copyright 2027); latest editions of Kumar & Clark, Patrick's medicinal chemistry, and the chosen medical-microbiology text.
- **Time-sensitive content:** All clinical practice guidelines, drug approvals, boxed warnings, and drug-interaction data change frequently (guidelines often annually). Every such item must be re-verified at time of study against the official portal or regulator (FDA/EMA). ADA 2026, GOLD 2026 and GINA 2026 are the current annual reports as of this writing; a new annual cycle will supersede them.
- **This is a knowledge curriculum, not clinical training.** It builds reading, reasoning, and mechanistic mastery — not licensure, patient-care competence, or prescribing authority. Nothing here should be used to make personal medical decisions.
- **Free-resource legality:** The free resources named (Causal Inference PDF, OpenStax, LibreTexts, StatPearls/NCBI Bookshelf, EQUATOR, PMC, official guideline portals, Rosenbaum simulations, nlmixr2/Pumas tutorials) are legitimately open. Textbook PDFs circulating on file-sharing sites are typically not — buy or borrow via a library.
- **HYPE-WATCH domains to read skeptically:** GLP-1 agonists as universal therapy; microbiome therapeutics; many AI-in-medicine and "precision medicine" claims; supplement/nutraceutical efficacy. Apply your Phase 0 toolkit hardest here.
- **Coverage gaps by design:** Anatomy is included only to the depth clinical context requires (via OpenStax + physiology texts), not as a full dissection-based course; a fuller foundational biology/organic-chemistry treatment would live in your separate chemistry track and in Alberts/Lehninger.
- **One unresolved citation flag:** The exact page range/DOI of the original 2015 SPRINT NEJM paper (373:2103–2116) is cited from a secondary source; the 2021 final report (384:1921–1930) was independently confirmed. Verify the 2015 primary paper directly when you read it.