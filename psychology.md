# A Graduate-Level Psychology Curriculum & Reading List for the Technical Autodidact

## TL;DR
- **This is a complete, primary-source-centered graduate psychology curriculum** organized as 13 sequential phases (history/methods → biological foundations → perception/cognition → learning/emotion/development → personality/social/clinical → evolutionary lens), with a **~6–9-month compressed MVP fast-path** and a **~3–4-year full arc**. Every phase names the authoritative current-edition graduate textbook, the seminal original papers (with precise citations), a hands-on Python/statistics project matched to your ML background, and an epistemic-calibration tag.
- **Honest replication calibration is built in.** Robust areas (psychophysics/signal-detection theory, working-memory capacity limits, the Big Five's descriptive structure, prospect theory) are tagged SETTLED; famous casualties of the replication crisis — ego depletion, social/elderly priming, power posing, and the Stanford Prison Experiment's "power of the situation" narrative — are tagged HYPE-WATCH with the specific debunking citations. The Open Science Collaboration (2015) found that only **36% of replications were statistically significant** versus 97% of the original studies.
- **Many canonical primary works are free and legal.** Christopher D. Green's *Classics in the History of Psychology* (psychclassics.yorku.ca) hosts full texts of James, Ebbinghaus, Watson, Wundt, Miller, Asch, Milgram, and Bandura; the Internet Archive and Project Gutenberg host public-domain monographs (Hebb, Pavlov). These are distinguished throughout from paywalled graduate anchors (Kandel 6th ed., Gazzaniga 5th ed., DSM-5-TR).

## Key Findings
- **The curriculum is dual-track by design.** The MVP fast-path delivers an educated-generalist *advanced* command of the whole field in roughly 6–9 months of serious part-time study; the full arc is a multi-year program that engages the primary empirical literature phase by phase.
- **Current editions verified (September 2026):** Kandel et al., *Principles of Neural Science* **6th ed. (2021)**; Gazzaniga, Ivry & Mangun, *Cognitive Neuroscience: The Biology of the Mind* **5th ed. (2019)** (a 6th ed. adding Bassett & Phelps has been announced by W. W. Norton); Eysenck & Keane, *Cognitive Psychology: A Student's Handbook* **8th ed. (2020)**; Goldstein & Cacciamani, *Sensation and Perception* **11th ed. (2021)**; Domjan, *The Principles of Learning and Behavior* **7th ed. (2015)**; Fiske, Gilbert & Lindzey, *Handbook of Social Psychology* **5th ed. (2010)**; *DSM-5-TR* **(2022)**; Embretson & Reise, *Item Response Theory* (**new "Foundations for Psychologists and Social Scientists" edition, 2026**; original *Item Response Theory for Psychologists*, 2000); Buss, *Evolutionary Psychology: The New Science of the Mind* **7th ed. (2023)**; Leahey, *A History of Psychology* (8th ed.; a retitled 9th ed., *A Critical History of Psychology*, is now in print).
- **Replication status is load-bearing, not cosmetic.** The Open Science Collaboration sampled 100 studies from three 2008 journals (*Psychological Science*; *Journal of Personality and Social Psychology*; *Journal of Experimental Psychology: Learning, Memory, and Cognition*); 36% of replications reached significance and 39% were subjectively judged to have replicated. Social psychology fared worst (~25%).
- **Cross-disciplinary bridges are genuine.** Signal detection theory (from radar/information theory), the Rescorla-Wagner rule (the delta rule and precursor to temporal-difference reinforcement learning), factor analysis vs. PCA/eigen-decomposition, Hebbian learning and neural nets, Bayesian/predictive-coding models of perception, and Marr's three levels of analysis all map directly onto your ML/physics toolkit and are flagged as OPTIONAL enrichment where load-bearing.

## Details

### How to use this curriculum
Each phase specifies: (1) mastery goals; (2) prerequisites; (3) **PRIMARY** readings — canonical graduate texts plus seminal original papers, cited with author, title, year, and edition; (4) **SUPPLEMENTARY** readings; (5) an optional Python/statistics project; (6) estimated time. **Calibration tags:** SETTLED (robust, well-replicated consensus), CONTESTED (active scholarly disagreement), OPEN (genuinely unresolved), HYPE-WATCH (overhyped / weak or failed evidence). **Access tags:** FREE (public-domain / open-access) vs. PAYWALLED.

**Free-resource backbone (used throughout):**
- **Classics in the History of Psychology** — Christopher D. Green, York University, psychclassics.yorku.ca. Over 25 books and ~200 public-domain articles, several with commentaries by leading historians. **FREE.**
- **Internet Archive** (archive.org) and **Project Gutenberg** for public-domain monographs. **FREE.**
- **Noba Project, LibreTexts, OpenStax *Psychology 2e*, MIT OpenCourseWare** for open textbook-level scaffolding when you want a fast orientation before the primary sources. **FREE.**

### DEPENDENCY MAP
- **Phases 1 (History) and 2 (Methods/Statistics/Psychometrics)** run first and in parallel; they underpin everything and recalibrate how you read every later empirical claim.
- **Phase 3 (Biological)** feeds Phase 4 (Sensation/Perception), Phase 6 (Cognitive Neuroscience), Phase 7 (Learning), and Phase 8 (Motivation/Emotion).
- **Phase 4 → Phase 5 (Cognitive) → Phase 6 (Cognitive Neuroscience).**
- **Phases 5 and 2 → Phase 9 (Developmental), Phase 10 (Personality), Phase 11 (Social).**
- **Phases 3, 5, 10, 11 → Phase 12 (Clinical/Abnormal).**
- **Phase 13 (Evolutionary)** is an integrating lens applied retrospectively across Phases 7–12.

---

### PHASE 1 — History & Systems of Psychology
**Goals:** Trace the discipline from the philosophy of mind through Wundt and the founding of experimental psychology, structuralism, functionalism, Gestalt, psychoanalysis, behaviorism, the cognitive revolution, humanism, evolutionary psychology, the rise of neuroscience, and the replication/open-science era. Mastery = you can situate any modern claim in its intellectual lineage.
**Prerequisites:** None.
**PRIMARY readings:**
- Thomas Hardy Leahey, *A History of Psychology: From Antiquity to Modernity* (8th ed., Routledge; a 9th ed., retitled *A Critical History of Psychology: From Antiquity to Modernity*, is now published). The graduate-level standard. **PAYWALLED.**
- William James, *The Principles of Psychology* (Henry Holt, 1890) — read the chapters on habit, the stream of thought, attention, memory, will. **FREE** (psychclassics; Gutenberg).
- John B. Watson, "Psychology as the Behaviorist Views It," *Psychological Review*, 20 (1913), 158–177 — the behaviorist manifesto. **FREE** (psychclassics).
- Wilhelm Wundt, selections. **FREE** (psychclassics).
**SUPPLEMENTARY:** B. R. Hergenhahn & Tracy Henley, *An Introduction to the History of Psychology* (Cengage) — accessible narrative that ties concepts to their philosophical roots. **PAYWALLED** (older editions **FREE** via Internet Archive).
**Project:** Build a citation/influence network (NetworkX) of ~50 landmark works with edges representing intellectual influence; compute centrality measures to identify structural hubs (James, Wundt, Helmholtz, Darwin).
**Time:** 3–5 weeks.

---

### PHASE 2 — Research Methods, Statistics & Psychometrics
**Goals:** Master experimental design, measurement theory (classical test theory and item response theory), factor analysis, causal inference in psychology, meta-analysis, and — critically — the reproducibility crisis and its reforms (preregistration, registered reports, questionable research practices).
**Prerequisites:** Your existing statistics/linear-algebra/Bayesian background (satisfied).
**PRIMARY readings:**
- Susan E. Embretson & Steven P. Reise, *Item Response Theory: Foundations for Psychologists and Social Scientists* (Routledge, 2026 edition; the field-defining original was *Item Response Theory for Psychologists*, Lawrence Erlbaum, 2000). The canonical psychometrics graduate text. **PAYWALLED.**
- Joseph P. Simmons, Leif D. Nelson & Uri Simonsohn, "False-Positive Psychology: Undisclosed Flexibility in Data Collection and Analysis Allows Presenting Anything as Significant," *Psychological Science*, 22(11) (2011), 1359–1366 — defines "researcher degrees of freedom" and p-hacking. **PAYWALLED** (author PDF widely available).
- Open Science Collaboration, "Estimating the Reproducibility of Psychological Science," *Science*, 349(6251) (2015), article aac4716. The headline result, verbatim: *"Ninety-seven percent of original studies had statistically significant results. Thirty-six percent of replications had statistically significant results … Replication effects (Mr = .197, SD = .257) were half the magnitude of original effects (Mr = .403, SD = .188)."* **FREE** via OSF (osf.io/ezcuj).
- Brian A. Nosek et al., "The Preregistration Revolution," *PNAS* (2018). **FREE.**
**SUPPLEMENTARY:** Jacob Cohen, "The Earth Is Round (p < .05)," *American Psychologist* (1994); Borenstein et al., *Introduction to Meta-Analysis* for the meta-analytic machinery.
**Project:** Fit a 2-parameter logistic (2PL) IRT model to a public item-response dataset (e.g., an open Big Five or ability dataset) in Python; compare CTT vs. IRT item statistics; then run an exploratory factor analysis and contrast the factor solution against a PCA eigen-decomposition of the same correlation matrix.
**Bridge (OPTIONAL):** Factor analysis and PCA both rest on eigen-decompositions of covariance/correlation matrices, but factor analysis is a latent-variable *measurement* model that partitions common vs. unique variance; IRT is a nonlinear latent-trait model closely related to logistic regression — familiar territory for you.
**Calibration:** That the replication crisis occurred = **SETTLED**. Which specific classic effects survive = **CONTESTED**.
**Time:** 6–10 weeks.

---

### PHASE 3 — Biological / Physiological Psychology & Behavioral Neuroscience
**Goals:** Neurons and neurotransmission, brain organization, neuroendocrinology, psychopharmacology, and methods (EEG, fMRI, optogenetics, single-unit recording).
**Prerequisites:** Phases 1–2 helpful; your physics/math background aids the biophysics (Hodgkin-Huxley).
**PRIMARY readings:**
- Eric R. Kandel, John D. Koester, Sarah H. Mack & Steven A. Siegelbaum (eds.), *Principles of Neural Science*, 6th ed. (McGraw-Hill, 2021) — the gold-standard reference; the 6th edition adds a chapter on the computational bases of neural circuits. **PAYWALLED** (older editions **FREE** via Internet Archive).
- Donald O. Hebb, *The Organization of Behavior: A Neuropsychological Theory* (John Wiley & Sons, 1949). **FREE** (Internet Archive, original edition).
**SUPPLEMENTARY:** Dale Purves et al., *Neuroscience*, 6th ed. (Sinauer/Oxford, 2018) — a leaner alternative anchor. **PAYWALLED.**
**Project:** Implement the Hodgkin-Huxley equations in Python (SciPy ODE integration) and reproduce an action potential; then implement a Hebbian learning rule on a toy two-layer network and observe weight self-organization.
**Bridge (OPTIONAL):** Hebb's postulate ("cells that fire together wire together") is the direct ancestor of Hebbian learning rules and, with normalization/anti-Hebbian modification, of the unsupervised learning rules you already know.
**Time:** 8–12 weeks.

---

### PHASE 4 — Sensation & Perception
**Goals:** Psychophysics, signal detection theory, vision, audition, the chemical and tactile senses, and perceptual organization (Gestalt).
**Prerequisites:** Phase 3.
**PRIMARY readings:**
- E. Bruce Goldstein & Laura Cacciamani, *Sensation and Perception*, 11th ed. (Cengage, 2021) — the long-standing standard. **PAYWALLED.**
- Gustav Fechner, *Elements of Psychophysics* (1860) — selections on the Weber-Fechner law. **FREE** (psychclassics/Internet Archive).
- Gestalt primary sources: Max Wertheimer, Wolfgang Köhler, Kurt Koffka — selections. **FREE** (psychclassics).
- David Marr, *Vision: A Computational Investigation into the Human Representation and Processing of Visual Information* (W. H. Freeman, 1982; MIT Press reprint 2010, with Shimon Ullman foreword and Tomaso Poggio afterword). **PAYWALLED.**
**Project:** Simulate a signal-detection-theory model in Python: generate signal-plus-noise vs. noise distributions, compute d′ and criterion c, and plot the ROC curve; then fit a Fechner/Weber log-law (or Stevens power-law) to psychophysical discrimination data.
**Bridge (OPTIONAL):** SDT descends directly from radar detection and information theory (Tanner & Swets, 1954); d′ is a discriminability index mathematically identical to signal-to-noise separation — and it is the same framework underlying ROC/AUC evaluation in your fraud-detection models. Marr's three levels (computational / algorithmic / implementational) are a rigorous and reusable framework for structuring any modeling problem.
**Calibration:** Psychophysics and SDT = **SETTLED**. Fechner's exact logarithmic law vs. Stevens' power law = **CONTESTED**.
**Time:** 6–8 weeks.

---

### PHASE 5 — Cognitive Psychology
**Goals:** Attention, memory, knowledge representation, language, reasoning, problem-solving, and judgment/decision-making — plus the intellectual history of the cognitive revolution.
**Prerequisites:** Phase 4.
**PRIMARY readings:**
- Michael W. Eysenck & Mark T. Keane, *Cognitive Psychology: A Student's Handbook*, 8th ed. (Routledge, 2020) — widely regarded as the leading comprehensive text. **PAYWALLED.**
- George A. Miller, "The Magical Number Seven, Plus or Minus Two: Some Limits on Our Capacity for Processing Information," *Psychological Review*, 63(2) (1956), 81–97. **FREE** (psychclassics.yorku.ca/Miller/).
- Ulric Neisser, *Cognitive Psychology* (Appleton-Century-Crofts, 1967; Psychology Press Classic Edition, 2014) — the field's first true textbook. **PAYWALLED.**
- Noam Chomsky, review of B. F. Skinner's *Verbal Behavior*, *Language*, 35(1) (1959), 26–58 — the review that helped end behaviorism's dominance. **FREE** (chomsky.info).
- Hermann Ebbinghaus, *Memory: A Contribution to Experimental Psychology* (1885; Ruger & Bussenius trans., Teachers College, 1913). **FREE** (psychclassics.yorku.ca/Ebbinghaus/).
- Endel Tulving, "Episodic and Semantic Memory," in E. Tulving & W. Donaldson (eds.), *Organization of Memory* (Academic Press, 1972), 381–403. **PAYWALLED.**
- Daniel Kahneman & Amos Tversky, "Prospect Theory: An Analysis of Decision under Risk," *Econometrica*, 47(2) (1979), 263–291; and Tversky & Kahneman, "Judgment under Uncertainty: Heuristics and Biases," *Science*, 185(4157) (1974), 1124–1131. **FREE PDFs** widely mirrored.
- Elizabeth Loftus, seminal eyewitness-memory / misinformation-effect papers (e.g., Loftus & Palmer, 1974).
**Project:** Implement a drift-diffusion model of two-alternative forced-choice reaction time in Python and fit it to a public RT dataset; alternatively, reproduce the Deese-Roediger-McDermott false-memory analysis.
**Bridge (OPTIONAL):** Bayesian models of cognition and prospect theory's value/probability-weighting functions connect directly to your probability and decision-theory background.
**Calibration:** Working-memory capacity limits = **SETTLED**; Kahneman & Tversky heuristics and prospect theory = **SETTLED**; some social/attention priming subfields = **HYPE-WATCH**.
**Time:** 10–12 weeks.

---

### PHASE 6 — Cognitive Neuroscience
**Goals:** Bridge brain and cognition — methods, attention, memory systems, language, cognitive control, social cognition, consciousness.
**Prerequisites:** Phases 3 and 5.
**PRIMARY readings:**
- Michael S. Gazzaniga, Richard B. Ivry & George R. Mangun, *Cognitive Neuroscience: The Biology of the Mind*, 5th ed. (W. W. Norton, 2019); a 6th edition adding Dani S. Bassett and Elizabeth A. Phelps as authors has been announced. **PAYWALLED** (4th ed. **FREE** via Internet Archive).
**SUPPLEMENTARY:** Selected *Trends in Cognitive Sciences* and *Nature Reviews Neuroscience* review articles on your topics of interest.
**Project:** Download an open fMRI or EEG dataset from OpenNeuro and run a basic GLM analysis or multivariate pattern (MVPA) decoding with nilearn/MNE-Python.
**Time:** 6–8 weeks.

---

### PHASE 7 — Learning & Conditioning
**Goals:** Classical and operant conditioning, learning theory, the behaviorist history, and contemporary associative/computational models.
**Prerequisites:** Phases 3 and 5.
**PRIMARY readings:**
- Michael Domjan, *The Principles of Learning and Behavior*, 7th ed. (Cengage, 2015) — the standard graduate/advanced text. **PAYWALLED** (multiple editions **FREE** via Internet Archive).
- Ivan Pavlov, *Conditioned Reflexes* (Oxford, 1927). **FREE** (Internet Archive).
- B. F. Skinner, *The Behavior of Organisms* (1938) — selections.
- Robert A. Rescorla & Allan R. Wagner, "A Theory of Pavlovian Conditioning: Variations in the Effectiveness of Reinforcement and Nonreinforcement," in A. H. Black & W. F. Prokasy (eds.), *Classical Conditioning II: Current Research and Theory* (Appleton-Century-Crofts, 1972), 64–99. **PAYWALLED.**
**Project:** Implement the Rescorla-Wagner model in Python and reproduce the blocking and overshadowing phenomena; then demonstrate its algebraic equivalence to the delta rule and connect it to temporal-difference learning.
**Bridge (OPTIONAL):** The Rescorla-Wagner update, ΔV = αβ(λ − ΣV), is an error-correcting rule essentially identical to the Widrow-Hoff (1960) delta rule and a direct conceptual precursor to temporal-difference reinforcement learning (Sutton & Barto). The dopamine reward-prediction-error signal (Schultz, Dayan & Montague, *Science*, 1997) is its neural realization — a clean bridge from behaviorist psychology to modern RL.
**Calibration:** Rescorla-Wagner as the foundational quantitative model = **SETTLED**, with well-known limits (it cannot handle latent inhibition or configural learning without extension).
**Time:** 5–7 weeks.

---

### PHASE 8 — Motivation & Emotion / Affective Science
**Goals:** Theories of emotion (James-Lange, Cannon-Bard, Schachter-Singer two-factor, appraisal theories, basic-emotion theory, psychological constructionism), drives, and reward.
**Prerequisites:** Phases 3 and 5.
**PRIMARY readings:**
- Michael Lewis, Jeannette M. Haviland-Jones & Lisa Feldman Barrett (eds.), *Handbook of Emotions* (Guilford; current edition) — the field reference. **PAYWALLED.**
- William James, "What Is an Emotion?" *Mind*, 9 (1884), 188–205. **FREE.**
- Joseph E. LeDoux, "Rethinking the Emotional Brain," *Neuron*, 73(4) (2012), 653–676.
- Lisa Feldman Barrett, "The Theory of Constructed Emotion: An Active Inference Account of Interoception and Categorization," *Social Cognitive and Affective Neuroscience*, 12 (2017), 1–23.
- Kristen A. Lindquist et al., "The Brain Basis of Emotion: A Meta-Analytic Review," *Behavioral and Brain Sciences*, 35(3) (2012), 121–143.
**Project:** Build a valence-arousal (circumplex) affect classifier on a text corpus; empirically compare a discrete basic-emotion labeling scheme against a dimensional model.
**Bridge (OPTIONAL):** Barrett's constructed-emotion account is explicitly an *active-inference / predictive-coding* model — the same Bayesian machinery appearing in Phase 4/5.
**Calibration:** Basic-emotion theory (discrete emotions with distinct, localizable brain signatures) = **CONTESTED** (the Lindquist et al. meta-analysis found little evidence for clean localization); psychological constructionism = **CONTESTED/OPEN**.
**Time:** 4–6 weeks.

---

### PHASE 9 — Developmental Psychology
**Goals:** Lifespan development — Piaget, Vygotsky, attachment, and cognitive/social/moral development through aging.
**Prerequisites:** Phases 2 and 5.
**PRIMARY readings:**
- Jean Piaget, e.g., *The Origins of Intelligence in Children* (1936/1952).
- Lev Vygotsky, *Mind in Society: The Development of Higher Psychological Processes* (Harvard, 1978).
- John Bowlby, *Attachment and Loss* trilogy (1969–1980); Mary D. S. Ainsworth et al., *Patterns of Attachment* (Erlbaum, 1978) — the Strange Situation.
- A graduate handbook chapter set from the *Handbook of Child Psychology and Developmental Science* (Wiley, 7th ed.). **PAYWALLED.**
**Project:** Re-analyze an open longitudinal dataset and fit a growth-curve / mixed-effects model in Python (statsmodels or a Bayesian approach in PyMC).
**Calibration:** Attachment security predicting later outcomes = broadly **SETTLED**, but with modest effect sizes and debated cross-cultural generality; Piaget's discrete, age-locked stages = **CONTESTED** (ages and strict sequence substantially revised by later research).
**Time:** 6–8 weeks.

---

### PHASE 10 — Personality Psychology
**Goals:** Psychodynamic, trait (Big Five / Five-Factor Model), humanistic, and social-cognitive approaches; personality assessment; and the person-situation debate.
**Prerequisites:** Phases 2 and 5.
**PRIMARY readings:**
- Gordon W. Allport, *Personality: A Psychological Interpretation* (Holt, 1937).
- Lewis R. Goldberg, "An Alternative 'Description of Personality': The Big-Five Factor Structure," *Journal of Personality and Social Psychology*, 59(6) (1990), 1216–1229 — the lexical-tradition anchor. **FREE PDF** (ori.org).
- Paul T. Costa & Robert R. McCrae, foundational NEO-PI-R papers, including McCrae & Costa, "Updating Norman's 'Adequate Taxonomy,'" *JPSP*, 49 (1985), 710–721, and McCrae & John, "An Introduction to the Five-Factor Model and Its Applications," *Journal of Personality*, 60(2) (1992), 175–215.
- Walter Mischel, *Personality and Assessment* (Wiley, 1968) — the person-situation critique.
- Sigmund Freud, key works (e.g., *The Interpretation of Dreams*, *The Ego and the Id*). **FREE** selections (Gutenberg/psychclassics).
**Project:** Run exploratory and confirmatory factor analysis (EFA/CFA) on the open-source IPIP Big Five dataset in Python; test the five-factor structure and assess measurement invariance across groups.
**Bridge (OPTIONAL):** The Big Five *is* the output of factor analysis applied to the covariance of trait descriptors — a direct application of your linear-algebra background, and a clean case study in what factor analysis can and cannot tell you about latent structure.
**Calibration:** The Big Five's descriptive structure = **SETTLED**; classical Freudian psychodynamic theory as *falsifiable science* = **HYPE-WATCH** (historically foundational, empirically weak); the person-situation debate = resolved toward interactionism (**SETTLED**).
**Time:** 6–8 weeks.

---

### PHASE 11 — Social Psychology
**Goals:** Attitudes, social cognition, conformity, obedience, group processes, attribution, prejudice — and the modern reappraisals of the classic experiments.
**Prerequisites:** Phases 2, 5, and 10.
**PRIMARY readings:**
- Susan T. Fiske, Daniel T. Gilbert & Gardner Lindzey (eds.), *Handbook of Social Psychology*, 5th ed. (Wiley, 2010) — the standard professional reference. **PAYWALLED** (4th ed. **FREE** via Internet Archive).
- Leon Festinger, *A Theory of Cognitive Dissonance* (Stanford, 1957).
- Solomon Asch, conformity studies (1951, 1956). **FREE** (some via psychclassics).
- Stanley Milgram, "Behavioral Study of Obedience," *Journal of Abnormal and Social Psychology*, 67 (1963), 371–378. **FREE** (psychclassics).
- Albert Bandura, Dorothea Ross & Sheila Ross, Bobo-doll studies (*JASP*, 1961). **FREE** (psychclassics).
**Modern reappraisals (REQUIRED):**
- Thibault Le Texier, "Debunking the Stanford Prison Experiment," *American Psychologist*, 74(7) (2019), 823–839 (doi:10.1037/amp0000401). Based on *"a thorough investigation of the SPE archives and interviews with 15 of the participants,"* Le Texier documents demand characteristics and that guards were coached toward cruelty rather than spontaneously transformed — sharply downgrading the study's scientific standing.
- Open Science Collaboration (2015) — social psychology replicated at roughly 25%.
**Project:** Re-analyze an open Many Labs replication dataset; compute standardized effect sizes and compare original vs. replication magnitudes with forest plots.
**Calibration:** Ego depletion = **HYPE-WATCH** (a 23-lab registered replication and a collaborator-led project both failed to find the effect); social/elderly priming = **HYPE-WATCH** (Doyen et al. 2012 failed to replicate Bargh); power posing = **HYPE-WATCH** — original co-author Dana Carney's 2016 statement is unambiguous: *"I do not believe that 'power pose' effects are real … the evidence against the existence of power poses is undeniable."* Stanford Prison Experiment = **HYPE-WATCH/largely discredited**; Milgram obedience = **CONTESTED** (the effect is real but its internal validity and interpretation are actively debated); cognitive dissonance = **SETTLED**.
**Time:** 8–10 weeks.

---

### PHASE 12 — Clinical & Abnormal Psychology / Psychopathology
**Goals:** Models of mental disorder, the DSM/ICD classification systems and their controversies, major disorder categories, and therapeutic approaches (psychodynamic, behavioral, cognitive-behavioral, humanistic) with their efficacy evidence.
**Prerequisites:** Phases 3, 5, 10, and 11.
**PRIMARY readings:**
- American Psychiatric Association, *Diagnostic and Statistical Manual of Mental Disorders, 5th ed., Text Revision (DSM-5-TR)* (APA, 2022) — adds prolonged grief disorder and revised text for 70+ disorders. **PAYWALLED.**
- WHO, *ICD-11* — **FREE** (online browser).
- A graduate abnormal/clinical text such as Ann M. Kring et al., *Abnormal Psychology: The Science and Treatment of Psychological Disorders* (current edition). **PAYWALLED.**
- Aaron T. Beck, *Cognitive Therapy and the Emotional Disorders* (International Universities Press, 1976).
**Controversies (REQUIRED):** Allen Frances's critiques of DSM diagnostic inflation ("diagnostic hyperinflation"); the NIMH Research Domain Criteria (RDoC) as a dimensional alternative to categorical diagnosis.
**Project:** Analyze an open mental-health survey dataset; build a predictive model and write a critical discussion of construct validity and measurement issues (what does the label actually measure?).
**Calibration:** CBT efficacy for anxiety and depression = **SETTLED** (though absolute effect sizes and long-term durability are debated); DSM categorical validity = **CONTESTED**; the chemical-imbalance (serotonin) theory of depression = **HYPE-WATCH** — Moncrieff et al., "The Serotonin Theory of Depression: A Systematic Umbrella Review of the Evidence," *Molecular Psychiatry* (2022), concludes there is *"no convincing evidence that depression is caused by serotonin abnormalities, particularly by lower levels or reduced activity of serotonin"* (note that this concerns *etiology*, not whether SSRIs have clinical effects).
**Time:** 8–10 weeks.

---

### PHASE 13 — Evolutionary Psychology (Integrating Lens)
**Goals:** Use evolutionary theory as a metatheoretical lens across the field; understand adaptationism and, equally, its major criticisms.
**Prerequisites:** Phases 5–12 (apply retrospectively).
**PRIMARY readings:**
- Jerome H. Barkow, Leda Cosmides & John Tooby (eds.), *The Adapted Mind: Evolutionary Psychology and the Generation of Culture* (Oxford University Press, 1992) — the foundational volume, including Tooby & Cosmides, "The Psychological Foundations of Culture" (pp. 19–136).
- David M. Buss, *Evolutionary Psychology: The New Science of the Mind*, 7th ed. (Routledge, 2023). **PAYWALLED.**
- Leda Cosmides, "The Logic of Social Exchange: Has Natural Selection Shaped How Humans Reason? Studies with the Wason Selection Task," *Cognition*, 31(3) (1989), 187–276.
**Critiques (REQUIRED):**
- David J. Buller, *Adapting Minds: Evolutionary Psychology and the Persistent Quest for Human Nature* (MIT Press, 2005).
- Johan J. Bolhuis, Gillian R. Brown, Robert C. Richardson & Kevin N. Laland, "Darwin in Mind: New Opportunities for Evolutionary Psychology," *PLoS Biology*, 9(7) (2011), e1001109.
**Project:** Take one evolutionary-psychology claim (e.g., cheater detection, mate-preference sex differences) and critically evaluate it — either re-analyze available data or formalize its predictions and identify what evidence would falsify it.
**Calibration:** Evolutionary framing of cognition = **CONTESTED** (a useful and generative metatheory, but many specific adaptationist claims are **HYPE-WATCH** because they are difficult to falsify and prone to post-hoc storytelling).
**Time:** 4–6 weeks.

---

## TWO TRACKS

### MVP FAST-PATH (~6–9 months, part-time)
The minimum canonical spine to reach educated-generalist *advanced* command:
1. **History (skim):** Leahey, plus James and Watson primary excerpts (psychclassics).
2. **Methods essentials:** Embretson & Reise (selected chapters) + the three open-science papers (Simmons 2011; OSC 2015; Nosek 2018).
3. **Biological:** Kandel (selected chapters).
4. **Perception:** Goldstein (perception + psychophysics/SDT chapters).
5. **Cognition:** Eysenck & Keane + Miller (1956) and Kahneman-Tversky (1974, 1979).
6. **Learning:** Rescorla-Wagner paper + project.
7. **Cognitive neuroscience:** Gazzaniga (selected).
8. **Personality:** Goldberg (1990) + Big Five factor-analysis project.
9. **Social:** Milgram (1963) + Le Texier (2019) + OSC (2015).
10. **Clinical:** DSM-5-TR overview + one abnormal-psych chapter.
11. **Evolutionary lens:** Buss (2023).

Complete **four signature projects**: IRT/factor analysis, SDT/ROC, Rescorla-Wagner, and a Many Labs re-analysis. These four alone convert the reading into durable, defensible understanding.

### FULL ARC (~3–4 years)
All 13 phases in dependency order, with the complete primary-literature reading lists and every hands-on project. Budget roughly one phase every 6–10 weeks at ~8–10 hours/week; the biological, cognitive, social, and clinical phases are the heaviest.

## Recommendations
1. **Start immediately with Phases 1 + 2 in parallel.** History reading plus methods/psychometrics recalibrates how you read every later empirical claim. *Benchmark to proceed:* you can explain why the 2015 reproducibility rate was 36%, and correctly define p-hacking, HARKing, and preregistration.
2. **Front-load the projects that leverage your ML background** — IRT, factor analysis, SDT/ROC, and Rescorla-Wagner. Signal detection theory and decision thresholds in particular map onto your fraud-prevention work (ROC/AUC, criterion setting under asymmetric costs), so Phase 4 will pay professional dividends.
3. **Treat calibration tags as decision rules.** For any HYPE-WATCH finding, read the *original* and the *debunking* before you ever cite it. *Threshold to upgrade a finding from CONTESTED to SETTLED:* a preregistered, adequately powered, multi-lab replication (e.g., a Many Labs / Registered Replication Report).
4. **Use free primary sources first.** Exhaust psychclassics.yorku.ca, Internet Archive, and OSF before spending; then buy only the current-edition graduate anchors you will reference repeatedly — Kandel (6th), Gazzaniga (5th/6th), Eysenck & Keane (8th), Goldstein & Cacciamani (11th), and DSM-5-TR.
5. **Revisit Phase 13 last, then loop back.** Once you have the evolutionary lens, re-read your Phase 8/9/10/11 notes; the integration is where generalist mastery consolidates.

## Caveats
- **Edition currency:** Editions were verified as of September 2026. Two anchors are mid-transition — a Gazzaniga *Cognitive Neuroscience* 6th edition (adding Bassett & Phelps) and Leahey's retitled *A Critical History of Psychology* — so confirm the latest printing before purchase. The Embretson & Reise psychometrics text has been reissued under a new title/edition; either the 2000 original or the new edition is fine for the concepts.
- **Access:** Several seminal chapters and monographs (Tulving 1972, Rescorla-Wagner 1972, *The Adapted Mind*, the Marr and Neisser reprints) are paywalled; library or interlibrary access is assumed. Where I have flagged a work as FREE, that reflects a legal public-domain or open-access source (psychclassics, Internet Archive originals, OSF, author sites).
- **Epistemic tags are living annotations.** They reflect the evidence as of 2026 and will shift; a HYPE-WATCH effect could be rehabilitated by strong new replications, and today's SETTLED consensus could narrow. Re-check the replication literature (Many Labs, Registered Replication Reports, FORRT database) periodically.
- **One sourcing note:** the "chemical-imbalance = HYPE-WATCH" tag concerns the *serotonin-deficiency etiology* of depression, not the clinical question of whether antidepressants work — keep that distinction sharp when citing Moncrieff et al. (2022).