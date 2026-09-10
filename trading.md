# Trading: A Theory-Forward Curriculum
### Market microstructure + execution + the quant research pipeline + strategy families · intermediate → frontier

**Orientation:** theory-forward — the models and principles behind trading (microstructure theory, the mathematics of execution, the statistics of backtesting, the theory of why strategies work), not a build-a-trading-system course. Balanced across the three areas you weighted equally: **market microstructure & execution**, the **systematic/quant research pipeline**, and **strategy families**. **ML-for-trading** is woven throughout and gathered into a capstone (Phase 10). This completes the original map's trilogy: economics, finance, and now trading.

**A note on balance:** theory-forward naturally gives microstructure and execution more phases — they're the part of trading with the most developed theory (Kyle, Glosten–Milgrom, Almgren–Chriss), while strategy families and the alpha pipeline are more survey-and-evidence. That's balance *within a theory-forward lens*.

**The unifying spine, and the through-line of the whole field:** **markets are nearly efficient, so real edge is small, fragile, and mostly illusory — the central discipline is telling genuine signal from overfit noise.** This is exactly where your two backgrounds converge: the econometrics multiple-testing lesson *and* your ML overfitting instincts, pointed at the field that most punishes getting it wrong.

**Calibration is a backbone here, as in behavioral econ.** Trading is saturated with hype — retail "quant gurus," overfit backtests, survivorship bias, ignored costs, and "AI beats the market" marketing. Every phase separates the solid academic core (microstructure theory, optimal execution, documented risk premia) from the contested (why premia persist, HFT's effects) and the hype.

---

## Conventions

- **Calibration tags:** **[SETTLED]** (established theory/robust fact), **[CONTESTED]** (mechanism or interpretation debated), **[HYPE]** (claims outrunning evidence — trading's defining pathology), **[FRONTIER]** (active).
- **⊘ FREE** marks free resources (Lopez de Prado's papers, Bouchaud's group's work, and much of the academic strategy literature).
- **⚡ Physics/ML bridge:** learning accelerators — trading's quant core is unusually physics-native (Bouchaud's group literally does statistical physics of markets) and ML-native (the alpha pipeline is your day job).
- Each phase has an **MVP fast-path**; the assembled MVP spine is at the end.

---

## Scope decisions (yours)

- **Theory-forward.** Models and principles, with implementation engaged *conceptually* (backtesting methodology, execution algorithms as mathematical objects) rather than as an engineering course. Given you code, you can build any of this — the curriculum supplies the theory to build it *correctly*.
- **Balanced across all three** areas, with microstructure/execution weighted more phases (it has the most theory).
- **ML-for-trading woven throughout**, capstoned in Phase 10 — central to modern systematic trading and to your background.
- **Absorbs the microstructure/execution material** reserved out of the finance track.

Not here (finance track): asset pricing theory, the SDF, derivatives pricing, corporate finance — this track *uses* factors and derivatives but doesn't re-derive them.

---

## Your background as an accelerator (trading is physics- and ML-native)

1. **Optimal execution = stochastic optimal control; the market-impact square-root law = a scaling law.** Almgren–Chriss is a mean-variance efficient frontier over trading trajectories; the modern treatment is HJB stochastic control (Cartea–Jaimungal–Penalva). Bouchaud's group treats the whole thing with statistical physics. → Phase 4.
2. **Kyle's model = signal extraction / Bayesian filtering.** The market maker infers the informed trader's private signal from order flow — a filtering problem; Kyle's lambda is the price-impact regression coefficient. → Phase 2.
3. **Statistical arbitrage / mean-reversion = the Ornstein–Uhlenbeck process.** Pairs and cointegration-based stat arb model the spread as mean-reverting OU — the process you know from physics. → Phase 8.
4. **The fundamental law of active management = √N signal-to-noise scaling.** IR = IC × √breadth: independent bets average down noise like √N, so breadth, not per-bet accuracy, drives the information ratio. → Phase 5.
5. **Backtest overfitting = the multiple-comparisons / garden-of-forking-paths problem.** The deflated Sharpe ratio is a multiple-testing correction; purged cross-validation is leakage prevention under serial correlation — your ML overfitting instincts and the econometrics multiple-testing lesson, combined. → Phases 6, 10.
6. **The Kelly criterion = log-growth maximization = information theory.** Kelly's original derivation was information-theoretic; optimal bet sizing is geometric-mean/log-utility maximization; covariance shrinkage (Ledoit–Wolf) is your regularization instinct. → Phase 7.
7. **Optimal market-making (Avellaneda–Stoikov) = stochastic control with inventory state; RL-for-execution = your RL toolkit on a natural sequential problem.** → Phases 9, 10.

---

## Prerequisites & co-requisites

**Assumed (you have it):** stochastic processes, optimization, statistics, dynamic programming / stochastic control basics, and ML. The execution/MM math (HJB stochastic control) is developed as needed.

**Helpful co-reqs (all optional — this is self-contained):** the finance track (factors, derivatives, risk — this track uses them); the econometrics track (time series, cointegration, and the multiple-testing/backtesting statistics are the same discipline); the game theory track (Kyle's model and the HFT arms race are strategic).

**Genuinely new even for a quant:** market structure and institutions (how exchanges, order books, and clearing actually work) — Phase 1.

---

## Dependency map

```
        Phase 0  Prereqs (incl. market structure basics)
             │
        Phase 1  Market structure & institutions (the LOB, order types, regulation)
             │
        ┌────┴─────────────────┬──────────────────┐
   Microstructure          Quant pipeline      Strategy families
   Phase 2  Info & price    Phase 5  Signal /   Phase 8  Momentum, stat arb,
   formation (Kyle,          alpha research      carry, value, vol
   Glosten–Milgrom)          (the fundamental       │
   Phase 3  Inventory,       law)                    │
   liquidity, empirical      Phase 6  Backtesting     │
   Phase 4  Optimal          & overfitting            │
   execution (Almgren–       (the epistemic heart)    │
   Chriss, impact)           Phase 7  Portfolio       │
      │                      construction & Kelly     │
      └──────────┬───────────────┴─────────────────────┘
           Phase 9  Market making & HFT (Avellaneda–Stoikov; the HFT debate)
                             │
                        Phase 10  ML for trading (capstone)
```

**Reading:** 0→1 is the foundation; then the three areas run largely in parallel — microstructure (2→3→4), the quant pipeline (5→6→7), and strategy families (8). Phase 9 (MM/HFT) draws on microstructure and execution; Phase 10 (ML) draws on the quant pipeline and the backtesting discipline. Fastest balanced route: 0→1→2→4→5→6→8.

---

# PHASE 0 — Prerequisites & Placement
*Light-moderate — the new content is institutional, not mathematical.*

- **Goal:** confirm the math/ML toolkit; pick up the basics of how markets are organized.
- **Primary:** the opening chapters of **Harris, *Trading and Exchanges*** (institutional grounding — fast but genuinely new).
- **⊘ FREE:** exchange primers; regulatory overviews (SEC/ESMA).
- **Calibration:** **[SETTLED]** institutional facts (but market structure evolves — see the currency note).
- **⚡ bridge:** the math is yours; the new bit is the institutional vocabulary (order types, the NBBO, clearing).
- **Time:** 2–3 weeks.
- **MVP:** skim the institutional basics; skip the math.

---

# PHASE 1 — Market Structure & Institutions
*How markets actually work — the foundation the theory abstracts from.*

- **Goal:** the institutional reality — venues, order types, the order book, participants, and regulation.
- **Prerequisites:** Phase 0.
- **Topics:** trading venues (**exchanges, ECNs, dark pools, OTC/dealer markets**); **order types**; the **limit order book** and matching (price-time/FIFO priority); market participants (designated market makers, HFTs, institutional, retail); the trading lifecycle (order routing, best execution, clearing, settlement); **regulation** (Reg NMS and the NBBO, MiFID II, tick sizes); **market fragmentation** and its consequences.
- **Primary:** **Harris, *Trading and Exchanges: Market Microstructure for Practitioners*** (the definitive book on how markets work — comprehensive and readable; your spine here); **Foucault, Pagano & Röell, *Market Liquidity*** (the institutions-meets-theory bridge).
- **⊘ FREE:** exchange documentation; Lehalle's market-structure writings.
- **Calibration:** **[SETTLED]** facts, but **market structure changes** (tick-size regimes, venue rules, the move to sub-penny/round-lot reforms) — treat specifics as current-as-of-date.
- **⚡ bridge:** the LOB = a continuous double auction / queueing system; matching = a priority queue (your CS background); fragmentation = a distributed-order-routing problem.
- **Exercises:** trace an order through routing → matching → clearing → settlement; explain how price-time priority and the NBBO interact across fragmented venues.
- **Time:** 3–4 weeks.
- **MVP:** the LOB + order types + Reg NMS/NBBO + venue types; defer clearing/settlement depth.

---

# PHASE 2 — Microstructure Theory I: Information & Price Formation
*(Microstructure pillar.) The theoretical heart — how prices come to reflect information.*

- **Goal:** the information-based theory of price formation and the bid-ask spread.
- **Prerequisites:** Phase 1.
- **Topics:** **price formation and price discovery**; the **Glosten–Milgrom** sequential-trade model (the spread as compensation for adverse selection against informed traders); **Kyle's model** (the strategic informed trader; market depth; **Kyle's lambda** as price impact; how quickly prices become informative); the **bid-ask spread** and its decomposition into order-processing, inventory, and **adverse-selection** components (Glosten–Harris, Huang–Stoll); order flow and adverse selection.
- **Primary:** **O'Hara, *Market Microstructure Theory*** (the definitive theory text); **Foucault, Pagano & Röell, *Market Liquidity***; Hasbrouck (for the empirical bridge).
- **⊘ FREE:** the Kyle (1985) and Glosten–Milgrom (1985) papers; lecture notes.
- **Key original readings:** Kyle (1985) "Continuous Auctions and Insider Trading"; Glosten–Milgrom (1985); Glosten–Harris (1988).
- **Calibration:** Kyle and Glosten–Milgrom are **[SETTLED]** canonical theory — foundational and elegant; their empirical fit is reasonable but stylized. The adverse-selection component of spreads is **[SETTLED]**.
- **⚡ bridge:** **Kyle's model = a signal-extraction / Bayesian-filtering problem** — the market maker infers the informed trader's signal from aggregate order flow (your filtering wheelhouse); **Kyle's lambda = the price-impact coefficient** (a regression of price change on signed order flow); adverse selection = separating informed from uninformed order flow (a type-inference problem).
- **Exercises:** solve Glosten–Milgrom for the bid and ask; solve Kyle's model for lambda and the informed trader's optimal strategy; decompose an empirical spread into its three components.
- **Time:** 5–6 weeks.
- **MVP:** Glosten–Milgrom + Kyle (lambda, the informed trader) + spread decomposition; this is the theory to internalize.

---

# PHASE 3 — Microstructure Theory II: Inventory, Liquidity & Empirical Microstructure
*(Microstructure pillar.) The market-maker's inventory problem, the anatomy of liquidity, and how to measure it all.*

- **Goal:** inventory-based models, the theory and measurement of liquidity, and the empirical microstructure toolkit.
- **Prerequisites:** Phase 2.
- **Topics:** **inventory models** (Garman; Amihud–Mendelson; **Ho–Stoll**; Stoll — the market maker's inventory-risk management and its effect on quotes); **liquidity** (its dimensions — tightness, depth, resiliency; measures — the **Amihud illiquidity ratio**, effective/realized spreads, price impact; the **pricing of liquidity risk** — Pastor–Stambaugh, Acharya–Pedersen liquidity-adjusted CAPM); **order-flow toxicity** (**VPIN** — Easley–Lopez de Prado–O'Hara); **empirical market microstructure** (**Hasbrouck's** VAR of trades and quotes; information shares; price-impact estimation; the Roll spread estimator); **high-frequency data properties** (microstructure noise, realized volatility and the signature plot, the Epps effect, the bid-ask bounce).
- **Primary:** **O'Hara**; **Hasbrouck, *Empirical Market Microstructure***; **Foucault, Pagano & Röell**; Aït-Sahalia & Jacod, *High-Frequency Financial Econometrics* (for the HF-econometrics depth).
- **⊘ FREE:** the liquidity and VPIN papers; Hasbrouck's teaching materials.
- **Key original readings:** Ho–Stoll (1981); Amihud (2002) illiquidity; Pastor–Stambaugh (2003); Hasbrouck (1991, 1995); Roll (1984).
- **Calibration:** inventory models **[SETTLED]**; liquidity measurement **[SETTLED]** but with many competing measures; **VPIN is [CONTESTED]** (its flash-crash-prediction claims are disputed); microstructure-noise/realized-vol theory **[SETTLED]**.
- **⚡ bridge:** microstructure noise = measurement noise on the latent efficient price (a signal+noise decomposition); realized volatility = quadratic-variation estimation from HF data; the Epps effect = correlation attenuation from asynchronous high-frequency sampling (a sampling artifact); the Amihud measure = a price-impact-per-volume ratio.
- **Exercises:** solve a Ho–Stoll inventory model; compute the Amihud illiquidity measure and the Roll estimator on data; explain the realized-volatility signature plot via microstructure noise.
- **Time:** 5–6 weeks.
- **MVP:** inventory models + liquidity measures + Hasbrouck's approach + microstructure noise; defer VPIN and liquidity-adjusted CAPM.

---

# PHASE 4 — Optimal Execution
*(Microstructure/execution pillar — your physics sweet spot.) The mathematics of trading a large order without moving the market against yourself.*

- **Goal:** the theory of optimal trade execution — impact models, the efficient frontier of execution, and the stochastic-control formulation.
- **Prerequisites:** Phases 2–3.
- **Topics:** the **execution problem** (minimize expected cost plus risk when liquidating a large position); **market-impact models** (temporary vs. permanent impact; the **square-root law** of impact; propagator/transient-impact models — Bouchaud); the **Almgren–Chriss** framework (the efficient frontier of execution; optimal trading trajectories; the closed-form solution); LOB-based execution (Bertsimas–Lo; **Obizhaeva–Wang** — execution with order-book resilience); **algorithmic execution** (VWAP, TWAP, implementation shortfall, POV); **transaction cost analysis (TCA)**; **execution as stochastic control / RL** (the Cartea–Jaimungal–Penalva HJB framework; RL for execution).
- **Primary:** **Cartea, Jaimungal & Penalva, *Algorithmic and High-Frequency Trading*** (the definitive modern stochastic-control text — ideal for theory-forward + your math); **Bouchaud, Bonart, Donier & Gould, *Trades, Quotes and Prices: Financial Markets Under the Microscope*** (the statistical-physics-of-markets book — Bouchaud is a physicist; tailor-made for you); Almgren–Chriss (2000) original; Guéant, *The Financial Mathematics of Market Liquidity*.
- **⊘ FREE:** the Almgren–Chriss paper; Bouchaud's group's papers on impact (many free on arXiv); Lehalle's execution notes.
- **Key original readings:** Almgren–Chriss (2000); the square-root impact law (Bouchaud et al.; Torre/BARRA); Obizhaeva–Wang (2013).
- **Calibration:** Almgren–Chriss is **[SETTLED]** as the canonical framework; the **square-root law of impact is [SETTLED]** — one of the most robust empirical regularities in all of trading; propagator models are **[SETTLED/FRONTIER]**.
- **⚡ bridge (physics-native):** optimal execution = stochastic optimal control (HJB — you've seen it); Almgren–Chriss = a mean-variance efficient frontier over trajectories; **the square-root impact law = a scaling law** (Bouchaud's group derives it with statistical-physics arguments); execution = RL (a sequential decision problem — your toolkit). This phase is where a physicist feels most at home in trading.
- **Exercises:** derive the Almgren–Chriss optimal trajectory and its efficient frontier; verify the square-root impact law on data; set up execution as an HJB problem and sketch the RL formulation.
- **Time:** 6–7 weeks (fast given your control/RL background).
- **MVP:** the impact models (incl. the square-root law) + Almgren–Chriss + the stochastic-control framing; defer propagator models and LOB-resilience execution.

---

# PHASE 5 — Signal Research & the Alpha Pipeline
*(Quant-pipeline pillar — your ML-adjacent core.) What a predictive signal is, and the theory of active management.*

- **Goal:** the systematic search for predictive signals and the framework that governs how they translate into performance.
- **Prerequisites:** Phase 1 (independent of the microstructure branch).
- **Topics:** **alpha/signal research** (what a signal is; feature engineering under noise and non-stationarity; the brutal signal-to-noise reality of returns); **factor models and factor investing** (the canonical risk premia — value, momentum, carry, quality, low-vol, size; cross-sectional vs. time-series; the factor zoo and its replication problems — recap from finance); **signal combination** (aggregating weak signals); the **fundamental law of active management** (Grinold–Kahn: **IR = IC × √breadth** — the central identity of quant investing); the theory of active portfolio management.
- **Primary:** **Grinold & Kahn, *Active Portfolio Management*** (the classic — the fundamental law, IC, breadth); **Isichenko, *Quantitative Portfolio Management*** (excellent modern practitioner-theorist); Qian–Hua–Sorensen, *Quantitative Equity Portfolio Management*.
- **⊘ FREE:** the factor papers; Kakushadze's "101 Formulaic Alphas" (free — read *critically*, as an illustration of the overfitting problem, not a recipe).
- **Key original readings:** Grinold (1989) fundamental law; the factor-zoo papers (recap).
- **Calibration:** the fundamental law is **[SETTLED]** as a framework; specific factors are **[CONTESTED]** (the factor zoo, recap); **signal research is inherently [CONTESTED/HYPE-prone]** — most candidate "signals" are noise or overfitting, which is exactly why Phase 6 exists.
- **⚡ bridge:** signal research = feature engineering / supervised learning (your job) — but with far worse SNR and non-stationarity than typical ML; **the fundamental law (IR = IC × √breadth) = a √N signal-to-noise scaling** (independent bets average down noise); factor models = regression/PCA.
- **Exercises:** derive the fundamental law and interpret breadth as independent bets; construct and evaluate a simple cross-sectional signal's IC; show how signal decay interacts with turnover.
- **Time:** 5–6 weeks.
- **MVP:** the fundamental law + factor/risk-premia overview + signal-combination basics; defer the deep factor-zoo recap.

---

# PHASE 6 — Backtesting, Overfitting & the Statistics of Strategy Evaluation
*(Quant-pipeline pillar — the epistemic heart. The single most important phase.)*

- **Goal:** the discipline that separates real edge from overfit noise — the pitfalls of backtesting and the statistics of honest strategy evaluation.
- **Prerequisites:** Phase 5.
- **Topics:** the **backtesting problem** and its pitfalls (**look-ahead bias**, **survivorship bias**, **data snooping / multiple testing**, **overfitting**); the **statistics of Sharpe ratios** (Sharpe uncertainty; the **deflated Sharpe ratio** — Bailey–Lopez de Prado); **backtest overfitting** (the **probability of backtest overfitting** — Bailey–Borwein–Lopez de Prado–Zhu; "pseudo-mathematics and financial charlatanism"); **multiple-testing corrections** (White's **reality check**, Hansen's SPA test, Harvey–Liu–Zhu for factors — recap); **cross-validation for financial time series** (why standard CV leaks under serial correlation; **purged and embargoed CV** — Lopez de Prado); walk-forward analysis; the gulf between in-sample fit and out-of-sample reality.
- **Primary:** **Lopez de Prado, *Advances in Financial Machine Learning*** (the essential text on financial-ML pitfalls — purged CV, backtest overfitting, meta-labeling; directly your-background-relevant); the Bailey–Borwein–Lopez de Prado–Zhu papers; Harvey–Liu on multiple testing.
- **⊘ FREE:** **Lopez de Prado's papers** (SSRN — "The Probability of Backtest Overfitting," "Pseudo-Mathematics and Financial Charlatanism," and the purged-CV material) are free and essential.
- **Key original readings:** Bailey–Borwein–Lopez de Prado–Zhu (2014); White (2000) reality check; Harvey–Liu multiple testing.
- **Calibration (this phase *is* the calibration engine):** backtest overfitting is a **[SETTLED]** pervasive problem; the deflated Sharpe and PBO are **[SETTLED]** methods; the meta-lesson — **most published and virtually all marketed strategies are overfit** — is **[SETTLED]** among rigorous quants; **retail backtesting is the field's single largest source of [HYPE] and junk**. Assign the tags by asking: out-of-sample? realistic costs? corrected for the number of trials?
- **⚡ bridge:** backtest overfitting = the multiple-comparisons / garden-of-forking-paths problem (the econometrics-track lesson) plus your ML overfitting instincts; **purged CV = preventing data leakage across serially-correlated samples** (a leakage problem you know); the deflated Sharpe = a multiple-testing correction on the maximum observed Sharpe. This phase leans directly on your two strongest priors.
- **Exercises:** simulate backtest overfitting and compute the PBO; deflate a Sharpe ratio for the number of trials; build a purged-and-embargoed CV split and show why naive CV leaks; run White's reality check on a set of strategies.
- **Time:** 5–6 weeks.
- **MVP:** the pitfalls + the deflated Sharpe / PBO + purged CV + realistic costs. **Keep this in any MVP** — it's what makes everything else trustworthy.

---

# PHASE 7 — Portfolio Construction & Bet Sizing
*(Quant-pipeline pillar.) From signals to positions — and how much to bet.*

- **Goal:** translating forecasts into a portfolio, and the theory of optimal position sizing and risk.
- **Prerequisites:** Phases 5–6.
- **Topics:** **portfolio construction** (from alphas to positions; mean-variance revisited with **estimation error** — "Markowitz, the enemy of itself"; **shrinkage** — Ledoit–Wolf; Black–Litterman; robust optimization); **risk parity** and risk-based allocation; the **Kelly criterion** and growth-optimal betting (optimal leverage, fractional Kelly, the Kelly-vs-mean-variance link — Thorp); **position sizing and leverage**; **turnover- and cost-aware optimization** (alpha decays with turnover; net-of-cost optimization); **drawdown and tail-risk control for trading books** (real-time risk, limits — with VaR/ES depth referenced from the finance track).
- **Primary:** **Grinold & Kahn** (portfolio construction); **Isichenko**; MacLean–Thorp–Ziemba, *The Kelly Capital Growth Investment Criterion*; Ledoit–Wolf shrinkage papers.
- **⊘ FREE:** the Kelly and shrinkage literature; Thorp's writings.
- **Key original readings:** Kelly (1956) (the information-theoretic origin); Ledoit–Wolf (2004) shrinkage.
- **Calibration:** mean-variance is **[SETTLED]** theory but **estimation-error-fragile** (tiny input errors → wild weights); shrinkage/robust methods are **[SETTLED]** improvements; **Kelly is [SETTLED]** theory but full Kelly is aggressive — practitioners use fractional Kelly; **risk parity is [CONTESTED]** (popular, but critiqued for its leverage and bond-heavy tilt).
- **⚡ bridge:** portfolio optimization = QP with estimation error, where shrinkage/robustness = your regularization instinct; **Kelly = log-growth maximization = information theory** (Kelly's original derivation); covariance shrinkage (Ledoit–Wolf) = regularized covariance estimation.
- **Exercises:** show how estimation error destabilizes mean-variance weights and how shrinkage fixes it; derive the Kelly fraction and the fractional-Kelly tradeoff; build a cost-aware optimizer and show the turnover/alpha tradeoff.
- **Time:** 4–6 weeks.
- **MVP:** mean-variance-with-shrinkage + Kelly/fractional-Kelly + cost-aware sizing; defer Black–Litterman and risk parity.

---

# PHASE 8 — Strategy Families
*(Strategy-families pillar.) What works, why it might work, and whether it will keep working.*

- **Goal:** the canonical systematic strategies, the evidence behind each, and the honest debate over why they persist.
- **Prerequisites:** Phases 5–7.
- **Topics:** **trend-following / momentum** (time-series momentum — Moskowitz–Ooi–Pedersen; cross-sectional — Jegadeesh–Titman; CTAs; the behavioral-underreaction-vs-risk debate over *why*); **mean-reversion / statistical arbitrage** (pairs trading — Gatev–Goetzmann–Rouwenhorst; cointegration-based; the OU framing; factor-neutral/PCA stat arb — Avellaneda–Lee); **carry** (FX, rates, and vol carry — Koijen–Moskowitz–Pedersen–Vrugt, "Carry"); **value** across asset classes; **volatility trading** (the variance risk premium; systematic options selling; vol arbitrage); **event-driven & arbitrage** (merger arb, index/ETF arb); and the organizing frame — every systematic strategy collects one of four **risk premia / "payments"**: **immediacy** (market making), **convergence** (stat arb/relative value), **risk transfer** (factors/carry/vol selling), or **convexity** (options/tail hedging).
- **Primary:** **Ilmanen, *Expected Returns: An Investor's Guide to Harvesting Market Rewards*** (the definitive book on risk premia across strategies); **Isichenko** (stat arb); the academic papers; Chan, *Algorithmic Trading* (practitioner strategy taxonomy — read critically).
- **⊘ FREE:** the academic strategy papers (Moskowitz–Ooi–Pedersen, Koijen et al., Gatev et al.) circulate as working papers.
- **Key original readings:** Jegadeesh–Titman (1993); Moskowitz–Ooi–Pedersen (2012); Koijen–Moskowitz–Pedersen–Vrugt (2018); Gatev–Goetzmann–Rouwenhorst (2006); McLean–Pontiff (2016) on post-publication decay.
- **Calibration:** the major risk premia (momentum, carry, value) are **[SETTLED]** as documented but **[CONTESTED]** as to *why* they persist (behavioral vs. risk) and *whether they'll continue* — anomalies decay ~one-third post-publication (McLean–Pontiff); **stat arb is [SETTLED] as a class but crowded and decaying**; retail strategy content is **[HYPE]**-heavy.
- **⚡ bridge:** **stat arb / mean-reversion = Ornstein–Uhlenbeck** (the spread as a mean-reverting process — physics); pairs/cointegration = the econometrics-track cointegration; momentum = time-series/cross-sectional autocorrelation; the risk-premia frame = compensation for bearing systematic factor risk.
- **Exercises:** implement a cointegration-based pairs trade and identify the OU parameters; document time-series momentum across asset classes; classify five strategies by which of the four "payments" they collect.
- **Time:** 5–7 weeks.
- **MVP:** momentum + stat arb (OU/cointegration) + carry + the four-payments frame; defer vol trading and event-driven.

---

# PHASE 9 — Market Making & High-Frequency Trading
*(Microstructure/strategy crossover — theory-forward.) The speed game and the model that governs it.*

- **Goal:** the theory of optimal market making and an evidence-based view of high-frequency trading.
- **Prerequisites:** Phases 2–4.
- **Topics:** **optimal market making** (the **Avellaneda–Stoikov** model — inventory risk, optimal bid-ask quotes, the reservation price; Guéant–Lehalle–Fernandez–Tapia extensions); **HFT strategies** (market making, latency/statistical arbitrage, order anticipation); the **microstructure of HFT** (latency, co-location, the order-book dynamics HFTs exploit); the **HFT debate** (liquidity provision vs. predatory trading; the **2010 Flash Crash**; the academic evidence — Brogaard–Hendershott–Riordan, Menkveld; **Budish–Cramton–Shim's "The High-Frequency Trading Arms Race"** and the frequent-batch-auction proposal).
- **Primary:** **Cartea, Jaimungal & Penalva** (the definitive treatment — Avellaneda–Stoikov and stochastic-control MM); Avellaneda–Stoikov (2008) original; the HFT-debate papers.
- **⊘ FREE:** Avellaneda–Stoikov and the Budish–Cramton–Shim paper are freely available.
- **Key original readings:** Avellaneda–Stoikov (2008); Budish–Cramton–Shim (2015); Menkveld (2013).
- **Calibration:** Avellaneda–Stoikov is **[SETTLED]** as the canonical MM model; **the HFT debate is [CONTESTED]** — liquidity provision vs. predation is genuinely unresolved, and the evidence is mixed; the Budish–Cramton–Shim arms-race critique is influential but its **[CONTESTED]** policy proposal (batch auctions) is not adopted.
- **⚡ bridge:** **optimal MM = stochastic control with inventory as a state variable** (HJB — your control background); the reservation price = an inventory-skewed mid-quote; market making = a natural **RL** problem (sequential quoting under inventory risk — your toolkit).
- **Exercises:** derive the Avellaneda–Stoikov optimal quotes and the reservation price; explain the batch-auction proposal and the arms-race logic; summarize the evidence on HFT and price discovery.
- **Time:** 5–6 weeks.
- **MVP:** Avellaneda–Stoikov + the HFT debate + Budish–Cramton–Shim; defer the extensions.

---

# PHASE 10 — ML for Trading
*(Capstone — your home turf.) Using machine learning for trading, done with the discipline the field demands.*

- **Goal:** the promise and the specific perils of ML in trading, and the toolkit that makes it honest.
- **Prerequisites:** Phases 5–6 (the pipeline and the backtesting discipline).
- **Topics:** **ML for alpha/signals** (the promise and the pitfalls — overfitting, non-stationarity, regime change, and the low SNR that makes naive ML fail); **Lopez de Prado's financial-ML toolkit** (recap and deepen: **purged/embargoed cross-validation**, **meta-labeling**, sample weights by uniqueness, **fractional differentiation** for the memory-vs-stationarity tradeoff, structural-break detection, financial feature importance); **RL for execution and market-making** (a natural fit for sequential trading decisions — and its challenges: sample efficiency, sim-to-real, non-stationarity); **deep learning for the cross-section** (Gu–Kelly–Xiu — recap from finance; the modest OOS edge); the **realistic assessment** (ML adds genuine but modest, breadth-dependent value; the winners use it as one disciplined tool, not a magic box).
- **Primary:** **Lopez de Prado, *Advances in Financial Machine Learning*** (recap/deepen from Phase 6 — the definitive text); **Lopez de Prado, *Machine Learning for Asset Managers*** (shorter, focused); **Dixon, Halperin & Bilokon, *Machine Learning in Finance: From Theory to Practice*** (comprehensive, incl. RL); the Gu–Kelly–Xiu paper.
- **⊘ FREE:** Lopez de Prado's papers; the Gu–Kelly–Xiu working paper; the RL-for-trading literature (arXiv).
- **Key original readings:** Gu–Kelly–Xiu (2020); Lopez de Prado's methodological papers; the RL-for-execution literature.
- **Calibration:** **[FRONTIER]** and hype-saturated. The **[SETTLED]** insight: naive ML overfits catastrophically in trading (low SNR × non-stationarity × multiple testing), and the discipline (purged CV, realistic costs, out-of-sample rigor) is what separates real edge from junk. ML-for-alpha delivers **[FRONTIER]**, genuine-but-modest edges; RL-for-execution is **[SETTLED/promising]**; **"AI beats the market" is [HYPE]**.
- **⚡ bridge (entirely your turf):** financial ML = your ML toolkit with the specific adaptations trading demands — purged CV = leakage prevention; meta-labeling = a two-stage classifier; **fractional differentiation = the memory-vs-stationarity tradeoff** (a signal-processing idea); RL-for-execution/MM = your RL applied to a natural sequential problem. This is the payoff phase for your exact profile — but the lesson is discipline, not firepower.
- **Exercises:** build a purged-CV pipeline for a return-prediction model and compare to naive CV; implement meta-labeling on a base signal; apply fractional differentiation and inspect the memory/stationarity tradeoff; sketch an RL formulation of optimal execution.
- **Time:** 5–7 weeks.
- **MVP:** the financial-ML pitfalls + purged CV + meta-labeling + the realistic assessment; defer RL depth and fractional differentiation. **Worth keeping in any MVP** — it unifies the track with your expertise while inoculating against the field's hype.

---

## The MVP fast-path (balanced core, ~4–6 months)

A route keeping all three areas plus the epistemic core, skipping Phases 0, 3, 7, 9:

1. **Phase 1 MVP** — the LOB + order types + market structure. *(~3 wk)*
2. **Phase 2 MVP** — Glosten–Milgrom + Kyle (lambda) + spread decomposition. *(~4 wk)*
3. **Phase 4 MVP** — impact models (square-root law) + Almgren–Chriss + the stochastic-control framing. *(~5 wk)*
4. **Phase 5 MVP** — the fundamental law + risk-premia overview. *(~4 wk)*
5. **Phase 6 MVP** — backtesting pitfalls + deflated Sharpe/PBO + purged CV. *(~5 wk)*
6. **Phase 8 MVP** — momentum + stat arb (OU) + carry + the four-payments frame. *(~4 wk)*
7. **Phase 10 MVP** — financial-ML pitfalls + purged CV + the realistic assessment. *(~4 wk)*

This hits microstructure (price formation), execution (Almgren–Chriss), the quant pipeline (the fundamental law + the backtesting discipline), strategy families, and ML — the balance you asked for. It defers inventory/liquidity depth, portfolio construction, and MM/HFT.

---

## Total timeline

| Route | Pace | Duration |
|---|---|---|
| **Full program** (Phases 0–10) | 8–12 hrs/wk | **~13–16 months** |
| **Balanced MVP** (above) | 8–12 hrs/wk | **~4–6 months** |

Your background compresses the execution math (Phase 4), the backtesting/ML phases (6, 10), and portfolio optimization (7). The three areas — microstructure (2→3→4), pipeline (5→6→7), and strategies (8) — run largely in parallel after Phase 1. The one phase not to skip in any version is Phase 6.

---

## Editions & currency

The canon is stable: **Harris (2003), O'Hara (1995), Hasbrouck (2007), Foucault–Pagano–Röell (2023), Cartea–Jaimungal–Penalva (2015), Bouchaud et al. (2018), Grinold–Kahn (2000), Ilmanen (2011), Lopez de Prado (2018)** — all current standards. **Two things move fast:** market structure/regulation (tick-size and venue rules change — treat Phase 1 specifics as current-as-of-date) and the **ML-for-trading frontier** (track arXiv, SSRN, and Lopez de Prado's ongoing work). And treat any *strategy* claim as decaying — published anomalies lose roughly a third of their edge post-publication (McLean–Pontiff), and marketed strategies should be assumed overfit until proven otherwise.

---

## What I can build next

- **The combined economics-and-finance-and-trading study plan** — the natural capstone now that all three fields from the original map are complete. The nine tracks deliberately cross-reference each other (micro is macro's co-req; behavioral deepens micro; game theory discharges micro/behavioral spin-offs; econometrics is the empirical spine; finance's asset pricing recurs in trading's factors; this track's stat arb is the econometrics track's cointegration), and I can sequence them into one coherent multi-year program with a dependency graph across all nine.
- A **week-by-week reading schedule** across Phases 0–10 against your hrs/week.
- A **problem-set companion** with the physics/ML-mapped derivations worked in full (Kyle as filtering, Almgren–Chriss as stochastic control, the square-root law as a scaling argument, the fundamental law as √N scaling, purged CV as leakage prevention).
- A **market-microstructure-only deep track** or an **optimal-execution-and-market-making deep track** (the Cartea–Jaimungal–Penalva / Bouchaud material) if the quant/physics core is your real target.
- A **fraud-and-trading applied dossier** — the subset most transferable to your PayPal work (the backtesting/overfitting discipline, purged CV, adversarial/non-stationary signal research, and the statistics of rare-event detection), mapped to your context.