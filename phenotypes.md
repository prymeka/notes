# A Rigorous Self-Study Curriculum: Human Phenotypic Variation and the History of Anthropological "Types" / Racial Typology

*Designed for a quantitatively sophisticated autodidact (MSc AI, BSc Physics, ML engineer). Framed as history-of-science + modern human biological variation. The typological race concept is treated as a historical, scientifically discredited paradigm; modern population genetics is taught as the legitimate replacement science.*

## TL;DR
- **The typological race concept — discrete, essential human "types" defined by clusters of phenotypic traits — is scientifically DISCREDITED, but human biological variation is real, measurable, largely CONTINUOUS/CLINAL, and structured by population history.** This curriculum teaches both the discredited paradigm (as history) and its valid replacement (population and evolutionary genetics), keeping them clearly labeled.
- **The curriculum is phased (Phase 0–6) with a compressed MVP fast-track (~30–40 hours)**, primary-source readings with full citations, free-access flags, Python/computational exercises (PCA on 1000 Genomes/HGDP, F_ST, clinal analysis), and per-phase SETTLED / CONTESTED / DISCREDITED calibration callouts.
- **Your physics/ML background is a genuine accelerator**: variance apportionment (Lewontin 1972) is an ANOVA/information-theory problem; the Lewontin–Edwards debate is literally about correlation structure and classification in high dimensions; PCA of genotypes, F_ST, and isolation-by-distance map directly onto tools you already know.

## Key Findings (orientation before you start)
- **The single most-cited empirical result:** Lewontin (1972, Table 4, p. 396) partitioned human diversity as **85.4% within populations, 8.3% among populations within a "race," and only 6.3% among races**. Rosenberg et al. (2002) corroborated with a different marker set: "Within-population differences among individuals account for 93 to 95% of genetic variation; differences among major groups constitute only 3 to 5%." This is SETTLED.
- **The most important nuance** (CONTESTED in interpretation, not in math): A.W.F. Edwards (2003) argued Lewontin's taxonomic conclusion "is unwarranted because the argument ignores the fact that most of the information that distinguishes populations is hidden in the correlation structure of the data and not simply in the variation of the individual factors." So "most variation is within groups" does NOT by itself imply you cannot statistically assign individuals to populations. Both Lewontin's and Edwards's arithmetic are correct; they answer different questions. The mainstream synthesis (Rosenberg, Novembre, Templeton) is that clustering reflects real population structure and isolation-by-distance, NOT discrete biological races.
- **The paradigm shift** runs Linnaeus → Blumenbach → craniometry (Morton, Retzius, Broca) → eugenics apex (Grant, Coon) → collapse (Boas, Montagu, Livingstone, UNESCO) → genomic synthesis (HGP, Rosenberg, ancient DNA/Reich). Understanding *why* each step failed is the core intellectual payload.
- **Modern phenotype science** explains the very traits typology fixated on — skin color (Jablonski/Chaplin UV hypothesis; SLC24A5; MFSD12), lactase persistence (convergent evolution), EDAR (hair/teeth/sweat glands) — as *independent, clinal, adaptive* traits whose distributions are discordant with one another, which is precisely why trait-clustering into "types" fails.

---

## HOW TO USE THIS DOCUMENT

Each phase lists: **Objectives**, **Primary readings** (full citations, free-access flagged **[FREE]**), **Supplementary**, **Exercises** (including Python), **Time estimate**, and **Calibration callouts** tagged:
- **[SETTLED]** — scientific consensus, not seriously contested.
- **[CONTESTED]** — genuinely open or actively debated among mainstream scientists.
- **[DISCREDITED]** — historically influential but rejected by modern science.
- **[HYPE/PSEUDOSCIENCE]** — fringe or politically motivated claims that misuse the science; flagged so you can recognize them.

**Free-access infrastructure you'll use throughout:**
- **Internet Archive** (archive.org), **Biodiversity Heritage Library** (biodiversitylibrary.org), **Project Gutenberg**, **Wellcome Collection** — public-domain historical texts.
- **PubMed Central (PMC)** — free biomedical papers.
- **1000 Genomes** (via cog-genomics.org/plink/2.0/resources) and **HGDP** (gnomAD-harmonized release) — public genotype data.

---

## DEPENDENCY MAP (why the sequence is what it is)

```
Phase 0  Conceptual & statistical foundations (genotype/phenotype, norm of reaction, variance)
   │        └─ REQUIRED because every later claim is about partitioning variation and
   │           distinguishing heritable disposition from plastic phenotype.
   ▼
Phase 1  Glossary & terminology (HIGHEST WEIGHT)
   │        └─ You cannot read the primary literature (historical or modern) without a
   │           calibrated vocabulary and a map of which terms are valid vs. discredited.
   ▼
Phase 2  History of the typological paradigm (Linnaeus → Coon)
   │        └─ Understand the paradigm on its own terms BEFORE critiquing it, so the
   │           critique is grounded in what was actually claimed.
   ▼
Phase 3  The critique & collapse (Boas, Montagu, Livingstone, UNESCO, Lewontin)
   │        └─ Depends on Phase 2 (what is being refuted) and Phase 0 (variance logic).
   ▼
Phase 4  Modern population genetics of variation (F_ST, PCA, clines, admixture)  ← COMPUTATIONAL CORE
   │        └─ Depends on Phase 3 (Lewontin) and Phase 0 (statistics). This is where you
   │           replicate the key results yourself in Python.
   ▼
Phase 5  Phenotypic traits & their modern genetic/evolutionary explanations (2nd WEIGHT)
   │        └─ Depends on Phase 4 (selection, clines, allele frequencies) to explain WHY
   │           each trait is distributed as it is, and why traits are discordant.
   ▼
Phase 6  Contested frontiers: forensic ancestry, ancient DNA, medical genomics, pseudoscience
            └─ Depends on ALL prior phases; this is where calibration is hardest and most
               load-bearing.
```

Core logic: **statistics → language → historical paradigm → its refutation → the replacement science → the phenotypes themselves → the live debates.** You could in principle do Phase 5 (traits) right after Phase 1, but you'd lack the population-genetic machinery to explain the traits correctly, which is the whole point.

---

## MVP / FAST-TRACK (credible conversational baseline, ~30–40 hours)

If you want the minimum to be genuinely calibrated fast, do exactly this:

1. **Read** Adam Rutherford, *How to Argue With a Racist* (2020) — one sitting, ~4 hrs. Your orientation and myth-inventory.
2. **Read** the **AABA (AAPA) Statement on Race and Racism (2019)** **[FREE]** — the current professional consensus, ~30 min.
3. **Read** Lewontin (1972) *and* Edwards (2003) back-to-back **[both findable FREE]**, then Novembre (2022) review **[FREE, PMC]** — the central quantitative debate, ~4 hrs.
4. **Read** Rosenberg et al. (2002) **[FREE PDF, Rosenberg lab]** + Serre & Pääbo (2004) **[FREE]** — clusters vs. clines, ~3 hrs.
5. **Skim** Jablonski & Chaplin (2000) or the 2010 PNAS version **[FREE, PMC]** — the model case of an adaptive clinal phenotype, ~2 hrs.
6. **Do** the Phase 4 Python exercise: PCA on 1000 Genomes + compute a global F_ST. ~8–12 hrs. *This is the single highest-value activity for you specifically* — it makes Lewontin/Edwards/Rosenberg concrete.
7. **Read** DiGangi & Bethard (2021) **[FREE, PMC]** for the live forensic-ancestry controversy, ~2 hrs.

Fast-track calibration you'll leave with: typology is **[DISCREDITED]**; within > between variation is **[SETTLED]**; "can we cluster/assign individuals" is **[SETTLED: yes, statistically]** but "does that validate folk races" is **[SETTLED: no]**; forensic ancestry reform is **[CONTESTED]**.

---

## PHASE 0 — Conceptual & Statistical Foundations
**Time: 8–12 hours** (compressible given your background)

### Objectives
- Precisely distinguish **genotype vs. phenotype**, and understand why the distinction dooms typology.
- Master **norm of reaction (Reaktionsnorm)**, penetrance, expressivity, pleiotropy, polygenic/quantitative traits, plasticity, heritability (and what heritability does NOT mean).
- Frame variation as a **variance-partitioning / information-theoretic** problem (your accelerator).

### Primary readings
- Wilhelm Johannsen, *Elemente der exakten Erblichkeitslehre* (Jena: Gustav Fischer, 1909) — the coinage of **gene, genotype, phenotype**. German; you need only the conceptual history, not the full text. **[FREE scans exist via archive.org / Linda Hall Library]**
- Johannsen, W. (1911). "The Genotype Conception of Heredity." *The American Naturalist* 45(531): 129–159. **[FREE — public domain, JSTOR/archive.org]** — the English statement of the distinction.

### Supplementary
- The ASU Embryo Project entry "Wilhelm Johannsen's Genotype-Phenotype Distinction" (embryo.asu.edu) **[FREE]** — clean secondary summary; notes Johannsen equated genotype with Reaktionsnorm.
- Any rigorous quantitative-genetics primer on heritability and variance components (e.g., relevant chapters of Falconer & Mackay, *Introduction to Quantitative Genetics*, 4th ed., 1996, ISBN 978-0582243026).

### Exercises
1. **Norm-of-reaction simulation (Python):** Simulate a quantitative phenotype `P = G + E + G×E + noise` for several genotypes across an environmental gradient. Plot reaction norms that cross. Deliverable: a figure demonstrating why two individuals with the same phenotype can have different genotypes and vice versa — the conceptual death of typology.
2. **Variance decomposition:** Given simulated multi-population data, compute total variance and partition into within/between components (one-way ANOVA). This is your warm-up for Lewontin.

### Calibration
- **[SETTLED]** Genotype ≠ phenotype; phenotype = genotype × environment (× development). Heritability is a population- and environment-specific ratio, NOT a measure of how "genetic" a trait is in an individual, and says nothing about causes of *between*-group differences.
- **[DISCREDITED]** The typological assumption that a visible phenotype reliably indexes an underlying essential "type."

---

## PHASE 1 — Glossary & Conceptual Foundation (HIGHEST WEIGHT)
**Time: 12–18 hours.** Build a written glossary; this is a deliverable to yourself.

### Objectives
Produce a personal glossary in three explicitly labeled columns: **(A) Historical/typological terms**, **(B) Craniometric/anthropometric method terms**, **(C) Modern population-genetics terms** — each tagged SETTLED/DISCREDITED and cross-referenced.

### Terms to define (grouped)
**(A) Historical/typological & population-thinking vocabulary:** variety, race, subrace, type, deme, population, breeding population, ecotype, cline (Huxley 1938), clinal variation. Note which survive in modern usage (population, deme, cline, ecotype — valid) vs. which are discredited as biological taxonomy (race, subrace, type).

**(B) Anthropometric / craniometric method terms:** cephalic index (Retzius), cranial index, dolichocephalic / mesocephalic / brachycephalic, cranial capacity, facial index, nasal index (leptorrhine / mesorrhine / platyrrhine), prognathism / orthognathism, Camper's facial angle, craniometric landmarks, epicanthic fold, pigmentation and soft-tissue descriptors, stature and body-proportion indices. **These are historical METHODS — learn them to read the literature and to understand why trait-clustering fails, NOT as a field guide to "identify" anyone.**

**(C) Modern population-genetics vocabulary:** allele frequency, polymorphism (SNP), F_ST and fixation indices (Wright), heterozygosity, Hardy–Weinberg equilibrium, Wahlund effect, admixture, ancestry-informative markers (AIMs), haplogroup, mtDNA/Y-chromosome lineages, principal component analysis of genotypes, STRUCTURE/ADMIXTURE model-based clustering, isolation by distance (Wright), serial founder effect, effective population size (Nₑ), gene flow, genetic drift, coalescent.

### Primary readings
- Julian Huxley (1938) coined **cline**; read a modern treatment via Mielke, Konigsberg & Relethford (below) rather than hunting the original.
- Rasmus G. Winther, "Lewontin (1972)" (arXiv:2110.10945, 2022) **[FREE]** — makes explicit the six Shannon information measures and the Wahlund effect underlying the variance apportionment. *This is the ideal bridge for your information-theory background.*

### Anchor textbook (buy this — it is the spine of Phases 1, 4, 5)
- James H. Mielke, Lyle W. Konigsberg & John H. Relethford, *Human Biological Variation*, 2nd ed. (New York: Oxford University Press, 2011). ISBN 978-0-19-538740-7. Explicitly keeps mathematics to basic algebra, covers race concept, F_ST, population structure, quantitative genetics.

### Exercises
1. Write the tri-columnar glossary (target: 60–80 terms).
2. For each craniometric index, write the formula (e.g., cephalic index = 100 × max head breadth / max head length) and the historical cut-points, then note (a) its measurement error/plasticity and (b) that Boas showed the cephalic index is environmentally plastic within a generation.

### Calibration
- **[SETTLED]** Cline, deme, population, F_ST, admixture, isolation-by-distance are valid, load-bearing modern concepts.
- **[DISCREDITED]** "Race," "subrace," and discrete "type" as biological taxa; the cephalic index as a stable racial marker.
- **[CONTESTED]** The word "population" itself is definition-dependent and sometimes arbitrary (see Van Arsdale & Nelson 2025 on "the population problem") — a subtlety worth knowing.

---

## PHASE 2 — The Typological Paradigm in History (Linnaeus → Coon)
**Time: 20–30 hours (reading-heavy)**

### Objectives
Reconstruct, sympathetically and accurately, how natural historians built the "types" paradigm, so your later critique targets what was actually claimed. Distinguish monogenism vs. polygenism; environmental vs. essentialist explanations.

### Primary sources (mostly public domain — **[FREE]**)
- **Carl Linnaeus**, *Systema Naturae* (1735; 10th ed. 1758). The four *Homo sapiens* varieties. **[FREE — BHL]**
- **Johann Friedrich Blumenbach**, *De generis humani varietate nativa*, 3rd ed. (Göttingen: Vandenhoek et Ruprecht, 1795). Five "varieties," coinage of **"Caucasian."** **[FREE — BHL (DOI 10.5962/bhl.title.35972); Wellcome Collection]**. English: *The Anthropological Treatises of Johann Friedrich Blumenbach*, trans. & ed. Thomas Bendyshe (London: Longman, 1865). **[FREE — archive.org]**
- **Petrus Camper** on the **facial angle** (posthumous, 1791). Read via secondary sources.
- **Samuel George Morton**, *Crania Americana* (Philadelphia: J. Dobson, 1839). Craniometry, the American School. **[FREE — archive.org/BHL]**
- **Josiah Nott & George Gliddon**, *Types of Mankind* (Philadelphia: Lippincott, Grambo, 1854). Polygenism's apex. **[FREE — archive.org]**
- **William Z. Ripley**, *The Races of Europe* (New York: D. Appleton, 1899). Teutonic/Alpine/Mediterranean. **[FREE — archive.org]**
- **Madison Grant**, *The Passing of the Great Race* (New York: Scribner, 1916). The eugenics/scientific-racism apex. **[FREE — archive.org]** — *read critically as a primary document of pseudoscience, not as science.*
- **Carleton S. Coon**, *The Races of Europe* (New York: Macmillan, 1939) and *The Origin of Races* (New York: Knopf, 1962). The last major typological system and its controversy.

Also note (context): Anders Retzius (cephalic index, 1840s), Paul Broca (craniometry, founder of the Paris Anthropological Society, 1859), Joseph Deniker (*The Races of Man*, 1900, coined much terminology), Earnest Hooton (Harvard physical anthropology).

### Secondary / history-of-science (buy or borrow)
- **Nancy Stepan**, *The Idea of Race in Science: Great Britain, 1800–1960* (London: Macmillan/St Antony's, 1982). ISBN 978-0-333-28856-6 (hbk) / US Archon Books ISBN 978-0-208-01972-1. **[FREE to borrow — archive.org]**
- **Elazar Barkan**, *The Retreat of Scientific Racism: Changing Concepts of Race in Britain and the United States Between the World Wars* (Cambridge: Cambridge University Press, 1992; pbk 1993). Hbk ISBN 978-0-521-39193-1; pbk ISBN 978-0-521-45875-7.
- **George W. Stocking Jr.**, *Race, Culture, and Evolution: Essays in the History of Anthropology* (New York: Free Press, 1968; Chicago pbk 1982, ISBN 978-0-226-77494-5).
- **Stephen Jay Gould**, *The Mismeasure of Man*, rev. & expanded ed. (New York: W. W. Norton, 1996). ISBN 978-0-393-31425-0. **Read WITH its critique** (see Phase 3 calibration).

### Exercises
1. **Concordance table:** For 4–5 historical schemes (Linnaeus, Blumenbach, Deniker, Ripley, Coon), tabulate the number of "types," the defining traits, and the boundaries. Observe that the schemes disagree on number (3 to 30+) and boundaries — a first empirical clue that the categories are not carving nature at its joints.
2. **Trace one term:** Follow "Caucasian" from Blumenbach's aesthetic/cranial reasoning to its modern folk usage. Write 500 words on how a scientific-sounding term outlived its discredited basis.

### Calibration
- **[DISCREDITED]** Every typological classification in this phase as a valid biological taxonomy; polygenism; the inference from cranial capacity to intellectual worth; any ranking of "types."
- **[SETTLED as history]** These works were enormously influential and materially shaped law, immigration policy (e.g., US 1924), and atrocity. Study them as history and as a cautionary tale about motivated reasoning in science.
- **[HYPE/PSEUDOSCIENCE]** Grant's and much of Coon's *Origin of Races* framing; note that Coon's polygenic "five subspecies evolving into sapiens separately" thesis was rejected by contemporaries (Dobzhansky, Montagu) and is refuted by modern genetics.

---

## PHASE 3 — The Critique & Collapse of the Paradigm
**Time: 15–20 hours**

### Objectives
Understand *how and why* typology collapsed: empirical (plasticity, clines), theoretical (Modern Synthesis population thinking), and the pivotal quantitative result (Lewontin) plus its principal critique (Edwards).

### Primary readings
- **Franz Boas**, "Changes in the Bodily Form of Descendants of Immigrants" (*American Anthropologist*, 1912, 14(3):530–562) **[FREE]** — cranial form is plastic within one generation; the cephalic index is not a fixed racial marker.
- **Theodosius Dobzhansky**, *Genetics and the Origin of Species* (New York: Columbia University Press, 1937) — population thinking; and **Ernst Mayr**, *Systematics and the Origin of Species* (1942) — the biological population concept that replaces the type.
- **Ashley Montagu**, *Man's Most Dangerous Myth: The Fallacy of Race* (1942; 6th ed., Walnut Creek, CA: AltaMira Press, 1997, ISBN 978-0-7619-8946-8).
- **Frank B. Livingstone**, "On the Non-Existence of Human Races" (*Current Anthropology*, 1962, 3(3):279–281), published with a reply by Dobzhansky. "There are no races, there are only clines." *Read carefully*: Livingstone's argument is about crisscrossing character gradients, not a simple within/between claim.
- **UNESCO**, *The Race Question* (1950) and the revised *Statement on the Nature of Race and Race Differences* (1951), plus later (1964, 1967) statements. **[FREE — unesco.org / archive.org]**
- **Richard C. Lewontin**, "The Apportionment of Human Diversity," in T. Dobzhansky et al. (eds.), *Evolutionary Biology*, vol. 6 (New York: Appleton-Century-Crofts, 1972), pp. 381–398. DOI 10.1007/978-1-4684-9063-3_14. His Table 4 (p. 396) apportioned diversity as **85.4% within populations, 8.3% among populations within a race, 6.3% among races**, concluding (p. 397): "Since such racial classification is now seen to be of virtually no genetic or taxonomic significance either, no justification can be offered for its continuance."
- **A. W. F. Edwards**, "Human Genetic Diversity: Lewontin's Fallacy" (*BioEssays*, 2003, 25(8):798–801). DOI 10.1002/bies.10315. The correlation-structure critique, in his words: the taxonomic conclusion "is unwarranted because the argument ignores the fact that most of the information that distinguishes populations is hidden in the correlation structure of the data and not simply in the variation of the individual factors."

### Supplementary (the modern retrospective — essential for calibration)
- **John Novembre**, "The background and legacy of Lewontin's apportionment of human genetic diversity" (*Phil. Trans. R. Soc. B*, 2022, 377:20200406). **[FREE — PMC9014184]** — the definitive 50-years-later assessment.
- **Jedidiah Carlson & Kelley Harris**, "The apportionment of citations: a scientometric analysis of Lewontin 1972" (*Phil. Trans. R. Soc. B*, 2022, 377:20200409). **[FREE — PMC9019867]**
- **D. J. Witherspoon et al.** (2007), "Genetic Similarities Within and Between Human Populations" (*Genetics* 176(1):351–359) **[FREE — PMC]** — reconciles Lewontin and Edwards: given enough loci, assignment accuracy → 100%, yet a randomly chosen pair from different populations can still be more similar than a pair from the same population when few loci are used.

### Exercises
1. **Replicate Lewontin's arithmetic** conceptually with a Shannon-entropy diversity measure on a small allele-frequency table; then reproduce it as an F_ST. Confirm the ~85/8/6 split.
2. **Demonstrate Edwards's point in code:** simulate many loci with small per-locus F_ST but correlated frequency differences; show that a linear classifier's accuracy rises toward 1.0 as the number of loci grows, even though per-locus within-group variance dominates. *This is the crux for you: it's a signal-accumulation / SNR argument you already understand.*

### Calibration
- **[SETTLED]** Within-population variation greatly exceeds between-group variation (Lewontin's core empirical result; robust across data and statistics). Cranial plasticity (Boas) is real. Population thinking replaced typological thinking.
- **[SETTLED]** Edwards is arithmetically correct that classifiability depends on multi-locus correlation structure; and Lewontin is arithmetically correct about variance apportionment. They are compatible. The rhetorical leap from "clusters exist" to "folk races are valid biological taxa" is **[DISCREDITED / a non sequitur]**.
- **[CONTESTED — historiography]** The *Mismeasure of Man*: Lewis et al. (2011, *PLoS Biology*, "The Mismeasure of Science") **[FREE]** re-measured Morton's skulls and argued Gould's charge of bias was itself biased; but Kaplan, Pigliucci & Banta (2015) and Weisberg & Paul (2016) largely defended Gould's broader point while conceding errors. Net: Gould's specific Morton accusation is doubtful; his general thesis that unconscious bias pervades measurement stands. Read Gould, but read the critiques alongside.

---

## PHASE 4 — Modern Population Genetics of Human Variation (COMPUTATIONAL CORE)
**Time: 25–40 hours (hands-on)**

### Objectives
Move from reading about F_ST/PCA/clines to *computing them yourself* on real public data, and to internalize the clusters-vs-clines synthesis.

### Primary readings
- **Noah A. Rosenberg et al.**, "Genetic Structure of Human Populations" (*Science*, 2002, 298(5602):2381–2385). DOI 10.1126/science.1078311. Abstract, verbatim: "We studied human population structure using genotypes at 377 autosomal microsatellite loci in 1056 individuals from 52 populations. Within-population differences among individuals account for 93 to 95% of genetic variation; differences among major groups constitute only 3 to 5%. Nevertheless, without using prior information about the origins of individuals, we identified six main genetic clusters, five of which correspond to major geographic regions." **[FREE PDF — rosenberglab.stanford.edu/papers/popstruct.pdf]**
- **David Serre & Svante Pääbo**, "Evidence for Gradients of Human Genetic Diversity Within and Among Continents" (*Genome Research*, 2004, 14(9):1679–1685). DOI 10.1101/gr.2529604. **[FREE]** — the clines rebuttal to naïve cluster interpretation.
- **Rosenberg et al.** (2005), "Clines, Clusters, and the Effect of Study Design on the Inference of Human Population Structure" (*PLoS Genetics* 1(6):e70). **[FREE — PLoS]** — the synthesis: both clinal and clustered structure are real; clustering depends on sampling.
- **Alan R. Templeton**, "Biological races in humans" (*Studies in History and Philosophy of Biological and Biomedical Sciences*, 2013, 44(3):262–271). DOI 10.1016/j.shpsc.2013.04.010. Tests two biological race definitions; chimpanzees have races, humans do not. **[FREE PDF widely available]**

### Supplementary
- Mielke, Konigsberg & Relethford (2011), chapters on population structure, distance, F_ST.
- Coop lab, *Population and Quantitative Genetics* notes (Graham Coop, UC Davis) **[FREE, open textbook]** — rigorous, Python/R-friendly.

### Exercises (the heart of the curriculum for you)
1. **PCA on 1000 Genomes (Python):** Download the PLINK2 phase-3 fileset (cog-genomics.org/plink/2.0/resources#1kg_phase3). QC with PLINK (MAF>0.05, LD-prune `--indep-pairwise 50 5 0.5`), export, load in Python (`scikit-allel` / `pandas` / `scikit-learn`), compute PCA, color by the provided population/superpopulation panel. Reproduce the canonical continental "triangle." Deliverable: a labeled biplot + a paragraph on why gradients (not gaps) appear when sampling is dense.
2. **Compute global and pairwise F_ST** (Weir & Cockerham) across superpopulations; confirm the ~0.10–0.15 magnitude. Relate to Lewontin's ~15% among-groups component.
3. **Isolation by distance:** Using HGDP (the gnomAD-harmonized WGS release, Koenig et al. 2024), regress genetic distance on geographic (great-circle) distance; reproduce the serial-founder decline of heterozygosity with distance from Africa (cf. Ramachandran et al. 2005).
4. **Clines vs. clusters demonstration:** Re-run STRUCTURE/ADMIXTURE at K=2..7 and show how cluster "crispness" changes with sampling density — replicate the Serre–Pääbo / Rosenberg-2005 lesson in miniature.

### Calibration
- **[SETTLED]** Human population structure is real, measurable, and reproducible; it reflects demographic history (migration, drift, gene flow, founder effects), and is dominated by isolation-by-distance → mostly clinal, with some sharper features at geographic barriers.
- **[SETTLED]** Statistical assignment of individuals to populations is possible with enough markers. This does **not** validate discrete biological races.
- **[CONTESTED]** Whether "cluster" solutions should ever be reified as populations vs. treated purely as data-summary artifacts (Winther; the STRUCTURE authors themselves caution the method summarizes, not tests). The number of clusters K is a modeling choice, not a natural constant.
- **[HYPE/PSEUDOSCIENCE]** Blogs/actors who cite Rosenberg 2002 or Edwards 2003 as "proof races are real biologically." The original authors explicitly reject this reading (see Rosenberg's own later writing and the "Are Clusters Races?" analysis, Maglo et al.).

---

## PHASE 5 — Phenotypic Traits & Their Modern Genetic/Evolutionary Explanations (2nd WEIGHT)
**Time: 20–30 hours**

### Objectives
For each visible phenotype historically used to build "types," learn (a) the actual trait and how it was measured, (b) its true continuous/clinal distribution, (c) its modern genetic architecture, and (d) its evolutionary explanation — and see that the traits are **mutually discordant**, which is why they cannot define coherent types.

### Trait-by-trait primary literature (all citations verified)

**Skin pigmentation (the model case):**
- Nina G. Jablonski & George Chaplin, "The evolution of human skin coloration" (*Journal of Human Evolution*, 2000, 39(1):57–106). DOI 10.1006/jhev.2000.0403. The UV/folate/vitamin-D balancing-selection model.
- Jablonski & Chaplin, "Human skin pigmentation as an adaptation to UV radiation" (*PNAS*, 2010, 107(Suppl 2):8962–8968). DOI 10.1073/pnas.0914628107. **[FREE — PMC3024016]**
- Rebecca L. Lamason et al., "SLC24A5, a Putative Cation Exchanger, Affects Pigmentation in Zebrafish and Humans" (*Science*, 2005, 310(5755):1782–1786). DOI 10.1126/science.1116238. The rs1426654 (Ala111Thr) variant "explains between 25 and 38% of the European-African difference in skin melanin index"; the ancestral G allele is near-fixed in African and East Asian samples while the derived A allele is nearly fixed (98.7–100%) in Europeans. **[Free PDF via Davidson College; not on PMC]**
- Nicholas G. Crawford et al., "Loci associated with skin pigmentation identified in African populations" (*Science*, 2017, 358(6365):eaan8433). DOI 10.1126/science.aan8433. **[FREE — PMC5759959]** SLC24A5, MFSD12, DDB1, OCA2/HERC2; shows the "ancestral dark skin" story is more complex — some light-skin alleles are ancient and some "dark" alleles segregate in Europeans.
- Eye color: Hans Eiberg et al. (*Human Genetics*, 2008, 123(2):177–187, DOI 10.1007/s00439-007-0460-x) and R. A. Sturm et al. (*Am. J. Hum. Genet.*, 2008, 82(2):424–431, DOI 10.1016/j.ajhg.2007.11.005) **[FREE — PMC2427173]** on the OCA2/HERC2 blue-eye founder variant.

**Lactase persistence (textbook convergent adaptation):**
- Todd Bersaglieri et al., "Genetic Signatures of Strong Recent Positive Selection at the Lactase Gene" (*Am. J. Hum. Genet.*, 2004, 74(6):1111–1120). DOI 10.1086/421051. **[FREE — PMC1182075]** European LCT/MCM6 −13910.
- Sarah A. Tishkoff et al., "Convergent adaptation of human lactase persistence in Africa and Europe" (*Nature Genetics*, 2007, 39(1):31–40). DOI 10.1038/ng1946. **[FREE — PMC2672153 author manuscript]** Different African alleles, same phenotype — the paradigm case of why phenotype ≠ single ancestry.

**Hair, tooth, and sweat-gland morphology (EDAR):**
- Akihiro Fujimoto et al., "A scan for genetic determinants of human hair morphology: EDAR is associated with Asian hair thickness" (*Human Molecular Genetics*, 2008, 17(6):835–843). DOI 10.1093/hmg/ddm355. **[FREE — Oxford Academic]** The V370A (rs3827760) variant.
- Yana G. Kamberov et al., "Modeling Recent Human Evolution in Mice by Expression of a Selected EDAR Variant" (*Cell*, 2013, 152(4):691–702). DOI 10.1016/j.cell.2013.01.016. **[FREE — PMC3575602]** One pleiotropic allele affects hair thickness, incisor shovel-shape, sweat-gland density, and mammary glands — a vivid pleiotropy lesson.

**Dental morphology (Sinodonty / Sundadonty):**
- Christy G. Turner II, "Major features of Sundadonty and Sinodonty…" (*Am. J. Phys. Anthropol.*, 1990, 82(3):295–317). DOI 10.1002/ajpa.1330820308.
- G. Richard Scott & Christy G. Turner II, *The Anthropology of Modern Human Teeth* (Cambridge: Cambridge University Press, 1997). DOI 10.1017/CBO9781316529843.

**Body size/shape (ecogeographic rules):**
- Bergmann's and Allen's rules in humans: read via Mielke/Konigsberg/Relethford and Katzmarzyk & Leonard (1998, *Am. J. Phys. Anthropol.*) on climate and human body proportions.

### Supplementary books
- **Nina G. Jablonski**, *Skin: A Natural History* (Berkeley: University of California Press, 2006, ISBN 978-0-520-24281-4) and *Living Color: The Biological and Social Meaning of Skin Color* (2012, ISBN 978-0-520-25153-3).
- **Jonathan Marks**, *Human Biodiversity: Genes, Race, and History* (New York: Aldine de Gruyter, 1995, ISBN 978-0-202-02033-4).

### Exercises
1. **Discordance map (Python):** Pull allele frequencies for SLC24A5 (rs1426654), LCT (rs4988235), EDAR (rs3827760), and a Duffy/malaria-related locus across 1000 Genomes/HGDP populations; map each. Show the geographic patterns do NOT coincide → traits are discordant → no consistent "type." *This is the empirical kill-shot against typology, done in code.*
2. **Skin reflectance vs. UV regression:** Reproduce the Jablonski–Chaplin correlation of skin reflectance with autumn UV using their published data table.

### Calibration
- **[SETTLED]** Skin color is adaptive, clinal, polygenic, convergent (light and dark skin each evolved more than once), and a poor proxy for overall ancestry. Lactase persistence is a textbook case of recent, convergent, region-specific selection. EDAR pleiotropy explains a cluster of East Asian/Native American traits from one variant.
- **[SETTLED]** Trait discordance: the geographic distributions of skin color, blood groups, lactase persistence, dentition, and cranial indices do not coincide, so no small set of traits defines internally consistent "types."
- **[CONTESTED / evolving]** The full adaptive story for some traits (e.g., exactly which selective pressure fixed EDAR-V370A; the relative roles of drift vs. selection for some pigmentation loci). Ancient-DNA data are rapidly revising skin-pigmentation history in Europe (e.g., many light-skin alleles arrived/rose recently).

---

## PHASE 6 — Contested Frontiers & Calibration Under Fire
**Time: 15–25 hours**

### Objectives
Handle the hardest, most politically loaded live debates with explicit calibration: forensic "ancestry," ancient DNA and precolonial population history, race in biomedicine, and how to recognize pseudoscience that misuses legitimate genomics.

### A) Forensic anthropology's "ancestry" debate **[CONTESTED — genuinely live]**
- Elizabeth A. DiGangi & Jonathan D. Bethard, "Uncloaking a Lost Cause: Decolonizing ancestry estimation in the United States" (*Am. J. Phys. Anthropol.*, 2021, 175(2):422–436). DOI 10.1002/ajpa.24212. **[FREE — PMC8248240]** Argues to *abolish* ancestry estimation from morphoscopic traits.
- Ann H. Ross & Shanna E. Williams, "Ancestry Studies in Forensic Anthropology: Back on the Frontier of Racism" (*Biology*, 2021, 10(7):602). DOI 10.3390/biology10070602. **[FREE — PMC8301154]**
- Kate Spradley et al. / the "population affinity" reform camp (Forensic Anthropology, 2021, 4(4):309–318, DOI 10.5744/fa.2021.0017) — argues for replacing "ancestry" with **"population affinity"** and reforming rather than abolishing. **[FREE PDF — UF Press]**
- Read the Stull et al. commentary defending continued (reformed) practice for context.

Calibration: **[SETTLED]** skeletal morphology correlates non-zero with geographic origin/social race, so forensic assignment has some predictive value; **[SETTLED]** the traditional 3-race framing is scientifically antiquated; **[CONTESTED]** whether to abolish, reform (→ "population affinity"), or retain ancestry estimation — this is an active, unresolved intra-disciplinary debate, not a settled question.

### B) Ancient DNA and precolonial population history **[fast-moving]**
- **David Reich**, *Who We Are and How We Got Here: Ancient DNA and the New Science of the Human Past* (New York: Pantheon, 2018, ISBN 978-1-101-87032-7; Oxford UP, ISBN 978-0-19-882125-0). Read *with caveats* (see below).
- The core, well-supported finding: **almost all modern populations are admixtures** of earlier, often deeply divergent populations; "precolonial" populations were themselves products of repeated migration and mixture (steppe expansions, farming expansions, etc.). This directly refutes any notion of pure, ancient, static "types."

Calibration: **[SETTLED]** mass admixture is the norm; there are no pure ancestral races; ancient DNA has overturned many older narratives. **[CONTESTED]** specific migration models are revised frequently — treat any single result as provisional. **[CONTESTED — read critically]** Reich's public suggestion that genomics may find average biological differences among populations drew a sharp response: an open letter, "How Not To Talk About Race And Genetics" (BuzzFeed, March 30, 2018), signed by **67 scholars** (led by Jonathan Kahn, Alondra Nelson, Joseph Graves, Marcy Darnovsky, Osagie Obasogie and others), responded to Reich's *New York Times* op-ed (March 23, 2018, "How Genetics Is Changing Our Understanding of 'Race'"). The scientific consensus: such differences, if any, would be small, clinal, and would NOT map onto folk races — and social/environmental confounding is severe for behavioral traits.

### C) Race, ancestry, and biomedicine
- Read the AABA/AAPA (Fuentes et al. 2019, *Am. J. Phys. Anthropol.* 169(3):400–402, DOI 10.1002/ajpa.23882) and AAA (1998) statements **[FREE]**; and the 2023 US National Academies report *Using Population Descriptors in Genetics and Genomics Research* **[FREE — nap.nationalacademies.org]**.

Calibration: **[SETTLED]** self-identified race is a social variable that can proxy for environment, racism-related exposures, and *sometimes* allele-frequency differences relevant to specific variants (e.g., APOL1, some pharmacogenomics), but genetic ancestry is the more precise construct; **[DISCREDITED]** using race as a biological essence in medicine; **[CONTESTED]** best practice for population descriptors in research (the National Academies report is the current reference point).

### D) Recognizing pseudoscience **[HYPE/PSEUDOSCIENCE]**
- **Adam Rutherford**, *How to Argue With a Racist: History, Science, Race and Reality* (London: Weidenfeld & Nicolson, 2020; US: The Experiment, ISBN 978-1-61519-671-5; UK ISBN 978-1-4746-1125-1). Practical field guide to the common misuses (ancestry purity myths, sports "race" claims, IQ hereditarianism).
- **Angela Saini**, *Superior: The Return of Race Science* (Boston: Beacon Press, 2019, ISBN 978-0-8070-7691-0) — on the organized political revival of race science.
- Recognize the standard fallacies: reifying STRUCTURE clusters as races; the Lewontin's-fallacy citation used beyond its warrant; conflating heritability-within-groups with causes-of-differences-between-groups (Lewontin's classic seed/soil rebuttal); and cherry-picked polygenic-score claims.

### Exercises
1. Write a 1,000-word calibrated briefing: "What genomics does and does not say about human races," citing primary literature, with explicit SETTLED/CONTESTED/DISCREDITED tags.
2. Take one viral "race science" claim and dissect it in a short memo: what's the real datum, what's the misuse, what would a correct statement be.

---

## CONSOLIDATED CALIBRATION SUMMARY (the load-bearing takeaways)

**[SETTLED]**
- Typological race (discrete, essential, trait-cluster-defined human types) is not a valid biological taxonomy.
- Human genetic variation is mostly within populations (Lewontin's 85.4% within / 8.3% among-populations-within-race / 6.3% among-races; Rosenberg's 93–95% within-population).
- Variation is largely continuous/clinal, structured by isolation-by-distance and demographic history.
- Individual phenotypic traits (skin, dentition, blood groups, lactase persistence) are discordant in their geographic distributions.
- Statistical assignment/clustering of individuals is possible with enough markers — and does not validate folk races.
- All modern populations are admixed; no pure ancestral races exist.

**[CONTESTED]** (genuine open questions among mainstream scientists)
- Whether/how forensic anthropology should estimate "ancestry"/"population affinity."
- The precise definition and non-arbitrariness of "population" and of cluster number K.
- Details of specific ancient-migration models (revised frequently).
- Best-practice population descriptors in biomedicine/genomics.
- The exact selective pressures behind specific adaptive alleles.

**[DISCREDITED]**
- Polygenism; craniometric ranking; the cephalic index as a stable racial marker; Coon's separate-subspecies-origins thesis; any inference from head/brain size to group intellectual worth.

**[HYPE/PSEUDOSCIENCE — flag on sight]**
- "Rosenberg/Edwards prove races are biologically real."
- Ancestry-"purity" claims; race-based sports/IQ determinism; misuse of polygenic scores across populations; conflating within-group heritability with between-group causation.

---

## Recommendations (staged, with thresholds)

1. **Start now with Phase 0 + the MVP fast-track in parallel.** Do the Rutherford read and the Lewontin/Edwards/Rosenberg core immediately; they give you a calibrated baseline within a week. **Threshold to proceed:** you can state, unprompted, why Lewontin and Edwards are *both* right and what each measures.
2. **Prioritize the Phase 4 computational core.** For you specifically, the PCA + F_ST + discordance-map exercises will cement the concepts faster than any reading. **Threshold:** you can reproduce the 1000 Genomes PCA triangle and explain why denser sampling turns "clusters" into "gradients."
3. **Do Phase 2 history in one focused block** (it's reading-heavy) using free public-domain primary sources plus Stepan + Barkan as the scholarly frame. **Threshold to move to Phase 3:** you can tabulate 4–5 historical schemes and articulate their mutual inconsistency.
4. **Treat Phase 6 as ongoing, not terminal.** Ancient DNA and the forensic debate are moving; re-check the literature every 6–12 months. **Benchmark that should change your views:** a well-replicated, confound-controlled finding would update specific claims — but note that no such finding currently overturns any **[SETTLED]** item above.
5. **Buy three books, borrow/free the rest:** Mielke/Konigsberg/Relethford (spine), Rutherford (orientation), and either Stepan or Barkan (history). Everything else is free or borrowable.
6. **Keep a running SETTLED/CONTESTED/DISCREDITED ledger** as your primary deliverable-to-self; update it as you read. This is the artifact that will make you calibrated rather than merely informed.

## Caveats
- **Fast-moving fields:** ancient-DNA/population genomics and the forensic-ancestry debate are actively evolving; specific migration models and reform proposals will change. Treat single studies as provisional.
- **Source access:** several landmark papers (Lamason 2005, Turner 1990, Edwards 2003, some Reich chapters) are paywalled at the publisher; free routes noted where they exist (PMC, author manuscripts, institutional PDFs). Historical primary sources are almost all public-domain and free.
- **This is not a "how to identify race by appearance" resource** — by design. The anthropometric methods are taught to read the historical literature and to understand *why trait-clustering fails*, not to classify people.
- **Politicization:** this topic attracts motivated misuse from multiple directions. The calibration tags are your defense; always trace claims to primary literature and to the authors' own stated conclusions.
- **One historiographic caution:** the popular narrative that pre-20th-century "race" always meant sharp discontinuities is itself contested by historians (e.g., work noting older usages meant lineage/variety); read the history with the same skepticism you apply to the science.