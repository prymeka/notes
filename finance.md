# Finance: A Balanced, Self-Contained Curriculum
### Corporate finance + asset pricing + quantitative finance · intermediate → frontier · theory-forward

**Orientation:** theory-forward and balanced across the three pillars you weighted equally — **corporate finance**, **asset pricing / investments**, and **quantitative finance / derivatives** — with **asset pricing recapped and deepened self-contained** (it does not lean on the macro track, and it adds the full empirical cross-section macro didn't cover). **Behavioral finance is included** (routed here from the behavioral track). **Market microstructure and trading-adjacent material are reserved** for a future trading track, per your choice.

**The unifying spine:** everything in finance flows from a single principle — **no-arbitrage**. The stochastic discount factor and the Fundamental Theorem of Asset Pricing generate all of it; asset pricing, derivatives, and fixed income are one idea in three costumes. And the field's central *unresolved* tension — running from asset pricing through market efficiency to behavioral finance — is whether prices are **right** (Fama) or systematically **wrong** (Shiller).

**Tuned to your background twice over:** the quant core is your physics sweet spot (stochastic calculus is SDEs; Black–Scholes *is* the heat equation; Vasicek *is* Ornstein–Uhlenbeck), and empirical asset pricing is your ML/econometrics sweet spot (the cross-section of returns is supervised learning on returns).

---

## Conventions

- **Calibration tags:** **[SETTLED]** (proven/robust), **[CONTESTED]** (assumptions or interpretation debated), **[HYPE]** (claims outrunning evidence — finance has cautionary tales), **[FRONTIER]** (active).
- **⊘ FREE** marks free resources (Cochrane's course, Damodaran's corporate-finance materials, and many working papers).
- **⚡ Physics/ML bridge:** learning accelerators — finance, especially the quant core, is unusually physics-native; several mappings are exact.
- Each phase has an **MVP fast-path**; the assembled MVP spine is at the end.

---

## Scope decisions (yours)

- **Balanced across all three pillars.** Corporate finance, asset pricing/investments, and quant/derivatives each get real, substantial treatment. (Asset pricing spans more phases only because you asked for a self-contained recap-and-deepen, which adds the empirical cross-section as its own phase — not because it outranks the others.)
- **Asset pricing → self-contained.** The macro track covered consumption-based asset pricing, the SDF, and the puzzles from a *macro* angle. Here it's rebuilt from a *finance* angle, deepened (Hansen–Jagannathan bounds, the full empirical program), and standing alone.
- **Behavioral finance → included** (Phase 11), completing what the behavioral track routed here, and carrying that track's replication discipline.
- **Market microstructure / trading → reserved** for a separate trading track. Order books, execution, market-making, and HFT are *not* here.

Corporate finance is delivered as one dense pillar (Phase 8); it's genuinely large enough to warrant its own multi-phase track, so a **corporate-finance deep dive** is offered in "what's next."

---

## Your background as an accelerator (finance is physics-native)

1. **The SDF = a pricing kernel = a change of measure.** The stochastic discount factor is a Radon–Nikodym derivative; risk-neutral pricing is a measure change (Girsanov). State prices are Green's functions/propagators — pricing a payoff is integrating it against state prices. → Phases 1, 5.
2. **Black–Scholes = the heat equation.** The BS PDE transforms to the heat/diffusion equation by a change of variables; you've solved it. Delta-hedging = constructing a replicating portfolio. → Phase 6.
3. **Itô's lemma = the stochastic chain rule; Feynman–Kac = the PDE↔SDE bridge.** The Itô correction is the drift from quadratic variation (the Laplacian term in a diffusion); Feynman–Kac is the diffusion/path-integral connection straight out of physics. → Phase 5.
4. **Vasicek = Ornstein–Uhlenbeck.** The mean-reverting short-rate model is the OU process you know; affine term-structure models are its tractable exponential-affine solutions. → Phase 7.
5. **Mean-variance = quadratic programming; CAPM beta = a regression coefficient; factor models = PCA/regression.** Portfolio optimization and empirical asset pricing are your optimization and ML toolkits. → Phases 2, 4.
6. **Empirical asset pricing = supervised learning on returns.** The cross-section of expected returns is a prediction problem; Gu–Kelly–Xiu is your ML stack applied to returns, and testing asset-pricing models is the econometrics you just learned. → Phase 4.
7. **Real options = American options = optimal stopping; Merton credit = an option on firm value; risk measures = tail statistics; bank runs = a coordination game.** Recurring cross-links to optimal stopping, options, extreme-value theory, and game theory. → Phases 6–10.

---

## Prerequisites & co-requisites

**Assumed (you have it):** probability, linear algebra, optimization, and basic stochastic processes. The heavier quant math (stochastic calculus) is *built* in Phase 5, not assumed.

**Genuinely new even for a quant:** finance has domain-specific content — accounting and financial statements, institutional/market structure, and the specific no-arbitrage machinery — that ML/physics doesn't cover. Phase 0/1 handle it.

**Co-reqs from other tracks (all optional, since this is self-contained):** the econometrics track (empirical asset pricing in Phase 4 *is* applied econometrics — GMM, Fama–MacBeth, GARCH); the micro track (corporate finance's contracting draws on information economics); the game theory track (bank runs and takeovers are strategic).

---

## Dependency map

```
        Phase 0  Prereqs (incl. finance-specific: accounting, no-arbitrage intuition)
             │
        Phase 1  Foundations: no-arbitrage, state prices & the SDF/FTAP
           /   │   \
   Phase 2   Phase 5   Phase 8
   Portfolio  Stochastic Corporate
   & CAPM/APT calculus    finance
      │          │          │
   Phase 3    Phase 6    Phase 9
   Asset      Derivatives Market efficiency,
   pricing I  & options   banking & intermediation
   (theory)      │
      │       Phase 7
   Phase 4    Fixed income
   Asset      & credit
   pricing II    │
   (empirical)   │
      └──────────┴────► Phase 10  Risk management
                             │
                        Phase 11  Behavioral finance
```

**Reading:** 0→1 is the foundation; the SDF/FTAP in Phase 1 unlocks the three pillars. Asset pricing: 2→3→4. Quant: 5→6→7. Corporate: 8 (draws on 1). Phase 9 (efficiency/banking) draws on asset pricing; Phase 10 (risk) draws on the quant chain (and econometrics); Phase 11 (behavioral finance) draws on asset pricing and efficiency. Fastest balanced route: 0→1→2→3→5→6→8.

---

# PHASE 0 — Prerequisites & Placement
*Light-moderate — finance has domain-specific foundations that are new even to a quant.*

- **Goal:** the finance-specific groundwork ML/physics doesn't provide — time value of money, reading financial statements (for corporate finance), market institutions, and no-arbitrage intuition.
- **Primary:** the early chapters of **Berk & DeMarzo, *Corporate Finance*** (for time value, statements, institutional basics — fast) or **Damodaran's** free online materials.
- **⊘ FREE:** **Aswath Damodaran (NYU)** hosts extensive free corporate-finance and valuation materials; MIT OCW finance.
- **Calibration:** **[SETTLED]** foundations.
- **⚡ bridge:** the math is trivial for you; the *new* content is institutional (what a balance sheet is, how markets are organized).
- **Time:** 2–3 weeks (the accounting/institutional part is the new bit).
- **MVP:** skim the statements/institutional material; skip the math.

---

# PHASE 1 — Foundations: No-Arbitrage, State Prices & the SDF
*The unifying spine of all of finance. Everything else is a special case.*

- **Goal:** the theoretical core from which asset pricing, derivatives, and fixed income all flow — no-arbitrage and the stochastic discount factor.
- **Prerequisites:** Phase 0.
- **Topics:** the **law of one price** and **no-arbitrage**; **state prices / Arrow–Debreu securities**; the **stochastic discount factor (pricing kernel)** and the central pricing equation `p = E[m·x]`; **complete vs. incomplete markets**; **risk-neutral probabilities** and the equivalence to state prices; the **Fundamental Theorem of Asset Pricing** (no arbitrage ⟺ a positive SDF / equivalent martingale measure exists; completeness ⟺ uniqueness); the risk-return tradeoff expressed through the SDF.
- **Primary:** **Cochrane, *Asset Pricing*** (revised ed.) — the SDF-centric bible; the entire book (and this curriculum's spine) is organized around `p = E[mx]`; **Duffie, *Dynamic Asset Pricing Theory*** (the rigorous reference); **Back, *Asset Pricing and Portfolio Choice Theory***.
- **⊘ FREE:** **Cochrane's "Asset Pricing" course** (video lectures + notes, free online).
- **Key original readings:** the FTAP (Harrison–Kreps, Harrison–Pliska); Cochrane's SDF framing.
- **Calibration:** the FTAP and no-arbitrage pricing are **[SETTLED]** — rigorous theorems, the bedrock of the field.
- **⚡ bridge:** the SDF = a pricing kernel / Radon–Nikodym derivative (the change of measure to risk-neutral); state prices = Green's functions (pricing = integrating a payoff against state prices); no-arbitrage = a consistency/conservation condition on prices.
- **Exercises:** derive `p = E[mx]` from a state-price model; show no-arbitrage implies a positive SDF; convert between state prices, the SDF, and risk-neutral probabilities; price a simple asset three equivalent ways.
- **Time:** 4–5 weeks.
- **MVP:** the SDF, `p = E[mx]`, risk-neutral pricing, and the FTAP; this is the phase to internalize deeply — it recurs everywhere.

---

# PHASE 2 — Portfolio Theory, the CAPM & APT
*(Asset pricing/investments pillar.) The workhorse models of investments — and the CAPM's instructive empirical failure.*

- **Goal:** portfolio choice and the classic factor/equilibrium pricing models.
- **Prerequisites:** Phase 1.
- **Topics:** **mean-variance optimization** (Markowitz), the efficient frontier, the two-fund theorem, the tangency portfolio; the **CAPM** (Sharpe–Lintner — the security market line, beta, the SDF derivation); the **APT** (Ross — factor structure, arbitrage pricing); portfolio choice under utility; **performance evaluation** (Sharpe ratio, Jensen's alpha, information ratio); the connection of all of these to the SDF from Phase 1.
- **Primary:** **Cochrane, *Asset Pricing*** (mean-variance and the SDF connection); **Campbell, *Financial Decisions and Markets*** (the excellent modern graduate text — comprehensive); Ingersoll, *Theory of Financial Decision Making*.
- **⊘ FREE:** Cochrane's course; QuantEcon (portfolio optimization in Python).
- **Key original readings:** Markowitz (1952); Sharpe (1964); Ross (1976).
- **Calibration:** mean-variance/Markowitz **[SETTLED]** as normative theory. The **CAPM is [SETTLED as theory but empirically rejected]** — beta alone doesn't explain the cross-section (the anomalies literature, Phase 4); it remains foundational as a benchmark and organizing idea. APT is **[SETTLED]** but its factors are not pinned down by theory.
- **⚡ bridge:** mean-variance = quadratic programming (you know it); the efficient frontier = a Pareto frontier; CAPM beta = a regression coefficient / projection onto the market factor.
- **Exercises:** derive the efficient frontier and tangency portfolio; derive the CAPM from mean-variance and from the SDF; compute and interpret performance measures.
- **Time:** 4–5 weeks.
- **MVP:** mean-variance + the CAPM (both derivations) + APT; defer performance-evaluation depth.

---

# PHASE 3 — Asset Pricing I: Equilibrium Theory & the Puzzles
*(Recap & deepen, self-contained.) The macro track's Phase 7, rebuilt from a finance angle and taken further.*

- **Goal:** consumption-based asset pricing, the great empirical puzzles, and the modeling responses.
- **Prerequisites:** Phase 1 (Phase 2 helpful).
- **Topics:** **consumption-based CAPM (CCAPM)** and the SDF from the representative agent's Euler equation; the **equity premium puzzle** (Mehra–Prescott), the **risk-free-rate puzzle**, the **excess volatility puzzle** (Shiller); the **Hansen–Jagannathan bounds** (the finance-side deepening — a variance bound on the SDF); resolutions: **habit formation** (Campbell–Cochrane), **long-run risk** (Bansal–Yaron), **rare disasters** (Rietz–Barro), **Epstein–Zin** recursive preferences; the **intertemporal CAPM** (Merton ICAPM).
- **Primary:** **Cochrane, *Asset Pricing*** (the definitive treatment); **Campbell, *Financial Decisions and Markets***; the original papers.
- **⊘ FREE:** Cochrane's course.
- **Key original readings:** Mehra–Prescott (1985); Shiller (1981); Hansen–Jagannathan (1991); Campbell–Cochrane (1999); Bansal–Yaron (2004); Barro (2006).
- **Calibration:** the **puzzles are [SETTLED]** (real, robust). The **resolutions are [CONTESTED]** — habits vs. long-run risk vs. disasters each fit some moments, no consensus winner (carrying the macro track's verdict).
- **⚡ bridge:** the Hansen–Jagannathan bound = a lower bound on the SDF's volatility implied by the Sharpe ratio (a variance constraint on the pricing kernel); recursive (Epstein–Zin) preferences = a recursive value function (dynamic programming).
- **Exercises:** derive the CCAPM Euler equation and the equity-premium puzzle magnitude; derive the Hansen–Jagannathan bound and plot it against candidate SDFs; work the mechanism of the Campbell–Cochrane habit model.
- **Time:** 5–6 weeks.
- **MVP:** CCAPM + the equity-premium and Hansen–Jagannathan-bound results + one resolution (habits or long-run risk); defer the full menu.

---

# PHASE 4 — Asset Pricing II: Empirical Asset Pricing & the Cross-Section
*(The finance-angle deepening beyond macro — and your ML/econometrics sweet spot.)*

- **Goal:** the empirical program — explaining and testing the cross-section of returns, and the ML frontier.
- **Prerequisites:** Phases 2–3.
- **Topics:** the **CAPM's empirical failure** and the **cross-section of expected returns**; the **Fama–French** three- and five-factor models; **momentum** (Jegadeesh–Titman, Carhart); the **factor zoo** (Harvey–Liu–Zhu, Hou–Xue–Zhang, and the replication debate — Jensen–Kelly–Pedersen); **testing asset-pricing models** (**Fama–MacBeth** regressions, the **GRS test**, GMM tests of the SDF); **return predictability** (Campbell–Shiller, the dividend-price ratio, and the in-sample-vs-out-of-sample debate — Goyal–Welch vs. Campbell–Thompson); the **ML-in-asset-pricing frontier** (Gu–Kelly–Xiu — deep learning for the cross-section, and the tiny-but-real out-of-sample edge).
- **Primary:** **Cochrane, *Asset Pricing*** (empirical methods); **Bali, Engle & Murray, *Empirical Asset Pricing: The Cross Section of Stock Returns***; **Campbell, *Financial Decisions and Markets***; the factor-zoo and Gu–Kelly–Xiu papers. Python: `pandas`, `statsmodels`, and your own ML stack.
- **⊘ FREE:** Cochrane's course; Kelly's and others' ML-in-finance materials; the factor/ML papers are working papers.
- **Key original readings:** Fama–French (1993, 2015); Jegadeesh–Titman (1993); Harvey–Liu–Zhu (2016); Fama–MacBeth (1973); Gibbons–Ross–Shanken (1989); Goyal–Welch (2008); Gu–Kelly–Xiu (2020).
- **Calibration:** Fama–French **[SETTLED]** as an empirical benchmark; **the factor zoo is [CONTESTED]** (Harvey–Liu–Zhu's t>3 threshold; replication debates — carrying the map's verdict); **return predictability is [CONTESTED]** (in-sample vs. out-of-sample — Goyal–Welch's skepticism); **ML-in-asset-pricing is [FRONTIER]** (genuine but modest, breadth-dependent edges).
- **⚡ bridge (your sweet spot):** the cross-section is supervised learning on returns; factor models = regression/PCA; testing models = the GMM/Fama–MacBeth econometrics you just learned; Gu–Kelly–Xiu = your ML stack applied to returns, with the crucial caveat that the per-stock predictable R² is tiny (the map's datapoint: monthly OOS R² ~0.4% for neural nets).
- **Exercises:** run Fama–MacBeth and the GRS test on portfolio returns; construct Fama–French factors; replicate the small OOS R² of an ML return forecast and see why breadth, not per-stock accuracy, drives the Sharpe ratio.
- **Time:** 6–7 weeks.
- **MVP:** Fama–French + momentum + Fama–MacBeth/GRS testing + the ML-in-AP frontier; defer the predictability debate depth.

---

# PHASE 5 — Stochastic Calculus & Continuous-Time Finance
*(Quant pillar, part 1.) Your physics sweet spot — this will be fast and satisfying.*

- **Goal:** the mathematical machinery of continuous-time finance.
- **Prerequisites:** Phase 1.
- **Topics:** **Brownian motion** and its properties; **Itô's lemma**; **stochastic differential equations**; **martingales** and the martingale representation theorem; **Girsanov's theorem** (change of measure); the **Feynman–Kac formula** (PDE↔SDE); quadratic variation and stochastic integration.
- **Primary:** **Shreve, *Stochastic Calculus for Finance II: Continuous-Time Models*** (the standard — rigorous but accessible); **Björk, *Arbitrage Theory in Continuous Time*** (the standard quant-finance-theory text); **Karatzas & Shreve, *Brownian Motion and Stochastic Calculus*** (the hardcore math reference); Øksendal, *Stochastic Differential Equations*.
- **⊘ FREE:** QuantEcon (stochastic processes in Python); lecture notes.
- **Calibration:** **[SETTLED]** mathematics.
- **⚡ bridge (dense):** Brownian motion = the Wiener process/diffusion (you know it); Itô's lemma = the stochastic chain rule, the extra term being the drift from quadratic variation (the Laplacian in a diffusion); **Feynman–Kac = the diffusion/path-integral connection** — literally from physics; Girsanov = a change of measure on path space (importance sampling / a Radon–Nikodym derivative on paths).
- **Exercises:** apply Itô's lemma to geometric Brownian motion; use Girsanov to change to the risk-neutral measure; use Feynman–Kac to turn a pricing PDE into an expectation and back.
- **Time:** 5–6 weeks (fast given your background, but substantial).
- **MVP:** Brownian motion + Itô + Girsanov + Feynman–Kac; skip the measure-theoretic depth of Karatzas–Shreve.

---

# PHASE 6 — Derivatives & Option Pricing
*(Quant pillar, part 2.) Black–Scholes is the heat equation — and then everything the smile forces you beyond it.*

- **Goal:** option pricing from Black–Scholes through the modern models and numerical methods.
- **Prerequisites:** Phase 5.
- **Topics:** **Black–Scholes–Merton** derived two ways (the **delta-hedging/PDE** approach and the **risk-neutral/martingale** approach — and seeing they agree); the **Greeks**; **implied volatility** and the **volatility smile/skew**; put-call parity; beyond BS: **local volatility** (Dupire), **stochastic volatility** (Heston), **jump-diffusion** (Merton), Lévy processes; **exotic options**; **American options** (optimal stopping, early exercise); **numerical methods** (binomial trees, **Monte Carlo**, **finite-difference/PDE**).
- **Primary:** **Shreve II**; **Björk**; **Hull, *Options, Futures, and Other Derivatives*** (the comprehensive practitioner standard). Python: `QuantLib`, `numpy` for Monte Carlo/PDE.
- **⊘ FREE:** QuantEcon; lecture notes; Hull's companion materials.
- **Key original readings:** Black–Scholes (1973); Merton (1973) option pricing; Heston (1993); Dupire (1994).
- **Calibration:** Black–Scholes is **[SETTLED as the benchmark but its assumptions fail]** — constant volatility and no jumps are violated (the smile is [SETTLED] evidence against BS), which is exactly why stochastic-vol and jump models exist; those extensions are **[SETTLED]**.
- **⚡ bridge:** the **Black–Scholes PDE = the heat equation** (a change of variables you've done); delta-hedging = a dynamic replicating portfolio; Monte Carlo pricing = your simulation skills; the Greeks = sensitivities; American exercise = optimal stopping / dynamic programming.
- **Exercises:** derive Black–Scholes both ways and reconcile them; transform the BS PDE to the heat equation; compute the Greeks; price an American option by a binomial tree and a barrier option by Monte Carlo; recover the smile under Heston.
- **Time:** 6–7 weeks.
- **MVP:** Black–Scholes (both derivations) + the Greeks + the smile + one extension (Heston) + Monte Carlo pricing; defer exotics and PDE methods.

---

# PHASE 7 — Fixed Income & Credit
*(Quant pillar, part 3.) The rates and credit worlds — where Ornstein–Uhlenbeck and Merton's option trick reappear.*

- **Goal:** bond pricing, the term structure, and credit risk.
- **Prerequisites:** Phase 6.
- **Topics:** **bond pricing** and the **yield curve**; **duration and convexity**; **term-structure models** (Vasicek, Cox–Ingersoll–Ross, Hull–White, **Heath–Jarrow–Morton**, affine term-structure models — Duffie–Kan); interest-rate derivatives (caps, floors, swaptions); **credit risk** — structural models (**Merton's model**: equity as a call option on firm assets; KMV), reduced-form/intensity models (Jarrow–Turnbull, Duffie–Singleton); **credit derivatives** (CDS) and credit-portfolio risk (CDOs, correlation).
- **Primary:** **Shreve II** (term structure); **Björk**; **Hull** (fixed income & credit); **Brigo & Mercurio, *Interest Rate Models — Theory and Practice*** (the definitive rates text); **Duffie & Singleton, *Credit Risk***.
- **⊘ FREE:** lecture notes; working papers.
- **Key original readings:** Vasicek (1977); Cox–Ingersoll–Ross (1985); Heath–Jarrow–Morton (1992); Merton (1974) structural credit.
- **Calibration:** term-structure and credit models **[SETTLED]**; the choice of model is **[CONTESTED/model-dependent]**; the **Gaussian-copula approach to CDO correlation is a [HYPE]-turned-cautionary-tale** — its role in the 2008 crisis is the field's starkest example of a model over-trusted.
- **⚡ bridge:** the Vasicek short rate = the Ornstein–Uhlenbeck process (mean-reverting, from physics); affine models = tractable exponential-affine solutions; **Merton's structural credit model = an option on firm value** (equity = a call on assets — the Phase 6 machinery reused); credit correlation = copulas.
- **Exercises:** price a bond under Vasicek and identify the OU structure; derive Merton's structural default probability from option pricing; price a CDS in a reduced-form model.
- **Time:** 5–6 weeks.
- **MVP:** bond pricing + duration/convexity + one short-rate model (Vasicek) + Merton structural credit; defer HJM and credit portfolios.

---

# PHASE 8 — Corporate Finance
*(Corporate pillar — one dense phase; genuinely warrants its own track.) How firms finance and govern themselves.*

- **Goal:** the theory of corporate financial decisions — capital structure, investment, payout, governance, and control.
- **Prerequisites:** Phase 1 (valuation).
- **Topics:** **capital structure** (Modigliani–Miller irrelevance and the frictions that break it: taxes, bankruptcy costs, the **trade-off theory**, the **pecking-order theory** — Myers–Majluf; agency costs of debt and equity); **investment / capital budgeting** (NPV/IRR; **real options** — investment under uncertainty, Dixit–Pindyck); **payout policy** (dividends vs. buybacks; dividend irrelevance and its frictions); **financing and security issuance** (IPOs, SEOs, underpricing); **M&A and corporate control** (takeovers, the market for corporate control); **corporate governance** (agency theory — Jensen–Meckling; free-cash-flow — Jensen; managerial incentives, boards, ownership); **financial contracting** (incomplete contracts and control rights — the bridge to micro information economics and the game-theory track).
- **Primary:** **Tirole, *The Theory of Corporate Finance*** (the definitive graduate text — comprehensive and rigorous; your spine here); **Grinblatt & Titman, *Financial Markets and Corporate Strategy***; **Berk & DeMarzo** (for institutional basics).
- **⊘ FREE:** **Damodaran (NYU)** — extensive free corporate-finance and valuation materials.
- **Key original readings:** Modigliani–Miller (1958); Myers–Majluf (1984); Jensen–Meckling (1976); Jensen (1986); Dixit–Pindyck (1994).
- **Calibration:** **MM irrelevance is [SETTLED]** as the benchmark; the **theories of capital structure (trade-off vs. pecking-order) are [CONTESTED]** — the empirical evidence is mixed with no clean winner; agency theory is **[SETTLED]** as a framework; real options are **[SETTLED]** theory.
- **⚡ bridge:** **real options = American options = optimal stopping** (a project is an option to invest — the Phase 6 machinery again); MM irrelevance = a value-conservation/invariance argument (how you slice the claims doesn't change total value, absent frictions — like a conservation law); capital structure with frictions = constrained optimization.
- **Exercises:** prove MM irrelevance and add taxes/bankruptcy to get the trade-off theory; derive the pecking order from adverse selection (Myers–Majluf); value a project as a real option; work an agency-cost model of debt.
- **Time:** 6–8 weeks (dense — covers a lot).
- **MVP:** MM + trade-off/pecking-order + real options + agency theory; defer M&A and issuance depth.

---

# PHASE 9 — Market Efficiency, Banking & Intermediation
*(Markets & institutions.) The Fama–Shiller debate, and why banks exist and are fragile.*

- **Goal:** the efficient-markets debate and the theory of banking and financial intermediation.
- **Prerequisites:** Phases 2–4.
- **Topics:** **market efficiency (EMH)** — the three forms, the **joint-hypothesis problem**, the **Fama vs. Shiller** debate (recap and deepen from the asset-pricing side), event studies, the evidence; **banking and intermediation** — why banks exist (**delegated monitoring** — Diamond; liquidity provision), **bank runs** (Diamond–Dybvig), maturity transformation, the theory of intermediation, **regulation** (capital requirements, Basel, deposit insurance); **financial crises and systemic risk** (the finance/banking angle; the macro-finance frictions were covered in the macro track).
- **Primary:** **Campbell, *Financial Decisions and Markets*** (efficiency); **Freixas & Rochet, *Microeconomics of Banking*** (the definitive banking-theory text); **Tirole** (intermediation); the EMH-debate papers.
- **⊘ FREE:** working papers; Cochrane's and Shiller's course materials.
- **Key original readings:** Fama (1970, 1991); Shiller (1981); Diamond–Dybvig (1983); Diamond (1984).
- **Calibration:** **the EMH is [CONTESTED]** — the canonical Fama vs. Shiller debate (they shared the 2013 Nobel), and the joint-hypothesis problem means it can't be cleanly tested; the consensus is "mostly efficient with exploitable pockets" (carrying the map's verdict). Diamond–Dybvig and delegated monitoring are **[SETTLED]** theory.
- **⚡ bridge:** **bank runs = a coordination game with multiple equilibria** (the good and run equilibria — a direct game-theory link); the **joint-hypothesis problem = an identification problem** (you can't test efficiency without a model of expected returns — the exact identification spine from the econometrics track).
- **Exercises:** state the joint-hypothesis problem precisely; solve the Diamond–Dybvig model and identify the two equilibria; run an event study.
- **Time:** 4–6 weeks.
- **MVP:** the EMH debate + the joint-hypothesis problem + Diamond–Dybvig; defer regulation depth.

---

# PHASE 10 — Risk Management
*(Markets & institutions.) Measuring tail risk — and the field's cautionary tales about over-trusted models.*

- **Goal:** the quantitative measurement and management of financial risk.
- **Prerequisites:** Phases 5–7 (Phase 4's volatility/econometrics helps).
- **Topics:** **Value-at-Risk (VaR)** and its limitations (non-subadditivity, tail-blindness); **Expected Shortfall / Conditional VaR** (coherent risk measures — Artzner–Delbaen–Eber–Heath; the FRTB shift to ES at 97.5%); market/credit/liquidity/operational/counterparty risk; **volatility modeling for risk** (GARCH — recap from econometrics, EWMA/RiskMetrics, realized and implied vol); **extreme value theory** (tail risk); **copulas** (dependence — and their role in 2008); stress testing and VaR backtesting; regulatory frameworks (Basel).
- **Primary:** **McNeil, Frey & Embrechts, *Quantitative Risk Management: Concepts, Techniques and Tools*** (the definitive QRM text — rigorous); **Hull, *Risk Management and Financial Institutions***; the Artzner et al. coherent-risk-measures paper.
- **⊘ FREE:** lecture notes; the coherent-risk-measures literature.
- **Key original readings:** Artzner–Delbaen–Eber–Heath (1999) coherent risk measures.
- **Calibration:** **VaR is [SETTLED but flawed]** (non-subadditive — it can penalize diversification — and blind to losses beyond the threshold); **Expected Shortfall is [SETTLED as the coherent successor]**, now regulatory-mandated; the **Gaussian copula for CDO correlation is [HYPE]-turned-disaster** (the 2008 story); EVT and copulas are **[SETTLED]** methods.
- **⚡ bridge:** VaR/ES = quantiles/tail expectations of a loss distribution; coherent risk measures = a set of axioms where **subadditivity encodes "diversification helps" (a convexity property)**; EVT = extreme-value distributions (Fréchet/Gumbel/Weibull — tail statistics); copulas = dependence separated from marginals (Sklar's theorem).
- **Exercises:** compute VaR and ES for a portfolio and construct a case where VaR violates subadditivity; verify the coherent-risk-measure axioms for ES; fit a GARCH model for volatility forecasting; fit an EVT tail.
- **Time:** 4–6 weeks.
- **MVP:** VaR vs. ES + coherent-risk axioms + GARCH for risk + the subadditivity example; defer EVT/copula depth.

---

# PHASE 11 — Behavioral Finance
*(Routed here from the behavioral track.) Why mispricing can persist — and the Shiller side of the central debate.*

- **Goal:** the behavioral challenge to efficient markets — limits to arbitrage, investor behavior, and behavioral asset pricing.
- **Prerequisites:** Phases 2–4, 9.
- **Topics:** **limits to arbitrage** (why smart money can't always correct mispricing — Shleifer–Vishny; **noise-trader risk** — De Long–Shleifer–Summers–Waldmann; fundamental risk; implementation costs); **investor behavior** (the **disposition effect** — Odean; overconfidence and excessive trading — Barber–Odean; **extrapolation** — Greenwood–Shleifer; attention and sentiment); **behavioral asset pricing** (investor sentiment and the cross-section — Baker–Wurgler); **bubbles and crashes** (rational vs. behavioral bubbles; Shiller's excess volatility and "irrational exuberance"); the **EMH debate through the behavioral lens** (the Shiller side of Phase 9).
- **Primary:** **Shleifer, *Inefficient Markets: An Introduction to Behavioral Finance*** (the classic intro); **Barberis & Thaler, "A Survey of Behavioral Finance"** (the definitive Handbook survey); the original papers.
- **⊘ FREE:** the survey and most papers circulate freely.
- **Key original readings:** De Long–Shleifer–Summers–Waldmann (1990) noise traders; Shleifer–Vishny (1997) limits of arbitrage; Odean (1998) disposition effect; Baker–Wurgler (2006) sentiment; Greenwood–Shleifer (2014) extrapolation.
- **Calibration:** **limits to arbitrage is [SETTLED]** — a robust, important insight explaining why mispricing persists; specific behavioral effects vary (the disposition effect is **[SETTLED]**, some sentiment effects **[CONTESTED]**); behavioral finance overall is **[SETTLED]** as a field, carrying the **same replication caveats as behavioral economics** — apply the discipline from that track.
- **⚡ bridge:** limits to arbitrage = frictions preventing equilibrium restoration; noise-trader risk = a self-fulfilling risk that deters arbitrageurs (a strategic complementarity — a game-theory flavor); sentiment = a common (mispricing) factor across assets.
- **Exercises:** work the De Long et al. noise-trader model and show how noise-trader risk limits arbitrage; state the Shleifer–Vishny agency argument; connect the excess-volatility puzzle to the behavioral vs. efficient-markets debate.
- **Time:** 4–6 weeks.
- **MVP:** limits to arbitrage (noise-trader risk) + the disposition effect + the behavioral side of the EMH debate; defer sentiment-factor depth.

---

## The MVP fast-path (balanced core, ~5–6 months)

A route keeping all three pillars, skipping Phases 0, 7, 9, and compressing the rest:

1. **Phase 1 MVP** — the SDF, `p = E[mx]`, risk-neutral pricing, the FTAP. *(~4 wk)*
2. **Phase 2 MVP** — mean-variance + CAPM + APT. *(~3 wk)*
3. **Phases 3–4 MVP** — the puzzles + Hansen–Jagannathan + Fama–French/Fama–MacBeth + the ML-in-AP frontier. *(~6 wk)*
4. **Phases 5–6 MVP** — Itô/Girsanov/Feynman–Kac + Black–Scholes (both ways) + the Greeks + the smile + Monte Carlo. *(~7 wk)*
5. **Phase 8 MVP** — MM + trade-off/pecking-order + real options + agency theory. *(~5 wk)*
6. **Phase 10 MVP** — VaR vs. ES + coherent risk + GARCH. *(~3 wk)*

This hits all three pillars — asset pricing (SDF, puzzles, cross-section, ML), quant (stochastic calculus + Black–Scholes), and corporate (capital structure, real options) — plus core risk. It defers fixed income/credit, efficiency/banking, and behavioral finance.

---

## Total timeline

| Route | Pace | Duration |
|---|---|---|
| **Full program** (Phases 0–11) | 8–12 hrs/wk | **~14–18 months** |
| **Balanced MVP** (above) | 8–12 hrs/wk | **~5–6 months** |

The largest track (tied with econometrics), but your background compresses the quant core (Phases 5–6) and the empirical phase (Phase 4). The asset-pricing (2→3→4), quant (5→6→7), and corporate (8) pillars run largely in parallel after Phase 1.

---

## Editions & currency

The canon is stable: **Cochrane (2005), Campbell (2018), Duffie (2001), Shreve (2004), Björk (2019), Hull (11th ed.), Tirole (2006), Freixas–Rochet (2008), McNeil–Frey–Embrechts (2015), Brigo–Mercurio (2006)** — all current standards. **Two areas move fast:** the **ML-in-asset-pricing frontier** (Gu–Kelly–Xiu and successors — track recent journals and SSRN) and the **factor-zoo/replication debate**. Post-2008, credit-correlation and risk-model practice also evolved substantially (the FRTB shift to Expected Shortfall) — use post-crisis editions for risk. Cochrane's free "Asset Pricing" course and Damodaran's free corporate-finance materials are the standout open resources.

---

## What I can build next

- The **trading track** you reserved microstructure for — order books, execution, market-making, algorithmic and high-frequency trading, transaction-cost analysis, and the quant research/backtesting pipeline (the third field from the original map, and the one most directly adjacent to your ML work).
- A **corporate-finance deep dive** — the full multi-phase treatment (capital structure, contracting, governance, M&A, restructuring) that this track compressed into one dense pillar.
- A **quantitative-finance-only deep track** if the derivatives/stochastic-calculus core is your real target (stochastic calculus → exotics → term-structure → numerical methods).
- The **combined economics-and-finance study plan** sequencing all eight tracks into one coherent multi-year program — the natural capstone, now that the tracks deliberately cross-reference each other.
- A **fraud-and-markets applied dossier** — the subset of finance most usable in your work (empirical asset pricing / ML on returns, risk measurement, and the econometrics of market data), mapped to your PayPal context.