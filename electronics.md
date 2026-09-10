# A Rigorous Self-Study Curriculum in Electronics, Circuits, and Components — for a Physicist

## TL;DR
- **Yes, this is achievable as a rigorous, theory-first program**, and a physics BSc is the ideal launchpad: the hardest math (ODEs, complex analysis, Fourier, E&M) is already yours, so the work is mostly learning engineering conventions and device physics. Budget roughly 18–30 months part-time for the full four-domain program (Phases 0–8), or ~8–10 months for the compressed MVP path.
- **Spine of canonical texts, current editions confirmed:** Agarwal & Lang (free via MIT 6.002) → Sedra & Smith *Microelectronic Circuits* 8th ed. (2020) and Razavi *Fundamentals of Microelectronics* 3rd ed. (2021) → Razavi *Design of Analog CMOS IC* 2nd ed. (2017) → Streetman/Sze for device physics → Harris & Harris RISC-V (2021) for digital → Erickson & Maksimović 3rd ed. (2020) for power → Pozar 4th ed. (2012) + Razavi *RF Microelectronics* 2nd ed. (2011) for RF, with *The Art of Electronics* 3rd ed. (2015) as the lifelong bench reference.
- **Hardware verdict:** for a theory-focused learner, do ~90% in simulation (LTspice + ngspice/KiCad, all free), and buy exactly one all-in-one USB instrument — the **Digilent Analog Discovery 3 ($379 retail / $249 academic)** or the **ADI ADALM2000 (~$253 at DigiKey, 2026)** — which unlocks empirical verification of concepts SPICE cannot teach faithfully (noise, parasitics, instability, EMI). A full bench is unnecessary unless RF/power hardware becomes a goal.

## Key Findings

1. **The physics-to-EE gap is conventions, not concepts.** You do not need remedial math. You need: `j = √−1` (because `i` is current); the phasor/impedance formalism (which is just complex-exponential steady-state solutions of the ODEs you know); the Laplace-domain method (your ODE toolbox, repackaged); decibels; Bode plots; and engineering sign/reference conventions (passive sign convention). Each maps onto something you already own.

2. **Sequencing matters more than book choice.** The correct spine is: linear circuit analysis → dynamics/Laplace/frequency response → semiconductor device physics → analog → (branch into) digital/embedded, power, and RF. The four required domains share a common trunk (Phases 0–4); they diverge only in Phases 5–8.

3. **Free resources are strong enough to carry the entire trunk.** MIT 6.002 (Agarwal & Lang, the actual textbook authors), TI Precision Labs, the All About Circuits free textbook, NPTEL, Razavi's own UCLA lectures on YouTube, and ADI's Active Learning wiki collectively cover most of the program at zero cost. Paid canonical texts add rigor and problem sets but are not strictly gating.

4. **Simulation is the default; hardware is a targeted supplement.** SPICE (LTspice, ngspice) is free, industry-relevant, and sufficient for the vast majority of derivation-verification. The one all-in-one USB instrument earns its place specifically for phenomena that idealized simulation hides.

5. **Calibration is essential and provided explicitly** — SPICE fidelity limits, grounding/EMC folklore vs. engineering, audiophile pseudoscience, and the VHDL/Verilog/SystemVerilog debate are all addressed so you can tell settled consensus from engineering judgment from folklore.

---

## Tooling (with currency callouts, verified early 2026)

**Simulation (the workhorses):**
- **LTspice** — free, from Analog Devices. The de-facto hobbyist/industry SPICE for board-level analog and especially switching power supplies. Current status: **LTspice 24** on Windows (the Wikipedia infobox lists stable release 26.0.1, dated Jan 2026); on **macOS the newest build is 17.2.x** (v24 is Windows-only, though it runs on Mac under Wine/CrossOver). ADI's own page markets "LTspice 24.1: Fast, Free, Unlimited." Best for: transient/AC analysis, switching converters. Worst for: large digital, RF distributed structures.
- **ngspice** — free, open-source (BSD-3-Clause). **Stable release 46, dated 29 March 2026** (per the Wikipedia Ngspice infobox; prior line ngspice-45.2 was Sept. 2025). The engine embedded in KiCad; de-facto open-source SPICE standard.
- **KiCad** — free, open-source EDA. **KiCad 9.0 (2025); 10.0.0 released 20 March 2026** (per the Wikipedia KiCad infobox). Integrates ngspice for schematic-driven SPICE. Best when you want schematic capture + simulation + eventual PCB in one tool.
- **TINA-TI** — free (Texas Instruments); the simulator used exclusively in TI Precision Labs. Good for op-amp/precision analog work.
- **Falstad/CircuitJS** — free browser circuit simulator; superb for real-time intuition (watch charge flow, RLC ringing). Actively maintained (open-sourced by Paul Falstad, developed by Iain Sharp). Best pedagogical "see it move" tool; not for quantitative rigor.
- **Qucs-S** — free; useful front-end that can drive ngspice/Xyce, with some RF/S-parameter conveniences.

**Python angle (you can exploit these; verified currency):**
- **scikit-rf (skrf)** — actively maintained (lead maintainer Julien Hillairet, CEA/IRFM; v1.0.0 in 2024, ~v1.9.0 by early 2026). RF/microwave two-ports, S-parameters, Touchstone files, Smith charts. Pairs perfectly with the RF phase.
- **python-control** — current stable **0.10.2 (July 2025)**. Per the project's official Version 0.10.2 release notes: "This version of python-control requires Python 3.10 or higher, NumPy 1.23 or higher (2.x recommended), and SciPy 1.8 or higher." Bode/Nyquist/root-locus, state-space; ideal for the feedback/stability and converter-control phases.
- **PySpice** — Python bindings to ngspice/Xyce. The original (Fabrice Salvaire) is only lightly maintained (latest ~v1.5); the actively developed 2026 fork is **InSpice (v1.7.0.1, 2026, Python ≥3.12)**. Use it to script parameter sweeps / Monte Carlo from Python.

**Tooling verdict:** LTspice for analog/power, KiCad+ngspice for schematic-to-sim, scikit-rf + python-control for the Python-native analyses (a genuine edge for you). Don't over-invest in tool-collecting; two SPICEs and two Python libraries cover everything.

---

## Hardware Recommendation (tiered)

**Assessment principle:** Physical hardware adds pedagogical value precisely where idealized models lie. That means: noise (Johnson/shot/flicker you can actually *see* on a spectrum), parasitics (lead inductance, stray capacitance), real op-amp non-idealities, oscillation/instability from layout, EMI/ground bounce, and the "why won't this converge/work" gap between netlist and breadboard. It adds little where the math is clean and the model is faithful (ideal-ish linear networks, transfer-function algebra, logic truth tables) — do those in simulation.

**Tier 0 — Simulation only ($0).** LTspice + KiCad/ngspice + Falstad + Python (scikit-rf, python-control, PySpice/InSpice). Sufficient for Phases 0–4 trunk theory, most of digital (use an FPGA toolchain sim), and first-pass power/RF. **Recommendation: everyone starts here and stays here until a concept demands a real measurement.**

**Tier 1 — The one instrument worth buying (~$250–$400). This is the answer for you.**
- **Digilent Analog Discovery 3 — $379 retail ($249 academic).** Per Digilent's official blog: "The Analog Discovery 3 retails for $379 USD, which is $20 less than the retail price of the Analog Discovery 2 of $399. The academic price of the Analog Discovery 3 goes for $249 USD if you qualify as an academic through our verification system." It is a 14-bit, 125 MS/s USB oscilloscope built on a Spartan-7 FPGA (an upgrade from the AD2's Spartan-6), plus a 2-ch waveform generator, 16-ch logic analyzer/pattern generator, programmable supplies, and — critically — a built-in **network/Bode analyzer and spectrum analyzer**. The Bode analyzer alone justifies it: you can measure a real filter/amplifier transfer function and overlay it on your hand-derived Bode plot. WaveForms software is free (Win/Mac/Linux) with a Python SDK.
- **Alternative: ADI ADALM2000 (M2K) — ~$253 (listed $253.32 at DigiKey, 2026).** Similar capability: per Analog Devices' official page, "With 12-bit ADCs (at 100MSPS) and DACs (at 150MSPS), the M2K brings the power of high performance lab equipment to the palm of your hand." Free Scopy software, network + spectrum analyzer. Its decisive advantage is the **free ADI "Active Learning" curriculum** (wiki.analog.com/university) written *specifically* for it, with LTspice files and structured Electronics I/II labs.
- Pair either with the **ADALP2000 Analog Parts Kit** and a breadboard, plus a cheap DMM (~$50). This is the complete "verify concepts empirically" kit.
- **Verdict:** Buy **one** — AD3 if you want the better instrument (14-bit front end, larger buffers, Spartan-7); ADALM2000 if you want the tightly-integrated free curriculum. For a theory learner this single purchase captures ~95% of the empirical value of a home lab.

**Tier 2 — Serious home bench ($800–$3,000+).** Standalone DSO (a 100+ MHz scope), a real bench DMM, a linear bench PSU, a function generator, a soldering station, and — only if you pursue RF or power seriously — a VNA (the budget NanoVNA is remarkable value for HF/VHF; a used benchtop VNA for real work) and/or power-specific gear. **Only justified if** you decide to actually build RF front-ends, switching converters, or motor drives. For pure theory, this is optional.

**Honest bottom line:** Hardware value is real but bounded. The AD3/ADALM2000 tier is the sweet spot; below it you miss the "models lie" lessons, above it you're paying for a hobby you may not have. TI Precision Labs' optional **$199 Op-Amp EVM** is worth it only if you deeply follow that curriculum.

---

## The Phased Curriculum

### Phase 0 — Bridge & Orientation (2–4 weeks)
**Objective:** Install the engineering conventions onto your physics foundation; stand up the toolchain.
**Prerequisites:** BSc physics (done).
**Cross-links to physics (make these explicit now):** `j` vs `i`; phasors = complex-exponential ansatz for steady-state ODE solutions; impedance = generalized resistance in the complex frequency domain; the passive sign convention; dB = 10·log₁₀ of power ratios.
**Primary (free):** MIT OCW **6.002 Circuits and Electronics** (Agarwal & Lang) lectures 1–3; skim *The Art of Electronics* 3rd ed. Ch. 1.
**Do:** Install LTspice, KiCad, a Python env with scikit-rf/python-control. Simulate a resistive divider and an RC step response; confirm against hand analysis.
**Time:** 20–30 h.

### Phase 1 — Linear Circuit Analysis (4–8 weeks)
**Objective:** Fluency in KVL/KCL, nodal/mesh analysis, Thévenin/Norton, superposition; understand the **lumped-element abstraction and when it breaks** (when wavelength ≈ circuit size — the bridge you'll cash in during RF).
**Prerequisites:** Phase 0.
**Primary text:** **Nilsson & Riedel, *Electric Circuits*, 12th ed., Pearson, 2023** (the 11th ed., 2019, is fine and cheaper) — the cleanest rigorous treatment of analysis technique. *Alternative/parallel:* **Agarwal & Lang, *Foundations of Analog and Digital Electronic Circuits*, Morgan Kaufmann, 2005** (the 6.002 text; unusually rigorous about the abstraction itself).
**Supplementary (free):** MIT 6.002 problem sets; All About Circuits free textbook Vol. I (DC) — Tony Kuphaldt's *Lessons in Electric Circuits*, hosted free at allaboutcircuits.com/textbook.
**Cross-link:** The lumped abstraction is exactly the quasi-static limit of Maxwell's equations — connect explicitly to your E&M.
**Exercises/Projects:** ~40 problems from Nilsson; in LTspice, build and verify a Wheatstone bridge and a multi-loop network; extract a Thévenin equivalent numerically.
**Time:** 50–70 h.

### Phase 2 — Dynamics, Phasors, Laplace, Frequency Response (6–10 weeks)
**Objective:** First/second-order transients; sinusoidal steady state; impedance; resonance; the Laplace-domain method for circuits; transfer functions, poles/zeros, Bode plots.
**Prerequisites:** Phase 1.
**Primary text:** Nilsson & Riedel chapters on RL/RC/RLC, phasors, Laplace, and frequency response. **Bridge text (canonical): Oppenheim & Willsky, *Signals and Systems*, 2nd ed., Prentice Hall, 1996/97** + MIT OCW **6.003** (free lectures/notes) — for the transform machinery as a systems-theory foundation.
**Cross-link (high value):** The series/parallel **RLC circuit *is* the driven damped harmonic oscillator** — same ODE, same Q, same resonance, same phase behavior. Map ζ, ω₀, Q directly. Laplace/Fourier circuit methods are tools you already own from ODEs/physics.
**Tooling:** Use **python-control** to generate Bode/pole-zero plots; verify against hand-drawn asymptotic Bode plots. If you bought the AD3/ADALM2000, measure a real RLC transfer function on the built-in Bode/network analyzer.
**Exercises/Projects:** Derive and measure the transfer function of a 2nd-order RLC bandpass; extract Q three ways (time-domain ringing, −3 dB bandwidth, pole locations).
**Time:** 60–90 h.

### Phase 3 — Semiconductor Device Physics (6–12 weeks)
**Objective:** Band theory, doping, carrier statistics and transport, pn junction, diode I–V, then BJT and MOSFET operation and small-signal models — grounded in solid-state physics, with a clear line drawn between *device-physics depth* and *circuit-level modeling depth*.
**Prerequisites:** Phase 2; your physics stat-mech and QM.
**Primary text:** **Streetman & Banerjee, *Solid State Electronic Devices*, 7th ed., Pearson, 2014/2015** — the standard bridge between physics and EE, rigorous but readable.
**Reference (deep):** **Sze, Li & Ng, *Physics of Semiconductor Devices*, 4th ed., Wiley, 2021** — the encyclopedic reference; consult, don't read cover-to-cover.
**Circuit-modeling companion:** **Razavi, *Fundamentals of Microelectronics*, 3rd ed., Wiley, 2021** — introduces device models exactly as a circuit designer uses them.
**Free:** Razavi's UCLA "Electronics 1" lectures on YouTube (charge carriers, doping, diodes, transistors — from the textbook author; catalogued by InfoCoBuild as "Electronic Circuits I, Professor Behzad Razavi, UCLA"); NPTEL device courses (e.g., IIT Delhi "Analog Electronic Circuit," free on nptel.ac.in / YouTube).
**Cross-link (high value):** Carrier statistics ↔ **Fermi–Dirac distribution** and the density of states from your stat mech; the pn junction built-in potential ↔ chemical-potential equilibration; drift-diffusion ↔ transport theory.
**Calibration note:** Know the difference between a physicist's PDE-level device model (Sze) and the algebraic small-signal model a circuit designer actually uses. You will rarely solve the drift-diffusion equations in practice, but knowing they underlie the SPICE model tells you *when the model breaks*.
**Time:** 70–110 h.

### Phase 4 — Analog Electronics: The Core (12–20 weeks)
**Objective:** Single-transistor amplifiers, biasing, small-signal analysis, multistage amplifiers, differential pairs, current mirrors, the op-amp (ideal and non-ideal), **negative feedback theory (loop gain, stability, phase margin)**, active filters, oscillators, data converters (ADC/DAC), and **noise in circuits** (thermal/shot/flicker).
**Prerequisites:** Phases 2–3.
**Primary text:** **Sedra, Smith, Chan Carusone & Gaudet, *Microelectronic Circuits*, 8th ed., Oxford University Press, 2020** (two new coauthors joined for this edition; ISBN 9780190853464) — the market-standard rigorous course. *Parallel:* Razavi *Fundamentals of Microelectronics* for a second explanation style.
**Advanced follow-on:** **Razavi, *Design of Analog CMOS Integrated Circuits*, 2nd ed., McGraw-Hill, 2017** — for IC-level depth (cascodes, mirrors, opamp topologies, feedback, noise).
**Bench reference:** **Horowitz & Hill, *The Art of Electronics*, 3rd ed., Cambridge University Press, 2015**, plus *The x-Chapters* (2020) — the practitioner's judgment layer. (An expanded x-Chapters edition, ~30% longer with a new sensors chapter, is announced for release in 2026; the 2015 3rd ed. of the main book remains current.) Companion *Learning the Art of Electronics* (Hayes & Horowitz) is the lab-course version.
**Free:** **TI Precision Labs — Op Amps** (40+ modules, free with a myTI account, uses free TINA-TI); TI's *Op Amps for Everyone* handbook and *Analog Engineer's Pocket Reference*.
**Cross-link (high value):** Circuit **noise ↔ statistical/thermal physics** — Johnson–Nyquist thermal noise `⟨v²⟩ = 4kTRΔf` is the fluctuation-dissipation theorem; shot noise ↔ Poisson statistics of discrete carriers. This is a place your physics gives you a genuine head start over most EEs.
**Tooling/hardware:** This is where the **AD3/ADALM2000 pays off most** — measure a real op-amp's finite gain-bandwidth, slew rate, offset, and noise floor; build an oscillator and watch it actually start up; verify phase margin by ringing.
**Exercises/Projects:** (1) Design, simulate, and (optionally) build a two-stage discrete amplifier; measure gain vs. frequency. (2) Op-amp Sallen–Key active filter: derive H(s), simulate, measure. (3) Noise: hand-calculate a resistor's thermal noise, then measure it on the spectrum analyzer.
**Time:** 120–200 h. **This is the keystone phase.**

### Phase 5 — Digital & Embedded (10–18 weeks)
**Objective:** Boolean algebra, combinational/sequential logic, timing, an HDL, FPGA basics, computer-architecture fundamentals, then microcontrollers/embedded (memory-mapped I/O, interrupts, peripherals, real-time).
**Prerequisites:** Phase 1 (digital abstraction); Phase 4 helpful but not gating.
**Primary text:** **Harris & Harris, *Digital Design and Computer Architecture, RISC-V Edition*, Morgan Kaufmann, 2021** — logic gates → combinational/sequential → HDL → build a RISC-V processor. Integrates **both SystemVerilog and VHDL** side by side.
**Free:** The authors' **edX MOOCs ENGR85A/ENGR85B** (video + interactive problems); Neso Academy's free Digital Electronics YouTube series; NPTEL digital courses.
**Embedded follow-on:** Any current ARM Cortex-M text; hands-on with a cheap dev board (e.g., an STM32 or RP2040 board, ~$5–$20).
**Calibration note — VHDL vs. Verilog vs. SystemVerilog:** This is **engineering judgment, not a correctness question.** Consensus: **SystemVerilog** dominates US commercial digital/verification and is the pragmatic default; **VHDL** remains strong in Europe, aerospace/defense, and safety-critical work; plain Verilog is legacy-ish but underlies SystemVerilog. Recommendation: **learn SystemVerilog for design**, read enough VHDL to be literate. Ignore tribal "one is better" claims.
**Tooling:** Free FPGA simulators (open-source Verilator/Icarus, or vendor tools). The AD3's logic analyzer/pattern generator is genuinely useful here.
**Exercises/Projects:** Implement and simulate an FSM; synthesize the Harris RISC-V core on an FPGA (or in simulation); write bare-metal C driving a peripheral via memory-mapped I/O + an interrupt.
**Time:** 100–160 h.

### Phase 6 — Power Electronics (8–14 weeks)
**Objective:** Diode/thyristor rectifiers; DC–DC converters (buck/boost/buck-boost); **averaged and state-space-averaged models**; magnetics and transformer design; feedback control of converters; linear vs. switching regulators; intro to motor drives/inverters.
**Prerequisites:** Phases 2 & 4 (feedback, Laplace).
**Primary text:** **Erickson & Maksimović, *Fundamentals of Power Electronics*, 3rd ed., Springer, 2020** — the rigorous graduate standard; superb on averaging, converter dynamics, and control. New 3rd-ed. material: switching-loss modeling, wide-bandgap devices, Nyquist criterion, a digital-control chapter.
**Breadth reference:** **Mohan, Undeland & Robbins, *Power Electronics: Converters, Applications, and Design*, 3rd ed., Wiley, 2003** — broader applications coverage (drives, utility).
**Free:** Maksimović's CU Boulder **Coursera Power Electronics specialization** (mirrors the book); NPTEL power electronics.
**Cross-link:** State-space averaging ↔ your linear-systems and perturbation instincts; magnetics ↔ your E&M (Ampère's law, energy in `B` fields, `½LI²`).
**Tooling:** **LTspice is the industry-relevant tool here** — simulate a buck converter, verify the averaged model against the switching waveform, close a control loop. python-control for the compensator design.
**Calibration note:** SPICE switching sims are trustworthy for topology/control but **poor for absolute loss/thermal numbers** without careful device and parasitic models — a known fidelity limit; trust hand analysis of averaged models for design, sim for verification.
**Exercises/Projects:** Derive the buck CCM conversion ratio and small-signal control-to-output transfer function; design a compensator for a target phase margin; verify in LTspice.
**Time:** 90–140 h.

### Phase 7 — RF / High-Frequency (10–18 weeks)
**Objective:** Transmission-line theory; the Smith chart; S-parameters and two-port networks; impedance matching; RF amplifiers; LNAs; mixers; oscillators; intro to antennas and EMC.
**Prerequisites:** Phase 2 (frequency response), Phase 4 (amplifiers), and your E&M/wave background.
**Primary text:** **Pozar, *Microwave Engineering*, 4th ed., Wiley, 2012** — the canonical field-based treatment (lines, networks, matching, S-params, components).
**IC-design follow-on:** **Razavi, *RF Microelectronics*, 2nd ed., Prentice Hall/Pearson, 2011/2012** — LNAs, mixers, oscillators, synthesizers at the transistor level.
**Cross-link (high value):** **Transmission lines ↔ the 1-D wave equation and boundary reflections** you know from physics — the reflection coefficient Γ is exactly the wave reflection at an impedance discontinuity; the Smith chart is a conformal map (Möbius transform) of complex Γ, which your complex-analysis background makes transparent. This is where the "lumped abstraction breaks" thread from Phase 1 finally pays off.
**Tooling (your Python edge):** **scikit-rf** for S-parameters, Touchstone files, de-embedding, and Smith-chart plotting — a real advantage for you. A **NanoVNA (~$50–$150)** is the one RF hardware purchase that genuinely teaches (measure real S11, see matching work).
**Exercises/Projects:** Design a two-element L-match on the Smith chart, verify in scikit-rf; design and simulate an LNA for a target NF and gain; analyze a real device's S-parameters.
**Time:** 100–160 h.

### Phase 8 — Capstone & Integration (open-ended)
**Objective:** Integrate across domains on one substantial project.
**Suggested capstones:** (a) a mixed-signal data-acquisition front-end (analog conditioning + ADC + FPGA/MCU capture); (b) a closed-loop switching regulator with digital control; (c) an RF receiver front-end (LNA + mixer + IF). Each forces you to reconcile idealized theory with real measurement using your AD3/ADALM2000.

---

## The MVP / Time-Compressed Path (~8–10 months part-time)

For the shortest *rigorous* route to competence across all four domains, compress as follows (skip nothing conceptually, but use lecture courses over exhaustive textbook problem sets):

1. **Trunk (fast):** MIT 6.002 (Agarwal & Lang) end-to-end — covers Phases 1–2 and touches 3–4 in one rigorous course. Add python-control for Bode/Laplace. **(6–8 weeks)**
2. **Devices (targeted):** Streetman Chs. 1–6 only (band theory → pn → BJT/MOSFET), skip optoelectronics/advanced. **(3–4 weeks)**
3. **Analog (keystone, don't skimp):** Sedra & Smith selected chapters (op-amps, single-stage/diff amps, feedback, filters, noise) + **all** of TI Precision Labs Op Amps. **(8–10 weeks)**
4. **Digital (fast):** Harris & Harris via the free edX ENGR85A/B, through the single-cycle RISC-V core; one small MCU project. **(5–6 weeks)**
5. **Power (concepts):** Maksimović Coursera + Erickson Chs. 1–3, 7–9 (basic converters + averaging + control); one LTspice buck project. **(4–5 weeks)**
6. **RF (concepts):** Pozar Chs. 2–5 (lines, Smith chart, matching, two-ports/S-params) + a scikit-rf matching exercise; skip deep component design. **(4–5 weeks)**

**MVP hardware:** one AD3 or ADALM2000, nothing else. **MVP dependency rule:** you may reorder Power/Digital/RF (Phases 5–7 are siblings), but never attempt them before the Phase 1–4 trunk.

---

## Calibration: Settled vs. Contested vs. Folklore

**SETTLED consensus (trust and internalize):**
- KVL/KCL, Thévenin/Norton, superposition for linear networks; phasor/impedance methods; Laplace circuit analysis.
- Small-signal linearization; the ideal op-amp abstraction with negative feedback; Barkhausen criterion for oscillation (as a necessary heuristic).
- Johnson–Nyquist and shot noise formulas (these are physics, not convention).
- Nyquist/Bode stability criteria; phase margin as a design target.
- Transmission-line theory, S-parameters, the Smith chart.

**CONTESTED / matter of engineering judgment (know the trade-offs):**
- **SPICE fidelity vs. hand analysis.** SPICE is excellent for linear/mildly-nonlinear behavior and topology validation, but model quality is everything: transistor models vary in accuracy, thermal/parasitic effects are often under-modeled, and switching-loss/EMI numbers are frequently untrustworthy without careful setup. **Rule: trust hand analysis for insight and first-order design; trust SPICE for tedious verification; distrust any sim you can't sanity-check.**
- **VHDL vs. Verilog vs. SystemVerilog** — regional/industry preference, not correctness (see Phase 5).
- **Grounding, decoupling, and layout** — this is *real, rigorous engineering* (return-current paths, loop inductance, ground bounce) that is **often taught as cargo-cult ritual** ("add a 0.1 µF cap because you always do"). Learn the physics (it's your E&M: `V = L·di/dt`, loop area sets inductance) so you can distinguish the genuine rule from the copied-without-understanding one. Horowitz & Hill and Henry Ott's EMC work are the antidotes.
- **How much classical hand-analysis technique still matters** in the IC/simulation era — a real debate. Verdict: the *techniques* (nodal, two-port, feedback analysis) remain essential for *insight*; exhaustive by-hand solution of large networks is obsolete. Learn to analyze by inspection (Razavi's whole pedagogy), not to grind.

**OVERSTATED / folklore (be skeptical):**
- **Audiophile component pseudoscience** — directional cables, exotic capacitor "sound," oxygen-free-copper mysticism for line-level signals: almost entirely unsupported by measurement. Real effects (dielectric absorption, ESR/ESL, microphonics) exist and are quantifiable; the mystical layer on top is marketing. Your physics is the correct filter here.
- **"SPICE is truth"** — the inverse error of distrusting sim: treating simulation output as reality. Both extremes are wrong.
- **Over-precise device datasheet numbers** — typical/min/max spreads and temperature/process variation mean textbook "exact" bias-point arithmetic is an idealization.

---

## Cross-Connections to Physics (consolidated — your accelerators)
- **RLC resonance ↔ driven damped harmonic oscillator** (identical ODE; ζ, Q, ω₀).
- **Transmission lines ↔ 1-D wave equation + boundary reflections**; Γ ↔ wave reflection coefficient; **Smith chart ↔ Möbius/conformal map** of complex Γ.
- **Laplace/Fourier circuit methods ↔ your ODE/transform toolbox** (you already own the math).
- **Semiconductor carrier statistics ↔ Fermi–Dirac / density of states**; junction built-in potential ↔ chemical-potential equilibration.
- **Circuit noise ↔ thermal/statistical physics** (Johnson–Nyquist = fluctuation-dissipation; shot noise = Poisson process).
- **Impedance & the phasor method ↔ complex analysis** and steady-state solutions of linear ODEs.
- **Magnetics/transformers ↔ E&M** (Ampère/Faraday, energy in fields).
- **The lumped-element abstraction ↔ the quasi-static limit of Maxwell's equations** — and its breakdown at high frequency is the whole premise of the RF phase.

## Recommendations (staged, with thresholds)
1. **Start now, spend nothing:** Install LTspice + KiCad + Python (scikit-rf, python-control). Do Phases 0–1 entirely free via MIT 6.002 and Nilsson. **Threshold to proceed:** you can derive and SPICE-verify an RLC step response and its transfer function without help.
2. **Buy the one instrument when you hit Phase 2–4:** Purchase a **Digilent Analog Discovery 3** ($379 / $249 academic) *or* **ADALM2000** (~$253) + ADALP2000 parts kit + DMM. **Trigger:** the moment you want to *measure* a Bode plot or a noise floor. Choose ADALM2000 if you value the free ADI Active Learning labs; AD3 for the better instrument.
3. **Treat Phase 4 (Analog) as the keystone** — invest the most time here; it's the prerequisite mindset for power and RF. **Threshold:** you can analyze a feedback amplifier for loop gain and phase margin by inspection.
4. **Parallelize the branches (Phases 5–7)** once the trunk is solid — do them in whatever order matches your interest; they're independent. Use your Python fluency as a genuine edge (python-control for power/feedback, scikit-rf for RF).
5. **Only ascend to a Tier-2 bench** if you commit to building real RF or power hardware. **Threshold:** you've completed the relevant phase in simulation and have a specific build in mind. Otherwise the AD3/ADALM2000 is sufficient indefinitely.
6. **Prefer canonical texts + free author lectures over secondary summaries** throughout; use All About Circuits / Neso / NPTEL for a second explanation, not as the spine.

## Applied Companions: Home Wiring & the Power Grid

These two sections sit deliberately *outside* the theory-first electronics spine above. Residential wiring is fundamentally a **codes-and-practice** domain (safety-critical, jurisdiction-specific, not derivation-heavy), and the grid is an **infrastructure/systems** domain. Your physics explains *why* the rules and architectures are what they are — so each companion foregrounds the physics beneath the practice — but the rules themselves are regional and, for wiring, legally binding. Both are structured like the rest of the curriculum (objective, prerequisites, resources with editions, free-resource flags, physics cross-links, calibration, projects, time/MVP).

*Regional centering:* the wiring companion leads with the **German/IEC (DIN VDE)** framework and the grid companion with the **Continental-European (ENTSO-E, 50 Hz)** grid, with US, UK, and India cross-referenced throughout. Swap the anchor to your jurisdiction if different.

### Companion I — Residential Electrical Installation (Everything an Electrician Must Know)

**Objective:** Understand end-to-end how a building's low-voltage installation is designed, protected, wired, and verified — to the depth a qualified electrician works at — plus the physics beneath each rule.
**Prerequisites:** Phases 0–2 (AC, RMS, impedance, the power triangle). Phase 6 (power) helps for supply-side context.

**⚠️ Legal & safety reality — read first.** In most jurisdictions, fixed mains wiring is *legally restricted* work. In **Germany**, fixed-installation work must be done by (or under) a registered **Elektrofachkraft** in an eingetragener Elektrobetrieb; in the **UK**, much domestic work is **notifiable under Building Regulations Part P**; in the **US**, permits and licensing apply. Treat this section as *understanding*, not a license to rewire your home. Where it says "practice," that means under a qualified electrician or on **de-energized training rigs**. This is the one domain in the whole curriculum where "learn by tinkering live" is the wrong instinct — mains voltage kills.

**The domain map (what an electrician actually knows):**
1. **Supply & service entry** — how power reaches the building: service drop/lateral, the meter, the main distribution board (Zählerschrank / consumer unit / panelboard), main switch/isolator. Single-phase vs. **three-phase supply** (German homes commonly get 400 V three-phase / 230 V phase-to-neutral; US homes get 120/240 V split-phase).
2. **Earthing (grounding) systems** — the most important *and* most misunderstood topic. The IEC 60364 taxonomy: **TN-C, TN-S, TN-C-S (PME), TT, IT** — what each means for the neutral/earth relationship, fault-current return paths, and shock safety. US equivalent: the grounding-electrode system + equipment grounding conductor.
3. **Overcurrent & fault protection** — fuses, **MCBs** and their tripping curves (**B/C/D** in the IEC world), discrimination/selectivity, and short-circuit breaking capacity.
4. **Earth-fault / shock protection** — **RCDs (residual current devices) / GFCIs**, **RCBOs**, **AFDDs** (arc-fault detection); required disconnection times; the physiology of why tens of mA through the heart is lethal.
5. **Circuit design & cable sizing** — conductor **ampacity** and derating (grouping, ambient temperature, insulation type), **voltage-drop** limits, **diversity/demand factors**, **radial vs. ring final circuits** (the UK ring main is a genuine outlier), cable types (**NYM-J** in Germany, **NM-B "Romex"** in the US, **T&E** in the UK), conduit/trunking methods.
6. **Special locations** — bathroom/shower **zones** and **IP ratings**, kitchens, outdoors and wet areas, and increasingly **EV charging** and **PV/battery** connection points.
7. **Inspection & testing** — the verification regime every installation must pass: continuity of protective conductors, **insulation resistance**, **earth-fault-loop impedance (Zs)**, **RCD trip testing**, polarity, and prospective fault current — performed with a multifunction tester (MFT). This is where the theory meets an instrument.
8. **Documentation & compliance** — certificates (EIC/EICR in the UK; Prüfprotokoll per DIN VDE 0100-600/-610 in Germany) and the governing code.

**Code systems by region (this determines everything — pick yours):**
- **International baseline:** **IEC 60364**, *Low-voltage electrical installations* — the parent standard most national codes derive from.
- **Germany / much of Europe (primary anchor):** the **DIN VDE 0100** series (German adoption of harmonized **HD 60364 / IEC 60364**), plus **VDE-AR-N 4100** (Technical Connection Rules for LV networks). The formal trade route is the **Elektroniker für Energie- und Gebäudetechnik** apprenticeship — its curriculum *is* the "what an electrician knows" syllabus.
- **UK / Ireland:** **BS 7671:2018+A4:2026** — the **"Orange Book,"** IET Wiring Regulations 18th Edition Amendment 4, published April 2026, superseding the A2:2022+A3:2024 "Brown Book" (valid only until 15 October 2026). Companions: the IET **On-Site Guide** and **Guidance Notes 1–8**.
- **USA:** the **National Electrical Code, NFPA 70, 2026 edition** (revised on a strict three-year cycle; the 2026 adds new **Article 750** on grounding/bonding of limited-energy systems, reorganizes Chapter 2 by voltage class, and folds Chapter 8 into the general rules). NFPA provides **free read-only online access**.
- **India:** the **National Electrical Code of India (SP 30, BIS)**, **IS 732** (code of practice for electrical wiring installations), and the **CEA (Measures Relating to Safety and Electric Supply) Regulations**.

**Primary resources (annotated, with sequencing):**
- **Germany:** the **DIN VDE 0100** series itself (Beuth/VDE) — authoritative but dense — paired with a standard trade textbook such as **Europa-Lehrmittel, *Fachkunde Elektrotechnik*** (the standard Ausbildung reference covering exactly the electrician syllabus). *Sequence:* trade textbook first for structure, standard second for authority.
- **UK (the best English-language on-ramp even if you're in Germany, because it's rigorously and clearly written):** **Brian Scaddan, *IET Wiring Regulations: Explained and Illustrated* and *Wiring Systems and Fault Finding* (Routledge)**, plus **IET, *Requirements for Electrical Installations: IET Wiring Regulations 18th Edition, BS 7671:2018+A4:2026* (IET, 2026)** and the **On-Site Guide**. *Sequence:* Scaddan "Explained" → On-Site Guide → the full Regs.
- **USA:** **Rex Cauldwell, *Wiring a House*, 6th ed. (Taunton Press)** — the best conceptual "why," by a master electrician; **NFPA, *NEC Handbook*, 2026** for code-with-commentary; **Charles Michal, *Ugly's Electrical References*, 2026** as the field pocket reference; **Mike Holt** materials (much free on YouTube) for exam-grade code mastery.
- **Calculations (rigorous, physics-friendly):** **Christopher Kitcher & Brian Scaddan, *Electrical Installation Calculations* (Routledge)** — ampacity, voltage drop, Zs, adiabatic conductor sizing, worked from first principles.
- **Grounding, deep:** **IEEE Std 142 ("Green Book"), *Recommended Practice for Grounding of Industrial and Commercial Power Systems*** — the engineering rigor beneath the code rules.

**Free resources (flagged):** NFPA free online read-access to the NEC; Mike Holt's free video library (US code); manufacturer application/selection guides (Hager, ABB, Schneider) for IEC-world consumer-unit design and RCD/MCB coordination. Note: rigorous *free* IEC/DIN-world text is thinner than for the NEC — the standards themselves are paywalled.

**Physics cross-links (your accelerators):**
- **Earth-fault-loop impedance Zs ↔ the Thévenin equivalent** of the supply seen from a fault point: `Zs = Ze + (R1+R2)`, and fault current `Ia = U0/Zs` is Ohm's law on that Thévenin source. Disconnection-time rules then reduce to "does the breaker's I–t curve clear before the touch voltage persists too long?"
- **Three-phase 400/230 V ↔ three phasors 120° apart**; the √3 line-to-phase ratio falls straight out of the phasor geometry you already know.
- **RMS and the power triangle (P, Q, S, power factor) ↔ your Phase-2 phasor/impedance work** — the "why" behind kVA sizing and PF correction.
- **Adiabatic cable equation (`S² = I²t / k`) ↔ Joule heating** `∫ i²R dt` with no time to shed heat — pure thermal physics.
- **Skin effect** in large conductors ↔ diffusion of AC into a conductor, from your E&M.

**Calibration — settled vs. contested vs. folklore (this domain is *thick* with folklore):**
- **Settled (physics, non-negotiable):** shock physiology and RCD thresholds; the necessity of low-impedance fault paths and equipotential bonding; ampacity derating; disconnection-time logic.
- **Contested / genuine engineering trade-offs:** **TN-C-S (PME) vs. TT** earthing (PME shifts risk under a lost-neutral scenario — a real, debated trade-off, and the reason EV charge points get special treatment); **ring vs. radial** final circuits (defended on copper-economy grounds, attacked on fault-integrity grounds — reasonable engineers disagree); **AFDD/AFCI mandates** (US-led; cost-vs-benefit contested in Europe).
- **Folklore / overstated / sometimes dangerous:** "**backstab** the receptacle, it's fine" vs. screw terminals; **wire-nut vs. Wago lever-connector** tribal wars; assorted "always pigtail / never pigtail" shibboleths; and the genuinely *dangerous* belief that a ground rod alone protects a **TT** installation without an RCD (it does **not**). Your physics is again the right filter: if a claimed rule can't be traced to a fault-current or thermal argument, be suspicious.

**Projects / practice (within the legal limits):**
- **Study-only (safe, high-value):** take a real consumer-unit/panel schedule and *design* it — assign circuits, size cables and breakers, compute diversity, check Zs and voltage drop by hand, then validate against the code tables.
- **Simulate:** model a fault loop and breaker coordination using free manufacturer selectivity tools (ABB/Schneider).
- **Hands-on (supervised, or on a de-energized training rig only):** terminate cables, wire an MCB/RCD onto a training board, and run the full **inspection-and-test sequence** with an MFT. The measurement half — insulation resistance, Zs, RCD timing — is genuinely instructive and safe on a dead rig.

**Time:** ~40–80 h for solid literacy; full trade competence is a multi-year apprenticeship. **MVP:** one code framework (yours — DIN VDE 0100 for Germany) + Scaddan "Explained" + Cauldwell for the "why" + one pass through the test-and-inspect procedure ≈ 25–30 h.

### Companion II — The Power Grid: From Generation to Your Outlet

**Objective:** Trace electrical energy from the generator to the wall socket, and understand how the grid is kept stable, balanced, and protected — at a level that connects your physics (rotating machines, oscillators, conservation laws) to real power-system engineering.
**Prerequisites:** Phases 0–2 (AC, phasors, three-phase); Phase 6 (power electronics) for the inverter/HVDC parts; helpful: your mechanics — the swing equation is a pendulum.

**The domain map (generation → transmission → distribution → home):**
1. **Generation** — the **synchronous generator** (the workhorse: rotating field, `f = pN/120`), driven by steam (coal/gas/**nuclear**), hydro, or gas turbines; plus **inverter-based resources (IBR)** — wind and solar PV, which connect through power electronics, not spinning mass.
2. **Frequency = the balance signal** — **50 Hz** (Europe/India) or **60 Hz** (North America) holds constant only when generation exactly matches load; any imbalance appears instantly as a frequency deviation, arrested first by **rotational inertia**, then by **primary → secondary → tertiary control** (droop → AGC → dispatch).
3. **Why three-phase, why high voltage** — three-phase delivers constant instantaneous power with less conductor; transmission voltage is stepped **up** (hundreds of kV) specifically to cut **I²R losses** (`P = VI` ⇒ higher V ⇒ lower I ⇒ lower loss).
4. **Transmission** — **transformers**, EHV AC lines, and **HVDC** for long distances, asynchronous ties, and offshore wind. Lines use the same distributed-vs-lumped distinction you met in RF — but at 50/60 Hz the line is "electrically short," so π-section lumped models dominate.
5. **Substations & switchgear** — step-up/step-down, isolation, and **protection** (relays, breakers).
6. **Distribution** — **medium-voltage** primary feeders → **distribution transformers** → **low-voltage** secondary → the **service connection** to the building (where Companion I picks up).
7. **System analysis (the math):** the **per-unit** system, **power-flow (load-flow)** by Newton–Raphson, **fault analysis** via **symmetrical components (Fortescue)**, and **stability** (rotor-angle, voltage, frequency) governed by the **swing equation**.
8. **The modern grid** — renewables integration, **declining system inertia** and **grid-forming inverters**, storage, demand response, the **"duck curve,"** and electricity **markets** (day-ahead/intraday; in Germany/EU, EPEX SPOT).

**Grid architecture, by region:**
- **Continental Europe (primary anchor):** one large **synchronous area at 50 Hz**, coordinated by **ENTSO-E**. Germany is operated by four TSOs — **50Hertz, Amprion, TenneT DE, TransnetBW** — with distribution via many **DSOs**; grid-connection rules per the **VDE-AR-N** series.
- **North America:** three asynchronous **interconnections** — **Eastern, Western, and ERCOT (Texas)** — tied by HVDC links, under **NERC** reliability standards.
- **India:** a single synchronous **National Grid at 50 Hz**, operated under the **Indian Electricity Grid Code (IEGC)**.

**Primary resources (annotated, with sequencing):**
- **Best conceptual entry for a physicist — start here:** **Alexandra von Meier, *Electric Power Systems: A Conceptual Introduction* (Wiley-IEEE Press, 2006).** Unusually clear on the *physics and intuition* (why frequency matters, what reactive power really is) without drowning in per-unit bookkeeping. Her recorded lectures are available online.
- **The standard rigorous textbook:** **J. Duncan Glover, Mulukutla S. Sarma, Thomas J. Overbye & Adam B. Birchfield, *Power System Analysis and Design*, 7th ed. (Cengage, 2022).** Per-unit, transformers, transmission-line parameters, power-flow, faults, symmetrical components, protection, stability — and it ships with the **free student edition of PowerWorld Simulator**, which is genuinely good for *seeing* power flow and contingencies.
- **Concise, EU-flavored alternative:** **B. M. Weedy, B. J. Cory, N. Jenkins, J. B. Ekanayake & G. Strbac, *Electric Power Systems*, 5th ed. (Wiley, 2012).**
- **Stability & control, the deep reference:** **Prabha S. Kundur & Om P. Malik, *Power System Stability and Control*, 2nd ed. (McGraw-Hill, 2022)** — the classic, updated with renewables/IBR and cyber-security context. The original 1994 edition remains revered; the 2nd adds the modern material. Consult, don't read cover-to-cover.
- **Renewables / IBR & inertia (evolving frontier):** supplement the textbooks with recent review papers and **NERC / ENTSO-E** reports on grid-forming inverters and system inertia — this is moving too fast for any 2022 textbook.

**Free resources (flagged):** **MIT OCW 6.061 *Introduction to Electric Power Systems* (James Kirtley)** — a full rigorous free course; **NPTEL** power-systems courses (several, strong, free on YouTube); the **PowerWorld** free student simulator; von Meier's online lectures; and **ENTSO-E's public transparency platform** for real European grid data — a fun dataset given your Python/analytics background.

**Physics cross-links (unusually rich — your biggest advantage in this section):**
- **The swing equation *is* the driven-pendulum / coupled-oscillator equation:** `M d²δ/dt² = P_m − P_e` — rotor angle δ obeys the same dynamics as a physical pendulum, and a multi-machine grid is a network of coupled oscillators (the **Kuramoto model** is literally used to study grid synchronization). The most satisfying bridge in the whole document for a physicist.
- **Frequency stability ↔ conservation + inertia:** stored rotational kinetic energy `½Jω²` is the grid's shock absorber; replacing spinning mass with inverters removes that buffer — a live research problem you can reason about from first principles.
- **Symmetrical components (Fortescue) ↔ a change of basis / a 3-point DFT:** decomposing three unbalanced phasors into positive/negative/zero sequence is the eigendecomposition of a circulant (cyclic) system — the same linear-algebra move as the DFT you use in feature work.
- **Reactive power Q ↔ energy sloshing** in inductive/capacitive fields (zero average, but it still loads the network) — the Phase-2 power triangle at grid scale.
- **Why HV transmission ↔ Joule's law:** the whole architecture exists to minimize `I²R`.
- **Transmission lines ↔ the wave equation** again — but here in the "electrically short" regime, a nice contrast to the RF phase where the line is long.

**Calibration — settled vs. contested vs. folklore:**
- **Settled:** three-phase and per-unit analysis; why HV transmission; synchronous-machine operation; symmetrical components; power-flow and the swing equation; frequency-as-balance.
- **Contested / active research & policy:** how severe the **inertia decline** from high-IBR penetration really is, and whether **grid-forming inverters** fully substitute for synchronous inertia (open, fast-moving); **HVDC vs. AC** expansion strategy; **market design** — Europe's **zonal** pricing vs. the US **nodal (LMP)** model is a genuine unresolved economics-and-engineering debate; capacity vs. energy-only markets.
- **Overstated / folklore (both directions):** "**renewables will collapse the grid**" and "**baseload is obsolete / inertia doesn't matter**" are *both* slogans; the honest engineering picture is a manageable-but-real set of stability challenges with active solutions. Treat confident one-liners on either side with the skepticism you'd apply to a too-good backtest.

**Projects / exercises:**
- **PowerWorld:** build a small multi-bus system, run a power-flow, then trip a line and watch the contingency redistribute flows and voltages; add a generator and observe frequency/AGC behavior.
- **Python (home turf):** pull real load/frequency/price data from **ENTSO-E's transparency platform** and analyze it — e.g., correlate day-ahead prices with wind/solar output, or visualize frequency excursions.
- **By hand:** do a per-unit fault calculation with symmetrical components for a simple network; derive the two-machine swing-equation equilibrium and its small-signal oscillation frequency (and recognize it as a pendulum).

**Time:** ~40–70 h for strong conceptual command via von Meier + MIT 6.061; Glover cover-to-cover with PowerWorld is a further ~80–120 h; Kundur-level stability depth is a major additional commitment. **MVP:** von Meier (concepts) + the transmission/distribution and power-flow/fault/stability chapters of Glover + one PowerWorld contingency exercise + one ENTSO-E data pull ≈ 30–40 h.

**Currency & region caveats for these two companions:** Wiring codes update on fixed cycles and differ by jurisdiction — **NEC 2026** (US, 3-year cycle, next edition 2029), **BS 7671:2018+A4:2026** (UK "Orange Book," April 2026; the A2:2022+A3:2024 "Brown Book" is valid only until 15 October 2026), and the ever-evolving **DIN VDE 0100 / IEC 60364** series — so always confirm the current edition *for your locale* before relying on any specific rule. The grid companion's IBR/inertia/market material is the fastest-moving content here; the 2022 textbooks are solid on fundamentals but should be supplemented with current NERC/ENTSO-E literature for the frontier. Nothing in Companion I is a substitute for a licensed electrician or for local law.

## Caveats
- **Time estimates assume ~8–12 focused hours/week** and vary widely with depth; the full program is a multi-year commitment, which matches your stated intent.
- **Edition currency (verified early 2026):** Sedra & Smith 8th (2020), Razavi *Fundamentals of Microelectronics* 3rd (2021), Razavi *Design of Analog CMOS* 2nd (2017), Razavi *RF Microelectronics* 2nd (2011/12), Streetman 7th (2014/15), Sze 4th (2021), Erickson & Maksimović 3rd (2020), Mohan/Undeland/Robbins 3rd (2003), Pozar 4th (2012), Harris & Harris RISC-V (2021), Nilsson & Riedel 12th (2023), *Art of Electronics* 3rd (2015). Note: **Mohan and Pozar have not had recent new editions** — they remain standard, but expect some dated device coverage. **Razavi's RF text (2011) predates the newest RF-CMOS nodes** — supplement with recent papers for cutting-edge work.
- **Software versions move fast:** LTspice, ngspice (v46, March 2026), and KiCad (v9/v10) update frequently; the versions cited are early-2026 snapshots. PySpice specifically is in flux — prefer the maintained InSpice fork if you script SPICE from Python.
- **Hardware prices** are MSRP/typical-distributor as of 2026 and fluctuate; academic pricing (AD3 at $249) requires eligibility verification, and the ADALM2000's street price ranges roughly $232–$253 across distributors.
- **No definitive full Ali Hajimiri/Caltech RF video lecture series could be confirmed as freely posted**; Razavi's UCLA lectures (YouTube) and UC Berkeley EE105/EE140 course materials are the confirmed well-regarded free options.
- This curriculum optimizes for **depth/derivation over build-first**, per your explicit preference; a hobbyist would sequence very differently.