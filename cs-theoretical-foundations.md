# A Multi-Year Graduate Self-Study Curriculum in Theoretical Computer Science Foundations

## TL;DR
- This is a **12-phase, ~3–4 year** curriculum (compressible to ~15–18 months via the MVP fast-path) that carries a mathematically mature autodidact from automata/computability through the research frontier (STOC/FOCS/SODA/CCC/ITCS), built on canonical textbooks and the original seminal papers, with free legitimate PDFs flagged for the large majority of the spine.
- The **core spine** (Phases 1–7: computability → complexity → algorithms/data structures → advanced complexity) is sequential and load-bearing; the **four satellites** (logic/finite-model theory, information & coding theory, algorithmic game theory, computational geometry) are largely parallelizable modules (Phases 8–11) that plug into the spine at defined points, and a capstone research phase (Phase 12) closes the loop.
- The field is **settled** in its classical core (computability, the P/NP framework, Cook–Levin, Savitch, IP=PSPACE, PCP, Shannon's theorems) but **genuinely open** at exactly the frontier the learner wants to reach — P vs NP, whether one-way functions exist, P vs BPP, and the Unique Games Conjecture all remain unresolved as of 2026 — and I flag throughout where popular exposition overstates what is actually proved.

---

## Key Findings

**Editions/currency (verified 2026).** The load-bearing textbooks are stable: Sipser *Introduction to the Theory of Computation* is still in its **3rd edition (2013, Cengage)**; **CLRS 4th edition (MIT Press, April 5, 2022)** is current — and its own preface states, "We removed topics that were rarely taught. We dropped in their entirety the chapters on Fibonacci heaps, van Emde Boas trees, and computational geometry," so use de Berg for geometry and keep a 3rd edition around if you want vEB trees/Fibonacci heaps. Arora–Barak *Computational Complexity: A Modern Approach* remains the **2009 first edition** with the pre-publication 2007 draft free online; Cover–Thomas *Elements of Information Theory* is the **2nd edition (Wiley, 2006)**; de Berg et al. *Computational Geometry* is the **3rd edition (Springer, 2008)**; Nisan–Roughgarden–Tardos–Vazirani *Algorithmic Game Theory* is the **2007 first edition (free PDF from Cambridge)**; Roughgarden *Twenty Lectures* is **2016**; Cygan et al. *Parameterized Algorithms* is **2015 (free PDF from authors)**; Williamson–Shmoys *Design of Approximation Algorithms* is **2011 (free PDF)**.

**Free-and-legitimate spine.** An unusually large fraction of the best material is legitimately free from authors: Boaz Barak's *Introduction to Theoretical Computer Science* (full book, introtcs.org), the Arora–Barak draft, Goldreich's complexity book drafts (wisdom.weizmann.ac.il/~oded), Jeff Erickson's *Algorithms* (jeffe.cs.illinois.edu, CC-licensed), MacKay's *Information Theory, Inference, and Learning Algorithms* (inference.org.uk), Guruswami–Rudra–Sudan *Essential Coding Theory* (cse.buffalo.edu/faculty/atri), Williamson–Shmoys (designofapproxalgs.com), Cygan et al. (parameterized-algorithms.mimuw.edu.pl), Libkin *Elements of Finite Model Theory* (homepages.inf.ed.ac.uk/libkin/fmt/fmt.pdf), Pierce et al. *Software Foundations* (softwarefoundations.cis.upenn.edu), Roughgarden's lecture notes/videos, and MIT OCW (6.045/6.046/6.851). I flag each below.

**Polish heritage.** The Lvov–Warsaw school (Tarski, Łukasiewicz, Leśniewski, Mostowski, plus Presburger, Jaśkowski, Lindenbaum) is not a footnote — it is foundational to the logic satellite, and I surface it directly in Phase 8. (Fittingly, the flagship *Parameterized Algorithms* text is co-authored by a Warsaw-centered group — Cygan, Kowalik, and both Pilipczuks are at the University of Warsaw.)

---

## Details: The Phased Curriculum

### How to read this
Each phase gives (a) Goal, (b) Prerequisites, (c) Primary readings (spine: canonical books + seminal papers), (d) Supplementary, (e) Exercises/implementation, (f) Time estimate, (g) MVP fast-path. Intellectual-status tags: **[SETTLED]**, **[OPEN]**, **[HYPE-WATCH]**. Physics-scaffolding bridges are marked **⚛** and are intuition aids, not rigorous correspondences.

---

### PHASE 1 — Automata, Formal Languages & the Chomsky Hierarchy
**(a) Goal.** Fluency with finite automata (DFA/NFA), regular languages and the pumping lemma, context-free grammars and pushdown automata, the Chomsky hierarchy, and closure/decidability properties. Be able to prove languages non-regular/non-context-free and manipulate grammars.

**(b) Prerequisites.** Mathematical maturity, induction, basic discrete math. None internal.

**(c) Primary.**
- Sipser, *Introduction to the Theory of Computation*, 3rd ed. (Cengage, 2013), Part I (Ch. 0–2). The market-standard, exceptionally clean. *(Paywalled — buy it.)*
- Hopcroft, Motwani & Ullman, *Introduction to Automata Theory, Languages, and Computation*, 3rd ed. (Pearson, 2006) — reference for depth on parsing/LR(k). *(Paywalled.)*
- Seminal: Kleene (1956) on regular events; Rabin–Scott, "Finite Automata and Their Decision Problems" (*IBM J. Res. Dev.*, 1959, the Turing-Award-cited NFA paper); Chomsky (1956) "Three models for the description of language."

**(d) Supplementary.** Boaz Barak, *Introduction to Theoretical Computer Science* (**free**, introtcs.org) — note Barak deliberately starts from Boolean circuits rather than automata, a useful complementary framing.

**(e) Exercises.** Sipser Ch. 1–2 problem sets; implement a regex→NFA→DFA compiler + minimization in Python.

**(f) Time.** 3–5 weeks.

**(g) MVP.** Sipser Ch. 1–2 only; skip PDA minutiae.

⚛ *Bridge:* DFA state-transition as a discrete dynamical system/transfer matrix; the transfer-matrix method you know from 1D statistical mechanics is literally how you count accepted words of length n.

---

### PHASE 2 — Computability & Recursion Theory
**(a) Goal.** Turing machines and the Church–Turing thesis; decidability vs. recognizability; the halting problem; Rice's theorem; mapping/Turing reductions; the arithmetical hierarchy; Turing degrees; and Gödel incompleteness as it bears on computation. Be able to prove undecidability by reduction and place problems in the arithmetical hierarchy.

**(b) Prerequisites.** Phase 1.

**(c) Primary.**
- Sipser Part II (Ch. 3–6).
- Seminal papers — read the originals: **Turing (1936), "On Computable Numbers, with an Application to the Entscheidungsproblem"** (*Proc. London Math. Soc.*, ser. 2, vol. 42); **Church (1936)** on the Entscheidungsproblem; **Rice (1953), "Classes of recursively enumerable sets and their decision problems"** (*Trans. AMS*); **Gödel (1931)** incompleteness (read via a modern guide).

**(d) Supplementary.** Boolos, Burgess & Jeffrey, *Computability and Logic*, 5th ed. (Cambridge, 2007) — bridges to the logic track. Soare, *Turing Computability* (Springer, 2016) for Turing degrees and the arithmetical hierarchy at depth. **Overlaps your logic/philosophy track** — keep Gödel/Tarski's-truth here at the "as it bears on computation" level and defer full proof-theoretic treatment to that track.

**(e) Exercises.** Sipser Ch. 3–5 problems; implement a universal TM simulator and a Post-correspondence-problem search; formalize a reduction chain.

**(f) Time.** 5–7 weeks.

**(g) MVP.** Sipser Ch. 3–5; Turing 1936 + Rice 1953; skip Turing degrees.

⚛ *Bridge:* Undecidability ↔ the impossibility of a general "shortcut" oracle mirrors non-integrability/absence of closed-form solutions in dynamical systems; the halting problem's diagonal argument echoes Cantor.

---

### PHASE 3 — Core Algorithms & Amortized Analysis
**(a) Goal.** Master divide-and-conquer, dynamic programming, greedy, randomized algorithms, graph algorithms, and amortized analysis. Fluent competitive implementation and rigorous running-time proofs.

**(b) Prerequisites.** Phase 1 (for formal reasoning); can run in parallel with Phase 2.

**(c) Primary.**
- **CLRS, *Introduction to Algorithms*, 4th ed. (MIT Press, 2022)** — the standard reference; 4th ed. adds chapters on matchings in bipartite graphs, online algorithms, and machine learning, plus improved amortized-analysis/potential-function treatment. *(Paywalled.)*
- **Jeff Erickson, *Algorithms* (2019, free at jeffe.cs.illinois.edu; CC BY 4.0)** — superb on recursion/DP/flows and intuition; arguably the best free algorithms book.
- Kleinberg & Tardos, *Algorithm Design* (Pearson, 2005) — best prose on the *design process* and problem modeling. *(Paywalled.)*

**(d) Supplementary.** Roughgarden, *Algorithms Illuminated* (4 parts) + his free YouTube lectures.

**(e) Exercises.** Erickson's several-hundred exercises; a curated competitive-programming set for graph/DP fluency.

**(f) Time.** 8–10 weeks (skim if algorithms are already strong).

**(g) MVP.** Erickson chapters on recursion/DP/greedy + CLRS amortized analysis chapter; skip most if already fluent (the learner likely is).

⚛ *Bridge:* Dynamic programming = discrete Bellman/variational principle; you already have the transfer-matrix and path-integral intuition.

---

### PHASE 4 — Time & Space Complexity: P, NP, and the Classical Core
**(a) Goal.** Time/space hierarchy theorems; P, NP, coNP; **Cook–Levin**; Karp reductions and NP-completeness; space complexity: **Savitch's theorem**, L/NL, **Immerman–Szelepcsényi** (NL=coNL); PSPACE and PSPACE-completeness (TQBF); the polynomial hierarchy; EXP and provable intractability.

**(b) Prerequisites.** Phases 1–2.

**(c) Primary.**
- Sipser Part III (Ch. 7–9) for the gentle on-ramp.
- **Arora & Barak, *Computational Complexity: A Modern Approach* (Cambridge, 2009; free 2007 draft online)** — Ch. 1–5. This is the spine text for Phases 4–7.
- Papadimitriou, *Computational Complexity* (Addison-Wesley, 1994) — still the cleanest on the PH and logic-flavored complexity. *(Paywalled.)*
- Seminal: **Cook (1971), "The complexity of theorem-proving procedures"** (STOC); **Levin (1973)** (independent); **Karp (1972), "Reducibility among combinatorial problems"** (21 NP-complete problems); **Savitch (1970)**; **Immerman (1988)** and **Szelepcsényi (1987)** independently for NL=coNL; **Hartmanis–Stearns (1965)** hierarchy theorems.

**(d) Supplementary.** Goldreich, *Computational Complexity: A Conceptual Perspective* (Cambridge, 2008; **free drafts** at wisdom.weizmann.ac.il/~oded) for conceptual framing.

**(e) Exercises.** Arora–Barak Ch. 1–5 (300+ exercises with a hint set); prove ~10 NP-completeness reductions from scratch; SAT-solver mini-project.

**(f) Time.** 8–10 weeks.

**(g) MVP.** Sipser Ch. 7 + Arora–Barak Ch. 2 (NP), Ch. 3 (diagonalization), Ch. 4 (space) + Cook 1971 + Karp 1972.

**[OPEN] P vs NP** is unresolved — the Clay Mathematics Institute's official page heads it "Unsolved," and it is one of six still-open Millennium Prize Problems (only the Poincaré Conjecture has been solved). Formulated independently by Cook and Levin (1971). **[OPEN] NP vs coNP** is also open (and would separate P from NP if resolved negatively). **[HYPE-WATCH]** Periodic "proofs" of P≠NP or P=NP circulate; none has survived review (Woeginger's P-vs-NP page catalogs 100+ failed attempts).

⚛ *Bridge:* NP-hardness of ground-state problems ↔ you'll recognize Ising-model ground-state finding is NP-hard; the PH ↔ nested min–max/quantifier alternation.

---

### PHASE 5 — Randomness, Counting & Interaction
**(a) Goal.** Randomized classes BPP/RP/ZPP and their relations; the counting class #P and **the permanent** (Valiant); interactive proofs culminating in **IP=PSPACE**; the basics of pseudorandomness and derandomization; average-case complexity.

**(b) Prerequisites.** Phase 4; probability (you have this).

**(c) Primary.**
- Arora–Barak Ch. 7 (randomized computation), Ch. 8 (interactive proofs), Ch. 17 (counting), Ch. 20 (derandomization/pseudorandomness), Ch. 18 (average-case, Levin's theory).
- Seminal: **Valiant (1979), "The complexity of computing the permanent"** (#P-completeness); **Shamir (1992), "IP = PSPACE"** (*JACM*) with **Lund–Fortnow–Karloff–Nisan (1992)** on arithmetization; **Solovay–Strassen / Adleman** for randomized primality roots; **Nisan–Wigderson (1994), "Hardness vs. randomness"**; and the derandomization landmark **Impagliazzo–Wigderson (STOC 1997), "P = BPP if E requires exponential circuits: Derandomizing the XOR lemma."**

**(d) Supplementary.** Salil Vadhan, *Pseudorandomness* (**free** monograph, Foundations & Trends). Motwani & Raghavan, *Randomized Algorithms* (Cambridge, 1995).

**(e) Exercises.** Arora–Barak exercises; implement the sum-check protocol; implement Freivalds' and a Schwartz–Zippel-based tester.

**(f) Time.** 7–9 weeks.

**(g) MVP.** Arora–Barak Ch. 7–8 + Shamir 1992 + Valiant 1979.

**[OPEN] P vs BPP.** Most complexity theorists conjecture **P = BPP** (randomness is not essential for polynomial-time computation), on the strength of the Nisan–Wigderson / Impagliazzo–Wigderson hardness-vs-randomness program. This is a belief, not a theorem: Ryan Williams's *Some Estimated Likelihoods for Computational Complexity* assigns roughly 90% to "BPP ⊆ SUBEXP" and observes that "everything we know indicates that randomized computation is far, far weaker than deterministic exponential time." Treat P=BPP as the working conjecture (see Vadhan's *Pseudorandomness*, Open Problem 3.4). **[HYPE-WATCH]** "Randomized/quantum computers break all classical limits" is misleading — BPP is widely believed to equal P; the interesting power lies elsewhere.

⚛ *Bridge:* The permanent is the partition function of non-interacting bosons / a bipartite dimer model; #P-hardness of the permanent ↔ intractability of partition functions. Arithmetization in IP=PSPACE ↔ extending a discrete sum to a low-degree polynomial (analytic-continuation flavor).

---

### PHASE 6 — Circuits, Communication & Lower Bounds
**(a) Goal.** Boolean circuit complexity (AC⁰, NC, P/poly), the Karp–Lipton theorem, natural proofs as a barrier, and communication complexity as a lower-bound tool. Understand *why* lower bounds are hard (relativization, natural proofs, algebrization).

**(b) Prerequisites.** Phases 4–5.

**(c) Primary.**
- Arora–Barak Ch. 6 (circuits), Ch. 13 (communication complexity), Ch. 22–23 (proof complexity / why lower bounds are hard).
- **Kushilevitz & Nisan, *Communication Complexity* (Cambridge, 1997)** — the canonical text. *(Paywalled.)*
- Seminal: **Furst–Saxe–Sipser (1984)** and **Håstad's switching lemma (1986)** for AC⁰ lower bounds (parity); **Razborov (1985)** monotone circuit lower bounds; **Razborov–Rudich (1997), "Natural proofs"** (the barrier); **Baker–Gill–Solovay (1975)** relativization; **Yao (1979)** founding communication complexity.

**(d) Supplementary.** Jukna, *Boolean Function Complexity* (Springer, 2012). Rao–Yehudayoff, *Communication Complexity* (Cambridge, 2020) — modern.

**(e) Exercises.** Prove parity ∉ AC⁰ via the switching lemma; the fooling-set and rank lower bounds in communication complexity; discuss the log-rank conjecture.

**(f) Time.** 6–8 weeks.

**(g) MVP.** Arora–Barak Ch. 6 + Ch. 13 + Razborov–Rudich 1997.

**[OPEN]** Essentially all strong circuit lower bounds (e.g., NP ⊄ P/poly) are open; the **natural-proofs barrier** explains part of why. **[HYPE-WATCH]** Claimed circuit lower bounds routinely fail; note the three known barriers (relativization, natural proofs, algebrization) that any proof must evade.

---

### PHASE 7 — PCP, Hardness of Approximation & Advanced Complexity
**(a) Goal.** The **PCP theorem** and its equivalence with inapproximability; the label-cover/long-code machinery; Håstad's optimal inapproximability; the Unique Games Conjecture and its consequences.

**(b) Prerequisites.** Phases 4–6.

**(c) Primary.**
- Arora–Barak Ch. 11 (PCP theorem and hardness of approximation) and Ch. 22.
- Seminal — read in order: **Arora–Safra (1998), "Probabilistic checking of proofs"** (*JACM*; the PCP verifier characterization) and **Arora–Lund–Motwani–Sudan–Szegedy (1998), "Proof verification and the hardness of approximation problems"** (*JACM* 45(3):501–555) — together the PCP theorem. Then **Dinur (2007), "The PCP theorem by gap amplification"** (*JACM*) — the combinatorial reproof. **Håstad (2001), "Some optimal inapproximability results"** (*JACM* 48(4):798–859). **Khot (2002), "On the power of unique 2-prover 1-round games"** (the UGC).

**(d) Supplementary.** Dinur's gap-amplification paper is the most self-contained entry point; pair with Trevisan's lecture notes (free) and Ryan O'Donnell's *Analysis of Boolean Functions* (**free**, Cambridge 2014) for the Fourier-analytic machinery behind UGC-based hardness.

**(e) Exercises.** Work through Dinur's gap amplification; the Goemans–Williamson (1995) MAX-CUT SDP; and the **7/8 threshold for MAX-3SAT** — Håstad (2001) proved that "for any constant ε>0, it is NP-hard to find an assignment satisfying a (7/8 + ε)-fraction of the clauses of a 3-SAT instance even if one is promised that a satisfying assignment exists," which the Karloff–Zwick SDP algorithm (FOCS 1997, "a sequel to the MAX CUT algorithm of Goemans and Williamson") matches from above.

**(f) Time.** 8–10 weeks (the hardest phase).

**(g) MVP.** Arora–Barak Ch. 11 + Dinur 2007 (as the PCP entry) + Håstad 2001.

**[OPEN] The Unique Games Conjecture** remains open as of 2026. The major recent progress is the **2-to-2 Games Theorem**: Khot, Minzer & Safra, "Pseudorandom Sets in Grassmann Graph Have Near-Perfect Expansion" (FOCS 2018, DOI 10.1109/FOCS.2018.00062) — building on Khot–Minzer–Safra (STOC 2017) and Dinur–Khot–Kindler–Minzer–Safra (STOC 2018) — which proves it is NP-hard to distinguish ½-satisfiable from ε-satisfiable Unique Games instances. This is the strongest evidence to date *for* UGC but does **not** settle it (the full conjecture needs the near-perfect-completeness "1−ε vs ε" gap). Ryan Williams's calibration captures the expert view: "the present state of knowledge suggests to me that Unique Games (as usually stated) is probably intractable, but perhaps not NP-hard," and the KMS line "claims to settle the 2-to-2 conjecture, a close relative of Unique Games" — not UGC itself. **[HYPE-WATCH]** "UGC is basically proved" is wrong.

⚛ *Bridge:* PCP/gap amplification ↔ renormalization/coarse-graining — Dinur's proof repeatedly "amplifies" a constraint graph's gap while controlling alphabet size, structurally reminiscent of RG flow toward a fixed point (intuition only).

---

### PHASE 8 — Logic in CS & Finite Model Theory (Satellite)
**(a) Goal.** Propositional & first-order logic, proof theory, model theory and **finite model theory**; **descriptive complexity** (Fagin's theorem, Immerman–Vardi); lambda calculus & type theory; the **Curry–Howard correspondence**; temporal/modal logics; SAT/SMT; model checking; proof assistants. Surface the **Lvov–Warsaw school** heritage.

**(b) Prerequisites.** Phases 2 and 4 (computability + NP/PH). Descriptive complexity connects directly to Phase 4's PH.

**(c) Primary.**
- **Leonid Libkin, *Elements of Finite Model Theory* (Springer, 2004; author's free PDF at homepages.inf.ed.ac.uk/libkin/fmt/fmt.pdf)** — the spine for finite model theory and descriptive complexity.
- **Neil Immerman, *Descriptive Complexity* (Springer, 1999)** — the canonical descriptive-complexity text (chapter drafts on Immerman's UMass site).
- **Benjamin Pierce, *Types and Programming Languages* (MIT Press, 2002)** for lambda calculus/type theory *(paywalled)*; **Pierce et al., *Software Foundations* (free, softwarefoundations.cis.upenn.edu)** for Curry–Howard in a live proof assistant (Coq/Rocq).
- Seminal: **Fagin (1974), "Generalized first-order spectra and polynomial-time recognizable sets"** (NP = ∃SO — the founding descriptive-complexity theorem); **Immerman (1986)/Vardi (1982)** (P = FO+LFP over ordered structures); **Trakhtenbrot (1950)** (FO validity undecidable over finite models); **Curry (1934) & Howard (1980)** for propositions-as-types.
- **Polish/Lvov–Warsaw heritage:** **Tarski (1933/1936), "The concept of truth in formalized languages"** (foundational for model theory and semantics); **Presburger (1929)** (decidability of Presburger arithmetic — directly relevant to SMT); Łukasiewicz (many-valued logic, Polish notation); Mostowski (generalized quantifiers; the Kleene–Mostowski arithmetical hierarchy); Jaśkowski (natural deduction, independently of Gentzen; first formalized paraconsistent logic); Lindenbaum (Lindenbaum's lemma / maximalization).

**(d) Supplementary.** Huth & Ryan, *Logic in Computer Science*, 2nd ed. (Cambridge, 2004) for temporal logic/model checking; Clarke et al., *Model Checking*, 2nd ed. (MIT, 2018); Kroening & Strichman, *Decision Procedures*, 2nd ed. (Springer, 2016) for SAT/SMT. For the Lvov–Warsaw school as intellectual history: the *Stanford Encyclopedia of Philosophy* entry "Lvov–Warsaw School" (Woleński, Fall 2025 edition). **Overlaps your logic/philosophy track** — keep this satellite CS-facing (descriptive complexity, SAT/SMT, Curry–Howard) and route pure proof theory/model theory to that track.

**(e) Exercises.** Ehrenfeucht–Fraïssé games to prove FO-inexpressibility (connectivity, evenness); implement a DPLL SAT solver and a small tableau prover; do the first volumes of *Software Foundations* in Coq/Rocq; encode and type-check a proof via Curry–Howard.

**(f) Time.** 10–14 weeks (can overlap the spine).

**(g) MVP.** Libkin Ch. 1–3 + Fagin 1974 + *Software Foundations* Vol. 1 (Logical Foundations), partial.

⚛ *Bridge:* EF games ↔ locality/finite correlation length — two structures are FO-indistinguishable up to quantifier rank k roughly when a "local observer" cannot tell them apart, a combinatorial analog of finite correlation length.

---

### PHASE 9 — Information & Coding Theory (Satellite)
**(a) Goal.** Shannon entropy, mutual information, channel capacity; the source- and channel-coding theorems; rate–distortion; error-correcting codes (linear, Reed–Solomon, LDPC, polar); and **Kolmogorov/algorithmic information theory** with its links back to computability and complexity.

**(b) Prerequisites.** Probability (you have it); Phase 2 for the Kolmogorov-complexity links.

**(c) Primary.**
- **Cover & Thomas, *Elements of Information Theory*, 2nd ed. (Wiley, 2006)** — the standard. *(Paywalled.)*
- **David MacKay, *Information Theory, Inference, and Learning Algorithms* (Cambridge, 2003; free author PDF at inference.org.uk/itprnn/book.pdf — on-screen viewing licensed, print via publisher)** — physicist-friendly, superb on codes and inference.
- **Guruswami, Rudra & Sudan, *Essential Coding Theory* (free lecture-notes book, 2019/2023, cse.buffalo.edu/faculty/atri)** — the CS-facing coding-theory spine (Reed–Solomon, list decoding, polar codes, expander codes).
- Seminal: **Shannon (1948), "A Mathematical Theory of Communication"** (*Bell System Tech. J.*) — read the original; **Hamming (1950)**; **Reed–Solomon (1960)**; **Arıkan (2009)** on polar codes; **Gallager (1962)** LDPC; **Kolmogorov (1965)** and **Solomonoff (1964)/Chaitin** on algorithmic information.

**(d) Supplementary.** Roth, *Introduction to Coding Theory* (Cambridge, 2006); Li & Vitányi, *An Introduction to Kolmogorov Complexity and Its Applications*, 4th ed. (Springer, 2019) — the definitive Kolmogorov text, bridging to Phases 2/5.

**(e) Exercises.** MacKay's exercises; implement Huffman/arithmetic coding, a Reed–Solomon encoder/decoder, and an LDPC belief-propagation decoder; compute empirical vs. Shannon entropy on real data.

**(f) Time.** 8–10 weeks.

**(g) MVP.** MacKay Ch. 1–11 + Shannon 1948 + Cover–Thomas Ch. 2 & 7.

⚛ *Bridge:* This is your strongest home turf — Shannon entropy vs. Gibbs/Boltzmann entropy; free energy and the MaxEnt principle (Jaynes) ↔ inference; the partition function ↔ the normalizing constant; channel capacity via the method of types ↔ large-deviations/saddle-point. Explicitly contrast **physical (thermodynamic) entropy vs. Shannon entropy** — same functional form, different ontic status; MacKay is good on this.

---

### PHASE 10 — Algorithmic Game Theory & Mechanism Design (Satellite)
**(a) Goal.** Nash and correlated equilibria and the **computational complexity of equilibria (PPAD-completeness)**; price of anarchy/stability; auctions and mechanism design (VCG, Myerson); matching markets; online/no-regret learning and its game-theoretic connections.

**(b) Prerequisites.** Phases 3–4; Phase 6 (for PPAD/TFNP context). LP duality (Phase 11) helps for mechanism design.

**(c) Primary.**
- **Roughgarden, *Twenty Lectures on Algorithmic Game Theory* (Cambridge, 2016)** — the best modern entry; pair with his free Stanford video lectures and lecture notes (timroughgarden.org). *(Book paywalled; lectures free.)*
- **Nisan, Roughgarden, Tardos & Vazirani (eds.), *Algorithmic Game Theory* (Cambridge, 2007; free PDF from Cambridge/authors)** — the reference handbook.
- Seminal: **Nash (1950), "Equilibrium points in n-person games"** (*PNAS*) and **Nash (1951)** (*Annals of Math.*); **von Neumann (1928)** minimax; **Vickrey (1961)**, **Clarke (1971)**, **Groves (1973)** for VCG; **Myerson (1981)** optimal auctions; **Koutsoupias–Papadimitriou (1999)** price of anarchy; **Roughgarden–Tardos (2002), "How bad is selfish routing?"** (*JACM*); **Gale–Shapley (1962)** stable matching.
- PPAD landmark — read precisely: **Daskalakis, Goldberg & Papadimitriou, "The Complexity of Computing a Nash Equilibrium,"** STOC 2006 (pp. 71–78, DOI 10.1145/1132516.1132527; proved PPAD-completeness for ≥4 players), journal version *SIAM J. Comput.* 39(1):195–259, 2009 (DOI 10.1137/070699652). Then **Chen & Deng, "Settling the Complexity of Two-Player Nash Equilibrium,"** FOCS 2006 (extended to bimatrix games), journal version **Chen, Deng & Teng**, *JACM* 56(3):Art. 14, 2009 (DOI 10.1145/1516512.1516516). The class PPAD is from **Papadimitriou (1994), "On the complexity of the parity argument and other inefficient proofs of existence"** (*JCSS* 48(3):498–532).

**(d) Supplementary.** Karlin & Peres, *Game Theory, Alive* (AMS, 2017, free draft). Hartline, *Mechanism Design and Approximation* (free draft). For no-regret learning: Cesa-Bianchi & Lugosi, *Prediction, Learning, and Games* (Cambridge, 2006).

**(e) Exercises.** Implement Lemke–Howson for bimatrix Nash; compute price of anarchy for routing/load-balancing; implement a VCG auction and multiplicative-weights/no-regret dynamics and observe convergence to correlated equilibrium.

**(f) Time.** 7–9 weeks.

**(g) MVP.** Roughgarden *Twenty Lectures* Ch. 1–3, 13–17, 19–20 + Nash 1951 + DGP 2006.

**[OPEN/SETTLED nuance]** Whether **PPAD = P** is open, but Nash-equilibrium computation being PPAD-complete is settled and is strong evidence of intractability. **[HYPE-WATCH]** "Markets/games find equilibria efficiently" — the PPAD-completeness results are precisely a formal caution against assuming equilibria are efficiently computable.

⚛ *Bridge:* No-regret dynamics converging to correlated equilibria ↔ relaxational dynamics to a fixed point; potential games ↔ energy-minimizing (gradient) systems with a Lyapunov/potential function; PPAD's Brouwer fixed points ↔ existence-without-construction.

---

### PHASE 11 — Optimization, Approximation, Online, Streaming & Parameterized Algorithms (Satellite/Spine bridge)
**(a) Goal.** Linear programming & duality; network flow; approximation algorithms (LP rounding, primal–dual, SDP); online algorithms & competitive analysis; streaming/sketching; parameterized/FPT complexity; and advanced/succinct/persistent/cache-oblivious/self-adjusting data structures.

**(b) Prerequisites.** Phase 3; Phase 4 (NP-hardness) and Phase 7 (inapproximability) inform the limits.

**(c) Primary.**
- **Williamson & Shmoys, *The Design of Approximation Algorithms* (Cambridge, 2011; free PDF at designofapproxalgs.com)** — the spine for approximation.
- **Cygan, Fomin, Kowalik, Lokshtanov, Marx, Pilipczuk, Pilipczuk & Saurabh, *Parameterized Algorithms* (Springer, 2015; free PDF at parameterized-algorithms.mimuw.edu.pl)** — the FPT spine (a Warsaw-centered Polish flagship text).
- LP/duality: Bertsimas & Tsitsiklis, *Introduction to Linear Optimization* (Athena, 1997); or Vanderbei. *(Paywalled.)*
- Data structures: **Erik Demaine's MIT 6.851 *Advanced Data Structures* (free on MIT OCW, Spring 2012 video set at ocw.mit.edu; most recent offering Spring 2021; all offerings at courses.csail.mit.edu/6.851)** — covers persistent, retroactive, geometric/temporal, cache-oblivious, and succinct structures.
- Seminal: **Dantzig (1947)** simplex; **Khachiyan (1979)** ellipsoid (LP ∈ P); **Karmarkar (1984)** interior point; **Goemans–Williamson (1995)** MAX-CUT SDP; **Sleator–Tarjan (1985)** amortized analysis & splay trees; **Alon–Matias–Szegedy (1999)** streaming/frequency moments; **Downey–Fellows** founding FPT (see their *Fundamentals of Parameterized Complexity*, Springer 2013).

**(d) Supplementary.** Vazirani, *Approximation Algorithms* (Springer, 2001); Borodin & El-Yaniv, *Online Computation and Competitive Analysis* (Cambridge, 1998); McGregor's streaming surveys; Demaine's OCW 6.046.

**(e) Exercises.** Implement simplex + verify duality; LP-rounding for vertex cover and set cover; primal–dual for facility location; GW MAX-CUT with an SDP solver; a bounded-search-tree FPT algorithm for vertex cover + a kernelization; implement a persistent balanced BST and a cache-oblivious B-tree.

**(f) Time.** 10–12 weeks.

**(g) MVP.** Williamson–Shmoys Ch. 1–7 + Cygan et al. Part I + Demaine 6.851 lectures on persistence & cache-obliviousness.

**[OPEN]** The **Exponential Time Hypothesis (ETH)** and **Strong ETH (SETH)** of Impagliazzo–Paturi(–Zane) are unproven conjectures (stronger than P≠NP) now central to fine-grained complexity; treat them as working hypotheses, not theorems.

⚛ *Bridge:* LP duality ↔ Lagrangian duality/Legendre transform from mechanics/thermo; SDP relaxations ↔ mean-field/semidefinite relaxations of spin Hamiltonians; competitive analysis ↔ worst-case/adversarial bounds.

---

### PHASE 12 — Computational Geometry + Capstone / Frontier (Satellite + Research)
**(a) Goal.** Convex hulls, Voronoi diagrams & Delaunay triangulations, arrangements, range searching, geometric data structures, LP-type problems, randomized incremental construction, mesh generation — then transition to reading and producing frontier research.

**(b) Prerequisites.** Phases 3, 5 (randomization), 11.

**(c) Primary.**
- **de Berg, Cheong, van Kreveld & Overmars, *Computational Geometry: Algorithms and Applications*, 3rd ed. (Springer, 2008)** — the canonical text (needed because CLRS 4th ed. removed its geometry chapter). *(Paywalled.)*
- Seminal: **Graham (1972)** convex-hull scan; **Shamos–Hoey (1975)** Voronoi/sweep; **Clarkson–Shor (1989)** randomized incremental construction & its analysis; **Fortune (1987)** sweepline Voronoi; **Matoušek–Sharir–Welzl** for LP-type problems.

**(d) Supplementary.** Matoušek, *Lectures on Discrete Geometry* (Springer, 2002); Edelsbrunner, *Algorithms in Combinatorial Geometry* (Springer, 1987).

**(e) Exercises.** Implement Graham scan, Fortune's sweepline Voronoi, Delaunay via RIC, and a kd-tree/range tree; handle robustness/degeneracies.

**Capstone / frontier practice.**
- Replicate 2–3 landmark papers end-to-end (proofs + implementation where possible).
- Track venues: **STOC, FOCS, SODA, CCC, ITCS**; ECCC (eccc.weizmann.ac.il) and arXiv cs.CC/cs.DS for preprints; *Bulletin of the EATCS* surveys; *Theory of Computing* (open access); Simons Institute program videos.
- Surveys/monographs for the frontier: Wigderson, *Mathematics and Computation* (Princeton, 2019; free author PDF); O'Donnell, *Analysis of Boolean Functions* (free); Moore & Mertens, *The Nature of Computation* (Oxford, 2011) — the single best physicist-facing overview of the whole field.

**(f) Time.** Geometry 6–8 weeks; capstone ongoing.

**(g) MVP.** de Berg Ch. 1–7, 9, 11 + Clarkson–Shor 1989; then jump to the capstone.

**[OPEN — the frontier the learner wants]** Beyond P vs NP: **whether one-way functions exist** — the foundational open assumption of cryptography — was given a sharp characterization by **Liu & Pass, "On One-way Functions and Kolmogorov Complexity," FOCS 2020** (pp. 1243–1254, DOI 10.1109/FOCS46700.2020.00118; full version ePrint 2020/423): one-way functions exist **iff** the time-bounded Kolmogorov complexity K^t is mildly hard-on-average — the first natural problem whose average-case hardness exactly characterizes one-way functions, tightly linking your crypto track to meta-complexity. The existence question itself remains open (their existence would imply P≠NP, but not conversely). Also open as of 2026: P vs BPP, UGC, ETH/SETH, and most circuit lower bounds.

⚛ *Bridge:* Randomized incremental construction's backwards analysis ↔ expectation over random insertion order (probabilistic method); Delaunay triangulations ↔ the empty-circumcircle/energy-minimizing meshes used in finite-element physics.

---

## Dependency Map

```
Phase 1 (Automata) ──► Phase 2 (Computability) ──► Phase 4 (P/NP/Space)
      │                                                │
      └──────────────► Phase 3 (Algorithms) ───────────┤
                              │                         │
                              │                         ▼
                              │                  Phase 5 (Random/Counting/IP)
                              │                         │
                              │                         ▼
                              │                  Phase 6 (Circuits/Comm)
                              │                         │
                              │                         ▼
                              │                  Phase 7 (PCP/Hardness)
                              │
   SATELLITES (attach where noted; largely parallel):
   Phase 8  (Logic/FMT)      ← needs Phases 2 & 4
   Phase 9  (Info/Coding)    ← needs probability (+ Phase 2 for Kolmogorov)
   Phase 10 (Game Theory)    ← needs Phases 3–4 (+ 6 for PPAD, + 11 for MD)
   Phase 11 (Approx/FPT/DS)  ← needs Phase 3 (+ 4 & 7 for limits)
   Phase 12 (Geometry+Capstone) ← needs Phases 3, 5, 11
```

**Sequential trunk (do in order):** 1 → 2 → 4 → 5 → 6 → 7.
**Can start early / run in parallel:** Phase 3 (with/after Phase 1); Phase 9 (any time after basic probability); Phase 11 (after Phase 3).
**Attach points:** Phase 8 after 4; Phase 10 after 4 (finish after 6/11); Phase 12 last.

---

## Overall MVP Fast-Path (~15–18 months part-time)
1. **Foundations (compressed):** Sipser Ch. 1–5, 7 + Turing 1936, Rice 1953, Cook 1971, Karp 1972. *(Phases 1–2, 4 core.)*
2. **Complexity spine:** Arora–Barak Ch. 2–4, 7–8, 11 + Shamir 1992 + Dinur 2007. *(Phases 4–7 core.)*
3. **Algorithms/limits:** Erickson (DP/flows) + Williamson–Shmoys Ch. 1–7 + Cygan et al. Part I. *(Phases 3, 11.)*
4. **One satellite of choice at depth** — given the ML/physics profile, **Phase 9 (Information & Coding, via MacKay)** is the highest-leverage and most scaffolded onto existing knowledge; **Phase 10 (AGT)** is second for its ML/no-regret connections.
5. **Capstone:** pick one open-problem area (recommend derandomization or hardness-of-approximation), read the seminal papers, and start tracking ECCC/arXiv.

---

## Recommendations

**Staged plan.**
1. **Months 0–6:** Phases 1–2 + start Phase 3 in parallel. Benchmark to advance: prove undecidability by reduction and place a problem in the arithmetical hierarchy without aids.
2. **Months 6–15:** Phase 4 → 5, with Phase 9 (Information/Coding) running in parallel as your scaffolded satellite. Benchmark: reproduce the Cook–Levin proof and the IP=PSPACE sum-check from memory.
3. **Months 15–30:** Phases 6 → 7 (the hard core), with Phase 11 in parallel. Benchmark: work through Dinur's gap amplification and one Håstad inapproximability result.
4. **Months 30–42:** Phases 8, 10, 12 as interest dictates, then the capstone. Benchmark: replicate a recent STOC/FOCS paper and draft a short note or open-problem writeup.

**Thresholds that change the plan.** If algorithms are already strong (likely), compress Phase 3 to CLRS amortized analysis + Erickson flows and reclaim ~6 weeks. If you gravitate to average-case/meta-complexity, promote Phase 5's average-case material and the Liu–Pass line and coordinate tightly with your crypto track. If lower bounds fascinate you, weight Phase 6 heavily and pursue O'Donnell's Boolean-functions machinery early.

**Problem sources (best per area).** Arora–Barak (300+ complexity exercises w/ hint set); Sipser (computability); Erickson (algorithms, hundreds); MacKay (information theory); Williamson–Shmoys and Cygan et al. (approximation/FPT); de Berg (geometry); Kushilevitz–Nisan (communication). For quals-style breadth, use MIT OCW 6.045/6.046 problem sets and Berkeley/Stanford/CMU theory-qual archives.

**Video courses (all free).** MIT OCW 6.045 (automata/computability/complexity), 6.046 (algorithms), 6.851 (Demaine, advanced data structures); Roughgarden's algorithms and AGT lectures on YouTube; Ryan O'Donnell's CMU complexity and analysis-of-Boolean-functions lectures on YouTube; Simons Institute program talks.

**Frontier-tracking shortlist.** ECCC and arXiv (cs.CC, cs.DS); *Theory of Computing* (open access); *Bulletin of the EATCS* surveys; STOC/FOCS/SODA/CCC/ITCS proceedings; blogs by Scott Aaronson (Shtetl-Optimized), Lance Fortnow & Bill Gasarch (Computational Complexity), and Terence Tao for adjacent math.

---

## Caveats
- **Free-PDF legality:** the author-hosted/OCW links above (Barak, Erickson, MacKay, Williamson–Shmoys, Cygan et al., Guruswami–Rudra–Sudan, Libkin, Immerman drafts, Goldreich drafts, Software Foundations, Arora–Barak 2007 draft, Vadhan, O'Donnell, Wigderson) are legitimately free. Third-party PDF mirrors (Scribd, random GitHub dumps, konkur.in, etc.) for in-copyright books (Sipser, CLRS, Cover–Thomas, de Berg, Papadimitriou, Kushilevitz–Nisan, Pierce) are **not** authorized — buy those.
- **Edition drift:** editions verified as of 2026; I found no announced new editions of Sipser (3rd/2013), Arora–Barak (2009), Cover–Thomas (2006), or de Berg (3rd/2008). CLRS is at 4th (2022); the 4th ed. dropped Fibonacci heaps, van Emde Boas trees, and computational geometry, so keep a 3rd edition (or supplements) if you want those. If a Sipser 4th or Arora–Barak 2nd appears, prefer it.
- **Overlap management:** Phases 2 and 8 deliberately touch Gödel/Tarski and proof theory that your logic/philosophy track covers in depth, and Phase 12's one-way-functions material touches your crypto track — I've kept those CS-facing here and flagged where to defer.
- **Calibration:** I've tagged open problems (P vs NP, NP vs coNP, one-way functions, P vs BPP, UGC, ETH/SETH, circuit lower bounds) as genuinely unresolved; treat any source claiming otherwise skeptically. The 2-to-2 Games Theorem (KMS 2018) is real and major but does **not** prove UGC; P=BPP is a well-founded conjecture, not a theorem.
- **Scope realism:** this is a genuine multi-year program; the time estimates assume serious part-time study (~10–15 hrs/week) by someone with strong math maturity. Depth-over-breadth — the full spine plus one satellite at research depth — is a more realistic path to the frontier than uniform coverage of all four satellites.