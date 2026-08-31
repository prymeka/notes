# How AI Changed Testing: A Reading Curriculum

**Companion to:** *Testing & Testable Code: A Curriculum* (the prior doc). This one is research-paper-led, tracing how machine learning — and specifically LLMs — reshaped automated test generation, plus the practitioner debate over how to use these tools well.

**Target profile:** SWE, ~2 yrs Python, intermediate; ML engineer by trade (fraud detection), so the ML-pipeline thread is weighted accordingly.
**Scope:** brief pre-LLM history → LLM test generation canon (2022–2026) → agentic/autonomous test+repair → ML/data-pipeline-specific testing with LLMs → human opinion on tooling (skeptical, balanced, enthusiast).
**Budget:** ~8 hrs/week, intensive.
**Total horizon:** ~10–12 weeks for the full path; ~5 weeks for the Minimum Viable Path (see end).
**Centre of gravity:** current SOTA (2023–2026), with just enough history to make the progress legible.

---

## How to read this document

- **Primary** = read in full, it's load-bearing for the narrative.
- **Supplementary** = read selectively / skim for the delta over the primary.
- **Optional** = depth if the thread grabs you or is directly job-relevant.
- **[FREE]** = legally free (arXiv, author-hosted, open-access). Almost everything here is on arXiv.
- Citations give authors, title, venue, year, and arXiv ID / DOI where available.
- **A note on velocity:** this is the fastest-moving area in software engineering research right now. Conference-published anchors (ICSE, FSE, TSE, NeurIPS) are stable; arXiv preprints from the last 18 months are *snapshots of a moving target* — read them for ideas and framing, not as settled fact. The two systematic reviews in Phase 1 are your map for finding what's newer when you read this.
- Threads are loosely sequential but **Phase 5 (opinion)** can and should be read in parallel throughout — the essays are short and they're the interpretive glue. The history (Phase 0) is deliberately compressed.

---

## A one-paragraph orientation

Automated test generation is old; what changed is the *generator*. The pre-LLM state of the art was **search-based** (evolutionary algorithms optimizing coverage, e.g. EvoSuite/Pynguin) and **symbolic/concolic** execution — both produce high-coverage tests but with mechanical, hard-to-read assertions and a fundamental weakness on the *oracle problem* (knowing what the right answer is). LLMs flipped the trade-off: they write natural, readable, human-like tests with plausible assertions, but with weaker coverage guarantees and a new failure mode — **confidently wrong assertions** that pin existing behavior (bugs included) rather than intended behavior. The research arc from 2022 onward is largely about **closing that gap**: hybridizing LLMs with search (CodaMOSA), feeding coverage back into prompts (CoverUp), adding generate-run-repair loops (TestART), wrapping everything in *assurance filters* so only verifiably-improving tests survive (Meta's TestGen-LLM), and finally embedding test generation inside autonomous agents that fix bugs (SWT-bench, agentic program repair). The practitioner debate, running in parallel, is about one thing: an LLM that derives tests *from your code* transcribes its behavior rather than verifying its intent — so the human's job shifts from *writing* tests to *deciding what correct means* and *measuring whether the tests actually catch bugs* (mutation testing recurs as the answer).

---

## Phase 0 — The pre-LLM baseline (Week 1, ~6 hrs)

**Goal:** Understand what "automated test generation" meant *before* LLMs, so the LLM contribution is legible as a specific trade-off rather than magic. Keep this brief — it's preamble.

**Primary**
- Gordon Fraser & Andrea Arcuri, *"EvoSuite: Automatic Test Suite Generation for Object-Oriented Software"*, ESEC/FSE 2011. [FREE] https://www.evosuite.org/wp-content/papercite-data/pdf/esecfse11.pdf — the reference point for **search-based software testing (SBST)**: evolve whole test suites to maximize a coverage criterion, then suggest assertions that capture observed behavior. Note the two enduring limitations you'll see LLMs attack: (1) mechanical, low-readability assertions, and (2) the assertions encode *current* behavior, not *intended* behavior (the oracle problem).
- Stephan Lukasczyk & Gordon Fraser, *"Pynguin: Automated Unit Test Generation for Python"*, ICSE 2022 Companion. [FREE] https://arxiv.org/abs/2202.05218 — the Python SBST tool that later LLM-hybrid work (CodaMOSA, CoverUp) builds on or benchmarks against. Relevant because it's *your* language; skim to see how SBST plays out in a duck-typed setting (harder than Java — no static types to constrain inputs).

**Supplementary**
- Earl T. Barr, Mark Harman, Phil McMinn, Muzammil Shahbaz & Shin Yoo, *"The Oracle Problem in Software Testing: A Survey"*, IEEE TSE 2015. [FREE] https://discovery.ucl.ac.uk/id/eprint/1471263/ — the canonical statement of *the* hard problem: generating inputs is comparatively easy; knowing the correct output is the bottleneck. This single concept frames the entire LLM-testing literature — LLMs are, in effect, a heuristic oracle, with all the risk that implies. **If you read one thing in Phase 0, read this** (at least the framing sections).
- Sina Shamshiri, René Just, José Miguel Rojas, Gordon Fraser, Phil McMinn & Andrea Arcuri, *"Do Automatically Generated Unit Tests Find Real Faults? An Empirical Study of Effectiveness and Challenges"*, ASE 2015. [FREE] https://www.lines.cse.usf.edu/ — sobering baseline: high coverage ≠ finding real bugs. The same critique resurfaces, almost verbatim, against LLM-generated tests a decade later. (Search the title; it's widely mirrored.)

**Takeaway to carry forward:** every LLM-testing paper is implicitly answering "we generate *readable* tests with *plausible* oracles — but are the oracles *correct*, and do we still get *coverage*?" Hold those two axes (readability/oracle-quality vs. coverage) as your evaluation lens for everything below.

---

## Phase 1 — Get the map: two systematic reviews (Week 1–2, ~6 hrs)

**Goal:** Before diving into individual papers, get the lay of the land from two recent surveys. These are your index and your means of finding what's newer than this document.

**Primary**
- Junjie Wang, Yuchao Huang, Chunyang Chen, Zhe Liu, Song Wang & Qing Wang, *"Software Testing with Large Language Models: Survey, Landscape, and Vision"*, IEEE TSE 50(4), 2024. [FREE] https://arxiv.org/abs/2307.07221 — the most-cited broad survey; organizes the field by testing activity (unit test generation, test oracle generation, debugging, etc.) and by how the LLM is used. Read for the taxonomy and the vocabulary.
- Wendkûuni C. Ouédraogo et al. (or the iSEngLab group), *"Large Language Models for Unit Testing: A Systematic Literature Review"*, 2025. [FREE] https://arxiv.org/abs/2506.15227 — narrower and more recent, focused exactly on unit testing (your interest). Use it to triage which primary papers below matter most and to spot 2025+ work this doc may have missed.

**Supplementary**
- The living bibliography: iSEngLab, *"Awesome-LLM4SE: A Survey on Large Language Models for Software Engineering"*. [FREE] https://github.com/iSEngLab/AwesomeLLM4SE — a continuously-updated GitHub list with a large testing section. **This is how you keep this curriculum current** — check it for anything post-dating this doc.

**How to use this phase:** skim both surveys' section structure and tables, read the unit-testing and oracle-generation sections closely, and bookmark 5–8 primary papers they cite that aren't already below. Don't try to read every cited paper — the surveys exist so you don't have to.

---

## Phase 2 — The LLM unit-test-generation canon (Weeks 3–5, ~24 hrs)

**Goal:** The historical-technical spine. Read these roughly in order; together they tell the story of the field maturing from "can an LLM write a test?" (2022) through "here's how to make them reliable" (2024–25).

**Primary — read in this sequence:**

1. **The first credible empirical study.** Max Schäfer, Sarah Nadi, Aryaz Eghbali & Frank Tip, *"An Empirical Evaluation of Using Large Language Models for Automated Unit Test Generation"* (TestPilot), IEEE TSE 2023 (preprint 2023). [FREE] https://arxiv.org/abs/2302.06527 — landmark: shows a zero-training, prompt-with-signature-and-docs approach (TestPilot) beats prior feedback-directed JS test generation on coverage, and introduces the now-standard **generate → run → if-fail-repair** loop. Establishes that off-the-shelf LLMs are genuinely useful for tests. Note the error taxonomy (assertion errors dominate) — the seed of the whole "assertion correctness" concern.

2. **The honest look at quality.** Zhiqiang Yuan et al., *"No More Manual Tests? Evaluating and Improving ChatGPT for Unit Test Generation"* (ChatTester), 2023 (later Proc. ACM SE 2024). [FREE] https://arxiv.org/abs/2305.04207 — the first systematic audit of *correctness, sufficiency, readability, usability* of ChatGPT tests. Key finding to internalize: passing tests resemble human ones, but a large fraction **don't compile or have wrong assertions**, and the dominant failure is incorrect assertions. Proposes self-improvement (ChatTester). This is the empirical backbone of the skeptics' case in Phase 5.

3. **The hybrid breakthrough — LLM + search.** Caroline Lemieux, Jeevana Priya Inala, Shuvendu K. Lahiri & Siddhartha Sen, *"CodaMOSA: Escaping Coverage Plateaus in Test Generation with Pre-Trained Large Language Models"*, ICSE 2023. [FREE] https://www.microsoft.com/en-us/research/publication/codamosa-escaping-coverage-plateaus-in-test-generation-with-pre-trained-large-language-models/ — the key *architectural* idea: run SBST (Pynguin) until coverage stalls, then ask an LLM for example tests targeting under-covered functions, and re-seed the search with them. Marries SBST's coverage rigor to the LLM's ability to synthesize meaningful inputs. The template for "neither alone, but both" — and it's Python-based. (Code: https://github.com/microsoft/codamosa)

4. **Coverage-guided prompting.** Juan Altmayer Pizzorno & Emery D. Berger, *"CoverUp: Coverage-Guided LLM-Based Test Generation"*, FSE 2025 (preprint 2024). [FREE] https://arxiv.org/abs/2403.16218 — feeds *which lines/branches are still uncovered* directly into the prompt, iterating to drive coverage up. Compares directly to CodaMOSA. Read as the refinement of the coverage-closing idea, and again **Python-native** — closest to something you'd actually run on your own code.

5. **The generate-and-repair co-evolution.** Siqi Gu et al., *"TestART: Improving LLM-Based Unit Testing via Co-Evolution of Automated Generation and Repair Iteration"*, 2024 (v6 2025). [FREE] https://arxiv.org/abs/2408.03095 — formalizes the loop: generate, run, capture the error, *repair using templated fixes for common error classes*, repeat — explicitly engineered around LLM failure modes (faithfulness hallucination, repetition suppression). The bridge from Phase 2 into the agentic Phase 3.

**Supplementary**
- Mohammed Latif Siddiq et al., *"Using Large Language Models to Generate JUnit Tests: An Empirical Study"*, EASE 2024. [FREE] https://arxiv.org/abs/2305.00418 — multi-model (Codex, GPT-3.5, StarCoder) study on HumanEval and EvoSuite's SF110; documents early coverage/compilability/reliability challenges. Useful as the "where we started" data point.
- Benjamin Steenhoek, Michele Tufano, Neel Sundaresan & Alexey Svyatkovskiy, *"Reinforcement Learning from Automatic Feedback for High-Quality Unit Test Generation"*, 2023. [FREE] https://arxiv.org/abs/2310.02368 — RL-from-execution-feedback to push test quality (not just coverage). Optional unless the training-time angle interests you.
- *"Test Wars: A Comparative Study of SBST, Symbolic Execution, and LLM-Based Approaches to Unit Test Generation"*, 2025. [FREE] https://arxiv.org/abs/2501.10200 — recent head-to-head of the three paradigms; a clean way to see the current trade-off frontier in one place.

**Calibration note:** results in this phase are reported against benchmarks (HumanEval, SF110, Defects4J, npm packages) that suffer from **data-leakage risk** — popular open-source code is likely in the model's training set, inflating apparent performance versus your proprietary fraud code. Treat coverage/pass numbers as upper bounds, not what you'd see internally. The Phase 1 SLR discusses this explicitly.

---

## Phase 3 — Agentic & industrial-scale: assurance, repair, autonomy (Weeks 6–7, ~16 hrs)

**Goal:** The current frontier and the part most relevant to where tooling is heading. Two sub-threads: (a) **assurance** — making generated tests trustworthy enough to deploy at scale; (b) **agency** — test generation as one move inside an autonomous bug-fixing loop.

**Primary**

*Assurance / industrial deployment:*
- Nadia Alshahwan, Jubin Chheda, Anastasia Finogenova, Beliz Gokkaya, Mark Harman, Inna Harper, Alexandru Marginean, Shubho Sengupta & Eddy Wang (Meta), *"Automated Unit Test Improvement using Large Language Models at Meta"* (TestGen-LLM), FSE 2024 Companion (preprint 2024). [FREE] https://arxiv.org/abs/2402.09171 — **the most important industrial paper here.** The "Assured Offline LLMSE" idea: don't trust the LLM — wrap it in *filters* that discard any generated test unless it provably builds, passes reliably, and *measurably increases coverage* over the existing suite. Deployed at Instagram/Facebook test-a-thons; ~73% of surviving recommendations accepted by engineers. The reframe is crucial: the LLM proposes, a *verifier* disposes. Maps directly onto how you'd responsibly add LLM test generation to a regulated fraud pipeline.
- Nadia Alshahwan, Mark Harman, Alexandru Marginean, Shubho Sengupta & Eddy Wang, *"Assured LLM-Based Software Engineering"* (keynote), ICSE 2024 InteNSE workshop. [FREE] https://arxiv.org/abs/2402.04380 — the conceptual generalization of the above: a manifesto for *verifiable guarantees* around LLM-generated software artifacts. Short; read it for the principle.

*Agency / autonomous test + repair:*
- Niels Mündler, Mark Niklas Müller, Jingxuan He & Martin Vechev, *"SWT-Bench: Testing and Validating Real-World Bug-Fixes with Code Agents"*, NeurIPS 2024. [FREE] https://arxiv.org/abs/2406.12952 — the benchmark that shifted the question from "can an agent fix a bug?" (SWE-bench) to "can an agent *write a test that reproduces* the bug?" Introduces evaluating LLM agents on **test generation from issue reports**. The natural successor to SWE-bench and the anchor for the agentic thread.
- Pat Rondon, Renyao Wei, José Cambronero, Jürgen Cito, Aaron Sun, Siddhant Sanyam, Michele Tufano & Satish Chandra (Google), *"Evaluating Agent-Based Program Repair at Google"*, 2025. [FREE] https://arxiv.org/abs/2501.07531 — a second industrial data point (after Meta): autonomous agents using test-execution feedback to repair failures at scale. Read alongside TestGen-LLM to see the two big-tech approaches converging on "LLM in a loop with a verifier."

**Supplementary**
- Noor Nashid, Islem Bouzenia, Michael Pradel & Ali Mesbah, *"Issue2Test: Generating Reproducing Test Cases from Issue Reports"*, 2025. [FREE] https://arxiv.org/abs/2503.16320 — concrete instance of the SWT-bench problem: turn a natural-language bug report into a failing test. Directly relevant if you ever want an agent to reproduce a fraud-rule regression from a ticket.
- Konstantinos Kitsios, Marco Castelluccio & Alberto Bacchelli, *"Automated Generation of Issue-Reproducing Tests by Combining LLMs and Search-Based Testing"*, 2025. [FREE] https://arxiv.org/abs/2509.01616 — the CodaMOSA hybrid idea (LLM + search) applied to the agentic reproducing-test problem; nice closing-of-the-loop between Phases 2 and 3.

**Critical counterpoint (read here, it punctures the hype):**
- Jie Huang, Xinyun Chen, Swaroop Mishra, Huaixiu Steven Zheng, Adams Wei Yu, Xinying Song & Denny Zhou, *"Large Language Models Cannot Self-Correct Reasoning Yet"*, ICLR 2024. [FREE] https://arxiv.org/abs/2310.01798 — essential caveat for the whole "self-repair / co-evolution / agentic loop" thread: without an *external* signal (a real test execution, a verifier), LLMs are poor at correcting their own reasoning, and self-correction can even degrade output. This is *why* the assurance filters and execution feedback in TestGen-LLM / TestART / SWT-bench matter — the loop only works because something outside the model checks the work. Hold this against any claim of autonomous test correctness.

**Calibration note:** the agentic results are the least settled in this document — benchmark numbers move month to month and "agent" means different harnesses in different papers. Read for the *shape* of the approach (propose → execute → verify → iterate) and the *role of the external oracle*, not the leaderboard position.

---

## Phase 4 — Testing ML/data pipelines with (and against) LLMs (Weeks 8–9, ~16 hrs)

**Goal:** Your domain, and a genuinely distinct area. **Two directions that are easy to conflate — keep them separate:**
- **(A) Using LLMs to test ML/data systems** — generating data validations, test inputs, metamorphic relations for pipelines.
- **(B) Testing the ML/LLM systems themselves** — the older "ML testing" field, into which (A) is now bleeding.

This connects straight to Phase 4C of the prior curriculum (ML/data-pipeline testing) — read these as the AI-era extension of that.

**Primary — foundations of testing ML systems (so the LLM additions have a frame):**
- Jie M. Zhang, Mark Harman, Lei Ma & Yang Liu, *"Machine Learning Testing: Survey, Landscapes and Horizons"*, IEEE TSE 48(1), 2022. [FREE] https://arxiv.org/abs/1906.10742 — the canonical survey of how you test ML systems (test data, test oracles for non-deterministic models, metamorphic testing, the "no ground-truth oracle" problem). Predates the LLM wave but defines the vocabulary. **Read the metamorphic-testing and oracle sections closely** — they're the bridge to your SHAP/invariance work in the prior doc.
- Vincenzo Riccio, Gunel Jahangirova, Andrea Stocco, Nargiz Humbatova, Michael Weiss & Paolo Tonella, *"Testing Machine Learning Based Systems: A Systematic Mapping"*, Empirical Software Engineering 25, 2020. [FREE] https://arxiv.org/abs/2007.00808 — complementary map; good for seeing the breadth of ML-testing concerns (data, model, deployment) before LLMs entered.

**Primary — the metamorphic-testing thread (the key technique for oracle-free ML testing, now LLM-assisted):**
- Why this matters for you: when you have **no ground-truth oracle** (the norm in ML, including a fraud classifier where "correct" is fuzzy), you assert *relations between outputs* under input transformations — "permuting feature-column order must not change a tree model's prediction," "duplicating a row must not change learned statistics," "scaling a monotone feature must move the score in the expected direction." This is exactly the metamorphic / invariance / directional-expectation testing from the prior doc's 4C, and LLMs are now used to *propose candidate metamorphic relations*.
- *Metamorphic Testing of Deep Code Models: A Systematic Literature Review*, ACM TOSEM 2025. [FREE] https://arxiv.org/abs/2410.07516 (and the TOSEM version) — survey of metamorphic testing applied to code/ML models, including LLM-assisted relation discovery. Use as the index into this sub-field.

**Supplementary — LLMs generating tests/validations for data & ML pipelines:**
- Marco Tulio Ribeiro, Tongshuang Wu, Carlos Guestrin & Sameer Singh, *"Beyond Accuracy: Behavioral Testing of NLP Models with CheckList"*, ACL 2020 (best-paper). [FREE] https://aclanthology.org/2020.acl-main.442/ — already in the prior doc's 4C, but re-read it *here* through the AI lens: the invariance / directional-expectation / minimum-functionality taxonomy is precisely what LLM-generated behavioral tests now try to automate. The conceptual parent of "ask the LLM for failure-mode tests."
- *Validating LLM-Generated Programs with Metamorphic Prompt Testing*, 2024. [FREE] https://arxiv.org/abs/2406.06864 — when you can't compare against a ground-truth program (because the LLM *is* writing the program), use metamorphic relations over prompts to catch inconsistency. The technique generalizes to validating any generated artifact, including generated tests.
- *Tracking the Moving Target: A Framework for Continuous Evaluation of LLM Test Generation in Industry*, 2025. [FREE] https://arxiv.org/abs/2504.18985 — practical framing of the data-leakage and "benchmarks go stale" problems when you deploy LLM test generation in a real org; relevant to evaluating any tool you'd adopt at PayPal.

**Optional — the security/adversarial angle (relevant to fraud's adversarial setting):**
- Ying Zhang et al., *"How well does LLM generate security tests?"*, 2023. [FREE] https://arxiv.org/abs/2310.00710 — LLMs generating tests for security properties; the adversarial framing rhymes with fraud-model testing (an adversary actively probing for gaps).

**Connecting to your stack (explicit):** your TreeSHAP explainability outputs are a *source of testable invariants* — feature-importance stability across retrains, local-explanation consistency under small perturbations — and these are metamorphic/behavioral tests in exactly the Zhang/Ribeiro sense. The new capability the LLM adds is *proposing* candidate relations and *drafting* the Hypothesis/pytest harness for them; the assurance lesson from Phase 3 says you must still *verify* each proposed relation actually holds for a correct model (an LLM-suggested "invariant" that isn't truly invariant is a false oracle). Pair this phase with the prior doc's Phase 4A (property-based testing) — Hypothesis is the execution vehicle for LLM-proposed properties.

**Calibration note:** direction (A) — LLMs generating ML-pipeline tests — is *young and thin* on rigorous evaluation; much of it is preprints and tool demos. Direction (B) — testing ML systems — is mature and stable (the Zhang and Riccio surveys). Weight your confidence accordingly: the *principles* (metamorphic relations, behavioral testing, separate data/model/code testing) are solid; the *LLM-automates-it tooling* is speculative and worth prototyping rather than trusting.

---

## Phase 5 — The human debate: how to actually use these tools (parallel throughout, ~10 hrs)

**Goal:** The opinion side, read in parallel with everything above. The essays cluster into three positions; reading across all three is the point. The center of gravity of the *thoughtful* practitioner consensus, notably, lands in the same place the research does: **the LLM proposes, the human (and a verifier) decides what "correct" means.**

### 5A — The skeptical case (read first — it sharpens everything)
- David Adamo Jr., *"AI-Generated Tests Are Lying to You"*, 2026. [FREE] https://davidadamojr.com/ai-generated-tests-are-lying-to-you/ — the single best statement of the core objection: a test derived *from your code* is **transcription, not testing** — it asserts what the code *does*, not what it *should do*, so it cheerfully pins your bugs in a form you won't recognize. Constructive close: ask the LLM for *failure modes* not success paths ("how could this break?"), use it for *creativity not confirmation*, and measure quality with **mutation testing**. The cleanest articulation of the whole skeptical thread.
- Swizec Teller, *"Why You Shouldn't Use AI to Write Your Tests"*, 2024. [FREE] https://swizec.com/blog/why-you-shouldnt-use-ai-to-write-your-tests/ — the original, written in reaction to Meta's TestGen-LLM. The "Beyoncé rule" argument (if you liked it you should have put a test on it — but you can't, because the test came from the code) and the case for *feature coverage over code coverage*. Short, sharp, and names the same trap independently.
- *"AI-Generated Tests Give False Confidence"*, CodeIntelligently, 2026. [FREE] https://codeintelligently.com/blog/ai-generated-tests-false-confidence — the operational version: concrete examples of LLM-generated tests that mock away all real behavior and pass even with bugs, plus a CI recipe (mutation-testing gate with Stryker, fail-the-build thresholds). The "humans decide *what* to test, AI helps with *how*" rule. Pairs with the prior doc's Phase 5 (mutation testing as the real quality signal).

### 5B — The balanced / disciplined-adoption case (the mainstream)
- Addy Osmani, *"My LLM Coding Workflow Going into 2026"*, 2025. [FREE] https://addyosmani.com/blog/ai-coding-workflow/ — treat AI output like a *fast but unreliable junior developer*: review every diff, always run/test what it writes, and **weave a testing plan into the planning stage**. Quotes Simon Willison's framing of the LLM pair programmer as "over-confident and prone to mistakes." The pragmatic middle, with testing as the non-negotiable check on generation.
- Simon Willison, *"Agentic Engineering Patterns"* (esp. *Red/Green TDD* and *First Run the Tests*), 2026. [FREE] https://simonwillison.net/guides/agentic-engineering-patterns/ — the most useful *operational* guidance: a solid test suite is what lets an agent iterate-until-green safely; without tests it "cheerfully declares done on broken code." The TDD-with-agents pattern (human writes/curates the tests, agent makes them pass) is the practical synthesis of the whole curriculum — and notice it inverts the risky direction (tests constrain the agent, rather than the agent authoring its own oracle).
- Simon Willison, *"How I Use LLMs to Help Me Write Code"*, 2025. [FREE] https://simonwillison.net/2025/Mar/11/using-llms-for-code/ — broader workflow context for the above; the "verify everything, the model won't tell you it's wrong" discipline.

### 5C — The research-meets-practice / enthusiast-with-rigor case
- Martin Fowler & colleagues, *"Exploring Generative AI"* (ongoing memo series), 2023–2026. [FREE] https://martinfowler.com/articles/exploring-gen-ai.html — Thoughtworks' running, evidence-as-it-unfolds investigation. Read for the disposition: *systematic ongoing investigation* rather than verdicts, and the recurring finding that AI **rewards existing best practices** — clear specs, good tests, code review all become *more* valuable with an agent in the loop, not less. The intellectual bridge between the skeptics and the enthusiasts.
- (Optional, for the industrial-assurance voice already met in Phase 3) re-read the framing of Meta's TestGen-LLM as a *practitioner* artifact: it's the enthusiast case done responsibly — ship LLM tests, but only behind verifiable guarantees.

**How to read this phase:** start with 5A to install the right skepticism, then 5B for the working compromise, then 5C for the disposition. The throughline — strikingly consistent from solo bloggers to Meta's research org — is that **the human owns the oracle**: deciding what "correct" means and verifying the tests actually detect incorrectness (mutation testing), while the LLM accelerates the mechanical production of test code. That is the same conclusion the research arc reaches from the other direction.

---

## Minimum Viable Path (~5 weeks, if time compresses)

If you want the essential narrative fast:

1. **Phase 0** — the oracle-problem framing only (Barr et al., skim) + skim the EvoSuite abstract. (½ week) — *just enough to see the trade-off LLMs change.*
2. **Phase 1** — the Wang et al. TSE 2024 survey (taxonomy) + bookmark the Awesome-LLM4SE list. (½ week)
3. **Phase 2** — three papers only: TestPilot (2302.06527), "No More Manual Tests?" (2305.04207), CodaMOSA (ICSE 2023). (1.5 weeks) — *the arc from "it works" → "but assertions are wrong" → "hybridize with search."*
4. **Phase 3** — Meta's TestGen-LLM (2402.09171) + "LLMs Cannot Self-Correct Reasoning Yet" (2310.01798). (1 week) — *assurance + the reason you need it.*
5. **Phase 4** — Zhang et al. ML Testing survey (1906.10742), metamorphic + oracle sections only. (1 week) — *your domain's frame.*
6. **Phase 5** — Adamo's "Lying to You" + Willison's Red/Green TDD pattern. (½ week, parallel) — *the two poles of the practitioner view.*

That gives you: the historical trade-off, the canonical generation papers, the industrial assurance reframe, the ML-testing frame for your work, and both edges of the opinion debate. Everything else is depth you can pull from the surveys on demand.

---

## Inter-phase dependency map

```
Phase 0 (pre-LLM baseline: SBST + the oracle problem)
   │
   ▼
Phase 1 (surveys = the map) ──────────────┐
   │                                       │
   ▼                                       │
Phase 2 (LLM unit-test canon, 2022→2025)   │
   │   TestPilot → ChatTester → CodaMOSA    │
   │   → CoverUp → TestART                  │
   │                                       ▼
   ▼                              Phase 5 (human opinion:
Phase 3 (agentic + industrial assurance)    skeptical / balanced /
   │   TestGen-LLM, Assured LLMSE,           enthusiast — read in
   │   SWT-bench, Google repair              PARALLEL throughout)
   │   ⚠ counterpoint: "can't self-correct"
   │
   ▼
Phase 4 (ML/data-pipeline testing w/ LLMs)
       [ties to prior doc's Phase 4A + 4C]
       direction A (LLMs test ML) — young
       direction B (testing ML) — mature
```

---

## A note on currency (important for this topic specifically)

This field moves faster than any other in the prior curriculum. Concretely:
- **Conference anchors are stable:** EvoSuite (FSE'11), CodaMOSA (ICSE'23), TestPilot (TSE'23), TestGen-LLM (FSE'24), SWT-bench (NeurIPS'24), the Zhang ML-testing survey (TSE'22). Cite and trust these.
- **arXiv preprints from ~2024 onward are snapshots** — TestART, CoverUp, the agentic-repair papers, and essentially all of Phase 4 direction (A) are moving targets. Read for ideas; expect numbers and SOTA claims to be superseded.
- **Keep it live via two sources:** the **Awesome-LLM4SE** GitHub list (Phase 1) for new papers, and the **systematic reviews** (Phase 1) which are periodically updated. When you read this six months on, start there to find what's new.
- **The opinion essays** are timestamped reactions; the *arguments* (transcription-not-testing, mutation-testing-as-gate, human-owns-the-oracle, AI-rewards-best-practices) are durable even as specific tools and model names age.
- **Tool/model names** (GPT-3.5, Codex, StarCoder in the older papers) date the work but don't invalidate the methods — mentally substitute "a current frontier model" and the findings on *assertion correctness* and *the need for an external verifier* still hold.