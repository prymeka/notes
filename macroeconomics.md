# Macroeconomics: A Theory-Focused Curriculum
### Intermediate foundation → graduate core → research frontier (HANK · macro-finance)

**Orientation:** theory-first. The spine is canonical graduate textbooks plus the original papers; computation (solving/estimating models) is flagged as an *optional* strand throughout, since you chose theory focus. Two caveats to that: (1) the frontier phases (6–7) are *inherently* computational at the research level — you can understand the models, mechanisms, and results analytically, but implementing them requires code, so I mark where that line falls; (2) the payoff of the whole program is calibration — knowing which of macro's claims are settled consensus vs. live disputes vs. marketing.

---

## Conventions

- **Calibration tags** (applied to *substantive claims*, not to math):
  - **[SETTLED]** — mainstream consensus, strong theoretical + empirical support.
  - **[CONTESTED]** — actively debated; no professional consensus; know the antagonists.
  - **[HYPE]** — popular claims that outrun the evidence.
  - **[FRONTIER]** — active research; methods may be settled but conclusions are still forming.
- **Free resources** are marked **⊘ FREE**.
- **Edition currency:** editions below are as of my knowledge (early 2026). Textbook editions move; *verify the latest edition before buying* — this matters most for Blanchard/Jones (frequent revisions) and least for the graduate canon (Acemoglu, Woodford, Cochrane are single-edition or slow-moving).
- **⚡ Physics/ML bridge:** each phase flags where your background collapses the learning curve. This is not decoration — modern macro *is* dynamic optimization, stochastic processes, and (at the frontier) statistical mechanics and information theory wearing economics notation.
- Each phase has an **MVP fast-path** for compression; the assembled MVP spine is at the end.

---

## Your background as an accelerator

You are entering this with a physicist's math and an ML engineer's computational instincts. The five highest-leverage mappings, which recur throughout:

1. **Dynamic optimization = analytical mechanics + optimal control.** The Bellman equation is the discrete-time Hamilton–Jacobi–Bellman equation; the continuous-time Ramsey problem is Euler–Lagrange/Hamiltonian mechanics; the costate is a conjugate momentum; the transversality condition is a boundary condition at infinity; saddle-path stability is stable/unstable manifolds. Dynamic programming and physics' optimal control are *the same subject* (Bellman and Pontryagin were contemporaries). → Phases 2–3.
2. **Heterogeneous-agent macro = many-body statistical mechanics.** You track a *distribution* over agent states, not a representative particle. The stationary wealth distribution is the stationary density of a stochastic process; its evolution is governed by the Kolmogorov Forward (Fokker–Planck) equation — literally the same PDE as in stat mech. HANK's continuous-time formulation is a mean-field game (coupled HJB + Fokker–Planck). → Phase 6.
3. **RBC = a driven, damped oscillator.** Frisch's original "rocking horse" metaphor is exact: a stable linear system hit by stochastic shocks produces persistent cycles via impulse-response propagation. Calibration is moment-matching a model to observables. → Phase 4.
4. **Adaptive learning = stochastic approximation = SGD.** Evans–Honkapohja's learning stability (E-stability) is Robbins–Monro stochastic approximation — the same convergence theory as stochastic gradient descent. → Phase 8.
5. **Rational inattention = information theory.** Sims models attention as a Shannon channel-capacity constraint; the agent optimally allocates bits. Direct information-theoretic mapping. → Phase 8.

---

## Prerequisites & co-requisites

**Math (you have this — confirm, don't study):** constrained optimization (Lagrangian/KKT), difference & differential equations, dynamical systems (phase diagrams, local stability, saddle paths), basic probability & Markov chains, linear algebra (eigenvalues for linear rational-expectations solutions). Real analysis helps for the measure-theoretic rigor in Stokey–Lucas–Prescott but is skippable at first.

**Microeconomics (the real co-requisite):** Intermediate macro (Phase 1) needs only intermediate micro. But **graduate macro from Phase 3 onward assumes graduate micro** — utility/producer theory, intertemporal choice, and general-equilibrium existence. Run **Mas-Colell, Whinston & Green (MWG), *Microeconomic Theory*, Parts I–II** in parallel starting around Phase 2, or use **Jehle & Reny** as a gentler substitute. *I can build a standalone micro curriculum if you want the full treatment — say the word.*

---

## Dependency map

```
        Phase 0 (prereqs/placement — light)
             │
        Phase 1  Intermediate foundation
             │
        Phase 2  Dynamic methods  ◄── (graduate micro co-req begins)
           /   \
   Phase 3      Phase 4
   Growth       Business cycles / RBC
      │            │
      │        Phase 5  New Keynesian & monetary
      │           /   \
      └────► Phase 6    Phase 7
             Heterogeneity/HANK   Macro-finance
                    \        /
                   Phase 8  Frontier debates & empirics (capstone)
```

**Reading of the graph:** 0→1→2 is a strict chain (the toolkit gate). Phase 2 unlocks 3 and 4 in parallel. Phase 4 feeds 5 (NK is RBC + rigidities). Phases 3, 5 feed the two frontier pillars 6 and 7, which can be taken in either order. Phase 8 is the synthesis capstone and assumes 5–7. The **fastest route to a specific frontier** is 0→1→2→4→5→(6 or 7).

---

# PHASE 0 — Prerequisites & Placement
*Light. Mostly confirmation + grabbing the micro you'll need.*

- **Goal:** verify the math toolkit; slot in the intermediate-micro base; skim the "shape" of macro so Phase 1 has a target.
- **Prerequisites:** none beyond your degree.
- **Primary:** self-diagnostic against the math list above. For any rust: **Simon & Blume, *Mathematics for Economists*** (the standard reference, dip in as needed). Intermediate micro base: **Varian, *Intermediate Microeconomics*** (skim fast) or **Nechyba** — you can move at 3–4× normal pace.
- **Supplementary / ⊘ FREE:** **MRU (Marginal Revolution University)** intro macro videos for a zero-cost overview of the vocabulary.
- **Key papers:** none yet.
- **Calibration:** foundational; **[SETTLED]**.
- **⚡ Bridge:** if you can do Lagrangian mechanics and solve a linear ODE system with phase portraits, you already own most of Phase 0.
- **Exercises:** work 5–10 optimization + ODE-stability problems cold to confirm fluency.
- **Time:** 1–3 weeks.
- **MVP:** skip entirely if the math list looks trivial; jump to Phase 1.

---

# PHASE 1 — Intermediate Macro Foundations
*Build macro-specific intuition and the national-accounts vocabulary before the formalism. Worth doing even for a mathematician — this is the "physical picture."*

- **Goal:** master the short-run/medium-run/long-run decomposition, national income accounting, and the core models (IS-LM → modern 3-equation, Solow) in their simplest analytically-tractable form. Meet the big policy debates before they get technical.
- **Prerequisites:** Phase 0.
- **Topics:** national accounts & the saving-investment identity, balance of payments; short run — IS-LM, its modern successor the **three-equation New Keynesian model** (IS + Phillips curve + monetary policy rule) in reduced form, AD-AS; medium run — Phillips curve, Okun's law, the natural rate; **long run — the Solow growth model** (the crown jewel here, and the direct on-ramp to Phase 3); open economy — Mundell-Fleming, exchange-rate regimes; money, inflation, central-bank operations; fiscal policy and debt dynamics.
- **Primary (pick one spine + Carlin-Soskice):**
  - **Charles I. Jones, *Macroeconomics*** (~5th ed.) — modern, growth-forward, sets up the graduate arc best; **or Blanchard, *Macroeconomics*** (~8th ed.) — polished and standard.
  - **Carlin & Soskice, *Macroeconomics: Institutions, Instability, and the Financial System*** (OUP, 2015) — uses the modern 3-equation model *and* takes financial instability seriously, which pre-loads the macro-finance frontier (Phase 7). Strongly recommended as the second text.
- **Supplementary:** **Stephen Williamson, *Macroeconomics*** — a more micro-founded intermediate text that eases the jump to graduate.
- **⊘ FREE:** the Penn World Table and FRED (for any growth-accounting you want to try); MRU.
- **Key original readings:** **Solow (1956), "A Contribution to the Theory of Economic Growth"** — read the actual paper; it's short and beautiful.
- **Calibration:** Solow growth **[SETTLED]** (the organizing framework of long-run macro). IS-LM **[SETTLED as pedagogy / CONTESTED as a literal model]** — superseded by DSGE, but the intuition is load-bearing. The Phillips curve **[CONTESTED]** — its slope, stability, and whether it has "flattened" is a genuinely live post-2020 debate. Mundell-Fleming **[SETTLED as pedagogy]**.
- **⚡ Bridge:** Solow is the fixed-point/steady-state of a nonlinear ODE; convergence to the balanced growth path is relaxation to equilibrium; the capital-accumulation equation is logistic-type dynamics with depreciation. You can derive the entire model's steady state, golden rule, and convergence speed analytically in an afternoon.
- **Exercises:** solve Solow end-to-end (steady state, golden-rule saving, convergence half-life, growth accounting); work the 3-equation model's response to a demand shock; Jones/Blanchard end-of-chapter problems on IS-LM and the Phillips curve.
- **Time:** 6–10 weeks.
- **MVP:** Jones's growth + short-run chapters only (Solow, growth accounting, the 3-equation model); defer open-economy depth and debt dynamics.

---

# PHASE 2 — Dynamic Methods: The Graduate Toolkit
*The gateway. Everything graduate runs through this. Your single biggest math payoff phase — and where your physics background is most decisive.*

- **Goal:** master deterministic and stochastic dynamic optimization, recursive methods, and the solution of linear rational-expectations models.
- **Prerequisites:** Phase 1; begin MWG micro in parallel.
- **Topics:** deterministic dynamic optimization (calculus of variations, optimal control / Pontryagin & the Hamiltonian, the continuous-time Ramsey problem); discrete-time **dynamic programming** (Bellman equation, contraction-mapping/Blackwell sufficient conditions, value & policy iteration, the envelope theorem, Euler equations); **stochastic** DP (Markov processes, stochastic Euler equations, the stochastic growth model); **rational expectations & linear solutions** (log-linearization, Blanchard–Kahn conditions, determinacy, the method of undetermined coefficients, state-space form).
- **Primary:**
  - **Ljungqvist & Sargent, *Recursive Macroeconomic Theory*** (4th ed., MIT Press, 2018) — the graduate methods-plus-models bible; the backbone of Phases 2, 4, 6, 7.
  - **Stokey, Lucas & Prescott, *Recursive Methods in Economic Dynamics*** (1989) — the rigorous mathematical foundation of DP in economics (measure-theoretic; use selectively).
  - **Acemoglu, *Introduction to Modern Economic Growth*** (Princeton, 2008) — its math appendices on dynamical systems and dynamic optimization are superb; also your Phase 3 spine.
- **Supplementary:** **Miao, *Economic Dynamics in Discrete Time*** (2nd ed., MIT, 2020) — clean complement to SLP.
- **⊘ FREE:** **QuantEcon lectures (Sargent & Stachurski, quantecon.org)** — pedagogically world-class on DP and linear RE, even if you don't run the code; **Dirk Krueger's graduate macro notes**; **Eric Sims's (Notre Dame) graduate macro notes**; **Jesús Fernández-Villaverde's slides** (excellent on solving DSGE).
- **Key original readings:** Bellman's principle of optimality (any DP source); Blanchard & Kahn (1980) on solving linear RE models.
- **Calibration:** DP / recursive methods **[SETTLED]** — pure mathematics. But sharply distinguish the *math* from the *behavioral assumption*: **rational expectations as a model of how agents forecast is [CONTESTED]** (it's the standard, but bounded rationality, adaptive learning, and behavioral alternatives are active — see Phase 8). Learn the toolkit as a toolkit, not as a claim about human cognition.
- **⚡ Bridge (the big one):** the Bellman equation ⇄ Hamilton–Jacobi–Bellman; continuous-time Ramsey ⇄ Euler–Lagrange / Hamiltonian mechanics; costate variable ⇄ conjugate momentum; transversality ⇄ boundary condition at infinity; saddle-path stability ⇄ stable manifold of a saddle fixed point; the stochastic Euler equation ⇄ a martingale/optimality condition on a stochastic process. You are re-learning analytical mechanics and optimal control in new notation.
- **Exercises:** solve the deterministic Ramsey model (phase diagram, saddle path, verify transversality); set up and solve the stochastic growth model's Bellman equation; derive the permanent-income hypothesis via DP; log-linearize a simple model and apply Blanchard–Kahn to check determinacy.
- **Time:** 8–12 weeks (the hardest phase; do not rush it — the ROI compounds).
- **MVP:** Ljungqvist–Sargent chapters on DP + the stochastic growth model + Blanchard–Kahn determinacy; skip the measure-theoretic SLP rigor.

---

# PHASE 3 — Growth Theory (the long run, done properly)
*The most self-contained graduate pillar; can run in parallel with Phase 4.*

- **Goal:** the full theory of long-run growth, from optimal growth through endogenous growth to the frontier of why nations differ.
- **Prerequisites:** Phase 2; MWG in parallel.
- **Topics:** **Ramsey–Cass–Koopmans** optimal growth (welfare, the modified golden rule); **Diamond OLG** (dynamic inefficiency, over-accumulation); **endogenous growth** (AK models; Romer's expanding-variety/R&D model; Aghion–Howitt Schumpeterian creative destruction; Lucas human capital); the **semi-endogenous-growth / scale-effects debate** (Jones critique); unified growth theory & the Malthusian escape (Galor); cross-country income differences, development accounting, **misallocation** (Hsieh–Klenow); the institutions vs. geography vs. culture debate on fundamental causes.
- **Primary:**
  - **Acemoglu, *Introduction to Modern Economic Growth*** — the definitive graduate text.
  - **Barro & Sala-i-Martin, *Economic Growth*** (2nd ed., MIT, 2003) — excellent complement, strong on continuous-time technique.
  - **Aghion & Howitt, *The Economics of Growth*** (MIT, 2008) — for the Schumpeterian tradition.
- **Key original readings (the canon — you value primary sources):** Ramsey (1928); Romer (1990) "Endogenous Technological Change"; Lucas (1988) "On the Mechanics of Economic Development"; Aghion–Howitt (1992) creative destruction; Jones (1995) semi-endogenous critique; Hsieh–Klenow (2009) misallocation.
- **Calibration:** neoclassical growth (Solow/Ramsey/OLG) **[SETTLED]**. Endogenous-growth *engines* **[CONTESTED]** — which mechanism (R&D varieties vs. Schumpeterian vs. AK) and whether scale effects exist; the Jones semi-endogenous critique is unresolved. Cross-country growth *empirics* **[CONTESTED]** — the regressions are fragile (Levine–Renelt robustness pessimism; Sala-i-Martin's "two million regressions" is partly a joke about this). Institutions-as-fundamental-cause (Acemoglu–Robinson) vs. geography (Sachs) **[CONTESTED]**.
- **⚡ Bridge:** OLG dynamics ⇄ discrete iterated maps and their fixed-point stability; dynamic inefficiency ⇄ over-accumulation past a turnpike; endogenous growth's non-convexities/increasing returns ⇄ self-sustaining dynamics and threshold behavior.
- **Exercises:** solve Ramsey and Diamond OLG analytically; derive the balanced growth path in Romer's variety model; state and interpret the dynamic-inefficiency condition; derive the development-accounting decomposition.
- **Time:** 6–8 weeks.
- **MVP:** Acemoglu's Ramsey, OLG, and one endogenous-growth model (Romer varieties); skip unified growth theory and the empirics survey.

---

# PHASE 4 — Business Cycles: RBC & the Equilibrium Approach
*The methodological origin of all modern DSGE. Short but pivotal.*

- **Goal:** the real business cycle model and the quantitative-theory revolution it launched (Lucas critique, calibration, micro-founded DSGE) — and an honest accounting of what survived.
- **Prerequisites:** Phase 2.
- **Topics:** the **Lucas critique**; the equilibrium/Frisch–Slutsky view of cycles; the **basic RBC model** (Kydland–Prescott, Long–Plosser); **calibration methodology**; asset pricing inside RBC and the **equity premium puzzle** (Mehra–Prescott — your bridge to Phase 7); RBC's labor-market puzzles (Hansen indivisible labor); the "what does RBC actually explain?" debate.
- **Primary:**
  - **David Romer, *Advanced Macroeconomics*** (5th ed., 2018) — the most readable graduate text; ideal for theory focus. Its RBC and (later) NK chapters are the clearest entry points.
  - **Ljungqvist & Sargent** — RBC chapters for depth.
  - King & Rebelo, "Resuscitating Real Business Cycles" (Handbook of Macroeconomics ch.) — the mature statement.
- **Key original readings:** Lucas (1976) critique; Kydland–Prescott (1982) "Time to Build and Aggregate Fluctuations"; Long–Plosser (1983) "Real Business Cycles"; Mehra–Prescott (1985) "The Equity Premium: A Puzzle."
- **Calibration (an important two-part verdict):** RBC as a **methodology** — micro-founded, calibrated, quantitative DSGE — is **[SETTLED]** and transformative; it *created* modern macro. RBC as an **explanation of cycles** — technology shocks drive recessions, money and demand don't matter — is **[CONTESTED, largely rejected in its pure form]**; the profession moved to New Keynesian models precisely because pure RBC can't generate monetary non-neutrality, involuntary unemployment, or demand-driven recessions. The framework lived; the pure-RBC economics did not.
- **⚡ Bridge:** the Frisch–Slutsky paradigm ⇄ a damped harmonic oscillator driven by noise producing persistent cycles (Frisch's literal "rocking horse"); calibration ⇄ fitting model parameters to match empirical moments (as you'd fit a model to observables); technology shocks + propagation ⇄ stochastic forcing + impulse response.
- **Exercises:** derive and calibrate the basic RBC model; compute the magnitude of the equity-premium puzzle; sketch/interpret the impulse response to a technology shock.
- **Time:** 5–7 weeks.
- **MVP:** Romer's RBC chapter + Kydland–Prescott + the equity-premium puzzle.

---

# PHASE 5 — New Keynesian Economics & Monetary Theory
*The modern mainstream — the model central banks actually use.*

- **Goal:** nominal rigidities, the New Keynesian DSGE model, optimal monetary policy, and the monetary-theory canon.
- **Prerequisites:** Phase 4.
- **Topics:** monopolistic competition (**Dixit–Stiglitz**); price stickiness (**Calvo pricing**, menu costs, Rotemberg); the **New Keynesian Phillips curve**; the **three-equation NK model** and determinacy (the **Taylor principle**); the **effective lower bound**, liquidity traps, and **forward guidance** (and the "forward-guidance puzzle"); **optimal monetary policy**, commitment vs. discretion, **time inconsistency** (Kydland–Prescott 1977; Barro–Gordon); the **fiscal theory of the price level**; **medium-scale DSGE** (Christiano–Eichenbaum–Evans; Smets–Wouters).
- **Primary:**
  - **Jordi Galí, *Monetary Policy, Inflation, and the Business Cycle*** (2nd ed., Princeton, 2015) — *the* definitive, teachable NK text. Your spine here.
  - **Michael Woodford, *Interest and Prices*** (Princeton, 2003) — the monumental theoretical treatise; dense, foundational; read selectively.
  - **Carl Walsh, *Monetary Theory and Policy*** (4th ed., MIT, 2017) — comprehensive reference complement.
- **Key original readings:** Clarida–Galí–Gertler (1999) "The Science of Monetary Policy"; Calvo (1983); Kydland–Prescott (1977) "Rules Rather than Discretion"; Barro–Gordon (1983); Christiano–Eichenbaum–Evans (2005); Smets–Wouters (2007).
- **Calibration:** that **nominal rigidities make monetary policy have real effects** is **[SETTLED]** (strong evidence — the core NK insight, and the empirical vindication of Keynesian intuition on rigorous foundations). The specific **Calvo microfoundation** is **[CONTESTED]** (time-dependent Calvo vs. state-dependent menu costs — Golosov–Lucas vs. Nakamura–Steinsson). The **forward-guidance puzzle** and NK behavior at the ELB are **[CONTESTED]** — their implausible predictions drove the field to HANK (Phase 6). **FTPL [CONTESTED]** (Cochrane vs. mainstream). **Medium-scale DSGE for forecasting/policy [CONTESTED]** post-2008 (see Phase 8). Time-inconsistency/optimal-policy theory **[SETTLED]**.
- **⚡ Bridge:** **Calvo pricing ⇄ a Poisson process** with constant reset hazard (exact); Dixit–Stiglitz aggregation ⇄ CES/power-law aggregation; the log-linearized NK model ⇄ a linear system with forward-looking (jump) and predetermined (state) variables, solved as a boundary-value problem; the Taylor principle / determinacy ⇄ eigenvalue conditions for a unique bounded solution.
- **Exercises:** derive the NK Phillips curve from Calvo pricing; solve the 3-equation model and verify the Taylor principle; work optimal policy under commitment vs. discretion (and see the inflation bias); analyze a liquidity-trap example.
- **Time:** 8–10 weeks.
- **MVP:** Galí chs. 2–5 (basic NK model + optimal policy) + Clarida–Galí–Gertler; defer Woodford and FTPL.

---

# PHASE 6 — Heterogeneity, Incomplete Markets & HANK
*Frontier pillar #1. Beyond the representative agent — where the distribution, not just the average, is the object of study. Your physics background pays its largest dividend here.*

- **Goal:** the incomplete-markets/heterogeneous-agent tradition, from its Bewley–Huggett–Aiyagari foundations to **HANK** (the requested frontier).
- **Prerequisites:** Phases 2, 5.
- **Topics:** **precautionary saving & incomplete markets** (Bewley–Huggett–**Aiyagari** models; idiosyncratic risk + borrowing constraints; the wealth distribution as an equilibrium object); **consumption under uncertainty** (buffer-stock saving — Carroll, Deaton; the **marginal propensity to consume** and why MPC heterogeneity matters); **Krusell–Smith** (aggregate + idiosyncratic risk; "approximate aggregation"); **HANK** — Kaplan–Moll–Violante's "Monetary Policy According to HANK" (the **direct vs. indirect** decomposition of monetary transmission; the death of the representative-agent Euler equation; liquidity and the "wealthy hand-to-mouth"; fiscal multipliers); **two-asset HANK** and intertemporal MPCs; **continuous-time heterogeneous-agent methods** (Achdou–Han–Lasry–Lions–Moll: coupled HJB + Kolmogorov Forward — mean-field games); the **sequence-space Jacobian** solution method (Auclert et al.).
- **Primary:**
  - **Ljungqvist & Sargent** — incomplete-markets/Bewley chapters (your rigorous base).
  - **Heathcote, Storesletten & Violante (2009), "Quantitative Macroeconomics with Heterogeneous Households"** (*Annual Review of Economics*) — the survey.
  - **Kaplan & Violante (2018), "Microeconomic Heterogeneity and Macroeconomic Shocks"** (*JEP*) — the accessible HANK overview; start here.
  - **Kaplan, Moll & Violante (2018), "Monetary Policy According to HANK"** (*AER*) — the landmark.
  - **Achdou, Han, Lasry, Lions & Moll (2022), "Income and Wealth Distribution in Macroeconomics: A Continuous-Time Approach"** (*ReStud*) — the mean-field-games methodology.
- **Key original readings:** Aiyagari (1994); Huggett (1993); Krusell–Smith (1998); Auclert, Bardóczy, Rognlie & Straub (2021) on sequence-space Jacobians.
- **⊘ FREE (excellent):** **Ben Moll's website & lecture notes (benjaminmoll.com)** — the definitive continuous-time/HANK teaching materials, with code if you later want the computational strand.
- **Calibration:** that **MPC heterogeneity and incomplete markets matter for fiscal/monetary transmission** is increasingly **[SETTLED]** (strong micro evidence on MPCs; representative-agent models get transmission channels quantitatively wrong). But **HANK as *the* replacement for RANK is [FRONTIER]** — a very active area; which frictions matter most, and how much HANK actually changes policy conclusions versus RANK, is unsettled. The continuous-time/mean-field-games machinery is a **[SETTLED] method** in **[FRONTIER]** application.
- **⚡ Bridge (the showcase):** the stationary wealth distribution ⇄ the stationary density of a stochastic process; its evolution obeys the **Kolmogorov Forward = Fokker–Planck equation** — *identical* to statistical mechanics; the coupled **HJB + KF system ⇄ mean-field games** (Lasry–Lions), a forward-backward PDE pair deeply tied to optimal transport, where the KF is the adjoint of the linearized HJB; heterogeneous-agent aggregation ⇄ computing moments of a distribution over a state space (many-body → mean field); Krusell–Smith "approximate aggregation" ⇄ a few moments summarizing the field's aggregate effect. **This is the single most physics-native area of macroeconomics.**
- **Exercises (theory-level):** derive the KF equation for a simple income process; characterize an Aiyagari stationary equilibrium; work the direct/indirect decomposition of monetary transmission in HANK; understand the sequence-space Jacobian on a toy example. *(Implementing any of these requires code — optional strand.)*
- **Time:** 8–12 weeks (dense frontier material).
- **MVP:** Kaplan–Violante *JEP* + Kaplan–Moll–Violante *AER* + Aiyagari (1994); own the direct/indirect decomposition; defer continuous-time PDE machinery and sequence-space methods.
- **Note on your theory-focus choice:** this phase is inherently computational to *practice*. I've kept it analytical (models, mechanisms, results). If you later want to *solve* these models, I'll bolt on a computational strand (Moll's codes + QuantEcon's heterogeneous-agent lectures).

---

# PHASE 7 — Macro-Finance
*Frontier pillar #2. Where asset pricing and macro fuse — financial frictions, intermediary asset pricing, and the macroeconomics of crises. Directly connects to your markets interest.*

- **Goal:** integrate consumption-based asset pricing with macro, then layer in financial frictions and the intermediary/continuous-time frontier.
- **Prerequisites:** Phases 4, 5 (Phase 6 helpful, not required).
- **Topics:** consumption-based asset pricing and its **puzzles** (equity premium, risk-free-rate, excess volatility) — the bridge from Phase 4; **resolutions** (habit formation — Campbell–Cochrane; long-run risk — Bansal–Yaron; rare disasters — Rietz/Barro; Epstein–Zin recursive preferences); **financial frictions in macro** (costly state verification / the **financial accelerator** — Bernanke–Gertler–Gilchrist; **collateral constraints** — Kiyotaki–Moore "Credit Cycles"); **intermediary asset pricing** (He–Krishnamurthy; **Brunnermeier–Sannikov** continuous-time — endogenous risk, the volatility paradox, liquidity spirals); banking, runs, and systemic risk (Gertler–Kiyotaki); the **macroprudential** frontier.
- **Primary:**
  - **John Cochrane, *Asset Pricing*** (revised ed., Princeton, 2005) — the definitive text linking asset pricing to macro via the **stochastic discount factor**. Your spine.
  - **Ljungqvist & Sargent** — asset-pricing chapters.
  - Brunnermeier, Eisenbach & Sannikov, "Macroeconomics with Financial Frictions: A Survey" — the map of this literature.
- **Key original readings:** Mehra–Prescott (1985, revisited from Phase 4); Campbell–Cochrane (1999) "By Force of Habit"; Bansal–Yaron (2004) "Risks for the Long Run"; Barro (2006) rare disasters; Kiyotaki–Moore (1997) "Credit Cycles"; Bernanke–Gertler–Gilchrist (1999) financial accelerator; He–Krishnamurthy (2013) "Intermediary Asset Pricing"; Brunnermeier–Sannikov (2014) "A Macroeconomic Model with a Financial Sector."
- **⊘ FREE:** **Perry Mehrling, "Economics of Money and Banking"** (Coursera) — superb institutional intuition for the money/credit view that complements the models; **John Cochrane's course materials & blog**.
- **Calibration:** the consumption-based **puzzles** are **[SETTLED]** (real and robust). The **resolutions** are **[CONTESTED]** — habits vs. long-run risk vs. disasters each fit some moments; no consensus winner. That **financial frictions matter for macro** became **[SETTLED]** post-2008 (the crisis vindicated the Kiyotaki–Moore / BGG literature). **Intermediary / continuous-time macro-finance is [FRONTIER]** — elegant and active, quantitatively young. **Macroprudential policy design [CONTESTED]** (theory ahead of consensus).
- **⚡ Bridge:** the stochastic discount factor ⇄ a change-of-measure / Radon–Nikodym pricing kernel (risk-neutral pricing is a measure change); the Brunnermeier–Sannikov "volatility paradox" and amplification ⇄ nonlinear feedback and instability near a boundary (endogenous-risk amplification is analogous to critical phenomena); long-run risk ⇄ low-frequency variance dominance (1/f-type spectra); rare disasters ⇄ heavy-tailed jump processes / extreme-value theory.
- **Exercises:** derive the SDF and the equity-premium bound (Hansen–Jagannathan); work the mechanism of the Campbell–Cochrane habit model; analyze the financial accelerator's amplification; understand the volatility paradox in Brunnermeier–Sannikov conceptually.
- **Time:** 7–10 weeks.
- **MVP:** Cochrane *Asset Pricing* core (SDF, equity premium, the puzzles) + Kiyotaki–Moore + Bernanke–Gertler–Gilchrist + the Brunnermeier–Sannikov key ideas; defer full continuous-time derivations.

---

# PHASE 8 — The Frontier: Methodological Debates & Empirical Identification
*Capstone / synthesis. The calibration payoff — where macro is genuinely uncertain, what the DSGE fight is really about, and how models meet data.*

- **Goal:** engage the live methodological debates and the empirical toolkit for identifying macro shocks; form your own calibrated view of the field.
- **Prerequisites:** Phases 5–7.
- **Topics:**
  - **The DSGE controversy:** Romer "The Trouble with Macroeconomics" (2016); Blanchard "Do DSGE Models Have a Future?"; the defense (Christiano–Eichenbaum–Trabandt "On DSGE Models," *JEP* 2018); Stiglitz's critique. State of the art vs. marketing.
  - **Empirical macro / identification** (essential even for theory focus — it's how you know which models to believe): structural **VARs** (Sims 1980); **local projections** (Jordà 2005); **narrative identification** (Romer–Romer); **high-frequency identification** of monetary shocks (Gertler–Karadi; Nakamura–Steinsson). Ramey's "Macroeconomic Shocks and Their Propagation" (Handbook) is the synthesis.
  - **Bounded rationality, learning & behavioral macro:** adaptive learning (Evans–Honkapohja); **rational inattention** (Sims); diagnostic expectations (Bordalo–Gennaioli–Shleifer); behavioral NK (Gabaix). The live challenge to rational expectations.
  - **Heterodox schools — an honest, calibrated appraisal:** Post-Keynesian, **MMT**, Austrian. What each claims, where it overlaps with or diverges from the mainstream. On MMT specifically (the map flagged it): the *accounting identities it emphasizes are correct*; its *stronger policy claims* (that a currency-issuing government faces no meaningful financing constraint, only an inflation constraint, and can/should run deficits accordingly) are **[CONTESTED-to-HYPE]** and rejected by most mainstream macroeconomists. Austrian business-cycle theory is **[CONTESTED / largely outside the mainstream]**.
  - **Post-2008 / post-COVID rethinking:** secular stagnation (Summers); r-star; the return of fiscal policy; the 2021–2023 inflation and what it taught (reigniting the Phillips-curve debates from Phase 1).
- **Primary:** the debate essays above; **Ramey (2016)** for identification; **Evans & Honkapohja, *Learning and Expectations in Macroeconomics*** (2001) for the learning formalism; **Mitchell, Wray & Watts, *Macroeconomics*** (the MMT textbook) read *critically alongside* **Mankiw, "A Skeptic's Guide to Modern Monetary Theory."**
- **⊘ FREE:** nearly all the debate papers circulate as NBER/working-paper PDFs; the NBER Macroeconomics Annual; Handbook of Macroeconomics chapters as working papers.
- **Calibration (this phase *is* the map):** the meta-verdict to leave with — macro's **toolkit** (DP, DSGE, incomplete markets, identification) is **[SETTLED]**; its **substantive answers** to the big questions (what causes cycles, how policy transmits, why growth differs) remain genuinely **[CONTESTED]**; and much popular macro discourse (strong-form MMT, Austrian cycle theory, gold-bug/permabear content) is **[HYPE]**.
- **⚡ Bridge:** **adaptive learning ⇄ stochastic approximation (Robbins–Monro) ⇄ SGD convergence** — E-stability is literally the ODE-method stability condition you know from ML; **rational inattention ⇄ Shannon channel capacity** (optimal bit allocation under an information constraint); diagnostic expectations ⇄ an overreaction perturbation to the Kalman filter.
- **Exercises:** reproduce a narrative/high-frequency shock event study conceptually; derive an E-stability condition for a simple learning model; write a short, rigorous critical assessment of one heterodox claim using the mainstream toolkit.
- **Time:** 5–7 weeks.
- **MVP:** Romer + Blanchard DSGE essays + Ramey identification survey + Mankiw-on-MMT; skip the learning-theory formalism.

---

## The MVP fast-path (compressed spine, ~4–6 months)

For a rigorous-but-fast route that reaches both frontiers, do the MVP sub-path of each of these, skipping Phases 0 and 3:

1. **Phase 1 MVP** — Jones's Solow + 3-equation model. *(~3 wk)*
2. **Phase 2 MVP** — Ljungqvist–Sargent DP + stochastic growth + Blanchard–Kahn. *(~5 wk)*
3. **Phase 4 MVP** — Romer's RBC + Kydland–Prescott + equity-premium puzzle. *(~3 wk)*
4. **Phase 5 MVP** — Galí chs. 2–5 + Clarida–Galí–Gertler. *(~4 wk)*
5. **Phase 6 MVP** — Kaplan–Violante *JEP* + Kaplan–Moll–Violante *AER* + Aiyagari. *(~4 wk)*
6. **Phase 7 MVP** — Cochrane's SDF/equity-premium core + Kiyotaki–Moore + BGG. *(~3 wk)*

This sacrifices growth theory (Phase 3), the frontier PDE/continuous-time machinery, and the Phase 8 debates — but gets you to a working command of DSGE, NK monetary theory, HANK, and macro-finance. Growth and the methodological debates can be added afterward as standalone reads.

---

## Total timeline

| Route | Pace | Duration |
|---|---|---|
| **Full program** (Phases 0–8) | 8–12 hrs/wk | **~14–20 months** |
| **MVP spine** (above) | 8–12 hrs/wk | **~4–6 months** |

Phases 3 & 4 can overlap; 6 & 7 can overlap. The math-toolkit gate (Phase 2) is the one place not to compress below the MVP.

---

## Editions & currency (verify before buying)

Graduate canon is stable: **Ljungqvist–Sargent 4th (2018), Galí 2nd (2015), Woodford (2003), Acemoglu (2008), Cochrane revised (2005), Walsh 4th (2017), Barro–Sala-i-Martin 2nd (2003)** — all current as of my knowledge, unlikely to have new editions. **David Romer *Advanced Macro* 5th (2018)** — confirm no 6th. Intermediate texts (**Blanchard, Jones**) revise often — always get the newest. Frontier material lives in **papers, not textbooks**; the HANK/macro-finance literature moves fast, so supplement with recent NBER working papers and check Moll's site for the latest teaching versions.

---

## What I can build next

- A **week-by-week reading schedule** mapping specific chapters/papers to dates against your hrs/week.
- A **problem-set companion** (curated exercises per phase, with the physics-mapped derivations spelled out).
- The **computational strand** — re-activating the code layer for Phases 2, 4, 6, 7 (QuantEcon + Moll + Fernández-Villaverde), in Python.
- A **standalone graduate microeconomics curriculum** to run as the co-requisite.
- A **macro-finance-only deep track** if that frontier pillar is the real priority.