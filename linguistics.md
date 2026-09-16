# A Broad, Even-Handed Linguistics Curriculum & Reading List (Intermediate, ~2 Years)
### Consolidated edition — editions, access, and calibration verified September 2026

## TL;DR
- **A panoramic survey of all the core subfields** in 14 modules: foundations → phonetics → phonology → morphology → syntax (data, then frameworks) → semantics → pragmatics → historical/comparative → typology & universals → sociolinguistics → psycholinguistics/acquisition/neurolinguistics → computational & corpus → capstone.
- **Intermediate depth (the "in-between" bar).** More than a shallow survey, short of graduate research mastery across every subfield: you'll be able to *do* the analysis in each area and read the foundational literature. ~2 years part-time.
- **Even-handed on the field's central divide.** Wherever the generative/Chomskyan and functionalist/usage-based/cognitive traditions diverge — syntax, semantics, phonology, acquisition — you read the leading text from *each* camp plus the debate papers.
- **Moderate, Python-friendly hands-on** — a few signature exercises per module, with **[BRIDGE]** markers where your signal-processing, information-theory, logic/type-theory, automata, and regression background is genuinely load-bearing.
- **Honest, current calibration.** Universal Grammar / poverty-of-the-stimulus is CONTESTED and has been reignited by large language models (Piantadosi 2024 vs. rebuttals; Kallini et al. 2024 vs. Hunter 2025); strong linguistic relativity is rejected while weak relativity is supported in specific domains; the comparative method is bedrock; long-range macro-families are HYPE-WATCH; the field's syntax is genuinely split.
- **Overlaps re-covered here, per your call:** Sapir-Whorf/relativity, language ideology, and ethnography of communication are re-covered in the socio/psycho modules; applied phonetics is re-covered fresh as a core subfield. Your second-language-*learning* tracks stay separate; first-language acquisition is in scope.
- **All editions and access verified September 2026.** Five citation corrections were made (Tallerman → 6th 2025; Saeed → 5th 2022; Booij → 3rd 2012 [prior "4th 2019" was an error]; Odden flagged for publisher check; SLP dated to its Jan 2025 draft). Reappraisal tags refreshed (Labov's death Dec 2024; the FOXP2 non-replication; Grambank 2023; the LLM/UG debate).

## How to use this
Each module gives: (1) goals; (2) prerequisites; (3) **PRIMARY** readings (authoritative textbooks + seminal papers, with recommended editions); (4) **SUPPLEMENTARY** (a companion, a critique, or the opposing-framework text); (5) a **moderate hands-on** component (a few Python-friendly exercises; named software like Praat where standard); (6) time estimate. **Access tags:** FREE (open/public-domain) vs. PAYWALLED. **Calibration tags:** SETTLED · CONTESTED · OPEN · HYPE-WATCH. Optional enrichment connections to your quantitative/CS background are marked **[BRIDGE]**.

**Use your languages as data.** German (V2 word order, case, umlaut), Polish and Russian (rich Slavic case + verbal aspect + consonant clusters + palatalization), and Spanish (Romance phonology, clitics, subjunctive) give you first-hand data for the morphology, phonology, syntax, and typology exercises — a real advantage most learners don't have.

**Free-resource backbone (verified licenses/hosts):**
- **Jurafsky & Martin, *Speech and Language Processing* (3rd-ed. online draft)** — web.stanford.edu/~jurafsky/slp3; free full PDF, Creative Commons; **most recent draft release January 12, 2025** (still a draft — there is no print 3rd edition). The computational/corpus spine.
- **WALS Online** (wals.info, MPI-EVA Leipzig) — free, **CC-BY 4.0**; a "finished" project, data archived at Zenodo.
- **Grambank** (grambank.clld.org, MPI-EVA / Grambank Consortium) — free, **CC-BY 4.0**; released 2023; **2,467 language varieties, 215 families + 101 isolates, 195 features, 400,000+ data points** (the largest comparative grammatical database).
- **Praat** (praat.org, Boersma & Weenink, Univ. Amsterdam) — free, open source (**GPL**); updates frequently, so cite "current version."
- **NLTK book, *Natural Language Processing with Python*** (nltk.org/book) — free, CC (Python-3/NLTK-3 edition; the Python-2 first edition is archived at nltk.org/book_1ed).
- **LingBuzz** (ling.auf.net) — free linguistics preprint archive.
- **Open-access journals:** *Glossa: a journal of general linguistics* (Open Library of Humanities; **CC-BY, no author fees**) and *Semantics & Pragmatics* (semprag.org, LSA; **diamond OA — no fees of any kind**).
- **The IPA chart** (internationalphoneticassociation.org) — free (**CC BY-SA**; the association's pages inconsistently cite 3.0/4.0).
- **foma** finite-state tool (github.com/mhulden/foma) — free, **Apache 2.0** (a free replacement for Xerox XFST/lexc).
- **Language Files** (Ohio State University Press, **13th ed., 2022**) — buy it (PAYWALLED) as your problem-set engine across Modules 1–8.

**Access caveats to remember:** the LSA flagship *Language* is green OA — **free only after a one-year embargo** (immediate OA costs a $400 APC); both English translations of Saussure's *Cours* remain in copyright (route to the public-domain French original); and Grice (1975) and Greenberg (1963) have **no clean licensed free copy** — cite the print originals.

**Frankfurt-area & nearby anchors (your geographic advantage):**
- **Max Planck Institute for Psycholinguistics**, Nijmegen (NL) — the world's leading psycholinguistics institute.
- **Max Planck Institute for Evolutionary Anthropology**, Leipzig — home of WALS, Grambank, and major typology work (Haspelmath).
- **Leibniz-Institut für Deutsche Sprache (IDS)**, Mannheim (near Frankfurt) — German-language research and the huge DeReKo corpus.
- **MPI for Human Cognitive and Brain Sciences**, Leipzig — neurolinguistics (Friederici).
- **Deutsche Gesellschaft für Sprachwissenschaft (DGfS)** — the national society; annual meeting.

---

## DEPENDENCY MAP (the through-lines)
- **Module 0** (foundations + math-for-linguists) comes first and frames everything.
- **The "form" core is sequential:** 1 Phonetics → 2 Phonology → 3 Morphology → 4 Syntax I → 5 Syntax II.
- **The "meaning" core:** 6 Semantics → 7 Pragmatics (both depend on 4–5 for structure).
- **8 Historical** depends on 1–3; **9 Typology** depends on 3–5 and pairs with 8.
- **10 Sociolinguistics** depends on 1–3 + basic stats; **11 Psycholinguistics** depends on 1–6.
- **12 Computational** depends on 0 (automata/logic) and pairs with 4–6 and 9.
- **Two tracks can run in parallel** once 0–3 are done: the **structural/formal track** (4–7, 12) and the **empirical/variation track** (8–11).
- **13 Capstone** integrates everything.

---

### MODULE 0 — Foundations & the Shape of the Field
**Goals:** Understand linguistics as *descriptive*, not prescriptive; know Hockett's design features; internalize the core dualities (synchrony/diachrony; Saussure's *langue*/*parole* and the sign; Chomsky's competence/performance; form vs. function); grasp the generative revolution and the functionalist counter-tradition; hold an even-handed map of the theoretical landscape; refresh the math/logic linguists use.
**Prerequisites:** None.
**PRIMARY:**
- Ferdinand de Saussure, *Course in General Linguistics* (1916) — read the Introduction and Part I. The **French original is public domain**; **both** English translations (Wade Baskin 1959, Columbia UP reissue 2011; Roy Harris 1983/1986, Duckworth/Open Court) remain **in copyright** — for a free text, use the French *Cours*. Translations PAYWALLED.
- Charles F. Hockett, "The Origin of Speech" (*Scientific American*, 1960) — the design features. PAYWALLED (widely anthologized).
- Noam Chomsky, *Syntactic Structures* (1957; 2nd ed. 2002 w/ Lightfoot intro, Mouton) — Chs. 1–6; and the review of B. F. Skinner's *Verbal Behavior* (*Language* 35, 1959) — SELECTIONS. Review free (green) via Southampton Cogprints; authoritative version PAYWALLED (JSTOR).
- Barbara H. Partee, Alice ter Meulen & Robert E. Wall, *Mathematical Methods in Linguistics* (Kluwer/Springer, 1990) — SELECTIONS (sets, relations, functions, logic, finite automata). PAYWALLED.
**SUPPLEMENTARY:** Frederick J. Newmeyer, *Language Form and Language Function* (MIT Press, 1998) — the balanced treatment of the formalism/functionalism split; framing chapters now, revisit after Module 5.
**Hands-on:** (1) Brief distinguishing prescriptive vs. descriptive claims (German/English examples). (2) A positive and a borderline example for each Hockett design feature. (3) [BRIDGE] Sketch the Chomsky hierarchy and predict where natural language sits (confirmed in Module 12).
**Calibration:** Competence/performance and *langue*/*parole* = SETTLED as framing (what belongs on each side is CONTESTED). Structuralism as *the* theory = superseded; its concepts (phoneme, paradigm) are permanent.
**Time:** 3 weeks.

---

### MODULE 1 — Phonetics (re-covered fresh as a core subfield)
**Goals:** Command articulatory, acoustic, and auditory phonetics; transcribe in the IPA; read spectrograms and identify formants; understand the source-filter model; use Praat; appreciate cross-linguistic phonetic diversity.
**Prerequisites:** Module 0.
**PRIMARY:**
- Peter Ladefoged & Keith Johnson, *A Course in Phonetics* (**7th ed., Cengage, 2014 — current, no newer edition**) — read fully; do the exercises. PAYWALLED.
- Keith Johnson, *Acoustic and Auditory Phonetics* (3rd ed., Wiley-Blackwell, 2011) — the acoustics chapters. **[BRIDGE — load-bearing]** voiced speech = a glottal source shaped by vocal-tract resonances (formants); a spectrogram is a short-time Fourier transform. With your DSP/librosa background this is your fastest module. PAYWALLED.
- Peter Ladefoged & Ian Maddieson, *The Sounds of the World's Languages* (Blackwell, 1996 — still the standard) — SELECTIONS. PAYWALLED.
**SUPPLEMENTARY:** the IPA Handbook / chart (free chart at internationalphoneticassociation.org).
**Hands-on:** (1) Transcribe 30 words each from English, German, Spanish, and Polish in IPA; check against a pronouncing dictionary. (2) In **Praat** (or `parselmouth`/`librosa` in Python) measure F1/F2 for your own vowels across the four languages; plot the vowel space. (3) [BRIDGE] Compute a spectrogram with `librosa`; annotate formant tracks and a stop burst/VOT.
**Calibration:** The IPA and the articulatory/acoustic framework = SETTLED. The exact universal feature inventory = CONTESTED (Module 2). Categorical perception = SETTLED-with-nuance.
**Time:** 5 weeks.

---

### MODULE 2 — Phonology (even-handed across frameworks)
**Goals:** Analyze phoneme/allophone systems; use distinctive features; write and evaluate phonological rules (SPE) *and* constraint rankings (OT) *and* understand usage-based/exemplar alternatives; handle syllable structure, stress, tone; grasp autosegmental and prosodic phonology.
**Prerequisites:** Module 1.
**PRIMARY:**
- Bruce Hayes, *Introductory Phonology* (Wiley-Blackwell, 2009) — the main text; problem-driven. PAYWALLED.
- David Odden, *Introducing Phonology* (Cambridge) — **use the current edition: 1st (2005), 2nd (2013); a revised edition is advertised by Cambridge — verify the latest printing before buying** (I could not confirm a distinct "3rd ed. 2020" this pass). PAYWALLED.
- Noam Chomsky & Morris Halle, *The Sound Pattern of English* (SPE) (Harper & Row, 1968; MIT reprint) — SELECTIONS (the rule formalism and features), as the historical foundation. PAYWALLED.
- Alan Prince & Paul Smolensky, *Optimality Theory: Constraint Interaction in Generative Grammar* (1993 ms.; Blackwell, 2004) — SELECTIONS; pair with René Kager, *Optimality Theory* (Cambridge, 1999) as the teachable OT textbook. **[BRIDGE]** OT is a constraint-optimization system — natural for someone who knows optimization/constraint satisfaction. PAYWALLED.
**SUPPLEMENTARY / usage-based counterpoint:** Janet Pierrehumbert's exemplar-theoretic / Laboratory Phonology work (e.g., "Exemplar dynamics," 2001) — the frequency-and-use alternative. Mixed access.
**Hands-on:** (1) Full phoneme analysis (complementary distribution, minimal pairs) on Polish or Russian palatalization. (2) Write SPE-style rules for German final devoicing and Polish voicing assimilation; re-analyze one as an OT tableau. (3) [BRIDGE] Implement a tiny OT evaluator in Python.
**Calibration:** Phoneme/allophone and features = SETTLED. **OT = a major but CONTESTED framework** (dominant from the mid-1990s; rule-based and exemplar/usage-based approaches persist; opacity is a known problem). The universal feature set = CONTESTED.
**Time:** 5 weeks.

---

### MODULE 3 — Morphology (even-handed; Slavic/Germanic data)
**Goals:** Segment morphemes; distinguish inflection vs. derivation; place languages on the morphological-typology cline; analyze word-formation and productivity; compare item-and-arrangement, item-and-process, and word-and-paradigm models; build a finite-state analyzer.
**Prerequisites:** Modules 1–2.
**PRIMARY:**
- Martin Haspelmath & Andrea D. Sims, *Understanding Morphology* (2nd ed., Hodder/Routledge, 2010) — typologically informed and framework-fair. PAYWALLED.
- Geert Booij, ***The Grammar of Words* (3rd ed., Oxford, 2012)** — SELECTIONS. *(Note: this is the current edition; an earlier draft of this curriculum listed a nonexistent "4th ed. 2019" — that year belongs to Booij's separate* Morphology of Dutch*, 2nd ed.)* PAYWALLED.
- Kenneth R. Beesley & Lauri Karttunen, *Finite State Morphology* (CSLI, 2003) — SELECTIONS. **[BRIDGE — load-bearing]** morphology as regular relations via finite-state transducers; the free **foma** tool (Apache 2.0) or Python `pyfoma`/`hfst` realizes this. Book PAYWALLED; foma FREE.
**SUPPLEMENTARY:** Mark Aronoff & Kirsten Fudeman, *What Is Morphology?* (2nd ed., Wiley-Blackwell) as a gentler companion.
**Hands-on:** (1) Full morphological analysis of the Polish or Russian nominal case paradigm (stems, endings, syncretism); same for German strong/weak verbs. (2) [BRIDGE] Build a finite-state analyzer in **foma** for a fragment of Spanish verb conjugation or Polish noun declension. (3) Compute a hapax-based productivity measure (Baayen's P) for a derivational affix.
**Calibration:** Inflection/derivation and typological distinctions = SETTLED-as-useful (fuzzy boundaries). Which model (IA/IP/WP) is "correct" = CONTESTED; word-and-paradigm/realizational approaches have gained ground for fusional languages.
**Time:** 4 weeks.

---

### MODULE 4 — Syntax I: The Data and Descriptive Tools (theory-neutral)
**Goals:** Establish constituency (and the tests for it), syntactic categories, grammatical relations, argument structure, cross-linguistic word order; draw and defend trees — before committing to a framework.
**Prerequisites:** Module 3.
**PRIMARY:**
- Maggie Tallerman, ***Understanding Syntax* (6th ed., Routledge, 2025; ISBN 978-1-032-62955-1)** — the theory-neutral, typologically grounded foundation; read fully. *(Updated from the 5th ed.)* PAYWALLED.
**SUPPLEMENTARY:** the syntax chapters of *Language Files* (13th ed., 2022) for extra problem sets.
**Hands-on:** (1) Apply constituency tests (movement, substitution, coordination, clefting) to German and Spanish sentences; note where German V2 complicates the picture. (2) Classify five of your languages/dialects by basic word order and identify correlated features (a preview of typology). (3) Draw trees for English/German sentences and argue PP attachment.
**Calibration:** Constituency and grammatical relations = SETTLED as descriptive tools (their theoretical status differs sharply across frameworks — Module 5).
**Time:** 4 weeks.

---

### MODULE 5 — Syntax II: The Frameworks (EVEN-HANDED — the crux)
**Goals:** Understand and *use* the three major traditions and articulate the debate: (a) generative (X-bar → Government & Binding → the Minimalist Program); (b) constraint-based/non-transformational (HPSG, LFG); (c) functional/cognitive (Role and Reference Grammar; Construction Grammar).
**Prerequisites:** Module 4.
**PRIMARY:**
- **Generative:** Andrew Carnie, *Syntax: A Generative Introduction* (**4th ed., Wiley-Blackwell, 2021 — current**) — X-bar/GB core; David Adger, *Core Syntax* (Oxford, 2003) for the Minimalist Program. Chomsky primaries: *Syntactic Structures* (1957) and SELECTIONS of *Aspects of the Theory of Syntax* (1965). PAYWALLED.
- **Constraint-based:** Ivan A. Sag, Thomas Wasow & Emily M. Bender, *Syntactic Theory: A Formal Introduction* (2nd ed., CSLI, 2003) — HPSG; rigorous and computationally friendly. PAYWALLED.
- **Functional/cognitive:** Robert D. Van Valin Jr., *An Introduction to Syntax* (Cambridge, 2001) or *Exploring the Syntax–Semantics Interface* (2005) for Role and Reference Grammar; Talmy Givón, *Syntax: An Introduction* (Benjamins, 2001); Adele E. Goldberg, *Constructions* (Chicago, 1995) and *Constructions at Work* (Oxford, 2006) for Construction Grammar. PAYWALLED.
**SUPPLEMENTARY / the debate:** Frederick Newmeyer, *Language Form and Language Function* (1998), read in full.
**Hands-on:** (1) Analyze the *same* three sentences (one English, one German with V2, one with a long-distance dependency) in a generative tree, an HPSG feature structure, and a construction-grammar analysis; write a page on what each captures and misses. (2) [BRIDGE] Implement a small context-free grammar + CKY parser in Python for a fragment of English (following Jurafsky & Martin's CFG chapter). (3) Take one construction (the English ditransitive, or a German equivalent) and lay out the generative vs. constructionist accounts.
**Calibration:** **Syntax is the field's most genuinely split area — still CONTESTED as of 2025.** The Minimalist Program is the dominant *generative* paradigm, but HPSG/LFG and Construction Grammar/usage-based approaches are serious, active rivals (see e.g. *A Companion to Chomsky*, 2021; Müller's *Grammatical Theory*). Transformational movement itself is CONTESTED (constraint-based frameworks reject it). The innate-UG assumptions underlying Minimalism = CONTESTED (Module 11), now overlaid by the LLM debate (Module 12).
**Time:** 6–7 weeks (the heaviest module).

---

### MODULE 6 — Semantics (EVEN-HANDED: two traditions side by side)
**Goals:** Do truth-conditional/compositional (formal) semantics — model theory, compositionality, the lambda calculus, Montague grammar — *and* understand cognitive/lexical semantics — frames, prototypes, conceptual metaphor. Compute simple meanings; read both literatures.
**Prerequisites:** Modules 4–5; Module 0's logic primer.
**PRIMARY:**
- **Formal:** Irene Heim & Angelika Kratzer, *Semantics in Generative Grammar* (Blackwell, 1998) — the standard formal text; **[BRIDGE — load-bearing]** meanings as typed lambda terms composed by function application — exactly the type-theory/lambda-calculus you know. Pair with L. T. F. Gamut, *Logic, Language, and Meaning* (2 vols., Chicago, 1991). PAYWALLED.
- **Broad survey (both traditions):** John I. Saeed, ***Semantics* (5th ed., Wiley-Blackwell, 2022/©2023; ISBN 978-1-119-70985-5)** — read fully; the most even-handed single text. *(Updated from the 4th ed.)* PAYWALLED.
- **Cognitive/lexical:** George Lakoff, *Women, Fire, and Dangerous Things* (Chicago, 1987) — SELECTIONS; Ronald Langacker's Cognitive Grammar (via Croft & Cruse); William Croft & D. Alan Cruse, *Cognitive Linguistics* (Cambridge, 2004); D. A. Cruse, *Lexical Semantics* (Cambridge, 1986) — SELECTIONS. PAYWALLED.
**SUPPLEMENTARY:** Kate Kearns, *Semantics* (Palgrave) as an accessible formal companion.
**Hands-on:** (1) Give lambda-calculus denotations for a small fragment (determiners, transitive verbs, quantifiers) and compute truth conditions for five sentences by hand. (2) [BRIDGE] Do the same in Python with **NLTK's semantics** (`nltk.sem`), or implement a tiny compositional evaluator over a toy model. (3) Analyze one polysemous word (Polish *zamek* 'castle/lock/zipper', or English *over*) in prototype/frame terms; contrast with a formal lexical entry.
**Calibration:** Compositionality as a working principle = SETTLED (its exact scope CONTESTED). Formal vs. cognitive semantics = two live, partly complementary traditions. Conceptual Metaphor Theory (Lakoff & Johnson) = influential but CONTESTED on its strong claims and testability.
**Time:** 6 weeks.

---

### MODULE 7 — Pragmatics
**Goals:** Handle deixis; speech act theory; Gricean implicature and the maxims; presupposition; relevance theory; the semantics/pragmatics boundary.
**Prerequisites:** Module 6.
**PRIMARY:**
- Stephen C. Levinson, *Pragmatics* (Cambridge, 1983) — the classic; read fully. PAYWALLED. (Modern companion: Yan Huang, *Pragmatics*, **2nd ed., Oxford, 2014 — current, no 3rd edition**.)
- H. P. Grice, "Logic and Conversation" (1975, in *Syntax and Semantics* 3, pp. 41–58; repr. in *Studies in the Way of Words*, 1989) — read in full. **No clean licensed free copy — cite the print original** (course-page PDFs exist but aren't authoritative). PAYWALLED.
- J. L. Austin, *How to Do Things with Words* (2nd ed., Oxford, 1975) — SELECTIONS; John R. Searle, *Speech Acts* (Cambridge, 1969) — SELECTIONS. PAYWALLED.
- Dan Sperber & Deirdre Wilson, *Relevance: Communication and Cognition* (2nd ed., Blackwell, 1995) — SELECTIONS. PAYWALLED.
**SUPPLEMENTARY:** Laurence Horn & Gregory Ward (eds.), *The Handbook of Pragmatics* (Blackwell, 2004) — reference.
**Hands-on:** (1) Collect ten real utterances (chat logs, ads, dialogue) and analyze the implicatures, specifying which maxim is exploited. (2) Presupposition-projection analysis of sentences with definite descriptions and factive verbs. (3) Contrast Gricean vs. relevance-theoretic accounts of one indirect speech act across English/German/Polish (politeness differences make this vivid).
**Calibration:** Gricean implicature and speech-act theory = SETTLED foundations. The exact semantics/pragmatics division of labor = OPEN/CONTESTED. Politeness theory (Brown & Levinson) = influential but CONTESTED cross-culturally.
**Time:** 4 weeks.

---

### MODULE 8 — Historical & Comparative Linguistics (hands-on comparative method)
**Goals:** Understand sound change and the Neogrammarian regularity principle; *do* the comparative method and reconstruction; handle analogy and grammaticalization; know how language families are established; understand the limits of reconstruction and why long-range proposals fail.
**Prerequisites:** Modules 1–3.
**PRIMARY:**
- Lyle Campbell, *Historical Linguistics: An Introduction* (**4th ed., Edinburgh UP 2020 / MIT Press 2021 — current**) — the standard, richly exercised; read fully. PAYWALLED.
- Hans Henrich Hock & Brian D. Joseph, *Language History, Language Change, and Language Relationship* (3rd ed., De Gruyter Mouton, 2019) — SELECTIONS. PAYWALLED.
- Paul J. Hopper & Elizabeth Closs Traugott, *Grammaticalization* (2nd ed., Cambridge, 2003) — SELECTIONS. PAYWALLED.
**SUPPLEMENTARY:** on the macro-family controversies, read Campbell's own critiques of Greenberg's mass comparison and Nostratic.
**Hands-on:** (1) Comparative-method reconstruction from a supplied cognate set (Romance or Slavic is ideal — you can build your own Spanish/other-Romance set) to a proto-form, stating the regular correspondences. (2) Trace one grammaticalization path (e.g., a future auxiliary from a motion/volition verb) across your languages. (3) [BRIDGE] Explore an automated cognate-detection or phylogenetic tool (e.g., LingPy in Python) and critique it against the manual method.
**Calibration:** The comparative method = SETTLED (bedrock). Neogrammarian regularity of sound change = SETTLED, with **lexical diffusion as a CONTESTED qualification**. Grammaticalization *unidirectionality* = CONTESTED. **Long-range macro-families and "mass comparison" (Greenberg's Amerind; Nostratic; Proto-World) = HYPE-WATCH/rejected by the mainstream.** Computational phylogenetics = promising but CONTESTED in its deeper claims (e.g., dating).
**Time:** 5 weeks.

---

### MODULE 9 — Linguistic Typology & Universals (hands-on with WALS/Grambank)
**Goals:** Read and use implicational universals; analyze word-order and morphological typology; understand markedness; mine the great typological databases; engage the universals-vs-diversity debate even-handedly.
**Prerequisites:** Modules 3–5; pairs with 8.
**PRIMARY:**
- Bernard Comrie, *Language Universals and Linguistic Typology* (2nd ed., Chicago, 1989 — still standard) — read fully. PAYWALLED.
- William Croft, *Typology and Universals* (2nd ed., Cambridge, 2003 — still standard) — SELECTIONS. PAYWALLED.
- Joseph H. Greenberg, "Some Universals of Grammar with Particular Reference to the Order of Meaningful Elements" (1963, in *Universals of Language*, MIT Press, pp. 73–113) — read in full. **No clean licensed free copy — cite the print original.** PAYWALLED.
- **WALS Online** (wals.info, CC-BY 4.0) and **Grambank** (grambank.clld.org, CC-BY 4.0) — the databases. **FREE.**
- **REQUIRED even-handed debate reading:** Nicholas Evans & Stephen C. Levinson, "The myth of language universals: Language diversity and its importance for cognitive science," *Behavioral and Brain Sciences* 32(5), 2009, pp. 429–448 (DOI 10.1017/S0140525X0999094X) — target article + skim the commentaries and response. Free (green) via ANU/author self-archiving; authoritative version PAYWALLED (Cambridge Core).
**SUPPLEMENTARY:** Jae Jung Song (ed.), *The Oxford Handbook of Linguistic Typology* — reference. And the new large-scale evidence: **Hedvig Skirgård et al., "Grambank reveals the importance of genealogical constraints on linguistic diversity and highlights the impact of language loss," *Science Advances* 9(16):eadg6175 (2023, CC-BY)** — the field's largest structural database, showing diversity is shaped strongly by genealogical inheritance alongside contact, that grammatical evolution is measurably constrained, and that language endangerment threatens severe loss of structural diversity.
**Hands-on:** (1) [BRIDGE] Download WALS/Grambank as CSV; in pandas, test a Greenbergian implicational universal (e.g., OV ⊃ postpositions) and quantify exceptions; map a feature. (2) Compute a simple areal/genealogical control and note "Galton's problem" (non-independence of related languages) — the very issue Skirgård et al. formalize. (3) Place your four languages on a set of WALS/Grambank features and write up where they cluster.
**Calibration:** Greenbergian implicational universals = SETTLED as robust *statistical tendencies* but **CONTESTED as exceptionless "universals"** (Evans & Levinson). Markedness = SETTLED-as-useful but theoretically CONTESTED. The universals-vs-diversity question = OPEN and alive — with Grambank (2023) shifting the framing toward how much of diversity is constrained by descent vs. free variation.
**Time:** 4 weeks.

---

### MODULE 10 — Sociolinguistics (re-covers the ling-anthropology overlap; hands-on regression)
**Goals:** Master the variationist paradigm and its quantitative methods; understand change in progress and social meaning; know dialectology, multilingualism, and contact; and — re-covered here from the linguistics angle — language ideology, the ethnography of communication, and linguistic relativity with modern evidence.
**Prerequisites:** Modules 1–3; basic regression (you have this).
**PRIMARY:**
- William Labov, *Sociolinguistic Patterns* (Penn, 1972) — SELECTIONS (the department-store study; the observer's paradox; the linguistic variable). *(Labov, the founder of variationist sociolinguistics, died 17 December 2024, aged 97.)* PAYWALLED.
- Sali A. Tagliamonte, *Analysing Sociolinguistic Variation* (Cambridge, 2006) and/or *Variationist Sociolinguistics: Change, Observation, Interpretation* (Wiley-Blackwell, 2012) — the methods; **[BRIDGE]** variation modeled with logistic/mixed-effects regression (Rbrul/`lme4`; portable to Python `statsmodels`/`bambi`). PAYWALLED.
- Penelope Eckert, "Three Waves of Variation Study: The Emergence of Meaning in the Study of Sociolinguistic Variation," *Annual Review of Anthropology* 41 (2012) — read in full. PAYWALLED.
- **Re-covered ling-anthropology material:** Dell Hymes, "Models of the Interaction of Language and Social Life" (1972) — the ethnography of communication and the SPEAKING model; plus a language-ideology reading (Michael Silverstein or Kathryn Woolard's overview). SELECTIONS. PAYWALLED.
- **Re-covered linguistic relativity, with modern experimental evidence:** Brent Berlin & Paul Kay, *Basic Color Terms* (UC Press, 1969) and the World Color Survey (Kay & Regier 2003, *PNAS* 100:9085–9089); experimental work by Lera Boroditsky (space, time, grammatical gender) and Gary Lupyan; Winawer et al. (2007, "Russian blues," *PNAS*). SELECTIONS. Mixed access.
**SUPPLEMENTARY:** Miriam Meyerhoff, *Introducing Sociolinguistics* (**3rd ed., Routledge, 2018 — current, no 4th edition**) as the connective textbook. On the relativity synthesis: Wolff & Holmes, "Linguistic relativity," *WIREs Cognitive Science* 2(3):253–265 (2011).
**Hands-on:** (1) [BRIDGE] Take a variationist dataset (or build one from a small speech corpus) and fit a mixed-effects logistic model of a variable (e.g., (ing), or a German/Polish variable), interpreting the social and linguistic constraints. (2) Mini ethnography-of-communication analysis of one speech event with Hymes's SPEAKING grid. (3) Design (on paper) a replication of one Boroditsky relativity experiment and state what result would support *weak* vs. *strong* relativity.
**Calibration:** The variationist method = SETTLED. **Strong linguistic relativity (Whorfian determinism) = rejected/HYPE-WATCH; weak relativity = SETTLED-with-support** in specific domains (color, spatial frames, grammatical gender, time), though effect sizes are modest and sometimes fragile (Wolff & Holmes 2011). **Color universals and weak relativity are now seen as compatible:** the World Color Survey confirmed robust universal naming tendencies (Kay & Regier), while boundary effects on memory/discrimination (Kay & Kempton 1984; Winawer et al. 2007) preserve a role for relativity. Berlin & Kay's strong universalist claim = SETTLED-with-significant-revisions. Eckert's "third wave" (social meaning/indexicality) = increasingly SETTLED as a paradigm.
**Time:** 5 weeks.

---

### MODULE 11 — Psycholinguistics, First-Language Acquisition & Neurolinguistics (EVEN-HANDED on acquisition)
**Goals:** Understand speech perception/production, lexical access, and sentence processing (garden paths, self-paced reading, the N400/P600 ERPs, eye-tracking); engage the nativism-vs-usage-based debate on first-language acquisition even-handedly; know the basics of bilingualism and neurolinguistics.
**Prerequisites:** Modules 1–6.
**PRIMARY:**
- Eva M. Fernández & Helen Smith Cairns, *Fundamentals of Psycholinguistics* (Wiley-Blackwell, 2011) — the main text (or Trevor A. Harley, *The Psychology of Language*, **4th ed., 2014, Psychology Press/Routledge — current**). PAYWALLED.
- **The acquisition debate, both sides:** Steven Pinker, *The Language Instinct* (1994) and María Teresa Guasti, *Language Acquisition: The Growth of Grammar* (2nd ed., MIT, 2016) for the nativist/UG account (poverty of the stimulus); **versus** Michael Tomasello, *Constructing a Language: A Usage-Based Theory of Language Acquisition* (Harvard, 2003) for the usage-based/constructivist account. Framing chapters of each. PAYWALLED.
- Sentence-processing and ERP primaries: Kutas & Hillyard (1980) on the N400; Osterhout & Holcomb (1992) on the P600 — SELECTIONS. PAYWALLED.
**SUPPLEMENTARY:** Angela D. Friederici, *Language in Our Brain* (MIT, 2017) — the neurolinguistic language network. PAYWALLED.
**Hands-on:** (1) Analyze a self-paced reading or eye-tracking dataset (several are open) in Python: compute reading-time effects for a garden-path manipulation. (2) Read one poverty-of-the-stimulus argument and one usage-based rebuttal; write a two-page even-handed adjudication — and note explicitly how LLMs learning syntax from data bear on it (Module 12). (3) Sketch the classical language network (Broca/Wernicke) and one modern revision.
**Calibration:** **Universal Grammar / an innate language-specific faculty / poverty of the stimulus = CONTESTED** — a central, polarizing, live debate, now reignited by large language models (Module 12). Strong claims of a rich innate UG lean HYPE-WATCH; strong claims that LLMs "refute UG" are also premature. The N400/P600 findings = SETTLED (robust); their interpretation is CONTESTED but converging — recent work increasingly supports a Retrieval–Integration split (N400 = lexical retrieval, P600 = integration effort; Brouwer et al. 2017; Aurnhammer et al. 2021–2023), though no full consensus. The classical Broca/Wernicke localization = SETTLED-but-substantially-revised. **"FOXP2 = the language gene / a recent human selective sweep" = HYPE-WATCH:** Atkinson et al. (2018, *Cell* 174(6):1424–1435) found the earlier sweep signal (Enard et al. 2002) did not replicate once African and non-African samples were separated — it was an artifact of sample composition. (FOXP2's *functional* role in speech is not disputed, and newer methods still flag it as a candidate for older/subtler selection — so frame carefully rather than as "not a language gene.") Pinker's strong "language instinct" framing = CONTESTED.
**Time:** 5 weeks.

---

### MODULE 12 — Computational & Corpus Linguistics (light/moderate survey, leveraging your skills)
**Goals:** Understand formal-language theory and where natural language sits in the Chomsky hierarchy; use finite-state and corpus methods; grasp information-theoretic linguistics; think clearly about what modern NLP/LLMs do and don't tell us about linguistic theory.
**Prerequisites:** Module 0 (automata/logic); pairs with 4–6, 9.
**PRIMARY:**
- Dan Jurafsky & James H. Martin, *Speech and Language Processing* (3rd-ed. online draft) — **FREE** (web.stanford.edu/~jurafsky/slp3; latest draft release **January 12, 2025** — still a draft, no print 3rd edition). Read the chapters on regular expressions/FSAs, context-free grammars and parsing, and language modeling. **[BRIDGE]** squarely your territory.
- Stuart M. Shieber, "Evidence against the context-freeness of natural language," *Linguistics and Philosophy* 8(3), 1985, pp. 333–343 (DOI 10.1007/BF00630917) — read in full (the Swiss-German cross-serial-dependency argument; why natural language is *mildly context-sensitive*). Free (green) via Harvard DASH; authoritative version PAYWALLED (Springer). Pair with a brief note on Aravind Joshi's Tree-Adjoining Grammar (TAG).
- Corpus/quantitative: Steven Bird, Ewan Klein & Edward Loper, *Natural Language Processing with Python* (the NLTK book) — **FREE** (nltk.org/book), SELECTIONS.
**SUPPLEMENTARY:** on information-theoretic linguistics — George K. Zipf, *Human Behavior and the Principle of Least Effort* (1949) for Zipf's law, and the Uniform Information Density hypothesis (Levy & Jaeger 2007; Jaeger 2010). **[BRIDGE — load-bearing]** entropy, surprisal, and channel-capacity reasoning applied to language.
**Hands-on:** (1) [BRIDGE] Verify Zipf's law on a corpus of each of your languages; compare exponents. (2) Build a concordancer + collocation extractor (PMI/log-likelihood) in Python (NLTK/spaCy); analyze a keyword. (3) [BRIDGE] Compute per-word surprisal from an n-gram or small neural LM and test a Uniform-Information-Density prediction (e.g., optional-*that* omission). (4) Implement a CKY parser (if not done in Module 5) and parse with a small CFG.
**Calibration:** **Natural language is mildly context-sensitive (not context-free) = SETTLED** (Shieber 1985). Zipf's law = SETTLED empirically (its deep explanation CONTESTED). The Uniform Information Density hypothesis = CONTESTED/OPEN (growing but debated support). **What LLMs imply for linguistic theory = OPEN and actively contested.** The live exchange: Steven Piantadosi, "Modern language models refute Chomsky's approach to language" (2024, in *From fieldwork to linguistic theory*, eds. Gibson & Poliak, Language Science Press, pp. 353–414; first circulated 2023) vs. rebuttals — Roni Katzir, "Why Large Language Models Are Poor Theories of Human Linguistic Cognition" (*Biolinguistics* 17, 2023) and Kodner, Payne & Heinz (2023); and Chomsky, Roberts & Watumull, "The False Promise of ChatGPT" (*New York Times* op-ed, 8 March 2023). Controlled evidence: Kallini et al., "Mission: Impossible Language Models" (ACL 2024, Best Paper) found GPT-2 learns attested-type languages better than systematically "impossible" ones — but Hunter (2025, *Computational Linguistics* 51(2):641–650) argues a design confound. **Treat strong claims in either direction skeptically.**
**Time:** 4 weeks.

---

### MODULE 13 — Capstone & the Literature
**Goals:** Integrate the subfields on one substantial project; learn to read the primary journals.
**Prerequisites:** All prior modules (or the Fast-Path).
**Capstone options (pick one, ~6–8 weeks):**
- **A.** A descriptive sketch of a language you know well (Polish or Russian recommended): phoneme inventory + key phonological processes + a morphology fragment (a finite-state analyzer) + a short syntax section — a mini reference grammar.
- **B.** A variationist study: collect/borrow a small speech corpus and model one variable with mixed-effects regression, written to journal norms.
- **C.** A formal-semantics fragment: implement a compositional semantics for a slice of one language in Python and test it against truth-conditional judgments.
- **D.** A typological analysis: pose a hypothesis, test it against WALS/Grambank in pandas with areal/genealogical controls, and write it up.
**Reading the literature:** general — *Language* (LSA; **free after a 1-year embargo**), *Journal of Linguistics*; syntax/formal — *Linguistic Inquiry*, *Natural Language & Linguistic Theory*, and the open-access *Glossa*; phonology — *Phonology*; semantics — *Journal of Semantics*, *Semantics and Pragmatics* (diamond OA); pragmatics — *Journal of Pragmatics*; sociolinguistics — *Language Variation and Change*, *Journal of Sociolinguistics*; psycholinguistics — *Journal of Memory and Language*, *Cognition*; typology — *Linguistic Typology*. Set up alerts; many authors post preprints on **LingBuzz** (ling.auf.net) — FREE.
**Frankfurt-area anchors:** follow MPI Nijmegen and MPI-EVA Leipzig outputs; use IDS Mannheim's DeReKo for German corpus work; attend a DGfS meeting.
**Time:** 6–8 weeks.

---

## MVP Fast-Path (compressed core-subfield spine, ~5–6 months part-time)
For a solid working command of the core fast: **Module 0 → 1 (Phonetics) → 2 (Phonology) → 3 (Morphology) → 4 (Syntax I) → 6 (Semantics, formal + Saeed's cognitive chapters) → 7 (Pragmatics) → 9 (Typology, incl. Evans & Levinson)**, skimming Module 5's three frameworks via Tallerman + Carnie's opening chapters + one Construction-Grammar chapter.
- Anchor texts: *Language Files* (13th, 2022; the exercise spine) + Tallerman (6th, 2025) + Hayes (phonology) + Haspelmath & Sims (morphology) + Saeed (5th, 2022; semantics) + Levinson (pragmatics).
- Anchor papers: Hockett (1960); Greenberg (1963); Grice (1975); Evans & Levinson (2009); Shieber (1985).
- Deliverable: a phoneme analysis + a finite-state morphology fragment + a compositional-semantics mini-exercise, all on a language you know.

## Full Arc (~2 years part-time, ~8–10 hrs/week)
- **Months 1–3:** Module 0 + 1 (Phonetics).
- **Months 4–7:** 2 (Phonology) + 3 (Morphology).
- **Months 8–12:** 4 + 5 (Syntax — the heavy stretch).
- **Months 13–16:** 6 (Semantics) + 7 (Pragmatics).
- **Months 17–20:** two parallel tracks — 8 (Historical) + 9 (Typology) alongside 10 (Sociolinguistics) + 11 (Psycholinguistics).
- **Months 21–24:** 12 (Computational) + 13 (Capstone).
Total ≈ 22–24 months with buffer.

---

## Verified Editions & Access — Quick Reference (September 2026)

| Work | Recommended edition | Free? | Free host / caveat |
|---|---|---|---|
| Ladefoged & Johnson, *A Course in Phonetics* | 7th, 2014, Cengage (current) | No | — |
| Keith Johnson, *Acoustic and Auditory Phonetics* | 3rd, 2011, Wiley-Blackwell | No | — |
| Ladefoged & Maddieson, *Sounds of the World's Languages* | 1996, Blackwell (standard) | No | — |
| Hayes, *Introductory Phonology* | 2009, Wiley-Blackwell | No | — |
| Odden, *Introducing Phonology* | **2nd, 2013, Cambridge (verify latest printing)** | No | revised ed. advertised — confirm on publisher page |
| Prince & Smolensky, *Optimality Theory* | 2004, Blackwell | No | — |
| Kager, *Optimality Theory* | 1999, Cambridge | No | — |
| Haspelmath & Sims, *Understanding Morphology* | 2nd, 2010, Routledge | No | — |
| Booij, *The Grammar of Words* | **3rd, 2012, Oxford** (not "4th 2019") | No | — |
| Tallerman, *Understanding Syntax* | **6th, 2025, Routledge (ISBN 978-1-032-62955-1)** | No | — |
| Carnie, *Syntax: A Generative Introduction* | 4th, 2021, Wiley-Blackwell | No | — |
| Adger, *Core Syntax* | 2003, Oxford | No | — |
| Sag, Wasow & Bender, *Syntactic Theory* | 2nd, 2003, CSLI | No | — |
| Heim & Kratzer, *Semantics in Generative Grammar* | 1998, Blackwell | No | — |
| Saeed, *Semantics* | **5th, 2022/©2023, Wiley-Blackwell (ISBN 978-1-119-70985-5)** | No | — |
| Gamut, *Logic, Language, and Meaning* | 1991, Chicago (2 vols.) | No | — |
| Partee, ter Meulen & Wall, *Mathematical Methods in Linguistics* | 1990, Kluwer | No | — |
| Levinson, *Pragmatics* | 1983, Cambridge | No | — |
| Yan Huang, *Pragmatics* | 2nd, 2014, Oxford (current) | No | — |
| Campbell, *Historical Linguistics: An Introduction* | 4th, 2020 Edinburgh / 2021 MIT | No | — |
| Hock & Joseph, *Language History…* | 3rd, 2019, De Gruyter Mouton | No | — |
| Comrie, *Language Universals and Linguistic Typology* | 2nd, 1989, Chicago (standard) | No | — |
| Croft, *Typology and Universals* | 2nd, 2003, Cambridge (standard) | No | — |
| Fernández & Cairns, *Fundamentals of Psycholinguistics* | 2011, Wiley-Blackwell | No | — |
| Harley, *The Psychology of Language* | 4th, 2014, Psychology Press (current) | No | — |
| Guasti, *Language Acquisition* | 2nd, 2016, MIT | No | — |
| Tomasello, *Constructing a Language* | 2003, Harvard | No | — |
| Meyerhoff, *Introducing Sociolinguistics* | 3rd, 2018, Routledge (current) | No | — |
| Tagliamonte, *Variationist Sociolinguistics* | 2012, Wiley-Blackwell | No | — |
| *Language Files* | 13th, 2022, OSU Press | No | — |
| Jurafsky & Martin, *Speech and Language Processing* | 3rd-ed. draft (rel. Jan 12, 2025) | **Yes** | web.stanford.edu/~jurafsky/slp3 (draft) |
| WALS Online | — | **Yes** | wals.info — CC-BY 4.0 |
| Grambank | — | **Yes** | grambank.clld.org — CC-BY 4.0 |
| Praat | current version | **Yes** | praat.org — GPL |
| NLTK book | Python-3 ed. | **Yes** | nltk.org/book |
| *Glossa* | — | **Yes** | OLH — CC-BY, no fees |
| *Semantics & Pragmatics* | — | **Yes** | semprag.org — diamond OA |
| *Language* (LSA) | — | **After 1-yr embargo** | LSA green OA ($400 APC for immediate) |
| Saussure, *Cours* | French original (PD) | Français only | English translations (Baskin, Harris) in copyright |
| Sapir, *Language* (1921) | — | **Yes** | Project Gutenberg #12629 (US PD) |
| Grice (1975); Greenberg (1963) | print originals | **No clean OA** | cite print; course-page PDFs not authoritative |
| Shieber (1985) | — | **Yes (green)** | Harvard DASH (Springer paywalled) |
| Evans & Levinson (2009) | — | **Yes (green)** | ANU / author (Cambridge Core paywalled) |
| IPA chart | — | **Yes** | internationalphoneticassociation.org — CC BY-SA |
| foma | — | **Yes** | github.com/mhulden/foma — Apache 2.0 |

---

## Recommendations
1. **Buy a small set and rely on free resources for the rest:** *Language Files* (13th, 2022; your problem-set engine), one syntax pair (Tallerman 6th 2025 + Carnie 4th 2021), Hayes (phonology), and Saeed (5th, 2022; semantics). Everything computational (Jurafsky & Martin), typological (WALS/Grambank), and phonetic-analytic (Praat) is free.
2. **Front-load phonetics** — where your DSP/audio background compounds fastest, and it grounds phonology. Do the acoustic exercises in Python (`parselmouth`/`librosa`) as well as Praat.
3. **Take even-handedness seriously in Modules 5, 6, and 11.** For each contested area, state the strongest version of *both* accounts before forming a view. The field's biggest failure mode is paradigm tribalism; your outsider status is an asset.
4. **Exploit your languages and your code.** Slavic morphology (Polish/Russian) and German V2 give you data most English-only learners lack; the [BRIDGE] exercises (finite-state morphology, CKY parsing, lambda-calculus semantics, Zipf/surprisal, mixed-effects variation) turn abstract theory into things you build.
5. **Verify the one open edition question before buying phonology:** confirm on cambridge.org whether a post-2013 edition of Odden's *Introducing Phonology* exists; otherwise use the 2nd (2013). Every other edition above is locked as of September 2026.
6. **Escalation trigger:** if the formal/computational side (5, 6, 12) grips you, that's the natural on-ramp to the deeper *formal & computational linguistics* track (formal language theory, formal semantics, OT, CL/NLP) at advanced-practitioner depth — a separate build, and your day job's nearest neighbor.

## Caveats
- **Editions verified September 2026, but printings turn over.** Five corrections are baked in above (Tallerman 6th 2025; Saeed 5th 2022; Booij 3rd 2012; SLP dated to its Jan 2025 draft; Odden flagged). The frequently-updated ones to re-check at purchase are *A Course in Phonetics*, Carnie, Tallerman, Campbell, Huang, Meyerhoff, and *Language Files*. The recommended translations/classics (Heim & Kratzer, Sag-Wasow-Bender, Prince & Smolensky, Greenberg 1963, Grice 1975, Shieber 1985) are stable.
- **Odden *Introducing Phonology* is the one unresolved edition:** confirmed 1st (2005) and 2nd (2013); a revised edition is advertised by Cambridge but a distinct "3rd (2020)" could not be confirmed — verify directly before buying.
- **Access reality:** most textbooks and the top journals are paywalled. The genuinely free, first-rate resources are Jurafsky & Martin (3rd-ed. draft), WALS, Grambank, Praat, the NLTK book, LingBuzz, and the OA journals *Glossa* and *Semantics & Pragmatics*. Route around three soft spots: *Language* (1-year embargo), Saussure (use the French PD original), and Grice/Greenberg (cite print originals — no clean OA).
- **This is an intermediate broad survey, not research training.** It reads most primary works as selections and does not exhaust any subfield's frontier; the formal/computational side can be taken much deeper (a separate track).
- **Even-handedness is a design choice, not a claim that the debates are undecidable.** Where the evidence leans (mild context-sensitivity; weak but real relativity; the comparative method's validity; the rejection of mass comparison; the FOXP2 non-replication), the calibration tags say so.
- **A few reappraisal specifics rest partly on secondary summaries** (the precise N400/P600 review citations; the color-universals follow-up list). Verify against primary sources if exactitude matters for citation. Also note: the FOXP2 2018 non-replication is robust for the *recent selective-sweep* claim, but the gene's functional role in speech is undisputed and newer methods still flag it as a candidate for older selection — avoid overstating "FOXP2 is not a language gene."
- **A small number of book editions were not independently re-verified this pass** (Hayes, Kager, Prince & Smolensky, Haspelmath & Sims, Sag/Wasow/Bender, Hock & Joseph, and various classic monographs); these are long-stable, but a final spot-check at purchase is prudent.