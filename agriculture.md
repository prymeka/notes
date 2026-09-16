# A Multi-Year Autodidact Curriculum in Agriculture & Forestry
### Balanced across both · all four lenses (science · practice · systems/policy · quantitative/tech) · standalone

## TL;DR
- **A ~36–48 month, part-time (≈8–12 hrs/week) standalone program in 9 phases** covering agriculture and forestry in equal measure, integrating all four lenses you chose — biophysical science, applied practice/management, systems/sustainability/policy, and the quantitative/tech layer — and aiming at **deep scientific & technical mastery + the ability to critically read the primary literature** (journals + the FAO/IPCC/IPBES report canon) + informed fluency. A compressed **~11–13 month MVP fast-path** gets you to solid literacy and paper-reading competence.
- **Scope you set:** balanced ag/forestry; **not** hands-on production competence (so projects are analytical/quantitative/appraisal, not "plant a plot"); deep technical mastery is in scope, and you selected the **quantitative/tech lens**, so the physics bridges are foregrounded — the **Faustmann rotation is a discounted-optimization problem**, **soil water is the Richards equation (Darcy flow in porous media)**, **crop productivity is Monteith radiation-use efficiency**, **evapotranspiration is Penman–Monteith energy balance**, and **remote sensing is radiative transfer**. These sit squarely in your wheelhouse.
- **Anchor texts (verified current, Sept 2026):** Brady & Weil *The Nature and Properties of Soils* **15e (2016/17)**; Ashton & Kelty *The Practice of Silviculture: Applied Forest Ecology* **10e (2018)**; Nair, Kumar & Nair *An Introduction to Agroforestry* **2e (2021)**; Gliessman *Agroecology* **3e (2015)**. Current free report canon: **FAO SOFO 2024** & the annual **SOFA**; **IPCC SRCCL (2019)** and **AR6 WGIII AFOLU (2022)**.
- **European/German anchor woven throughout:** forestry-as-a-science begins here — von Carlowitz's *Sylvicultura oeconomica* (1713) coined sustained-yield/*Nachhaltigkeit*; Faustmann (1849) and Liebig (1840) are German foundations of forest economics and agricultural chemistry; and EU CAP / Forest Strategy 2030 / the Deforestation Regulation are your live policy context.

---

## Key Findings

**1. Soil is the shared foundation of both halves, and it's the right place to start.** Everything in agronomy and silviculture rests on soil–plant–water relations. Brady & Weil (15e) is the market-leading standard and the single highest-leverage first text; the soil-water and nutrient sections are also where your physics pays off immediately (Darcy's law, the Richards equation, mass-balance nutrient cycling).

**2. The four lenses layer cleanly rather than competing.** Biophysical science comes first (soil, plant/tree physiology, ecology, genetics); applied practice/management builds on it (agronomy, animal science, silviculture, forest management); systems/sustainability/policy integrates it (agroecology, climate/carbon, economics, CAP/FAO/IPCC); and the quantitative/tech layer (precision ag, forest mensuration, remote sensing) runs as a strand through all of them and is consolidated at the end. The curriculum is sequenced to respect that.

**3. This field has an unusually large gap between hype and evidence — ideal for your calibration discipline.** Regenerative-agriculture and soil-carbon-sequestration claims, no-till carbon, biochar, organic yield gaps, biofuels, and "plant a trillion trees to fix the climate" are all genuinely **CONTESTED** or **HYPE-WATCH**, with high-profile disputes (e.g., the critiques of Bastin et al. 2019 on tree-restoration potential) that are themselves the best possible training in critical reading. Every such claim is tagged.

**4. The authoritative literature is substantially free and current.** The **FAO** flagship reports (SOFO, SOFA, FRA), **IPCC** land reports (SRCCL, AR6), **IPBES** assessments, **World Agroforestry (ICRAF)** materials, **NPTEL** agriculture/forestry courses, and open satellite data (**Copernicus/Sentinel**, **Google Earth Engine**, **Global Forest Watch**) let you build most of the systems/policy and quantitative strands at zero cost.

**5. The quantitative core of forestry is elegant and physics-adjacent.** Forest mensuration, allometric biomass scaling (metabolic scaling theory / power laws), yield modeling, and the Faustmann optimal-rotation problem give you a rigorous, math-heavy spine that a typical forestry student finds hard and you will find familiar — a genuine accelerator for the quant/tech lens you chose.

---

## Details: The Phased Curriculum (Full Arc)

**Conventions.** Effort assumes serious part-time study (~8–12 hrs/week). Calibration tags: **SETTLED** (established consensus), **CONTESTED** (actively debated), **OPEN** (genuinely unresolved), **HYPE-WATCH** (overclaimed). Free = openly/legally free; Paywalled = purchase/library. Editions marked "verified" were confirmed against publisher pages in Sept 2026. **[Physics/Quant bridge]** flags where your background accelerates a topic. Because you weighted both halves equally, the arc **interleaves** agriculture and forestry on a shared soil/plant/ecology foundation.

---

### PHASE 0 — Orientation: the land, the disciplines, and the quantitative & literature toolkit (foundational, partly parallel)
**Goal:** Map the two fields and their sub-disciplines, and stand up the two strands that run throughout — the quantitative toolkit (agro-meteorology, statistics for field trials, spatial/remote-sensing basics) and the literature/report-reading toolkit.
**Prerequisites:** None (leverages your statistics/Python).

**Primary readings:**
- A one-volume orientation to each field: skim the opening chapters of Brady & Weil (soil), Ashton & Kelty (forestry), and Gliessman (systems) to build the map before depth. **SETTLED.**
- **Report-reading toolkit:** read the **FAO SOFO 2024** ("Forest-sector innovations towards a more sustainable future," free at fao.org) and the most recent **FAO State of Food and Agriculture (SOFA)** end-to-end as your first exercise in reading the report canon critically — what's data, what's projection, what's advocacy. **SETTLED** (as authoritative syntheses).
- **Foundational history (short, high-value):** read *about* von Carlowitz's *Sylvicultura oeconomica* (1713) and the origin of *Nachhaltigkeit*, Liebig's law of the minimum (1840), and the Faustmann formula (1849) — the three intellectual roots you'll return to. **SETTLED** (historical).

**Supplementary / FREE:** NPTEL courses on soil science / agronomy / forestry (free video, good survey); the *Encyclopedia of Agriculture and Food Systems* (reference) for orientation; Global Forest Watch and the FAO FAOSTAT portal to see the actual data.

**Project / quantitative task:** Build an "agro-meteorology mini-toolkit" in Python: implement growing-degree-days, a reference-evapotranspiration calculator via **Penman–Monteith**, and a simple water-balance. **[Physics bridge]** ET is an energy-balance + aerodynamic-resistance problem — derive it, don't just call a library. Separately, write a critical one-pager on one SOFO/SOFA claim (method, uncertainty, framing).
**Time:** 6–8 weeks to a working baseline; then it runs in the background.
**Currency notes:** **TIME-SENSITIVE** — SOFO is biennial (check for a 2026 edition) and SOFA is annual; always pull the latest.

---

### PHASE 1 — Soil science: the shared foundation (+ soil–water–nutrient physics)
**Goal:** Deep mastery of soils — formation, physical/chemical/biological properties, fertility, water, and classification — the substrate for everything in both fields.
**Prerequisites:** Phase 0 optional.

**Primary readings:**
- Brady NC & Weil RR, *The Nature and Properties of Soils*, **15th ed. (Pearson, 2016; US ISBN 9780133254488 / Global 9781292162232)** — verified. The definitive introduction; note it explicitly spans forest, range, agricultural, wetland, and constructed ecosystems. **SETTLED.** *This is your spine text for Phase 1.*
- Soil classification: the **USDA Soil Taxonomy** keys and the **FAO/IUSS World Reference Base (WRB)** — read both systems (WRB is the international/European standard). Both **free**. **SETTLED.**

**Primary quantitative/physics readings (optional deep-dive):**
- Soil physics: the water-movement chapters, grounded in **Darcy's law** and the **Richards equation** (a nonlinear diffusion PDE for unsaturated flow). **[Physics bridge]** this is flow in porous media — the same mathematics you'd meet in transport physics. **SETTLED.**
- Hillel D, *Introduction to Environmental Soil Physics* (Academic Press, 2003) — the rigorous soil-physics reference. **SETTLED** (verify edition/availability).

**Supplementary / FREE:** LibreTexts soil-science modules; FAO Global Soil Partnership resources and *Status of the World's Soil Resources* (2015, free); the free ICRAF soil-health materials.

**Project / quantitative task:** Implement a 1-D unsaturated-flow / soil-water-balance model (numerical solution of a simplified Richards equation, or a tipping-bucket model) and drive it with real weather data; compare infiltration under two soil textures. **[Physics bridge]** connect field capacity / wilting point to matric potential and the water-retention curve.
**Time:** 4–6 months.
**Currency notes:** WRB has periodic updates (a 2022 revision is current — verify); Soil Taxonomy is stable.

---

### PHASE 2 — Plant & tree biology: physiology, growth, productivity, and improvement (biophysical science core, shared)
**Goal:** Understand how plants and trees function and grow — photosynthesis, water/nutrient relations, growth and development — plus the genetic basis of crop and tree improvement. This is the science both halves depend on.
**Prerequisites:** Phase 1.

**Primary readings:**
- Taiz L, Zeiger E, Møller IM & Murphy A, *Plant Physiology and Development*, **6th ed. (Sinauer/Oxford, 2018; ISBN 9781605357454)** — the standard (verify whether a newer edition has appeared). **SETTLED.** *(Overlaps your Biology track's plant coverage — lean on that if you did it first.)*
- Crop/tree productivity: Connor DJ, Loomis RS & Cassman KG, *Crop Ecology: Productivity and Management in Agricultural Systems*, **2nd ed. (Cambridge, 2011; ISBN 9780521744034)** — a rigorous, quantitative systems view of productivity. **SETTLED.** **[Physics bridge]** its core is **Monteith's radiation-use-efficiency** framework: yield ≈ intercepted PAR × light-use efficiency × harvest index.
- Plant improvement: Acquaah G, *Principles of Plant Genetics and Breeding*, **2nd ed. (Wiley-Blackwell, 2012; ISBN 9780470664766)** — breeding methods incl. molecular/genomic selection (verify edition). **SETTLED** methods; specific biotech applications **CONTESTED** in policy.

**Landmark/foundational works:**
- Monteith JL (1977), "Climate and the efficiency of crop production in Britain," *Phil. Trans. R. Soc. B* 281:277–294 — the radiation-use-efficiency foundation. **SETTLED.** **[Physics bridge].**
- **GMO safety:** read a major consensus review (e.g., the US National Academies 2016 report *Genetically Engineered Crops*, free). The food-safety verdict is **SETTLED** (approved GE crops are as safe to eat as conventional); ecological, economic, and governance questions remain **CONTESTED**; blanket "GMOs are dangerous" and blanket "GMOs will feed the world" are both **HYPE-WATCH**.

**Supplementary / FREE:** OpenStax *Biology 2e* plant units for gap-filling; the free National Academies GE-crops report.

**Project / quantitative task:** Implement a simple **light-use-efficiency crop-growth model** (intercepted radiation → biomass → yield via harvest index) and calibrate it to a published crop dataset; run a sensitivity analysis on radiation, LUE, and season length. **[Physics bridge]** relate canopy light interception to **Beer's law** (exponential extinction through the canopy).
**Time:** 5–7 months.
**Currency notes:** Verify Taiz and Acquaah current editions; genomic-selection methods evolve — flag recent work.

---

### PHASE 3 — Agronomy & crop production systems (+ crop protection & precision agriculture)
**Goal:** How crops are actually produced — cropping systems, nutrient and water management, and the protection triad (weeds, pests, diseases) — with the precision-agriculture/data layer introduced here.
**Prerequisites:** Phases 1–2.

**Primary readings:**
- Continue Connor, Loomis & Cassman *Crop Ecology* 2e for the systems/management chapters. **SETTLED.**
- Nutrient management: a soil-fertility text or the fertility chapters of Brady & Weil, grounded in **nutrient mass balance** and **Liebig's law of the minimum**. **SETTLED.** **[Quant bridge]** treat nutrient budgeting as a box-model mass balance.
- Crop protection: Agrios GN, *Plant Pathology*, **5th ed. (Academic Press, 2005; ISBN 9780120445653)** — the standard plant-pathology reference (dated but canonical; supplement with current reviews). **SETTLED** fundamentals. Pair with an IPM/economic-entomology text (e.g., Pedigo & Rice, *Entomology and Pest Management* — verify edition). **SETTLED** framework.

**Precision agriculture (your tech lens):**
- Shannon DK, Clay DE & Kitchen NR (eds.), *Precision Agriculture Basics* (ASA/CSSA/SSSA, 2018; ISBN 9780891183679) — current, practical, data-oriented. **SETTLED** basics; ROI/adoption claims **CONTESTED**.
- Vegetation remote sensing intro: Jones HG & Vaughan RA, *Remote Sensing of Vegetation: Principles, Techniques, and Applications* (Oxford, 2010) — verify edition. **[Physics bridge]** vegetation indices (NDVI etc.) come from **spectral radiative transfer** in leaves/canopies.

**Landmark/foundational works:** the Green Revolution literature (Borlaug; and Evenson & Gollin 2003, *Science*, on its impact) — **SETTLED** on productivity gains, **CONTESTED** on distributional/environmental effects; Tilman et al. (2002), "Agricultural sustainability and intensive production practices," *Nature* 418:671–677 — **SETTLED** framing, some specifics **CONTESTED**.

**Project / quantitative task:** Pull an open **Sentinel-2** scene (Copernicus, free; or via **Google Earth Engine**) over an agricultural area, compute an **NDVI** time series across a season, and relate it to crop phenology. **[Physics bridge]** explain NDVI from red/NIR reflectance physics. Optional: a simple yield-response-to-nitrogen curve and economic-optimum-N calculation.
**Time:** 5–7 months (large phase).
**Currency notes:** Agrios is 20 years old — fundamentals SETTLED but pull current reviews for specific pathogens/pesticides; precision-ag tools evolve fast.

---

### PHASE 4 — Animal science & integrated livestock systems (agriculture, science + practice)
**Goal:** The livestock half of agriculture — animal nutrition, physiology, genetics/breeding, and production systems — plus their environmental footprint and integration with cropping.
**Prerequisites:** Phase 2 (biology); Phase 1 (for grassland/soil links).

**Primary readings:**
- Animal nutrition: McDonald P, Edwards RA, Greenhalgh JFD, Morgan CA, Sinclair LA & Wilkinson RG, *Animal Nutrition*, **8th ed. (Pearson, 2022; ISBN 9781292251660)** — the leading (UK/European) standard (verify edition). **SETTLED.** **[Quant bridge]** energy/protein systems are input–output balances.
- Production systems: Field TG & Taylor RE, *Scientific Farm Animal Production*, **12th ed. (Pearson, 2019; ISBN 9780135184917)** — species-by-species production overview (verify edition). **SETTLED.**

**Landmark/foundational works & key reports:**
- Livestock and environment: FAO's *Livestock's Long Shadow* (2006) and the follow-up *Tackling Climate Change Through Livestock* (2013), both free — foundational and **CONTESTED** in their exact figures; read alongside critiques of the "14.5% of emissions" figure. **HYPE-WATCH** on both extreme "meat is the main climate driver" and "livestock is climate-neutral" claims.
- Enteric methane, feed efficiency, and grazing-vs-feedlot debates — **CONTESTED/OPEN**.

**Supplementary / FREE:** NPTEL animal-science courses; national extension animal-nutrition resources.

**Project / quantitative task:** Build a ration-balancing / feed-energy-budget spreadsheet-or-Python model for a ruminant, and estimate the associated enteric-methane output from feed intake using a published emission factor; discuss the uncertainty. **[Quant bridge]** this is a coupled mass-and-energy balance.
**Time:** 3–5 months.
**Currency notes:** Livestock-emissions accounting is actively contested and updated — verify current figures and methods (e.g., GWP* vs GWP100 debates for methane). **CONTESTED.**

---

### PHASE 5 — Forest ecology & silviculture (forestry, science + practice)
**Goal:** The forestry science-and-practice core — how forest ecosystems function and how silviculture tends and regenerates them across stand structures and objectives.
**Prerequisites:** Phases 1–2 (soil, plant physiology).

**Primary readings:**
- Ashton MS & Kelty MJ, *The Practice of Silviculture: Applied Forest Ecology*, **10th ed. (Wiley-Blackwell, 2018; ISBN 9781119270959)** — verified. The definitive, full-color silviculture text; covers forest carbon, fire and climate, ecosystem services, and multi-aged silviculture. **SETTLED.** *This is your forestry spine.*
- Forest ecology (process/quantitative): Waring RH & Running SW, *Forest Ecosystems: Analysis at Multiple Scales*, **3rd ed. (Academic Press, 2007; ISBN 9780123706058)** — a physiological, quantitative, scale-aware treatment that suits your background (water/carbon/energy budgets of forests). **SETTLED.** **[Physics bridge].**

**Landmark/foundational works:**
- von Carlowitz's sustained-yield principle (1713) as the origin of the discipline; the German/Central-European silvicultural tradition (age-class vs continuous-cover forestry — *Dauerwald*). **SETTLED** history; continuous-cover vs rotation forestry remains a live **CONTESTED** management debate, especially in Europe.
- Forest dynamics & disturbance: Oliver & Larson, *Forest Stand Dynamics* (update ed., 1996) — **SETTLED** framework for stand development.

**Supplementary / FREE:** for European/German-tradition tree identification and dendrology, the *Collins Tree Guide* (Johnson & More) and national forestry-service silvicultural guides; NPTEL forestry courses.

**Project / quantitative task:** For a chosen forest type, diagram stand development through the four Oliver-&-Larson stages, and model self-thinning using the **−3/2 self-thinning law**. **[Physics bridge]** connect self-thinning and biomass partitioning to **allometric/metabolic scaling** (power laws; West–Brown–Enquist). Optional: compute a stand's carbon stock from an inventory using published allometric equations.
**Time:** 5–7 months.
**Currency notes:** Waring & Running is 2007 — process-based fundamentals SETTLED; pull current work on forest carbon/drought mortality. Continuous-cover forestry is CONTESTED.

---

### PHASE 6 — Forest management, mensuration & forest economics (forestry, management + quantitative)
**Goal:** The quantitative management core — measuring forests (mensuration/inventory), modeling growth and yield, planning/optimization, and forest economics. This is the phase your math background most accelerates.
**Prerequisites:** Phase 5.

**Primary readings:**
- Mensuration: Kershaw JA, Ducey MJ, Beers TW & Husch B, *Forest Mensuration*, **5th ed. (Wiley-Blackwell, 2016; ISBN 9781118902035)** — the standard for measuring trees/stands, sampling, and inventory (verify edition). **SETTLED.** **[Quant bridge]** sampling theory, allometry, volume/taper equations.
- Management & planning: Bettinger P, Boston K, Siry JP & Grebner DL, *Forest Management and Planning*, **2nd ed. (Academic Press, 2017; ISBN 9780128094761)** — includes linear/integer-programming optimization for harvest scheduling (verify edition). **SETTLED.** **[Quant bridge]** operations research applied to land.
- Forest economics: Amacher GS, Ollikainen M & Koskela E, *Economics of Forest Resources* (MIT Press, 2009; ISBN 9780262012414) — rigorous, model-based. **SETTLED.** **[Quant bridge]** the **Faustmann rotation** is a discounted-cash-flow optimization (choose rotation age to maximize land expectation value) — a clean optimal-stopping/calculus problem.

**Landmark/foundational works:**
- Faustmann M (1849), the land-expectation-value / optimal-rotation formula — read a modern exposition, then the historical note. **SETTLED** (a foundational quantitative result).

**Supplementary / FREE:** open growth-and-yield model documentation (e.g., US Forest Vegetation Simulator, FVS; free); national forest-inventory methodology (e.g., the German Bundeswaldinventur, US FIA) — free and instructive.

**Project / quantitative task:** Implement the **Faustmann optimal-rotation** calculation for a stand given a growth curve, price, and discount rate; show how the optimum shifts with interest rate and how it differs from the maximum-mean-annual-increment (biological) rotation. **[Quant bridge]** this is your optimization comfort zone. Optional: design a simple systematic forest-inventory sampling scheme and estimate volume with confidence intervals.
**Time:** 5–7 months.
**Currency notes:** Verify Kershaw and Bettinger current editions; methods are stable, growth models are region-specific.

---

### PHASE 7 — Agroforestry & the agriculture–forestry intersection; land-use systems
**Goal:** The seam between your two halves — integrating trees with crops and livestock (agroforestry), and the land-use-systems view that ties soil, plants, animals, and forests together.
**Prerequisites:** Phases 3, 5 (both practice cores).

**Primary readings:**
- Nair PKR, Kumar BM & Nair VD, *An Introduction to Agroforestry: Four Decades of Scientific Developments*, **2nd ed. (Springer, 2021; ISBN 9783030753573)** — verified. The definitive agroforestry text; covers silvopasture, alley cropping, homegardens, windbreaks, soil-carbon sequestration, and ecosystem services. **SETTLED.** *(Note the strong Göttingen/German soil-biogeochemistry lineage in the author team.)*
- Land-system science: read a current synthesis on land-use/land-cover change and the food–land–climate nexus (e.g., Foley et al. 2011, "Solutions for a cultivated planet," *Nature* 478:337–342). **SETTLED-ish** framing.

**Landmark/foundational works & key reports:**
- IPCC **Special Report on Climate Change and Land (SRCCL, 2019)** — free — the authoritative land-use/land-degradation/food-security synthesis; read the SPM in full and dip into chapters. **SETTLED** synthesis; specific mitigation potentials **CONTESTED**.
- **IPBES** Land Degradation and Restoration Assessment (2018) — free. **SETTLED-ish.**

**Supplementary / FREE:** World Agroforestry (ICRAF) publications (the Nair intro is even freely posted on their site); EU agroforestry policy materials under the CAP.

**Project / quantitative task:** Quantitatively compare a monoculture with a silvopasture/alley-cropping system on the **Land Equivalent Ratio (LER)** using published yield data, and estimate the added soil-carbon sequestration with appropriate uncertainty bounds. **[Quant bridge]** LER is a simple but revealing productivity ratio; treat the carbon estimate as an uncertain quantity, not a point value.
**Time:** 4–6 months.
**Currency notes:** **TIME-SENSITIVE** — check for newer IPCC/IPBES land outputs; agroforestry carbon claims are CONTESTED (measurement and permanence).

---

### PHASE 8 — Systems, sustainability, climate & policy + the digital/remote-sensing frontier (capstone integration)
**Goal:** Integrate everything through the systems/sustainability/policy lens and the quantitative/tech frontier — agroecology, climate and carbon, biodiversity, economics, EU/global policy, and precision/remote-sensing at scale. This is where all four lenses converge on real debates, doubling as advanced critical-reading practice.
**Prerequisites:** Phases 1–7.

**Primary readings:**
- Gliessman SR, *Agroecology: The Ecology of Sustainable Food Systems*, **3rd ed. (CRC Press, 2015; ISBN 9781439895610)** — the conceptual framework for sustainable food systems (verify current edition). **SETTLED** framework; strong claims about scalability **CONTESTED**.
- Agricultural economics/development: Norton GW, Alwang J & Masters WA, *Economics of Agricultural Development*, **4th ed. (Routledge, 2021; ISBN 9780367110673)** — verify edition. **SETTLED** core.
- Climate & land: IPCC **AR6 WGIII (2022)**, the **AFOLU** chapter, plus the SRCCL from Phase 7 — free. **SETTLED** synthesis.

**Landmark/frontier works (read critically — this is the calibration capstone):**
- Bonan GB (2008), "Forests and climate change: forcings, feedbacks, and the climate benefits of forests," *Science* 320:1444–1449 — why forests' climate effect is not just carbon (albedo, evapotranspiration). **SETTLED** physics; naive "all trees cool the planet" is **CONTESTED**. **[Physics bridge]** surface energy balance.
- Bastin J-F et al. (2019), "The global tree restoration potential," *Science* 365:76–79, **together with its published critiques and the authors' correction** — a case study in how a high-profile carbon claim was over-interpreted. **HYPE-WATCH / CONTESTED.** Read this specifically to practice weighing a contested result against its rebuttals.
- Soil-carbon sequestration & regenerative agriculture: read a balanced current review — the mechanism is **SETTLED**, but the magnitude, permanence, and climate significance of agricultural soil-carbon gains (and "regenerative" branding) are genuinely **CONTESTED / HYPE-WATCH**.
- Biofuels/bioenergy and BECCS land demand — **CONTESTED**.

**Policy anchors (your EU/German context — TIME-SENSITIVE):** the EU **Common Agricultural Policy (CAP 2023–2027)**; the **EU Forest Strategy for 2030**; the **EU Deforestation Regulation (EUDR)** — whose application timeline has shifted, so verify its current status; and Germany's federal forest inventory (**Bundeswaldinventur**) and forest-damage reporting. **CONTESTED** in design and impact.

**The digital/remote-sensing frontier (your tech lens, consolidated):** land-cover and forest-change monitoring (**Global Forest Watch**, Hansen et al. global forest-change dataset), LiDAR-based forest structure and biomass, and digital soil mapping. **[Physics bridge]** radiative transfer, LiDAR ranging, and geostatistics (kriging). **SETTLED** methods; specific biomass/carbon-map accuracies **CONTESTED**.

**Project / quantitative task (capstone):** Using **Google Earth Engine** (free) and the **Hansen Global Forest Change** dataset, quantify forest loss/gain over a chosen region and decade, then write a calibrated brief that integrates the biophysical, management, policy, and data dimensions of what you find — with SETTLED/CONTESTED/OPEN tags on each claim. This exercises all four lenses at once.
**Time:** 5–7 months.
**Currency notes:** **HIGHLY TIME-SENSITIVE** — CAP, EUDR, IPCC outputs, and satellite datasets all update; re-verify before relying on any figure or regulation.

---

## The MVP Fast-Path (~11–13 months, ~10 hrs/week)

Shortest route to informed fluency + competent literature/report reading + a solid (not exhaustive) technical base across both halves:

1. **Months 1–2 — Orientation (Phase 0):** field maps + read FAO SOFO 2024 and the latest SOFA critically; build the Penman–Monteith/GDD toolkit. → *unlocks report reading immediately.*
2. **Months 2–5 — Soil + plant/tree science (Phases 1–2, compressed):** Brady & Weil core chapters; Taiz/Connor productivity chapters; do the light-use-efficiency crop-model project.
3. **Months 4–8 — One practice core each side (Phases 3 & 5, compressed):** Connor *Crop Ecology* management chapters + Agrios fundamentals for agriculture; Ashton & Kelty core silviculture for forestry; do the NDVI-time-series project.
4. **Months 7–10 — Quantitative forestry + intersection (Phases 6–7, compressed):** the Faustmann rotation and a Land Equivalent Ratio comparison; skim Nair agroforestry.
5. **Months 10–13 — Systems/policy/frontier (Phase 8, compressed):** IPCC SRCCL SPM + Bonan (2008) + the Bastin (2019) debate; the Global Forest Watch capstone; learn the CAP/EUDR landscape.

**MVP outcome:** you'll follow ag/forestry news and policy fluently, talk substantively with agronomists and foresters, critically appraise most journal papers and the FAO/IPCC reports, and hold a coherent picture across both halves and all four lenses — with solid (not comprehensive) depth. The full arc then deepens soil physics, animal science, mensuration/economics, and the long tail of systems science.

---

## Dependency Map

```
PHASE 0 (Orientation + quant/literature toolkit) ── runs FIRST, then parallel throughout ─────────┐
                                                                                                  │
PHASE 1 (Soil science — SHARED foundation)                                                        │
   │                                                                                              │
   └──> PHASE 2 (Plant & tree biology + improvement — SHARED science core)                        │
            │                                                                                     │
   ┌────────┴───────────────┐                                                                     │
   ▼ (agriculture)          ▼ (forestry)                                                          │
PHASE 3 (Agronomy +      PHASE 5 (Forest ecology                                                  │
  crop protection +        + silviculture)                                                        │
  precision ag)              │                                                                     │
   │                         ▼                                                                     │
PHASE 4 (Animal science) PHASE 6 (Mensuration,                                                    │
   │                        management & economics — quant core)                                  │
   └───────────┬─────────────┘                                                                     │
               ▼                                                                                   │
        PHASE 7 (Agroforestry / intersection / land-use systems)                                   │
               │                                                                                   │
               ▼                                                                                   │
        PHASE 8 (Systems, sustainability, climate, policy + digital/remote-sensing — ALL lenses) <─┘
```

**Strict serial spine:** 0 → 1 → 2, then the two branches (3→4 for agriculture; 5→6 for forestry) can run in parallel or in sequence, converging at 7 → 8. **Parallelizable strands:** the quantitative/tech toolkit (Phase 0) and the report-reading habit run continuously; precision-ag/remote-sensing appears in Phases 3, 6, and 8. **Overlap with your other tracks:** Phase 1 soil overlaps your **Geology** (pedology/weathering) track and Phase 2 plant physiology overlaps your **Biology** track — lean on whichever you did first.

---

## Overall Timeline & Effort

- **Full arc:** ~**36–48 months** (≈3–4 years) at ~8–12 hrs/week — roughly **1,600–2,300 hours**. This is the broadest of your recent domains (balanced ag + forestry × four lenses × deep mastery), so the calendar is long; Phases 3, 5, 6, and 8 dominate.
- **MVP fast-path:** ~**11–13 months** at ~10 hrs/week (~500–560 hours).
- The quantitative phases (1 soil physics, 2 productivity, 6 mensuration/economics, 8 remote sensing) are where your physics/math background buys the most time back.

---

## Recommendations (staged, with decision thresholds)

**Stage 1 (Months 0–2): Start the toolkit and the soil foundation together.** Phase 0 quant/report toolkit (fast, plays to your strengths) + begin Brady & Weil. **Threshold to proceed:** you can read a SOFO/SOFA claim critically and compute reference ET and a water balance.

**Stage 2 (Months 2–8): Own the shared science, then split.** Drive Phases 1–2 to real depth, then start both practice cores (3 and 5). **Threshold:** you can explain soil–plant–water relations and reconstruct the light-use-efficiency yield identity from memory, and read a Sentinel scene into an NDVI series.

**Stage 3 (Months 8–24): Build the quantitative and management cores.** Phases 4, 6, 7 — the Faustmann rotation and LER comparison are the signature quantitative deliverables. **Threshold:** you can set up and solve an optimal-rotation problem and design a defensible forest-inventory sample.

**Stage 4 (Months 24+): Systems, policy, frontier.** Phase 8. **Threshold to declare "literature-competent":** you can read a new *Nature Food* / *Forest Ecology and Management* / *Agriculture, Ecosystems & Environment* paper — and an FAO/IPCC chapter — and produce a calibrated (SETTLED/CONTESTED/OPEN) appraisal in under two hours, and write the four-lens capstone brief.

**Ongoing:** follow tables of contents for *Nature Food*, *Field Crops Research*, *Agriculture, Ecosystems & Environment*, *Soil Biology & Biochemistry*, *Forest Ecology and Management*, and *Agroforestry Systems*; track the FAO SOFO/SOFA/FRA cycle and IPCC/IPBES outputs; and watch EU CAP/Forest-Strategy/EUDR developments as your live policy context. Re-verify any policy or carbon figure at the moment you rely on it.

**What would change this plan:** if the goal narrows to one half, drop the other branch (3–4 or 5–6). If you later want hands-on production competence (explicitly excluded now), attach practical field/extension modules after the relevant practice core. If a target text's newer edition ships mid-study, switch at a phase boundary. If the quant/tech lens becomes the priority, expand Phases 6 and 8 (mensuration, optimization, remote sensing, geostatistics) into a dedicated strand.

---

## Caveats

- **Editions verified vs. not:** Verified against publisher pages (Sept 2026): Brady & Weil 15e (2016, ISBN 9780133254488), Ashton & Kelty *Practice of Silviculture* 10e (2018, ISBN 9781119270959), Nair/Kumar/Nair *Introduction to Agroforestry* 2e (2021, ISBN 9783030753573), and the FAO SOFO 2024 report. **Cited from established knowledge — verify current edition at purchase:** Gliessman *Agroecology* 3e (2015); Taiz et al. *Plant Physiology and Development* 6e (2018); Connor/Loomis/Cassman *Crop Ecology* 2e (2011); Acquaah *Plant Genetics and Breeding* 2e (2012); Agrios *Plant Pathology* 5e (2005, dated); McDonald et al. *Animal Nutrition* 8e (2022); Field & Taylor *Scientific Farm Animal Production* 12e (2019); Waring & Running *Forest Ecosystems* 3e (2007); Kershaw et al. *Forest Mensuration* 5e (2016); Bettinger et al. *Forest Management and Planning* 2e (2017); Amacher et al. *Economics of Forest Resources* (2009); Norton/Alwang/Masters *Economics of Agricultural Development* 4e (2021); Jones & Vaughan *Remote Sensing of Vegetation*; Hillel *Environmental Soil Physics*. **Free/current report canon (verify latest cycle):** FAO SOFO 2024 (biennial) & SOFA (annual) & FRA (next 2025); IPCC SRCCL (2019) & AR6 WGIII (2022); IPBES assessments; National Academies *Genetically Engineered Crops* (2016); all free.
- **This is a knowledge curriculum, not production or professional training.** Per your scope it builds scientific/technical understanding, literature fluency, and reasoning — not hands-on farming or forest-management competence, licensure, or agronomic advice for a specific field.
- **Free-resource legality:** the free resources named (FAO, IPCC, IPBES, ICRAF, National Academies, NPTEL, Copernicus/Sentinel, Google Earth Engine, Global Forest Watch, LibreTexts) are legitimately open. Textbook PDFs on file-sharing sites generally are not — buy or borrow via a library.
- **HYPE-WATCH domains to read hardest with your calibration toolkit:** tree-planting/afforestation as a climate fix (and the Bastin 2019 saga); regenerative-agriculture and soil-carbon-sequestration magnitude/permanence; no-till carbon; biochar; "carbon-neutral" livestock and, conversely, "meat is the dominant climate driver"; organic-vs-conventional yield and environmental claims; and bioenergy/BECCS land demand. The evidence is genuinely mixed in each — tag accordingly.
- **Genuinely time-sensitive:** all policy (CAP, EU Forest Strategy 2030, EUDR — whose start date has moved), all FAO/IPCC/IPBES report cycles, and satellite datasets. Confirm the current version before relying on any specific number or rule.
- **Coverage by design:** the two halves are interleaved on a shared soil/biology foundation rather than taught as two separate silos; genetics/breeding is folded into Phase 2 and crop protection into Phase 3 rather than given standalone phases; the quantitative/tech lens runs as a cross-cutting strand (Phases 0, 3, 6, 8) rather than a single block; and hands-on practice is deliberately excluded per your scope. European/German context is woven in throughout, consistent with your geology track's regional bias.