# A Multi-Year Graduate Self-Study Curriculum in Human- and Application-Facing Computer Science

*Balanced read + build · all four sub-areas (HCI · visual computing · visualization · software engineering) · graduate / qualifying-exam depth · resources current as of early 2026 (editions not live-verified this pass — see Caveats)*

## TL;DR
- A **13-phase, ~3.5–4.5 year** curriculum (compressible to ~18–22 months via the MVP fast-path) spanning human–computer interaction, the full visual-computing stack (real-time **and** physically-based graphics, geometry/animation, computational photography), data & scientific visualization, and software engineering as an empirical discipline — canonical texts + seminal papers, with a concrete build artifact in every phase.
- Unlike theory and systems, this cluster is **four semi-independent tracks** over a shared foundation. After a perception base (Phase 1) and a signal/image base (Phase 5), the HCI, visual-computing, visualization, and software-engineering tracks can be pursued **in parallel or in any order** — the dependency map makes the few real prerequisites explicit.
- This is the cluster where **your physics is a superpower**: physically-based rendering *is* radiative transfer plus Monte Carlo integration; image processing is Fourier analysis and the sampling theorem; physically-based animation is PDEs and numerical integration; volume rendering is an emission–absorption radiative-transfer integral; and even Fitts's law was framed by Fitts as Shannon channel capacity. Bridges are marked ⚛ throughout.
- **Calibration matters most in software engineering**, which is notoriously weak on evidence — much "best practice" is convention, not data. I foreground what's actually empirically supported (the DORA/*Accelerate* findings, code-review efficacy) versus what isn't (TDD-always, the "10x engineer", specific Agile prescriptions), and flag the contested spots in HCI (Nielsen's "5 users") and visualization (Tufte's chartjunk dogma).
- **Overlap handled:** formal-methods foundations stay in your theory curriculum (SWE points there for applied verification); CS-graphics stays distinct from your Filmmaking/Colour-theory tracks; and real-time graphics **builds on** the GPU/CUDA phase from your systems curriculum rather than re-teaching the hardware.

---

## Key orientation

**Four tracks, one foundation.** HCI, graphics, visualization, and software engineering are genuinely different disciplines with different literatures, methods, and venues. Rather than forcing a single linear path, this curriculum establishes two shared foundations — human perception (which underlies both HCI and visualization) and signal/image processing (which underlies both graphics and computational photography) — and then lets the four tracks run independently. Pick the order that matches your appetite; the dependency map shows the (few) hard prerequisites.

**Read + build, per track's idiom.** "Balanced" means something different in each track: in graphics you learn by **writing a renderer** (a path tracer, then a real-time pipeline); in HCI you learn by **running a real usability study** with proper experimental design; in visualization by **building interactive views** (D3 + scientific viz); in software engineering by **refactoring, architecting, and doing empirical mini-studies**. Tooling follows the idiom — Python/NumPy for imaging, viz prototyping, and HCI stats; C++/Rust + a GPU API for graphics; web/D3/JS for interactive visualization.

**Physics scaffolding (⚛).** Called out per phase, but the headline bridges: the **rendering equation** (Fredholm integral equation of the second kind) and **Monte Carlo path tracing** (importance sampling, Russian roulette — your stat-mech/QFT toolkit); light transport ↔ **radiative/neutron transport** (Chandrasekhar); **image processing** ↔ Fourier, convolution, the Nyquist–Shannon sampling theorem; **physically-based animation** ↔ Navier–Stokes, elasticity/FEM, symplectic integrators; **volume rendering** ↔ the emission–absorption radiative-transfer integral; **visual-encoding effectiveness** ↔ psychophysics (Weber–Fechner, Stevens' power law); **Fitts's law** and **Hick–Hyman law** ↔ Shannon information.

**Free-resource density.** Several spine texts are legitimately free online — *Physically Based Rendering* (pbr-book.org), Szeliski's *Computer Vision*, Wilke's *Fundamentals of Data Visualization*, the Google *SRE* books — plus the Ray Tracing in One Weekend series, tinyrenderer, LearnOpenGL, CMU 15-463, WCAG, and the Nielsen Norman Group articles. Each is flagged **[FREE]**; in-copyright books are **[BUY]**, and pirated PDFs aren't endorsed.

---

## The Phased Curriculum

**Legend.** Per phase: (a) Goal · (b) Prerequisites · (c) Primary (canonical texts + seminal papers) · (d) Supplementary · (e) Exercises + **Build** · (f) Time · (g) MVP. Status tags: **[SETTLED]**, **[CONTESTED]**, **[HYPE-WATCH]**, **[EVOLVING]**. Physics bridges: ⚛.

---

### PHASE 1 — Human Perception & Psychophysics (shared foundation: HCI + visualization)
**(a) Goal.** The perceptual and cognitive machinery that HCI and visualization both exploit: visual perception, pre-attentive processing, the Gestalt principles, colour perception, attention and memory, and how to *measure* perception quantitatively.

**(b) Prerequisites.** None internal. Feeds Phases 2 (HCI) and 10 (visualization).

**(c) Primary.**
- Colin Ware, *Information Visualization: Perception for Design*, 4th ed. (Morgan Kaufmann, 2021) **[BUY]** — the best perception-for-design text; used again in Phase 10.
- Stephen Palmer, *Vision Science: Photons to Phenomenology* (MIT Press, 1999) **[BUY]** — for rigorous depth (optional but excellent for a physicist).
- Seminal: the **Weber–Fechner law**; **Stevens, "On the Psychophysical Law" (1957)** — the power law of perceived magnitude; the **Gestalt grouping principles**.

**(d) Supplementary.** Goldstein, *Sensation and Perception* (a standard textbook) for breadth.

**(e) Exercises + Build.** **Build (Python/PsychoPy):** run a small **psychophysics experiment** — measure a just-noticeable-difference (a discrimination threshold) or a Stevens power-law exponent for a perceptual dimension, with proper staircase methods and analysis. This doubles as your first taste of the experimental rigor Phase 3 formalizes.

**(f) Time.** 4–6 weeks.

**(g) MVP.** Ware's chapters on low-level vision, pre-attentive processing, and colour + the JND experiment.

⚛ *Bridge:* psychophysics is **quantitative perception** — the Weber–Fechner (logarithmic) and Stevens (power-law) laws are measurement/scaling relations of exactly the kind you write in physics, relating a physical stimulus to a perceived magnitude. **[SETTLED]** (as empirical laws with known domains of validity).

---

### PHASE 2 — HCI I: Cognitive Foundations & Interaction Design
**(a) Goal.** The core theory of interaction: affordances/signifiers, mental models, the gulfs of execution and evaluation, user-centered and goal-directed design, and quantitative human-performance models (Fitts, Hick–Hyman, GOMS/KLM).

**(b) Prerequisites.** Phase 1.

**(c) Primary.**
- Don Norman, *The Design of Everyday Things*, revised & expanded ed. (Basic Books, 2013) **[BUY]** — the foundational design text; affordances, signifiers, the two gulfs.
- Card, Moran & Newell, *The Psychology of Human-Computer Interaction* (Erlbaum, 1983) **[BUY]** — the founding cognitive-modeling work (Model Human Processor, GOMS).
- Rogers, Sharp & Preece, *Interaction Design: Beyond Human-Computer Interaction* (5th ed., ~2019 — **verify edition**) **[BUY]** — the standard HCI textbook.
- Seminal: **Fitts, "The Information Capacity of the Human Motor System in Controlling the Amplitude of Movement" (1954)**; **Hick (1952)** and **Hyman (1953)**; **Engelbart, "Augmenting Human Intellect" (1962)**.

**(d) Supplementary.** Cooper et al., *About Face: The Essentials of Interaction Design*, 4th ed. (Wiley, 2014) **[BUY]** for goal-directed design and personas; Nielsen Norman Group articles **[FREE]**.

**(e) Exercises + Build.** **Build:** design and prototype a non-trivial interface (Figma or code) applying Norman's principles end-to-end; then do a **GOMS/KLM analysis** to predict expert task times and a Fitts's-law analysis of a pointing task.

**(f) Time.** 6–8 weeks.

**(g) MVP.** Norman (all) + the Fitts/Hick material + one prototype with a KLM analysis.

⚛ *Bridge (the standout):* **Fitts framed his law using Shannon's information theory** — the "index of difficulty" ID = log₂(2D/W) is a channel-capacity expression, and movement time is linear in ID, i.e., the motor system has a roughly constant *information rate*. The **Hick–Hyman law** says choice reaction time is proportional to the *information* (log of the number of alternatives) in the decision. Information theory, reappearing in human performance. **[SETTLED]** (robust empirical laws).

---

### PHASE 3 — HCI II: Usability Evaluation & Empirical Methods
**(a) Goal.** How HCI knows what it knows: usability inspection (heuristic evaluation, cognitive walkthrough), user studies (think-aloud, controlled experiments), survey and qualitative methods, and — crucially — the **experimental design and statistics** behind CHI-quality empirical work.

**(b) Prerequisites.** Phase 2.

**(c) Primary.**
- Lazar, Feng & Hochheiser, *Research Methods in Human-Computer Interaction*, 2nd ed. (Morgan Kaufmann, 2017) **[BUY]** — the methods-and-statistics bible for HCI research.
- Nielsen, *Usability Engineering* (Morgan Kaufmann, 1993) **[BUY]** — heuristics and discount usability.
- Seminal: **Nielsen & Molich, "Heuristic Evaluation of User Interfaces" (CHI 1990)**; the **think-aloud protocol** (Ericsson & Simon, *Protocol Analysis*).

**(d) Supplementary.** Sauro & Lewis, *Quantifying the User Experience*, 2nd ed. (Morgan Kaufmann, 2016) **[BUY]** — the statistics of UX metrics, pitched practically.

**(e) Exercises + Build.** **Build:** run a **real controlled usability experiment** on your Phase-2 prototype — a within- or between-subjects design with a clear hypothesis, proper randomization/counterbalancing, and correct inferential statistics (your physics stats training is a direct asset). Separately, conduct a heuristic evaluation and reconcile what each method found.

**(f) Time.** 7–9 weeks.

**(g) MVP.** Lazar et al. chapters on experimental design + statistics + one properly-run experiment.

⚛ *Bridge:* this is **experimental science** — the hypothesis testing, effect sizes, power analysis, and confound control you know from physics apply unchanged; HCI's replication and measurement debates mirror the ones you know from empirical science.

**[CONTESTED] "Five users find ~85% of usability problems."** Nielsen & Landauer's widely-cited claim rests on a specific problem-detection-probability model (p ≈ 0.31); when problems are rarer or the interface is complex, five is far too few (see Woolrych & Cockton's critique). Treat the "magic number 5" as a rule of thumb with real boundary conditions, not a law.

---

### PHASE 4 — HCI III: Accessibility, CSCW & Ubiquitous Computing
**(a) Goal.** Designing beyond the single able-bodied user at a desktop: web/app **accessibility** (WCAG, assistive tech, inclusive design), **computer-supported cooperative work** (the challenges of distance, awareness, coordination), and **ubiquitous/embodied** interaction.

**(b) Prerequisites.** Phase 2 (design foundations).

**(c) Primary.**
- **W3C WCAG 2.2** (and the WAI materials) **[FREE]** — the normative accessibility spec.
- Seminal: **Weiser, "The Computer for the 21st Century" (1991)** **[FREE]** — the founding ubicomp vision; **Olson & Olson, "Distance Matters" (2000)** — why co-located collaboration is hard to replicate remotely; **Grudin's CSCW survey work**; **Ackerman, "The Intellectual Challenge of CSCW" (2000)**.

**(d) Supplementary.** Horton & Quesenbery, *A Web for Everyone* (Rosenfeld, 2013) **[BUY]**; Paul Dourish, *Where the Action Is: The Foundations of Embodied Interaction* (MIT Press, 2001) **[BUY]** — phenomenology of interaction (a bridge to your logic/philosophy track — it draws on Heidegger and Merleau-Ponty).

**(e) Exercises + Build.** **Build:** a full **accessibility audit** of a real site/app — screen-reader walkthrough, keyboard-only navigation, WCAG 2.2 conformance check, and a remediation plan; plus a small collaborative/groupware feature reasoning explicitly about awareness and coordination.

**(f) Time.** 5–7 weeks.

**(g) MVP.** WCAG 2.2 essentials + the accessibility audit + Weiser 1991 + Olson & Olson 2000.

⚛ *Bridge (light):* CSCW's coordination problems — shared state, awareness, latency — rhyme with the **distributed-systems** consistency challenges from your systems curriculum; "distance matters" is, loosely, the human-scale cost of the same partition/latency trade-offs.

---

### PHASE 5 — Signal & Image Foundations (shared foundation: graphics + computational photography)
**(a) Goal.** Images as 2D signals: sampling and aliasing, convolution and linear filtering, the **frequency domain** (2D Fourier), image pyramids, restoration, and feature/edge detection. This is the mathematical bedrock for both graphics (antialiasing, texture filtering) and computational photography.

**(b) Prerequisites.** None internal (your Fourier/linear-systems background covers the math). Feeds Phases 6, 7, 9.

**(c) Primary.**
- Gonzalez & Woods, *Digital Image Processing*, 4th ed. (Pearson, 2018) **[BUY]** — the standard image-processing text.
- Szeliski, *Computer Vision: Algorithms and Applications*, 2nd ed. (Springer, 2022) **[FREE online]** (szeliski.org/Book) — use the **classical imaging chapters** (image formation, filtering, features); treat the recognition/learning chapters as pointers, per your AI/ML deferral.
- Seminal: the **Nyquist–Shannon sampling theorem** (Shannon 1949); the **FFT** (Cooley & Tukey 1965); the **Canny edge detector** (1986).

**(d) Supplementary.** Oppenheim & Willsky, *Signals and Systems* (as a signal-processing reference, if needed).

**(e) Exercises + Build.** **Build (Python/NumPy):** implement from scratch — spatial convolution and separable filters, a **2D FFT-based frequency-domain filter** (low/high-pass, and demonstrate aliasing then fix it with proper prefiltering), Gaussian/Laplacian **image pyramids**, and Canny edge detection. Validate against the convolution theorem.

**(f) Time.** 6–8 weeks.

**(g) MVP.** Gonzalez & Woods chapters on filtering + the frequency domain + sampling + the convolution/FFT/pyramid builds.

⚛ *Bridge:* **your home turf.** Images are 2D signals; filtering is convolution; the **convolution theorem** and **Fourier analysis** are exactly as you know them; aliasing is a violation of the **Nyquist criterion**. Nothing here is new math — it's your signal-processing toolkit in two dimensions. **[SETTLED]**

---

### PHASE 6 — Computer Graphics I: Real-Time Rendering & the GPU Pipeline
**(a) Goal.** The rasterization pipeline end-to-end: transforms and projective geometry, the vertex/fragment shader model, texturing and antialiasing, shadow mapping, deferred shading, and real-time approximations of physically-based shading and global illumination. Build a real-time renderer.

**(b) Prerequisites.** Phase 5 (sampling/antialiasing); linear algebra. Builds on the **GPU architecture/CUDA phase from your systems curriculum** (you already understand the hardware — here you drive its graphics pipeline).

**(c) Primary.**
- Marschner & Shirley, *Fundamentals of Computer Graphics*, 5th ed. (CRC Press, 2021) **[BUY]** — the standard intro (transforms, rasterization, shading); shared with Phase 7.
- Akenine-Möller, Haines, Hoffman, et al., *Real-Time Rendering*, 4th ed. (CRC Press, 2018) **[BUY]** — the real-time bible.
- **LearnOpenGL** (Joey de Vries) **[FREE]** (learnopengl.com) — the build spine.
- Seminal: **Catmull (Z-buffer, 1974)**; **Gouraud (1971)** and **Phong (1975)** shading; the programmable-shader lineage.

**(d) Supplementary.** **WebGPU Fundamentals** **[FREE]** (webgpufundamentals.org) for the modern API; Hughes, van Dam et al., *Computer Graphics: Principles and Practice*, 3rd ed. (2013) **[BUY]** for encyclopedic depth.

**(e) Exercises + Build.** **Build:** a **real-time renderer in C++/OpenGL** (or **Rust + wgpu**) following LearnOpenGL — through lighting, texturing, shadow mapping, and a **deferred, PBR-shaded** pipeline with HDR and tone mapping. This is where your C++/Rust and GPU knowledge converge.

**(f) Time.** 9–12 weeks.

**(g) MVP.** Marschner & Shirley transforms/rasterization/shading + LearnOpenGL through lighting and shadow mapping.

⚛ *Bridge:* the transform stack is **projective geometry / linear algebra** (homogeneous coordinates); real-time shading models are cheap approximations of the BRDFs you'll treat rigorously in Phase 7.

**[EVOLVING]** The real-time/offline boundary is dissolving as **hardware ray tracing** (RTX-class GPUs) brings path-traced effects into real time — a moving target as of 2026; treat "real-time can't do GI" as outdated.

---

### PHASE 7 — Computer Graphics II: Physically-Based / Offline Rendering (the physics-heavy path)
**(a) Goal.** Light transport from first principles: **radiometry** (radiance, irradiance, BRDFs, the measurement equation), the **rendering equation**, and **Monte Carlo path tracing** with importance sampling, multiple importance sampling, and bidirectional methods. Build a physically-based renderer.

**(b) Prerequisites.** Phase 5; Phase 6 helps but isn't required. Your Monte Carlo / radiative-transfer background is the real prerequisite.

**(c) Primary.**
- Pharr, Jakob & Humphreys, *Physically Based Rendering: From Theory to Implementation*, **4th ed. (2023)** **[FREE online]** (pbr-book.org) — the offline-rendering bible, a complete literate-programming physically-based renderer. This is the spine.
- Peter Shirley, *Ray Tracing in One Weekend* / *…The Next Week* / *…The Rest of Your Life* **[FREE]** (raytracing.github.io) — the gentle build on-ramp before pbrt.
- Seminal: **Kajiya, "The Rendering Equation" (SIGGRAPH 1986)** — read the original; **Whitted, "An Improved Illumination Model for Shaded Display" (1980)**; **Cook & Torrance (1982)** microfacet BRDF; **Veach, "Robust Monte Carlo Methods for Light Transport Simulation" (PhD thesis, 1997)** — MIS and bidirectional path tracing.

**(d) Supplementary.** *Ray Tracing Gems* I & II (Nvidia, **[FREE]**) for modern GPU ray tracing.

**(e) Exercises + Build.** **Build:** the **Ray Tracing in One Weekend** trilogy → then implement/extend a **physically-based path tracer** (following pbrt's structure), with a microfacet BRDF, importance sampling, **multiple importance sampling**, and Russian roulette; validate with **furnace/white-furnace tests** and against analytic solutions.

**(f) Time.** 10–14 weeks (the deepest graphics phase).

**(g) MVP.** Ray Tracing in One Weekend (all three) + pbrt chapters on radiometry, the rendering equation, and Monte Carlo integration + Kajiya 1986.

⚛ *Bridge (the headline of this whole curriculum):* the **rendering equation is a Fredholm integral equation of the second kind**; radiometry (radiance/irradiance/BRDF/the measurement equation) **is radiative-transfer physics**; **path tracing is Monte Carlo integration** with importance sampling and Russian roulette — the exact estimator machinery you know from statistical mechanics and lattice/QFT computations. **Veach's path-integral formulation** of light transport is a direct **Feynman-path-integral analog** (integrate contributions over all light paths). Light transport ↔ **neutron transport / Chandrasekhar's radiative transfer**. You will find this phase almost eerily familiar. **[SETTLED]**

---

### PHASE 8 — Geometry Processing & Physically-Based Animation/Simulation
**(a) Goal.** Discrete geometry (meshes, the cotangent Laplacian, subdivision, parameterization, smoothing) and physically-based animation (mass-spring systems, rigid bodies, cloth, fluids) with proper numerical integration.

**(b) Prerequisites.** Phase 6 or 7 (geometry/rendering basics); your PDE/numerical-methods background.

**(c) Primary.**
- Botsch, Kobbelt, Pauly, Alliez & Lévy, *Polygon Mesh Processing* (CRC Press, 2010) **[BUY]** — the geometry-processing standard.
- **Baraff & Witkin, "Physically Based Modeling" SIGGRAPH course notes** **[FREE]** — the classic simulation primer; Bridson, *Fluid Simulation for Computer Graphics*, 2nd ed. (2015) **[BUY]**.
- Seminal: **Catmull–Clark** and **Loop subdivision**; the **cotangent Laplacian** (Pinkall & Polthier 1993); **Baraff & Witkin, "Large Steps in Cloth Simulation" (SIGGRAPH 1998)** — implicit integration; **Stam, "Stable Fluids" (SIGGRAPH 1999)**.

**(d) Supplementary.** **libigl tutorials** **[FREE]** for geometry-processing builds; the SIGGRAPH course "Discrete Differential Geometry" (Crane) **[FREE]**.

**(e) Exercises + Build.** **Build:** a **mass-spring cloth simulator with implicit (backward-Euler) integration** (Baraff–Witkin); a **"Stable Fluids" solver** (Stam) in Python or C++; and a mesh-processing task (Laplacian smoothing or parameterization) with libigl.

**(f) Time.** 8–11 weeks.

**(g) MVP.** Baraff–Witkin notes + the cloth simulator + the Stable Fluids solver.

⚛ *Bridge:* **your turf again.** Cloth/soft bodies are **mass-spring/elasticity** systems; fluids are the **Navier–Stokes equations** (Stable Fluids is an operator-splitting scheme with a projection step enforcing incompressibility — a discrete Helmholtz decomposition); implicit vs explicit and **symplectic integrators** are the numerical-stability trade-offs you know; the **discrete Laplacian** is the discretized ∇². **[SETTLED]**

---

### PHASE 9 — Computational Photography
**(a) Goal.** Turning captured light into images computationally: HDR imaging and tone mapping, edge-preserving (bilateral) filtering, panorama stitching, light fields and the plenoptic camera, and the computational-camera pipeline.

**(b) Prerequisites.** Phase 5 (signal/image foundations).

**(c) Primary.**
- **CMU 15-463 "Computational Photography"** course materials (lecture notes + assignments) **[FREE]**.
- Szeliski (relevant chapters, **[FREE]**) as the reference.
- Seminal: **Debevec & Malik, "Recovering High Dynamic Range Radiance Maps from Photographs" (SIGGRAPH 1997)**; **Levoy & Hanrahan, "Light Field Rendering" (SIGGRAPH 1996)**; **Durand & Dorsey, "Fast Bilateral Filtering for the Display of High-Dynamic-Range Images" (SIGGRAPH 2002)**; **Brown & Lowe, panorama stitching / AutoStitch (2007)**.

**(d) Supplementary.** Raskar & Tumblin, *Computational Photography* (draft/notes).

**(e) Exercises + Build.** **Build (Python):** **HDR merge + tone mapping** from a bracketed exposure stack (recover the camera response, then tone-map); **panorama stitching** (feature detection → homography → blending); a **bilateral filter**; and explore a **light-field dataset** (refocusing). Classical methods are the spine; note where learned methods now dominate.

**(f) Time.** 7–9 weeks.

**(g) MVP.** CMU 15-463 core lectures + the HDR-and-tone-mapping and panorama builds + Debevec & Malik 1997.

⚛ *Bridge:* **HDR recovery is radiometric camera-response estimation** (the physics of light measurement and sensor response); a **light field is the plenoptic function** — a physical description of radiance along all rays through a volume; the camera is an **optical sampling system**. Touches your photography/filmmaking interest on the imaging side. **[SETTLED for the classical methods; ML methods EVOLVING.]**

---

### PHASE 10 — Data & Scientific Visualization
**(a) Goal.** The theory and practice of turning data into effective pictures: the perception-grounded theory of **visual encoding**, information visualization (Munzner's what–why–how), scientific visualization (volume/flow/field rendering), visual analytics, and interaction techniques for exploratory analysis.

**(b) Prerequisites.** Phase 1 (perception); Phase 6/7 helps for the scientific-viz rendering.

**(c) Primary.**
- Tamara Munzner, *Visualization Analysis and Design* (CRC Press, 2014) **[BUY]** — the canonical modern viz textbook.
- Colin Ware, *Information Visualization: Perception for Design*, 4th ed. (2021) **[BUY]** — perceptual foundations (from Phase 1).
- Claus Wilke, *Fundamentals of Data Visualization* (O'Reilly, 2019) **[FREE online]** (clauswilke.com).
- Seminal: **Bertin, *Semiology of Graphics* (1967/1983)**; **Cleveland & McGill, "Graphical Perception: Theory, Experimentation, and Application to the Development of Graphical Methods" (1984)** — the empirical ranking of visual encodings; **Mackinlay, "Automating the Design of Graphical Presentations" (APT, 1986)**; **Shneiderman, "The Eyes Have It: A Task by Data Type Taxonomy for Information Visualizations" (1996)**.

**(d) Supplementary.** Edward Tufte, *The Visual Display of Quantitative Information*, 2nd ed. (2001) **[BUY]** — read critically (see below); Telea, *Data Visualization: Principles and Practice* for scientific viz; the D3 documentation and Observable **[FREE]**.

**(e) Exercises + Build.** **Build:** several **D3.js visualizations** (data → interactive, coordinated views); one **scientific-visualization project** — volume rendering or vector/flow-field visualization of a **physics dataset** you understand; and a reproduction of a **Cleveland–McGill-style perception experiment** ranking encoding effectiveness.

**(f) Time.** 9–12 weeks.

**(g) MVP.** Munzner (the framework chapters) + Cleveland & McGill 1984 + Shneiderman 1996 + the D3 builds.

⚛ *Bridge:* the **effectiveness ranking of visual encodings** (position > length > angle > area > colour for quantitative decoding) is **grounded in psychophysics** — it's Stevens' power law applied to graphical perception. And **volume rendering is an emission–absorption radiative-transfer integral** — the same physics as Phase 7's light transport, now integrating along viewing rays through a scalar field (you'll recognize the optical-depth/transmittance terms). **[SETTLED for the perception ranking.]**

**[CONTESTED] Tufte's "chartjunk" / data-ink-ratio dogma.** Tufte's prescription to maximize data-ink and strip "chartjunk" is enormously influential but empirically contested: **Bateman et al., "Useful Junk?" (CHI 2010)** found that embellished charts were often remembered better and no less accurately read. Treat minimalism as a strong default with documented exceptions, not a law.

---

### PHASE 11 — Software Engineering I: Architecture & Design (as a discipline)
**(a) Goal.** The intellectual core of building large software: managing complexity, modularity and information hiding, coupling/cohesion, architecture styles and patterns, and design patterns — read *critically*, with attention to what's principled versus conventional.

**(b) Prerequisites.** General programming maturity (you have it). Independent of the other tracks.

**(c) Primary.**
- John Ousterhout, *A Philosophy of Software Design*, 2nd ed. (Yaknyam Press, 2021) **[BUY]** — short, excellent, complexity-and-modularity-first; the best modern starting point.
- Bass, Clements & Kazman, *Software Architecture in Practice*, 4th ed. (Addison-Wesley, 2021) **[BUY]** — the architecture standard (quality attributes, tactics, ADRs).
- Gamma, Helm, Johnson & Vlissides (GoF), *Design Patterns* (Addison-Wesley, 1994) **[BUY]** — read critically.
- Seminal: **Parnas, "On the Criteria To Be Used in Decomposing Systems into Modules" (1972)** — the founding information-hiding paper, read it; **Conway's Law (1968)**; **Brooks, *The Mythical Man-Month* (1975)** and **"No Silver Bullet" (1986)**.

**(d) Supplementary.** Fowler, *Patterns of Enterprise Application Architecture* (2002) **[BUY]**; Buschmann et al., *Pattern-Oriented Software Architecture (POSA)* series **[BUY]**.

**(e) Exercises + Build.** **Build:** a **refactoring kata** (take deliberately messy code to well-structured code, narrating each move by Ousterhout's/Fowler's principles); design a non-trivial system with explicit **architecture decision records** and a critique of the quality-attribute trade-offs; apply *and* critique three GoF patterns in a real context.

**(f) Time.** 8–10 weeks.

**(g) MVP.** Ousterhout (all) + Parnas 1972 + Brooks "No Silver Bullet" + the refactoring kata.

⚛ *Bridge (light):* modularity and information hiding are about **decoupling weakly-interacting subsystems and hiding internal degrees of freedom** behind clean interfaces — the software analog of identifying separable subsystems and effective variables in physics.

**[CONTESTED] Design patterns and "Clean" prescriptions.** Peter Norvig's well-known observation is that several GoF patterns are **workarounds for language limitations** (many vanish in more expressive languages); patterns are also frequently over-applied. Robert Martin's *Clean Architecture*/*Clean Code* are popular but **empirically unsupported** and genuinely contested — read them as opinionated heuristics, not evidence. **[SETTLED-as-thesis]** Brooks's "No Silver Bullet": no single technique yields an order-of-magnitude productivity gain (still debated in the LLM era).

---

### PHASE 12 — Software Engineering II: Testing, Verification & Empirical SE / DevOps
**(a) Goal.** How software engineering establishes correctness and *evidence*: property-based and mutation testing, fuzzing, applied verification, empirical software engineering (experimentation and mining repositories), and evidence-based delivery (SRE, the DORA/*Accelerate* findings).

**(b) Prerequisites.** Phase 11.

**(c) Primary.**
- Wohlin, Runeson, Höst et al., *Experimentation in Software Engineering*, 2nd ed. (Springer, 2012) **[BUY]** — the empirical-SE methods text.
- **Google, *Site Reliability Engineering* and *The Site Reliability Workbook*** **[FREE online]** (sre.google) — the modern operations discipline.
- Forsgren, Humble & Kim, *Accelerate* (IT Revolution, 2018) **[BUY]** — the rigorous **DORA** research on what actually predicts software-delivery performance.
- Seminal: **Claessen & Hughes, "QuickCheck: A Lightweight Tool for Random Testing of Haskell Programs" (2000)** — property-based testing; **DeMillo, Lipton & Sayward (1978)** — mutation testing; **Royce (1970)** (and how "waterfall" misreads it); the empirical-SE evidence movement (Basili).

**(d) Supplementary.** Feathers, *Working Effectively with Legacy Code* (2004) **[BUY]**; Oram & Wilson (eds.), *Making Software* (O'Reilly, 2010) **[BUY]** — what the evidence says. **Applied verification (pointer, not spine):** Lamport, *Specifying Systems* (TLA+) **[FREE]** and Alloy — but defer the *foundations* to your theoretical-CS curriculum's logic phase.

**(e) Exercises + Build.** **Build:** a **property-based test suite** (Hypothesis for Python) for a real module; a **mutation-testing** run and an interpretation of the surviving mutants; a small **mining-software-repositories** empirical study (mine a Git history for a stated hypothesis — e.g., do larger changes correlate with later bug-fixes? — with proper stats); and a CI/CD pipeline instrumented for the **four DORA metrics**.

**(f) Time.** 8–11 weeks.

**(g) MVP.** *Accelerate* + the SRE book's core chapters + QuickCheck 2000 + the property-based-testing and MSR builds.

⚛ *Bridge:* **empirical SE is experimental science** — the same experimental design, statistics, and causal-inference care from Phase 3 and your physics training; A/B testing and the DORA analysis are applied inference.

**[HYPE-WATCH] Software engineering is weak on evidence.** A great deal of "best practice" is convention, not data: strong claims for **TDD-always**, **pair programming**, or specific **Agile** ceremonies are not well-supported empirically, and software *productivity measurement* is a notorious open problem (the "10x engineer" is largely myth). The **DORA/*Accelerate*** findings and the efficacy of **code review** are among the better-established results. Foreground the distinction between what's measured and what's asserted — this is the single most important calibration lesson in the cluster.

---

### PHASE 13 (Capstone) — Integrative Project + the Frontier
**(a) Goal.** Combine the tracks into one substantial artifact and transition to reading (and optionally producing) frontier work.

**(b) Prerequisites.** Most of Phases 1–12.

**(c) Capstone options (pick one).**
- **All four tracks at once:** a **scientific-visualization + rendering tool for a physics dataset** — physically-based volume/flow rendering (graphics + viz), engineered with proper architecture and testing (SWE), and evaluated with a real usability study (HCI).
- **A computational-photography application** with a well-designed, **accessible** UI, empirically evaluated.
- **A rendering-research reproduction:** reproduce a SIGGRAPH/EGSR paper end-to-end, engineered and documented.

**(d) Frontier tracking.** Venues: **CHI, UIST, CSCW** (HCI); **SIGGRAPH, SIGGRAPH Asia, EGSR, HPG, I3D** (graphics); **IEEE VIS / TVCG, EuroVis** (visualization); **ICSE, FSE (ESEC/FSE), ASE, EMSE** (software engineering). The ACM Digital Library and each field's "best paper" lists; SIGGRAPH course notes **[FREE]** are a goldmine.

**(e) Build.** The capstone itself, iterated to something presentable.

**(f) Time.** Ongoing (3–6 months for a solid capstone).

**(g) MVP.** A reduced version of one capstone option + a standing paper-reading habit (one paper/week from a chosen venue).

---

## Dependency Map

```
                 ┌─────────────────────────── FOUR SEMI-INDEPENDENT TRACKS ───────────────────────────┐

P1 Perception ──►  P2 HCI I ──► P3 HCI II ──► P4 HCI III            [HCI TRACK]
     │
     └───────────────────────────────────────────────► P10 Visualization   [VIZ TRACK]
                                                              ▲
P5 Signal/Image ─► P6 Graphics I (real-time) ─┐               │ (scientific viz uses rendering)
   foundations  │  P7 Graphics II (offline) ──┼─► P8 Geometry/Animation      [VISUAL-COMPUTING TRACK]
                └► P9 Computational Photography ┘

P11 SWE I (architecture) ──► P12 SWE II (testing/empirical/DevOps)          [SOFTWARE-ENGINEERING TRACK]

                 └───────────── all feed ─────────────► P13 Capstone + Frontier
```

- **Two shared foundations:** **P1 (perception)** before the HCI and visualization tracks; **P5 (signal/image)** before the graphics and computational-photography phases.
- **Within tracks (sequential):** HCI is P2→P3→P4; visual computing is P5→{P6, P7}→P8 and P5→P9; SWE is P11→P12.
- **Across tracks (parallel):** the four tracks are otherwise **independent** — do them in any order, or braid them. P11–P12 (SWE) can run entirely in parallel from day one.
- **Cross-links:** P6 builds on your systems-curriculum GPU/CUDA phase; P10's scientific viz reuses P6/P7 rendering; P12's applied verification points to your theory-curriculum logic phase.

---

## Overall MVP Fast-Path (~18–22 months part-time)
1. **Perception + HCI core:** Ware (perception essentials, Phase 1) → Norman + Fitts/GOMS (Phase 2) → Lazar et al. experimental design + one real usability study (Phase 3).
2. **Image + graphics core:** Gonzalez–Woods filtering/frequency/sampling (Phase 5) → **Ray Tracing in One Weekend** trilogy + pbrt's radiometry/rendering-equation/Monte-Carlo chapters (Phase 7) → LearnOpenGL through shadow mapping (Phase 6, lighter). *(Given your physics, Phase 7 is the highest-leverage, most-transferable phase in the whole curriculum — prioritize it.)*
3. **Visualization:** Munzner's framework + Cleveland–McGill + a couple of D3 builds and one scientific-viz project (Phase 10).
4. **Software engineering:** Ousterhout + Parnas + a refactoring kata (Phase 11) → *Accelerate* + property-based testing + one MSR mini-study (Phase 12).
5. **Capstone:** the physics-dataset viz+rendering tool (touches all four tracks), reduced.

---

## Recommendations

**Staged plan (assuming ~10–15 hrs/week), braiding the tracks.**
1. **Months 0–8:** P1 → P2 (perception + HCI I) **in parallel with** P5 (signal/image) and P11 (SWE I). *Benchmark:* your JND experiment analyzes cleanly; your from-scratch FFT filter demonstrates and then fixes aliasing; your refactoring kata is defensible.
2. **Months 8–20:** P3–P4 (HCI methods + accessibility) **‖** P6–P7 (graphics, real-time then offline) **‖** P12 (SWE testing/empirical). *Benchmark:* a properly-run controlled usability experiment; a validated path tracer passing a furnace test; a property-based suite that finds a real bug.
3. **Months 20–34:** P8–P9 (geometry/animation, computational photography) **‖** P10 (visualization). *Benchmark:* a Stable-Fluids solver; an HDR+panorama pipeline; a scientific-viz view of a physics dataset.
4. **Months 34+:** the capstone + a standing paper-reading habit.

**Where your choices shape the plan.** *Balanced* means the builds are the point — budget ~half your time for them, and the graphics/imaging phases are the most build-intensive. *Both rendering flavors in* means Phase 7 (offline, physics-heavy) and Phase 6 (real-time) both stay — but if time compresses, **do Phase 7 at full depth** (it's the one your background makes uniquely efficient) and treat Phase 6 as the lighter, applied companion. *All four sub-areas in* is broad; the software-engineering track (P11–P12) is the most self-contained and can be time-sliced independently if the visual-computing track dominates your attention.

**Best free lecture courses (all [FREE]).** MIT 6.837 (Computer Graphics), Stanford CS148/CS348 (graphics/rendering), TU Wien "Rendering" and UC San Diego rendering courses (on YouTube), CMU 15-463 (Computational Photography), the SIGGRAPH course-notes archive; IEEE-VIS tutorials; the Interaction Design Foundation and Nielsen Norman Group materials for HCI; the Google SRE books for the SWE-operations side.

**Frontier-tracking shortlist.** ACM DL for CHI/UIST/CSCW, SIGGRAPH/EGSR/HPG, IEEE VIS/TVCG, and ICSE/FSE/ASE/EMSE; the annual SIGGRAPH technical-papers "trailer" and course notes; "Papers We Love"; for evidence-based SWE, follow the empirical-SE and DORA research lines.

---

## Caveats
- **Editions not live-verified this pass.** Editions reflect my knowledge as of early 2026; I couldn't run a live check this turn. Verify especially: **Rogers–Sharp–Preece *Interaction Design*** (5th vs a newer edition), **Bass–Clements–Kazman *Software Architecture in Practice*** (4th ed. year), **Ware** (4th ed. 2021), **Real-Time Rendering** (4th ed. 2018 — check for a 5th), **Marschner & Shirley** (5th ed. 2021), and confirm **pbrt is on its 4th edition and still free at pbr-book.org**, **Szeliski's 2nd edition is still free**, and **Wilke** and the **Google SRE** books remain free. If you re-enable the Research toggle I'll verify the whole list and refresh links.
- **Free-vs-paid.** The **[FREE]** items are legitimately free from authors/publishers/universities (pbr-book.org, Ray Tracing in One Weekend, tinyrenderer, LearnOpenGL, WebGPU Fundamentals, Szeliski's *Computer Vision*, Wilke's *Fundamentals of Data Visualization*, the Google SRE books, CMU 15-463, the SIGGRAPH course archive, W3C WCAG, NN/g articles, and most seminal papers via authors' pages or DOI). In-copyright **[BUY]** books (Norman, Ware, Munzner, Tufte, Gonzalez–Woods, Real-Time Rendering, Marschner–Shirley, Ousterhout, Bass–Clements–Kazman, GoF, Wohlin et al., *Accelerate*, Lazar et al., etc.) should be purchased — pirated PDFs aren't endorsed.
- **Overlap boundaries.** Formal-methods *foundations* live in your theory curriculum (this cluster's SWE track only points to applied tools like TLA+/Alloy); CS-graphics stays algorithmic and distinct from your Filmmaking/Colour-theory tracks (with the light/camera/colour touchpoints flagged); real-time graphics assumes the GPU/CUDA knowledge from your systems curriculum rather than re-teaching it.
- **Calibration.** The genuinely contested/low-evidence spots are tagged: software engineering's weak evidence base and the productivity-measurement problem **[HYPE-WATCH]**, the design-patterns/"Clean" critiques **[CONTESTED]**, Nielsen's "5 users" **[CONTESTED]**, Tufte's chartjunk dogma **[CONTESTED]**, and the converging real-time/offline rendering boundary **[EVOLVING]**. Treat sources that present these as settled with suspicion.
- **Scope realism.** This is a genuine multi-year, build-heavy, four-track program; estimates assume a mathematically mature learner at ~10–15 hrs/week. Because the tracks are semi-independent, this curriculum tolerates interleaving and pausing better than the theory or systems ones — pick the track that fits your current appetite and let the others wait.