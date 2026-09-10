# Microeconomics: A Theory-Focused Curriculum
### Intermediate foundation → research frontier · focused core (game theory & mechanism/market design spun off)

**Orientation:** theory-first, and deliberately *focused*. This covers the core price-theory spine — consumer, producer, choice under uncertainty, general equilibrium, welfare, information economics, and imperfect competition — to the research frontier. Game theory and mechanism/market design are held to the **minimum the core needs** and left for dedicated tracks (see the exclusions box). Computation is an optional strand; the payoff is a rigorous command of the theorems *and* a calibrated sense of how far their real-world reach actually extends.

**This doubles as your graduate-micro co-requisite for macro.** Phases 2–5 here are precisely what the macroeconomics curriculum (Phase 3 onward) assumes in parallel.

---

## Conventions

- **Calibration tags** (applied to *substantive claims*, not to the math):
  - **[SETTLED]** — consensus; for micro this usually means a *proven theorem* or an empirically robust model.
  - **[CONTESTED]** — the theorem may be settled but its *descriptive relevance* or *interpretation* is debated.
  - **[HYPE]** — popular claims outrunning the evidence.
  - **[FRONTIER]** — active research; conclusions still forming.
- **Free resources** marked **⊘ FREE**.
- **Edition currency:** micro's canon is unusually stable — most classics are single-edition and current as of early 2026. Verify before buying; this matters least here of any field.
- **⚡ Physics/ML bridge:** flagged as *learning accelerators* (they help you learn faster), independent of content weighting — micro theory is, mathematically, convex analysis + fixed-point theory + (at the frontier) statistical mechanics and robust optimization wearing economics notation. Some of these mappings are exact and beautiful.
- Each phase has an **MVP fast-path**; the assembled MVP spine is at the end.

---

## Deliberately excluded (your call: "keep micro focused; spin those off")

Held to a minimal-primer level here, offered as standalone curricula later:

- **Game theory** (full treatment: extensive/normal form, refinements, repeated games, evolutionary GT, epistemic foundations). Only a **minimal toolkit** — Nash equilibrium, dominance, subgame perfection, Bayesian Nash — is embedded where Phases 7–8 need it.
- **Mechanism design** (implementation theory, optimal auctions, the full revelation-principle machinery). Only *mentioned* as the gateway out of information economics (Phase 7).
- **Market design** (auctions in practice, matching markets à la Gale–Shapley/Roth, kidney exchange, school choice).
- **Full industrial organization** and **full behavioral/experimental economics** are *partially* here (the micro-theory core of each, in Phases 8 and 4 respectively) and can also be expanded into their own tracks.

The minimal GT you'll need: skim **Osborne & Rubinstein, *A Course in Game Theory*** (chs. on Nash, subgame perfection, Bayesian games) — or the GT sections of **⊘ Rubinstein's free lecture notes** — before Phases 7–8. Don't go deeper until the dedicated GT track.

---

## Your background as an accelerator (the exact mappings)

1. **Consumer/producer duality = the Legendre transform.** The expenditure and indirect-utility functions are Legendre-conjugate, exactly as Lagrangian↔Hamiltonian or internal-energy↔free-energy. Same for cost↔profit. Once you see it, half of duality theory is free. → Phases 2–3.
2. **The Slutsky matrix is symmetric because of a Maxwell relation.** Symmetry of the substitution matrix = equality of cross-partials of the expenditure function = an integrability condition. It's the same argument that gives Maxwell relations in thermodynamics. → Phase 2.
3. **Revealed preference / integrability = conservative vector fields.** Whether observed demand comes from *some* utility function is whether the "field" is path-independent (has a potential). Afriat's theorem is the discrete version. → Phase 2.
4. **Discrete choice (logit) = the Boltzmann distribution.** McFadden's conditional logit gives choice probability ∝ exp(utility/scale) — literally the Gibbs/Boltzmann distribution; the "scale" is temperature. Random utility is statistical mechanics; it's also the softmax you already use. → Phase 4.
5. **Ambiguity aversion (maxmin expected utility) = distributionally robust optimization.** Gilboa–Schmeidler's agent maximizes the worst-case expected utility over a *set* of priors — exactly minimax/DRO from robust ML. → Phase 4.
6. **GE existence = fixed-point theorems; tâtonnement stability = dynamical systems.** Brouwer/Kakutani for existence; Lyapunov functions for stability. → Phase 5.
7. **The SMD theorem = failure of micro→macro reduction.** Rational individual demand imposes essentially *no* structure on aggregate excess demand — an emergence/non-reducibility result that will feel familiar from physics. → Phase 5.

---

## Prerequisites & co-requisites

**Math (you have the substance — the micro-specific pieces may be new):** convex analysis (separating/supporting hyperplanes, convexity), constrained optimization (Kuhn–Tucker, envelope theorem), **fixed-point theorems** (Brouwer, Kakutani), **correspondences** (upper/lower hemicontinuity) and **Berge's maximum theorem**, basic point-set topology, and probability/measure basics for decision theory. Physics/AI covers the analysis; the correspondence/maximum-theorem machinery is the one genuinely micro-flavored addition.

**No external co-requisite** — this *is* the foundational field. (It is itself the co-req for macro.)

---

## Dependency map

```
        Phase 0  Prereqs / placement (math: fixed points, correspondences)
             │
        Phase 1  Intermediate micro foundations
             │
        ┌────┴────┐
   Phase 2        Phase 3
   Consumer/demand   Producer          (dual — run in parallel)
        │    \      /
        │     \    /
   Phase 4     \  /
   Choice under  \
   uncertainty    Phase 5  General equilibrium
   & decision        │
        │        Phase 6  Welfare & social choice
        │
        └──────► Phase 7  Information economics & contracts  (+ minimal GT)
                     │
                Phase 8  Imperfect competition & market failures  (+ minimal GT)
```

**Reading:** 0→1→(2,3) is the spine; 2 and 3 are dual and parallel. Phase 4 (uncertainty) needs only 1–2 and feeds both GE-under-uncertainty and info economics. Phase 5 (GE) needs 2+3; Phase 6 follows 5. Phase 7 needs 2+4 (and the minimal GT). Phase 8 needs 2+3 (and the minimal GT). Fastest route to the two big theorems (welfare theorems + info-economics core) is 0→1→2→3→5→7.

---

# PHASE 0 — Prerequisites & Placement
*Light. The one new-ish piece is the correspondence/fixed-point toolkit.*

- **Goal:** confirm optimization + convex analysis; pick up correspondences, hemicontinuity, and Berge's maximum theorem (used heavily in GE).
- **Prerequisites:** your degree.
- **Primary:** **Simon & Blume, *Mathematics for Economists*** (reference; the correspondences/fixed-point chapters). For rigor: **Ok, *Real Analysis with Economic Applications*** (⊘ partial drafts historically circulated) — the definitive math-for-micro-theory text, dip into fixed points, correspondences, and the maximum theorem.
- **⊘ FREE:** **Rubinstein's *Lecture Notes in Microeconomic Theory*** (rubinstein.tau.ac.il) — start here for the whole field; its early chapters set the axiomatic style.
- **Calibration:** foundational **[SETTLED]**.
- **⚡ Bridge:** Kakutani is Brouwer for correspondences; Berge's maximum theorem is "the argmax varies continuously with parameters" — you've used the idea informally in optimization already.
- **Exercises:** prove a simple maximum-theorem application; verify hemicontinuity of a budget correspondence.
- **Time:** 1–3 weeks (or skip the optimization parts).
- **MVP:** learn Kakutani + Berge's theorem statements and jump to Phase 1.

---

# PHASE 1 — Intermediate Microeconomics Foundations
*The "physical picture." Fast for you, but worth the vocabulary and intuition before the axioms.*

- **Goal:** the standard intermediate toolkit — demand/supply, surplus, elasticity, monopoly basics, partial-equilibrium market failure — and a first taste of each pillar so the graduate treatment has a target.
- **Prerequisites:** Phase 0.
- **Topics:** budget sets & preferences, demand and its properties, cost and supply, perfect competition & partial-equilibrium welfare (surplus), monopoly & basic price discrimination, first look at externalities/public goods, first look at asymmetric information (the lemons intuition), a *minimal* first look at game theory (Nash, prisoner's dilemma).
- **Primary:** **Varian, *Intermediate Microeconomics: A Modern Approach*** (skim fast) — or **Nicholson & Snyder**. The strong bridge into the graduate core: **Jehle & Reny, *Advanced Microeconomic Theory*** (3rd ed.) — start it here and carry it through Phases 2–5.
- **⊘ FREE:** MRU (Marginal Revolution University) intermediate micro; Rubinstein's notes.
- **Calibration:** the intermediate core is **[SETTLED]** pedagogy. Consumer/producer surplus as an exact welfare measure is **[SETTLED with caveats]** (exact only under quasilinearity — the graduate treatment fixes this with CV/EV).
- **⚡ Bridge:** the marginal utility of income is a Lagrange multiplier / shadow price — the same object as a constraint force in mechanics.
- **Exercises:** derive monopoly pricing and the deadweight loss; work a lemons example; Jehle–Reny early problems.
- **Time:** 4–6 weeks.
- **MVP:** skim Varian for vocabulary only; go straight to Phase 2 if the intermediate material is already comfortable.

---

# PHASE 2 — Consumer & Demand Theory (graduate)
*The most-used pillar, and where your duality/thermodynamics instincts pay off immediately.*

- **Goal:** the axiomatic theory of the consumer — from preference relations to demand, duality, revealed preference, aggregation, and welfare.
- **Prerequisites:** Phases 0–1.
- **Topics:** preference relations & rationality axioms, utility representation (incl. Debreu's continuity conditions); the **utility-maximization** and **expenditure-minimization** problems; Marshallian & Hicksian demand; the **Slutsky equation** and the Slutsky matrix (symmetry, negative semidefiniteness); **duality** (indirect utility, expenditure function, Roy's identity, Shephard's lemma, the duality between them); **integrability** (recovering preferences from demand); **revealed preference** (WARP, SARP, **Afriat's theorem**); **aggregation** (Gorman polar form, the representative consumer); **welfare measures** (compensating & equivalent variation, consumer surplus and its limits).
- **Primary:** **MWG Part I (chs. 1–4)** — the standard; **Kreps, *Microeconomic Foundations I*** (chs. on choice & demand) — the cleanest modern rigorous treatment; **Jehle & Reny** ch. 1.
- **⊘ FREE:** **Rubinstein, *Lecture Notes*** (Parts I–II on preferences, utility, demand); Jonathan Levin & Nolan Miller course notes.
- **Key original readings:** Slutsky (1915); Samuelson (1938) revealed preference; Afriat (1967); Gorman (1961) aggregation.
- **Calibration:** the theory is **[SETTLED]** (a mature, closed body of results). But two calibration points: whether real choice satisfies the **rationality axioms** is **[CONTESTED]** (the behavioral critique — see Phase 4); and the **representative consumer** is a modeling convenience whose validity requires strong (Gorman) conditions — treating aggregate demand as one agent's is **[CONTESTED]** (and undercut by SMD in Phase 5).
- **⚡ Bridge (three exact ones):** duality = Legendre transform; Slutsky symmetry = a Maxwell relation (integrability of the expenditure function); revealed preference/integrability = whether demand is a conservative field with a potential. → this phase is thermodynamics with utility as the potential.
- **Exercises:** derive the Slutsky equation and prove matrix symmetry via the expenditure function; move between direct and indirect utility via duality; apply Afriat's theorem to a small dataset; check when Gorman aggregation holds.
- **Time:** 6–8 weeks.
- **MVP:** MWG chs. 2–3 (UMP/EMP, Slutsky, duality) + revealed preference basics; defer aggregation and integrability depth.

---

# PHASE 3 — Producer Theory (graduate)
*Short and dual to Phase 2 — run them together.*

- **Goal:** the theory of the firm as the formal dual of the consumer.
- **Prerequisites:** Phase 2 (parallel).
- **Topics:** production sets & their properties (returns to scale, free disposal, convexity); **cost minimization** and the cost function; **profit maximization** and the profit function; **duality** (Hotelling's lemma, Shephard's lemma, recovering technology from cost); aggregation of supply; the geometry of efficient production.
- **Primary:** **MWG ch. 5**; **Kreps *Foundations I*** (production); **Varian, *Microeconomic Analysis*** (3rd ed.) — terse and elegant on production duality.
- **⊘ FREE:** Rubinstein notes; Levin/Miller notes.
- **Key original readings:** McKenzie and Shephard on duality (any graduate source suffices).
- **Calibration:** **[SETTLED]** — a clean dual theory.
- **⚡ Bridge:** cost↔profit is again a Legendre transform; the whole phase is Phase 2 with signs flipped — you're re-deriving conjugate structure, so most of it transfers directly.
- **Exercises:** derive supply and factor demands via Hotelling/Shephard; recover a production function from a cost function; verify the profit function's convexity in prices.
- **Time:** 3–5 weeks.
- **MVP:** MWG ch. 5 core (cost/profit duality); this phase is already near-minimal.

---

# PHASE 4 — Choice Under Uncertainty & Decision Theory
*A rich pillar with a genuine, active frontier — and the densest cluster of ML mappings. Behavioral economics lives here (integrated, per your balanced choice).*

- **Goal:** the theory of choice under risk and uncertainty, from expected utility through its documented failures to the modern frontier (ambiguity, non-EU, behavioral, stochastic choice).
- **Prerequisites:** Phases 1–2.
- **Topics:**
  - **Expected utility under risk:** von Neumann–Morgenstern axioms & representation; **risk aversion** (Arrow–Pratt measures, certainty equivalents); **stochastic dominance**; comparative statics of risk; the state-preference approach.
  - **Subjective uncertainty:** Savage's subjective expected utility; the Anscombe–Aumann framework.
  - **The paradoxes (the calibration hinge):** **Allais** (violating independence) and **Ellsberg** (ambiguity/violating SEU) — robust, replicable behavioral failures of the standard theory.
  - **Frontier — ambiguity:** maxmin expected utility (**Gilboa–Schmeidler**), Choquet EU (Schmeidler), variational preferences (Maccheroni–Marinacci–Rustichini).
  - **Frontier — non-EU under risk:** rank-dependent utility (Quiggin), Machina's non-EU, and the foundations of **prospect theory** (Kahneman–Tversky 1979; cumulative PT 1992).
  - **Frontier — behavioral & dynamic:** reference-dependence (Kőszegi–Rabin), temptation & self-control (Gul–Pesendorfer), hyperbolic discounting; **stochastic choice / random utility** (Luce, McFadden discrete choice); rational inattention as decision theory (Sims; Caplin–Dean).
- **Primary:** **MWG ch. 6**; **Kreps, *Notes on the Theory of Choice*** (the classic short treatment); **Gilboa, *Theory of Decision under Uncertainty*** (the frontier text); **Wakker, *Prospect Theory for Risk and Ambiguity*** (definitive on PT foundations).
- **⊘ FREE:** Rubinstein notes (choice under uncertainty; also his *Modeling Bounded Rationality*, portions free); MIT OCW 14.123.
- **Key original readings:** von Neumann–Morgenstern (1944); Savage (1954); Arrow–Pratt (1964–65); Allais (1953); Ellsberg (1961); Gilboa–Schmeidler (1989); Kahneman–Tversky (1979); McFadden (1974).
- **Calibration:** the **vNM/Savage representation theorems are [SETTLED]** mathematics. **EU as a description of behavior is [CONTESTED]** — Allais and Ellsberg are among the most replicable results in economics. The ambiguity and non-EU frontiers are **[FRONTIER]** (no single successor has won). Behavioral economics carries the same caveat as in the macro track: prospect theory itself is robust, but the **broader behavioral literature has real replication problems** — treat individual "bias" effects as **[CONTESTED]**, and pop-behavioral overreach as **[HYPE]**.
- **⚡ Bridge (the showcase cluster):** discrete choice/logit = Boltzmann distribution = softmax (McFadden ⇄ Gibbs); maxmin EU = distributionally robust optimization (worst-case over a prior set = DRO/minimax); rational inattention = Shannon channel capacity; risk aversion (concavity) ⇄ the curvature/second-order structure you know from utility-as-potential.
- **Exercises:** prove the vNM representation; compute Arrow–Pratt coefficients and rank prospects by stochastic dominance; work the Ellsberg example under maxmin EU; show McFadden's logit is a Boltzmann distribution.
- **Time:** 6–8 weeks.
- **MVP:** MWG ch. 6 (vNM + Arrow–Pratt + stochastic dominance); read Ellsberg + one ambiguity model; defer the non-EU/behavioral frontier.

---

# PHASE 5 — General Equilibrium Theory
*The intellectual summit of micro — existence, the welfare theorems, and the hard truths about their reach. The most demanding phase.*

- **Goal:** Walrasian general equilibrium: existence, efficiency (the two welfare theorems), the core, stability, the SMD limits, and the incomplete-markets frontier.
- **Prerequisites:** Phases 2–3 (Phase 4 for the uncertainty extension).
- **Topics:** the Walrasian model & Walras's law; the **Edgeworth box**; **existence** of competitive equilibrium (via Brouwer/Kakutani; Arrow–Debreu, McKenzie); the **First & Second Fundamental Theorems of Welfare Economics**; the **core** and **core convergence** (Debreu–Scarf); **uniqueness & stability** (tâtonnement); the **Sonnenschein–Mantel–Debreu theorem** (aggregate excess demand is essentially unrestricted); **computation** of equilibrium (Scarf); **uncertainty in GE** (Arrow–Debreu contingent commodities, Arrow securities); **frontier — general equilibrium with incomplete markets (GEI)** (Radner; the welfare theorems *fail* — the bridge to macro-finance), and GE with asymmetric information.
- **Primary:** **MWG Part IV (chs. 15–17)**; **Kreps *Foundations I*** (competitive markets & welfare theorems); **Debreu, *Theory of Value*** (1959) — the axiomatic classic, read as a primary source; **Mas-Colell, *The Theory of General Economic Equilibrium: A Differentiable Approach*** (frontier/advanced).
- **⊘ FREE:** Rubinstein notes (competitive equilibrium); Levin's GE notes.
- **Key original readings:** Arrow–Debreu (1954); the welfare theorems (any rigorous source); Debreu–Scarf (1963); Sonnenschein (1972)/Mantel (1974)/Debreu (1974); Radner (1972) GEI.
- **Calibration (the central calibration lesson of the whole curriculum):** existence and the **two welfare theorems are [SETTLED]** — landmark, Nobel-honored theorems. But their **descriptive reach is much narrower than folklore suggests, and that gap is [CONTESTED/underappreciated]**: tâtonnement **stability is not generically guaranteed**; **SMD** shows the model imposes almost no testable structure on aggregates (so "the economy is a stable equilibrium system" is not a theorem); and with **incomplete markets (GEI) the welfare theorems fail** outright. "Markets reach efficient equilibria" is a vastly stronger — and unproven — claim than "competitive equilibria are efficient." Hold the theorems as settled and the real-world inference as contested.
- **⚡ Bridge:** existence = fixed-point theory (Kakutani); tâtonnement = a dynamical system with Lyapunov stability (generically *not* globally stable — the interesting part); **SMD = non-reducibility/emergence** (micro rationality underdetermines macro structure).
- **Exercises:** prove existence for a simple exchange economy via Kakutani; prove the First Welfare Theorem; work Debreu–Scarf core convergence in the Edgeworth box; construct an unstable tâtonnement example; state precisely why GEI breaks the Second Welfare Theorem.
- **Time:** 7–9 weeks.
- **MVP:** MWG ch. 15–16 (existence + both welfare theorems) + the SMD *statement and its meaning*; defer computation, differentiable approach, and full GEI.

---

# PHASE 6 — Welfare Economics & Social Choice
*Compact, theorem-dense, and philosophically loaded. Some of this borders mechanism design — kept light per your instruction.*

- **Goal:** the normative core — efficiency vs. distribution, social welfare functions, and the great impossibility theorems.
- **Prerequisites:** Phase 5.
- **Topics:** Pareto efficiency and its limits; **Bergson–Samuelson social welfare functions**; interpersonal comparisons and **Harsanyi's utilitarian aggregation**; **Arrow's impossibility theorem**; **Gibbard–Satterthwaite** (stated as the bridge to mechanism design — kept light); **Sen's liberal paradox** and the capabilities critique; fairness/no-envy; **Nash bargaining** (stated only — full bargaining is in the GT spin-off).
- **Primary:** **MWG chs. 21–22**; **Sen, *Collective Choice and Social Welfare*** (expanded ed., 2017) — the definitive primary source; **Arrow, *Social Choice and Individual Values*** (the original).
- **⊘ FREE:** Rubinstein notes; Klaus Nehring / Ariel Rubinstein social-choice materials.
- **Key original readings:** Arrow (1951/1963); Gibbard (1973)/Satterthwaite (1975); Sen (1970) on the impossibility of a Paretian liberal; Harsanyi (1955).
- **Calibration:** Arrow and Gibbard–Satterthwaite are **[SETTLED]** impossibility theorems — as solid as results get. What they *imply for institutional design* (which escape routes — restricted domains, cardinal information — are acceptable) is **[CONTESTED]** and genuinely philosophical.
- **⚡ Bridge:** impossibility theorems are, structurally, "no function satisfies all these axioms simultaneously" — the same flavor as no-go theorems in physics; the proofs are combinatorial/logical rather than analytic.
- **Exercises:** prove Arrow's theorem (via the decisive-set / pivotal-voter argument); state Gibbard–Satterthwaite and its link to the revelation principle; work Sen's liberal-paradox example.
- **Time:** 3–5 weeks.
- **MVP:** Arrow's theorem (statement + one proof) + the welfare theorems' normative interpretation; defer Sen and bargaining.

---

# PHASE 7 — Information Economics & Contract Theory
*The pillar closest to modern applied micro. Needs the minimal GT toolkit. The revelation principle is the one door left ajar to the mechanism-design spin-off.*

- **Goal:** economics under asymmetric information — adverse selection, signaling, screening, moral hazard — and the theory of contracts.
- **Prerequisites:** Phases 2, 4; minimal GT (Bayesian Nash).
- **Topics:**
  - **Adverse selection:** Akerlof's **market for lemons**; insurance **screening** (Rothschild–Stiglitz); self-selection & second-degree price discrimination as a screening problem.
  - **Signaling:** Spence's **job-market signaling**; separating vs. pooling equilibria; refinements (intuitive criterion — light).
  - **Moral hazard:** the hidden-action **principal–agent** model; the **informativeness principle** (Holmström); the risk/incentive trade-off; **multitasking** (Holmström–Milgrom).
  - **Contract theory:** complete vs. **incomplete contracts**; the **property-rights approach** (Grossman–Hart–Moore); career concerns; relational contracts.
  - **The mechanism-design gateway:** the **revelation principle** (stated, as the bridge to the MD track); **information design / Bayesian persuasion** (Kamenica–Gentzkow — flagged as frontier, bordering MD, kept light).
- **Primary:** **MWG chs. 13–14** (+ ch. 23 revelation principle, lightly); **Bolton & Dewatripont, *Contract Theory*** (the definitive text); **Laffont & Martimort, *The Theory of Incentives*** (principal–agent depth).
- **⊘ FREE:** Rubinstein notes; MIT OCW 14.121/14.281 (contract theory) materials.
- **Key original readings:** Akerlof (1970); Spence (1973); Rothschild–Stiglitz (1976); Holmström (1979); Grossman–Hart (1986); Holmström–Milgrom (1991); Myerson (1981) on the revelation principle.
- **Calibration:** the **core models are [SETTLED]** and foundational (three Nobel prizes' worth). The **foundations of incomplete contracts are [CONTESTED]** — the Maskin–Tirole critique questioned whether incompleteness is well-defined, and the debate isn't fully resolved. **Information design/Bayesian persuasion is [FRONTIER]** (very active).
- **⚡ Bridge:** the principal–agent problem is constrained optimization subject to **incentive-compatibility** and **participation** constraints — the same optimization-with-constraints structure you use daily; screening/self-selection is optimization over a menu subject to no-envy-across-types (a combinatorial constraint set).
- **Exercises:** solve the lemons model; derive the Rothschild–Stiglitz separating equilibrium; solve a two-outcome principal–agent problem and read off the informativeness principle; state the revelation principle precisely.
- **Time:** 6–8 weeks.
- **MVP:** MWG ch. 13–14 core (lemons, signaling, basic moral hazard); defer incomplete-contracts foundations and information design.

---

# PHASE 8 — Imperfect Competition & Market Failures
*The applied-theory capstone within micro. Uses the minimal GT toolkit; this is the micro-theory core of IO and public economics (both possible spin-offs).*

- **Goal:** market power and the classic market failures — the theory that sits under industrial organization and public economics.
- **Prerequisites:** Phases 2–3; minimal GT (Nash, subgame perfection).
- **Topics:**
  - **Monopoly & price discrimination:** first/second/third-degree; nonlinear pricing (Mussa–Rosen, Maskin–Riley); bundling.
  - **Oligopoly:** Cournot, Bertrand, Stackelberg; the Bertrand paradox and its resolutions; product differentiation (**Hotelling**, **Salop** circular city); **Dixit–Stiglitz** monopolistic competition; entry, contestability, and (lightly) entry deterrence.
  - **Externalities:** the Coase theorem; Pigouvian remedies; missing markets.
  - **Public goods:** the **Samuelson condition**; free-riding; Lindahl pricing; (lightly) Tiebout.
  - **Common-pool resources:** the tragedy of the commons (Hardin) and its critique (Ostrom).
- **Primary:** **MWG chs. 10–12**; **Tirole, *The Theory of Industrial Organization*** (the classic — use the micro-theory chapters); **Jehle & Reny** (imperfect competition).
- **⊘ FREE:** Rubinstein notes; MRU (externalities/public goods).
- **Key original readings:** Cournot (1838); Bertrand (1883); Hotelling (1929); Dixit–Stiglitz (1977); Coase (1960); Samuelson (1954); Ostrom (1990, overview).
- **Calibration:** monopoly and the canonical oligopoly models are **[SETTLED]** theory; but **specific oligopoly predictions are model-dependent and [CONTESTED]** (Cournot vs. Bertrand can give opposite conclusions — the "right" model is an empirical question, which is why structural IO exists). The **Coase theorem** is **[SETTLED as a theorem / CONTESTED in application]** (zero transaction costs is the crux, and rarely holds). Ostrom's work is **[SETTLED]** as an empirical corrective to naive commons pessimism.
- **⚡ Bridge:** Dixit–Stiglitz aggregation is CES/power-law aggregation (you'll have met it in the macro NK track too); Hotelling/Salop spatial competition is an optimization on a metric space; externalities are simply objective functions with interaction terms the market price doesn't internalize.
- **Exercises:** solve Cournot and Bertrand and compare welfare; derive optimal second-degree price discrimination (a screening problem — ties back to Phase 7); derive the Samuelson condition and show the free-riding shortfall; work a Coase-theorem bargaining example.
- **Time:** 5–7 weeks.
- **MVP:** MWG chs. 10–12 core (monopoly, Cournot/Bertrand, externalities, public goods); defer spatial models and commons.

---

## The MVP fast-path (compressed core, ~3–4 months)

Rigorous-but-fast route to the load-bearing theorems, skipping Phases 0–1, the frontiers, and Phase 6:

1. **Phase 2 MVP** — consumer theory: UMP/EMP, Slutsky, duality. *(~4 wk)*
2. **Phase 3 MVP** — producer theory: cost/profit duality. *(~2 wk)*
3. **Phase 4 MVP** — vNM expected utility + Arrow–Pratt + stochastic dominance. *(~3 wk)*
4. **Phase 5 MVP** — existence + both welfare theorems + the meaning of SMD. *(~4 wk)*
5. **Phase 7 MVP** — information economics core: lemons, signaling, basic moral hazard. *(~3 wk)*

This gets you the consumer/producer machinery, decision-under-risk, the welfare theorems (and their limits), and the asymmetric-information core — the parts macro actually leans on. It defers general equilibrium's harder results, social choice, imperfect competition, and every frontier.

---

## Total timeline

| Route | Pace | Duration |
|---|---|---|
| **Full program** (Phases 0–8) | 8–12 hrs/wk | **~10–14 months** |
| **MVP core** (above) | 8–12 hrs/wk | **~3–4 months** |

Shorter than the macro track because game theory and mechanism/market design are spun off. Phases 2 & 3 run in parallel; the one phase not to compress below MVP is Phase 5 (general equilibrium).

---

## Editions & currency

Micro's canon is the most stable of any field here. **MWG (1995)** is *the* single-edition standard and remains current. **Kreps *Foundations I* (2013), Jehle–Reny 3rd (2011), Bolton–Dewatripont (2005), Laffont–Martimort (2002), Tirole IO (1988), Gilboa (2009), Wakker (2010), Debreu (1959), Mas-Colell (1985)** — all effectively current; no edition anxiety. **Rubinstein's free lecture notes** are updated periodically on his site — grab the latest. Frontier material (ambiguity, information design, incomplete-markets GE) lives in journal articles; supplement with recent working papers there.

---

## What I can build next

- The three **spin-off tracks** your "keep micro focused" choice implies: **game theory** (the big one), **mechanism design** (implementation, optimal auctions), and **market design** (auctions in practice, matching — Gale–Shapley/Roth).
- A **week-by-week reading schedule** across Phases 0–8 against your hrs/week.
- A **problem-set companion** with the physics-mapped derivations (Slutsky-as-Maxwell-relation, logit-as-Boltzmann, maxmin-as-DRO) worked in full.
- A **full industrial-organization** track or a **full behavioral/experimental** track, each expanding its micro-theory core from Phases 8 / 4.
- The **combined econ study plan** interleaving this with the macro curriculum (this is macro's co-requisite — I can sequence them together).