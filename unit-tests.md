# Testing & Testable Code: A Curriculum

**Target profile:** SWE, ~2 yrs Python, intermediate (not a beginner). Primary language Python; secondary exposure to other languages.
**Scope:** Unit testing and test design → testable architecture → domain-specific testing (CLI, GUI, ML/data pipelines, databases) → language-agnostic principles.
**Budget:** ~8 hrs/week, intensive.
**Total horizon:** ~16–20 weeks for the full path; ~8 weeks for the Minimum Viable Path (see end).
**Orientation:** Balanced — every phase pairs a principles read with hands-on tooling work.

---

## How to read this document

- **Primary** = work through fully, do the exercises.
- **Supplementary** = read selectively, use as reference.
- **Optional** = depth/breadth if the topic grabs you or is directly job-relevant.
- **[FREE]** = legally free online (official docs, author-hosted full text, open-access papers).
- Citations give author, title, publisher/edition, year. Where a free full text exists, the URL is in the entry.
- Phases are mostly sequential; **Phase 6 (cross-language)** can be read in parallel with anything from Phase 3 onward. Domain phases (4A–4D) are independent of each other — do them in whatever order matches your priorities, though 4C/4D lean on Phase 3.

---

## Phase 0 — Mental model & vocabulary (Week 1, ~8 hrs)

**Goal:** Get the conceptual frame straight before touching tooling, so later choices (mock vs. fake, unit vs. integration) are principled rather than cargo-culted. As an ML engineer you already reason about train/serve skew and reproducibility — testing is the same discipline applied to code behavior: pin the inputs, assert the invariant, isolate the variable.

**Primary**
- Martin Fowler, *"UnitTest"* and *"TestPyramid"* — short canonical essays. [FREE] https://martinfowler.com/bliki/UnitTest.html and https://martinfowler.com/bliki/TestPyramid.html
- Martin Fowler, *"Mocks Aren't Stubs"* — the reference text on the London-vs-Detroit (mockist vs. classical) split and the taxonomy of test doubles (dummy/stub/spy/mock/fake). [FREE] https://martinfowler.com/articles/mocksArentStubs.html

**Supplementary**
- Google, *Software Engineering at Google*, ed. Winters, Manshreck, Wright (O'Reilly, 2020), Ch. 11–14 (Testing Overview, Unit Testing, Test Doubles, Larger Testing). [FREE] https://abseil.io/resources/swe-book — the most coherent industrial account of *why* a large codebase tests the way it does; the test-double chapter pairs directly with Fowler.

**Calibration note:** Fowler and the Google book disagree in emphasis — Google leans classical/state-based and is wary of over-mocking; the mockist tradition leans the other way. Hold both; the right choice is contextual. You'll revisit this in Phase 3 with a concrete opinion.

**Deliverable for yourself:** write a one-paragraph definition of each test-double type in your own words. You'll know the vocabulary stuck if you can explain why a "fake in-memory database" is not a "mock."

---

## Phase 1 — pytest fluency (Weeks 2–4, ~24 hrs)

**Goal:** Operational mastery of the framework you'll use daily — fixtures, parametrization, markers, plugins, coverage. This is the practical spine of the whole curriculum.

**Primary**
- Brian Okken, *Python Testing with pytest: Simple, Rapid, Effective, and Scalable*, 2nd ed. (Pragmatic Bookshelf, 2022). Examples on Python 3.10 / pytest 7. This is *the* book; the 2nd ed. grew from 7 to 16 chapters and adds depth on parametrization, markers, coverage, mocking, tox/CI, and plugin authoring. Work the `cards_proj` examples.
  - Critical chapters: fixtures (scope, teardown, `conftest.py`), parametrization (incl. advanced), markers, `unittest.mock` integration, coverage, building plugins.
- pytest official documentation. [FREE] https://docs.pytest.org/ — read alongside the book; the "How-to guides" and "Reference" sections are where you'll live once past the basics. **Verify version when you start** — the book targets pytest 7; current pytest may differ in defaults.

**Supplementary**
- Python `unittest` and `unittest.mock` docs. [FREE] https://docs.python.org/3/library/unittest.html and https://docs.python.org/3/library/unittest.mock.html — you must be literate in stdlib `unittest` even if you prefer pytest, because you'll meet it in other people's code and in constrained environments. Pay attention to `mock.patch`, `autospec`, `spec_set`, and the *where-to-patch* rule ("patch where it's looked up, not where it's defined") — the single most common mocking mistake.
- Okken's blog, pythontest.com. [FREE] https://pythontest.com/ — actively maintained (2025), good for newer-version idioms and edge topics.

**Tooling to set up this phase:** `pytest`, `pytest-cov` (coverage), `pytest-xdist` (parallel), `tox` or `nox` (multi-env). Get coverage reporting wired into your editor.

**Calibration note on coverage:** treat line/branch coverage as a *floor-finding* tool (what's totally untested), not a *quality* metric. 100% coverage with weak assertions is theater. Okken and the Google book both make this point.

---

## Phase 2 — Test design & TDD (Weeks 5–6, ~16 hrs)

**Goal:** Move from "can operate pytest" to "writes good tests" — naming, structure (Arrange-Act-Assert / Given-When-Then), one-reason-to-fail, and the TDD red-green-refactor loop. The methodology layer.

**Primary**
- Harry Percival, *Test-Driven Development with Python*, 2nd ed. (O'Reilly, 2017). [FREE] https://www.obeythetestinggoat.com/ — "the testing goat" book. Builds a real Django web app test-first, end to end. Even though it's Django-flavored, the *discipline* (functional tests → unit tests → outside-in TDD) is the transferable core. Skim the Django-specific deployment chapters; do the TDD-cycle chapters properly. **Note edition currency** — a newer revision may exist; check the site, the methodology is stable regardless.

**Supplementary**
- Kent Beck, *Test-Driven Development: By Example* (Addison-Wesley, 2002). The origin text. Java/Python examples, short, still the clearest statement of the *rhythm* of TDD. Read Part I (the money example) as a single sitting.
- Vladimir Khorikov, *Unit Testing: Principles, Practices, and Patterns* (Manning, 2020). C#-based but the **most rigorous treatment of what makes a test valuable** — the four pillars (protection against regressions, resistance to refactoring, fast feedback, maintainability) and why "resistance to refactoring" is the one everyone sacrifices. Strongly recommended; the language barrier is trivial for you. Chapters 4–5 (what makes a good test; mocks and test fragility) are the payload.

**Optional**
- Khorikov's blog, enterprisecraftsmanship.com. [FREE] https://enterprisecraftsmanship.com/posts/ — extends the book.

**Calibration note:** Khorikov is opinionated and partly mockist-skeptical; he argues most unit tests should be state-based against a "humble object" boundary. This is a coherent counterweight to TDD-with-mocks orthodoxy. By end of this phase you should be able to state *your own* position on when to mock.

---

## Phase 3 — Testable architecture (Weeks 7–9, ~24 hrs)

**Goal:** The highest-leverage phase. Most "hard to test" code is badly *designed*, not badly *tested*. Learn dependency inversion, ports/adapters (hexagonal), the repository and unit-of-work patterns, and the "functional core, imperative shell" idea. This is what lets you test ML pipelines, DB code, and CLIs without pain later.

**Primary**
- Harry Percival & Bob Gregory, *Architecture Patterns with Python: Enabling Test-Driven Development, Domain-Driven Design, and Event-Driven Microservices* (O'Reilly, 2020). [FREE] https://www.cosmicpython.com/ — full text online ("the cosmic python book"). The single best Python resource on *structuring code so it's testable*: dependency inversion → ports & adapters, Repository pattern (so you can swap a real DB for a fake), Unit of Work, service layer, and fakes-over-mocks at the boundaries. Work the repo examples.
  - Payload chapters: Repository pattern, Unit of Work, Service Layer, and the recurring "fake repository in tests" technique.

**Supplementary**
- Gary Bernhardt, *"Boundaries"* (talk + transcript). [FREE] https://www.destroyallsoftware.com/talks/boundaries — the "functional core, imperative shell" formulation in 30 minutes. The intellectual companion to the cosmic python book; explains *why* pushing logic into pure functions makes the bulk of your code testable without any doubles at all. (As a physics person you'll appreciate the framing: isolate the pure/deterministic part, quarantine the stateful I/O at the edges.)
- Robert C. Martin, *Clean Architecture* (Prentice Hall, 2017), the dependency-rule chapters. Language-agnostic statement of the same dependency-inversion principle. Supplementary, not essential if you've absorbed cosmic python.

**Calibration note:** hexagonal/DDD machinery is *overkill for small scripts*. The lesson to extract is the principle (depend on abstractions, isolate I/O), applied proportionally. Don't build a service layer for a 200-line tool.

**Why this phase is the hinge:** every domain phase below is, underneath, an application of "isolate the impure dependency behind a seam." DB → repository. ML model → inject the artifact. CLI → separate parsing from logic. GUI → separate presenter from view. Get this and the rest is configuration.

---

## Phase 4 — Domain-specific testing

Four independent modules. You selected all four as relevant; they're ordered to roughly track your priorities (ML/data and DB closest to your PayPal fraud work). 4C and 4D assume Phase 3.

### 4A — Property-based testing (transveral; Weeks 10, ~8 hrs)

**Why first among the domains:** property-based testing (PBT) is the technique most likely to change how you test *everything* — especially data transformations and ML preprocessing, where example-based tests miss edge cases. You assert *properties that hold for all inputs* (round-trip, invariants, metamorphic relations) and let the framework search for counterexamples and shrink them to minimal failing cases.

**Primary**
- Hypothesis official documentation — tutorial + "what you can generate" (strategies) + stateful testing. [FREE] https://hypothesis.readthedocs.io/ — actively developed; verify version. Start with the tutorial, then strategies, then `RuleBasedStateMachine` for stateful testing.

**Supplementary**
- David MacIver et al., *"Hypothesis: A new approach to property-based testing"*, Journal of Open Source Software 4(43), 2019. [FREE] https://doi.org/10.21105/joss.01891 — the canonical citation; short, explains the shrinking/minimization design that distinguishes Hypothesis from naive QuickCheck clones.
- Fred Hebert, *Property-Based Testing with PropEr, Erlang, and Elixir* (Pragmatic Bookshelf, 2019). Optional and non-Python, but the **best book-length treatment of how to *find* good properties** — the hard part of PBT is not the tool, it's knowing what invariant to assert. The "thinking in properties" chapters transfer directly to Hypothesis. *(Marked optional given the language, but the property-discovery material is rare and high-value.)*

**ML-specific hook:** metamorphic testing — when you lack a ground-truth oracle (common in ML), you assert *relations between outputs* (e.g., "scaling all features shouldn't change a tree model's predictions"; "adding a duplicate row shouldn't change learned statistics"). PBT is the natural vehicle. See 4C.

### 4B — Database & data-layer testing (Weeks 11, ~8 hrs)

**Goal:** Test code that touches a DB without slow, flaky, or polluting tests. The core tension: speed/isolation (fakes, in-memory) vs. fidelity (real engine).

**Primary**
- Cosmic Python (Phase 3), Repository + Unit of Work chapters — reread through the testing lens: the repository abstraction is *precisely* what lets you unit-test business logic against an in-memory fake and reserve the real DB for a thin integration layer. [FREE] https://www.cosmicpython.com/
- `pytest` fixtures for DB lifecycle — transaction-rollback-per-test and the "create schema once, roll back each test" pattern. Covered in Okken Ch. on fixtures (Phase 1).

**Supplementary**
- Testcontainers for Python documentation. [FREE] https://testcontainers-python.readthedocs.io/ — spin up a *real* ephemeral Postgres/MySQL in Docker per test session. The modern answer to "test against the real engine without a shared staging DB." High fidelity, moderate speed cost — use for the integration layer, not for every test.
- SQLAlchemy docs on testing / "joining a session into an external transaction." [FREE] https://docs.sqlalchemy.org/ — if you use SQLAlchemy, the canonical savepoint-rollback pattern for fast isolated tests.

**Calibration note — the SQLite-as-fake trap:** substituting in-memory SQLite for production Postgres is fast but *low fidelity* (different SQL dialect, types, constraints, concurrency). Fine for exercising logic; dangerous for anything dialect-sensitive. Decision rule: fake/SQLite for the bulk of logic tests, Testcontainers (real engine) for a smaller integration suite, and don't let the fake's behavior diverge silently from production.

### 4C — ML & data-pipeline testing (Weeks 12–13, ~16 hrs)

**Goal:** The hardest domain and the one closest to your work. ML systems fail in ways unit tests don't catch: data drift, schema changes, train/serve skew, silent degradation. You test *code*, *data*, and *model* separately, plus the pipeline gluing them.

**Primary**
- Eric Breck et al. (Google), *"The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction"*, IEEE Big Data, 2017. [FREE] https://research.google/pubs/pub46555/ — the foundational checklist: 28 tests across data, model, infrastructure, and monitoring. Maps directly onto a fraud-detection production system; treat it as an audit template for your own pipelines.
- D. Sculley et al. (Google), *"Hidden Technical Debt in Machine Learning Systems"*, NeurIPS 2015. [FREE] https://papers.nips.cc/paper/2015/hash/86df7dcfd896fcaf2674f757a2463eba-Abstract.html — *why* ML systems rot (entanglement/CACE, feedback loops, data dependencies). Not testing per se, but the diagnosis that motivates data/model testing. The "CACE principle" (Changing Anything Changes Everything) is the ML analogue of the coupling problems Phase 3 addresses.

**Supplementary**
- Great Expectations documentation. [FREE] https://docs.greatexpectations.io/ — declarative *data* validation (schema, distributions, nullity, ranges) as first-class testable assertions. Directly relevant to fraud features: assert that a feature's distribution hasn't drifted, that categoricals stay in-vocabulary, that no nulls appear where none should.
- Jeremy Jordan, *"Effective testing for machine learning systems"*. [FREE] https://www.jeremyjordan.me/testing-ml/ — a clear practitioner synthesis distinguishing pre-train tests (run fast, no training needed — e.g., model outputs the right shape, loss decreases on a batch) from post-train tests (behavioral: invariance, directional expectation, minimum-functionality — after Ribeiro et al.).
- Marco Tulio Ribeiro et al., *"Beyond Accuracy: Behavioral Testing of NLP Models with CheckList"*, ACL 2020. [FREE] https://aclanthology.org/2020.acl-main.442/ — introduces invariance / directional-expectation / minimum-functionality tests. NLP-framed but the taxonomy generalizes to any model, including tabular fraud classifiers.
- `deepchecks` documentation. [FREE] https://docs.deepchecks.com/ — batteries-included test suites for data integrity, train/test distribution drift, and model evaluation; a faster on-ramp than hand-rolling.

**Connecting to your stack:** your SHAP/TreeSHAP explainability work is itself a source of testable invariants — e.g., feature-importance stability across retrains, or local-explanation consistency under small input perturbations, are *behavioral tests* in the Ribeiro sense. Metamorphic relations (4A) are the right tool: "permuting feature column order must not change predictions," "a monotone feature must move the score in the expected direction."

**Calibration note:** ML testing is a younger field — the papers above are consensus *framing*, but tooling (Great Expectations, deepchecks, evidently) is fast-moving; verify current APIs and consider what's actively maintained when you adopt. The *principles* (test data, code, and model separately; monitor in production) are stable; the libraries are not.

### 4D — CLI & GUI testing (Week 14, ~8 hrs)

**Goal:** Test user-facing entry points. The unifying principle (from Phase 3): **separate the logic from the I/O shell**, then unit-test the logic directly and keep a thin layer of end-to-end tests for the wiring.

**CLI — Primary**
- Click's testing documentation (`CliRunner`). [FREE] https://click.palletsprojects.com/en/stable/testing/ — if you use Click, `CliRunner` invokes commands in-process and captures output/exit codes. Also applicable in spirit to argparse-based tools.
- Typer's testing docs (built on Click's runner). [FREE] https://typer.tiangolo.com/tutorial/testing/ — if you use Typer.

**CLI — Supplementary**
- Core technique, framework-agnostic: keep `main()`/argument-parsing as a thin adapter that calls pure functions; unit-test the functions, use the runner only for the parse-and-dispatch seam. Use `capsys`/`capfd` (pytest) to assert on stdout/stderr, `monkeypatch` for env vars and `sys.argv`. Covered in Okken (Phase 1).

**GUI — Primary**
- `pytest-qt` documentation. [FREE] https://pytest-qt.readthedocs.io/ — if you touch Qt (PyQt/PySide): the `qtbot` fixture simulates clicks/keypresses and waits on signals.

**GUI — Supplementary**
- The Humble Dialog / Humble Object pattern — Michael Feathers' formulation (and Khorikov, Phase 2). [FREE] http://www.michaelfeathers.com/Articles/TheHumbleDialogBox.pdf — the canonical answer to "GUIs are hard to test": make the view *humble* (no logic), push everything into a testable presenter/view-model (MVP/MVVM). This is the GUI-specific instance of "functional core, imperative shell."
- For web/browser UIs: Playwright for Python. [FREE] https://playwright.dev/python/ — modern end-to-end browser automation; use sparingly (slow, top of the pyramid).

**Calibration note:** GUI end-to-end tests are slow and brittle — they belong at the *top* of the pyramid (few, high-value smoke paths). The payoff comes from making the view humble so 90% of behavior is testable without driving the UI at all.

---

## Phase 5 — CI, scale & sustainable test suites (Week 15, ~8 hrs)

**Goal:** Make tests run automatically, fast, and reliably as the suite grows. The difference between tests you *have* and tests you *trust*.

**Primary**
- `tox`/`nox` docs (multi-version, multi-env automation). [FREE] https://tox.wiki/ and https://nox.thea.codes/
- Okken, Phase 1 chapters on tox and CI — reread now that you have a suite to orchestrate.

**Supplementary**
- Martin Fowler, *"Continuous Integration"* (revised essay). [FREE] https://martinfowler.com/articles/continuousIntegration.html — the *why*.
- Google SWE book (Phase 0), Ch. on Larger Testing and on the testing culture at scale. [FREE] https://abseil.io/resources/swe-book
- On flaky tests: Google Testing Blog, *"Flaky Tests at Google and How We Mitigate Them"*. [FREE] https://testing.googleblog.com/2016/05/flaky-tests-at-google-and-how-we.html — flakiness is the silent killer of suite trust; learn to detect, quarantine, and fix rather than retry-and-ignore.
- `pytest-xdist` (parallelism) and `mutmut` or `cosmic-ray` for **mutation testing** [FREE] — the real answer to "are my assertions any good?": mutation testing perturbs your *source* and checks whether tests catch it. A far better quality signal than coverage. Optional but illuminating; run it once on a module you think is well-tested and be humbled.

---

## Phase 6 — Cross-language principles (parallel from Phase 3 onward, ~8 hrs)

**Goal:** You use other languages sometimes; testing concepts are 90% portable but idioms and tooling differ. This phase generalizes the Python-specific skills and gives you a foothold in the major ecosystems. **Read in parallel — it's reference, not a blocker.**

**Primary**
- Gerard Meszaros, *xUnit Test Patterns: Refactoring Test Code* (Addison-Wesley, 2007). The *language-agnostic* pattern catalog behind every xUnit-style framework (pytest, JUnit, NUnit, Go's testing, etc.). Comprehensive (it's a doorstop) — use as a **reference**, not cover-to-cover: read the "Test Smells" and "Test Double Patterns" catalogs, dip into the rest by need. This is the canonical source for the vocabulary you started in Phase 0.

**Supplementary (pick by relevance to languages you actually touch)**
- Michael Feathers, *Working Effectively with Legacy Code* (Prentice Hall, 2004). Language-agnostic (C++/Java/C# examples). The bible for *getting untested code under test* — "seams," dependency-breaking techniques, the characterization-test workflow. Directly useful whenever you inherit a codebase with no tests. Highly recommended regardless of language.
- Go: the standard library `testing` package + table-driven tests. [FREE] https://go.dev/doc/tutorial/add-a-test and the blog on table-driven tests. Go's testing philosophy (no assertion library, table-driven, subtests) is a useful contrast to pytest's richness.
- JavaScript/TypeScript: Vitest [FREE] https://vitest.dev/ or Jest [FREE] https://jestjs.io/ docs — if you do any front-end or Node work.
- Rust: the built-in test framework, *The Rust Programming Language* Ch. 11. [FREE] https://doc.rust-lang.org/book/ch11-00-testing.html — tests-as-first-class-language-feature.

**Transfer note:** the constants across all of these are the test pyramid, AAA structure, the double taxonomy, and "isolate the impure boundary." What changes is mocking ergonomics (heavy in C#/Java, lighter and more controversial in Go), assertion style, and how the language's type system reduces the *need* for certain tests. Map each new ecosystem onto the concepts you already own rather than relearning from scratch.

---

## Minimum Viable Path (~8 weeks, if time compresses)

If you need competence fast and will backfill later, do exactly this:

1. **Phase 0** — Fowler's three essays + the test-double taxonomy. (½ week)
2. **Phase 1** — Okken's pytest book, core chapters (fixtures, parametrization, mocking, coverage) + pytest docs. (2 weeks) — *non-negotiable spine.*
3. **Phase 2** — Khorikov Ch. 1–5 (what makes a test valuable) + skim the testing-goat TDD cycle. (1.5 weeks)
4. **Phase 3** — Cosmic Python: Repository + Unit of Work + Service Layer + the "fakes in tests" technique, plus Bernhardt's *Boundaries* talk. (2 weeks) — *the hinge; don't skip.*
5. **One domain module** matching your immediate need — for you, **4C (ML/data)**: the ML Test Score paper + Jeremy Jordan's article + Great Expectations quickstart. (1.5 weeks)
6. **Phase 4A (PBT)** — Hypothesis tutorial only. (½ week)

That gets you: operating pytest well, writing tests that resist refactoring, structuring code so it's testable, and a working approach to your own ML pipelines. Phases 4B/4D, 5, and 6 become just-in-time reading when a specific need arises.

---

## Inter-phase dependency map

```
Phase 0 (vocabulary)
   │
   ▼
Phase 1 (pytest) ──────────────┐
   │                           │
   ▼                           │
Phase 2 (TDD/design) ──────────┤
   │                           │
   ▼                           ▼
Phase 3 (testable arch) ── Phase 6 (cross-language, parallel)
   │
   ├──► 4A (property-based)  ─── feeds ──► 4C
   ├──► 4B (databases)        [needs Phase 3]
   ├──► 4C (ML/data)          [needs Phase 3; uses 4A]
   └──► 4D (CLI/GUI)          [needs Phase 3]
   │
   ▼
Phase 5 (CI / scale / mutation testing)
```

---

## A note on currency

Several entries are version-sensitive and worth a 30-second check before you start the relevant phase, since editions and APIs move:

- **pytest** — Okken's 2nd ed. targets pytest 7 / Python 3.10; confirm current pytest defaults.
- **Testing Goat (Percival TDD)** — check obeythetestinggoat.com for the latest revision.
- **Hypothesis, Great Expectations, deepchecks, Testcontainers, Playwright, pytest-qt** — all actively developed; read current docs rather than older tutorials, and sanity-check that a given ML-testing library is still actively maintained before adopting it.
- The **books** (Khorikov, Meszaros, Feathers, Beck, cosmic python, Google SWE) are stable — their principles don't expire even where example languages age.