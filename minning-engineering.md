# Zinc & Lithium Mining — Process Engineering & Industrial Operations Deep-Dive
### Companion to the main curriculum. Deepens Phases 1D–1E, 2D and 3C to the level needed for geometallurgy and process-data-science conversations.

**Why this document exists.** Two of the CS/ML job families in mining — resource geology/geometallurgy and metallurgical/process data science — sit directly on top of the flowsheet. You cannot build a recovery model, a Bond Work Index predictor, or a flotation-control soft sensor without knowing what the unit operations *do*, what the machinery is, and which parameters matter. The main curriculum covers processing at conversational-fluency depth; this goes to engineering depth: the physics and chemistry of each step, the actual equipment, typical operating parameters, and the full flowsheets for both metals. It is pitched to a physics background, so quantitative anchors (comminution energy, Faraday's law, current efficiency) are included.

**The mental model to hold throughout — the flowsheet.** Every mine is a sequence of unit operations connected by material streams: `ore → comminution → concentration → (concentrate) → extraction/refining → (metal or chemical) → tailings/residue management`. Each box is a piece of machinery with inputs, outputs, a recovery, and a set of control levers. "Metallurgical accounting" tracks mass and metal across the whole chain (feed grade × tonnes in = product + tailings + residue). Learn to think in these boxes and streams and you can follow any operator's description of their plant.

**Calibration tags:** `[SETTLED]` mature, standard industrial practice · `[EMERGING]` real but still proving out at scale · `[ORE-SPECIFIC]` the number varies by deposit, so quote ranges not points.

---

## Part 1 — Shared unit operations & machinery (the toolkit both flowsheets draw on)

### 1.1 Comminution & classification — breaking rock, the energy-dominant step
Comminution (size reduction) is where most of a mine's electricity goes — commonly 30–50% of site energy — because you are fracturing rock down to the grain size at which valuable minerals are *liberated* from gangue (tens to a few hundred microns). `[SETTLED]`

**The equipment train, in order of decreasing particle size:**
- **Primary crushers** — take run-of-mine rock (up to ~1.5 m). **Gyratory crushers** (a cone gyrating inside a concave bowl) for high-tonnage open-pit feed; **jaw crushers** (two plates, one fixed one reciprocating) for smaller/underground operations. Output ~100–150 mm.
- **Secondary/tertiary crushers** — **cone crushers** (e.g., Metso HP/MP series) reduce to ~10–30 mm. Increasingly replaced or supplemented by:
- **High-Pressure Grinding Rolls (HPGR)** — two counter-rotating rolls (one fixed, one floating on hydraulic rams) crush a compressed particle bed. More energy-efficient than conventional crushing/grinding and induces micro-cracks that ease downstream grinding; vendors thyssenkrupp, Köppern, FLSmidth, Metso. `[EMERGING→SETTLED]` — now standard on many hard-ore circuits.
- **Tumbling mills** — rotating steel drums:
  - **SAG (Semi-Autogenous) mills** — large diameter (up to ~12 m / 40 ft), grind using the ore itself *plus* a ~8–15% charge of steel balls. The workhorse of most base-metal concentrators.
  - **Ball mills** — smaller media (steel balls), finer grind; usually follow the SAG (the "SAB"/"SABC" circuit = SAG–Ball–(pebble) Crusher).
  - **Rod mills** — steel rods; older, coarser product.
- **Stirred/vertical mills for fine & ultrafine grinding** — **IsaMill** (Glencore Technology), Metso **Vertimill**, FLSmidth/Metso **SMD**. Used when minerals are finely disseminated and must be ground below ~20 µm (increasingly common as high-grade coarse ores deplete).

**Classification** separates "fine enough" from "recycle":
- **Vibrating screens** (coarse) and, dominantly, **hydrocyclones** — a slurry is fed tangentially into a cone; centrifugal force sends coarse particles down the wall (underflow, back to the mill) and fine particles up the centre (overflow, on to flotation). Cyclone clusters (Krebs/Cavex) are ubiquitous.

**The physics (your entry point).** Comminution energy is described empirically by **Bond's Third Theory**: the work to reduce a particle scales with the change in the inverse square root of particle size,
`W = 10 · Wi · (1/√P₈₀ − 1/√F₈₀)` (kWh/t),
where `Wi` is the **Bond Work Index** (a material property, kWh/t), and `F₈₀`/`P₈₀` are the 80%-passing sizes of feed and product. `Wi` is measured by a standardized lab test; predicting it across an orebody from sparse test work is a canonical geometallurgy ML problem (see Part 4). Bond sits alongside Kick's law (coarse) and Rittinger's law (fine); modern practice uses the JK drop-weight/SMC parameters (A, b, ta) for SAG modelling.

### 1.2 Concentration by froth flotation — the single most important separation
Flotation exploits differences in *surface chemistry* to separate finely ground minerals. It is the heart of nearly every sulphide concentrator (including zinc) and is used in spodumene beneficiation. `[SETTLED]`

**How it works.** Ground ore is slurried (~25–40% solids) in a cell and aerated. Chemicals are added so that target-mineral surfaces become **hydrophobic**; air bubbles attach to those particles and carry them up into a **froth** that overflows as concentrate, while hydrophilic gangue stays in the pulp (tailings). The governing physics is bubble–particle collision-and-attachment, contact angle, and froth stability; particle size matters enormously (ultrafines <10 µm and coarse >150 µm both float poorly).

**Reagent families — the chemistry an operator lives by:**
- **Collectors** — adsorb on the mineral and make it hydrophobic. For sulphides, **xanthates** (SEX/SIPX — sodium ethyl/isopropyl xanthate) and **dithiophosphates**. Dosage ~20–200 g/t.
- **Frothers** — stabilize bubbles/froth. **MIBC** (methyl isobutyl carbinol), polyglycols.
- **Modifiers** — the selectivity toolkit: **pH regulators** (lime, soda ash); **activators** (copper sulphate, CuSO₄, activates sphalerite); **depressants** (zinc sulphate + sodium cyanide to hold sphalerite back; sodium sulphide; lime to depress pyrite). This activator/depressant interplay is exactly how zinc is separated from lead (see Part 2).

**Cell types (the machinery):**
- **Mechanical (tank) cells** — an impeller disperses air and keeps solids suspended; forced-air (Metso/Outotec TankCell) or self-aspirating (FLSmidth WEMCO/Dorr-Oliver). Arranged in banks; cell volumes now reach 300–600 m³.
- **Flotation columns** — tall vessels with countercurrent wash water; superior for cleaning (high-grade final concentrate).
- **Jameson Cell** (Glencore Technology) — high-intensity downcomer that generates fine bubbles; fast, compact.

**Circuit design.** Cells are staged: **rougher** (bulk recovery) → **scavenger** (recover what the roughers missed) → **cleaner** (upgrade rougher concentrate, often after a **regrind** mill). There is always a **grade–recovery trade-off**: push recovery and grade falls, and vice versa — the single most important curve in a concentrator, and a natural optimization target.

**Instrumentation & control** — froth cameras (VisioFroth/FrothCam) read bubble size and froth velocity; on-stream XRF analyzers (Courier/Outotec) assay slurry streams every few minutes; level and air-flow controllers per cell. This is where process data science plugs in.

### 1.3 Gravity, dense-media & magnetic separation (supporting concentration)
- **Dense-Medium Separation (DMS)** — sink-float in a magnetite/ferrosilicon suspension of controlled density; used to reject barren waste early (and, importantly, as the first stage in **spodumene** beneficiation, since spodumene is denser than most host minerals). `[SETTLED]`
- **Gravity** — jigs, spirals, shaking tables, centrifugal concentrators (Knelson/Falcon) for dense minerals.
- **Magnetic separation** — low- and high-intensity (LIMS/WHIMS); critical in lithium finishing to strip iron contamination to battery-grade limits.

### 1.4 Solid–liquid separation & dewatering
Between and after wet steps you must separate solids from water:
- **Thickeners/clarifiers** — large tanks where **flocculants** (long-chain polymers) agglomerate fines so they settle; clear water overflows, thickened underflow is pumped on. High-rate and paste thickeners (Outotec, FLSmidth). `[SETTLED]`
- **Filters** — **plate-and-frame/pressure filters** (Metso Larox), **belt** and **vacuum disc/ceramic** filters, dry the concentrate or residue to a filter cake. Filtration is also what makes "dry-stack" tailings possible (§1.9).

### 1.5 Leaching reactors — dissolving the metal (hydrometallurgy)
Leaching dissolves the target metal into solution for later recovery:
- **Heap leaching** — crushed ore stacked on a lined pad, irrigated with lixiviant (acid or, for gold, cyanide); cheap, low-recovery, slow. Rio Tinto's Nuton is a heap-leach-for-copper venture. `[SETTLED]`
- **Agitated tank leaching** — stirred CSTR cascades; faster, higher recovery; the norm for zinc calcine leaching.
- **Pressure leaching (autoclaves)** — sealed titanium/brick-lined vessels at high temperature and oxygen pressure (e.g., ~150–230 °C, 1–3 MPa) to dissolve refractory minerals directly (used in zinc **pressure leaching** to attack sphalerite without roasting, and in some iron-residue routes). Kinetics (temperature, particle size, oxygen mass transfer) govern throughput. `[SETTLED]`

### 1.6 Solution processing — purifying the pregnant liquor
- **Solvent Extraction (SX)** — a metal-selective organic extractant contacts the aqueous liquor in **mixer-settlers**; the metal transfers to the organic phase, then is stripped back into a clean, concentrated aqueous stream. The backbone of copper hydrometallurgy; used for boron removal in lithium brines and increasingly explored for DLE. `[SETTLED]`
- **Ion exchange (IX)** — resin beds selectively grab target ions; used as a polishing step (e.g., final impurity removal in lithium finishing, and in several DLE schemes).
- **Precipitation** — adjust pH/add reagents to drop impurities (or the product) out as solids (iron as jarosite/goethite; magnesium as hydroxide; lithium as carbonate).
- **Cementation** — add a more reactive metal powder to displace a less reactive one from solution (zinc dust displaces Cu/Cd/Co/Ni in zinc purification — see Part 2).

### 1.7 Electrometallurgy — winning the pure metal
- **Electrowinning (EW)** — pass current through the purified solution; metal plates onto the **cathode**, oxygen (and regenerated acid) forms at the **anode**. Used for zinc, copper, nickel, cobalt.
- **Electrorefining** — dissolve an impure metal anode and re-deposit pure metal on the cathode.
- **The physics & throughput (Faraday's law).** Deposition rate is set by current: `m = (M · I · t)/(z · F)`, where `M` = molar mass, `I` = current, `t` = time, `z` = electrons transferred (2 for Zn²⁺), `F` = Faraday constant (96,485 C/mol). For zinc the practical **electrochemical equivalent is ~1.2195 g per amp-hour**. **Current efficiency** (typically ~88–92% industrially) is below 100% because hydrogen co-evolves at the cathode — which is *why* the solution must be purified of Co/Ni (they lower the hydrogen overpotential and slash efficiency). This clean chain of physics — impurities → overpotential → efficiency → energy cost — is a good example to have ready.

### 1.8 Pyrometallurgy — heat-driven processing
- **Roasting** — heat a sulphide in air to convert it to an oxide plus SO₂ (a "dead roast"). **Fluidized-bed roasters** (Outotec/Lurgi) — feed floats on an upward air stream for excellent gas–solid contact — are standard for zinc; older multiple-hearth and suspension roasters persist. `[SETTLED]`
- **Smelting** — melt and chemically reduce ore/concentrate to metal (blast furnaces, flash furnaces, electric furnaces).
- **Rotary kilns & calciners** — long rotating inclined tubes for calcination/thermal conversion. **Direct-fired** (material contacts combustion gas) vs **indirect-fired/calciner** (material is heated through the shell, isolated from combustion products) — a distinction that matters critically in spodumene processing (see Part 3). Vendors FEECO, Metso, thyssenkrupp.

### 1.9 Tailings & water management (the ESG-critical back end)
Tailings are the fine wet waste from flotation/leaching. How they are stored is now a board-level, GISTM-governed decision:
- **Conventional slurry TSF** — pumped as slurry behind an embankment. **Upstream** dam construction (building the wall on top of previously deposited tailings) is cheapest but the failure mode implicated at Brumadinho; **downstream** and **centreline** are more stable and now often mandated. `[SETTLED, but practice tightening]`
- **Thickened / paste / filtered ("dry-stack") tailings** — progressively remove water (thickeners → filters) so tailings can be stacked with far less dam risk and better water recovery. `[EMERGING at very large scale]` — the direction of travel, but energy- and cost-intensive at high tonnage.
- **Water balance** is a first-order design constraint everywhere, and the dominant constraint for lithium brine operations in arid Andean basins.

---

## Part 2 — Zinc: the full industrial flowsheet (mine to metal)

Zinc reaches the market via two routes: the dominant **hydrometallurgical Roast-Leach-Electrowin (RLE)** route (>90% of production) and the declining pyrometallurgical **Imperial Smelting Process**. The RLE flowsheet, step by step:

### Step 1 — Concentration: differential Pb–Zn flotation
Sphalerite (ZnS) almost always occurs with galena (PbS) and often chalcopyrite/pyrite, so the concentrator uses **sequential (differential) flotation** — the textbook demonstration of the activator/depressant chemistry from §1.2:
1. Grind to liberation (SAG/ball circuit, target P₈₀ ~ 45–75 µm). `[ORE-SPECIFIC]`
2. **Float galena first** while **depressing sphalerite and pyrite** — add zinc sulphate + sodium cyanide (or SO₂) to keep sphalerite hydrophilic; a short-chain xanthate floats the lead. Product: a lead concentrate.
3. **Then activate sphalerite** with **copper sulphate** (Cu²⁺ replaces Zn²⁺ on the surface, making it respond to collector), raise pH with lime to depress pyrite, and float the zinc. Product: a **zinc concentrate at ~50–55% Zn** (sphalerite is 67% Zn in theory; the rest is Fe, Pb, gangue). `[SETTLED]`

The **iron content of the concentrate (often several %, up to ~12%)** is the villain of the next stage.

### Step 2 — Roasting: sphalerite → calcine + sulphuric acid
The zinc concentrate is dead-roasted at **~900 °C in a fluidized-bed roaster**: `2 ZnS + 3 O₂ → 2 ZnO + 2 SO₂`. Two products: `[SETTLED]`
- **Calcine** (crude ZnO) — fed to leaching.
- **SO₂ gas** → a **contact-process sulphuric acid plant**. Acid is not a nuisance byproduct; it is an essential co-product and often a meaningful revenue/logistics factor for a smelter.

The catch: any iron combines with zinc to form **zinc ferrite (ZnFe₂O₄)**, which is *insoluble* under normal leach conditions — locking up zinc and forcing the iron-management problem below.

### Step 3 — Leaching: calcine → zinc sulphate solution
Calcine is dissolved in sulphuric acid, supplied as the **spent electrolyte returned from electrowinning** (closing the acid loop): `ZnO + H₂SO₄ → ZnSO₄ + H₂O`. Two stages: `[SETTLED]`
- **Neutral (weak) leach** (~pH 5, ~60–70 °C) dissolves the easy ZnO.
- **Hot acid leach** (~90–95 °C, high free acid) attacks the zinc ferrite to recover the locked zinc — but this also dissolves the iron, which must then be removed.

### Step 4 — Iron removal: the defining zinc-hydromet problem
Dissolved iron must be precipitated as a filterable, storable residue. Three main routes, a genuine engineering trade-off: `[SETTLED]`
- **Jarosite** process — precipitate iron as `(Na/K/NH₄)Fe₃(SO₄)₂(OH)₆` at ~pH 1.5 and ~95 °C. High zinc recovery, easy operation, but produces large volumes of jarosite residue (35–50% iron oxide) that is a long-term storage liability.
- **Goethite** process (Vieille Montagne) — precipitate iron as FeOOH at pH ~2–3.5 by controlling ferric concentration; denser residue, less volume.
- **Hematite** process — precipitate iron as Fe₂O₃ in an autoclave (~200 °C, elevated pressure); the cleanest, most compact residue (potentially saleable) but capital- and energy-intensive.
Which route a smelter runs is a real point of differentiation and a good thing to ask an operator about.

### Step 5 — Solution purification: cementation
Before electrowinning, the neutral zinc sulphate liquor must be stripped of metals that would poison the cell (especially **Co, Ni, Cu, Cd** — the hydrogen-overpotential wreckers). This is done by **cementation with zinc dust** (add fine zinc powder; more-noble metals plate out): `[SETTLED]`
- A **hot stage** removes copper and cadmium.
- A **cobalt/nickel stage** (harder) uses zinc dust with activators (antimony or arsenic trioxide + copper). Cadmium recovered here is itself a saleable byproduct.

### Step 6 — Electrowinning: plating zinc metal
The purified solution goes to the **cell house (tankhouse)**. `[SETTLED]`
- **Cathodes: aluminium** blanks; **anodes: lead–silver alloy** (~0.5–1% Ag, to reduce corrosion and oxygen overpotential).
- Typical operation: current density **~400–650 A/m²**, cell voltage **~3.2–3.5 V**, electrolyte **~30–40 °C** (cooled via towers), **current efficiency ~88–92%**, specific energy **~3.0–3.3 kWh per kg Zn** (one of the more energy-intensive metal refining steps).
- Every **24–48 hours** the zinc is stripped from the aluminium cathodes by **automated stripping machines**; the spent, re-acidified electrolyte returns to leaching.
- Product: **Special High Grade (SHG) zinc, 99.995% Zn**.

### Step 7 — Melting & casting
Cathode zinc is melted in **induction furnaces** and cast into SHG ingots/jumbos or alloyed (e.g., **Zamak** die-casting alloys, or **continuous-galvanizing-grade** alloys with aluminium) and often shipped molten to nearby galvanizing lines. `[SETTLED]`

### The alternative: Imperial Smelting Process (ISF)
A pyrometallurgical route that smelts zinc **and lead together**: sinter the mixed feed (sinter plant), reduce in a **blast furnace** with coke, and condense zinc vapour in a **lead-splash condenser**. Energy-intensive and declining, surviving mainly at some integrated Zn–Pb sites in China, India, Japan, and Poland. Do not assume ISF availability — most plants are aging. `[SETTLED, but shrinking]`

### Quantitative anchor for conversation
A 200,000 t/yr electrolytic zinc plant, at ~3.1 kWh/kg, draws on the order of **~620 GWh/yr** just for electrowinning — which is why zinc smelters are extremely power-price-sensitive and why several idled during the 2022 European energy crisis. Pair this with Faraday's law (§1.7) and you can reason quantitatively about a cell house on the fly.

### Zinc machinery summary
Gyratory/jaw + cone crushers (± HPGR) → SAG/ball mills + cyclones → mechanical/column flotation banks → thickeners/filters → **fluidized-bed roaster + sulphuric acid plant** → agitated leach tanks → iron-precipitation reactors (± autoclave) → cementation reactors → **EW cell house (Al cathodes, Pb–Ag anodes) + automated strippers** → induction melting/casting.

---

## Part 3 — Lithium: two industrial flowsheets (hard-rock and brine) plus DLE

Lithium is fundamentally different: the products are **chemicals** — lithium carbonate (Li₂CO₃) and lithium hydroxide monohydrate (LiOH·H₂O) — not a refined metal, and the two feedstocks (hard rock and brine) run almost completely different plants that converge only at the final chemical-conversion steps.

### Flowsheet A — Hard-rock (spodumene) conversion
Spodumene (LiAlSi₂O₆, up to 8% Li₂O in pure mineral) is the dominant hard-rock source. The route from rock to battery chemical:

**A1 — Mining & beneficiation to SC6.** Conventional open-pit (sometimes underground) mining → crush/grind → **Dense-Medium Separation** and/or **flotation** to reject gangue and produce a **spodumene concentrate at ~6% Li₂O ("SC6")**, the traded feedstock. `[SETTLED]`

**A2 — Decrepitation (α→β phase conversion).** Natural **α-spodumene** is dense and chemically inert. Calcining SC6 at **~1,075–1,100 °C** in a **direct-fired rotary kiln** (set at a slight incline; gravity moves material down the drum) converts it to **β-spodumene**, expanding the crystal structure by **~30%** and opening it to chemical attack. Temperature control is critical: approaching ~1,400 °C forms undesirable eutectic melts. A **direct-fired** kiln is used here because α-spodumene tolerates contact with combustion gases. This step alone consumes roughly **half** a lithium refinery's energy — hence the strong decarbonization interest. `[SETTLED]`

**A3 — Sulphuric acid roast.** The cooled β-spodumene is ground (<~150 µm), mixed with **concentrated sulphuric acid** (~93%, typically ~30–40% stoichiometric excess), and roasted in a **separate indirect-fired rotary kiln (calciner)** at **~200–250 °C for ~30 min–1 h**: the acid's protons swap for lithium, forming **water-soluble lithium sulphate (Li₂SO₄)**. An **indirect** kiln is mandatory here because β-spodumene must *not* contact combustion products. `[SETTLED]`

**A4 — Water leach & impurity removal.** The roasted mass is leached in water (near ambient) to dissolve Li₂SO₄. The solution is then cleaned in stages: precipitate **iron and aluminium** (pH adjustment), remove **magnesium and calcium** as hydroxides/carbonates (lime + soda ash), and polish with **ion exchange** to hit battery-grade impurity limits. Lithium recovery from β-spodumene through this sulphate route reaches **~95–97%**. `[SETTLED]`

**A5 — Chemical conversion to the saleable product.**
- **Lithium carbonate** — add **soda ash (Na₂CO₃)** to the hot purified liquor; Li₂CO₃ has *retrograde* solubility (less soluble hot), so it precipitates, is filtered, washed, and dried. `Li₂SO₄ + Na₂CO₃ → Li₂CO₃↓ + Na₂SO₄`.
- **Lithium hydroxide** — either react Li₂CO₃ with **lime** (`Li₂CO₃ + Ca(OH)₂ → 2 LiOH + CaCO₃↓`) or convert Li₂SO₄ directly via causticization/electrodialysis; then **crystallize** LiOH·H₂O. `[SETTLED]`

**A6 — Battery-grade finishing.** Micronize to spec particle size, strip iron to sub-ppm with **high-intensity magnetic separation**, and package under controlled (often dry/inert) atmosphere. Battery-grade means **≥99.5%** purity with tight limits on Na, K, Ca, Mg, Fe, and sulphate — a genuinely different (and more valuable) product than technical grade. `[SETTLED]`

**Emerging alternatives** `[EMERGING]`: **fluidized-bed calcination** instead of rotary kilns (better heat transfer, decarbonization); and **acid-free/alkaline routes** (soda-ash "carbonizing" roast, lime roast, chlorination) that aim to cut the acid step — mostly pilot/research, not yet mainstream.

### Flowsheet B — Continental brine (salar) processing
Brine operations are chemical-plant-plus-evaporation, not mining in the mechanical sense:

**B1 — Wellfield.** Lithium-bearing brine is pumped from beneath a salar (e.g., Atacama, ~0.15% Li — the world's richest; grade and the **magnesium-to-lithium ratio** are the key quality variables). `[SETTLED]`

**B2 — Staged solar evaporation.** Brine flows through a **sequence of large lined ponds** over **12–18 months**; as water evaporates, salts drop out in order — first **halite (NaCl)**, then potassium salts (**sylvinite/carnallite**, often recovered as a potash byproduct) — progressively concentrating lithium from ~0.15% to several percent. Along the way **magnesium, calcium, and boron** are removed (lime precipitation for Mg/Ca; **solvent extraction** or ion exchange for boron). Overall lithium recovery is modest, **~40–50%**, and the process is land-, water-, and time-intensive. `[SETTLED]`

**B3 — Chemical plant.** The concentrated, purified brine is treated with **soda ash** to precipitate **Li₂CO₃** (same carbonation chemistry as A5), then optionally converted to hydroxide. `[SETTLED]`

The brine route's economics are the mirror image of hard rock: low operating cost but very slow, capital-locked in ponds, weather-exposed, and geographically constrained.

### Flowsheet C — Direct Lithium Extraction (DLE) — the contested frontier
DLE pulls lithium selectively from brine **without** (or with much-reduced) evaporation ponds. Four technology families: `[EMERGING / CONTESTED]`
- **Adsorption** — lithium-selective sorbents (aluminate-based, e.g., LiCl·2Al(OH)₃; or **manganese/titanium oxide "ion sieves"**) load lithium in columns, then release it on regeneration. This is the most commercially advanced form (deployed in China and Argentina).
- **Ion exchange** — resins/oxides that swap H⁺ for Li⁺.
- **Membranes** — nanofiltration and **electrodialysis** to separate Li⁺ from Mg²⁺/other ions.
- **Solvent extraction** — Li-selective organic extractants in mixer-settlers.

**Why it matters:** faster (hours–days vs months), higher recovery (potentially >80%), smaller footprint, and it unlocks lower-grade/higher-impurity brines (including geothermal and oilfield brines). **Why it's contested:** higher capex and often higher opex than conventional brine; selectivity and sorbent-lifetime challenges against high magnesium; large fresh-water and reagent demands in regeneration; and scale-up has repeatedly run slower and costlier than promised, with profitability sensitive to depressed lithium prices. The honest framing: **adsorption DLE is real and operating, but "DLE will imminently transform the market" is hype** — its technology-readiness at scale is genuinely debated in the literature. Always pair a proponent source with a skeptic.

### The battery-chemistry linkage (why the product split matters)
- **Lithium hydroxide** is preferred for **high-nickel NMC/NCA** cathodes — it decomposes at a lower temperature (~450 °C vs ~750 °C for carbonate), preserving the nickel-rich crystal structure.
- **Lithium carbonate** feeds **LFP (lithium iron phosphate)** and lower-nickel cathodes.
The global swing toward LFP (now roughly half the EV market, dominant in China) has shifted demand back toward carbonate and eroded the earlier "hydroxide premium" thesis. Knowing this carbonate-vs-hydroxide / LFP-vs-NMC linkage is a strong credibility signal on the lithium side. `[SETTLED trend, with forecast uncertainty]`

### Lithium machinery summary
- **Hard rock:** crushers → mills → **DMS + flotation** → **direct-fired decrepitation kiln (~1,075–1,100 °C)** → cooling/grinding → **indirect-fired acid-roast calciner (~250 °C)** → water-leach tanks → impurity-removal reactors + ion exchange → carbonation/causticization crystallizers → micronizing + magnetic separation + controlled-atmosphere packaging.
- **Brine:** wellfield pumps → **evaporation pond trains** (± Mg/B removal via lime and solvent extraction) → carbonation plant → (optional) hydroxide conversion. **DLE** replaces the ponds with **sorbent columns / IX / membrane / SX** trains plus regeneration circuits.

---

## Part 4 — The geometallurgy & process-data bridge (why this connects to the ML jobs)

This is the payoff: understanding the flowsheet tells you what data exists, what is worth predicting, and where a data scientist actually plugs in.

**Where the data comes from:**
- **Online/at-line analyzers** — on-belt PGNAA/XRF elemental analyzers (Scantech/Thermo), laser particle-size analyzers, **on-stream slurry XRF** (Courier), and **froth cameras** in flotation.
- **Process control historians** — DCS/PLC/SCADA systems logging thousands of tags (flows, levels, pressures, temperatures, motor loads) at second-to-minute resolution — the raw material for soft sensors and predictive control.
- **Laboratory & test-work databases (LIMS)** — assays, metallurgical test results, and the drill-hole database.
- **Automated mineralogy** — **QEMSCAN / MLA** (automated SEM-EDS) quantifying mineral associations and liberation — increasingly ML-analyzed.

**The high-value prediction targets (what the models actually do):**
- **Comminution/geometallurgy** — predict **Bond Work Index, SMC/drop-weight parameters, and throughput** across the orebody from sparse test work plus dense drill-hole assays (the canonical "infer BWI on RC holes from a handful of diamond holes" problem). Feeds mine scheduling and plant-throughput forecasting.
- **Flotation** — predict/optimize **recovery and concentrate grade**, reagent dosing, and the grade–recovery frontier; froth-image classification for cell state.
- **Comminution & fixed-plant control** — **model-predictive control (MPC)** of SAG mills, flotation circuits, and (for lithium) kiln/calciner and (for zinc) autoclave/leach control; **soft sensors** that infer an unmeasured quality variable from cheap measurements.
- **Geometallurgical domaining** — clustering the orebody into zones of similar processing behaviour, so the plant can be tuned block-by-block.

**Standard test work you should be able to name:** Bond ball/rod/abrasion tests and **JK Drop-Weight / SMC** (comminution); flotation kinetic/rate tests and locked-cycle tests; leach amenability tests; and QEMSCAN/MLA mineralogy. When a metallurgist references "the drop-weight test" or "locked-cycle flotation," you now know what they mean.

**Where the roles sit:** the *resource geologist/geometallurgist* owns the orebody-to-plant prediction layer (grade estimation, geomet domaining, throughput models), while the *process/metallurgical data scientist* owns the plant-control-and-optimization layer (recovery models, MPC, soft sensors, predictive maintenance on mills/pumps). Both require exactly the flowsheet understanding above — which is why these two families need this document, and why they are less "commodity-agnostic" than data-platform or forecasting roles.

---

## Part 5 — Engineering-specific reading to go deeper
Layer these on top of the general reading list (the main companion document). All process-focused:

- **Wills, B. A. & Finch, J. A.** *Wills' Mineral Processing Technology*, 8th ed. (Elsevier, 2016). `[Working→Advanced]` — read comminution, classification, flotation, and dewatering chapters in full for the shared toolkit (Part 1). (paid)
- **Gupta, A. & Yan, D. S.** *Mineral Processing Design and Operations*, 2nd ed. (Elsevier, 2016). `[Working]` — the equipment-sizing and circuit-calculation companion to Wills; heavier on the design equations. (paid)
- **Napier-Munn, T. J. et al.** *Mineral Comminution Circuits: Their Operation and Optimisation* (JKMRC). `[Advanced]` — the deep reference for §1.1 and the geometallurgy/BWI material. (paid)
- **King, R. P.** *Modeling and Simulation of Mineral Processing Systems*, 2nd ed. (SME, 2012). `[Advanced]` — quantitative unit-operation models; the natural bridge from process engineering to process data science. (paid)
- **Sinclair, R. J.** *The Extractive Metallurgy of Zinc* (AusIMM Spectrum Series Vol. 13, 2005). `[Ref→Working]` **(free PDF from AusIMM)** — the definitive walk-through of the entire zinc RLE flowsheet (Part 2): roasting, leaching, iron control, purification, electrowinning. Free and directly on-topic.
- **Free, M. L.** *Hydrometallurgy: Fundamentals and Applications* (Wiley/TMS, 2013). `[Advanced]` — leaching, SX, IX, and electrowinning fundamentals underlying §1.5–1.7. (paid)
- **Chagnes, A. & Świątowska, J. (eds.)** *Lithium Process Chemistry: Resources, Extraction, Batteries, and Recycling* (Elsevier, 2015). `[Advanced]` — a proper reference on lithium extraction chemistry (Part 3). (paid)
- **Spodumene sulphuric-acid-process review papers** (open-access, e.g., in *Minerals*/*Sustainability*/*Metals*, 2019–2024) — free, detailed, current on decrepitation/acid-roast/leach parameters. (free)
- **Equipment-vendor technical libraries** — Metso, FLSmidth, Weir, and FEECO (kilns/calciners) publish accurate free process notes and equipment descriptions; useful for machinery detail and current terminology. (free)
- **Journals for depth:** *Minerals Engineering* and *Hydrometallurgy* (processing/extraction); *Minerals* (MDPI, open access). (freemium/free)

---

## Part 6 — Calibration: what's settled vs contested in the engineering
- `[SETTLED]` The entire shared toolkit (comminution, flotation, thickening/filtration, leaching, SX/IX, electrowinning, roasting); the **zinc RLE flowsheet** end to end; the **spodumene sulphuric-acid process**; and **brine solar evaporation**. These are mature, textbook, globally deployed. Numbers vary by orebody `[ORE-SPECIFIC]` — always quote ranges (grades, recoveries, work indices, reagent dosages) rather than single points, because a real operator's numbers depend on their ore.
- `[EMERGING]` **HPGR and stirred/fine-grinding mills** displacing conventional circuits; **filtered/dry-stack tailings** at very large scale; **fluidized-bed spodumene calcination** and **acid-free lithium routes**; and comminution/kiln **electrification and decarbonization**. Real and advancing, but not yet universal.
- `[CONTESTED]` **DLE economics and technology-readiness at scale** — adsorption DLE is operating, but broad commercial viability across brine types is genuinely debated; treat bullish claims skeptically and always cite both a proponent and a skeptic. Likewise, novel **direct-to-hydroxide** and **chloride/alkaline** lithium flowsheets are promising but unproven at industrial scale.
- **The safest posture in conversation:** describe the standard flowsheet confidently, name the machinery and the operating-parameter *ranges*, and flag the emerging/contested alternatives as exactly that. Overstating DLE or a novel flowsheet as "solved" is the fastest way to sound like someone who read a press release rather than a plant.