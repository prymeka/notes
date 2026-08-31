Let me verify a couple of editions before I lock the list in.Confirmed the latest editions — two key books had new releases in the last 18 months that meaningfully change the recommendation. Here's the plan.

# A deep-Python reading curriculum

Eight books, five phases. The ordering matters: each phase unlocks the next, and Phases 4 and 5 can run partly in parallel with Phase 3. Reading time at a steady pace (~5 hrs/week) is roughly 9–12 months end-to-end, but you'll get useful payoff from Phase 1 alone.

## Phase 1 — The language, deeply

The premise: you can't reason about CPython's behaviour, or about why one piece of Python is 50× slower than another, until you see Python the way Python sees itself — through the data model.

**1. Fluent Python, 2nd edition** — Luciano Ramalho (O'Reilly, 2022)
The single best book for going from "comfortable" to "deep." Covers the data model (`__dunder__` protocols and why they're the soul of the language), sequence/dict/set internals from the API side, functions as first-class objects, OOP idioms (descriptors, ABCs, protocols, type hints), iterators/generators/coroutines, and a substantial concurrency section. Don't skip the metaprogramming chapters — descriptors in particular show up later when you understand why attribute access has a cost.

## Phase 2 — Behind the curtain

You now know what Python does. These books show how it does it.

**2. CPython Internals** — Anthony Shaw (Real Python, 2021)
A guided tour of the actual CPython source: compiler pipeline (lexer → parser → AST → bytecode), the evaluation loop, the object model in C, memory management and the cyclic GC, the GIL, and the parallelism primitives. Pinned to 3.9, but the architecture is largely intact; layer in PEP 659 (specializing adaptive interpreter, 3.11+) and PEP 703 (optional no-GIL build, 3.13+) as you go — both well-documented in the official PEPs if you want a follow-up.

**3. Inside the Python Virtual Machine** — Obi Ike-Nwosu (Leanpub, free PDF)
A short, sharper companion. Tighter focus on frames, code objects, and bytecode dispatch — exactly the bits you'll be most curious about after Shaw. Reading them together gives you a stereo view of the interpreter that's hard to get from either alone.

## Phase 3 — Making it fast

Now you can profile and optimise with intent rather than superstition.

**4. High Performance Python, 3rd edition** — Micha Gorelick & Ian Ozsvald (O'Reilly, April 2025)
This is the book to pair with what you just learned in Phase 2. Profiling (cProfile, line_profiler, memory_profiler, py-spy, scalene), lists vs arrays vs NumPy from a hardware-aware angle, generators and lazy evaluation, Cython and Numba, the multiprocessing / async / threading trade-off, GPU offload, scaling beyond RAM, and end-of-chapter war stories from production ML. The 3rd edition adds material on GenAI workloads and productionised ML inference — directly relevant to your fraud-serving context.

**5. Effective Python, 3rd edition** — Brett Slatkin (Addison-Wesley, November 2024)
125 specific items, expanded from 90, and crucially the new edition adds chapters on writing high-performance code and on building C-extension modules / interfacing with native shared libraries — exactly the low-latency-inference territory you flagged. Treat it as a referee after High Performance Python: when you're unsure of the idiomatic implementation of an optimisation, this book usually has the 2–3 page answer.

## Phase 4 — Concurrency, deeply

Two complementary books. Read them in order; they emphasise different things and the disagreement is informative.

**6. Python Concurrency with asyncio** — Matthew Fowler (Manning, 2022)
The modern, focused treatise. Event loops, tasks, cancellation, async iteration and context managers, structured concurrency, real-world I/O patterns (HTTP clients, DBs, sockets), and — important for you — pairing async with `multiprocessing` or thread pools when wrapping CPU/GPU-bound model calls inside an async serving layer. This is the canonical pattern for low-latency inference services in Python.

**7. Using Asyncio in Python** — Caleb Hattingh (O'Reilly, 2020)
Shorter and sharper. Particularly good on the *why* of asyncio's design and on common pitfalls (`gather` vs `wait`, sync/async bridging, when `create_task` silently swallows exceptions). Reading it after Fowler is a useful perspective check.

## Phase 5 — Field-tested idioms (ongoing reference)

**8. Python Cookbook, 3rd edition** — David Beazley & Brian Jones (O'Reilly, 2013)
Yes, it's from 2013. Yes, it's still the best advanced Python cookbook by a wide margin, and almost nothing in it is wrong. Beazley is one of the deepest Python practitioners alive (his "Understanding the Python GIL" talk is essentially required viewing once you finish Phase 2 — I know you said books only, but consider this one exception). The recipes on generators, coroutines, descriptors, metaclasses, and concurrency teach idioms you'll use forever. Use it as a reference: skim once for a map, then return when you hit a related problem.

---

## A few notes on what's *not* on this list

- **Pure low-latency-serving books for Python don't really exist.** The closest you'll find is the relevant chapters of High Performance Python (3rd ed), Slatkin's new performance + C-extension chapters, and the async books above. For systems-level thinking about latency budgets — useful but adjacent — *Designing Data-Intensive Applications* (Kleppmann) is the standard, though it's not Python-specific.
- **NumPy/scientific Python books** were left out deliberately — you'll have absorbed the relevant material from Phase 3 plus your ML day-to-day, and dedicated books here mostly duplicate it.
- **Books on `async` web frameworks** (FastAPI, Starlette) aren't included because the framework-specific knowledge dates fast and the underlying asyncio knowledge from Phase 4 is what actually carries over.

If you want, I can turn this into a paced reading schedule (week-by-week or chapter targets), or expand any phase into a deeper sub-curriculum — Phase 2 in particular benefits from a guided source-reading companion once you're a few chapters into Shaw.