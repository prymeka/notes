# A Self-Study Curriculum & Reading List in Marketing for an Advanced Autodidact

## TL;DR
- **A phased, sector-agnostic curriculum is the right structure**: eleven phases (0–10) moving from foundations → strategy/branding → consumer psychology → the marketing mix → digital/growth → measurement (conceptual) → contemporary landscape → capstone. A four-item MVP fast-path reaches real fluency in ~10–12 weeks; the full arc runs ~9–12 months part-time.
- **The single most important intellectual move for this learner is to hold two rival schools in tension**: the classical Kotler/Aaker "differentiate and build loyalty" tradition versus the empirical Ehrenberg-Bass/Byron Sharp school ("mental & physical availability, double jeopardy, light buyers, penetration over loyalty"). Most textbooks teach only the first; the modern evidence base substantially favors the second. This is CONTESTED and is the spine of the curriculum.
- **Treat all analytics conceptually and cross-reference your existing quant tracks**: attribution, marketing-mix modeling, CLV, incrementality and A/B testing are best learned here as *what/when/why/pitfalls*, deferring the math to your ML/causal-inference tracks; likewise route consumer-psychology depth to your behavioral-economics track and ad-auction/competitive-strategy depth to your game-theory track.

## Key Findings

**On canon and editions (verified):** The core "spine" texts are current and identifiable. Kotler/Keller/Chernev *Marketing Management* is now in its **17th edition (2022, ISBN-13 9780138184889 for the Pearson+ eText; a "2024 update" exists)**, with the **16th Global Edition** still widely used. Byron Sharp's *How Brands Grow* (2010) and Romaniuk & Sharp's *How Brands Grow Part 2* (**Revised Edition, Oxford University Press, 2021**) are the empirical-school anchors. Keller/Swaminathan *Strategic Brand Management* is in its **5th edition (2020)**. Chaffey & Ellis-Chadwick *Digital Marketing* is in its **8th edition (Pearson, 2022)**. Cialdini's *Influence* is best read in the **New and Expanded edition (2021)**, which adds a seventh principle, Unity. All are paywalled trade/textbooks.

**On free/open resources (verified):** **OpenStax *Principles of Marketing*** (2022, authors Gomez Albrecht, Green, Hoffman; CC-licensed) is a genuinely free, comprehensive intro text with a built-in semester-long marketing-plan project template — an ideal non-technical backbone. Wharton's **"Introduction to Marketing"** on Coursera (Kotler-tradition faculty) is **free to audit**. Levitt's *Marketing Myopia* (HBR 1960) and Vargo & Lusch's *Service-Dominant Logic* (Journal of Marketing 2004) are seminal articles findable in full-text PDF.

**On the live debates:** Beyond the classical-vs-empirical split, the **brand-building vs performance ("60/40") debate** (Binet & Field, IPA, 2013) and the **attribution wars** are the field's other flashpoints. The measurement world in 2025–26 has decisively pivoted away from user-level multi-touch attribution (post-Apple ATT and cookie disruption) toward a "triangulation" of **marketing-mix modeling + incrementality experiments + attribution** — a shift that plays directly to your causal-inference strengths.

**On time-sensitive items (flag for verification):** Google's third-party-cookie saga reversed twice — it **abandoned forced deprecation in July 2024** and, on **April 22, 2025, announced it would not introduce a standalone consent prompt in Chrome**, leaving third-party cookies enabled by default. Then, on **October 17, 2025, Google VP of Privacy Sandbox Anthony Chavez confirmed retirement of the remaining Privacy Sandbox APIs** (Topics, Protected Audience/PAAPI, Attribution Reporting, etc.) for Chrome and Android — as the UK Competition and Markets Authority released Google from its Sandbox commitments — with deprecation set for Chrome M144 (January 2026) and removal in M150 (July 2026). Retail media (led by Amazon) and generative AI in marketing are the fastest-moving areas and are tagged HYPE-WATCH where claims outrun evidence.

## Details

### The field's core intellectual tensions (learn these as the organizing spine)

1. **Classical school (Kotler, Keller, Aaker, Ries & Trout) vs. Empirical/Ehrenberg-Bass school (Byron Sharp, Jenni Romaniuk).** [CONTESTED] The classical tradition emphasizes segmentation, differentiation, brand loyalty, and positioning as psychological battle. The Ehrenberg-Bass school argues from repeated empirical regularities that brands grow primarily by increasing **penetration** (reaching more light/occasional buyers), that **loyalty metrics are largely a by-product of market share** (the "double jeopardy law"), and that the job of marketing is building **mental availability** (being easy to think of) and **physical availability** (being easy to buy) plus **distinctive brand assets**, rather than persuasion-through-differentiation. The empirical laws (double jeopardy, duplication of purchase, the Pareto/60-20 pattern, natural monopoly) are SETTLED as descriptive regularities; the strategic *prescription* to de-emphasize differentiation and loyalty is CONTESTED. This learner should read both and treat the tension as unresolved-but-evidence-weighted.

2. **Brand-building vs. performance marketing — the "60/40 rule."** [CONTESTED] Les Binet and Peter Field, analyzing the IPA Databank (*The Long and the Short of It*, IPA, 2013), found that the most effective campaigns allocated roughly **60% of budget to long-term brand building and 40% to short-term sales activation**; their follow-up, *Effectiveness in Context* (IPA, 2018), refined the optimum split to **62:38 brand:activation**. The ratio flexes by category and brand maturity — more brand-heavy for new/low-share brands, and a tilt toward activation (**~46% brand / 54% activation, found for B2B by the LinkedIn B2B Institute in 2019**). The headline ratio is an empirical average, not a law, and is often misapplied as dogma — flag it CONTESTED.

3. **Marketing as art vs. science.** [OPEN] The discipline is genuinely split between creativity/craft (positioning, storytelling, brand) and measurement/econometrics. This learner's edge is the science side; the deliberate goal of this curriculum is to build the *craft/conceptual* muscle he lacks.

4. **The attribution wars & the measurement pivot.** [CONTESTED→shifting toward SETTLED] User-level multi-touch and last-click attribution have been undermined by privacy changes (Apple's App Tracking Transparency, iOS 14.5, April 2021; cookie disruption). The field is converging on **triangulation**: marketing-mix modeling (MMM) for strategic breadth, incrementality/geo experiments for causal ground truth, and attribution for tactical in-flight optimization. Angelina Eng (VP, Measurement Center, IAB) frames it directly: "The real power in measurement isn't choosing between MMM, attribution, and incrementality. It's triangulating across all three." Open-source MMM tooling now anchors this shift — **Google's Meridian** (announced March 2024; made generally available January 29, 2025; open-source, Bayesian, successor to LightweightMMM) and **Meta's Robyn** (released 2020, ridge-regression/evolutionary). Rick Bruner (CEO, Central Control) captures the incrementality view: randomized geo experiments "provide deterministic results without personal data or expensive infrastructure like user ID graphs, tracking pixels or clean rooms."

### Phase-by-phase curriculum (FULL ARC)

**Phase 0 — Orientation & the shape of the discipline (1 week)**
- *Goal:* Build a mental map of marketing's sub-fields and vocabulary before deep reading.
- *Prerequisites:* None.
- *Primary:* OpenStax *Principles of Marketing* (2022), Unit 1 (free). AMA current definition of marketing ("the activity, set of institutions, and processes for creating, communicating, delivering, and exchanging offerings that have value for customers, clients, partners, and society at large" — approved 2013, reaffirmed on periodic review). [SETTLED]
- *Supplementary:* Skim the table of contents of Kotler/Keller *Marketing Management* 16th/17th ed. to see the "managerial" ontology.
- *Project:* Write a 1-page "map of marketing" taxonomy in your own words, tagging which sub-areas overlap your existing quant tracks. *Deliverable:* the map.
- *Time:* 1 week.

**Phase 1 — Foundations & history of marketing thought (3–4 weeks)**
- *Goal:* Understand how the marketing concept evolved (production → product → selling → marketing → societal/relationship/digital eras) and read the seminal primary sources.
- *Prerequisites:* Phase 0.
- *Primary readings:*
  - Theodore Levitt, "Marketing Myopia," *Harvard Business Review*, 1960 (reprinted "Best of HBR," 2004). [SETTLED as canon] Free PDFs circulate; the authoritative version is paywalled at HBR.
  - Vargo & Lusch, "Evolving to a New Dominant Logic for Marketing," *Journal of Marketing*, 68(1), 2004, pp. 1–17 (DOI 10.1509/jmkg.68.1.1.24036). [CONTESTED — influential paradigm, not universally adopted] Free author-hosted PDFs exist; journal version paywalled.
  - OpenStax *Principles of Marketing*, chapters on marketing concept & strategic planning (free).
- *Supplementary:* Wroe Alderson (functionalist tradition — read a secondary summary rather than the primary, which is dense); a short piece on the AMA definition's history (1935 → 1985 → 2004 → 2007 → 2013 revisions).
- *Project:* Write a 1,500-word essay tracing one modern company through the "eras" lens and arguing whether Levitt's myopia thesis applies to it today. *Deliverable:* essay.
- *Time:* 3–4 weeks.

**Phase 2 — Marketing strategy & the classical canon, incl. the great tension (5–6 weeks)**
- *Goal:* Master STP (segmentation, targeting, positioning), the marketing mix (4Ps/7Ps), competitive strategy, and confront the classical-vs-empirical debate head-on.
- *Prerequisites:* Phase 1.
- *Primary readings:*
  - Kotler/Keller/Chernev, *Marketing Management*, 16th Global or 17th ed. — chapters on strategy, STP, and the marketing mix. [classical canon]
  - Al Ries & Jack Trout, *Positioning: The Battle for Your Mind* (20th Anniversary ed., McGraw-Hill, 2001). [SETTLED as canon]
  - Byron Sharp, *How Brands Grow* (Oxford University Press, 2010) **and** Romaniuk & Sharp, *How Brands Grow Part 2*, Revised Edition (OUP, 2021). [empirical school — CONTESTED prescriptions, SETTLED empirical laws]
  - Michael Porter, *Competitive Strategy* (1980) and *Competitive Advantage* (1985) — read the five forces and value chain conceptually (secondary summaries acceptable given your strategy needs). [SETTLED as canon]
- *Supplementary:* Ansoff matrix (growth-vector framework, 1957 — read a summary); W. Chan Kim & Renée Mauborgne, *Blue Ocean Strategy* (Expanded Edition, Harvard Business Review Press, 2015). [CONTESTED — popular, critiqued for selection-on-the-dependent-variable]
- *Cross-references:* Route deep **competitive-strategy / game-theory** foundations (Nash equilibria, entry deterrence, auction theory) to your game-theory track; here treat five forces and positioning as managerial heuristics.
- *Project:* Choose a real product and (a) write a one-sentence positioning statement, (b) build a **perceptual map** (2×2, spreadsheet or hand-drawn) plotting it against 5–6 competitors, and (c) write a 2-page memo arguing how the Ehrenberg-Bass lens would change the strategy versus the classical lens. *Deliverable:* positioning statement + perceptual map + memo.
- *Time:* 5–6 weeks.

**Phase 3 — Consumer behavior & psychology (4 weeks)**
- *Goal:* Understand decision processes, perception, attitudes, motivation, involvement, and the psychology of persuasion — at a craft level.
- *Prerequisites:* Phase 1.
- *Primary readings:*
  - Robert Cialdini, *Influence: The Psychology of Persuasion*, New and Expanded edition (Harper Business, 2021) — seven principles: reciprocity, commitment/consistency, social proof, authority, liking, scarcity, unity. [SETTLED as accessible anchor; individual effect sizes CONTESTED given replication debates in social psych]
  - Michael Solomon, *Consumer Behavior: Buying, Having, and Being* (15th ed., Pearson — the current edition; the 13th ed. is also widely available) OR Hoyer & MacInnis, *Consumer Behavior* — read one, conceptually.
  - OpenStax *Principles of Marketing*, consumer & B2B buying-behavior chapters (free).
- *Cross-references:* Defer the deep decision-science foundations (prospect theory, heuristics & biases, dual-process/System 1–2, nudging) to your **behavioral-economics track**; here focus on how marketers operationalize them.
- *Project:* Conduct a "consumer decision journey" teardown of your own recent considered purchase, mapping need recognition → search → evaluation → purchase → post-purchase, and label which Cialdini principles and biases the sellers used. *Deliverable:* annotated journey map (2–3 pages).
- *Time:* 4 weeks.

**Phase 4 — Branding, product, and pricing (5 weeks)**
- *Goal:* Master brand equity models, brand architecture/identity, product life cycle, new-product development, diffusion, and pricing strategy conceptually.
- *Prerequisites:* Phases 2–3.
- *Primary readings:*
  - Kevin Lane Keller (& Swaminathan), *Strategic Brand Management*, 5th ed. (Pearson, 2020) — customer-based brand equity (CBBE) pyramid: salience → performance/imagery → judgments/feelings → resonance. [SETTLED as canon]
  - David Aaker, *Managing Brand Equity* (Free Press, 1991) and/or *Building Strong Brands* (1996) — brand-equity dimensions (awareness, associations, perceived quality, loyalty). [SETTLED as canon]
  - Everett Rogers, *Diffusion of Innovations*, 5th ed. (Free Press, 2003) — adopter categories, S-curve. [SETTLED]
  - OpenStax chapters on product life cycle, NPD, and pricing (free); Kotler/Keller pricing chapter.
- *Supplementary:* A conceptual treatment of value-based vs. cost-plus vs. competitive pricing and psychological pricing.
- *Cross-references:* Defer deep **pricing psychology** (anchoring, decoy/asymmetric dominance, price-quality inference, willingness-to-pay elicitation) to your behavioral-economics track.
- *Project:* Conduct a **brand audit** of a chosen brand: map it onto Keller's CBBE pyramid and Aaker's dimensions, assess its distinctive brand assets (Ehrenberg-Bass lens), and recommend a positioning/architecture adjustment. *Deliverable:* 5–7 page brand audit.
- *Time:* 5 weeks.

**Phase 5 — Marketing communications (IMC) & advertising (3–4 weeks)**
- *Goal:* Understand advertising theory/effects, creative strategy, media planning, PR, sales promotion, and the brand-vs-performance spend debate.
- *Prerequisites:* Phases 2–4.
- *Primary readings:*
  - Les Binet & Peter Field, *The Long and the Short of It* (IPA, 2013) and *Effectiveness in Context* (IPA, 2018). [CONTESTED headline ratio; SETTLED that two distinct effects operate on different timescales]
  - Kotler/Keller IMC chapters; OpenStax IMC + promotion-mix chapters (free).
- *Supplementary:* The System1 and adam&eveDDB body of work on emotional advertising (secondary); classic hierarchy-of-effects models (read a summary — CONTESTED/dated).
- *Project:* **Critique a real campaign's IMC**: pick a current multi-channel campaign, deconstruct its objective (brand vs. activation), creative strategy, channel mix, and estimate where it sits on the 60/40 spectrum; argue what you'd change. *Deliverable:* 4–5 page campaign critique.
- *Time:* 3–4 weeks.

**Phase 6 — Digital marketing & the martech stack (4–5 weeks)**
- *Goal:* Get current, conceptual fluency across SEO, paid search/SEM, social, content, email, mobile, programmatic/display, and the martech stack.
- *Prerequisites:* Phase 5.
- *Primary readings:*
  - Chaffey & Ellis-Chadwick, *Digital Marketing*, 8th ed. (Pearson, 2022) — includes the RACE planning framework (Reach, Act, Convert, Engage). [current]
  - Avinash Kaushik, *Web Analytics 2.0* (Wiley, 2009) — conceptually excellent on segmentation and "actionable metrics," though platform specifics are dated. [dated on tools, SETTLED on philosophy]
- *Supplementary (free, vendor-run, verify currency):* **Google Skillshop / Google Digital Garage** and **Meta Blueprint** for platform mechanics (free; vendor-biased — HYPE-WATCH on their "best practice" claims).
- *Project:* Build a **digital-channel plan** for a chosen product using the RACE framework, specifying channel roles, example KPIs, and one measurable hypothesis per channel. *Deliverable:* channel plan (spreadsheet + 2-page narrative). Optional Python variant: pull a public SEO/keyword dataset and cluster query intent.
- *Time:* 4–5 weeks.

**Phase 7 — Performance & growth marketing (4 weeks)**
- *Goal:* Master conversion funnels, pirate metrics (AARRR), growth loops, retention/churn, virality, and product-led growth.
- *Prerequisites:* Phase 6.
- *Primary readings:*
  - Sean Ellis & Morgan Brown, *Hacking Growth* (Currency/Crown, 2017) — the growth-experimentation process. [SETTLED as practitioner canon]
  - Gabriel Weinberg & Justin Mares, *Traction* (Portfolio, 2015) — the 19 traction channels and the Bullseye Framework. [SETTLED as practitioner canon]
  - Dave McClure's **AARRR "pirate metrics"** (Acquisition, Activation, Retention, Referral, Revenue) — read the original framework and a modern critique. [SETTLED as framework]
- *Cross-references:* Route the *statistics* of experimentation, sequential testing, and uplift modeling to your ML/experimentation track; here focus on funnel/loop design and prioritization (e.g., ICE scoring).
- *Project:* **Design a growth-funnel model** for a chosen product: define the AARRR metrics, sketch at least one growth loop, and write a backlog of 10 prioritized growth experiments with hypotheses and success metrics. *Deliverable:* funnel model + experiment backlog (spreadsheet).
- *Time:* 4 weeks.

**Phase 8 — Marketing analytics & measurement (CONCEPTUAL) (3–4 weeks)**
- *Goal:* Understand marketing metrics/dashboards, ROMI, attribution models and the attribution wars, marketing-mix modeling, CLV, and incrementality/A-B testing — as concepts and pitfalls.
- *Prerequisites:* Phases 6–7.
- *Primary readings:*
  - Mark Jeffery, *Data-Driven Marketing: The 15 Metrics Everyone in Marketing Should Know* (Wiley, 2010; named AMA best marketing book of 2011) — ROMI, CLV, the metrics framework. [SETTLED conceptually; examples dated]
  - Kaushik, *Web Analytics 2.0* (measurement philosophy chapters).
  - Current landscape readings on the measurement pivot: Angelina Eng (IAB), "Why marketing measurement needs triangulation" (MarTech); Google's Meridian documentation (open-source MMM); an incrementality/geo-experiment primer (e.g., Rick Bruner, AdExchanger, Sept 2025).
- *Cross-references (critical):* This is where you *cross-reference your ML/causal-inference/experimentation track for all the mathematics*. Attribution ≈ credit assignment (understand last-click, linear, time-decay, position-based, and data-driven/Shapley-style models as concepts, and why they are correlational not causal); MMM ≈ regression/Bayesian time-series with adstock and saturation curves (Google Meridian is Bayesian; Meta Robyn is ridge-regression + evolutionary optimization); CLV ≈ probabilistic/discounted-cashflow modeling; incrementality ≈ randomized/geo experiments (your home turf, treated as ground truth). Learn *pitfalls*: selection bias, correlation-vs-causation, over-attribution to bottom-funnel, Simpson's paradox in channel roll-ups.
- *Project:* Write a **measurement-strategy white paper** for a chosen company: specify which of MMM/incrementality/attribution answers which question (the "triangulation" frame), design one geo-holdout experiment (conceptually), and list the top five pitfalls you'd guard against. *Deliverable:* 5-page white paper. Optional Python variant: simulate adstock/saturation transforms on synthetic spend data.
- *Time:* 3–4 weeks.

**Phase 9 — Services, relationship marketing/CRM, and B2B vs B2C (2–3 weeks)**
- *Goal:* Cover services marketing (intangibility, the gaps model, servicescapes), relationship marketing/CRM, and the general B2B-vs-B2C distinctions (not sector specialization).
- *Prerequisites:* Phases 2–4.
- *Primary readings:* OpenStax services & CRM chapters (free); a services-marketing treatment of the **SERVQUAL/Gaps model** (Parasuraman, Zeithaml, Berry). Vargo & Lusch's service-dominant logic (revisit from Phase 1) frames this well. B2B fundamentals: buying centers, longer cycles, and the **"95-5 rule"** — the heuristic (Prof. John Dawes, Ehrenberg-Bass Institute, for the LinkedIn B2B Institute, May 2021) that at any given time only ~5% of B2B buyers are in-market, derived from roughly five-year corporate switching cycles (~20%/year, ~5%/quarter). Dawes himself cautions it is "not meant to be a precise rule… a heuristic." [CONTESTED-but-evidence-backed]
- *Project:* Write a 3-page comparison of how you'd adapt a single product's marketing plan for a B2C vs. a B2B buyer. *Deliverable:* comparison memo.
- *Time:* 2–3 weeks.

**Phase 10 — Contemporary & emerging landscape + Capstone (4–5 weeks)**
- *Goal:* Get current on privacy/data, AI in marketing, creator economy, and retail media; then integrate everything into a full marketing plan.
- *Prerequisites:* All prior phases.
- *Primary readings / landscape (all TIME-SENSITIVE — verify before relying):*
  - **Privacy & data:** GDPR fundamentals; the third-party-cookie saga (Google abandoned forced deprecation July 2024; on April 22, 2025 announced no standalone Chrome consent prompt, leaving cookies enabled by default; on October 17, 2025 confirmed retirement of the remaining Privacy Sandbox APIs — Topics, Protected Audience/PAAPI, Attribution Reporting — with deprecation at Chrome M144 in January 2026 and removal at M150 in July 2026, as the UK CMA released Google from its Sandbox commitments). First-party data strategies and consent management are now the durable play. [privacy law SETTLED; cookie/platform status TIME-SENSITIVE]
  - **AI / generative AI in marketing:** [HYPE-WATCH] Adoption is real but uneven — the Spring 2024 CMO Survey put gen-AI use at ~7% of marketing activities, rising fast into everyday workflows by 2025; back-office uses (data analysis, market research, creative variation) are outpacing headline consumer-facing stunts, and ROI measurement lags adoption (only ~49% of marketers measured AI ROI in 2025 per Jasper's survey). Treat "agentic marketing" claims as speculative.
  - **Retail media networks:** [partly HYPE-WATCH] The fastest-growing ad channel, dominated by Amazon. US retail media ad spend was **$60.32 billion in 2025 and is forecast at $71.09 billion in 2026** (EMARKETER, December 2025 forecast); Amazon holds more than half of global retail media spend and accounted for **more than 75% of US retail media ad spending in 2025** (EMARKETER). Re-verify figures before citing.
  - **Influencer/creator-economy marketing:** conceptually cover creator selection, disclosure/FTC rules, and measurement challenges.
- *Capstone project:* Build a **complete marketing plan** for a chosen product/company integrating STP, positioning, brand strategy, the marketing mix, an IMC + digital/growth plan, a measurement strategy, and a privacy-aware data plan. Use the OpenStax marketing-plan template as scaffolding. *Deliverable:* 15–25 page marketing plan.
- *Time:* 4–5 weeks.

### The MVP fast-path (minimum core to real fluency, ~10–12 weeks)
For a quant-strong autodidact who wants fluency fast, read these four in order and do three projects:
1. **OpenStax *Principles of Marketing*** (free) — skim for the whole-discipline scaffold (2–3 weeks). → *Project: the "map of marketing."*
2. **Byron Sharp, *How Brands Grow* (2010)** — the single highest-leverage book to inoculate against folk-marketing myths (2 weeks). → *Project: brand audit through the mental/physical availability lens.*
3. **Cialdini, *Influence* (2021 ed.)** — consumer psychology anchor (2 weeks).
4. **Binet & Field, *The Long and the Short of It* (2013)** + **Ellis & Brown, *Hacking Growth* (2017)** — the brand-vs-performance frame plus the growth operating model (3–4 weeks). → *Project: positioning statement + perceptual map + a growth-funnel model.*
Optionally add Chaffey & Ellis-Chadwick chapters for digital currency. This delivers the bulk of practical fluency; the full arc adds depth, primary sources, and the measurement/contemporary layers.

### Dependency map
```
Phase 0 (Orientation)
   │
Phase 1 (Foundations/History)
   │
   ├── Phase 2 (Strategy & Canon) ──────────────┐
   │        │  ⇄ GAME THEORY track (competitive strategy, auctions)
   │        ▼
   ├── Phase 3 (Consumer Behavior)              │
   │        ⇄ BEHAVIORAL ECONOMICS track (decision science)
   │        ▼
   ├── Phase 4 (Branding/Product/Pricing) ◀─────┘
   │        ⇄ BEHAVIORAL ECONOMICS track (pricing psychology)
   │        ▼
   ├── Phase 5 (IMC & Advertising)
   │        ▼
   ├── Phase 6 (Digital & Martech)
   │        ▼
   ├── Phase 7 (Performance/Growth)
   │        ⇄ ML/EXPERIMENTATION track (test design, uplift)
   │        ▼
   ├── Phase 8 (Analytics/Measurement, conceptual)
   │        ⇄ ML/CAUSAL-INFERENCE track (attribution math, MMM, CLV, incrementality)
   │        ▼
   ├── Phase 9 (Services/CRM/B2B)
   │        ▼
   └── Phase 10 (Contemporary + Capstone)
```
Cross-reference rule of thumb: whenever a phase reaches a mathematical or deep-decision-science layer, *stop and route to the relevant existing track* rather than re-deriving it here.

### Key academic journals to be aware of
*Journal of Marketing* and *Journal of Marketing Research* (both AMA; the former more managerial/theory, the latter more methodological), *Marketing Science* (INFORMS; quantitative/modeling — the closest to your quant home), and *Journal of Consumer Research* (consumer behavior/psychology). Use these to go deeper than the textbooks in Phases 2, 3, and 8.

## Recommendations
1. **Start with the MVP fast-path immediately** (OpenStax → Sharp → Cialdini → Binet & Field + Hacking Growth). This is the highest-ROI sequence and prevents you from absorbing folk-marketing myths before you have the empirical antibodies. Benchmark to advance: you can explain double jeopardy, mental/physical availability, and the 60/40 debate to a skeptical colleague without notes.
2. **Read the two schools in deliberate opposition.** Whenever a classical text (Kotler, Aaker) asserts a loyalty/differentiation claim, check it against the Ehrenberg-Bass evidence. If you find yourself accepting either school wholesale, you've stopped thinking — the honest position is evidence-weighted tension.
3. **Deliberately under-invest in the math, over-invest in the craft.** For every analytics concept (attribution, MMM, CLV, incrementality), spend your time on *when/why/pitfalls* and route the derivations to your existing tracks. Your risk is not under-quant; it's under-craft.
4. **Do every project — they are the point.** For a non-technical track, the deliverables (positioning statement, perceptual map, brand audit, campaign critique, growth-funnel model, measurement white paper, full marketing plan) are where fluency is forged. Keep them in a portfolio.
5. **Timebox the contemporary/time-sensitive material and re-verify quarterly.** Privacy law, cookie/platform status, AI-in-marketing, and retail-media figures decay fast. Do a verification pass before relying on any specific claim in Phase 10.
6. **Thresholds that would change the plan:** if you find the classical texts too shallow for your taste, substitute primary journal articles (Journal of Marketing, JMR, Marketing Science, JCR). If you need a credential, convert the audited Coursera specializations (Wharton, Kellogg, Darden/UVA) into paid certificates.

## Caveats
- **Editions:** The 17th edition of Kotler/Keller/Chernev *Marketing Management* (2022, with a 2024 update) is current; the 16th Global Edition remains widely used and is fine. Solomon *Consumer Behavior* is at the 15th edition (US); the 13th is common secondhand. *How Brands Grow Part 2* should be the 2021 Revised Edition (Oxford). Verify the specific ISBN before purchase, as global/regional editions differ (e.g., Keller's 5th ed. is a Pearson India/Global co-authored edition).
- **Free vs. paywalled:** OpenStax, the Levitt and Vargo & Lusch PDFs, and audited Coursera courses are free; Google Skillshop/Digital Garage and Meta Blueprint are free but vendor-biased. All the trade textbooks (Kotler, Keller, Aaker, Sharp, Solomon, Chaffey, Cialdini, Jeffery, Kaushik) are paywalled.
- **Contested prescriptions:** The Ehrenberg-Bass prescriptions and the 60/40 (or 62/38) ratio are evidence-backed but not universally accepted; present them as strong hypotheses, not settled law. The 95-5 rule is an explicitly acknowledged heuristic, not a measured constant.
- **Time-sensitive:** All Phase 10 platform/privacy/AI/retail-media specifics need re-verification; the cookie situation in particular has reversed multiple times (July 2024, April 2025, October 2025), and the Privacy Sandbox removal milestones (Chrome M144/M150, 2026) are announced-but-future-dated.
- **Replication caveat:** Some consumer-psychology effect sizes (Cialdini's principles among them) sit within social psychology's broader replication debates; treat individual effects as directional.
- **Source quality:** Several landscape claims come from vendor blogs with commercial interests (measurement vendors, martech platforms); I have flagged these and leaned on IAB, Google/Meta official docs, Forrester, EMARKETER, and academic sources where possible. The reported claim that "Meta is winding down Robyn" rests on anonymous sourcing (AdExchanger) and is unconfirmed.