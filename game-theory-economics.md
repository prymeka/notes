# Game Theory: A Non-Cooperative-Forward Curriculum
### Intermediate foundation → research frontier · classical core + mechanism & market design + behavioral game theory

**Orientation:** theory-forward and **non-cooperative-forward**. This is the largest track in the program, and it deliberately absorbs two earlier deferrals: **mechanism design and market design** (routed here from the micro track) and **social preferences and behavioral game theory** (routed here from the behavioral track) are full pillars. Cooperative game theory is included as **essentials only** (one compact phase). Algorithmic/computational game theory is a **light, economics-flavored** thread rather than a CS pillar — but learning-in-games (no-regret dynamics → correlated equilibrium) is core, and the ML correspondences are flagged as accelerators throughout.

**The market-design highlight:** most of this program teaches theory whose real-world reach is narrower than it looks. Market design is the exception — the FCC spectrum auctions, kidney-exchange chains, and the medical-residency and school-choice matches are this theory, deployed and running. Its calibration is "settled *and* built."

---

## Conventions

- **Calibration tags:** **[SETTLED]** (proven/robust), **[CONTESTED]** (magnitude, interpretation, or predictive validity debated), **[HYPE]** (claims outrunning evidence), **[FRONTIER]** (active).
- **⊘ FREE** marks free resources — game theory is unusually well-served here (Rubinstein and Roughgarden both host major texts free; Yale's Polak lectures are open).
- **⚡ Physics/ML bridge:** learning accelerators, independent of content weighting. Modern game theory shares deep structure with online learning, dynamical systems, and constrained optimization — several mappings below are exact.
- Each phase has an **MVP fast-path**; the assembled MVP spine is at the end.

---

## Scope decisions (yours)

- **Cooperative game theory → essentials only.** Nash bargaining, the core, the Shapley value, and the nucleolus get one compact phase (Phase 4). The full cooperative apparatus (coalition-formation theory, values beyond Shapley, cooperative solution correspondences) is out; can be a spin-off.
- **Algorithmic game theory → light, economics-flavored.** Learning-in-games and no-regret dynamics are core (Phase 5); the price of anarchy and the LP view of mechanism design are noted where natural. The full AGT apparatus (PPAD-completeness proofs, algorithmic mechanism design, combinatorial-auction approximation) is *pointed to*, not built — **⊘ Nisan–Roughgarden–Tardos–Vazirani, *Algorithmic Game Theory*** (free online) and Roughgarden's free lectures are the door if you later want it.

What this delivers that was owed: **mechanism design** (Phase 7), **auctions + matching/market design** (Phase 8), **social preferences + behavioral game theory** (Phase 9).

---

## Your background as an accelerator (the exact mappings)

1. **Zero-sum/minimax = LP duality = the GAN objective.** Von Neumann's minimax theorem is linear-programming duality; solving a zero-sum game is a saddle-point problem — the same minimax optimization as adversarial training. → Phase 1.
2. **Replicator dynamics = multiplicative weights.** The continuous-time replicator equation *is* the continuous limit of the multiplicative-weights / exponential-weights update. Evolutionary dynamics and your online-learning toolkit are the same object. → Phase 5.
3. **No-regret learning = online convex optimization.** If every player runs a no-regret algorithm, the empirical play converges to the set of coarse correlated equilibria (Hart–Mas-Colell). This is your wheelhouse, and it's the most satisfying modern answer to "why would anyone play an equilibrium?" → Phase 5.
4. **Quantal response equilibrium = softmax/logit equilibrium.** QRE replaces best-response with a Boltzmann/softmax response; the "rationality" parameter is inverse temperature. It's the game-theoretic version of the logit you've now met in micro and behavioral. → Phase 9.
5. **Backward induction = dynamic programming.** Sequential rationality solved by working backward is Bellman's principle again. → Phase 2.
6. **Deferred acceptance (Gale–Shapley) = a combinatorial algorithm with a lattice structure.** Stable matchings form a lattice; the algorithm is a constructive fixed-point computation. → Phase 8.
7. **Level-k / cognitive hierarchy = depth-limited search.** Bounded strategic reasoning is iterated best-response truncated at a finite depth — bounded-depth game-tree reasoning. → Phase 9.

---

## Prerequisites & co-requisites

**Math (you have this):** optimization and Lagrangian/KKT; probability (for mixed strategies and Bayesian games); **fixed-point theorems** (Brouwer/Kakutani — Nash existence, as in micro GE); linear programming and duality (zero-sum games, and the LP view of mechanism design); basic combinatorics/discrete math (matching, mechanism design). This is built from the intermediate level up, so no game-theory prerequisite is assumed.

**Relationship to the other tracks:** this is self-contained. It discharges the GT/mechanism/market-design spin-offs promised by the micro track and the social-preference/behavioral-GT spin-offs promised by the behavioral track; Phase 9 carries the behavioral track's replication discipline.

---

## Dependency map

```
        Phase 0  Prereqs (fixed points, LP duality, combinatorics)
             │
        Phase 1  Static games, complete information (Nash, minimax, correlated eq)
             │
        Phase 2  Dynamic & incomplete-information games (SPE, Bayesian, sequential eq)
           /  │  \
   Phase 3   Phase 4   Phase 5           Phase 6
   Repeated  Bargaining Learning &       Epistemic
   games &   & coop.    evolution        foundations
   reputation essentials (no-regret,     (common knowledge;
      │       (core,     replicator,      MVP-skippable)
      │       Shapley)   ESS)
      │
      └──────────────► Phase 7  Mechanism design (revelation, VCG, Myerson)
                            │
                       Phase 8  Auctions & market design (Gale–Shapley, Roth)
                            │
                       Phase 9  Behavioral GT & social preferences
```

**Reading:** 0→1→2 is the core chain. Phase 2 unlocks 3, 4, 5, 6 (largely parallel). Phase 7 (mechanism design) needs Bayesian games (Phase 2) and the social-choice results (recap from micro); Phase 8 needs 7 plus the core (Phase 4, for matching). Phase 9 tests the games of 1–3. Fastest route through the owed material: 0→1→2→7→8→9.

---

# PHASE 0 — Prerequisites & Placement
*Light. Confirm fixed points, LP duality, and enough discrete math.*

- **Goal:** confirm the toolkit — Brouwer/Kakutani (Nash existence), LP duality (zero-sum), combinatorics (matching).
- **Primary:** any of the game-theory texts' math appendices; you've met Kakutani in micro GE.
- **⊘ FREE:** Yale Open Courses — **Ben Polak, *Game Theory* (ECON 159)** — start these lectures alongside Phase 1 for intuition.
- **Calibration:** **[SETTLED]** foundations.
- **⚡ Bridge:** LP duality = minimax; you already have the fixed-point machinery from GE.
- **Time:** 1–2 weeks (or skip).
- **MVP:** skip if the math is comfortable.

---

# PHASE 1 — Static Games of Complete Information
*The core solution concepts, from the intermediate on-ramp to correlated equilibrium.*

- **Goal:** strategic-form games and their solution concepts — dominance, rationalizability, Nash (pure and mixed), existence, the minimax theorem, and correlated equilibrium.
- **Prerequisites:** Phase 0.
- **Topics:** strategic (normal) form; strict/weak **dominance** and iterated deletion; **rationalizability** (Bernheim, Pearce); **Nash equilibrium** (pure and mixed) and its **existence** (Nash's theorem via Kakutani); **zero-sum games and the minimax theorem** (von Neumann; the LP-duality connection); **correlated equilibrium** (Aumann); interpretations of mixed strategies (the perennial puzzle).
- **Primary:**
  - **Tadelis, *Game Theory: An Introduction*** — the best modern bridge from intermediate to graduate; your spine for Phases 1–3.
  - **Osborne & Rubinstein, *A Course in Game Theory*** — the rigorous standard.
  - **Fudenberg & Tirole, *Game Theory*** — the graduate reference (dense; use for depth).
  - **Osborne, *An Introduction to Game Theory*** — gentler, for the intermediate layer.
- **⊘ FREE:** **Osborne–Rubinstein *A Course in Game Theory*** (Rubinstein hosts it free at arielrubinstein.org); **Polak's Yale lectures**; Jackson/Leyton-Brown/Shoham Coursera game theory.
- **Key original readings:** Nash (1950, 1951); von Neumann (1928) minimax; Aumann (1974) correlated equilibrium; Bernheim (1984)/Pearce (1984) rationalizability.
- **Calibration:** **Nash equilibrium is [SETTLED]** as *the* central solution concept. But its **interpretation and predictive validity are [CONTESTED]** — multiplicity, and the "why would agents actually play it?" problem, which Phases 5 (learning), 6 (epistemics), and 9 (behavior) each address from a different angle. Correlated equilibrium is **[SETTLED]** and arguably more natural (it's what no-regret learning reaches).
- **⚡ Bridge:** minimax = LP duality = saddle-point/GAN optimization; Nash existence = Kakutani; a mixed equilibrium is a fixed point of the best-response correspondence.
- **Exercises:** compute mixed-strategy equilibria; solve a zero-sum game via LP; find the correlated equilibria of a coordination game and compare to Nash; prove Nash existence for a 2×2 game via Kakutani.
- **Time:** 5–7 weeks.
- **MVP:** Tadelis on dominance, Nash (pure/mixed), and correlated equilibrium; defer rationalizability depth.

---

# PHASE 2 — Dynamic Games & Games of Incomplete Information
*Extensive form, credibility, and beliefs — the workhorse machinery of applied theory.*

- **Goal:** sequential rationality and incomplete information — subgame perfection, Bayesian and perfect Bayesian equilibrium, signaling, and the refinements.
- **Prerequisites:** Phase 1.
- **Topics:** extensive form, information sets, **behavioral strategies** (Kuhn's theorem); **backward induction** and **subgame-perfect equilibrium** (Selten); commitment and credibility; **games of incomplete information** (Harsanyi) and **Bayesian Nash equilibrium**; dynamic + incomplete → **perfect Bayesian** and **sequential equilibrium** (Kreps–Wilson); **signaling games** (separating/pooling); **refinements** (trembling-hand perfection — Selten; the intuitive criterion; forward induction) and the honest caveat that the refinement literature overproliferated.
- **Primary:** **Fudenberg & Tirole** (the definitive treatment of this material); **Tadelis**; **Osborne–Rubinstein**; **Myerson, *Game Theory: Analysis of Conflict*** (strong on foundations).
- **⊘ FREE:** Osborne–Rubinstein (Rubinstein's site); Polak's Yale lectures.
- **Key original readings:** Selten (1965) SPE, (1975) trembling-hand; Harsanyi (1967–68) incomplete information; Kreps–Wilson (1982) sequential equilibrium.
- **Calibration:** SPE/backward induction **[SETTLED]** as logic. The **refinement literature is [CONTESTED]** — an acknowledged embarrassment of competing criteria. And backward induction's **behavioral** validity is **[CONTESTED]** (the centipede game and guessing games — foreshadowing Phase 9).
- **⚡ Bridge:** backward induction = dynamic programming (Bellman, once more); sequential rationality = optimality at every information set given beliefs (beliefs updated by Bayes where possible).
- **Exercises:** solve a signaling game for its separating and pooling PBE and apply the intuitive criterion; work a finite-horizon bargaining game by backward induction; construct a sequential equilibrium with off-path beliefs.
- **Time:** 6–8 weeks.
- **MVP:** Fudenberg–Tirole on SPE, Bayesian Nash, and PBE + one signaling game; defer the refinement zoo.

---

# PHASE 3 — Repeated Games & Reputation
*Why cooperation can be an equilibrium — and why the theory permits almost anything.*

- **Goal:** repeated interaction, the folk theorems, reputation, and imperfect monitoring.
- **Prerequisites:** Phase 2.
- **Topics:** finitely and infinitely **repeated games**; discounting and trigger strategies; the **folk theorems** (Nash-threat; the subgame-perfect folk theorem — Fudenberg–Maskin); cooperation and collusion; **reputation effects** (Kreps–Milgrom–Roberts–Wilson "gang of four"; the chain-store paradox); **imperfect monitoring** (public — Green–Porter, Abreu–Pearce–Stacchetti self-generation; private monitoring).
- **Primary:** **Fudenberg & Tirole** (repeated games chapter); **Mailath & Samuelson, *Repeated Games and Reputations*** (the definitive monograph — frontier depth).
- **⊘ FREE:** lecture notes from Mailath's and others' courses circulate.
- **Key original readings:** Fudenberg–Maskin (1986) folk theorem; Kreps–Milgrom–Roberts–Wilson (1982) reputation; Abreu–Pearce–Stacchetti (1990).
- **Calibration:** the **folk theorems are [SETTLED]** theorems — but their "**almost anything is an equilibrium**" conclusion is a genuine limitation on predictive content (the GT analogue of SMD in micro: the theory permits too much). Reputation results are **[SETTLED]** theoretically and among GT's most influential applied ideas.
- **⚡ Bridge:** the Abreu–Pearce–Stacchetti self-generation method is dynamic programming on *sets of equilibrium values* — a fixed-point operator on value sets, structurally like value iteration lifted to correspondences.
- **Exercises:** prove the folk theorem for the repeated prisoner's dilemma with trigger strategies; derive the critical discount factor for cooperation; sketch the APS operator on a simple example.
- **Time:** 5–7 weeks.
- **MVP:** Fudenberg–Tirole on infinitely repeated games + the subgame-perfect folk theorem + reputation basics; defer imperfect-monitoring depth.

---

# PHASE 4 — Bargaining & Cooperative Essentials
*Compact, per your "essentials only." Bargaining bridges the non-cooperative and cooperative worlds.*

- **Goal:** the bargaining problem from both sides, plus the core cooperative solution concepts.
- **Prerequisites:** Phases 1–2 (Rubinstein bargaining needs extensive-form/SPE).
- **Topics:** **non-cooperative bargaining** — Rubinstein's alternating-offers model and its unique SPE; the **Nash bargaining solution** (axiomatic: Pareto, symmetry, IIA, invariance) and the **Nash program** (Rubinstein's model converging to Nash's axiomatic solution as the bridge between the two paradigms); the **core** (and its relation to competitive equilibrium — recap from micro GE — and to matching); the **Shapley value** (axioms; applications to cost-sharing and voting power — Shapley–Shubik); the **nucleolus** (briefly). This is the *only* cooperative material, kept tight.
- **Primary:** **Osborne & Rubinstein, *Bargaining and Markets*** (the bargaining classic — **⊘ FREE** on Rubinstein's site); **Maschler, Solan & Zamir, *Game Theory*** (the best rigorous treatment of the cooperative essentials); **Osborne–Rubinstein** *A Course* (cooperative chapters).
- **⊘ FREE:** *Bargaining and Markets* and *A Course in Game Theory* (Rubinstein's site).
- **Key original readings:** Nash (1950) bargaining; Rubinstein (1982) alternating offers; Shapley (1953) value; Gillies (1959) core.
- **Calibration:** Rubinstein's uniqueness result and the Nash bargaining axioms are **[SETTLED]**; the Nash program (their equivalence) is **[SETTLED]** and elegant. The Shapley value and core are **[SETTLED]** classical results.
- **⚡ Bridge:** Rubinstein's SPE is again a backward-induction/fixed-point argument; the core is the intersection of a family of half-space constraints (an LP-flavored object); the Shapley value is an averaging over orderings (an expectation over permutations).
- **Exercises:** derive the Rubinstein SPE and take the frictionless limit to the Nash solution; verify the Nash bargaining axioms; compute a Shapley value and a core for a 3-player game.
- **Time:** 4–6 weeks.
- **MVP:** Rubinstein bargaining + Nash solution + the Nash program; skim the core and Shapley value.

---

# PHASE 5 — Learning & Evolution in Games
*The dynamic foundations — and, for you, the phase where online learning is literally the subject.*

- **Goal:** how equilibrium might *emerge* from adaptive or evolutionary dynamics, and the no-regret route to correlated equilibrium.
- **Prerequisites:** Phase 1.
- **Topics:** **learning dynamics** (fictitious play, best-response dynamics) and their convergence/non-convergence; **no-regret learning** and its convergence to (coarse) correlated equilibrium (Hart–Mas-Colell; Blackwell approachability) — the modern answer to equilibrium justification; **evolutionary game theory** (evolutionarily stable strategies — Maynard Smith; replicator dynamics; evolutionary stability); **stochastic evolutionary dynamics** and stochastic stability (Kandori–Mailath–Rob; Young). Light algorithmic touch: no-regret dynamics are computationally efficient and reach coarse correlated equilibrium; the **price of anarchy** is defined here (used in Phase 8).
- **Primary:** **Fudenberg & Levine, *The Theory of Learning in Games*** (the definitive text); **Weibull, *Evolutionary Game Theory***; **Sandholm, *Population Games and Evolutionary Dynamics***; **Young, *Strategic Learning and Its Limits***.
- **⊘ FREE:** Roughgarden's AGT lectures (for the no-regret → correlated-equilibrium and price-of-anarchy material); *Algorithmic Game Theory* (NRTV, free online).
- **Key original readings:** Maynard Smith (1973) ESS; Kandori–Mailath–Rob (1993) and Young (1993) stochastic evolution; Hart–Mas-Colell (2000) no-regret and correlated equilibrium.
- **Calibration:** the learning/evolutionary dynamics are **[SETTLED]** mathematics; whether *actual* play converges to equilibrium is **[CONTESTED/mixed]** (some games converge, many cycle). ESS is **[SETTLED]** in evolutionary biology and a useful refinement in economics.
- **⚡ Bridge (the payoff cluster):** replicator dynamics = continuous-time multiplicative weights; no-regret learning = online convex optimization, converging to coarse correlated equilibrium; fictitious play = a specific learning rule; stochastic stability = perturbed Markov chains / simulated-annealing-style selection among equilibria. This is the corner of GT closest to your day-to-day.
- **Exercises:** simulate/analyze replicator dynamics for rock–paper–scissors (and see the cycling); show a no-regret algorithm's empirical play is coarse-correlated-equilibrium; compute an ESS; find the stochastically stable equilibrium of a 2×2 coordination game.
- **Time:** 5–7 weeks.
- **MVP:** no-regret learning → correlated equilibrium + replicator dynamics + ESS; defer stochastic-stability depth.

---

# PHASE 6 — Epistemic Foundations
*Deep and clarifying: what each solution concept actually assumes. Compact and MVP-skippable.*

- **Goal:** the interactive-epistemology foundations — knowledge, common knowledge, and the epistemic conditions for solution concepts.
- **Prerequisites:** Phases 1–2.
- **Topics:** knowledge and belief operators; **common knowledge** (Aumann); the **"agreeing to disagree"** theorem and common priors; **epistemic conditions for solution concepts** (rationalizability = common knowledge of rationality; the epistemic conditions for Nash — Aumann–Brandenburger; for correlated equilibrium); type spaces and hierarchies of beliefs (Mertens–Zamir); the electronic mail game (Rubinstein) and the fragility of common knowledge.
- **Primary:** **Perea, *Epistemic Game Theory: Reasoning and Choice*** (the modern textbook); **Osborne–Rubinstein** (knowledge chapter); Dekel–Siniscalchi Handbook chapter.
- **⊘ FREE:** Osborne–Rubinstein (Rubinstein's site); Perea maintains course materials.
- **Key original readings:** Aumann (1976) agreeing to disagree; Aumann–Brandenburger (1995) epistemic conditions for Nash equilibrium; Rubinstein (1989) electronic mail game.
- **Calibration:** epistemic GT is **[SETTLED]** as rigorous foundations and **[FRONTIER/specialized]** as an active, philosophically deep area. Its value is diagnostic — it tells you exactly what assumptions each solution concept smuggles in (e.g., that Nash requires much stronger epistemic conditions than rationalizability).
- **⚡ Bridge:** common knowledge is a fixed point of a knowledge operator; the belief hierarchy / type space is a recursive (coinductive) structure — the same self-referential flavor as recursive types in programming.
- **Exercises:** prove the agreement theorem in a small example; state the Aumann–Brandenburger conditions for Nash; work the electronic mail game and see why approximate common knowledge fails.
- **Time:** 3–5 weeks.
- **MVP:** **skippable.** If included: common knowledge + the agreement theorem + the epistemic conditions for Nash vs. rationalizability.

---

# PHASE 7 — Mechanism Design
*(Owed from micro — full pillar.) Reverse game theory: designing the rules to get the outcomes you want.*

- **Goal:** the design problem, the revelation principle, and the landmark possibility/impossibility results.
- **Prerequisites:** Phase 2 (Bayesian games); the social-choice results (Gibbard–Satterthwaite) recapped from micro.
- **Topics:** the mechanism-design problem; the **revelation principle** (Myerson); **dominant-strategy vs. Bayesian implementation**; **Gibbard–Satterthwaite** (recap) and its escape via restricted domains / transfers; the **Vickrey–Clarke–Groves (VCG)** mechanism and Groves mechanisms (efficient, dominant-strategy); **Myerson's optimal (revenue-maximizing) mechanism** (virtual valuations, ironing); the **revenue equivalence theorem**; individual rationality and budget balance; the **Myerson–Satterthwaite impossibility** (no mechanism achieves efficient bargaining under two-sided incomplete information — a key negative result); **Nash implementation** (Maskin monotonicity); **robust mechanism design** (Bergemann–Morris) and the **Wilson doctrine** (frontier).
- **Primary:** **Börgers, *An Introduction to the Theory of Mechanism Design*** (the best modern text); **Fudenberg & Tirole** (mechanism-design chapter); **Vohra, *Mechanism Design: A Linear Programming Approach*** (the LP view — light CS flavor); MWG ch. 23 (recap).
- **⊘ FREE:** Roughgarden's AGT lectures cover VCG and algorithmic mechanism design (the light-touch CS angle); *Algorithmic Game Theory* (NRTV).
- **Key original readings:** Myerson (1981) optimal auction design; Vickrey (1961), Clarke (1971), Groves (1973) — VCG; Myerson–Satterthwaite (1983); Maskin (1999) Nash implementation; Bergemann–Morris (2005).
- **Calibration:** the revelation principle, VCG, revenue equivalence, and Myerson–Satterthwaite are **[SETTLED]** landmark theorems. Robust mechanism design is **[FRONTIER]**. The core insight — that incentive compatibility is a *constraint* you optimize subject to — is bedrock.
- **⚡ Bridge:** mechanism design = constrained optimization (maximize the design objective subject to incentive-compatibility and individual-rationality constraints — the framing you met in micro information economics); VCG = pricing each agent their externality (Pigouvian logic); Myerson's optimal auction = an optimization over virtual valuations, with "ironing" enforcing monotonicity (a projection/isotonic-regression-like step).
- **Exercises:** apply the revelation principle to convert a mechanism to a direct one; derive VCG payments for a small allocation problem; derive Myerson's optimal reserve price; prove Myerson–Satterthwaite for uniform types.
- **Time:** 6–8 weeks.
- **MVP:** Börgers on the revelation principle + VCG + revenue equivalence + Myerson optimal auction; defer implementation theory and robust MD.

---

# PHASE 8 — Auction Theory & Market Design
*(Owed from micro — full pillar.) The theory that engineered real institutions. The program's clearest theory-to-practice win.*

- **Goal:** auction theory in full and the matching/market-design program, with its deployed successes.
- **Prerequisites:** Phase 7 (mechanism design); Phase 4 (the core, for matching).
- **Topics:**
  - **Auction theory:** the four standard auctions (English, Dutch, first-price, second-price/Vickrey); private vs. **common values** and the **winner's curse**; **revenue equivalence** (application); **optimal auctions** (Myerson, application); **interdependent values and the linkage principle** (Milgrom–Weber); multi-unit and **combinatorial auctions**; the **FCC spectrum auctions** and the incentive auction (theory built into policy); the price of anarchy of simple auctions (light algorithmic touch).
  - **Matching & market design:** **stable matching** and the **Gale–Shapley deferred-acceptance** algorithm; the marriage and college-admissions problems; matching with contracts (Hatfield–Milgrom); the **medical-residency match** (NRMP — Roth); **school choice** (Boston vs. deferred acceptance vs. top trading cycles — Abdulkadiroğlu–Sönmez); **kidney exchange** (top trading cycles; Roth–Sönmez–Ünver); the lattice structure of stable matchings; Roth's market-design program and "repugnant markets."
- **Primary:** **Krishna, *Auction Theory*** (2nd ed. — the definitive auction text); **Milgrom, *Putting Auction Theory to Work*** (the theorist-practitioner bridge); **Roth & Sotomayor, *Two-Sided Matching*** (the matching bible); **Roth, *Who Gets What — and Why*** (accessible market-design overview).
- **⊘ FREE:** Roth's course materials and market-design writings; Roughgarden's AGT lectures (combinatorial auctions, price of anarchy).
- **Key original readings:** Vickrey (1961); Milgrom–Weber (1982) affiliated values; Gale–Shapley (1962); Shapley–Scarf (1974) top trading cycles; Roth (1984) medical match; Roth–Sönmez–Ünver (2004) kidney exchange; Abdulkadiroğlu–Sönmez (2003) school choice.
- **Calibration:** auction theory and matching theory are **[SETTLED]**. Uniquely in this program, the **applications are [SETTLED] real-world successes** — spectrum auctions have raised hundreds of billions, deferred acceptance runs the residency match and multiple cities' school assignment, and kidney-exchange chains are saving lives. This is theory that *built working markets*: hold it as settled *and deployed*, not "settled theorem, unclear relevance."
- **⚡ Bridge:** deferred acceptance is a constructive algorithm converging to a fixed point; stable matchings form a lattice (a clean order-theoretic structure); combinatorial auctions are integer programs; the winner's curse is a conditional-expectation/selection effect (condition on winning).
- **Exercises:** derive the symmetric equilibrium of a first-price auction and verify revenue equivalence with the second-price; run deferred acceptance and verify stability and the lattice structure; show top-trading-cycles is strategy-proof and Pareto-efficient for house allocation.
- **Time:** 6–8 weeks.
- **MVP:** Krishna on the standard auctions + revenue equivalence + winner's curse; Gale–Shapley + top trading cycles + one deployed case (residency match or kidney exchange); defer combinatorial auctions and matching-with-contracts.

---

# PHASE 9 — Behavioral Game Theory & Social Preferences
*(Owed from behavioral — full pillar.) Where equilibrium play and self-interest meet the experimental evidence, carrying the behavioral track's calibration discipline.*

- **Goal:** the systematic departures from standard game theory — other-regarding preferences and bounded strategic reasoning — modeled formally and assessed critically.
- **Prerequisites:** Phases 1–3 (the games being tested).
- **Topics:**
  - **Social preferences:** the canonical experimental games (**ultimatum, dictator, trust/investment, public-goods, gift-exchange**); **fairness and reciprocity**; **inequity aversion** (Fehr–Schmidt; Bolton–Ockenfels ERC); **reciprocity/intentions** models (Rabin's fairness equilibrium; Dufwenberg–Kirchsteiger); the self-interest-vs-social-preference debate; **cross-cultural evidence** (Henrich et al.).
  - **Bounded strategic reasoning:** **level-k** and **cognitive hierarchy** (Stahl–Wilson; Camerer–Ho–Chong; Nagel's beauty contest); **quantal response equilibrium** (McKelvey–Palfrey); **learning models** (experience-weighted attraction — Camerer–Ho).
- **Primary:** **Camerer, *Behavioral Game Theory: Experiments in Strategic Interaction*** (Princeton — the definitive text; your spine here); the Handbook of Behavioral Economics chapters on strategic behavior.
- **⊘ FREE:** many of the source papers are freely available; experimental data via replication repositories.
- **Key original readings:** Fehr–Schmidt (1999) inequity aversion; Rabin (1993) fairness; McKelvey–Palfrey (1995) QRE; Nagel (1995) beauty contest; Camerer–Ho–Chong (2004) cognitive hierarchy; Henrich et al. (2001, 2005) cross-cultural.
- **Calibration (carrying the behavioral discipline):** **social preferences are [SETTLED]** — robust and replicating across cultures (with magnitude variation), one of behavioral economics' genuinely solid findings. The **specific model (Fehr–Schmidt vs. Rabin vs. others) is [CONTESTED]** — no consensus winner, and distributional vs. intentions-based accounts are hard to separate. **Level-k / cognitive hierarchy and QRE are [SETTLED]** as useful predictive models (they out-predict Nash in many one-shot games), though QRE's identification is debated. Apply the same critical lens as the behavioral track: robust core, contested modeling, and skepticism toward over-strong claims.
- **⚡ Bridge:** QRE = logit/softmax equilibrium (Boltzmann again — inverse temperature is the rationality parameter); level-k / cognitive hierarchy = depth-limited iterated best-response (bounded-depth reasoning, like truncated game-tree search); EWA learning = reinforcement learning with belief-based updating.
- **Exercises:** compute the level-k and QRE predictions for the beauty-contest game and compare to Nash and to data; fit a Fehr–Schmidt model to ultimatum-game rejections; state the identification problem separating inequity aversion from reciprocity.
- **Time:** 5–7 weeks.
- **MVP:** Camerer on social preferences (inequity aversion) + level-k/cognitive hierarchy + QRE; defer EWA learning and the intentions-vs-distribution debate.

---

## The MVP fast-path (compressed core, ~4–5 months)

Route to the non-cooperative core plus everything that was owed, skipping Phases 0, 4, 5, 6:

1. **Phase 1 MVP** — Nash (pure/mixed) + correlated equilibrium. *(~4 wk)*
2. **Phase 2 MVP** — SPE + Bayesian Nash + PBE + one signaling game. *(~5 wk)*
3. **Phase 3 MVP** — infinitely repeated games + the folk theorem + reputation. *(~3 wk)*
4. **Phase 7 MVP** — revelation principle + VCG + revenue equivalence + Myerson optimal auction. *(~4 wk)*
5. **Phase 8 MVP** — standard auctions + Gale–Shapley + top trading cycles + one deployed case. *(~4 wk)*
6. **Phase 9 MVP** — social preferences + level-k + QRE. *(~3 wk)*

This delivers the non-cooperative core and both discharged debts (mechanism/market design; behavioral GT/social preferences). It defers bargaining/cooperative essentials, learning/evolution, and the epistemic foundations.

---

## Total timeline

| Route | Pace | Duration |
|---|---|---|
| **Full program** (Phases 0–9) | 8–12 hrs/wk | **~11–16 months** |
| **MVP core** (above) | 8–12 hrs/wk | **~4–5 months** |

The largest track. Phases 3–6 run in parallel after Phase 2. The one phase you can cut with least loss is Phase 6 (epistemics); the ones not to compress are Phases 2, 7, and 8.

---

## Editions & currency

Game theory's canon is stable. **Osborne–Rubinstein *A Course in Game Theory* (1994), Fudenberg–Tirole (1991), Myerson (1991), Maschler–Solan–Zamir (2013/2020), Mailath–Samuelson (2006), Fudenberg–Levine (1998), Krishna 2nd ed. (2009), Roth–Sotomayor (1990), Camerer (2003)** — all current standards. **Tadelis (2013)** and **Börgers (2015)** are the freshest teaching texts. The living frontiers — robust mechanism design, algorithmic game theory, and market-design applications — move in journals and in **⊘ *Algorithmic Game Theory* / Roughgarden's lectures**; track those for current work. Free hosting is unusually generous here: **Rubinstein** (arielrubinstein.org) for the core texts and bargaining, **Polak's Yale course**, and **Roughgarden** for the CS-flavored material.

---

## What I can build next

- The **spin-offs this track's scope left open**: full **cooperative game theory** (coalition formation, values beyond Shapley) and full **algorithmic game theory** (PPAD-completeness, algorithmic mechanism design, combinatorial-auction approximation — your CS crossover, if you want it after all).
- A **week-by-week reading schedule** across Phases 0–9 against your hrs/week.
- A **problem-set companion** with the ML-mapped derivations worked in full (no-regret → correlated equilibrium, replicator = multiplicative weights, QRE as softmax equilibrium, VCG as externality pricing).
- The **combined "strategic behavior" study plan** interleaving this with the behavioral track (whose social-preference/behavioral-GT material it completes) and the micro track (whose mechanism/market-design spin-off it discharges).
- A **market-design deep dive** — a focused track on the deployed successes (spectrum auctions, matching markets, kidney exchange), which is the most directly applicable corner of everything here.