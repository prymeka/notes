# A Multi-Year Autodidact Curriculum in Neuroscience
### Molecular → Cellular → Systems → Cognitive · biology-first · standalone

## TL;DR
- **A ~32–44 month, part-time (≈8–12 hrs/week) standalone program in 9 phases** that builds neuroscience from the biophysics of a single neuron up to cognition, disorders, and the connectomics frontier — aiming at **deep mechanistic mastery + the ability to critically read the primary literature** (*Neuron*, *Nature Neuroscience*, *J. Neurosci.*) + informed fluency. A compressed **~10–12 month MVP fast-path** gets you to solid literacy and paper-reading competence.
- **Scope you set:** balanced weight across all four levels (molecular, cellular, systems, cognitive); **ML/AI bridges kept light** (neuroscience on its own terms — no predictive-coding-as-deep-learning framing); **no computational-modeling endpoint**, so the projects are consolidation-and-appraisal exercises, not a modeling track. Your **physics background is still used as scaffolding** for the biophysics (the action potential *is* a coupled ODE/cable system; ion-channel gating *is* a stochastic two-state process) — that's a cross-domain accelerator, distinct from the ML bridges, so it stays.
- **Anchor texts (all verified current, Sept 2026):** Kandel *Principles of Neural Science* **6e (2021)**; Purves *Neuroscience* **7e (2023)**; Bear, Connors & Paradiso *Neuroscience: Exploring the Brain* **4e/Enhanced (2015–16)**; Gazzaniga, Ivry, Mangun, Bassett & Phelps *Cognitive Neuroscience: The Biology of the Mind* **6e (2024)**. Strong **free** anchors exist (Purves 2e on NCBI Bookshelf; Henley's *Foundations of Neuroscience* OER; MIT OCW 9.13; BrainFacts.org).

---

## Key Findings

**1. The canonical spines are stable and freshly updated.** All four "bibles" are current: Kandel 6e (2021) even added chapters on brain–machine interfaces and decision-making; Gazzaniga's cognitive text went to 6e in 2024 with network-neuroscientist Dani Bassett and affective-neuroscientist Elizabeth Phelps joining the author team. You are buying into editions that will remain current for years.

**2. The molecular/cellular foundation is where your physics pays off most — and it's the true gate.** Membrane excitability, cable theory, and channel gating are quantitative biophysics you can move through faster than a typical biology student, but everything above (systems, cognitive) depends on getting the single-neuron and synapse picture right first. This is a strict dependency, not a preference.

**3. "Critical literature reading" needs its own methods strand.** Reading *Nature Neuroscience* competently is less about knowing facts and more about knowing what an experiment can and cannot show — electrophysiology, optogenetics, calcium imaging, fMRI, EEG/MEG, and the statistical pitfalls specific to neuroscience (circular analysis, the multiple-comparisons problem in imaging). This strand is built in from Phase 0 and deepened method-by-method as each level introduces its tools.

**4. Excellent free/open resources are verified and sufficient for most of the arc**: Purves *Neuroscience* 2nd ed. (2001) full text on **NCBI Bookshelf**; Casey Henley's **CC-licensed *Foundations of Neuroscience*** (Michigan State, 2021) and Austin Lim's **Open Neuroscience Initiative** (DePaul); **MIT OpenCourseWare 9.13 *The Human Brain*** (Nancy Kanwisher, full video lectures); **BrainFacts.org** (Society for Neuroscience); the **Allen Brain Atlas**; and the **FlyWire Codex** connectome explorer. The paywalled flagships are worth buying but are not strictly required to make progress.

**5. The field's live edges are genuinely exciting and worth reading as frontier, not settled canon**: the first complete adult-fly connectome landed in a nine-paper *Nature* package in October 2024 (~140,000 neurons, >50M synapses), mouse-cortex connectomics followed in 2025, and the consciousness-theory adversarial collaborations are actively unresolved. These are flagged **OPEN**, not taught as fact.

---

## Details: The Phased Curriculum (Full Arc)

**Conventions.** Effort assumes a working ML engineer studying seriously ~8–12 hrs/week. Calibration tags: **SETTLED** (established consensus), **CONTESTED** (actively debated), **OPEN** (genuinely unresolved), **HYPE-WATCH** (overclaimed in popular/some academic sources). Free = openly/legally free; Paywalled = purchase/library. Editions marked "verified" were confirmed against publisher pages in Sept 2026. **[Physics bridge]** flags where a physics intuition accelerates a biological mechanism — these stay biological, not ML.

Because you weighted **all four levels** equally, the arc is: Phases 1–3 = molecular/cellular; Phases 4–5 = systems; Phases 6–7 = cognitive; Phase 8 = clinical + frontier integration. Phase 0 runs first and partly in parallel throughout.

---

### PHASE 0 — Orientation: neuroanatomy scaffold + how to read the literature (foundational, partly parallel)
**Goal:** Acquire the anatomical vocabulary you'll need everywhere, and the experimental-logic + statistics toolkit that makes paper-reading possible. These are two parallel strands that begin now and never really stop.
**Prerequisites:** None (leverages your existing statistics/Python).

**Primary readings:**
- **Neuroanatomy scaffold:** Blumenfeld H, *Neuroanatomy through Clinical Cases*, **2nd ed. (Sinauer, 2010; ISBN 9780878930586)** — the accessible standard that teaches anatomy by function and case (verify whether a newer edition has appeared; 2e is the widely used one). **SETTLED.** Free alternative: the neuroanatomy chapters of Purves *Neuroscience* 2e on **NCBI Bookshelf** (NBK10799, free) and **BrainFacts.org**'s 3D brain.
- **Reading-the-literature toolkit:** work the neuroscience-specific parts of experimental design and statistics. Start with a short, rigorous refresher you can do fast given your background, then read the field's cautionary landmark: Eklund A, Nichols TE, Knutsson H (2016), "Cluster failure: why fMRI inferences for spatial extent have inflated false-positive rates," *PNAS* 113(28):7900–7905 — why a generation of imaging results needed re-examination. **SETTLED** (as a methodological correction). Pair with Kriegeskorte N et al. (2009), "Circular analysis in systems neuroscience: the dangers of double dipping," *Nature Neuroscience* 12:535–540. **SETTLED.**

**Supplementary / FREE:** the "dead salmon" poster — Bennett CM et al. (2009), neural correlates in a post-mortem Atlantic salmon — as a memorable illustration of the multiple-comparisons problem (later written up, *J. Serendipitous Unexpected Results*, 2010); the *Nature Neuroscience* and *Neuron* "how to read a paper" author guidelines.

**Project / active-learning task:** Build a one-page "brain map" (major divisions, lobes, key nuclei, the main pathways) from memory, then check it. Separately, take one recent open-access *Nature Neuroscience* paper and write a structured appraisal: what was measured, what was manipulated, what the controls rule out, and what the statistics do and don't license. **[Physics bridge]** treat the appraisal like reading an experimental-physics paper — separate the raw observable from the inferred quantity and the model assumptions bridging them.
**Time:** 6–8 weeks to a working baseline; then it runs in the background.
**Currency notes:** Verify whether Blumenfeld has a newer edition. Statistics content is stable; imaging-stats reforms are settled.

---

### PHASE 1 — Cellular & molecular neuroscience I: the neuron and membrane excitability
**Goal:** Master how a single neuron generates and propagates signals — resting potential, the action potential, cable properties, ion channels. This is your comparative-advantage phase.
**Prerequisites:** Phase 0 optional; basic biochemistry (folded in as needed — cell membranes, proteins).

**Primary readings:**
- Kandel *Principles of Neural Science* 6e (2021), Parts II–III (cell & molecular biology of neurons; membrane excitability). **SETTLED.** *This is your spine text for Phases 1–7.*
- Bear, Connors & Paradiso *Neuroscience: Exploring the Brain* 4e/Enhanced (2015–16), Chs. 2–4 — the friendliest first pass on the neuron and the action potential. **SETTLED.**

**Primary landmark paper (read in full — and it's quantitative):**
- Hodgkin AL & Huxley AF (1952), "A quantitative description of membrane current and its application to conduction and excitation in nerve," *J. Physiol.* 117(4):500–544. The foundational quantitative model of the action potential; Nobel 1963. **SETTLED.** **[Physics bridge]** this is a system of coupled nonlinear ODEs with voltage-dependent conductances — you can read it the way you'd read a dynamical-systems paper, and the "cable equation" for propagation is a diffusion-type PDE.

**Supplementary (deeper, physics-friendly — optional):**
- Hille B, *Ion Channels of Excitable Membranes*, **3rd ed. (Sinauer, 2001; ISBN 9780878933211)** — the definitive biophysics of ion channels; gating as stochastic state transitions. **SETTLED** (still the reference despite its age; verify no newer edition). **[Physics bridge]** channel gating is literally statistical mechanics of a few-state system.
- Izhikevich EM, *Dynamical Systems in Neuroscience: The Geometry of Excitability and Bursting* (MIT Press, 2007) — excitability via bifurcation theory. Mathematical, biological (not ML), optional deep-dive squarely in your wheelhouse. **SETTLED.**
- Levitan IB & Kaczmarek LK, *The Neuron: Cell and Molecular Biology*, **4th ed. (Oxford, 2015; ISBN 9780199773893)** — molecular depth on the neuron. **SETTLED** (verify edition).

**Project / active-learning task:** Work through the Hodgkin–Huxley model by hand to understand each current's role, then reproduce the action-potential waveform numerically (a legitimate mechanistic exercise, not a "modeling track"). Optional extension: show how changing a single conductance changes threshold or refractory period. **[Physics bridge]** connect the refractory period and all-or-none behavior to the model's nonlinearity.
**Time:** 3–4 months (fast for you on the quantitative parts; take time on the biology).
**Currency notes:** Hille and Levitan are older but canonical — verify current editions before purchase; content is SETTLED.

---

### PHASE 2 — Cellular & molecular neuroscience II: synaptic transmission & neurochemistry
**Goal:** Master how neurons communicate — chemical and electrical synapses, neurotransmitter release, receptors, and the major transmitter systems.
**Prerequisites:** Phase 1.

**Primary readings:**
- Kandel 6e, Part III (synaptic transmission — neuronal excitability, transmitters, transmitter release). **SETTLED.**
- Purves *Neuroscience* 7e (2023), the synaptic-transmission and neurotransmitter units — clear and current. **SETTLED.** (Free fallback: Purves 2e on NCBI Bookshelf.)

**Primary landmark papers (read in full):**
- Neher E & Sakmann B (1976), "Single-channel currents recorded from membrane of denervated frog muscle fibres," *Nature* 260:799–802 — the patch clamp; Nobel 1991. **SETTLED.** **[Physics bridge]** you are watching a single stochastic molecular machine open and close in real time.
- Katz & Miledi's quantal-release work (1960s–70s) — the vesicular/quantal nature of transmission (read a review or the Kandel synthesis if the primary papers are hard to source). **SETTLED.**

**Supplementary:**
- Siegel GJ et al. (eds.), *Basic Neurochemistry*, **8th ed. (Academic Press, 2012; ISBN 9780123749475)** — reference for transmitter systems and metabolism (older editions free on NCBI Bookshelf; verify current edition). **SETTLED.**
- Any current *Nature Reviews Neuroscience* review on a transmitter system of interest (dopamine, glutamate) — good bridge into review-literature reading.

**Project / active-learning task:** Build a reference table of the major neurotransmitter systems: synthesis → packaging → release → receptor families (ionotropic vs metabotropic) → reuptake/degradation → where the pathways live. This table becomes load-bearing for the systems, cognitive, clinical, and (light) pharmacology touch-points later. Optional: analyze a published miniature-EPSC recording to see quantal amplitude distributions.
**Time:** 3–4 months.
**Currency notes:** *Basic Neurochemistry* and the classic release papers are older — verify editions; mechanisms are SETTLED.

---

### PHASE 3 — Plasticity, learning & memory mechanisms + neural development
**Goal:** Understand how synapses and circuits change (LTP/LTD, molecular basis of memory) and how the nervous system wires itself (development, guidance, critical periods). These two pillars are grouped because both are about *change* in neural connectivity.
**Prerequisites:** Phases 1–2.

**Primary readings:**
- Kandel 6e — synaptic plasticity and the cellular/molecular mechanisms of learning and memory; plus the development section. **SETTLED.**
- Purves 7e — the neural-development unit (a strength of this text). **SETTLED.**

**Primary landmark papers (read in full):**
- Bliss TVP & Lømo T (1973), "Long-lasting potentiation of synaptic transmission in the dentate area of the anaesthetized rabbit…," *J. Physiol.* 232(2):331–356 — the discovery of LTP, foundation of synaptic-plasticity research. **SETTLED.**
- A representative Kandel *Aplysia* paper on the molecular basis of learning-related synaptic change (Nobel 2000) — read one primary paper plus his Nobel lecture as synthesis. **SETTLED** (mechanism); the **synaptic-plasticity-and-memory hypothesis** as *the* substrate of memory remains **CONTESTED** at the strong form.

**Supplementary:**
- Sanes DH, Reh TA & Harris WA, *Development of the Nervous System*, **4th ed. (Academic Press, 2019; ISBN 9780128039960)** — the standard developmental-neuro text. **SETTLED** (verify edition).
- Hebb's *The Organization of Behavior* (1949) — read the famous plasticity passage in its original framing (historical). **SETTLED** as origin.

**Project / active-learning task:** Diagram the molecular cascade of NMDA-receptor-dependent LTP (induction → expression → maintenance), citing which steps are SETTLED and which are still CONTESTED. Separately, trace one axon-guidance decision (e.g., commissural axons at the midline) from cue to receptor to cytoskeletal response.
**Time:** 3–4 months.
**Currency notes:** Memory-mechanism debates are live at the edges (e.g., engram cells, memory allocation) — flag as CONTESTED/OPEN when you read recent work.

---

### PHASE 4 — Systems neuroscience I: neural coding + the sensory systems
**Goal:** Move from single cells to circuits: how populations of neurons represent information, and how each sensory system transduces and processes the world. Vision gets the deep dive (best-understood system); audition, somatosensation, and the chemical senses follow.
**Prerequisites:** Phases 1–2 (hard); Phase 3 helpful.

**Primary readings:**
- Kandel 6e, Part IV (Perception) — the systems/sensory backbone. **SETTLED.**
- Purves 7e — sensory-systems units (well-illustrated). **SETTLED.**

**Primary landmark papers (read in full):**
- Hubel DH & Wiesel TN (1962), "Receptive fields, binocular interaction and functional architecture in the cat's visual cortex," *J. Physiol.* 160(1):106–154 — receptive fields, orientation selectivity, cortical columns; Nobel 1981. **SETTLED.**
- Quian Quiroga R, Reddy L, Kreiman G, Koch C & Fried I (2005), "Invariant visual representation by single neurons in the human brain," *Nature* 435:1102–1107 — the "concept cell"/"Jennifer Aniston neuron." **SETTLED** finding; its interpretation (sparse vs distributed coding, the "grandmother cell" debate) is **CONTESTED**.
- Optional (methods that transformed the field): Denk W, Strickler JH & Webb WW (1990), "Two-photon laser scanning fluorescence microscopy," *Science* 248:73–76. **SETTLED.**

**Supplementary (vision deep-dive, free):**
- Wandell BA, *Foundations of Vision* — the updated edition is **freely available online** (foundationsofvision.stanford.edu). **SETTLED.**
- A current *Annual Review of Neuroscience* piece on population coding, to practice review-reading. **[Physics bridge]** population coding connects naturally to information theory (mutual information, Fisher information) — engage it that way, staying on the neuroscience.

**Project / active-learning task:** Map the retina-to-V1 pathway end to end and explain, mechanistically, how orientation selectivity could arise from the wiring. Then use the **FlyWire Codex** (free) to trace a small sensory circuit in the fly connectome and describe its likely function. Optional quantitative extension: compute a tuning curve from a published spike dataset.
**Time:** 5–7 months (large phase; vision alone is deep).
**Currency notes:** Sensory coding has active edges — flag recent claims appropriately.

---

### PHASE 5 — Systems neuroscience II: motor control, neuromodulation & homeostatic systems
**Goal:** How the brain acts on the world (motor hierarchy, cerebellum, basal ganglia) and how global states are set (neuromodulatory systems, hypothalamus/autonomic, sleep, reward).
**Prerequisites:** Phases 1–2, 4.

**Primary readings:**
- Kandel 6e, Parts V–VII (Movement; the unconscious/autonomic and homeostatic control; and the sections on modulatory systems). **SETTLED.**
- Purves 7e — motor-systems and modulatory-systems units. **SETTLED.**

**Primary landmark papers (read in full):**
- Newsome WT, Britten KH & Movshon JA (1989), "Neuronal correlates of a perceptual decision," *Nature* 341:52–54, and the companion MT-microstimulation work (Salzman, Britten & Newsome, 1990) — linking neural activity causally to perception/behavior; a template for rigorous systems experiments. **SETTLED.**
- Optional (methods revolution — read for how modern systems causal claims are made): Boyden ES, Zhang F, Bamberg E, Nagel G & Deisseroth K (2005), "Millisecond-timescale, genetically targeted optical control of neural activity," *Nat. Neurosci.* 8:1263–1268 — optogenetics. **SETTLED.**

**Supplementary:**
- A current review on the basal ganglia and action selection, and one on the ascending arousal/sleep systems.
- Reward/dopamine: read a primary Schultz reward-prediction-error paper (e.g., Schultz, Dayan & Montague, 1997, *Science*) **for the neuroscience** — note in one line that this later influenced reinforcement learning, but per your scope we keep the ML connection light and stay on the biology. **SETTLED** (dopamine RPE signal); strong "the brain is doing RL" claims are **CONTESTED**.

**Project / active-learning task:** Diagram the motor hierarchy from intention to muscle, then explain what the cerebellum and basal ganglia each contribute and how their disorders (ataxia; Parkinsonism) map onto the circuit. Optional: trace the dopaminergic projections and the systems they modulate.
**Time:** 4–6 months.
**Currency notes:** Reward and decision circuitry are active areas — flag CONTESTED where appropriate.

---

### PHASE 6 — Cognitive neuroscience I: methods + attention, memory systems, and higher perception
**Goal:** Enter human cognitive neuroscience: first the tools (fMRI, EEG/MEG, TMS, lesion studies) and their inferential limits, then attention and the memory systems.
**Prerequisites:** Phases 1–5 for mechanism; Phase 0 methods strand matured.

**Primary readings:**
- Gazzaniga, Ivry, Mangun, Bassett & Phelps, *Cognitive Neuroscience: The Biology of the Mind*, **6e (2024)** — Chs. on methods, attention, and memory. **SETTLED.** *This is your spine for Phases 6–7.*
- Kandel 6e, Part VIII/IX (higher cognitive function; from perception to action) as the mechanistic complement. **SETTLED.**

**Primary landmark paper + case (read in full):**
- The patient H.M. literature — Scoville WB & Milner B (1957), "Loss of recent memory after bilateral hippocampal lesions," *J. Neurol. Neurosurg. Psychiatry* 20(1):11–21 — the founding case for declarative-memory systems. **SETTLED.**
- Maguire EA et al. (2000), "Navigation-related structural change in the hippocampi of taxi drivers," *PNAS* 97(8):4398–4403 — human structural plasticity. **SETTLED** finding; causal interpretation partly **CONTESTED**.

**Supplementary / FREE methods anchors:**
- **MIT OpenCourseWare 9.13 *The Human Brain*** (Nancy Kanwisher) — full free video lectures; superb on fMRI logic and functional specialization. **SETTLED.**
- Huettel SA, Song AW & McCarthy G, *Functional Magnetic Resonance Imaging*, **3rd ed. (Sinauer, 2014; ISBN 9780878936274)** — the fMRI methods reference. **SETTLED** (verify edition).
- Luck SJ, *An Introduction to the Event-Related Potential Technique*, **2nd ed. (MIT Press, 2014; ISBN 9780262525855)** — EEG/ERP. **SETTLED.**

**Project / active-learning task:** For each major method (fMRI, EEG/MEG, TMS, single-unit, lesion), write one line on what causal or correlational claim it can support and its key confound. Then re-appraise a recent human-memory fMRI paper using your Phase 0 statistics lens (double-dipping, cluster inference).
**Time:** 5–7 months.
**Currency notes:** Method best-practices evolve (preregistration, multiverse analysis) — read current methodological commentary; flag reform-in-progress as CONTESTED.

---

### PHASE 7 — Cognitive neuroscience II: language, executive function & decision-making, emotion & the social brain, consciousness
**Goal:** The highest-integration topics — and the ones where the science is most **CONTESTED**, so this phase doubles as advanced critical-reading practice.
**Prerequisites:** Phase 6.

**Primary readings:**
- Gazzaniga 6e — language, cognitive control/executive function, emotion (Phelps's contribution), social cognition, and consciousness chapters. **SETTLED** framework; many specifics **CONTESTED**.
- Split-brain foundation: read Gazzaniga's own accessible synthesis of the split-brain work (he initiated it with Sperry; Sperry's Nobel was 1981). **SETTLED** core; strong "two independent minds" readings are **CONTESTED**.

**Primary landmark / frontier reading:**
- Emotion: a current review contrasting the "basic emotions" view with constructionist accounts (e.g., Barrett's theory of constructed emotion) — read both sides. **CONTESTED.**
- Consciousness: read primers on the two leading families — Global (Neuronal) Workspace Theory and Integrated Information Theory — then the results of the **Cogitate adversarial collaboration** testing GNWT vs IIT (published ~2025 in *Nature*; verify exact citation). Note the 2023 open letter by a group of scientists labeling IIT "pseudoscience." This is a live, unresolved dispute. **OPEN**; **HYPE-WATCH** on strong consciousness claims from any single camp.

**Supplementary:**
- Ward J, *The Student's Guide to Cognitive Neuroscience*, **4th ed. (Routledge, 2020; ISBN 9781138490543)** — accessible reinforcement/alternative voice. **SETTLED** (verify edition).

**Project / active-learning task:** Pick one contested question (e.g., "does the fMRI evidence support a dedicated language network distinct from general cognition?") and write a two-page evidence-weighted review that ends in a calibrated verdict (SETTLED/CONTESTED/OPEN) — this is the capstone of your literature-reading goal.
**Time:** 5–7 months.
**Currency notes:** **HIGHLY TIME-SENSITIVE** debates (consciousness, emotion, language networks) — verify the latest results; treat popular coverage with suspicion.

---

### PHASE 8 — Clinical neuroscience + connectomics & frontiers (capstone integration)
**Goal:** Tie mechanism to disease, and survey where the field is going. This phase is where all four levels converge on real problems.
**Prerequisites:** Phases 1–7.

**Primary readings:**
- Kandel 6e — the disorders-of-the-nervous-system section (mechanistic pathophysiology of stroke, Parkinson's, MS, psychiatric disorders). **SETTLED** mechanisms; therapeutics evolve. *(This is the light, principled touch-point with your Medicine track — no need to re-do clinical medicine here.)*
- A current *Nature Reviews Neuroscience* / *Nature Neuroscience* review on one disorder of interest, read critically.

**Frontier reading (read as OPEN frontier, not canon):**
- **Connectomics:** White JG, Southgate E, Thomson JN & Brenner S (1986), "The structure of the nervous system of the nematode *C. elegans*," *Phil. Trans. R. Soc. B* 314:1–340 — the first connectome. **SETTLED.** Then the **FlyWire adult *Drosophila* connectome**: Dorkenwald S et al. (2024), "Neuronal wiring diagram of an adult brain," *Nature* 634:124–138, and Schlegel P et al. (2024), *Nature* 634:139–152 — ~140,000 neurons, >50M synapses (a nine-paper package). Explore the data yourself in the free **FlyWire Codex**. **SETTLED** as an achievement; what a connectome *explains* about function is **OPEN**.
- **Mammalian connectomics:** the 2025 mouse-visual-cortex connectome-plus-function effort (MICrONS Consortium, *Nature*, 2025; verify citation). **OPEN.**
- **Whole-brain modeling / large-scale initiatives:** survey the state of the BRAIN Initiative and the cell-census/atlas efforts. **CONTESTED** (how far bottom-up mapping gets us).

**HYPE-WATCH corner (read skeptically throughout, especially here):** neuromyths (learning styles; strict left-brain/right-brain; "we use 10% of our brains") — all debunked; commercial "brain training" transfer claims; overreach in brain-based lie detection and neuro-marketing; strong claims that any current AI system "works like the brain."

**Project / active-learning task (capstone):** Choose one nervous-system disorder and write an integrative brief that runs top to bottom — molecular lesion → cellular dysfunction → circuit/systems failure → cognitive/behavioral signs → current therapeutic logic — with calibration tags on each claim. This exercises every level at once.
**Time:** 4–6 months.
**Currency notes:** **HIGHLY TIME-SENSITIVE** — connectomics, atlases, and disease therapeutics move fast; always pull the latest.

---

## The MVP Fast-Path (~10–12 months, ~10 hrs/week)

Shortest route to informed fluency + competent paper-reading + a solid (not exhaustive) mechanistic base:

1. **Months 1–2 — Orientation (Phase 0):** neuroanatomy scaffold (Blumenfeld or free Purves 2e) + the methods/statistics toolkit (Eklund 2016; Kriegeskorte 2009). → *unlocks literature reading immediately.*
2. **Months 2–5 — Cellular core (Phases 1–2, compressed):** Bear 4e Chs. 2–6 as the readable path; read Hodgkin–Huxley and the patch-clamp paper in full; build the neurotransmitter-systems table. Use Kandel 6e as reference, not cover-to-cover.
3. **Months 4–7 — Systems (Phases 4–5, compressed):** Purves 7e sensory + motor units; read Hubel & Wiesel in full; trace one circuit in the FlyWire Codex.
4. **Months 6–10 — Cognitive (Phases 6–7, compressed):** MIT OCW 9.13 (free video) + Gazzaniga 6e methods/attention/memory chapters; read H.M. (Scoville & Milner 1957); do one critical fMRI-paper appraisal.
5. **Months 9–12 — Integration:** skim Kandel's disorders section; read the FlyWire connectome package as frontier; write one calibrated evidence-review on a contested topic.

**MVP outcome:** you'll follow neuroscience news and talk substantively with neuroscientists, critically appraise most systems/cognitive papers, and hold a coherent mechanistic picture across all four levels — with solid (not comprehensive) depth. The full arc then deepens the biophysics, plasticity/development, and the long tail of systems and cognitive science.

---

## Dependency Map

```
PHASE 0 (Neuroanatomy + literature/methods toolkit) ── runs FIRST, then parallel throughout ──┐
                                                                                              │
PHASE 1 (Cellular I: excitability, HH, channels)                                              │
   │                                                                                          │
   └──> PHASE 2 (Cellular II: synapses, neurochemistry)                                       │
            │                                                                                 │
            └──> PHASE 3 (Plasticity/learning + development)                                  │
                     │                                                                         │
   PHASE 4 (Systems I: coding + sensory) <── needs 1–2 ──┐                                     │
            │                                            │                                     │
   PHASE 5 (Systems II: motor, neuromodulation) <── needs 1–2, 4 ──┐                           │
                                                                   │                           │
                          PHASE 6 (Cognitive I: methods, attention, memory) <── needs 4–5 ─────┤
                                   │                                                            │
                          PHASE 7 (Cognitive II: language, decision, emotion, consciousness)    │
                                   │                                                            │
                          PHASE 8 (Clinical + connectomics/frontier — integrates ALL levels) <──┘
```

**Strict serial core:** 1 → 2 → 3, and 1–2 → 4 → 5 → 6 → 7 → 8. **Parallelizable:** the Phase 0 methods strand runs continuously; neuroanatomy (Phase 0) can be revisited just-in-time; the disorders reading (Phase 8) can be sampled early per interest. Your **Medicine track's** neuro-physiology (action potentials, neuro chapters) and this program's Phases 1–2 overlap — lean on whichever you did first to save time.

---

## Overall Timeline & Effort

- **Full arc:** ~**32–44 months** (≈2.5–3.5 years) at ~8–12 hrs/week — roughly **1,400–2,000 hours**. Phases 4, 6, and 7 dominate the calendar; Phases 1–3 are where your physics background buys the most time back.
- **MVP fast-path:** ~**10–12 months** at ~10 hrs/week (~450–520 hours).
- At 15–20 hrs/week, compress the full arc toward ~2 years.

---

## Recommendations (staged, with decision thresholds)

**Stage 1 (Months 0–2): Start two strands at once.** Phase 0 methods (fast, plays to your strengths) + the neuroanatomy scaffold. **Threshold to proceed:** you can appraise a systems/cognitive paper's statistics and locate the major structures/pathways unaided.

**Stage 2 (Months 2–8): Own the cellular foundation.** Drive Phases 1–2 to real depth — read Hodgkin–Huxley and the patch-clamp paper in full, reproduce the action potential numerically for understanding. This is your fastest, highest-leverage stretch. **Threshold:** you can explain, mechanistically, how an action potential and a chemical synapse work, and reconstruct the neurotransmitter-systems table from memory.

**Stage 3 (Months 8–22): Build the systems level.** Phases 3–5; read Hubel & Wiesel and Newsome; use the FlyWire Codex hands-on. **Threshold:** you can trace at least two sensory/motor circuits end to end and explain a coding principle.

**Stage 4 (Months 22+): Cognitive + clinical + frontier.** Phases 6–8. **Threshold to declare "literature-competent":** you can read a new *Neuron* or *Nature Neuroscience* paper and produce a calibrated (SETTLED/CONTESTED/OPEN) appraisal in under two hours, and write an integrative disorder brief spanning all four levels.

**Ongoing:** subscribe to *Neuron*, *Nature Neuroscience*, and *Journal of Neuroscience* tables of contents; add *Nature Reviews Neuroscience* for reviews and *Trends in Cognitive Sciences* for the cognitive side. Re-verify any frontier claim (connectomics, consciousness) at the moment you rely on it.

**What would change this plan:** if the goal narrows to critical-reading-only, stop after the MVP. If you later decide to foreground the computational/ML bridge (explicitly excluded now), Dayan & Abbott's *Theoretical Neuroscience* and a computational-neuroscience course would attach after Phase 5. If a target text's newer edition ships mid-study, switch at a phase boundary rather than mid-phase.

---

## Caveats

- **Editions verified vs. not:** Verified current against publisher pages (Sept 2026): Kandel 6e (2021, ISBN 9781259642234), Purves 7e (2023, ISBN 9780197616246), Bear 4e/Enhanced (2015–16, ISBN 9781284211283), Gazzaniga 6e (2024, ISBN 9781324088998). **Verify at purchase** (I cited these from established knowledge, not a live publisher check this session): Blumenfeld *Neuroanatomy through Clinical Cases* edition; Hille *Ion Channels* 3e; Levitan & Kaczmarek 4e; Siegel *Basic Neurochemistry* 8e; Sanes/Reh/Harris *Development of the Nervous System* 4e; Huettel fMRI 3e; Luck ERP 2e; Ward 4e. **Free/OER verified:** Purves 2e on NCBI Bookshelf; Henley *Foundations of Neuroscience* (MSU, 2021, CC BY-NC-SA, openbooks.lib.msu.edu/neuroscience); Austin Lim *Open Neuroscience Initiative*; MIT OCW 9.13; BrainFacts.org; Wandell *Foundations of Vision* online.
- **Post-cutoff / frontier citations to double-check:** the exact citation for the 2025 mouse-cortex (MICrONS) connectome paper and for the Cogitate consciousness adversarial-collaboration paper (~2025 *Nature*) should be verified directly — these are recent and I've flagged them OPEN rather than treated them as settled. The FlyWire fly-connectome package (*Nature* 634, Oct 2024) is confirmed.
- **This is a knowledge curriculum, not clinical or research training.** It builds mechanistic understanding, literature fluency, and reasoning — not licensure, wet-lab skills, or clinical competence. Nothing here is medical advice.
- **Free-resource legality:** the free resources named (NCBI Bookshelf, Henley/Lim OER, MIT OCW, BrainFacts, Wandell, FlyWire Codex) are legitimately open. Textbook PDFs on file-sharing sites generally are not — buy or borrow via a library.
- **HYPE-WATCH domains to read hardest with your Phase 0 toolkit:** consciousness theories, strong emotion-localization claims, commercial neuroplasticity/brain-training transfer, neuromarketing, and any "AI works like the brain" framing. Your explicit choice to keep the ML bridge light makes this easier — evaluate neuroscience claims on neuroscience evidence.
- **Coverage by design:** development and plasticity are grouped (Phase 3) rather than split; computational neuroscience is deliberately minimized per your scope (touched only where biophysics demands it); the clinical layer is a principled touch-point (Phase 8), not a repeat of your Medicine track.