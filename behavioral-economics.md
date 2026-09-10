# Behavioral Economics: A Theory-Forward, Self-Contained Curriculum
### Intermediate foundation → research frontier · individual decision-making · calibration as the backbone

**Orientation:** theory-forward and *self-contained*. Behavioral economics is an empirical field, so "theory-forward" here means the **formal models of behavior** — prospect theory, quasi-hyperbolic discounting, salience, rational inattention — engaged alongside the experimental evidence *critically*, not a run-your-own-lab methods course. This curriculum recaps and deepens the decision-theory foundations (so it stands alone), and focuses on **individual** decision-making: social preferences and behavioral game theory are carved out for the game-theory track (see the exclusions box).

**The defining feature of this track:** calibration is the backbone, not a footnote. Behavioral economics has the worst replication record of any field in this program. Every phase tags claims **[SETTLED] / [CONTESTED] / [HYPE] / [FRONTIER]**, and the whole thing culminates in a methodology-and-replication capstone that teaches you to assign the tags yourself.

---

## Conventions

- **Calibration tags:**
  - **[SETTLED]** — robustly replicated; a solid descriptive model or phenomenon.
  - **[CONTESTED]** — real debate over magnitude, mechanism, robustness, or interpretation.
  - **[HYPE]** — popular/policy claims far outrunning the evidence.
  - **[FRONTIER]** — active research; conclusions still forming.
- **⊘ FREE** marks free resources.
- **⚡ Physics/ML bridge:** learning accelerators (independent of content weighting). Behavioral econ's frontier is, mathematically, information theory + regularized optimization + reinforcement learning wearing economics notation — several mappings are exact.
- Each phase has an **MVP fast-path**; the assembled MVP spine is at the end.

---

## Deliberately excluded (your call: "both wait for the GT track")

Held out of this curriculum entirely, for the game-theory track:

- **Social preferences** — fairness, reciprocity, inequity aversion (Fehr–Schmidt, Bolton–Ockenfels), altruism, trust, spite.
- **Behavioral game theory** — ultimatum/dictator/trust/public-goods games, level-k and cognitive hierarchy, quantal response equilibrium (QRE), learning in games (Camerer's *Behavioral Game Theory*).

Also scoped out here: **behavioral finance** (overlaps the finance track — bubbles, limits to arbitrage, disposition effect, sentiment), and **running experiments as a practice** (design, IRB, execution) — this is theory-forward, so experiments are read and critiqued, not conducted.

What remains — and what this curriculum *is*: choice under risk, reference-dependence, judgment/heuristics-and-biases, intertemporal choice and self-control, bounded rationality and attention, behavioral belief formation, behavioral welfare and nudge policy, and the methodology/replication capstone.

---

## Your background as an accelerator (the standout mappings)

1. **Dopamine reward-prediction-error = temporal-difference learning.** The Schultz–Dayan–Montague result — that midbrain dopamine encodes the TD error δ = r + γV(s′) − V(s) — is one of the most celebrated neuroscience↔ML correspondences ever. The brain's valuation system is, to a first approximation, running RL. → neuro coda.
2. **Rational inattention = rate–distortion theory.** Sims models attention as a Shannon channel-capacity constraint; the agent optimally allocates bits under a mutual-information budget. It's information theory, exactly. → Phase 6.
3. **Gabaix's sparse-max = L1 / LASSO.** Behavioral inattention is formalized as an optimization with an L1 penalty on the number of attended dimensions — the same sparsity-inducing regularization you use. → Phase 6.
4. **Quasi-hyperbolic discounting = an intrapersonal game.** A present-biased agent's "selves" play a dynamic game; the sophisticated agent solves for subgame-perfect equilibrium against future selves. Time inconsistency is game theory of one person. → Phase 5.
5. **Resource-rational analysis = bounded/approximate computation.** Lieder–Griffiths reframe "biases" as *optimal* behavior under computational cost — cognition as a constrained optimization, which partly reconciles the great rationality debate and speaks directly to an ML/optimization mindset. → Phases 4, 6.
6. **Salience / diagnostic expectations = attention weighting / overreaction perturbations to Bayesian updating.** Bordalo–Gennaioli–Shleifer's mechanisms are reweightings of a measure — recognizable from attention mechanisms and from perturbed Kalman filtering. → Phase 6.

---

## Prerequisites & co-requisites

**Math/stats (you have this):** expected utility and Bayesian updating as *benchmarks* (the things behavioral econ deviates from); probability; and — important for the calibration backbone — enough **experimental statistics literacy** to read effect sizes, confidence intervals, power, and meta-analyses critically. That statistical fluency is what makes the replication material land.

**No external co-requisite.** This is built self-contained. (If you're also doing the micro track, Phases 2–3 here overlap micro Phase 4 — skim those if fresh.)

---

## Dependency map

```
        Phase 0  Prereqs (benchmarks + stats-for-reading-papers)
             │
        Phase 1  The behavioral program: framing & the rationality benchmark
             │
        Phase 2  Choice under risk: prospect theory (deep)
             │
        Phase 3  Reference-dependence, endowment effect & framing
             │
        ┌────┴──────────┬───────────────┐
   Phase 4          Phase 5         Phase 6
   Heuristics &     Intertemporal   Bounded rationality,
   biases +         choice &        attention & belief
   rationality      self-control    formation (frontier)
   debate              │                 │
        └──────┬───────┴─────────────────┘
          Phase 7  Behavioral welfare & nudge policy
             │
        Phase 8  Methodology, replication & epistemics (capstone)
             │
        [Coda] Neuroeconomics (optional frontier)
```

**Reading:** 0→1→2→3 is the foundation chain. Phases 4, 5, 6 are largely parallel applications/extensions and can be taken in any order (4 is the calibration-heavy one; 6 is the theory frontier). Phase 7 (welfare/policy) draws on all of them. Phase 8 (methods) is the capstone and reframes everything before it. The neuro coda is optional.

---

# PHASE 0 — Prerequisites & Placement
*Light. The one thing to sharpen is reading experimental evidence critically.*

- **Goal:** lock in the neoclassical benchmarks (rational choice, EU, exponential discounting, Bayesian beliefs) that behavioral econ departs from; sharpen the statistical literacy needed to judge findings (effect sizes, CIs, power, meta-analysis, publication bias).
- **Prerequisites:** your degree.
- **Primary:** a quick benchmark recap from any micro text (utility max, EU, Bayes); for the stats-of-evidence: skim **Gelman's writing on statistical significance and the "garden of forking paths"** (⊘ free, statmodeling.stat.columbia.edu).
- **⊘ FREE:** Data Colada blog (datacolada.org) — start following it now; it's the running case study for the whole track.
- **Calibration:** benchmarks are **[SETTLED]** (they're the null hypothesis).
- **⚡ Bridge:** treat every behavioral finding as a claim with an effect size and a p-value produced under researcher degrees of freedom — the same skepticism you'd apply to an ML result with a suspicious benchmark.
- **Exercises:** none formal; get comfortable reading a results table for effect size and CI, not just significance.
- **Time:** 1–2 weeks.
- **MVP:** skip if the benchmarks and evidence-reading are already second nature.

---

# PHASE 1 — The Behavioral Program: Framing & the Rationality Benchmark
*What behavioral economics is, where it came from, and the debate that frames everything.*

- **Goal:** the history and methodological stance of the field; the neoclassical benchmark stated precisely; and the **great rationality debate** introduced up front so it colors every later phase.
- **Prerequisites:** Phase 0.
- **Topics:** the neoclassical model as benchmark (rational preferences, EU, exponential discounting, Bayesian beliefs, self-interest); the history (Simon's bounded rationality → Kahneman–Tversky's heuristics-and-biases → Thaler's anomalies → the modern mainstreaming); what "a behavioral model" is (a *disciplined* deviation from the benchmark, not "anything goes"); and the two-cultures framing — **Kahneman–Tversky (heuristics produce systematic errors) vs. Gigerenzer (heuristics are adaptive, often near-optimal)** — as the organizing tension.
- **Primary:**
  - **Sanjit Dhami, *The Foundations of Behavioral Economic Analysis*** (OUP, 2016; also a 7-volume 2nd ed.) — the rigorous, comprehensive graduate reference; your spine for the whole track. Read its introduction and the map of the field.
  - **Angner, *A Course in Behavioral Economics*** (3rd ed.) — the accessible teaching text; good for structure.
  - **Thaler, *Misbehaving*** — the field's history, first-hand and readable.
  - **Kahneman, *Thinking, Fast and Slow*** — read *with the caveat* that its dual-process framing and several cited effects are contested (Phase 4/8).
- **⊘ FREE:** MRU behavioral economics; Matthew Rabin / Stefano DellaVigna course materials where available.
- **Key original readings:** Simon (1955) "A Behavioral Model of Rational Choice"; DellaVigna (2009) "Psychology and Economics: Evidence from the Field" (JEL) — the field survey.
- **Calibration:** the framing here is meta. State plainly: behavioral economics is a **[SETTLED]** and mainstreamed research program, *and* it is the field where the **[HYPE]**-to-evidence gap is largest — both are true, and holding both is the point.
- **⚡ Bridge:** "disciplined deviation from an optimizing benchmark" is exactly how you'd think about a regularized or misspecified model relative to the Bayes-optimal one.
- **Exercises:** for three famous "anomalies," write down precisely which benchmark assumption each violates.
- **Time:** 3–4 weeks.
- **MVP:** Dhami's intro + DellaVigna's field survey; skip the popular histories.

---

# PHASE 2 — Choice Under Risk: Prospect Theory (deep)
*Self-contained recap of the decision-theory core, then deeper than micro Phase 4 went.*

- **Goal:** the anomalies of expected utility and the prospect-theory response, in full — value function, probability weighting, and the honest state of the loss-aversion evidence.
- **Prerequisites:** Phase 1.
- **Topics:** EU benchmark and its violations (**Allais**, common-ratio/common-consequence effects; **Ellsberg** ambiguity — recap); **original prospect theory** (1979): editing, the **value function** (reference-dependence, **loss aversion**, diminishing sensitivity), and **probability weighting** (overweighting small probabilities); **cumulative prospect theory** (1992) and **rank-dependence** (Quiggin); the fourfold pattern of risk attitudes; axiomatic foundations (Wakker). Then the calibration: **the loss-aversion magnitude/existence debate**.
- **Primary:**
  - **Dhami** (the risk/prospect-theory chapters) — rigorous.
  - **Wakker, *Prospect Theory for Risk and Ambiguity*** (Cambridge, 2010) — the definitive formal treatment.
  - **Kahneman & Tversky (eds.), *Choices, Values, and Frames*** — the collected foundational papers.
- **⊘ FREE:** the original papers circulate widely; Wakker's website has extensive free notes and errata.
- **Key original readings:** Kahneman & Tversky (1979) "Prospect Theory," Econometrica; Tversky & Kahneman (1992) cumulative PT; Quiggin (1982) rank-dependent utility; **Gal & Rucker (2018) "The Loss of Loss Aversion"** (the skeptical case).
- **Calibration:** **prospect theory is [SETTLED]** as a descriptive model of lab choice under risk — one of behavioral econ's genuine successes. **Loss aversion's magnitude (and in some domains its existence) is [CONTESTED]** — Gal & Rucker argue the ~2:1 coefficient is overstated and context-dependent; defenders push back; the truth is "real but smaller and more conditional than the pop version." Probability weighting is **[SETTLED]** as a phenomenon.
- **⚡ Bridge:** the value function is a utility with a kink at the reference point (a potential with a discontinuous first derivative); probability weighting is a nonlinear reweighting of the probability measure — a distorted, non-additive "measure" (Choquet capacity in CPT).
- **Exercises:** show how prospect theory resolves the Allais paradox; derive the fourfold pattern from the weighting function; state the CPT representation precisely; summarize the loss-aversion debate in a paragraph with the evidence on each side.
- **Time:** 5–7 weeks.
- **MVP:** original + cumulative prospect theory (value function + weighting) and the loss-aversion debate; defer the full axiomatics.

---

# PHASE 3 — Reference-Dependence, the Endowment Effect & Framing
*Where the reference point comes from, and a clean case study in calibration.*

- **Goal:** reference-dependence beyond risky choice — endowment effect, status quo bias, endogenous reference points, framing, and mental accounting — with the endowment-effect robustness debate as a worked example.
- **Prerequisites:** Phase 2.
- **Topics:** the **endowment effect** and the WTA–WTP gap; **status quo bias**; **reference-point formation** and **Kőszegi–Rabin** (personal equilibrium; reference points as rational expectations — a major theoretical advance); **framing effects** and preference construction; **mental accounting** and **narrow bracketing** (Thaler); the **endowment-effect-as-artifact** critique (Plott–Zeiler).
- **Primary:**
  - **Dhami** (reference-dependence chapters).
  - **Kőszegi & Rabin (2006), "A Model of Reference-Dependent Preferences,"** QJE — the key modeling paper; read closely.
  - Thaler's mental-accounting papers.
- **⊘ FREE:** most of these are freely available as working papers/author copies.
- **Key original readings:** Kahneman, Knetsch & Thaler (1990/1991) endowment effect; **Plott & Zeiler (2005)** WTA–WTP gap as procedural artifact; Thaler (1985, 1999) mental accounting.
- **Calibration:** reference-dependence as a principle is **[SETTLED]**. The **endowment effect's robustness and mechanism are [CONTESTED]** — Plott–Zeiler showed much of the classic gap can be a procedural/misconception artifact; it survives in refined designs but smaller and more conditional. Kőszegi–Rabin is **[SETTLED]** as *theory* (elegant, influential) but its specific predictions are **[CONTESTED/mixed]** empirically. Mental accounting is **[SETTLED]** as a phenomenon.
- **⚡ Bridge:** an endogenous reference point (Kőszegi–Rabin) is a fixed point — the reference point must be consistent with the behavior it induces, a self-consistency condition like a mean-field/rational-expectations equilibrium.
- **Exercises:** solve for a Kőszegi–Rabin personal equilibrium in a simple example; lay out the Plott–Zeiler critique and what survives it; construct a framing/mental-accounting example and the benchmark it violates.
- **Time:** 4–5 weeks.
- **MVP:** endowment effect + the Plott–Zeiler debate + Kőszegi–Rabin core; defer narrow-bracketing depth.

---

# PHASE 4 — Judgment Under Uncertainty: Heuristics, Biases & the Rationality Debate
*The famous half of the field — and the phase where the replication scalpel comes out.*

- **Goal:** the heuristics-and-biases program in full, the dual-process framing and its critics, and a fair, rigorous treatment of the Gigerenzer counter-program.
- **Prerequisites:** Phase 1 (independent of 2–3).
- **Topics:**
  - **Heuristics and biases (Kahneman–Tversky):** **representativeness** (base-rate neglect, the conjunction fallacy / "Linda," the gambler's fallacy, the law of small numbers); **availability**; **anchoring-and-adjustment**; conjunction and disjunction effects.
  - **Belief biases:** overconfidence and miscalibration; confirmation bias; hindsight bias; motivated reasoning.
  - **Dual-process theory:** System 1 / System 2 (Kahneman) — and its critiques as a scientific theory (it explains too much, predicts too little).
  - **The great rationality debate:** **Gigerenzer's ecological rationality** and fast-and-frugal heuristics (take-the-best, recognition heuristic) as *adaptive* rather than error-prone; **frequency formats** dissolving base-rate neglect (Gigerenzer–Hoffrage); the Kahneman–Tversky vs. Gigerenzer exchange; **resource-rational analysis** (Lieder–Griffiths) as a partial synthesis — biases as optimal under computational cost.
- **Primary:**
  - **Kahneman, Slovic & Tversky (eds.), *Judgment under Uncertainty: Heuristics and Biases*** — the classic volume.
  - **Gigerenzer, Todd & the ABC Group, *Simple Heuristics That Make Us Smart***; **Gigerenzer & Selten (eds.), *Bounded Rationality: The Adaptive Toolbox***.
  - **Dhami** (heuristics/biases chapters) for the economics-facing treatment.
- **⊘ FREE:** Gigerenzer's papers (many on his Max Planck page); the Lieder–Griffiths (2020) *BBS* target article circulates freely.
- **Key original readings:** Tversky & Kahneman (1974) "Judgment under Uncertainty," Science; Gigerenzer & Hoffrage (1995) frequency formats; the Kahneman–Tversky (1996) / Gigerenzer (1996) *Psychological Review* exchange; Lieder & Griffiths (2020) resource rationality.
- **Calibration (the crux phase):** *individual* biases vary enormously in robustness. Anchoring, base-rate neglect, and overconfidence **[largely SETTLED]** (replicate). But the **interpretation** — "heuristics = irrationality" — is **[CONTESTED]** (Gigerenzer: they're adaptive; resource rationality: they're optimal under cost). **Dual-process/System-1-2 is [CONTESTED]** as a theory despite its popularity. And several once-famous effects in the adjacent literature are **[REFUTED]** (Phase 8). Don't take the *Thinking, Fast and Slow* catalog at face value.
- **⚡ Bridge:** resource-rational analysis frames a "bias" as the optimal output of a bounded computation under a cost constraint — the exact logic of approximate inference / anytime algorithms; representativeness ≈ overweighting a likelihood ratio while underweighting the prior (a mis-set Bayesian update).
- **Exercises:** work the Linda/conjunction and base-rate problems in both probability and frequency formats; state the resource-rational account of one bias; write the strongest version of each side of the Kahneman–Tversky vs. Gigerenzer debate.
- **Time:** 6–8 weeks.
- **MVP:** the core heuristics (representativeness, availability, anchoring) + the rationality debate (Gigerenzer + resource rationality); this phase's calibration content is the reason not to compress it too hard.

---

# PHASE 5 — Intertemporal Choice & Self-Control
*Discounting anomalies and the models of a divided self.*

- **Goal:** departures from exponential discounting and the formal models of present bias and self-control.
- **Prerequisites:** Phase 1 (independent of 2–4).
- **Topics:** the exponential-discounting benchmark and its **anomalies** (present bias, preference reversals, decreasing impatience, sign/magnitude effects); **quasi-hyperbolic (β–δ) discounting** (Laibson); Strotz's dynamic inconsistency; **naïve vs. sophisticated** agents (O'Donoghue–Rabin); **temptation and self-control** (Gul–Pesendorfer axiomatic; dual-self models, Fudenberg–Levine); applications to **savings, procrastination, and addiction** (rational addiction vs. behavioral accounts); and the calibration: **how strong is present bias, really** (Andreoni–Sprenger convex-time-budget critiques).
- **Primary:**
  - **Frederick, Loewenstein & O'Donoghue (2002), "Time Discounting and Time Preference: A Critical Review,"** JEL — the definitive survey; the anchor for this phase.
  - **Dhami** (intertemporal-choice chapters).
  - **Laibson (1997)** "Golden Eggs and Hyperbolic Discounting," QJE; **O'Donoghue & Rabin (1999)** "Doing It Now or Later," AER.
- **⊘ FREE:** the survey and key papers are freely available.
- **Key original readings:** Strotz (1955); Laibson (1997); O'Donoghue–Rabin (1999); Gul–Pesendorfer (2001); Andreoni–Sprenger (2012).
- **Calibration:** present bias **[SETTLED]** as a lab phenomenon; its **magnitude and the right functional form are [CONTESTED]** — field estimates are often smaller than lab, and Andreoni–Sprenger's convex-budget methods find weaker present bias than binary-choice designs, sparking a live methods debate. Gul–Pesendorfer temptation is **[SETTLED]** as an axiomatic model, one alternative among several.
- **⚡ Bridge:** the sophisticated β–δ agent solves an **intrapersonal dynamic game** — subgame-perfect equilibrium across time-selves; discounting functions are decay kernels, and quasi-hyperbolic is exponential plus a one-shot β drop at the present.
- **Exercises:** solve a β–δ consumption-savings problem for naïve and sophisticated agents and compare; show the preference reversal that exponential discounting cannot produce; state the Andreoni–Sprenger critique.
- **Time:** 5–6 weeks.
- **MVP:** the FLO survey + β–δ discounting (naïve vs. sophisticated) + the magnitude debate; defer temptation axiomatics and addiction.

---

# PHASE 6 — Bounded Rationality, Attention & Belief Formation
*The theory frontier — and, for you, the phase with the best ML bridges.*

- **Goal:** the deeper formal models of limited cognition and attention, and behavioral models of belief formation.
- **Prerequisites:** Phase 1 (Phases 4–5 helpful).
- **Topics:**
  - **Bounded rationality foundations:** Simon's satisficing and its modern revival.
  - **Attention & cognition costs:** **rational inattention** (Sims); **sparsity / behavioral inattention** (Gabaix's sparse-max); **salience theory** (Bordalo–Gennaioli–Shleifer); **limited attention in markets** (shrouded attributes; Gabaix–Laibson).
  - **Behavioral belief formation:** over- and under-reaction; **diagnostic expectations** (Bordalo–Gennaioli–Shleifer) and extrapolation; non-Bayesian updating; overconfidence dynamics. (This is the micro-foundation behind the behavioral-macro/finance expectations you saw flagged elsewhere.)
- **Primary:**
  - **Gabaix, "Behavioral Inattention"** (Handbook of Behavioral Economics, 2019) — the definitive survey; **Gabaix (2014)** "A Sparsity-Based Model of Bounded Rationality," QJE.
  - **Sims (2003)** "Implications of Rational Inattention," JME.
  - **Bordalo, Gennaioli & Shleifer** — salience (2012) and diagnostic expectations (2018) papers.
  - **Dhami** (bounded-rationality/attention chapters).
- **⊘ FREE:** the Handbook chapter and BGS/Gabaix papers circulate as working papers; Sims's rational-inattention materials are on his site.
- **Key original readings:** Simon (1955/1956); Sims (2003); Gabaix (2014, 2019); Bordalo–Gennaioli–Shleifer (2012, 2018).
- **Calibration:** rational inattention is **[SETTLED]** as a modeling framework, **[FRONTIER]** in empirical application. Sparse-max, salience, and diagnostic expectations are **[FRONTIER]** — promising, actively tested, not yet consensus. These are where the field is *building* rather than where it's settled.
- **⚡ Bridge (the payoff cluster):** rational inattention = rate–distortion / Shannon capacity; sparse-max = L1/LASSO regularization; salience = attention weighting (reweighting inputs by contrast); diagnostic expectations = a representativeness-driven overreaction, i.e., a perturbed Bayesian/Kalman update. This phase is the closest behavioral econ gets to your day job.
- **Exercises:** solve a simple rational-inattention problem (Gaussian, quadratic loss); derive attention allocation in a two-attribute sparse-max example; show how diagnostic expectations generate over-reaction relative to Bayesian updating.
- **Time:** 6–8 weeks.
- **MVP:** Gabaix's "Behavioral Inattention" survey + one rational-inattention problem + diagnostic expectations; defer salience-theory depth.

---

# PHASE 7 — Behavioral Welfare Economics & Nudge Policy
*The normative payoff — and the sharpest [HYPE]-vs-evidence phase.*

- **Goal:** how to do welfare economics when preferences are inconsistent, and an evidence-based reckoning with nudges.
- **Prerequisites:** Phases 2–6 (draws broadly).
- **Topics:** the **normative problem** — inconsistent/constructed preferences break revealed-preference welfare, so what is the criterion?; **behavioral welfare economics** (Bernheim–Rangel's choice-theoretic foundations; the "behavioral revealed preference" problem); **libertarian paternalism and nudges** (Thaler–Sunstein); **choice architecture and defaults** (retirement-savings defaults — Madrian–Shea; organ-donation defaults — Johnson–Goldstein); the **nudge effectiveness reckoning** (DellaVigna–Linos: nudge-unit field effects far smaller than academic studies; the Mertens et al. meta-analysis and the Maier et al. publication-bias critique); **ethics** (autonomy, manipulation, transparency, "sludge"); **behavioral IO** (firms exploiting biases — Heidhues–Kőszegi, shrouded attributes); behavioral public finance.
- **Primary:**
  - **Thaler & Sunstein, *Nudge*** (read as the manifesto).
  - **Bernheim & Rangel (2009)**, QJE — the rigorous welfare foundations.
  - **Dhami** (welfare/policy chapters).
  - **DellaVigna & Linos (2022)**, Econometrica — the large-scale nudge-unit evidence.
- **⊘ FREE:** DellaVigna–Linos, Bernheim–Rangel, and the Mertens/Maier meta-analysis exchange are freely available.
- **Key original readings:** Bernheim–Rangel (2009); Madrian–Shea (2001); Johnson–Goldstein (2003); DellaVigna–Linos (2022); Mertens et al. (2022) and Maier et al. (2022) (the meta-analysis and its rebuttal); Chetty (2015) on pragmatic behavioral policy.
- **Calibration:** **nudge effectiveness is [CONTESTED, often HYPE]** — some interventions (well-designed defaults) are robust and large; many others show small, fragile effects that shrink from lab → field → publication-bias-corrected (Maier et al. found ~no residual average effect after correction; DellaVigna–Linos found ~1.4pp in nudge units vs. ~8pp in academic papers). **Behavioral welfare economics is [FRONTIER/CONTESTED]** — its normative foundations are genuinely unsettled (whose "true" preference counts?). Defaults specifically: **[SETTLED]** as effective; the ethics of using them: an open normative debate.
- **⚡ Bridge:** the behavioral-welfare problem is an identification problem — recovering a "true" utility from choices generated by a *misspecified* decision process; you can't invert behavior to welfare without a model of the bias, exactly as you can't recover ground truth from a biased estimator without modeling the bias.
- **Exercises:** state the behavioral revealed-preference problem and one proposed resolution; compute the lab-vs-field-vs-corrected effect-size gap for nudges from the readings; argue both the autonomy critique and the defense of a specific default.
- **Time:** 5–7 weeks.
- **MVP:** Bernheim–Rangel core + defaults evidence + DellaVigna–Linos and the meta-analysis debate; defer behavioral IO.

---

# PHASE 8 — Methodology, Replication & the Epistemics of Behavioral Economics
*The capstone. This is where you learn to assign the tags yourself.*

- **Goal:** the tools to evaluate any behavioral claim — external validity, the replication crisis, questionable research practices, reforms, and the fraud cases — as a coherent methodology, not a list of scandals.
- **Prerequisites:** Phases 1–7 (reframes all of them).
- **Topics:**
  - **Lab vs. field & external validity:** the Levitt–List critique; generalizability; when lab results travel and when they don't.
  - **The replication crisis:** the Open Science Collaboration's Reproducibility Project; Many Labs 1–3; **Camerer et al.** replications of experimental economics (2016) and of *Nature*/*Science* social science (2018) — what replicated (economics fared better than social psych) and what didn't.
  - **Questionable research practices:** **Simmons–Nelson–Simonsohn, "False-Positive Psychology"** (researcher degrees of freedom); **Gelman's garden of forking paths**; p-hacking, HARKing, publication bias, the file-drawer problem.
  - **Reforms:** pre-registration, registered reports, multi-lab collaborations, open data, adversarial collaboration.
  - **Effect-size realism / the casualties:** ego depletion, power posing, and much of social priming (**[REFUTED]** or badly weakened); loss-aversion magnitude and the endowment effect (**[CONTESTED]**); scarcity/cognitive-load (**[CONTESTED]**).
  - **Fraud:** the **Ariely** and **Gino** cases (both tied to the famous "sign-at-the-top" honesty study — which failed to replicate *and* was found to contain fabricated data, exposed by **Data Colada**), and Stapel (wholesale fabrication in adjacent social psychology). Treat these as a lesson in incentives and detection, stated accurately (some individual-intent questions remain legally disputed).
- **Primary:**
  - **Simmons, Nelson & Simonsohn (2011)**, Psychological Science — the paper that named the problem.
  - **Open Science Collaboration (2015)**, Science; **Camerer et al. (2016, 2018)**.
  - **Levitt & List (2007)**, JEP — external validity.
  - **Dhami** and the **Handbook of Behavioral Economics** (Bernheim–DellaVigna–Laibson, eds.) methodological chapters.
- **⊘ FREE:** **Data Colada** (the Ariely/Gino investigations, posts #98 and #109–114); the Reproducibility Project and Many Labs materials on OSF (osf.io); Gelman's blog; most of these papers are open.
- **Calibration:** this phase *is* the calibration engine. The meta-lesson: economics' experimental record is **better than social psychology's but not clean**; robust findings exist (prospect theory, anchoring, present bias, defaults), a contested middle exists (loss-aversion magnitude, endowment effect, nudge sizes, scarcity), and a refuted layer exists (ego depletion, power posing, much priming). Learn to place a new claim by asking: pre-registered? replicated? field-confirmed? effect size after publication-bias correction?
- **⚡ Bridge:** the garden of forking paths is researcher degrees of freedom inflating false positives — the same overfitting/multiple-comparisons problem you guard against with held-out sets and pre-registration; a registered report is a pre-committed analysis plan, i.e., locking the test before seeing the data.
- **Exercises:** take one "famous" behavioral finding and assess it end-to-end (original effect, replication status, field evidence, corrected effect size, tag); write your own checklist for reading a behavioral paper.
- **Time:** 4–6 weeks.
- **MVP:** Simmons–Nelson–Simonsohn + the Camerer replications + the Data Colada cases + a personal reading checklist. **Keep this in any MVP** — it's what makes the rest usable responsibly.

---

# CODA (optional) — Neuroeconomics
*Peripheral to theory-forward behavioral econ, but it contains the field's single best ML bridge.*

- **Goal:** the neural foundations of valuation and choice, at a conceptual level.
- **Topics:** the brain's valuation and reward systems; **dopamine as a reward-prediction-error signal**; neural evidence on risk, time, and attention; the promises and the early over-claims of "neuro" branding.
- **Primary:** Camerer, Loewenstein & Prelec (2005) "Neuroeconomics," JEL; Glimcher & Fehr (eds.), *Neuroeconomics: Decision Making and the Brain*.
- **Key original reading:** **Schultz, Dayan & Montague (1997)**, Science — dopamine encodes the TD prediction error.
- **Calibration:** **[FRONTIER]**; the dopamine-RPE result is **[SETTLED]** and celebrated, but be wary of **[HYPE]** in over-broad "neuro-explains-economics" claims.
- **⚡ Bridge (the best one in the whole track):** dopamine RPE = the temporal-difference error δ = r + γV(s′) − V(s). The brain's reward system is, to first order, running reinforcement learning — the deepest neuroscience↔ML correspondence there is, and directly in your wheelhouse.
- **Time:** 2–3 weeks if pursued.

---

## The MVP fast-path (compressed core, ~3–4 months)

Rigorous-but-fast route, skipping Phases 0–1, 3, 6, and the coda — but **keeping the methodology capstone**, which is non-negotiable for this field:

1. **Phase 2 MVP** — prospect theory (value function + weighting) + the loss-aversion debate. *(~4 wk)*
2. **Phase 4 MVP** — core heuristics & biases + the rationality debate (Gigerenzer + resource rationality). *(~4 wk)*
3. **Phase 5 MVP** — β–δ discounting (naïve vs. sophisticated) + the magnitude debate. *(~3 wk)*
4. **Phase 7 MVP** — behavioral welfare core + defaults + the nudge effectiveness reckoning. *(~3 wk)*
5. **Phase 8 MVP** — false-positive psychology + the Camerer replications + the Data Colada cases + a reading checklist. *(~3 wk)*

This gives you the descriptive core (risk, judgment, time), the policy payoff, and — crucially — the epistemic toolkit to use it all responsibly. It defers reference-dependence depth, the attention/belief frontier, and neuroeconomics.

---

## Total timeline

| Route | Pace | Duration |
|---|---|---|
| **Full program** (Phases 0–8 + coda) | 8–12 hrs/wk | **~9–13 months** |
| **MVP core** (above) | 8–12 hrs/wk | **~3–4 months** |

Phases 4, 5, 6 run in parallel. The one phase not to skip in any version is Phase 8 — in this field, the methodology *is* the content.

---

## Editions & currency

**Dhami, *The Foundations of Behavioral Economic Analysis*** (2016 single volume; 2nd ed. split into 7 volumes) is the rigorous spine and current. **Angner** (3rd ed.), **Wakker** (2010), **Kahneman–Slovic–Tversky** and **Kahneman–Tversky** volumes are stable classics. The living frontier is the **Handbook of Behavioral Economics** (2018–19) plus recent journal work — and, uniquely for this field, the **replication and meta-science literature moves fast**, so track OSF, Data Colada, and registered-report replications for the current status of any specific effect. Treat any pre-2015 finding as "innocent until replicated."

---

## What I can build next

- The **game-theory track** that now owes you two chunks: **social preferences** (Fehr–Schmidt, inequity aversion, reciprocity) and **behavioral game theory** (ultimatum/trust games, level-k, cognitive hierarchy, QRE, Camerer's program).
- A **behavioral finance** deep track (bubbles, limits to arbitrage, disposition effect, sentiment) — the market-facing cousin of this material.
- A **week-by-week reading schedule** across Phases 0–8 against your hrs/week.
- A **problem-set companion** with the ML-mapped derivations worked in full (rational inattention as rate–distortion, sparse-max as LASSO, β–δ as an intrapersonal game, dopamine-RPE as TD learning).
- A **critical-appraisal dossier**: a worked, tag-by-tag assessment of the 25–30 most-cited behavioral findings (replication status, field evidence, corrected effect sizes) — effectively a personal calibration reference.
- The **combined behavioral-sciences study plan** interleaving this with the micro track (whose Phase 4 it deepens) and the eventual game-theory track.