# Systems, Security & Reliability — A Self-Taught Curriculum
### Prioritized · Deep-mastery track · Intermediate-start with one shared foundation phase

---

## 0. How to read this

**Prioritization logic.** You asked to lead with the highest-leverage fields. Leverage here = *(demand × AI-resilience × synergy with your ML/fraud trajectory × how many other fields it unlocks)*. That produces four bands:

- **Phase 0 — Shared foundation.** Systems programming in C + computer architecture. Everything below assumes it. You have the math and CS maturity; what ML work rarely forces is deep C, the memory hierarchy, and the ABI. This phase closes that gap.
- **Tier 1 — Core spine (do these, roughly in order).** Operating Systems → Compilers → Runtimes/JITs. The OS is the universal substrate; compilers+runtimes are the single strongest bridge from applied ML into ML-systems (MLIR/XLA/TVM/Triton/TorchInductor), which was the top pick in your career map.
- **Tier 2 — High-value specializations (all strong; sequence by taste).** Cryptography (adjacency to fraud & security-for-AI), Networking & Protocol Engineering, Site Reliability & Performance Engineering (performance half is immediately useful for inference optimization).
- **Tier 3 — Optional deep-hardware track.** Kernel → Embedded → Firmware. Very high resilience, narrower/more of a domain pivot. Depth, not obligation.

**Conventions.**
- **[Free]** — legally free online. **[Primary]** — the spine text to actually work through. **[Supp.]** — reference/secondary, reach for as needed.
- **⇄** — explicit connection to your ML-systems / fraud / security trajectory.
- **⚙︎** — a place your theoretical-physics + applied-math background is a real accelerator, not just flavor.
- Full citations (author, edition, publisher, year) given so you can source primary editions.

**The connective spine (why this set hangs together).** OS (memory, scheduling, syscalls) → compilers/runtimes (how code becomes execution) → performance engineering (making it fast) → networking (making it distributed) is *exactly the stack under modern ML-systems and inference infrastructure*. Crypto and firmware/embedded are the two "adversarial-and-physical" wings. Treat the spine as the trunk and the rest as branches.

**A note on C vs. Rust.** Learn **C to read the world** (kernel, embedded, CPython, LLVM, every legacy system) and **Rust for new systems work** (ascendant, memory-safe, increasingly the language of new kernels/embedded/tooling). This curriculum is C-first for reading and comprehension, with Rust on-ramps flagged where the ecosystem is strong (embedded especially). Don't skip C on the theory that Rust replaces it — you cannot read existing systems without it.

**Currency warnings (this is version-sensitive).** LLVM/MLIR move fast — pin to current release docs, not blog posts. Rust editions shift. The classic *kernel* books (Bovet & Cesati 2005, Love 2010, LDD3 2005) describe old kernel versions — conceptually gold, but always cross-check against current source and LWN. NIST post-quantum standards (FIPS 203/204/205) were **finalized August 2024**, so pre-2024 crypto texts predate them — supplement with the standards directly.

---

## Dependency map

```
                    ┌──────────────────────────────────────────┐
                    │ PHASE 0: C + Computer Architecture (CS:APP)│
                    └───────────────┬──────────────────────────┘
                                    │ (prerequisite for everything)
        ┌───────────────┬──────────┼───────────┬──────────────────┐
        ▼               ▼          ▼           ▼                  ▼
   ┌─────────┐   ┌────────────┐ ┌────────┐ ┌──────────┐    ┌──────────────┐
   │ TIER 1  │   │Cryptography│ │Network │ │  SRE &   │    │ (needs OS)   │
   │   OS    │   │  (Tier 2)  │ │(Tier 2)│ │  Perf    │    │              │
   └────┬────┘   └────────────┘ └───┬────┘ │ (Tier 2) │    │              │
        │                           │      └────┬─────┘    │              │
        ▼                           │           │          ▼              │
   ┌─────────┐                      └───────────┴───► Distributed Systems │
   │Compilers│◄──── strongest ⇄ ML-systems bridge      (connective tissue) │
   └────┬────┘                                                             │
        ▼                                          ┌──────────────────────┘
   ┌──────────┐                                     ▼
   │Runtimes/ │                            ┌──────────────────────────┐
   │  JITs    │                            │ TIER 3 (optional depth): │
   └──────────┘                            │ Kernel → Embedded → FW   │
                                           └──────────────────────────┘
```

Reading order that respects dependencies: **Phase 0 → OS → (Compilers → Runtimes) in parallel with (Crypto and/or Networking) → SRE/Perf → Distributed Systems → Kernel → Embedded → Firmware.**

---

# PHASE 0 — Shared Foundation: Systems Programming in C + Computer Architecture

**Why first.** Every field below is written in, or reasons about, C and the machine. This is the highest-ROI phase in the whole document.

**What you need to know.** The C language including undefined behavior and the memory model; pointers, memory layout, the stack/heap; the compilation & linking pipeline (preprocess → compile → assemble → link → load); the memory hierarchy and cache behavior; instruction set architecture basics (registers, addressing, x86-64 and/or RISC-V); pipelining, hazards, branch prediction, out-of-order execution at a conceptual level; calling conventions / the ABI; assembly reading fluency.

**Key textbooks**
- **[Primary]** Randal E. Bryant & David R. O'Hallaron, *Computer Systems: A Programmer's Perspective (CS:APP)*, 3rd ed., Pearson, 2015. — The single best systems on-ramp for a programmer. Work it *with the labs*.
- **[Primary/Free]** Brian Kernighan & Dennis Ritchie, *The C Programming Language*, 2nd ed., Prentice Hall, 1988 — canonical but C89-era; pair with a modern text.
- **[Supp./Free]** Jens Gustedt, *Modern C*, 2nd ed., Manning, 2019 — free PDF from the author; covers modern C (C17), better idioms than K&R alone.
- **[Supp.]** David A. Patterson & John L. Hennessy, *Computer Organization and Design (RISC-V Edition)*, 2nd ed., Morgan Kaufmann, 2020 — the undergrad architecture text.
- **[Supp.]** Noam Nisan & Shimon Schocken, *The Elements of Computing Systems (Nand2Tetris)*, 2nd ed., MIT Press, 2021 — build a computer from NAND gates up; superb intuition-builder. **[Free]** course.

**Courses, tools, standards & communities (SOP)**
- **[Free]** CMU **15-213 / 18-213** "Intro to Computer Systems" — the CS:APP course; lectures + the famous labs (Data, Bomb, Attack, Cache, Shell, Malloc, Proxy) are self-servable.
- **[Free]** UC Berkeley **CS61C**; **Nand2Tetris** on Coursera ("Build a Modern Computer from First Principles").
- **[Free]** Onur Mutlu's **Computer Architecture** lectures (ETH Zürich, YouTube) — for the deep dive later.
- **Tools:** `gcc`/`clang`, `gdb`, `valgrind`, `objdump`, `perf`, `strace`, and **Compiler Explorer (godbolt.org)** **[Free]** — live source↔assembly.
- **SOP/mental models:** never invoke UB; know your ABI (System V AMD64); read assembly without fear; profile before optimizing.
- **⚙︎** The memory hierarchy is a physics-flavored optimization problem (latency/bandwidth tradeoffs, locality); pipelining is a throughput/latency story you'll find familiar.

**Getting started (concrete).** Read CS:APP chs. 1–3 and 6; do the **Bomb Lab** (reverse-engineer assembly with gdb) and **Cache Lab**. This alone transforms how you read code.

**Going deeper.** Finish CS:APP + **Malloc Lab** (write an allocator — foundational for the runtimes tier). Then Patterson & Hennessy or Mutlu's lectures for microarchitecture; **[Supp.]** John L. Hennessy & David A. Patterson, *Computer Architecture: A Quantitative Approach*, 6th ed., Morgan Kaufmann, 2017 for the graduate treatment (caches, ILP, memory systems, accelerators — ⇄ directly relevant to GPU/ML-hardware reasoning).

**≈ Time:** 2–4 months at a serious pace. **MVP:** CS:APP chs. 1–3, 6; Bomb + Cache + Malloc labs; fluent gdb + godbolt. Do not skip Malloc Lab.

---

# TIER 1 — Core Spine (highest leverage)

## 1. Operating Systems

**Why here.** The OS is the substrate every other systems field stands on; it also unlocks kernel, SRE, and much of networking. Highest structural leverage in the document.

**What you need to know.** Processes vs. threads; scheduling; virtual memory and paging; concurrency (locks, condition variables, semaphores, lock-free basics, the memory-ordering model); deadlock; the syscall interface; file systems and the I/O stack; the boundary between user and kernel space.

**Key textbooks**
- **[Primary/Free]** Remzi & Andrea Arpaci-Dusseau, *Operating Systems: Three Easy Pieces (OSTEP)*, v1.10, Arpaci-Dusseau Books, 2018 (continuously updated) — the modern favorite, free, superbly written around "virtualization / concurrency / persistence."
- **[Primary/Free]** Russ Cox, Frans Kaashoek & Robert Morris, *xv6: a simple, Unix-like teaching operating system*, MIT (revised annually) — the companion to a real, hackable teaching OS.
- **[Supp.]** Abraham Silberschatz, Peter Baer Galvin & Greg Gagne, *Operating System Concepts*, 10th ed., Wiley, 2018 — the "dinosaur book," encyclopedic reference.
- **[Supp.]** Andrew S. Tanenbaum & Herbert Bos, *Modern Operating Systems*, 4th ed., Pearson, 2014 — strong on design and distributed OS.

**Courses, tools, standards & communities (SOP)**
- **[Free]** MIT **6.1810** (formerly 6.S081) "Operating System Engineering" — the xv6 labs (add syscalls, implement COW fork, a memory allocator, a scheduler). The best hands-on OS experience available.
- **[Free]** UC Berkeley **CS162** (Pintos projects) as an alternative track.
- **[Free]** Philipp Oppermann, **"Writing an OS in Rust"** (os.phil-opp.com) — build a small kernel from scratch in Rust; excellent modern on-ramp and a Rust bridge.
- **SOP:** POSIX as the interface contract; understand `fork/exec/wait`, `mmap`, the page fault path, and why context switches cost what they cost.

**Getting started.** Read OSTEP "Virtualization" + "Concurrency"; in parallel do the first few **6.1810 xv6 labs**. Reading + a real codebase together is what makes OS stick.

**Going deeper.** Finish OSTEP "Persistence"; then real-kernel internals via the Kernel tier (Tier 3). For distributed OS concepts, roll into the Distributed Systems section. **⚙︎** Scheduling is a constrained optimization / queueing problem; virtual memory is a caching problem — both map to intuitions you already have.

**≈ Time:** 3–5 months. **MVP:** OSTEP (all three parts) + first 4 xv6 labs.

---

## 2. Compilers

**Why here, high.** **⇄ This is the strongest single bridge from applied ML to ML-systems.** The entire modern ML-compiler stack — LLVM, MLIR, XLA, TVM, TorchInductor, Triton — is compiler engineering. Deep demand, very AI-resilient (whole-program reasoning, hard-to-verify correctness).

**What you need to know.** Lexing; parsing (recursive descent, LL/LR); ASTs; semantic analysis and type checking; intermediate representations; **SSA form**; dataflow analysis; classic optimizations (constant propagation, DCE, inlining, loop transforms); register allocation; instruction selection & scheduling; code generation.

**Key textbooks**
- **[Primary/Free]** Robert Nystrom, *Crafting Interpreters*, Genever Benning, 2021 — free online; you build a tree-walking interpreter *and* a bytecode VM in C. The best possible starting point; also seeds the Runtimes tier.
- **[Primary]** Keith D. Cooper & Linda Torczon, *Engineering a Compiler*, 3rd ed., Morgan Kaufmann, 2022 — modern, optimization- and backend-focused; the best single "real compilers" text today.
- **[Supp.]** Alfred V. Aho, Monica S. Lam, Ravi Sethi & Jeffrey D. Ullman, *Compilers: Principles, Techniques, and Tools (the "Dragon Book")*, 2nd ed., Addison-Wesley, 2006 — canonical reference; parsing-heavy and somewhat dated in emphasis (see Calibration).
- **[Supp.]** Andrew W. Appel, *Modern Compiler Implementation in ML* (the "Tiger book"), Cambridge University Press, 1998 — clean end-to-end project structure.
- **[Supp.]** Steven S. Muchnick, *Advanced Compiler Design and Implementation*, Morgan Kaufmann, 1997 — deep optimization catalogue for the advanced path.

**Courses, tools, standards & communities (SOP)**
- **[Free]** Stanford **CS143** materials; **[Free]** Cornell **CS6120** "Advanced Compilers" (Adrian Sampson) — self-guided, uses **LLVM** and the **Bril** IR; ideal for going deeper.
- **[Free]** The **LLVM Kaleidoscope** tutorial — build a JIT-compiled language front-end on LLVM.
- **[Free]** **MLIR** tutorials/docs and the **Triton** tutorials — **⇄** your ML-compiler entry points.
- **SOP:** know SSA cold; think in passes over an IR; use godbolt to see what optimizers actually do; read LLVM IR.

**Getting started.** Work through *Crafting Interpreters* end-to-end (both interpreters). Then start Cooper & Torczon and re-implement a front-end targeting LLVM IR via Kaleidoscope.

**Going deeper.** Cornell CS6120 + writing real LLVM passes; then MLIR — build a toy dialect and lower it. From there, read the sources of a production optimizer. **⚙︎** Dataflow analysis is a fixed-point/lattice computation; polyhedral loop optimization is linear-algebra-over-iteration-spaces — both very congenial to a math background.

**≈ Time:** 4–6 months (front-loaded by Crafting Interpreters). **MVP:** *Crafting Interpreters* complete + Kaleidoscope + Cooper & Torczon chs. on IR/SSA/optimization.

---

## 3. Runtimes & JITs

**Why here.** Sits right on top of compilers; **⇄ directly extends your Python-internals & performance work** (CPython is a bytecode VM; PyPy is a meta-tracing JIT). This is where "how does managed code actually run fast" lives.

**What you need to know.** Bytecode design; interpreter dispatch (switch, direct/indirect threading, computed goto); **garbage collection** (reference counting, mark-sweep, copying, generational, concurrent/region-based — G1, ZGC, Shenandoah); JIT compilation with **tiered execution** (baseline → optimizing); **inline caches**; speculative optimization & **deoptimization**; escape analysis; the language memory model.

**Key textbooks**
- **[Primary]** Richard Jones, Antony Hosking & Eliot Moss, *The Garbage Collection Handbook: The Art of Automatic Memory Management*, 2nd ed., CRC Press, 2023 — the definitive GC reference.
- **[Primary]** *Crafting Interpreters* (the **clox** bytecode-VM half) — reuse it here; it's the cleanest intro to a real VM.
- **[Supp.]** James E. Smith & Ravi Nair, *Virtual Machines: Versatile Platforms for Systems and Processes*, Morgan Kaufmann, 2005 — VM/ISA-emulation architecture.
- **[Supp./⇄]** Anthony Shaw, *CPython Internals*, Real Python, 2021 — dissects the CPython runtime; a direct tie to your existing Python-internals curriculum.

**Courses, tools, standards & communities (SOP)**
- **Study the canon of real runtimes:** the **CPython** source (`ceval.c`), **V8** (TurboFan/Maglev/Sparkplug — the V8 blog is excellent **[Free]**), **HotSpot JVM** (C1/C2, and Aleksey Shipilëv's GC/JVM talks **[Free]**), **LuaJIT** (Mike Pall's tracing JIT — a masterclass), and **PyPy/RPython** meta-tracing.
- **SOP:** understand tiering, on-stack replacement, guards/deopt, and why inline caches make dynamic languages fast; benchmark with statistically sound methodology (JMH-style thinking).

**Getting started.** Extend clox: add a real GC (upgrade from the book's mark-sweep), add optimizations, then profile it. In parallel, trace one bytecode through CPython's eval loop.

**Going deeper.** Implement a simple template/baseline JIT (or study LuaJIT's tracing design); read V8/HotSpot deeply; study a concurrent GC (ZGC/Shenandoah design docs). **⚙︎** GC pause/throughput tradeoffs are a queueing/latency-distribution problem; the generational hypothesis is an empirical distributional claim about object lifetimes.

**≈ Time:** 3–5 months. **MVP:** clox with a rewritten GC + reading CPython's eval loop + the GC Handbook's core algorithm chapters.

---

# TIER 2 — High-Value Specializations

## 4. Cryptography

**Why here.** **⇄ Nearest neighbor to your fraud/security world**, and flagged very-high-resilience (adversarial + mathematical). **⚙︎ Your math/physics background is a first-class asset**; this is the field where it pays off most directly.

**What you need to know.** Probability and modular arithmetic/number theory; symmetric crypto (block ciphers, AES, modes, stream ciphers); message authentication (MACs, authenticated encryption); hash functions; public-key (RSA, Diffie–Hellman, elliptic curves); digital signatures; key exchange and protocols (TLS 1.3); the **provable-security / reduction** mindset; side-channels and constant-time implementation; and the modern frontier: **post-quantum (lattices)** and **zero-knowledge proofs**.

**Key textbooks**
- **[Primary]** Jonathan Katz & Yehuda Lindell, *Introduction to Modern Cryptography*, 3rd ed., CRC Press, 2020 — the rigorous provable-security standard. This is the spine.
- **[Primary/Free]** Dan Boneh & Victor Shoup, *A Graduate Course in Applied Cryptography* — free online draft; modern, comprehensive, superb.
- **[Supp.]** Jean-Philippe Aumasson, *Serious Cryptography*, 2nd ed., No Starch Press, 2024 — accessible, practical, current (includes PQC). Great confidence-builder alongside Katz–Lindell.
- **[Supp.]** Niels Ferguson, Bruce Schneier & Tadayoshi Kohno, *Cryptography Engineering*, Wiley, 2010 — engineering pitfalls and system design.
- **[Supp./⚙︎ math depth]** Steven Galbraith, *Mathematics of Public Key Cryptography*, Cambridge University Press, 2012 **[Free]**; and Justin Thaler, *Proofs, Arguments, and Zero-Knowledge*, 2022 **[Free]** — the ZK bible.

**Courses, tools, standards & communities (SOP)**
- **[Free]** Dan Boneh's **Cryptography I** (Stanford, Coursera) — the canonical course.
- **[Free]** **Cryptopals Crypto Challenges** (cryptopals.com) — the canonical *hands-on* path; you break real constructions (padding oracles, CBC bit-flipping, weak RNGs). Do these.
- **Standards/SOP:** NIST **FIPS 197** (AES), **FIPS 186** (signatures), and the post-quantum suite **FIPS 203 / 204 / 205 (ML-KEM / ML-DSA / SLH-DSA), finalized Aug 2024**; NIST **SP 800-series**; **RFC 8446** (TLS 1.3). Cardinal rule: **never roll your own crypto in production; implement to learn, use vetted libraries to ship**; constant-time everything.

**Getting started.** Boneh's Cryptography I **plus** the first 3 Cryptopals sets, running Katz–Lindell chapters underneath for rigor. The combination of "prove it" (Katz) and "break it" (Cryptopals) is the fastest route to real understanding.

**Going deeper.** Finish Katz–Lindell + Boneh–Shoup; then specialize toward the two live frontiers with strong demand: **post-quantum / lattice crypto** (learn lattices, LWE, and the NIST PQC constructions directly from the standards + Galbraith) and **zero-knowledge** (Thaler's book; the "ZK Whiteboard Sessions" **[Free]**; implement a small SNARK/STARK). Both **⇄** privacy-preserving ML and fraud/identity.

**≈ Time:** 4–7 months to solid competence; frontiers (PQC/ZK) are open-ended. **MVP:** Boneh Crypto I + Cryptopals sets 1–3 + Aumasson cover-to-cover.

---

## 5. Networking & Protocol Engineering

**Why here.** Foundational to everything distributed; **⇄ AI-cluster interconnects, RDMA, and high-performance networking are core ML-systems concerns.** High resilience for the low-level/performance and protocol-design end.

**What you need to know.** The layered model and why it exists; Ethernet/IP/routing; **TCP** (reliability, flow control, **congestion control**); UDP and QUIC; DNS; HTTP/1.1→2→3; TLS as a protocol; **socket programming**; how to design and specify a protocol; how to *read an RFC*.

**Key textbooks**
- **[Primary]** James F. Kurose & Keith W. Ross, *Computer Networking: A Top-Down Approach*, 8th ed., Pearson, 2020 — the standard, well-paced intro.
- **[Primary/Free]** Larry L. Peterson & Bruce S. Davie, *Computer Networks: A Systems Approach*, open edition (systemsapproach.org) — free, systems-oriented, excellent complement.
- **[Supp.]** W. Richard Stevens & Kevin R. Fall, *TCP/IP Illustrated, Vol. 1: The Protocols*, 2nd ed., Addison-Wesley, 2011 — the deep protocol reference.
- **[Supp.]** W. Richard Stevens, Bill Fenner & Andrew M. Rudoff, *UNIX Network Programming, Vol. 1: The Sockets Networking API*, 3rd ed., Addison-Wesley, 2003 — the socket-programming bible.
- **[Supp./Free]** **Beej's Guide to Network Programming** (beej.us) — the beloved, free sockets on-ramp.

**Courses, tools, standards & communities (SOP)**
- **[Free]** Stanford **CS144** "Introduction to Computer Networking" — you **build a working TCP** in C++ (the labs are the highlight of the field). Strongly recommended.
- **Tools:** **Wireshark** (packet analysis), `tcpdump`, `netcat`, `ss`. **SOP:** learn to read **RFCs** and follow the **IETF** process; the robustness principle ("be conservative in what you send…") and its critiques.
- **⇄ Advanced/HPC networking:** **RDMA/RoCE/InfiniBand**, **DPDK** (kernel-bypass), and **eBPF/XDP** — the fast-path networking behind ML clusters and low-latency systems.

**Getting started.** Kurose & Ross + Beej's for sockets, then the **CS144 labs** (build TCP). Nothing teaches TCP like implementing it.

**Going deeper.** **QUIC** (RFC 9000) and HTTP/3; modern **congestion control** (BBR — read the papers); kernel-bypass (DPDK) and **eBPF/XDP** programming; protocol verification. **⚙︎** Congestion control is a control-theory / dynamical-systems problem; Shannon-style information theory underlies channel capacity and coding.

**≈ Time:** 3–5 months. **MVP:** Kurose & Ross + Beej's + CS144 TCP labs.

---

## 6. Site Reliability & Performance Engineering

**Why here.** Two coupled halves. **⇄ The *performance* half feeds ML-inference optimization directly** (and is the immediately-useful part given your production ML work); the *reliability* half is the operational discipline for running systems at scale. Your drift-monitoring work is already observability-adjacent.

**What you need to know.**
- *Reliability side:* **SLIs / SLOs / error budgets**; the four golden signals; observability (metrics, logs, distributed traces); incident response and **blameless postmortems**; capacity planning; toil reduction; **chaos engineering**; distributed-systems failure modes.
- *Performance side:* systematic **profiling**; the **USE method** (Utilization/Saturation/Errors); **flame graphs**; latency analysis and tail latency; CPU/memory/disk/network performance; scientific **benchmarking**.

**Key textbooks / primary resources**
- **[Primary/Free]** Betsy Beyer, Chris Jones, Jennifer Petoff & Niall Richard Murphy (eds.), *Site Reliability Engineering: How Google Runs Production Systems*, O'Reilly, 2016 — free at sre.google/books; the foundational SRE text.
- **[Primary/Free]** *The Site Reliability Workbook*, O'Reilly, 2018 (free) — the practical companion; and *Building Secure and Reliable Systems*, O'Reilly, 2020 (free) — **⇄** reliability∩security.
- **[Primary]** Brendan Gregg, *Systems Performance: Enterprise and the Cloud*, 2nd ed., Addison-Wesley, 2020 — the performance-engineering bible.
- **[Supp.]** Brendan Gregg, *BPF Performance Tools*, Addison-Wesley, 2019 — modern **eBPF** observability.
- **[Supp.]** Michael T. Nygard, *Release It!*, 2nd ed., Pragmatic Bookshelf, 2018 — resilience/stability patterns (circuit breakers, bulkheads).

**Courses, tools, standards & communities (SOP)**
- **[Free]** **brendangregg.com** — methodologies (USE method, flame graphs, the "Off-CPU" analysis), the reference site for the field.
- **Tools:** `perf`, **eBPF/bcc/bpftrace**, flame graphs, **Prometheus/Grafana**, **OpenTelemetry** distributed tracing (**Datadog** is in your stack). **SOP:** the **Principles of Chaos Engineering**; the RED method (Rate/Errors/Duration); error-budget policy; on-call hygiene.

**Getting started.** Read the Google **SRE book** parts I–II (free) for the reliability mental model; read **Gregg ch. 1–6** and *learn the USE method + flame graphs on a real workload you own*. Profiling your own ML inference is the perfect first exercise. **⇄**

**Going deeper.** eBPF programming (write custom bpftrace/bcc tools); tail-latency engineering; capacity modeling; then push into **Distributed Systems** (next section) for the theory behind the failures SRE manages. **⚙︎** Queueing theory (Little's Law, M/M/1, utilization→latency curves) is the quantitative backbone of both capacity planning and tail latency — a natural fit for you.

**≈ Time:** 3–5 months (performance half is faster to useful). **MVP:** Google SRE book Pt I–II + Gregg chs. 1–6 + profile-and-optimize one real service with flame graphs.

---

# CONNECTIVE TISSUE — Distributed Systems

Not on your list, but it's the glue across OS + Networking + SRE and the substrate under large-scale ML — worth a dedicated slot.

- **[Primary]** Martin Kleppmann, *Designing Data-Intensive Applications*, O'Reilly, 2017 — the modern classic on data systems, replication, consistency, and consensus. (A 2nd edition is in progress; the 1st remains canonical.)
- **[Free]** MIT **6.5840** (formerly 6.824) "Distributed Systems" — the labs (implement **Raft**, a fault-tolerant KV store, sharding) are the best hands-on distributed-systems experience available.
- **[Free]** Martin Kleppmann's Cambridge **Distributed Systems** lecture series (YouTube) + notes.
- **Core ideas:** consistency models, consensus (Raft/Paxos), replication, partitioning, the CAP/PACELC tradeoffs, exactly-once vs. at-least-once. **⚙︎** Consensus and failure-detector theory are impossibility-result-driven (FLP), congenial to a theory background.

**≈ Time:** 3–4 months. **MVP:** DDIA + 6.5840 Raft labs.

---

# TIER 3 — Optional Deep-Hardware Track

Do these only if the hardware/adversarial-physical direction appeals; each is very high resilience but a genuine specialization.

## 7. Linux Kernel Development

**Prereqs.** Phase 0 + OS. This is applied OS at production scale.

**What you need to know.** Kernel vs. user space in depth; the process scheduler (CFS/EEVDF); kernel memory management and the page allocator/slab; synchronization (spinlocks, RCU, memory barriers); the syscall path; interrupt handling; **device drivers**; the VFS and block layer; the networking stack; **eBPF**; and — critically — the *upstream development process*.

**Key textbooks**
- **[Primary]** Robert Love, *Linux Kernel Development*, 3rd ed., Addison-Wesley, 2010 — the best conceptual on-ramp (dated kernel version; concepts hold — verify against source).
- **[Supp./Free]** Jonathan Corbet, Alessandro Rubini & Greg Kroah-Hartman, *Linux Device Drivers (LDD3)*, 3rd ed., O'Reilly, 2005 — free; driver foundations (dated APIs, still formative).
- **[Supp.]** Daniel P. Bovet & Marco Cesati, *Understanding the Linux Kernel*, 3rd ed., O'Reilly, 2005; and Wolfgang Mauerer, *Professional Linux Kernel Architecture*, Wiley, 2008 — deep dives (older kernels).
- **[Supp./Free]** Mel Gorman, *Understanding the Linux Virtual Memory Manager* — deep on the mm subsystem.

**Courses, resources, standards & communities (SOP)**
- **[Free]** **LWN.net** — essential *ongoing* reading; the pulse of kernel development (much is free; a subscription is worth it).
- **[Free]** Linux Foundation **LFD103** "A Beginner's Guide to Linux Kernel Development"; **kernelnewbies.org** (first-patch tutorial); the in-tree `Documentation/process/` (submitting patches, the maintainer/LKML model, `checkpatch`).
- **SOP:** build and boot a custom kernel; write to coding style; the patch-submission etiquette is itself a skill.

**Getting started.** Love's book + **build/boot a custom kernel** + write a simple **character-device driver** (via LDD3 concepts, current APIs). Then land a *real* trivial patch (checkpatch/staging-driver cleanups) to learn the process.

**Going deeper.** Pick a subsystem (scheduler, mm, net, filesystems, or **eBPF**), read it against LWN coverage, and contribute upstream. Upstream contribution is the credential in this field.

**≈ Time:** 6–12+ months to real competence. **MVP:** Love's book + custom kernel build + one working module + one merged trivial patch.

## 8. Embedded Systems

**What you need to know.** Microcontrollers (ARM **Cortex-M**); bare-metal programming; **memory-mapped I/O** and registers; interrupts and NVIC; real-time constraints and **RTOS** basics; low-level debug (JTAG/SWD); reading **datasheets/reference manuals**; enough electronics to be dangerous; DSP/control basics.

**Key textbooks**
- **[Primary]** Elecia White, *Making Embedded Systems: Design Patterns for Great Software*, 2nd ed., O'Reilly, 2024 — the best modern intro; practical and current.
- **[Supp.]** Joseph Yiu, *The Definitive Guide to Arm Cortex-M3 and Cortex-M4 Processors*, 3rd ed., Newnes, 2013 — the ARM specifics.
- **[Supp./Free]** Edward A. Lee & Sanjit A. Seshia, *Introduction to Embedded Systems: A Cyber-Physical Systems Approach*, 2nd ed., MIT Press, 2017 — free; the theoretical/CPS view.
- **[Supp./Free · Rust]** *The Embedded Rust Book* and the *Discovery* book (Rust Embedded WG) — the strong modern Rust on-ramp.

**Courses, resources, standards & communities (SOP)**
- **Hardware:** an **STM32 Nucleo/Discovery** board or an **RP2040** (Pico) to start (cheap, well-documented).
- **[Free]** **Embedded.fm** (Elecia White's podcast + community); vendor reference manuals and the **ARM Architecture Reference Manual**.
- **SOP:** read the datasheet first; **MISRA C** in safety contexts; RTOS scheduling; deterministic timing; toolchains (`arm-none-eabi-gcc`, OpenOCD).

**Getting started.** Buy a board; blink an LED **bare-metal** (no HAL) by writing to registers; then read *Making Embedded Systems*; then an STM32 bare-metal series or the **Rust Discovery** book.

**Going deeper.** **RTOS internals** (FreeRTOS, **Zephyr**); real-time theory — Jane W. S. Liu, *Real-Time Systems*, Prentice Hall, 2000; safety-critical standards (DO-178C, IEC 61508); on-device DSP/ML (**⇄ TinyML** — running inference on MCUs is a natural bridge from your ML work). **⚙︎** Control loops, sampling theory, and DSP lean straight on your physics.

**≈ Time:** 4–8 months. **MVP:** bare-metal blink → UART → a small RTOS app on real hardware.

## 9. Firmware

**Why last.** Deepest hardware coupling; overlaps embedded but goes down into **boot and platform bring-up**. **⇄ Firmware security (secure/measured boot, chain of trust) is where this meets the crypto track.**

**What you need to know.** The **boot chain** (power-on → ROM → firmware → **bootloader** → OS); **bootloaders** (U-Boot); **UEFI** and **coreboot**; flash memory and storage; board bring-up and **board support packages**; **firmware/platform security** — secure boot, measured boot, **TPM**, root-of-trust.

**Key resources**
- **[Supp.]** Vincent Zimmer, Michael Rothman & Suresh Marisetty, *Beyond BIOS: Developing with the Unified Extensible Firmware Interface*, 3rd ed., De Gruyter, 2017 — the UEFI reference.
- **[Free]** **osdev.org** wiki — boot process, bootloaders, bare-metal from scratch.
- **[Free]** **Das U-Boot** documentation; **coreboot** docs; **EDK II** (the UEFI reference implementation) and its "build your first UEFI app" guides.
- **Security angle:** platform-firmware-security literature; **fwupd/LVFS**; secure-boot verification; firmware reverse-engineering (for the offensive/analysis side, which **⇄** connects to your fraud/abuse instincts).

**Standards & communities (SOP).** UEFI/PI specifications; the coreboot and U-Boot communities; the TCG (Trusted Computing Group) specs for TPM/measured boot; understand the chain-of-trust model end to end.

**Getting started.** Trace the full boot chain conceptually; build **U-Boot** for a supported board; write a minimal **UEFI application** with EDK II. Ground it on the embedded tier first — firmware without embedded fundamentals is rootless.

**Going deeper.** UEFI/EDK II driver development or **coreboot** porting to a board; firmware security (implement/verify a secure-boot chain — **⚙︎⇄** uses the signatures/hashing from your crypto tier); firmware analysis/reversing.

**≈ Time:** 4–8 months (after embedded). **MVP:** understand + document the boot chain end-to-end + build U-Boot + a "hello world" UEFI app.

---

# Cross-field capstone projects

Projects that fuse tiers and double as portfolio evidence (which, per your career map, matters more than tool-assisted breadth):

1. **Write a small OS kernel** (Rust, via Oppermann's guide) — fuses Phase 0 + OS + a slice of kernel/firmware (you touch the boot handoff).
2. **Build a JIT-compiled toy language on LLVM/MLIR, then profile and optimize the runtime** — fuses Compilers + Runtimes + Performance; **⇄** the exact skill set of ML-compiler/inference work.
3. **Implement TCP (CS144), add TLS 1.3 with a hand-rolled-for-learning crypto core (Cryptopals-grade), and run it under load with flame-graph profiling** — fuses Networking + Crypto + Performance.
4. **Implement Raft (6.5840) and instrument it with SLIs/SLOs + distributed tracing** — fuses Distributed Systems + SRE.
5. **TinyML on an MCU with a secure-boot chain** — fuses Embedded + Firmware + Crypto + (your) ML; a uniquely differentiated **⇄** project.

---

# Calibration — settled / contested / overstated

**Settled (consensus canon, safe to anchor on):** CS:APP, OSTEP, Cooper & Torczon / the Dragon Book, the GC Handbook, Katz–Lindell + Boneh–Shoup, Kurose & Ross, Stevens' TCP/IP, the Google SRE trilogy, and Brendan Gregg's *Systems Performance* are the field-standard references. The *core knowledge* in all nine fields is stable and slow-moving — your reading list will not rot the way a framework tutorial would.

**Contested (reasonable people disagree — decide deliberately):**
- **The Dragon Book's centrality.** Widely criticized as parsing-heavy and dated in emphasis; many practitioners prefer **Cooper & Torczon** and **Crafting Interpreters + Cornell CS6120** for a modern, optimization-and-backend view. Position taken here: Dragon as reference, not as your primary path.
- **C vs. Rust as *the* systems language.** Rust is genuinely ascendant (new kernels, embedded, tooling), but "C is obsolete" is false — you cannot read Linux, CPython, LLVM, or most embedded code without it. Position: C to read, Rust to build.
- **SRE as a distinct discipline** vs. "rebranded ops with SLOs." Fair debate; the SLO/error-budget framing is real intellectual content regardless of the label.
- **Whether "embedded" and "firmware" merit separate study** — they overlap heavily; some treat firmware as a subset of embedded. Kept separate here because the *boot/platform-security* layer is genuinely distinct.
- **"Learn everything low-level to do ML-systems"** — you don't need all nine to reach ML-systems; the spine (Phase 0 → OS → Compilers → Runtimes → Performance → Networking) is the load-bearing subset.

**Overstated / treat with skepticism (hype):**
- **"Write your own OS / learn assembly and the job follows."** Educationally superb; *direct* job relevance varies — pair it with a demonstrable specialization.
- **eBPF as a universal solvent.** Powerful and genuinely hot, but not a cure-all; learn it as a tool, not a religion.
- **Single-vendor tool mastery** (any one cloud/observability stack) as a durable skill — the *methodology* (USE method, SLOs, profiling discipline) travels; the specific dashboard does not.
- **Recency of the older kernel/networking texts.** Bovet & Cesati (2005), LDD3 (2005), Love (2010), Stevens (2011) are conceptually valuable but describe old versions — never treat their APIs/specifics as current; cross-check source + LWN/RFC updates.

---

# The MVP spine (if "no time pressure" ever changes)

You chose deep mastery, but here's the ~9–12 month load-bearing subset that yields real, durable, ML-systems-adjacent competence if pace ever compresses — do these in order and skip the rest:

1. **Phase 0 MVP:** CS:APP chs. 1–3, 6 + Bomb/Cache/Malloc labs.
2. **OS MVP:** OSTEP (all parts) + first 4 xv6 labs.
3. **Compilers MVP:** *Crafting Interpreters* (both interpreters) + LLVM Kaleidoscope.
4. **Runtimes MVP:** clox + a rewritten GC + read CPython's eval loop.
5. **Performance MVP:** Gregg chs. 1–6 + profile/optimize one real service.
6. **Networking MVP:** Kurose & Ross + Beej's + CS144 TCP labs.
7. *(pick one of)* **Crypto MVP** (Boneh Crypto I + Cryptopals 1–3 + Aumasson) **or** **Distributed MVP** (DDIA + 6.5840 Raft), by direction.

That spine is deliberately the ML-systems trunk plus one adversarial/distributed wing.

---

# Staying current — feeds, communities, SOPs

- **General systems:** **LWN.net** (kernel/systems), **Hacker News** (filter aggressively), **ACM Queue** and **USENIX** (**;login:**, and the **OSDI / SOSP / NSDI / ATC / EuroSys** proceedings — **[Free]**, the research frontier for OS/networking/systems).
- **Compilers/runtimes:** **LLVM Discourse**, the **V8** and **PyPy** blogs, **PLDI / CGO / OOPSLA** proceedings.
- **Crypto:** the **IACR ePrint archive** (eprint.iacr.org) **[Free]**, the **Real World Crypto** talks, the **NIST PQC** project pages.
- **Networking:** **IETF** drafts/RFCs, the **APNIC/Cloudflare** engineering blogs, **SIGCOMM**.
- **SRE/perf:** **brendangregg.com**, the **SREcon** talks (USENIX **[Free]**), Google's SRE site.
- **Embedded/firmware:** **Embedded.fm**, **Hackaday**, the **osdev** and **coreboot/EDK II** communities, **Interrupt (Memfault blog)**.
- **Universal SOP:** read primary sources (specs, RFCs, source) over blog summaries; implement to learn but ship vetted libraries; profile before optimizing; and in every one of these fields, *reading real production source* (kernel, LLVM, CPython, V8, U-Boot) is the deep-mastery accelerator that textbooks alone can't provide.

---

*Structure and sequencing chosen to lead with leverage; nothing dropped — Tier 3 is depth-on-tap, not a cut. Next steps I can take on request: (a) expand any single field into a full standalone phased curriculum with week-by-week pacing and exercise sets; (b) build the interleaved weekly schedule across tiers; or (c) produce the companion "projects to build/reproduce/extend" document in the format of your ML curricula.*