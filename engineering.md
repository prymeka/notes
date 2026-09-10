# The Four-Cores Engineering Curriculum: A Layered Trunk-and-Branch Self-Study Program

**For:** An ML engineer (fraud prevention, PayPal) with an MSc in AI and BSc in Physics, strong Python, physicist-level math maturity. Self-directed, no grading, primary-source mastery.

**Verification note:** All textbook editions and open-resource links below were verified via web search in September 2026.

---

## TL;DR
- This is a placement-plus-four-cores program: Layer 0 (math/physics) is a review checklist you mostly test out of; Layer 1 is a shared "trunk" of eight engineering sciences reused across all cores; Layer 2 develops Mechanical, Electrical, Civil, and Chemical engineering to solid undergraduate depth with explicitly-flagged graduate extensions; Layer 3 is four lightweight specialization addendums (Aerospace, Biomedical, Materials, Industrial) for conversational depth only.
- The spine is canonical textbooks in verified current editions — Strang *Introduction to Linear Algebra* 6th ed. (ISBN 978-1-7331466-7-8, published Jan 26, 2023, Wellesley-Cambridge Press, whose closing Chapter 10 now "describes the key ideas of Deep Learning"), Hibbeler *Statics* 15th, Çengel–Boles–Kanoglu *Thermodynamics* 10th ed. (ISBN 978-1266664489, published Jan 30, 2023, McGraw Hill), Sedra–Smith 8th/2020, Bird–Stewart–Lightfoot Revised 2nd, Fogler 6th/2020, Callister 10th — backed by free/open resources (MIT OpenCourseWare, LibreTexts Engineering, NPTEL, the Baker–Haynes open Statics text) and Python-first computational exercises (NumPy/SciPy, ngspice, FEniCS/OpenFOAM, Cantera, CoolProp).
- Full program envelope is long (multi-year part-time); the MVP fast-path compresses to the trunk plus one chosen core in roughly 6–9 months of serious part-time study. Classical fundamentals are SETTLED; the CONTESTED/HYPE tags are used mainly to flag region-specific codes (Eurocode vs. US ASCE/AISC/ACI — relevant to you in Europe) and vendor/tool claims.

---

## Key Findings (How to read and use this document)

1. **Trunk-and-branch, not four separate degrees.** The eight Layer-1 engineering sciences are the shared trunk. Every Layer-2 core reuses them; you learn thermodynamics, fluids, solid mechanics, circuits, and control *once* in Layer 1 and then specialize. This is why doing all four cores is far less than 4× the work.

2. **You already own most of Layer 0 and large parts of Layer 1.** As a physicist you have classical mechanics (→ statics/dynamics), E&M (→ circuits and electromagnetics), thermodynamics and stat mech (→ engineering thermo and, later, molecular thermo), oscillators/waves (→ vibrations, signals, RLC), and the full math stack. The curriculum flags exactly where to sprint and where genuinely new engineering content lives (design codes, empirical correlations, manufacturing, standards).

3. **Calibrated tags.** Each major block is tagged **SETTLED** (established science/engineering, not in dispute), **CONTESTED** (legitimate variation — usually regional codes or competing best practices), or **HYPE** (where popular/vendor claims outrun evidence). Classical engineering is overwhelmingly SETTLED; tags mostly warn you about code regionalism and tooling marketing.

4. **Free/open resources are flagged with ⭐ and verified live.** Commercial canonical texts remain the spine, but for every block there is at least one legitimately free alternative.

---

## DEPENDENCY MAP

```
LAYER 0 (Foundations — placement/review; mostly test out)
  Math: calculus (1V/MV), linear algebra, ODEs+intro PDEs, prob/stats, numerical methods
  Physical science: classical mechanics, thermo, E&M, modern physics, general chemistry
        │
        ▼
LAYER 1 (Common Engineering Sciences — the SHARED TRUNK)
  1A Statics & Mechanics of Materials ──────────┐
  1B Fluid Mechanics ───────────────────────────┤
  1C Engineering Thermodynamics ────────────────┤
  1D Heat & Mass Transfer (Transport) ──────────┤
  1E Electric Circuits & Basic Electronics ─────┤
  1F Signals & Systems ─────────────────────────┤
  1G Materials Science Fundamentals ────────────┤
  1H Systems & Control Fundamentals ────────────┘
        │            │            │            │
        ▼            ▼            ▼            ▼
LAYER 2 (Four Cores — undergrad depth; grad reach flagged)
  MECH ← 1A,1B,1C,1D,1G,1H (+dynamics, machine design, vibrations, manufacturing)
  ELEC ← 1E,1F,1H (+analog/digital, EM, power, comms, semiconductors)
  CIVIL← 1A,1B,1G (+structural steel/RC, geotech, hydrology, transportation, surveying, environmental)
  CHEM ← 1B,1C,1D,1G (+mat/energy balances, chem thermo, reaction eng, separations, process control, plant design)
        │
        ▼
LAYER 3 (Specialization ADDENDUMS — conversational only)
  AEROSPACE  ← branches from MECH (+ELEC for avionics)
  BIOMEDICAL ← branches from ELEC/MECH (+CHEM for biotransport)
  MATERIALS  ← branches from CHEM/MECH (+1G)
  INDUSTRIAL ← branches from your existing math/OR/stats + all cores
```

**Prerequisite rules of thumb:**
- 1A→1B (fluid statics builds on statics); 1C→1D (thermo before transport); 1E→1F→1H (circuits→signals→control); 1G is largely standalone (solid-state physics prerequisite you already have).
- Every Layer-2 core presupposes its listed Layer-1 blocks. Do not start a core until its trunk prerequisites are green on the placement checklist.

---

## OVERALL TIME ENVELOPE

- **Full program (all four cores to undergrad depth + all four addendums):** a multi-year part-time undertaking. Budget roughly Layer 1 trunk ≈ 4–6 months; each Layer-2 core ≈ 3–5 months; the four addendums ≈ 3–5 weeks total. At ~8–10 hrs/week this is on the order of 2.5–3.5 years; at 15–20 hrs/week, compressible toward ~1.5 years.
- **MVP fast-path (whole program):** Layer 0 checklist (fast) → Layer 1 trunk MVP (core chapters only) → ONE core of your choice → skim the four addendums. ≈ 6–9 months part-time. See the per-phase MVP boxes and the consolidated MVP at the end.

---

# LAYER 0 — FOUNDATIONS (PLACEMENT / REVIEW CHECKLIST)

**Tag: SETTLED.** This layer is not taught from scratch. Treat it as a self-diagnostic: for each item, attempt a few representative problems; if fluent, check it off; if rusty, use the targeted resource.

### Goal
Confirm the mathematical and physical-science prerequisites are fluent, and patch the two or three gaps a physicist typically has.

### Prerequisites
None (this is the base).

### Placement checklist — MATH (you almost certainly have all of this)
- Single- and multivariable calculus; vector calculus (grad/div/curl, Green/Stokes/divergence theorems).
- Linear algebra (eigen-decomposition, SVD, positive-definiteness).
- ODEs and an introduction to PDEs (separation of variables, the heat/wave/Laplace equations).
- Probability & statistics (you use this daily in ML).
- Numerical methods.

### Placement checklist — PHYSICAL SCIENCE
- Newtonian/classical mechanics ✅ (BSc physics).
- Thermodynamics & statistical mechanics ✅.
- Electromagnetism ✅ (Maxwell's equations).
- Modern physics (quantum, solid-state basics) ✅ — directly powers semiconductor devices and materials.
- General chemistry — **likely gap flag** (see below).

### Likely gaps for a physicist (patch these)
- **Engineering-specific numerical methods.** You know the math; you may not have done engineering-flavored FEM/CFD/finite-difference discretization or root-finding on empirical correlations. *Primary:* Strang, *Computational Science and Engineering* (Wellesley-Cambridge). ⭐ Free alternative: **MIT OCW 18.085/18.086 "Computational Science and Engineering I/II"** (Strang's own course; video + problem sets).
- **General/engineering chemistry, if rusty.** Needed mainly for Chemical core and Materials. ⭐ Free: **LibreTexts Chemistry** (chem.libretexts.org) — target stoichiometry, thermochemistry, equilibria, electrochemistry, phase diagrams. Physicists usually need only the chemical-equilibrium and reaction-stoichiometry pieces.
- **Statistics for engineering/quality** (design of experiments, control charts) — deferred to the Industrial addendum; your ML stats mostly covers it.

### Primary readings (reference, not cover-to-cover)
- Strang, *Introduction to Linear Algebra*, **6th ed. (ISBN 978-1-7331466-7-8, published Jan 26, 2023, Wellesley-Cambridge Press)** — the current edition, whose closing Chapter 10 now "describes the key ideas of Deep Learning" (directly relevant to your ML work); ⭐ pairs with the free **MIT OCW 18.06** video course and problem sets.
- Boyce, DiPrima & Meade, *Elementary Differential Equations (and Boundary Value Problems)*, **11th ed. (2017, Wiley)** — current edition.
- Kreyszig, *Advanced Engineering Mathematics*, **10th ed. (Wiley)** — the standard single-volume engineering-math reference; keep on the shelf for special functions, PDEs, complex analysis, and transforms as they arise in later layers.

### Supplementary
- 3Blue1Brown "Essence of Linear Algebra" / "Essence of Calculus" (intuition refreshers, supplementary only).

### Exercises / computational
- Rebuild 3–4 canonical numerical routines in Python from scratch (Newton–Raphson, RK4, finite-difference Poisson solver, least-squares) to confirm the engineering-numerics gap is closed. This doubles as warm-up for later simulation work.

### Time estimate
1–3 weeks if only patching gaps; skip almost entirely if placement is clean.

> **MVP fast-path (Layer 0):** Skip everything except a 2-hour diagnostic. Patch only chemistry (if doing Chemical core) and engineering numerical methods (if doing simulation-heavy cores).

---

# LAYER 1 — COMMON ENGINEERING SCIENCES (THE SHARED TRUNK)

**Overall tag: SETTLED.** These are the reusable engineering sciences. Physics scaffolding is called out per block; move fast where flagged.

---

## Phase 1A — Statics & Mechanics of Materials

### Goal
Master force/moment equilibrium of rigid bodies and internal stress/strain/deformation of deformable bodies — the basis of all structural and machine analysis.

### Prerequisites
Layer 0 (vector calculus, Newtonian mechanics).

### Primary readings
- Hibbeler, *Engineering Mechanics: Statics*, **15th ed. (Pearson)** — current edition.
- Hibbeler, *Mechanics of Materials* (current Pearson edition) — stress, strain, torsion, beam bending, deflection, buckling, Mohr's circle.
- ⭐ **Free open primary alternative:** Baker & Haynes, *Engineering Statics: Open and Interactive* (CC BY-NC-SA 4.0, engineeringstatics.org and Engineering LibreTexts) — a genuinely open, interactive statics textbook.

### Supplementary
- ⭐ MIT OCW **2.001 Mechanics & Materials I**.
- Gere & Goodno, *Mechanics of Materials*, **9th ed. (2018, Cengage)** — alternate primary for mechanics of materials; widely used in civil.

### Physics scaffolding
Statics is Newton's laws with zero acceleration; you can move fast. The genuinely new content is engineering bookkeeping (free-body diagrams, trusses/frames, distributed loads, second moments of area) and the stress-transformation formalism (Mohr's circle = a rotation in a symmetric-tensor eigenbasis — familiar from the physics of the inertia/stress tensor).

### Exercises / computational
- Work Hibbeler truss/frame and beam-deflection problem sets by hand.
- **Python:** write a 2-D pin-jointed truss solver (assemble equilibrium equations, solve with NumPy) and verify against textbook answers — direct bridge to the stiffness method / FEA later.

### Time estimate
4–6 weeks.

> **MVP:** Statics ch. on equilibrium + trusses; Mechanics of Materials ch. on axial/torsion/bending only. 2 weeks.

---

## Phase 1B — Fluid Mechanics

### Goal
Fluid statics, control-volume conservation laws, Bernoulli/energy, dimensional analysis and similitude, internal (pipe) and external (boundary-layer) flow, momentum integral methods.

### Prerequisites
1A; Layer 0 vector calculus.

### Primary readings
- White, *Fluid Mechanics*, **8th ed. (2016, McGraw-Hill)** — current edition; rigorous, control-volume-first.
- Alternate primary: Fox & McDonald's *Introduction to Fluid Mechanics* (current Wiley edition) or Munson's *Fundamentals of Fluid Mechanics* (Wiley) — the latter is favored in civil/hydraulics.

### Supplementary
- ⭐ LibreTexts *Fluid Mechanics* (Bar-Meir), open-license.
- ⭐ NPTEL fluid mechanics course sequences (nptel.ac.in — verified live; free courseware, optional paid certification).

### Physics scaffolding
The Navier–Stokes equations are Newton's second law for a continuum plus the continuity (mass-conservation) equation — you have already met continuity and the material derivative. Dimensional analysis/Buckingham-Π is the physicist's scaling-and-nondimensionalization instinct formalized. Reynolds/Froude/Mach numbers are ratios of physical effects.

### Exercises / computational
- Hand-work pipe-network and momentum problems.
- **Python:** solve the Blasius boundary-layer ODE (shooting method + SciPy); compute Moody-chart friction factors by iterating the Colebrook equation.

### Time estimate
5–7 weeks.

> **MVP:** Fluid statics, control-volume mass/momentum/energy, and pipe-flow friction. 2.5 weeks.

---

## Phase 1C — Engineering Thermodynamics

### Goal
Property evaluation (tables/EOS), first and second laws for closed and open systems, entropy and exergy, power/refrigeration cycles.

### Prerequisites
Layer 0 thermo.

### Primary readings
- Çengel, Boles & Kanoglu, *Thermodynamics: An Engineering Approach*, **10th ed. (ISBN 978-1266664489, published Jan 30, 2023, McGraw Hill)** — current edition; the standard.

### Supplementary
- ⭐ LibreTexts *Introduction to Engineering Thermodynamics* (Yan), open-license.
- ⭐ MIT OCW thermodynamics offerings (e.g., 2.005 Thermal-Fluids Engineering).

### Physics scaffolding
You know the laws; the new material is *engineering* property-handling (steam tables, quality, compressibility charts, EOS) and *device-level cycle analysis* (Rankine, Brayton, vapor-compression). Exergy/availability is your "useful work relative to dead state" — a repackaging of the second law you already understand. Move fast on the conceptual chapters; spend your time on cycle problems and property retrieval.

### Exercises / computational
- Cycle-analysis problem sets (Rankine with reheat/regeneration; Brayton with intercooling).
- **Python:** use **CoolProp** (⭐ free) to pull properties and script a parametric Rankine-cycle efficiency study — leverages your Python strength and removes table-lookup drudgery.

### Time estimate
4–6 weeks.

> **MVP:** First/second law for control volumes + one power cycle + one refrigeration cycle. 2 weeks.

---

## Phase 1D — Heat & Mass Transfer (Transport)

### Goal
Conduction (steady/transient), convection (forced/natural, internal/external), radiation, heat exchangers, and an introduction to mass diffusion (the transport analogy).

### Prerequisites
1B, 1C.

### Primary readings
- Çengel & Ghajar, *Heat and Mass Transfer: Fundamentals and Applications*, **6th ed. (2020, McGraw-Hill)** — current edition; consistent notation with the thermo text.
- Alternate/deeper: Incropera, DeWitt, Bergman & Lavine, *Fundamentals of Heat and Mass Transfer* (Wiley).

### Supplementary
- ⭐ MIT OCW **10.302 Transport Processes** (Fall 2004; verified live; free problem sets/exams) — heat and mass transfer with a chem-eng flavor; a useful bridge into the Chemical core.

### Physics scaffolding
Fourier's law, Newton's law of cooling, and Fick's law are all the same gradient-flux linear-response structure you know from diffusion and conduction in physics. The heat equation is the diffusion equation. Transient conduction = separation of variables + eigenfunction expansions (Layer 0). Dimensionless groups (Nusselt, Prandtl, Biot, Fourier) are scaling ratios.

### Exercises / computational
- Fin, lumped-capacitance, and heat-exchanger (LMTD/ε-NTU) problems.
- **Python:** finite-difference solver for 2-D steady conduction (Laplace) and 1-D transient conduction (explicit/implicit) — reuses your Layer-0 Poisson solver and previews FEA/CFD.

### Time estimate
4–6 weeks.

> **MVP:** 1-D conduction, one convection correlation set, and ε-NTU heat exchangers. 2 weeks.

---

## Phase 1E — Electric Circuits & Basic Electronics

### Goal
DC/AC circuit analysis (nodal/mesh, Thévenin/Norton, phasors), transient RLC response, op-amps, and first semiconductor devices (diodes, BJT/MOSFET biasing).

### Prerequisites
Layer 0 E&M and ODEs.

### Primary readings
- Circuits: Irwin, *Basic Engineering Circuit Analysis* (current Wiley ed.), or Hayt, *Engineering Circuit Analysis* (current McGraw-Hill ed.) — either is a fine primary.
- Sedra, Smith, Carusone & Gaudet, *Microelectronic Circuits*, **8th ed. (2020, Oxford)** — current edition; the standard for devices/analog.

### Supplementary
- ⭐ MIT OCW **6.002 Circuits and Electronics** (full video + assignments).
- ⭐ All About Circuits (free online text) — supplementary reference.

### Physics scaffolding
This is your strongest fast-track. The series RLC circuit *is* the damped harmonic oscillator: L↔mass, R↔damping, 1/C↔spring constant, and the quality factor Q is identical. Phasor analysis is complex-exponential steady-state you already use. You can compress DC/AC analysis dramatically and spend time on the genuinely new engineering content: op-amp topologies and transistor biasing/small-signal models.

### Exercises / computational
- Nodal/mesh and transient RLC problem sets.
- **Python/SPICE:** install **ngspice** (⭐ free) and simulate an RLC transient, an op-amp amplifier, and a common-source MOSFET stage; compare simulated Bode plots to hand analysis. Optionally drive ngspice from Python (PySpice) for parametric sweeps.

### Time estimate
5–7 weeks.

> **MVP:** Nodal/mesh + phasors + one op-amp circuit + diode/MOSFET biasing basics. 2.5 weeks (you can skip much of DC analysis).

---

## Phase 1F — Signals & Systems

### Goal
LTI systems, convolution, Fourier series/transform, Laplace and z-transforms, sampling, frequency response — continuous and discrete time.

### Prerequisites
1E (helpful), Layer 0 (ODEs, complex analysis).

### Primary readings
- Oppenheim, Willsky & Nawab, *Signals and Systems*, **2nd ed. (Pearson)** — the canonical text.
- (Discrete-time follow-on:) Oppenheim & Schafer, *Discrete-Time Signal Processing*, **3rd ed. (2010, Pearson)** — the definitive DSP reference; use in EE core's advanced DSP block.

### Supplementary
- ⭐ MIT OCW **6.003 Signals and Systems** (Fall 2011; full lectures + problem sets).

### Physics scaffolding
Fourier/Laplace are second nature to you. Convolution as the impulse-response integral is Green's-function thinking. Poles/zeros and stability are the eigenvalue/complex-plane analysis you already do for dynamical systems. This is mostly reframing familiar math in engineering language — move fast, but do enough z-transform and sampling problems (these are the parts most physicists have *not* seen).

### Exercises / computational
- Convolution, Fourier/Laplace, sampling/aliasing problem sets.
- **Python:** use `scipy.signal` to design and analyze filters, plot Bode/pole-zero diagrams, and demonstrate aliasing; implement the DFT/FFT and verify against `numpy.fft`.

### Time estimate
4–5 weeks (faster given your background).

> **MVP:** LTI + convolution + Fourier + sampling theorem + z-transform basics. 2 weeks.

---

## Phase 1G — Materials Science Fundamentals

### Goal
Atomic bonding, crystal structures and defects, phase diagrams and phase transformations, mechanical properties, electrical/thermal properties, failure (fatigue/creep/fracture), and materials classes (metals, ceramics, polymers, composites).

### Prerequisites
Layer 0 (modern physics / solid-state basics), some chemistry.

### Primary readings
- Callister & Rethwisch, *Materials Science and Engineering: An Introduction*, **10th ed. (2018, Wiley)** — current edition; the standard.

### Supplementary
- ⭐ MIT OCW **3.091 (Solid-State Chemistry)** and **3.012** for structure/thermodynamics of materials.

### Physics scaffolding
Crystallography and reciprocal lattices are solid-state physics you likely already know; Miller indices, Bravais lattices, and X-ray diffraction (Bragg) map directly. Electronic properties (band theory, Fermi–Dirac occupation) power the semiconductor content in the EE core. The genuinely new engineering content is phase diagrams (lever rule, eutectics), TTT/CCT diagrams, and mechanical-property/processing-microstructure relationships.

### Exercises / computational
- Phase-diagram (lever-rule), crystallographic-indexing, and tensile-property problems.
- **Python:** compute and plot a binary phase diagram / lever-rule tie-lines; index a simulated powder-diffraction pattern.

### Time estimate
3–5 weeks (compressible given solid-state background).

> **MVP:** Bonding/structure, phase diagrams + lever rule, mechanical properties, and failure modes. 2 weeks.

---

## Phase 1H — Systems & Control Fundamentals

### Goal
Modeling of dynamic systems, transfer functions and state space, transient/steady-state response, stability (Routh, root locus, Bode/Nyquist), and PID/lead-lag design.

### Prerequisites
1F (transforms), Layer 0 (ODEs, linear algebra).

### Primary readings
- Nise, *Control Systems Engineering*, **8th ed. (2020, Wiley)** — current edition; accessible and design-oriented. (Ogata, *Modern Control Engineering*, is the more mathematical alternate primary.)

### Supplementary
- ⭐ MIT OCW **6.302 / 2.004** control offerings; ⭐ Brian Douglas "Control System Lectures" (intuition, supplementary).

### Physics scaffolding
Control stability *is* dynamical-systems analysis: poles in the complex plane, eigenvalues of the state matrix, phase-space and linearization about fixed points — all familiar. State-space form is a first-order ODE system ẋ = Ax + Bu. What's new is the *design* machinery (root locus, loop-shaping, PID tuning) and frequency-domain stability margins.

### Exercises / computational
- Root-locus, Bode, and PID-tuning problem sets by hand.
- **Python:** use the `python-control` library to model plants, plot root loci and Bode/Nyquist diagrams, and tune a PID controller in simulation. Given your ML background, note the link to modern data-driven/optimal control (LQR/MPC) as an optional thread.

### Time estimate
4–6 weeks.

> **MVP:** Transfer functions, stability (Routh + Bode margins), and PID design. 2 weeks.

---

# LAYER 2 — THE FOUR CORES

Each core is to **solid undergraduate depth**; **graduate-reach** sub-areas are tagged **[GRAD]** so you can opt in per interest. Do not force graduate depth everywhere.

---

## Phase 2-MECH — Mechanical Engineering

### Goal
Undergraduate mastery across dynamics, advanced solid mechanics, fluids/thermal, machine design, vibrations, control, and manufacturing.

### Prerequisites
Trunk 1A, 1B, 1C, 1D, 1G, 1H.

### Primary readings
- Hibbeler, *Engineering Mechanics: Dynamics*, **15th ed. (Pearson)** — kinematics/kinetics, work-energy, impulse-momentum, rigid-body dynamics.
- Budynas & Nisbett, *Shigley's Mechanical Engineering Design*, **11th ed. (2020, McGraw-Hill)** — the machine-design bible (fatigue, shafts, gears, bearings, fasteners).
- Rao, *Mechanical Vibrations*, **6th ed. (Pearson)** — SDOF/MDOF, modal analysis, forced response.
- (Fluids/thermal/heat and control reuse White, Çengel, Nise from Layer 1.)

### [GRAD] Graduate reach
- **Continuum mechanics:** Lai, Rubin & Krempl, *Introduction to Continuum Mechanics*; or Gurtin. (Tensor formalism you already know from physics.)
- **Computational methods — FEA:** Hughes, *The Finite Element Method*; ⭐ practice with free **FEniCS/FEniCSx** or **CalculiX**.
- **Computational methods — CFD:** Versteeg & Malalasekera, *An Introduction to CFD: The Finite Volume Method*; ⭐ practice with free **OpenFOAM**.
- **Advanced/nonlinear dynamics & control:** Strogatz, *Nonlinear Dynamics and Chaos* (you may already own this); Khalil, *Nonlinear Systems*.
- **Combustion/propulsion:** Turns, *An Introduction to Combustion*.

### Physics scaffolding
Rigid-body dynamics (Euler's equations, inertia tensor, Lagrangian methods) is direct classical mechanics. Vibrations = coupled harmonic oscillators; modal analysis = eigen-decomposition of the mass/stiffness matrices. You can move quickly through dynamics and vibrations and invest in the *engineering-design* content (fatigue life, factor-of-safety codes, gear/bearing selection) and manufacturing, which are new.

### Manufacturing processes
- Kalpakjian & Schmid, *Manufacturing Engineering and Technology* (current Pearson ed.) — casting, forming, machining, joining, additive. **Tag: SETTLED**, but additive-manufacturing performance claims are often **HYPE** in vendor literature — treat AM property claims skeptically.

### Exercises / computational
- Shigley fatigue/shaft-design problems; Rao modal-analysis problems.
- **Python/FEA:** solve a cantilever-beam natural-frequency problem analytically, then in FEniCS/CalculiX, and compare; a simple OpenFOAM lid-driven-cavity or pipe-flow tutorial for CFD literacy.

### Time estimate
4–5 months undergrad; +2–4 months if pursuing [GRAD] FEA/CFD.

> **MVP:** Dynamics + Shigley (fatigue, shafts) + vibrations SDOF/MDOF; reuse trunk thermal/fluids/control. ~6 weeks.

---

## Phase 2-ELEC — Electrical Engineering

### Goal
Undergraduate mastery across circuits, analog/digital electronics, signals & DSP, electromagnetics, control, power, communications, and semiconductor devices.

### Prerequisites
Trunk 1E, 1F, 1H.

### Primary readings
- Sedra, Smith, Carusone & Gaudet, *Microelectronic Circuits*, **8th ed. (2020, Oxford)** — analog and digital electronics (reused/deepened from 1E).
- Oppenheim & Schafer, *Discrete-Time Signal Processing*, **3rd ed. (2010, Pearson)** — DSP.
- Sadiku, *Elements of Electromagnetics*, **7th ed. (2018, Oxford)** — fields, transmission lines, waves. (Hayt, *Engineering Electromagnetics*, is the alternate primary.)
- Digital logic: Harris & Harris, *Digital Design and Computer Architecture* (⭐ free companion materials) or Wakerly.

### [GRAD] Graduate reach
- **RF/microwave:** Pozar, *Microwave Engineering*.
- **Advanced DSP / statistical SP:** Hayes, *Statistical Digital Signal Processing*.
- **Semiconductor device physics:** Sze & Ng, *Physics of Semiconductor Devices* (your quantum/solid-state background is the prerequisite).
- **Power electronics:** Erickson & Maksimović, *Fundamentals of Power Electronics*.
- **Information/communication theory:** Proakis & Salehi, *Digital Communications*; Cover & Thomas, *Elements of Information Theory* (natural for an ML engineer).

### Physics scaffolding
Electromagnetics is your Maxwell's equations in engineering dress; transmission-line theory is wave propagation with the telegrapher's equations (a 1-D wave equation). Semiconductor devices run on Fermi–Dirac statistics, band theory, and drift-diffusion — physics you already have. This is arguably your fastest core on the theory side; invest in circuit *design* and DSP *implementation*.

### Exercises / computational
- Transmission-line/Smith-chart problems; filter-design and transistor-amplifier design.
- **Python/SPICE:** ngspice amplifier and filter designs; `scipy.signal` FIR/IIR filter design and real signal processing; optionally an information-theory notebook (entropy/mutual information) tying to your ML work.

### Time estimate
4–5 months undergrad; +2–4 months per [GRAD] thread.

> **MVP:** Deepen Sedra–Smith (amplifiers) + DSP (filter design) + electromagnetics through transmission lines. ~6 weeks.

---

## Phase 2-CIVIL — Civil Engineering

### Goal
Undergraduate mastery across structural analysis and steel/RC design, geotechnical/soil mechanics, hydraulics/hydrology, transportation, construction materials, surveying, and environmental basics.

### Prerequisites
Trunk 1A, 1B, 1G.

### Primary readings
- Hibbeler, *Structural Analysis*, **11th ed. (2023, Pearson)** — trusses, beams, frames, influence lines, force/displacement methods.
- McCormac & Csernak, *Structural Steel Design*, **6th ed. (2017/2018, Pearson)** — AISC-based (US, LRFD; the Pearson+ eText update is aligned to AISC 360-16).
- McCormac & Brown, *Design of Reinforced Concrete*, **10th ed. (2015/2016, Wiley)** — ACI-based (US).
- Das & Sobhan, *Principles of Geotechnical Engineering*, **9th ed. (2018, Cengage)** — soil mechanics.
- Munson et al., *Fundamentals of Fluid Mechanics* (reuse from 1B) for hydraulics.

### [GRAD] Graduate reach
- **FE structural analysis:** McGuire, Gallagher & Ziemian, *Matrix Structural Analysis* (⭐ free PDF from the authors).
- **Structural dynamics & earthquake engineering:** Chopra, *Dynamics of Structures*.
- **Advanced geotechnics:** Das, *Advanced Soil Mechanics*.

### ⚠️ CONTESTED — codes are regional (important for you in Europe)
Structural and geotechnical *design* is governed by codes that differ by jurisdiction. The US texts above teach **AISC 360 / ACI 318 (LRFD)**. **In Germany/Europe the governing codes are the Eurocodes: EN 1990 (basis), EN 1991 (actions/loads), EN 1992 (concrete, "EC2"), EN 1993 (steel, "EC3"), EN 1997 (geotechnical, "EC7"), EN 1998 (seismic, "EC8"), plus the German National Annexes (DIN EN).** The *mechanics* is SETTLED and identical; the *design philosophy, partial safety factors, and detailing rules differ*. Recommendation: learn the mechanics from the US texts, then read a Eurocode-based design text for your region — e.g., a *Designers' Guide to the Eurocodes* volume (Thomas Telford/ICE) or a German *Stahlbau/Stahlbetonbau nach Eurocode* text. Do not mix load factors across codes.

### Physics scaffolding
Structural analysis is statics/mechanics-of-materials scaled up; the matrix stiffness method is linear algebra (assemble, apply BCs, solve Ku=f) — directly the truss solver you built in 1A. Hydrology/hydraulics reuse fluid mechanics. Soil mechanics adds genuinely new empirical/constitutive content (effective stress, consolidation, shear strength) — spend time here.

### Exercises / computational
- Indeterminate-structure analysis (slope-deflection, moment distribution); RC beam and steel-column design checks; consolidation/settlement problems.
- **Python:** extend your truss solver into a 2-D frame stiffness-method code (beam elements with bending); compute a consolidation settlement time-history.

### Time estimate
4–5 months undergrad (+ time for Eurocode overlay); +2–3 months per [GRAD] thread.

> **MVP:** Structural analysis (determinate + one indeterminate method) + one steel and one RC design example + soil-mechanics basics (effective stress, shear strength). ~6–7 weeks.

---

## Phase 2-CHEM — Chemical Engineering

### Goal
Undergraduate mastery across material/energy balances, chemical-engineering thermodynamics, transport phenomena, reaction engineering, separations, process dynamics/control, and process/plant design & economics.

### Prerequisites
Trunk 1B, 1C, 1D, 1G; general chemistry (Layer 0 patch).

### Primary readings
- Felder, Rousseau & Bullard, *Elementary Principles of Chemical Processes*, **4th ed. (2020, Wiley)** — material and energy balances; the gateway course.
- Smith, Van Ness, Abbott & Swihart, *Introduction to Chemical Engineering Thermodynamics*, **9th ed. (ISBN 9781260721478, ©2022, McGraw Hill)** — current edition; Mark T. Swihart (UB Distinguished Professor and Chair of Chemical and Biological Engineering at the University at Buffalo, who "has taught Chemical Engineering Thermodynamics since 2002") was added as a coauthor for this edition. Covers phase/chemical equilibria, EOS, activity models.
- Bird, Stewart & Lightfoot, *Transport Phenomena*, **Revised 2nd ed. (2006/2007, Wiley)** — momentum/heat/mass transport, unified. **[GRAD-adjacent]**: BSL is rigorous; undergrad-level transport can also be met via Welty et al.
- Fogler, *Elements of Chemical Reaction Engineering*, **6th ed. (published Aug 18, 2020, Pearson)** — kinetics and reactor design; ⭐ its free companion site (umich.edu/~elements/6e) offers Living Example Problems "that provide more than 80 interactive simulations" in "Wolfram, Python, POLYMATH, and MATLAB" — ideal for your Python strength.
- Separations: Seader, Henley & Roper, *Separation Process Principles* (Wiley) or Geankoplis, *Transport Processes and Separation Process Principles*.
- Seborg, Edgar, Mellichamp & Doyle, *Process Dynamics and Control*, **4th ed. (2016, Wiley)** — process control (complements Nise from 1H).
- Turton et al., *Analysis, Synthesis, and Design of Chemical Processes*, current ed. (Pearson) — plant design, flowsheeting, economics.

### [GRAD] Graduate reach
- **Advanced transport phenomena:** Deen, *Analysis of Transport Phenomena*.
- **Molecular/statistical thermodynamics:** your physics stat-mech is the prerequisite; e.g., Sandler, *Chemical, Biochemical, and Engineering Thermodynamics*.
- **Advanced reactor design:** Froment, Bischoff & De Wilde, *Chemical Reactor Analysis and Design*.
- **Process systems engineering:** Biegler, Grossmann & Westerberg, *Systematic Methods of Chemical Process Design*.

### Physics scaffolding
Transport phenomena is the crown jewel for a physicist: momentum, heat, and mass transport are the *same* conservation/continuity structure (the "BSL analogy"), and the shell-balance derivations are exactly the control-volume conservation arguments you know. Chemical-engineering thermo extends your stat-mech/thermo to multicomponent phase and reaction equilibria (fugacity, activity, chemical potential — you know μ already). Reaction engineering is coupled ODEs/PDEs (mole balances) — your numerical-methods strength applies directly.

### Exercises / computational
- Felder material/energy-balance flowsheets; Fogler reactor-design problems; McCabe–Thiele distillation.
- **Python:** use **Cantera** (⭐ free) for chemical equilibrium and reactor networks; script a CSTR/PFR ODE solver in SciPy and reproduce Fogler examples; a flash-distillation VLE calculation using an activity model.

### Time estimate
4–5 months undergrad; +2–4 months per [GRAD] thread.

> **MVP:** Material/energy balances (Felder) + reaction engineering (Fogler CSTR/PFR) + one separation (distillation); reuse trunk transport/thermo. ~7 weeks.

---

# LAYER 3 — SPECIALIZATION ADDENDUMS (CONVERSATIONAL ONLY)

**These are explicitly NOT full curricula.** Each gives: (a) which core(s) it branches from, (b) a one-paragraph orientation, (c) 2–4 accessible entry readings for conversational depth, and (d) the canonical textbooks to go deeper *if you later choose*. Goal: conversational competence plus knowing exactly where to start.

---

## 3-AEROSPACE

- **Branches from:** Mechanical (fluids, thermo, dynamics, control) + some Electrical (avionics/GNC).
- **Orientation:** Aerospace applies fluid mechanics, thermodynamics, structures, and control to flight vehicles and spacecraft. It adds compressible/high-speed aerodynamics (shocks, supersonic/hypersonic flow), flight mechanics and stability, propulsion (air-breathing and rocket), and orbital mechanics (the two-body problem, orbital maneuvers, and rendezvous). For you, most of the physics is familiar — it is Newtonian mechanics and fluid dynamics in a specialized context.
- **Entry readings (conversational):** Anderson, *Introduction to Flight*, **8th ed. (2016, McGraw-Hill)** — broad, historical, accessible; selected chapters of Anderson, *Fundamentals of Aerodynamics*, **6th ed. (McGraw-Hill)**. ⭐ LibreTexts *Introduction to Aerospace Structures and Materials* (Alderliesten, open).
- **Go-deeper canonical texts:** Anderson, *Fundamentals of Aerodynamics* (6th) — full; Sutton & Biblarz, *Rocket Propulsion Elements*, **9th ed. (2017, Wiley)**; Curtis, *Orbital Mechanics for Engineering Students*, **4th ed. (2019/2020, Elsevier)** — the practical current edition (a 5th ed., ISBN 978-0443290152, is scheduled for release Oct 19, 2026 with new end-of-chapter problems and downloadable MATLAB algorithms; verify availability before buying).

---

## 3-BIOMEDICAL

- **Branches from:** Electrical (bioinstrumentation, imaging, signals) and Mechanical (biomechanics); some Chemical (biotransport/biomaterials).
- **Orientation:** Biomedical engineering applies engineering methods to biology and medicine: biomechanics (tissue and fluid mechanics of the body), bioinstrumentation and biosignals (ECG/EEG as signals-and-systems problems), medical imaging (MRI/CT/ultrasound — signals, systems, and inverse problems), and biomaterials. Your signals/systems and imaging math (Fourier, sampling, reconstruction) transfer directly; the new content is physiology and the biological constitutive behavior.
- **Entry readings (conversational):** Enderle & Bronzino, *Introduction to Biomedical Engineering*, **3rd ed. (2012, Academic Press)** — the standard broad survey (3rd is the latest edition); for imaging, selected chapters of Prince & Links.
- **Go-deeper canonical texts:** Fung, *Biomechanics: Mechanical Properties of Living Tissues*, **2nd ed. (1993, Springer)** — the definitive tissue-mechanics text (2nd is genuinely the final edition, not an oversight); Prince & Links, *Medical Imaging Signals and Systems*, **2nd ed. (2014, Pearson)**.

---

## 3-MATERIALS

- **Branches from:** the Materials Science trunk (1G) + Chemical (thermodynamics/kinetics) and Mechanical (mechanical behavior).
- **Orientation:** Materials engineering deepens the structure–processing–properties–performance paradigm from Layer 1: the thermodynamics and kinetics of phase transformations, mechanical behavior and failure, and the tailoring of metals, ceramics, polymers, semiconductors, and composites. Your solid-state physics and stat-mech make the thermodynamics/kinetics accessible.
- **Entry readings (conversational):** Callister & Rethwisch (10th, 2018) — the trunk text is itself the conversational entry; Ashby & Jones, *Engineering Materials 1 & 2* (accessible, mechanism-focused).
- **Go-deeper canonical texts:** Porter, Easterling & Sherif, *Phase Transformations in Metals and Alloys*, **4th ed. (2022, CRC Press)** (graduate; supersedes the long-standing 3rd/2009 edition); Ashby, *Materials Selection in Mechanical Design* (for design-driven selection).

---

## 3-INDUSTRIAL

- **Branches from:** your existing math/statistics/optimization plus all four cores (industrial engineering optimizes systems and processes).
- **Orientation:** Industrial engineering optimizes systems of people, materials, and information: operations research (linear/integer programming, networks, queueing, stochastic models), statistical quality control and design of experiments, and production/operations. For an ML engineer this is the most immediately familiar branch — LP/IP, simulation, and stochastic modeling overlap heavily with optimization and applied statistics you already use; the framing (SPC, DOE, supply chains) is the new part.
- **Entry readings (conversational):** Hillier & Lieberman, *Introduction to Operations Research*, **11th ed. (2021, McGraw-Hill)** — selected chapters (LP, networks, queueing); Montgomery, *Introduction to Statistical Quality Control*, **8th ed. (2020, Wiley)** — control charts and capability.
- **Go-deeper canonical texts:** Winston, *Operations Research: Applications and Algorithms*, **4th ed. (2004, Cengage)** (still the latest edition — no newer one exists); Montgomery, *Design and Analysis of Experiments* (current Wiley ed.). ⭐ Free tooling: Python `PuLP`/`scipy.optimize`/`OR-Tools` for LP/IP; `SimPy` for discrete-event simulation.

---

# CONSOLIDATED MVP FAST-PATH (WHOLE PROGRAM)

For a time-limited scenario, this compressed route yields working conversational-to-applied competence:

1. **Layer 0:** 2-hour diagnostic; patch only chemistry (if Chemical) and engineering numerics. (≈ few days)
2. **Layer 1 trunk MVP:** the eight per-phase MVP boxes only — roughly 16–18 weeks total, and much less if you exploit the physics fast-tracks (circuits, signals, thermo, materials are heavily compressible for you).
3. **Pick ONE core** and do its MVP box (~6–7 weeks).
4. **Skim all four Layer-3 addendums'** entry readings for conversational breadth (~1 week).

**Total MVP:** ≈ 6–9 months part-time for trunk + one core + addendum breadth.

**Recommended first core if undecided:** Given your ML/fraud-analytics day job and physics background, **Electrical** (fastest theory ramp via your E&M + oscillator intuition, plus DSP/information-theory synergy with ML) or **Chemical** (transport phenomena is the single most physics-native engineering subject and rewards your stat-mech) are the highest-leverage starting cores. Mechanical is the best choice if you want the broadest hands-on simulation portfolio (FEA/CFD).

---

# CALIBRATED-UNCERTAINTY SUMMARY

- **SETTLED (the vast majority):** all Layer 0 math/physics; all Layer 1 engineering sciences; the *mechanics/physics* underlying every Layer 2 core; core reaction engineering, transport, thermodynamics, circuits, signals, and control theory. These are mature, non-controversial, and stable across editions.
- **CONTESTED (region/practice-dependent — flag before applying):**
  - **Design codes.** Civil/structural and geotechnical *design* differs by jurisdiction: US texts teach AISC/ACI (LRFD); in Germany/Europe you must use the **Eurocodes (EC2/EC3/EC7/EC8) with German National Annexes**. Mechanical machine design (Shigley) and pressure-vessel/piping work similarly diverge (ASME vs. EN/DIN). Learn mechanics from the canonical texts, apply your regional code.
  - **"Best practice" in process/plant design and control tuning** genuinely varies by company and context.
- **HYPE (claims outrunning evidence — stay skeptical):**
  - **Additive-manufacturing** property/performance claims in vendor literature.
  - **Simulation-tool marketing** (CFD/FEA "push-button accuracy"): results are only as good as meshing, turbulence-model choice, and validation — treat unvalidated simulation output cautiously.
  - Any "AI-will-replace-first-principles-engineering" framing — the canonical models remain the ground truth against which data-driven methods are validated.

---

# RECOMMENDATIONS (staged, with decision thresholds)

**Stage 1 — Placement (Week 0).** Run the Layer 0 diagnostic. *Threshold to skip Layer 0 entirely:* you can, unaided, set up and solve a multivariable optimization, an eigenvalue problem, a second-order ODE with forcing, and a chemical-equilibrium stoichiometry problem. If any fails, patch just that item.

**Stage 2 — Build the trunk (Months 1–5).** Do all eight Layer-1 phases, exploiting the physics fast-tracks. *Benchmark to advance to a core:* you can hand-solve a truss, a control-volume momentum balance, a Rankine cycle, a 1-D transient-conduction problem, an RLC transient, a convolution/Fourier problem, a lever-rule phase-diagram problem, and a Bode-margin stability check — and you have working Python code for at least the truss solver, a SPICE simulation, and a finite-difference PDE.

**Stage 3 — Choose and complete ONE core (Months 6–10).** Pick based on interest/leverage (see "Recommended first core" above). *Threshold to declare undergrad competence:* you can complete representative end-of-chapter problems from each of the core's primary texts without solutions, and you have one non-trivial computational artifact (e.g., a frame stiffness solver, an ngspice amplifier design, a Cantera reactor model).

**Stage 4 — Breadth via addendums (ongoing, ~1 week).** Read the four addendum entry readings for conversational fluency. *This is the stopping point for "conversational + know where to start."*

**Stage 5 — Optional expansion.** Add further cores (each ~3–5 months, cheaper because the trunk is shared) or opt into [GRAD] threads aligned to your interests — e.g., FEA/CFD (Mechanical), information/communication theory (Electrical, high ML synergy), process systems engineering (Chemical), or structural dynamics (Civil). *Trigger to go graduate in an area:* you find yourself repeatedly hitting the ceiling of the undergrad text on a topic you care about.

**Cross-cutting recommendation — exploit your two superpowers.** (1) *Physics transfer:* deliberately map each new engineering concept onto the physics you know before reading the derivation; this is your single biggest time-saver. (2) *Python-first problem solving:* for every phase, build one small computational artifact — this cements understanding, plays to your strength, and produces a portfolio demonstrating the competence. Use only the ⭐ free tools (NumPy/SciPy, ngspice, FEniCS/OpenFOAM, Cantera, CoolProp, python-control, PuLP/OR-Tools, SimPy) so cost is never a blocker.

---

# CAVEATS

- **Editions verified September 2026; they drift.** Where a newer edition is imminent (Curtis *Orbital Mechanics* 5th ed., scheduled Oct 19, 2026), the current shipping edition is recommended and the pending one flagged. Re-check before purchase.
- **A few "latest editions" are genuinely old, not errors:** Fung *Biomechanics* stops at the 2nd ed. (1993); Winston *Operations Research* stops at the 4th ed. (2004); Enderle & Bronzino at the 3rd (2012). These remain the canonical texts despite their age.
- **Free ≠ authorized for every book.** The three open *platforms* cited (NPTEL at nptel.ac.in, MIT OpenCourseWare, LibreTexts Engineering) and the named open textbooks (Baker–Haynes Statics, Bar-Meir Fluids, Yan Thermodynamics, LibreTexts aerospace/materials titles, McGuire matrix-structural-analysis PDF) are legitimately free. The commercial canonical texts do **not** have authorized free publisher versions; obtain them through legitimate purchase, rental, or library access.
- **This is a self-study *knowledge* curriculum, not a licensure path.** It builds engineering understanding and applied/computational competence, not professional certification (PE/Chartered Engineer/EUR ING), which requires accredited coursework, supervised experience, and exams.
- **Code-dependent design content is region-specific.** Treat all US-code design procedures (AISC/ACI/ASME) as illustrative of method; for actual practice in Germany/Europe, the Eurocodes with National Annexes govern, and the numeric safety factors and detailing rules differ even though the underlying mechanics is identical.
- **Time estimates assume a mathematically mature, self-directed adult** exploiting the flagged fast-tracks. They will lengthen for topics with heavy new empirical content (soil mechanics, machine design, separations) and shorten for the physics-native blocks (circuits, signals, thermo, transport, materials).