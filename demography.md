# Advanced-Practitioner Demography: A Phased Curriculum & Reading List

## TL;DR
- **Yes, this is achievable in 2–3 years part-time.** Build formal/mathematical demography as the backbone (Preston–Heuveline–Guillot + Keyfitz–Caswell + Wachter), then layer population studies, applied/technical estimation, and historical demography on top; the R toolchain (HMDHFDplus, demography, StMoMo, DemoTools, popbio, bayesPop, DemoKin) lets you *run* every method, and your physics/ML background makes the load-bearing bridges (Perron–Frobenius, SVD, Markov chains, renewal integral equations, Bayesian hierarchical models) genuinely accelerating rather than decorative.
- **The canonical spine is stable and largely verifiable at the primary-source level:** Preston et al. (2001, Blackwell/Wiley, still current), Keyfitz & Caswell (3rd ed., 2005, Springer), Wachter (2014, Harvard, with free draft chapters), plus a cluster of seminal papers (Lotka; Bongaarts 1978; Omran 1971; Lee–Carter 1992; Oeppen–Vaupel 2002; Bongaarts–Feeney 1998) — and two fully free method compendia (IUSSP *Tools for Demographic Estimation* 2013; UN *Manual X* 1983).
- **Calibrate the theory honestly:** stable-population math and the Bongaarts accounting are SETTLED; classical demographic transition theory is SETTLED-descriptive but CONTESTED-causal (Princeton project); the Second Demographic Transition and the demographic dividend's automaticity are CONTESTED; the maximum-lifespan/late-life plateau question and the timing of peak world population are OPEN; the neo-Malthusian "population bomb" is HYPE-WATCH.

---

## Key Findings

**The field has a clear, verifiable canon.** The modern graduate spine is Samuel H. Preston, Patrick Heuveline & Michel Guillot, *Demography: Measuring and Modeling Population Processes* (Blackwell, 2001; now Wiley-Blackwell, ISBN 9781557864512 — still the current edition, no 2nd edition exists). The mathematical backbone is Nathan Keyfitz & Hal Caswell, *Applied Mathematical Demography* (3rd ed., Springer, 2005, ISBN 9780387225371). The best modern teaching text is Kenneth W. Wachter, *Essential Demographic Methods* (Harvard University Press, 2014, ISBN 9780674045576). The matrix-population reference is Hal Caswell, *Matrix Population Models: Construction, Analysis, and Interpretation* (2nd ed., Sinauer, 2001, ISBN 9780878930968).

**Two flagship method compendia are free.** The IUSSP *Tools for Demographic Estimation* (Moultrie, Dorrington, Hill, Hill, Timæus & Zaba, eds., 2013) is fully open at demographicestimation.iussp.org, and the UN *Manual X: Indirect Techniques for Demographic Estimation* (1983, ST/ESA/SER.A/81) is a free UN PDF.

**The R ecosystem is mature.** On CRAN: demography (Hyndman), HMDHFDplus (Riffe), StMoMo (Villegas, Millossovich & Kaishev), MortalityLaws (Pascariu), DemoDecomp (Riffe), popbio (Stubben), bayesTFR/bayesLife/bayesPop (Ševčíková & Raftery), DemoKin (Williams & Alburez-Gutierrez). Two caveats the learner must know: **DemoTools is GitHub-only** (install via `remotes::install_github("timriffe/DemoTools")`), and **MortalitySmooth was archived on CRAN on 2020-12-10** (its dependency svcm was archived) — install from the CRAN archive or prefer alternatives.

**Frankfurt/Germany anchors are strong.** The Bundesinstitut für Bevölkerungsforschung (BiB) is in Wiesbaden (~40 min from Frankfurt); the Max Planck Institute for Demographic Research (MPIDR) in Rostock co-hosts the Human Mortality Database; Destatis (Wiesbaden) and Eurostat provide German/EU data and projections. These are natural venues for talks, data, and possible collaboration.

---

## Details

### How to use this document
The program is organized as **Module 0 → Module 13**, each with goals/mastery, prerequisites, primary readings, supplementary readings, a moderate hands-on component (R-first, Python noted), and time estimate. After the modules you get the **Dependency Map**, an **MVP Fast-Path**, the **Full Arc**, **Calibration Tags**, and **Edition & Access** notes. Optional cross-disciplinary bridges are marked **[BRIDGE]** and are genuinely load-bearing for someone with your background.

Access legend: **FREE** = legally free/open; **PAYWALLED** = commercial; **FREE-DRAFT** = author or course PDF widely available.

---

### MODULE 0 — Orientation & Data Infrastructure
**Goals / mastery:** Explain what demography is; write and manipulate the demographic balancing equation; read and draw the Lexis diagram; distinguish period vs cohort perspectives; know the major data sources (censuses, vital registration, sample surveys) and their error structures; pull data programmatically from HMD, HFD, WPP, IPUMS, DHS; stand up a reproducible R (and Python) toolchain.
**Prerequisites:** None beyond your existing quant background.
**Primary readings:**
- Preston, Heuveline & Guillot, *Demography* (2001), Ch. 1–2. PAYWALLED.
- Wachter, *Essential Demographic Methods* (2014), Introduction & Ch. 1. PAYWALLED (FREE-DRAFT chapters circulate from Wachter's Berkeley course).
- HMD Methods Protocol (Wilmoth, Andreev, Jdanov, Glei et al.), at mortality.org. FREE.
**Supplementary:** Donald T. Rowland, *Demographic Methods and Concepts* (Oxford, 2003) Ch. 1–2 — gentle on-ramp with Excel modules on a companion CD-ROM. PAYWALLED.
**Hands-on:**
1. Install R + tidyverse/data.table; register at mortality.org and humanfertility.org; use **HMDHFDplus** to pull Germany (DEUTNP) and Sweden (SWE) life tables and HFD fertility. *Python:* there is no maintained equivalent; call R via rpy2, or hit HMD's CSV endpoints with pandas.
2. Draw a Lexis diagram programmatically; place a cohort, a period, and an age band; overlay actual deaths from an HMD Lexis triangle file.
3. Reproduce the balancing equation for Germany 2000→2020 using Destatis + HMD counts.
**Datasets:** HMD (DEUTNP, SWE), HFD, WPP 2024, Destatis Genesis.
**Estimated time:** 3–4 weeks.

---

### MODULE 1 — Rates, Exposure & Standardization
**Goals / mastery:** Compute person-years and occurrence-exposure rates; distinguish crude, age-specific, and standardized rates; perform direct and indirect standardization; compute comparative mortality/fertility figures and the SMR; understand the Kitagawa decomposition of a rate difference.
**Prerequisites:** Module 0.
**Primary readings:**
- Preston et al., *Demography* (2001), Ch. 2–3. PAYWALLED.
- Kitagawa, E. (1955), "Components of a Difference Between Two Rates," *JASA* 50(272):1168–1194. PAYWALLED (JSTOR).
**Supplementary:** Andrew Hinde, *Demographic Methods* (Arnold, 1998), Ch. 3–5. PAYWALLED.
**Hands-on:**
1. Directly and indirectly standardize German vs Nigerian crude death rates (WPP age structures); compute the SMR.
2. Kitagawa-decompose the crude death-rate gap between two German Länder into rate vs age-structure components (use **DemoDecomp**).
**Datasets:** WPP 2024, HMD, Destatis Länder tables.
**Estimated time:** 2–3 weeks.

---

### MODULE 2 — Mortality & the Life Table
**Goals / mastery:** Build complete and abridged period life tables from scratch; know all life-table functions and their relationships; handle the a(x) problem (Chiang, Preston, Andreev–Kingkade); build cohort life tables; construct multiple-decrement (cause-deleted) and associated single-decrement tables; articulate the exact link between the life table and hazard/survival analysis. **[BRIDGE]** The life-table survivorship l(x) is a survival function S(x); μ(x) is the hazard; you already know this from survival analysis — map every life-table column onto its hazard-analysis counterpart.
**Prerequisites:** Modules 0–1.
**Primary readings:**
- Preston et al., *Demography* (2001), Ch. 3–4 (life tables and multiple decrement). PAYWALLED.
- Chiang, C.L. (1984), *The Life Table and Its Applications*, Krieger. PAYWALLED.
- Keyfitz & Caswell, *Applied Mathematical Demography* (3rd ed., 2005), Ch. 2 ("The Life Table"). PAYWALLED.
**Supplementary:** Preston et al. appendix on a(x); Andreev & Kingkade (2015), "Average age at death in infancy...," *Demographic Research* 33:363–390. FREE (open access).
**Hands-on:**
1. Build a complete period life table for Germany from HMD Mx/Dx/Nx by hand in R; verify against HMD's published lt. *Python:* replicate with NumPy — this is a natural NumPy exercise.
2. Build an abridged (5-year) life table; compare a(x) assumptions.
3. Construct a cause-deleted life table (delete cardiovascular deaths) and compute the gain in e0. Use **MortalityLaws**/**DemoTools** helpers.
**Datasets:** HMD Germany, WHO cause-of-death.
**Estimated time:** 4–5 weeks.

---

### MODULE 3 — Mortality Modeling & Analysis
**Goals / mastery:** Fit parametric mortality laws (Gompertz, Gompertz–Makeham, Heligman–Pollard, Siler); use model life tables (Coale–Demeny, UN, INDEPTH, Wilmoth et al. log-quadratic); situate the epidemiologic transition; do cause-of-death analysis; decompose life-expectancy differences by age and cause (Arriaga; Pollard); compute health expectancy via the Sullivan method; state precisely what is known and unknown in the limits-to-longevity debate. **[BRIDGE]** Gompertz/Makeham are hazard functions μ(x)=α e^{βx}(+γ); fitting them is nonlinear regression / MLE on a hazard — familiar terrain.
**Prerequisites:** Module 2.
**Primary readings:**
- Gompertz, B. (1825), "On the Nature of the Function Expressive of the Law of Human Mortality," *Phil. Trans. R. Soc.* 115:513–583. FREE.
- Omran, A.R. (1971), "The Epidemiologic Transition: A Theory of the Epidemiology of Population Change," *Milbank Memorial Fund Quarterly* 49(4):509–538 (reprinted *Milbank Q.* 2005;83(4):731–757). FREE (Milbank).
- Arriaga, E. (1984), "Measuring and Explaining the Change in Life Expectancies," *Demography* 21(1):83–96. PAYWALLED.
- Wilmoth, J. et al. (2012), "A flexible two-dimensional mortality model for use in indirect estimation," *Population Studies* 66(1):1–28. PAYWALLED.
- Oeppen, J. & Vaupel, J.W. (2002), "Broken Limits to Life Expectancy," *Science* 296(5570):1029–1031, DOI 10.1126/science.1069675. PAYWALLED (FREE-DRAFT at user.demogr.mpg.de/jwv).
**Supplementary (the longevity debate — read as a set):** Barbi, Lagona, Marsili, Vaupel & Wachter (2018), "The plateau of human mortality: Demography of longevity pioneers," *Science* 360(6396):1459–1461; vs Dong, Milholland & Vijg (2016), "Evidence for a limit to human lifespan," *Nature* 538(7624):257–259; plus the comments (Beltrán-Sánchez, Austad & Finch 2018; Newman 2018) and Olshansky & Ault's fourth-stage paper (1986, *Milbank Q.* 64(3):355–391).
**Hands-on:**
1. Fit Gompertz–Makeham, Heligman–Pollard, and Siler to German adult mortality using **MortalityLaws**; compare AIC. *Python:* fit with scipy.optimize.
2. Arriaga-decompose the Germany-vs-Japan e0 gap by age (**DemoDecomp**), then by age and cause.
3. Sullivan health-expectancy calculation using SHARE/Eurostat disability prevalences.
4. Reproduce the Oeppen–Vaupel record-e0 line from HMD and extend to the present.
**Datasets:** HMD, WHO/Eurostat cause data, IDL (International Database on Longevity).
**Estimated time:** 5–6 weeks.

---

### MODULE 4 — Fertility
**Goals / mastery:** Compute CBR, GFR, ASFR, TFR, completed cohort fertility, parity, parity progression ratios; separate tempo and quantum; apply the Bongaarts–Feeney tempo adjustment and know its critiques; operationalize the Bongaarts proximate-determinants framework; place Coale's preconditions for fertility decline.
**Prerequisites:** Modules 0–2.
**Primary readings:**
- Bongaarts, J. (1978), "A Framework for Analyzing the Proximate Determinants of Fertility," *Population and Development Review* 4(1):105–132. PAYWALLED (JSTOR 1972149).
- Bongaarts, J. & Feeney, G. (1998), "On the Quantum and Tempo of Fertility," *Population and Development Review* 24(2):271–291. PAYWALLED.
- Preston et al., *Demography* (2001), Ch. 5 (fertility). PAYWALLED.
- Coale, A.J. (1973), "The demographic transition reconsidered," in *IUSSP International Population Conference, Liège*.
**Supplementary:** Stover, J. (1998), "Revising the Proximate Determinants of Fertility Framework: What Have We Learned in the Past 20 Years?" *Studies in Family Planning* 29(3):255–267 (critique/update); Kohler & Ortega (2002), tempo-adjusted parity measures, *Demographic Research* 6. FREE (Demographic Research).
**Hands-on:**
1. Compute period TFR and completed cohort fertility for Germany from HFD; visualize the tempo distortion of the 1970s–2000s.
2. Apply the Bongaarts–Feeney adjustment to German period TFR by birth order.
3. Fit the Bongaarts proximate-determinants indices (Cm, Cc, Ci, Ca) to a DHS country.
**Datasets:** HFD, DHS.
**Estimated time:** 4 weeks.

---

### MODULE 5 — Migration & Spatial Demography
**Goals / mastery:** Understand why migration is the hardest component to measure; compute in/out/gross/net migration; build multiregional life tables and projections (Rogers); fit gravity/spatial-interaction models; distinguish internal vs international migration; critically compare migration theories (Lee's push–pull; Zelinsky's mobility transition; Massey et al. cumulative causation).
**Prerequisites:** Modules 2, 6 (can be taken in parallel).
**Primary readings:**
- Rogers, A. (1975/1995), *Introduction to Multiregional Mathematical Demography*, Wiley (or *Multiregional Demography*, 1995). PAYWALLED.
- Lee, E.S. (1966), "A Theory of Migration," *Demography* 3(1):47–57. PAYWALLED.
- Zelinsky, W. (1971), "The Hypothesis of the Mobility Transition," *Geographical Review* 61(2):219–249. PAYWALLED.
- Massey, D. et al. (1993), "Theories of International Migration: A Review and Appraisal," *Population and Development Review* 19(3):431–466. PAYWALLED.
**Supplementary:** Abel, G. & Sander, N. (2014), "Quantifying Global International Migration Flows," *Science* 343(6178):1520–1522. PAYWALLED. (Abel's flow-estimation methods are implemented in R and worth replicating.)
**REFERENCE-AND-BUILD (do not re-teach):** For the *genetic* dimension of migration and population structure (F_ST, admixture, isolation-by-distance), you already have a population-genomics curriculum. Bridge it here: note that the demographic net-migration matrix and the population-genetics migration matrix are the same object viewed through different data; multiregional Leslie/Rogers matrices are the demographic analogue of stepping-stone/island migration models. Do **not** re-derive F_ST.
**Hands-on:**
1. Estimate net migration for German Länder by the residual (vital-statistics) method.
2. Fit a gravity model of interregional migration flows (Poisson GLM) — a natural regression exercise; *Python:* statsmodels GLM.
3. Build a two-region Rogers multiregional projection.
**Datasets:** Destatis interregional flows, Eurostat, global bilateral flow estimates.
**Estimated time:** 4 weeks.

---

### MODULE 6 — Age Structure, Stable Population Theory & Momentum
**Goals / mastery:** Read and build population pyramids; compute dependency and support ratios; derive and solve Lotka's renewal (integral) equation for the intrinsic growth rate r; characterize stable and stationary populations; compute population momentum (Keyfitz); state weak and strong ergodicity precisely. **[BRIDGE — load-bearing]** Lotka's characteristic equation ∫ e^{−rx} l(x) m(x) dx = 1 is a renewal/integral equation; the intrinsic rate r is its dominant root. The discrete analogue is the Leslie matrix whose dominant eigenvalue λ = e^r and whose right/left eigenvectors are the stable age distribution and reproductive value — this is the **Perron–Frobenius theorem** for nonnegative primitive matrices. Ergodicity = convergence to the dominant eigenvector regardless of initial conditions.
**Prerequisites:** Modules 2, and comfort with eigenvalue problems (you have this).
**Primary readings:**
- Sharpe, F.R. & Lotka, A.J. (1911), "A problem in age-distribution," *Philosophical Magazine* 21:435–438. FREE (public domain). See also Smith, D. & Keyfitz, N., *Mathematical Demography: Selected Papers* (2nd ed., Springer, 2013) — the annotated source collection. PAYWALLED.
- Coale, A.J. (1972), *The Growth and Structure of Human Populations: A Mathematical Investigation*, Princeton UP. PAYWALLED (JSTOR/MUSE).
- Keyfitz & Caswell (2005), Ch. 3–5 (stable populations, reproductive value, momentum). PAYWALLED.
- Keyfitz, N. (1971), "On the momentum of population growth," *Demography* 8(1):71–80. PAYWALLED.
**Supplementary:** Preston et al. (2001), Ch. 7 (stable populations).
**Hands-on:**
1. Solve Lotka's equation numerically for r given German l(x), m(x); compare to the observed growth rate.
2. Build a Leslie matrix; extract λ, the stable age vector, and reproductive value via eigen(); confirm Perron–Frobenius. *Python:* numpy.linalg.eig — trivial for you.
3. Compute Keyfitz momentum: project a population to stationarity after an instantaneous drop to replacement fertility.
**Datasets:** HMD/HFD Germany.
**Estimated time:** 4–5 weeks.

---

### MODULE 7 — Population Projection & Forecasting
**Goals / mastery:** Execute the cohort-component method; build Leslie-matrix projections; run deterministic scenario projections; forecast mortality with Lee–Carter and its major extensions (Lee–Miller; Li–Lee coherent; Hyndman–Ullah functional data; CBD for old age); forecast fertility and migration; run and interpret probabilistic/Bayesian projections (the UN WPP 2015+ methodology); understand the Wittgenstein/IIASA human-capital projections; evaluate forecast uncertainty; state precisely the disagreement over peak world population. **[BRIDGE — load-bearing]** Lee–Carter *is* an SVD/PCA of the log-mortality matrix: log m(x,t) = a(x) + b(x)k(t) + ε, where b(x), k(t) come from the first singular vectors (the original 1992 paper fits the 1933–1987 US death-rate matrix by SVD); you know SVD cold. Bayesian probabilistic projection is Bayesian hierarchical modeling + MCMC — again your home turf.
**Prerequisites:** Modules 3, 4, 6.
**Primary readings:**
- Lee, R.D. & Carter, L.R. (1992), "Modeling and Forecasting U.S. Mortality," *JASA* 87(419):659–671, DOI 10.2307/2290201. PAYWALLED (FREE-DRAFT at pages.stern.nyu.edu).
- Lee, R. & Miller, T. (2001), "Evaluating the performance of the Lee–Carter method," *Demography* 38(4):537–549. PAYWALLED.
- Li, N. & Lee, R. (2005), "Coherent mortality forecasts for a group of populations," *Demography* 42(3):575–594. PAYWALLED.
- Cairns, A., Blake, D. & Dowd, K. (2006), the CBD model, *Journal of Risk and Insurance* 73(4):687–718. PAYWALLED.
- Raftery, A.E., Li, N., Ševčíková, H., Gerland, P. & Heilig, G.K. (2012), "Bayesian probabilistic population projections for all countries," *PNAS* 109(35):13915–13921. FREE (PNAS).
- Gerland, P., Raftery, A.E. et al. (2014), "World population stabilization unlikely this century," *Science* 346(6206):234–237. PAYWALLED.
**Supplementary (the peak-population disagreement — read as a set):**
- Vollset, S.E. et al. (IHME) (2020), "Fertility, mortality, migration, and population scenarios for 195 countries and territories from 2017 to 2100," *The Lancet* 396(10258):1285–1306. The paper reports that "global population was projected to peak in 2064 at 9·73 billion (8·84–10·9) people and decline to 8·79 billion (6·83–11·8) in 2100" (95% uncertainty intervals in parentheses).
- UN DESA, *World Population Prospects 2024, Summary of Results* (11 July 2024): world population is projected as "reaching a peak of around 10.3 billion people in the mid-2080s, up from 8.2 billion in 2024... falling to 10.2 billion people by the end of the century" — i.e., a peak of 10.3 billion in 2084.
- Lutz, W., Butz, W.P. & KC, S. (eds.) (2014), *World Population and Human Capital in the Twenty-First Century*, Oxford UP (IIASA executive summary FREE) — the Wittgenstein Centre education-conditioned projections.
**Hands-on:**
1. Fit Lee–Carter to German mortality with **StMoMo** and with **demography** (Hyndman); forecast e0 to 2050 with intervals. *Python:* implement Lee–Carter via numpy SVD from scratch (recommended — you'll internalize it).
2. Fit a CBD model for ages 60+ with StMoMo; compare.
3. Run a full deterministic cohort-component projection for Germany with a Leslie matrix; then run a probabilistic one with **bayesTFR + bayesLife + bayesPop**; produce probabilistic pyramids.
4. Reproduce the peak-population disagreement: overlay UN WPP 2024, IHME 2020, and Wittgenstein trajectories.
**Datasets:** HMD, HFD, WPP 2024.
**Estimated time:** 7–8 weeks (the heaviest applied module).

---

### MODULE 8 — Population Dynamics & Mathematical Demography
**Goals / mastery:** Master matrix population models (Caswell): sensitivity/elasticity, LTRE, stochastic and density-dependent extensions; build increment-decrement / multistate life tables (working-life, marital-status, healthy-life — Rogers, Schoen); frame demography as Markov chains; understand the two-sex problem; compute formal kinship models (Goodman–Keyfitz–Pullum; Caswell's matrix kinship). **[BRIDGE — load-bearing]** Multistate/increment-decrement demography *is* a finite-state Markov chain (or Markov reward process); the fundamental matrix N=(I−U)^{−1} gives expected time in states — identical to absorbing-Markov-chain theory you know. Caswell's kinship model projects each kin type as a population via the same transition matrices.
**Prerequisites:** Modules 2, 6.
**Primary readings:**
- Caswell, H. (2001), *Matrix Population Models* (2nd ed.), Sinauer. PAYWALLED.
- Keyfitz & Caswell (2005), Ch. on Markov chains and multistate models. PAYWALLED.
- Rogers, A. (1975), multistate/increment-decrement foundations. PAYWALLED.
- Schoen, R. (1988), *Modeling Multigroup Populations*, Plenum. PAYWALLED.
- Goodman, L.A., Keyfitz, N. & Pullum, T.W. (1974), "Family formation and the frequency of various kinship relationships," *Theoretical Population Biology* 5:1–27. PAYWALLED.
- Caswell, H. (2019), "The formal demography of kinship: A matrix formulation," *Demographic Research* 41:679–712. FREE (open access).
**Supplementary:** Caswell's kinship series II–VI (2020–2024, all *Demographic Research*, FREE); Caswell, *Sensitivity Analysis of Matrix Models* (Springer, 2019, open access); Preston et al. Ch. 3 on multiple-state.
**Hands-on:**
1. Build and analyze a Leslie matrix with **popbio**: sensitivities, elasticities, LTRE decomposition.
2. Build a working-life (increment-decrement) table with employed/unemployed/retired states; compute expected working years via the fundamental matrix. *Python:* implement N=(I−U)^{−1} directly.
3. Compute the kinship network of a German "Focal" individual with **DemoKin**; plot expected number of living kin by Focal's age.
**Datasets:** HMD/HFD Germany, popbio built-ins.
**Estimated time:** 6 weeks.

---

### MODULE 9 — The Demographic Transition & Population Theory
**Goals / mastery:** State classical transition theory and its limits; explain what the Princeton project actually overturned; assess Caldwell's wealth-flows theory; evaluate the Second Demographic Transition; understand below-replacement fertility, the low-fertility-trap hypothesis, and pronatalist policy; assess the demographic dividend's conditionality; calibrate Malthus and neo-Malthusianism honestly.
**Prerequisites:** Modules 4, 7.
**Primary readings:**
- Notestein, F. (1945), "Population — The Long View," in Schultz (ed.), *Food for the World*.
- Davis, K. (1945), "The World Demographic Transition," *Annals AAPSS* 237:1–11. PAYWALLED.
- Coale, A.J. & Watkins, S.C. (eds.) (1986), *The Decline of Fertility in Europe*, Princeton UP — the Princeton European Fertility Project summary. PAYWALLED (chapters on Project MUSE/JSTOR).
- Caldwell, J.C. (1976), "Toward a Restatement of Demographic Transition Theory," *Population and Development Review* 2(3/4):321–366. PAYWALLED.
- Lesthaeghe, R. (2014), "The second demographic transition: A concise overview of its development," *PNAS* 111(51):18112–18115. FREE (PNAS).
- Lutz, W., Skirbekk, V. & Testa, M.R. (2006), "The low-fertility trap hypothesis," *Vienna Yearbook of Population Research*. FREE.
**Supplementary:** Kirk, D. (1996), "Demographic Transition Theory," *Population Studies* 50(3):361–387 (the balanced retrospective); Guinnane, T. (2011), "The historical fertility transition: A guide for economists," *Journal of Economic Literature* 49(3):589–614; Brown, J. & Guinnane, T. (1994), "What do we know about the timing of fertility transitions in Europe?" (the methodological critique of the Princeton Ig index).
**Hands-on:**
1. Reproduce the Coale–Trussell M/m fertility indices for European provinces from the Princeton data archive (oprdata.princeton.edu).
2. Plot the German transition (CBR/CDR 1840–present) and annotate stages.
**Datasets:** Princeton EFP archive, HFD, Gapminder.
**Estimated time:** 4 weeks (reading-heavy, light compute).

---

### MODULE 10 — Substantive Social Demography
**Goals / mastery:** Analyze nuptiality and family/household demography; grasp education/human-capital demography (Wittgenstein/Lutz); quantify socioeconomic mortality/health differentials and the SES–health gradient; assess population–environment linkages; understand the reconceptualization of ageing (Sanderson & Scherbov prospective age).
**Prerequisites:** Modules 4, 9.
**Primary readings:**
- Sanderson, W. & Scherbov, S. (2005), "Average remaining lifetimes can increase as human populations age," *Nature* 435:811–813; and (2010), "Remeasuring aging," *Science* 329:1287–1288. PAYWALLED.
- Lutz, W., Butz, W.P. & KC, S. (eds.) (2014), *World Population and Human Capital in the Twenty-First Century*, Oxford UP. PAYWALLED (IIASA exec. summary FREE).
- Hajnal, J. (1965), "European Marriage Patterns in Perspective." PAYWALLED.
**Supplementary:** Marmot, M. (2005), *Status Syndrome* (SES–health gradient, accessible); Preston, S. (1975), "The changing relation between mortality and level of economic development," *Population Studies* 29(2):231–248 (the Preston curve). PAYWALLED.
**Hands-on:**
1. Compute Sanderson–Scherbov prospective old-age dependency ratios for Germany and compare to the conventional OADR.
2. Build household-projection headship rates from German microdata (IPUMS-International / Mikrozensus).
**Datasets:** IPUMS, Wittgenstein Centre Data Explorer, HMD.
**Estimated time:** 4 weeks.

---

### MODULE 11 — Applied & Technical Demography
**Goals / mastery:** Estimate demographic parameters from imperfect/incomplete data — Brass-type indirect methods; child mortality from children-ever-born/children-surviving; orphanhood/widowhood methods; death-distribution methods (Growth Balance; Synthetic Extinct Generations) for adult-mortality/coverage; evaluate and adjust census data; do small-area estimation; understand health and business demography; work fluently with the two compendia.
**Prerequisites:** Modules 2, 3, 4.
**Primary readings:**
- Moultrie, T., Dorrington, R., Hill, A., Hill, K., Timæus, I. & Zaba, B. (eds.) (2013), *Tools for Demographic Estimation*, IUSSP. FREE (demographicestimation.iussp.org).
- United Nations (1983), *Manual X: Indirect Techniques for Demographic Estimation*, ST/ESA/SER.A/81. FREE (UN PDF).
- Preston, S., Coale, A., Trussell, J. & Weinstein, M. (1980), "Estimating the completeness of reporting of adult deaths in populations that are approximately stable," *Population Index* — the Synthetic Extinct Generations method. PAYWALLED.
- Hill, K. (1987), the Growth Balance method literature.
**Supplementary:** Siegel, J.S. & Swanson, D.A. (eds.) (2004), *The Methods and Materials of Demography* (2nd ed.), Elsevier/Academic Press — the applied reference. PAYWALLED. Also Siegel, J. (2002), *Applied Demography* (business/health applications).
**Hands-on:**
1. Estimate child mortality from summary birth histories (Brass) using **DemoTools** (GitHub-only — install via remotes).
2. Apply Growth Balance and Synthetic Extinct Generations to assess death-registration completeness for a country with defective data; use the IUSSP spreadsheets and DemoTools.
3. Detect and correct age-heaping (Whipple/Myers indices) with DemoTools.
**Datasets:** DHS, IPUMS-International census samples, IUSSP worked examples.
**Estimated time:** 6 weeks.

---

### MODULE 12 — Historical Demography
**Goals / mastery:** Perform family reconstitution from parish registers (Henry); understand aggregative back projection, inverse projection, and generalized inverse projection (Wrigley & Schofield; Ronald Lee); reconstruct fertility and mortality regimes of past populations; know the Cambridge Group tradition; state the paleodemography controversies (age estimation, the "nonstationarity" and reference-sample problems).
**Prerequisites:** Modules 2, 6.
**Primary readings:**
- Wrigley, E.A. & Schofield, R.S. (1981), *The Population History of England 1541–1871: A Reconstruction*, Edward Arnold (Cambridge UP paperback 1989, ISBN 9780521356886; with contributions from Ronald Lee and Jim Oeppen). PAYWALLED.
- Henry, L. & Fleury, M. (1956), *Des registres paroissiaux à l'histoire de la population* — family reconstitution foundations. PAYWALLED (French; the method is well summarized in English secondary sources).
- Lee, R.D. (1974), "Estimating series of vital rates and age structures from baptisms and burials: A new technique, with applications to pre-industrial England," *Population Studies* 28(3):495–512 — inverse projection. PAYWALLED.
- Wrigley, E.A., Davies, R.S., Oeppen, J. & Schofield, R.S. (1997), *English Population History from Family Reconstitution 1580–1837*, Cambridge UP. PAYWALLED.
**Supplementary:** Hoppa, R. & Vaupel, J. (eds.) (2002), *Paleodemography: Age Distributions from Skeletal Samples*, Cambridge UP (the controversies). PAYWALLED.
**Hands-on:**
1. Implement a simple inverse-projection engine in R (or Python) that takes baptism/burial series and produces vital rates; test on Wrigley–Schofield published series. *Python:* good linear-algebra/optimization exercise.
2. Reconstitute a small synthetic parish register (or a published extract) and compute age-specific marital fertility.
**Datasets:** Cambridge Group published series; synthetic registers.
**Estimated time:** 5 weeks.

---

### MODULE 13 — Capstone & the Journal Literature
**Goals / mastery:** Deliver a substantial reproducible project; read the current primary literature fluently.
**Prerequisites:** All prior modules (or the Fast-Path).
**Capstone options (pick one, ~8–10 weeks):**
- **A.** Build and forecast a national mortality surface for Germany from HMD: fit Lee–Carter, Li–Lee (coherent with a reference set), and CBD; back-test; quantify uncertainty. Deliver as an R package + reproducible report.
- **B.** A full probabilistic cohort-component projection for Germany with bayesTFR/bayesLife/bayesPop; compare to Destatis and Eurostat official projections; decompose the differences.
- **C.** Decompose German life-expectancy change 1990→present by age and cause (Arriaga + DemoDecomp), with a formal write-up.
**Reading the literature:** Set up alerts for the open-access *Demographic Research* (MPIDR) FREE; and *Demography*, *Population and Development Review*, *Population Studies*, *European Journal of Population* (mostly PAYWALLED — use university/library access; many authors post preprints on SocArXiv/OSF).
**Frankfurt/Germany anchors:** Follow BiB (Wiesbaden) and MPIDR (Rostock) working papers and events; use Destatis and Eurostat data portals; consider the MPIDR summer/short courses and the European Doctoral School of Demography (EDSD).
**Estimated time:** 8–10 weeks.

---

## Dependency Map

```
M0 Orientation
 └─> M1 Rates & Standardization
      └─> M2 Life Table ──────────────┬─> M3 Mortality Modeling
                                       ├─> M4 Fertility
                                       ├─> M6 Stable Pop & Momentum ─> M8 Matrix/Multistate/Kinship
                                       └─> M11 Applied/Indirect Estimation
 M2 + M6 ─> M5 Migration & Spatial
 M3 + M4 + M6 ─> M7 Projection & Forecasting
 M4 + M7 ─> M9 Transition Theory ─> M10 Social Demography
 M2 + M6 ─> M12 Historical Demography
 (all)   ─> M13 Capstone
```
Formal spine (must be sequential): **M0 → M1 → M2 → M6 → M7/M8**. Everything else hangs off M2 and M6.

---

## MVP Fast-Path (compressed methodological spine, ~6–8 months part-time)
For maximum method-per-hour, do only: **M0 → M1 → M2 → M3 (Lee–Carter portion) → M6 → M7 → M8 (matrix + multistate core)**, plus skim M11's *Tools for Demographic Estimation* chapters 1–3.
- Core texts: Wachter (2014) cover-to-cover; Preston et al. (2001) Ch. 1–7; Keyfitz & Caswell (2005) Ch. 2–5; Caswell (2001) Ch. 2–4, 9.
- Core papers: Sharpe–Lotka (1911); Lee–Carter (1992); Keyfitz (1971) momentum; Raftery et al. (2012).
- Deliverable: a from-scratch life table + Leslie projection + Lee–Carter forecast for Germany, in both R and NumPy.
This gives you the whole formal engine and the ability to run mortality forecasts and projections; return for the social/historical/applied breadth later.

---

## Full Arc (the complete ~2–3-year program)
A realistic part-time cadence (8–12 hrs/week):
- **Year 1 (formal backbone):** M0 (1mo), M1 (1mo), M2 (1.5mo), M3 (1.5mo), M4 (1mo), M6 (1.5mo), M7 (2mo). ~10 months.
- **Year 2 (dynamics + theory + applied):** M8 (1.5mo), M5 (1mo), M9 (1mo), M11 (1.5mo), M10 (1mo), M12 (1.5mo). ~8 months.
- **Year 3 (integration):** M13 capstone (2.5mo) + slack, revisiting primary literature, attending an MPIDR/EDSD short course, and optionally a second capstone. ~4–8 months.
Total: ~22–26 months of active study; 2–3 calendar years part-time with buffer.

---

## Calibration Tags on major claims/theories/debates
- **Stable population theory & Lotka's mathematics — SETTLED.** Pure mathematics (renewal theory + Perron–Frobenius); not empirically contestable.
- **The life table & its identities — SETTLED.**
- **Bongaarts proximate-determinants framework (1978) — SETTLED** as a robust accounting identity; the *parameter values* (e.g., contraceptive use-effectiveness) get revised (Stover 1998), but the decomposition is sound.
- **Lee–Carter (1992) — SETTLED workhorse with well-known limitations** (assumes an invariant b(x) age pattern and a roughly constant rate of decline, and can understate uncertainty; hence Li–Lee coherence, CBD for old age, and functional-data extensions).
- **Bayesian probabilistic UN projections (Raftery/Ševčíková/Gerland/Alkema) — increasingly the accepted best practice;** adopted by the UN from WPP 2015. Treat as the current standard, not hype.
- **Classical demographic transition theory — SETTLED as a descriptive generalization, CONTESTED as a predictive/causal theory.** The Princeton European Fertility Project (Coale & Watkins 1986) showed fertility declined across widely varying socioeconomic conditions, undermining strict threshold/modernization causation and boosting diffusion/cultural accounts. Caveat: Brown & Guinnane (1994) argued the Ig index can *miss* the true onset — a methodological qualification on the Princeton timing claims.
- **Second Demographic Transition (Lesthaeghe & van de Kaa) — CONTESTED.** Useful framework for postponement, cohabitation, and sub-replacement fertility in rich countries; its universality and status as a distinct "transition" are disputed.
- **Epidemiologic transition (Omran 1971) — SETTLED-descriptive but revised** (Olshansky–Ault's fourth stage of delayed degenerative disease; later "obesity/re-emergence" critiques; the McKeown debate over the *causes* of mortality decline).
- **Maximum human lifespan & the late-life mortality plateau — OPEN/CONTESTED.** Oeppen & Vaupel (*Science* 2002) is well-established empirically: record female life expectancy has risen linearly since 1840 at ~2.5 years per decade (regression slope ≈ 0.243), which they called possibly "the most remarkable regularity of mass endeavor ever observed." But whether there is a fixed lifespan limit and whether hazards plateau at extreme ages is unresolved. Barbi, Lagona, Marsili, Vaupel & Wachter (*Science* 2018), analyzing 3,836 documented Italians aged 105+ (born 1896–1910, observed 2009–2015), reported: "We observed level hazard curves, which were essentially constant beyond age 105" — implying no hard wall. Against this, Dong, Milholland & Vijg (*Nature* 2016), using International Database on Longevity maximum-reported-age-at-death data (US, France, Japan, UK, 1968–2006), found the maximum age at death plateaued around 1995 at an average maximum human lifespan of ~115 years and argued "the maximum lifespan of humans is fixed and subject to natural constraints." Pointed methodological critiques exist on both sides (e.g., Beltrán-Sánchez, Austad & Finch 2018; Newman 2018).
- **Timing/size of peak world population — OPEN.** The three leading projections differ materially: UN WPP 2024 projects a peak of ~10.3 billion in 2084 (declining to 10.2 billion by 2100); IHME/Vollset 2020 (*The Lancet*) projects a peak of 9.73 billion (95% UI 8.84–10.9) in 2064, declining to 8.79 billion (6.83–11.8) by 2100; the Wittgenstein Centre/IIASA education-conditioned projections fall in between. The divergence is driven mainly by different assumptions about the pace of African fertility decline and education feedbacks.
- **Neo-Malthusian "population bomb" catastrophist predictions — HYPE-WATCH.** Ehrlich-style mass-famine forecasts failed; Malthus's mechanism is real but was overtaken by the demographic and agricultural transitions. Read Malthus as history of thought, not forecasting.
- **The demographic dividend's automaticity — CONTESTED.** The age-structure window is real, but the economic payoff is conditional on policy (education, labor markets, governance), not automatic.
- **The "low-fertility trap" hypothesis (Lutz) — CONTESTED/OPEN.** Plausible self-reinforcing mechanisms proposed; empirical support is mixed and the hypothesis remains debated.

---

## Edition & Access currency (verified)
**Current editions to buy/borrow:**
- Preston, Heuveline & Guillot, *Demography* — **2001, Blackwell/Wiley, still the only edition** (ISBN 9781557864512). PAYWALLED.
- Keyfitz & Caswell, *Applied Mathematical Demography* — **3rd ed., 2005, Springer** (ISBN 9780387225371). PAYWALLED.
- Wachter, *Essential Demographic Methods* — **2014, Harvard UP (1st/only ed.)** (ISBN 9780674045576). PAYWALLED; FREE-DRAFT chapters from Wachter's Berkeley course.
- Caswell, *Matrix Population Models* — **2nd ed., 2001, Sinauer (now an Oxford imprint)** (ISBN 9780878930968). PAYWALLED. (No 3rd edition; Caswell's newer *Sensitivity Analysis of Matrix Models*, Springer 2019, is open access.)
- Rowland, *Demographic Methods and Concepts* — **2003, Oxford UP** (ISBN 9780198752639), with a companion Excel workbook (student CD-ROM). PAYWALLED. Single edition.
- Poston & Bouvier, *Population and Society* — **2nd ed., 2017, Cambridge UP** (ISBN 9781107042674 hbk / 9781107645936 pbk). PAYWALLED.
- Siegel & Swanson (eds.), *The Methods and Materials of Demography* — **2nd ed., 2004, Elsevier/Academic Press** (ISBN 9780126419559). PAYWALLED.
- Hinde, *Demographic Methods* — **1998, Arnold (Routledge reissue)** (ISBN 9780340718926). PAYWALLED.
- Coale, *The Growth and Structure of Human Populations* — **1972, Princeton UP** (Legacy reprint). PAYWALLED.
- Livi-Bacci, *A Concise History of World Population* — **latest edition is the 7th (Wiley-Blackwell, ISBN 9781394295753); the 6th (2017, ISBN 9781119029274) is the prior edition.** PAYWALLED.
- Lutz, Butz & KC (eds.), *World Population and Human Capital in the Twenty-First Century* — **2014, Oxford UP (paperback 2017)** (print ISBN 9780198703167). PAYWALLED; IIASA executive summary FREE (pure.iiasa.ac.at).

**Free/open resources (prioritize these):**
- **Human Mortality Database** (mortality.org) & **Human Fertility Database** (humanfertility.org) — FREE (registration). Co-hosted by MPIDR (Rostock) and UC Berkeley; HMD recently added cause-specific series.
- **IUSSP *Tools for Demographic Estimation*** (2013) — FREE, full text + Excel workbooks at demographicestimation.iussp.org.
- **UN *Manual X*** (1983, ST/ESA/SER.A/81) — FREE UN PDF (un.org/development/desa/pd).
- ***Demographic Research*** (MPIDR) — FREE, open access; the Caswell kinship series lives here.
- **UN World Population Prospects 2024** — FREE data.
- **Wittgenstein Centre Data Explorer** — FREE projections by education.
- **MPIDR** working papers and **BiB** (Wiesbaden) publications — FREE.

**R package status (verified):**
- CRAN: demography (Hyndman), HMDHFDplus (Riffe), StMoMo (Villegas/Millossovich/Kaishev), MortalityLaws (Pascariu), DemoDecomp (Riffe), popbio (Stubben), bayesTFR, bayesLife, bayesPop (Ševčíková & Raftery), DemoKin (Williams & Alburez-Gutierrez).
- **GitHub-only: DemoTools** (`remotes::install_github("timriffe/DemoTools")`), commissioned by the UN Population Division.
- **Archived on CRAN (2020-12-10): MortalitySmooth** (Camarda) — install from the CRAN archive or use P-spline alternatives (mgcv, or 2D smoothing in StMoMo).
- Python note: no full-stack equivalent exists; the demographic R stack is dominant. Use rpy2 to bridge, or reimplement the linear-algebra-heavy methods (life tables, Leslie, Lee–Carter SVD, multistate fundamental matrix, inverse projection) directly in NumPy/SciPy — recommended for internalization. `lifelines` covers survival/hazard basics; `statsmodels` covers the GLM/gravity work.

---

## Recommendations
1. **Start now with the MVP Fast-Path (M0–M2, M6–M8) using Wachter + Preston et al. + Keyfitz–Caswell.** Readiness benchmark to move on: you can build a German life table and a Leslie projection from raw HMD counts, from scratch, in both R and NumPy, and explain why λ=e^r.
2. **Buy the four spine books** (Preston et al.; Keyfitz & Caswell; Wachter; Caswell MPM) and rely on FREE resources (HMD/HFD, *Tools for Demographic Estimation*, *Demographic Research*, Manual X) for everything else. This keeps costs low and primary-source density high — matching your stated preference.
3. **Do every hands-on component twice where feasible — once in R (canonical), once in NumPy** — for the linear-algebra-heavy methods (life table, Leslie/Perron–Frobenius, Lee–Carter SVD, multistate fundamental matrix, inverse projection). This is where your physics/ML background compounds fastest.
4. **Treat the four OPEN/CONTESTED debates as live research, not settled fact** (max lifespan/plateau; peak population; SDT universality; low-fertility trap). In any capstone, present intervals and competing assumptions, not point forecasts.
5. **Use your Frankfurt location:** attend BiB (Wiesbaden) and MPIDR (Rostock) events; apply to an MPIDR short course or the EDSD; use Destatis/Eurostat for a Germany-focused capstone. Your German and Polish are assets for German regional and Central/Eastern European mortality/fertility literatures.
6. **Do NOT re-teach population-genetics migration/structure** (F_ST, admixture) — you have that elsewhere. In Module 5, only build the explicit bridge (net-migration matrix ↔ population-genetics migration matrix; multiregional Leslie ↔ stepping-stone models).
7. **Escalation/adjustment triggers:** if the formal modules feel too easy, compress M0–M2 into 6 weeks and go straight to Caswell's MPM and the kinship series; if applied estimation (M11) feels disconnected from your goals, demote it to reference-only and reallocate time to M7/M8. Re-evaluate scope at the end of Year 1: if forecasting/mortality is where your interest concentrates, drop M9–M12 to skim-level and do two capstones (A and C).

## Caveats
- **Editions move.** Livi-Bacci is now in a newer (7th) edition than the 6th named in the brief; verify the current printing at purchase. The four spine texts (Preston et al. 2001; Keyfitz–Caswell 2005; Wachter 2014; Caswell 2001) have not been superseded as of this writing.
- **Access reality:** most graduate textbooks and the top journals (*Demography*, *PDR*, *Population Studies*, *EJP*) are paywalled; budget for library/university access. *Demographic Research* is the major open-access exception and is genuinely first-rate.
- **Tooling churn:** DemoTools is GitHub-only and MortalitySmooth is CRAN-archived — plan installs accordingly; the rest of the stack is stable on CRAN.
- **Time estimates assume a strong quantitative autodidact** at ~8–12 hrs/week; the social/historical/theory modules are reading-heavy and may run longer if you engage the primary debates deeply.
- **Some foundational sources are non-English** (Henry & Fleury in French; Lesthaeghe & van de Kaa's original 1986 SDT paper in Dutch). English summaries and later restatements (e.g., Lesthaeghe 2014 PNAS) cover the substance; your languages help but are not required for the canon.
- **A few exact page ranges/subtitles for older papers** (e.g., Preston–Coale–Trussell–Weinstein 1980; Hajnal 1965; Notestein 1945; the specific Hill 1987 Growth Balance citation) should be confirmed against the journal of record before formal use; the module texts and IUSSP *Tools for Demographic Estimation* give the authoritative worked versions.