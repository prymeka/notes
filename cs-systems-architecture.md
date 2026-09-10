# A Multi-Year Graduate Self-Study Curriculum in Computer Systems & Architecture

*Balanced read + build · C and Rust throughout · graduate / qualifying-exam depth · resources current as of early 2026 (editions not live-verified this pass — see Caveats)*

## TL;DR
- A **14-phase, ~3.5–4.5 year** curriculum (compressible to ~18–22 months via the MVP fast-path) that carries you from NAND gates up through the modern systems research frontier (ISCA/MICRO/ASPLOS/OSDI/SOSP/NSDI/SIGCOMM/VLDB/SIGMOD/PLDI), built on canonical textbooks and seminal papers, with a concrete **C-or-Rust build artifact in every phase**.
- The **vertical spine** runs bottom-up — digital logic → architecture → the machine-level C view → OS → concurrency → compilers → networks → databases → distributed systems — then the four **boundary areas you selected** (accelerators/GPU, embedded/real-time, HPC, and the digital-logic on-ramp) plug in at their natural depth points, closing with a capstone.
- Systems is **settled** in its classical foundations (the memory hierarchy, virtual memory, TCP congestion control, ACID/MVCC, Paxos/Raft, linearizability) but **genuinely contested at the top** — the post-Dennard trajectory (general-purpose vs. domain-specific accelerators) is an open architectural bet, and several popular framings (CAP as "pick 2 of 3", RISC-vs-CISC, "NoSQL replaces SQL") are **oversimplified**; I flag these inline.
- **Overlap handled:** the hardware on-ramp stays at the **gate → ISA** abstraction (your Electronics track owns transistor/analog); the OS/architecture/security phases are the **general foundations that feed your GrapheneOS kernel work** rather than duplicating it; the embedded module stays on the **software/systems** side.

---

## Key orientation

**Why bottom-up + build.** Systems is the one CS cluster where the "build a small version of it" pedagogy dominates, because the abstractions only become real once you've implemented them. This curriculum pairs each canonical text with a lab: you'll build a CPU from gates (nand2tetris), extend a Unix kernel (xv6) and write one in Rust, implement lock-free structures and a language and a TCP stack and a database engine and Raft. The reading gives you the theory and the vocabulary of the field; the building gives you the intuition and the scar tissue.

**C then Rust, deliberately interleaved.** C is the lingua franca of the machine-level view and the existing canon (CS:APP, xv6, most kernels — and it feeds your GrapheneOS C work directly). Rust is introduced from Phase 3 onward and becomes a first-class build language for the OS, concurrency, networking, and embedded phases, where its ownership/`Send`+`Sync` model makes the systems invariants *explicit* in the type system. Where a canonical lab is in another language (xv6 in C, 6.5840 in Go, Crafting Interpreters in Java/C, 15-445 in C++), I note it and give the Rust-native alternative when one is good enough to stand in.

**Physics scaffolding (marked ⚛).** You have unusual leverage here. Landauer's principle sets the thermodynamic floor of irreversible computation; Dennard scaling and dark silicon are device physics you already know; Little's law and queueing govern throughput; Amdahl/Gustafson are scaling laws; and — the standout — Lamport's logical clocks were explicitly informed by *special relativity* (event ordering as more fundamental than absolute time). These are intuition bridges, not rigorous identities.

**Free-resource density.** A large fraction of the best material is legitimately free: OSTEP, nand2tetris, Crafting Interpreters, *The Rust Book*, *Rust Atomics and Locks*, "Writing an OS in Rust", the Embedded Rust Book, Peterson–Davie's open edition, van Steen–Tanenbaum's *Distributed Systems*, Kleppmann's lecture videos, Hellerstein's DB-architecture paper, and the MIT/CMU/Stanford course labs. Each is flagged **[FREE]** below; in-copyright books are marked **[BUY]** and pirated PDFs are not endorsed.

---

## The Phased Curriculum

**Legend.** Per phase: (a) Goal · (b) Prerequisites · (c) Primary (canonical texts + seminal papers) · (d) Supplementary · (e) Exercises + **Build** · (f) Time · (g) MVP fast-path. Status tags: **[SETTLED]**, **[CONTESTED]**, **[HYPE-WATCH]**. Physics bridges: ⚛.

---

### PHASE 1 — Digital Logic & Building a CPU from Gates (the on-ramp)
**(a) Goal.** Boolean logic, combinational and sequential circuits, and the gate → ALU → CPU → assembler → VM stack. End state: a working simple processor you built from NAND up, and comfort reading an HDL.

**(b) Prerequisites.** None internal. (Your Electronics track supplies the transistor-level story beneath the gate abstraction — we start *at* the gate.)

**(c) Primary.**
- Nisan & Schocken, *The Elements of Computing Systems* (nand2tetris), 2nd ed. (MIT Press, 2021). Book **[BUY]**; the **course, projects, and tools are [FREE]** at nand2tetris.org and on Coursera ("Build a Modern Computer from First Principles").
- Harris & Harris, *Digital Design and Computer Architecture, RISC-V Edition* (Morgan Kaufmann, 2021) **[BUY]** — for real depth on timing, FSMs, and an HDL (SystemVerilog).

**(d) Supplementary.** MIT 6.004 *Computation Structures* lecture materials **[FREE]**.

**(e) Exercises + Build.** **Build:** nand2tetris projects 1–6 — logic gates → ALU → memory → the Hack CPU → assembler. Optional stretch: re-implement a single-cycle RV32I datapath in Verilog or Chisel and simulate it.

**(f) Time.** 5–7 weeks.

**(g) MVP.** nand2tetris projects 1–5 only (through the CPU); defer the assembler/VM to Phase 7's context.

⚛ *Bridge:* a logic gate is a switching element; **Landauer's principle** (an irreversible bit erasure costs at least *kT* ln 2 of energy) is the thermodynamic reason logic dissipates heat — you'll meet it again at the power wall in Phase 4. **[SETTLED]** (Landauer's bound is experimentally confirmed; Bennett's reversible computing shows the erasure, not the computation, is what fundamentally costs.)

---

### PHASE 2 — Computer Architecture I: ISA, RISC-V, and the Single-Cycle→Pipelined Datapath
**(a) Goal.** Instruction-set design, the RISC-V ISA, assembly, the classic 5-stage pipeline, hazards and forwarding, and the hardware/software interface. Build and reason about a pipelined datapath.

**(b) Prerequisites.** Phase 1.

**(c) Primary.**
- Patterson & Hennessy, *Computer Organization and Design, RISC-V Edition*, 2nd ed. (Morgan Kaufmann, 2020) **[BUY]** — the standard undergraduate-into-graduate architecture text.
- The **RISC-V Unprivileged ISA specification** (riscv.org) **[FREE]**.
- Seminal: **Patterson & Ditzel, "The Case for the Reduced Instruction Set Computer" (1980)** (*ACM SIGARCH*) — read the founding RISC argument; **Amdahl (1967)** for the speedup law.

**(d) Supplementary.** Berkeley CS61C or CS152 materials **[FREE]**.

**(e) Exercises + Build.** **Build:** a **RISC-V (RV32I) emulator in Rust** — decode + execute the base integer ISA, run compiled C programs on it. (Rust's enums/pattern-matching make an instruction decoder a joy.) Extend with the pipeline model as a stretch.

**(f) Time.** 6–8 weeks.

**(g) MVP.** P&H COD chapters on the ISA and the pipelined datapath + the RV32I emulator; skip the peripheral I/O chapters.

**[HYPE-WATCH] The RISC-vs-CISC "debate" is largely moot today.** Modern x86 cores decode CISC instructions into internal RISC-like micro-ops, and the ISA matters far less than microarchitecture and process node. What *is* live is the open-ISA movement (RISC-V) as a licensing/ecosystem story, not a performance one.

---

### PHASE 3 — Systems Programming & the Machine (the CS:APP layer) + Rust entry
**(a) Goal.** How a program actually maps to the machine: data representation, assembly, the stack and calling conventions/ABI, linking and loading, the memory hierarchy from the programmer's side, and performance-aware C. This phase forges the **C fluency** the rest of the systems stack (and your GrapheneOS work) depends on, and starts Rust in parallel.

**(b) Prerequisites.** Phase 2. Runs well alongside Phase 4.

**(c) Primary.**
- Bryant & O'Hallaron, *Computer Systems: A Programmer's Perspective (CS:APP)*, 3rd ed. (Pearson, 2015) **[BUY]** — the single best "how the machine runs your code" book; CMU 15-213 lectures/labs are **[FREE]**.
- Klabnik & Nichols, *The Rust Programming Language* ("the book") **[FREE]** (doc.rust-lang.org/book) — start here for Rust; do **Rustlings [FREE]** alongside.

**(d) Supplementary.** *Dive into Systems* **[FREE]** (diveintosystems.org) as a gentler companion; K&R *The C Programming Language* as a C reference.

**(e) Exercises + Build.** **Build:** the **CS:APP labs** — Data Lab, Bomb Lab, Attack Lab (buffer overflows — directly relevant to hardened_malloc/GrapheneOS), and **Malloc Lab** (write your own allocator — a superb bridge to your GrapheneOS hardened_malloc goal). In Rust: work through Rustlings + rewrite a couple of small C utilities in Rust to feel the ownership model.

**(f) Time.** 8–10 weeks.

**(g) MVP.** CS:APP chapters on machine-level representation, the memory hierarchy, and linking + the Attack and Malloc labs; *The Rust Book* chs. 1–10.

⚛ *Bridge:* the memory hierarchy exists because **data movement, not computation, dominates energy** — moving a word from DRAM can cost orders of magnitude more energy than an ALU op, an idea you'll formalize in the roofline model (Phase 13). **[SETTLED]**

**GrapheneOS synergy flag:** Malloc Lab + the Attack Lab are the on-ramp to `hardened_malloc`; the memory-safety themes here motivate why Rust matters for systems security.

---

### PHASE 4 — Computer Architecture II: Microarchitecture, Memory Hierarchy, Multicore
**(a) Goal.** Out-of-order execution (Tomasulo), superscalar issue, branch prediction, speculation, deep cache design, virtual memory hardware, **cache coherence** (MESI) and **memory consistency models**, multicore, and the modern performance/power story. Graduate-depth quantitative reasoning about architecture.

**(b) Prerequisites.** Phases 2–3.

**(c) Primary.**
- Hennessy & Patterson, *Computer Architecture: A Quantitative Approach*, 6th ed. (Morgan Kaufmann, 2017/2019) **[BUY]** — the graduate architecture bible; work the appendices on memory hierarchy and the chapters on ILP, DLP, TLP, and the domain-specific-architectures chapter (which sets up Phase 11).
- Seminal: **Tomasulo, "An Efficient Algorithm for Exploiting Multiple Arithmetic Units" (1967)**; **Wulf & McKee, "Hitting the Memory Wall" (1995)**; **Hennessy & Patterson, "A New Golden Age for Computer Architecture" (CACM 2019)** — their Turing lecture; **Kocher et al. "Spectre" and Lipp et al. "Meltdown" (2018)** — speculation as a security boundary.

**(d) Supplementary.** Sorin, Hill & Wood, *A Primer on Memory Consistency and Cache Coherence* (Morgan & Claypool) — the clearest treatment of the consistency-model minefield.

**(e) Exercises + Build.** **Build:** a **cache simulator** (configurable associativity/replacement, driven by memory traces) and a **branch-predictor simulator** (bimodal → gshare → tournament), both in Rust or C; measure against real trace data. Extend the Phase-2 emulator with a cache model.

**(f) Time.** 9–12 weeks (the densest architecture phase).

**(g) MVP.** H&P chapters on ILP, memory hierarchy, and multiprocessor coherence + the cache simulator; the two 2018 speculation papers.

⚛ *Bridge:* **Dennard scaling** (your device-physics turf) and its breakdown → **dark silicon** (Esmaeilzadeh et al. 2011): you can't power all transistors at once, which is *the* physical driver of the pivot to accelerators. Throughput/latency trade-offs follow **Little's law** — a queueing identity that behaves like a conservation law. **[CONTESTED — see below.]**

**[CONTESTED] The post-Dennard trajectory is an open architectural bet.** Three camps: (1) Hennessy–Patterson's "new golden age" thesis — the future is **domain-specific accelerators** and open ISAs; (2) heterogeneous/chiplet integration as the main lever; (3) continued (slower) general-purpose gains from microarchitecture + packaging. This is a genuine live disagreement about where the field goes, not a settled fact — treat confident predictions skeptically.

---

### PHASE 5 — Operating Systems (OSTEP + xv6, and an OS in Rust)
**(a) Goal.** Processes and threads, CPU scheduling, virtual memory and paging, file systems, I/O, synchronization, kernel architecture (monolithic vs microkernel), virtualization, and containers. Build and extend a real (if small) kernel.

**(b) Prerequisites.** Phase 3. Phase 4's VM/coherence material deepens it.

**(c) Primary.**
- Arpaci-Dusseau & Arpaci-Dusseau, *Operating Systems: Three Easy Pieces (OSTEP)* **[FREE]** (ostep.org) — the best free OS text, and arguably the best OS text, full stop.
- Tanenbaum & Bos, *Modern Operating Systems* (5th ed., ~2022 — **verify edition**) **[BUY]**, or Silberschatz–Galvin–Gagne, *Operating System Concepts*, 10th ed. **[BUY]**, as a second reference.
- Seminal: **Ritchie & Thompson, "The UNIX Time-Sharing System" (1974)**; **Dijkstra, "The Structure of the THE Multiprogramming System" (1968)**; **Lampson, "Hints for Computer System Design" (1983)** — read this twice; **Saltzer, Reed & Clark, "End-to-End Arguments in System Design" (1984)**; **Denning, "The Working Set Model for Program Behavior" (1968)**.

**(d) Supplementary.** The xv6 book (*xv6: a simple, Unix-like teaching operating system*, MIT) **[FREE]**; Love, *Linux Kernel Development* as the bridge toward real kernels.

**(e) Exercises + Build.** **Build (primary):** the **MIT 6.1810 xv6 labs [FREE]** — implement syscalls, a copy-on-write fork, lazy allocation, a scheduler tweak, and a simple file-system change, all in C on the xv6 kernel. **Build (Rust path):** Philipp Oppermann's **"Writing an OS in Rust" [FREE]** (os.phil-opp.com) — a bare-metal kernel from scratch (VGA, interrupts, paging, async). Do at least the first through paging.

**(f) Time.** 12–16 weeks (can overlap Phase 6).

**(g) MVP.** OSTEP virtualization + concurrency + persistence "pieces" + the core xv6 syscall/page-table/COW labs.

**GrapheneOS synergy flag (important):** this is the load-bearing phase for your kernel track. Path forward: **OSTEP + xv6 (here) → Linux kernel internals (Love + LWN + the kernel source) → GrapheneOS `hardened_malloc` and kernel-hardening contributions (your other track).** The end-to-end argument and Lampson's hints are the design-taste foundation for that work.

⚛ *Bridge:* schedulers are resource-allocation policies under contention; the working-set model is a **locality** statement, kin to correlation length.

---

### PHASE 6 — Concurrency, Parallelism & Memory Models (the rigorous version)
**(a) Goal.** Threads, mutual exclusion, condition variables, lock-free and wait-free algorithms, **linearizability** as the correctness condition, transactional memory, and — with real rigor — **relaxed memory models** (the C/C++11 model and Rust's `Send`/`Sync` + atomics model). This is where C and Rust concurrency both pay off.

**(b) Prerequisites.** Phase 3; complements Phase 5. Feeds Phases 9 and 10.

**(c) Primary.**
- Herlihy & Shavit, *The Art of Multiprocessor Programming*, 2nd ed. (Morgan Kaufmann, 2020/2021) **[BUY]** — the canonical text.
- Williams, *C++ Concurrency in Action*, 2nd ed. (Manning, 2019) **[BUY]** for the C++ memory model in practice.
- Bos, *Rust Atomics and Locks* (O'Reilly, 2023) **[FREE online]** (marabos.nl/atomics) — the clearest practical treatment of atomics/orderings anywhere, in Rust.
- Seminal: **Herlihy & Wing, "Linearizability: A Correctness Condition for Concurrent Objects" (1990)**; **Herlihy, "Wait-Free Synchronization" (1991)** — the consensus hierarchy; **Boehm & Adve, "Foundations of the C++ Concurrency Memory Model" (2008)**; Lamport's bakery algorithm (1974).

**(d) Supplementary.** McKenney, *Is Parallel Programming Hard, And, If So, What Can You Do About It?* **[FREE]** (perfbook) — RCU and real-world kernel concurrency.

**(e) Exercises + Build.** **Build:** implement a **Treiber lock-free stack** and the **Michael–Scott lock-free queue** in *both* C++ (with `std::atomic` + explicit orderings) and Rust (with `std::sync::atomic`), then a **work-stealing scheduler**. Reason explicitly about the memory-ordering annotations and why each is necessary.

**(f) Time.** 8–11 weeks.

**(g) MVP.** Herlihy–Shavit chs. on mutual exclusion, linearizability, and lock-free structures + Bos's atomics chapters + the Treiber/Michael–Scott builds.

**[HYPE-WATCH] "Fearless concurrency" is real but bounded.** Rust's ownership model genuinely eliminates data races *in safe code* — a substantive advance. But it does **not** eliminate deadlocks, livelocks, or logic races, and `unsafe` + atomics still demand the full memory-model reasoning above. Memory-consistency models remain one of the most commonly-gotten-wrong areas in all of systems. **[SETTLED that the model is subtle.]**

---

### PHASE 7 — Compilers & Language Runtimes
**(a) Goal.** Lexing, parsing, ASTs, type checking, IRs, optimization, code generation, register allocation, plus runtime concerns — garbage collection and JIT. Build a working language end-to-end.

**(b) Prerequisites.** Phase 3 (machine-level view). Some Phase 2 (target ISA).

**(c) Primary.**
- Nystrom, *Crafting Interpreters* **[FREE online]** (craftinginterpreters.com) **[BUY for print]** — build a tree-walking interpreter (Java) then a bytecode VM (C). The best modern build-a-language book.
- Aho, Lam, Sethi & Ullman, *Compilers: Principles, Techniques, and Tools* (the "Dragon Book"), 2nd ed. (2006) **[BUY]** for theory (parsing, dataflow, optimization); or Cooper & Torczon, *Engineering a Compiler*, 3rd ed. (~2022 — **verify**) **[BUY]** for a more modern, IR-and-optimization-forward treatment.

**(d) Supplementary.** Appel, *Modern Compiler Implementation in ML/C/Java*; the LLVM "Kaleidoscope" tutorial **[FREE]** for an LLVM-backend project; Jones et al., *The Garbage Collection Handbook* for GC depth.

**(e) Exercises + Build.** **Build:** *Crafting Interpreters* in full (both interpreters). Stretch (**Rust**): reimplement the bytecode VM in Rust, or build a small compiler front-end that emits **LLVM IR** and lowers to native code. Connects to your **Python-internals** interest — CPython's bytecode VM is the same architecture as `clox`.

**(f) Time.** 10–13 weeks.

**(g) MVP.** *Crafting Interpreters* Part III (the bytecode VM) + Dragon Book chapters on lexing/parsing and dataflow analysis.

⚛ *Bridge (light):* compiler optimization is **search over a program-transformation space** under a cost model; register allocation is graph coloring (an NP-hard problem you met in the theory curriculum — here solved heuristically).

---

### PHASE 8 — Computer Networks
**(a) Goal.** The layered stack, IP and routing, **TCP and congestion control**, DNS/HTTP, the end-to-end principle, and modern topics — QUIC, TLS 1.3, SDN, and data-center networking. Implement a transport protocol.

**(b) Prerequisites.** Phase 3 (sockets/systems basics). Largely parallelizable — can run early.

**(c) Primary.**
- Kurose & Ross, *Computer Networking: A Top-Down Approach*, 8th ed. (Pearson, ~2020) **[BUY]** — the standard, pedagogically excellent.
- Peterson & Davie, *Computer Networks: A Systems Approach* — **open-source edition [FREE]** (systemsapproach.org) — the systems-oriented complement; also good on modern topics via their companion books.
- Seminal: **Cerf & Kahn, "A Protocol for Packet Network Intercommunication" (1974)**; **Jacobson, "Congestion Avoidance and Control" (1988)**; the end-to-end argument (already read in Phase 5); optionally the **BBR** congestion-control paper (Cardwell et al., 2016).

**(d) Supplementary.** Tanenbaum & Wetherall, *Computer Networks*, 6th ed. **[BUY]** for breadth; Beej's Guide to Network Programming **[FREE]** for sockets.

**(e) Exercises + Build.** **Build:** a **user-space TCP/IP stack** in Rust or C — Ethernet/ARP/IP/ICMP and a minimal TCP with the three-way handshake and a congestion-control scheme (study **smoltcp** in Rust as a reference); or, lighter, a **reliable-transport protocol over UDP** (sliding window + AIMD). Do Kurose–Ross's socket-programming assignments first.

**(f) Time.** 8–10 weeks.

**(g) MVP.** Kurose–Ross transport + network layers + the UDP-reliable-transport build; Jacobson 1988.

⚛ *Bridge:* AIMD congestion control is a **feedback control loop** seeking a stable operating point — the same negative-feedback stabilization you know from physics/EE; the sawtooth is a limit cycle.

---

### PHASE 9 — Databases & Storage Engines
**(a) Goal.** The relational model, storage and indexing (**B+-trees and LSM-trees**), query processing and optimization, **transactions and concurrency control** (ACID, MVCC, isolation levels), logging and recovery (**ARIES**), and column/streaming/distributed stores. Build a working storage-and-execution engine.

**(b) Prerequisites.** Phase 3; Phase 6 (concurrency control needs the concurrency foundations); some Phase 5 (buffer management ≈ paging).

**(c) Primary.**
- Kleppmann, *Designing Data-Intensive Applications (DDIA)* (O'Reilly, 2017; **2nd ed. in progress — verify status**) **[BUY]** — the indispensable systems-of-data book, and a bridge into Phase 10.
- Silberschatz, Korth & Sudarshan, *Database System Concepts*, 7th ed. (McGraw-Hill, ~2019) **[BUY]** for the relational/transaction theory.
- Petrov, *Database Internals* (O'Reilly, 2019) **[BUY]** — storage engines and distributed data, deep and practical.
- Seminal: **Codd, "A Relational Model of Data for Large Shared Data Banks" (1970)**; **Mohan et al., "ARIES" (1992)**; **Hellerstein, Stonebraker & Hamilton, "Architecture of a Database System" (2007) [FREE PDF]** — read this first as the map; the **C-Store**/column-store paper (Stonebraker et al. 2005); **Verbitski et al., "Amazon Aurora" (2017)**.

**(d) Supplementary.** Andy Pavlo's **CMU 15-445/645** lectures **[FREE]** (YouTube) — the best database-systems course available.

**(e) Exercises + Build.** **Build:** **CMU 15-445 BusTub [FREE]** projects — a buffer-pool manager, a **B+-tree index**, a query executor, and **concurrency control** (2PL/MVCC), in C++. (Note: C++, not C/Rust — but the closest thing to a canonical DB-internals lab, and worth the exception. A Rust stretch: implement an **LSM-tree** engine, e.g. following the "mini-LSM" project.)

**(f) Time.** 12–15 weeks.

**(g) MVP.** Hellerstein architecture paper + DDIA storage/transaction chapters + the BusTub buffer-pool and B+-tree projects.

**PayPal relevance flag:** transaction isolation, MVCC, and the OLTP/analytics split map directly onto production data systems you already work near; DDIA's chapters on replication/partitioning set up Phase 10.

**[HYPE-WATCH] "NoSQL replaced relational" is wrong.** The 2010s NoSQL wave traded transactional guarantees for scale; the 2020s "NewSQL"/distributed-SQL turn (Spanner, CockroachDB, etc.) largely brought ACID back at scale. Isolation levels are routinely misunderstood — "read committed" and "snapshot isolation" are *not* serializability, and many production anomalies live in that gap.

---

### PHASE 10 — Distributed Systems
**(a) Goal.** Logical/vector clocks, consistency models, **consensus (Paxos/Raft/BFT)**, replication, the **CAP/PACELC** framing, distributed transactions, and the classic Google-systems lineage. Build a replicated, fault-tolerant service.

**(b) Prerequisites.** Phases 6, 8, 9.

**(c) Primary.**
- van Steen & Tanenbaum, *Distributed Systems*, 4th ed. (~2023 — **verify**) **[FREE PDF]** (distributed-systems.net).
- Kleppmann, *DDIA* — the distributed chapters (consistency, consensus, replication, partitioning); pair with **Kleppmann's Distributed Systems lecture videos [FREE]** (Cambridge, on YouTube).
- Seminal (read these as a set): **Lamport, "Time, Clocks, and the Ordering of Events in a Distributed System" (1978)**; **Lamport, "The Part-Time Parliament" (1998)** and **"Paxos Made Simple" (2001)**; **Ongaro & Ousterhout, "In Search of an Understandable Consensus Algorithm (Raft)" (2014)**; **Fischer, Lynch & Paterson, "Impossibility of Distributed Consensus with One Faulty Process" (1985)** — the FLP result; **Gilbert & Lynch, "Brewer's Conjecture and the Feasibility of Consistent, Available, Partition-Tolerant Web Services" (2002)** — the CAP proof; **Dean & Ghemawat, "MapReduce" (2004)**; **Ghemawat et al., "The Google File System" (2003)**; **Chang et al., "Bigtable" (2006)**; **DeCandia et al., "Dynamo" (2007)**; **Corbett et al., "Spanner" (2012)**.

**(d) Supplementary.** Cachin, Guerraoui & Rodrigues, *Introduction to Reliable and Secure Distributed Programming* for the rigorous abstractions (broadcast, consensus, BFT).

**(e) Exercises + Build.** **Build:** the **MIT 6.5840 (formerly 6.824) labs [FREE]** — implement **Raft** (leader election, log replication, persistence) and build a **sharded, fault-tolerant key-value store** on top. Course language is **Go** (worth using here — it's canonical and the labs are excellent; a Rust Raft is a fine stretch but not the recommended first pass).

**(f) Time.** 14–18 weeks (with the labs, this is a major undertaking).

**(g) MVP.** Lamport 1978 + Raft 2014 + FLP + CAP proof + the Raft lab (leader election + log replication).

⚛ *Bridge (the standout):* **Lamport's logical clocks were explicitly informed by special relativity** — in the absence of a global "now," what's fundamental is the *causal ordering* of events (the happens-before relation), exactly as simultaneity is frame-relative and only the light-cone/causal structure is invariant. Vector clocks are the discrete analog of tracking causal past. This is the ideal bridge for a physicist.

**[HYPE-WATCH] CAP is routinely oversimplified.** The "pick 2 of 3" slogan is misleading: partitions are not optional (you don't "choose" CP vs AP in calm weather), and consistency/availability trade off only *during* a partition. **Kleppmann's "A Critique of the CAP Theorem" (2015)** is the corrective, and **PACELC** (Abadi) is the more precise framing: during a **P**artition trade **A**vailability vs **C**onsistency, **E**lse (normal operation) trade **L**atency vs **C**onsistency. **[SETTLED that the slogan is too coarse.]**

---

### PHASE 11 — Accelerators & Domain-Specific Hardware (GPU / TPU / FPGA)
**(a) Goal.** GPU architecture and the CUDA/SIMT programming model, **systolic arrays and TPUs/NPUs**, FPGAs, interconnects, and hardware/software co-design for ML. High leverage given your ML background.

**(b) Prerequisites.** Phase 4 (memory hierarchy, DLP). Phase 13 extends it toward HPC.

**(c) Primary.**
- Hwu, Kirk & El Hajj, *Programming Massively Parallel Processors (PMPP)*, 4th ed. (Morgan Kaufmann, 2022) **[BUY]** — the CUDA/GPU-architecture standard.
- Hennessy & Patterson, *CA:AQA* 6th ed. — the **domain-specific architectures** chapter (already owned from Phase 4).
- Seminal: **Jouppi et al., "In-Datacenter Performance Analysis of a Tensor Processing Unit" (ISCA 2017)** — read the TPU paper closely; Kung's systolic-array work (1982); **Esmaeilzadeh et al., "Dark Silicon and the End of Multicore Scaling" (2011)** (revisited from Phase 4).

**(d) Supplementary.** **Stanford CS149** *Parallel Computing* **[FREE]**; the CUDA C++ Programming Guide **[FREE]**; for FPGAs, a Chisel/Verilog accelerator tutorial.

**(e) Exercises + Build.** **Build:** **CUDA programming** (PMPP labs) — tiled matrix multiply, parallel reduction, scan, and a convolution kernel; profile and optimize for memory coalescing and occupancy. This is directly transferable to your **deep-learning / GNN** work at PayPal. Stretch: a simple **systolic matmul on an FPGA** in Chisel.

**(f) Time.** 8–11 weeks.

**(g) MVP.** PMPP chapters through shared-memory tiling + the tiled-matmul and reduction kernels + the TPU paper.

⚛ *Bridge:* the GPU is a **throughput machine** trading latency for parallelism — the roofline model (Phase 13) makes the arithmetic-intensity trade-off quantitative; systolic arrays are **dataflow** structures where data rhythmically pulses through a mesh (the name is literally a heartbeat analogy).

**[CONTESTED]** How far the accelerator wave goes — whether ML compute consolidates on a few architectures (GPU/TPU) or fragments into many domain-specific chips — is the open bet from Phase 4, seen from the hardware side.

---

### PHASE 12 — Embedded & Real-Time Systems (software / systems side)
**(a) Goal.** RTOS concepts, **real-time scheduling** (rate-monotonic and EDF, with the schedulability bounds), interrupt-driven and memory-constrained programming, and **embedded Rust** on a microcontroller. Kept to the software/systems layer (your Electronics track owns the hardware/analog interfacing).

**(b) Prerequisites.** Phases 2–3; some Phase 5 (scheduling/memory).

**(c) Primary.**
- Buttazzo, *Hard Real-Time Computing Systems*, 3rd ed. (Springer, 2011) **[BUY]** — the canonical real-time-scheduling theory (RM, EDF, Liu & Layland bounds, priority inheritance).
- **The Embedded Rust Book [FREE]** (docs.rust-embedded.org/book) + the **Discovery book [FREE]** — embedded Rust from scratch.
- Seminal: **Liu & Layland, "Scheduling Algorithms for Multiprogramming in a Hard-Real-Time Environment" (1973)** — the founding real-time-scheduling paper (the RM bound and EDF optimality).

**(d) Supplementary.** White, *Making Embedded Systems* (O'Reilly; **verify edition**) **[BUY]** for the pragmatics; FreeRTOS documentation **[FREE]**.

**(e) Exercises + Build.** **Build:** **embedded Rust on an STM32/Discovery board** — GPIO, timers, interrupts, and a small **cooperative or preemptive task scheduler** (or run an RTOS like RTIC/Embassy). Implement and measure an **EDF or rate-monotonic scheduler** and check a task set against its schedulability bound. (This dovetails with your Electronics hardware work — bring your own board.)

**(f) Time.** 7–9 weeks.

**(g) MVP.** Liu & Layland 1973 + the RM/EDF chapters of Buttazzo + the embedded-Rust blinky→interrupts→scheduler progression.

**Overlap flag:** analog peripheral interfacing, signal integrity, and board bring-up belong to your **Electronics** track; here we stay on scheduling, concurrency-under-constraint, and the embedded-Rust toolchain.

---

### PHASE 13 — High-Performance & Parallel Computing
**(a) Goal.** Parallel programming models (**OpenMP, MPI, SIMD/vectorization**), the **roofline** performance model, NUMA, cache-aware and communication-avoiding algorithm design, and GPU compute for scientific workloads. Make real code fast on real hardware.

**(b) Prerequisites.** Phases 4, 6, 11.

**(c) Primary.**
- Hager & Wellein, *Introduction to High Performance Computing for Scientists and Engineers* (CRC Press; **verify for a 2nd ed.**) **[BUY]** — the best node-level-performance-and-parallelism text; strong on the roofline model and cache effects.
- McCool, Reinders & Robison, *Structured Parallel Programming* (Morgan Kaufmann, 2012) **[BUY]** — parallel patterns (map/reduce/scan/stencil) done properly.
- Seminal: **Williams, Waterman & Patterson, "Roofline: An Insightful Visual Performance Model for Multicore Architectures" (CACM 2009)**; **Gustafson, "Reevaluating Amdahl's Law" (1988)**.

**(d) Supplementary.** The OpenMP and MPI standard documents **[FREE]**; "Introduction to Parallel Computing" (Grama et al.) for algorithm design.

**(e) Exercises + Build.** **Build:** take a **scientific kernel you understand from physics** (an N-body step, a stencil/PDE solver, or a dense linear-algebra routine) and parallelize it — first **SIMD-vectorize** the hot loop, then **OpenMP** across cores, then **MPI** across nodes, then a **CUDA** version; do a **roofline analysis** at each step and explain where you hit the memory vs. compute bound. This is where your physics-simulation background becomes a direct asset.

**(f) Time.** 9–12 weeks.

**(g) MVP.** Hager–Wellein roofline + node-level chapters + the OpenMP-and-SIMD version of one kernel + the roofline paper.

⚛ *Bridge:* the **roofline model** is a back-of-envelope plot (attainable FLOP/s vs. arithmetic intensity, capped by peak compute and peak bandwidth) that behaves exactly like the limiting-regime plots you draw in physics — you read off whether you're "bandwidth-bound" or "compute-bound" the way you read a dominant-balance argument. **Amdahl vs Gustafson** are two scaling laws (fixed-problem vs fixed-time), a distinction physicists find natural. **[SETTLED.]**

---

### PHASE 14 (Capstone) — A Full-Stack Systems Project + the Frontier
**(a) Goal.** Integrate the stack into one substantial artifact, and transition to reading and (optionally) producing frontier systems work.

**(b) Prerequisites.** Most of Phases 1–13.

**(c) Capstone options (pick one).**
- A **small distributed data system** end-to-end: a Raft-replicated, sharded, transactional key-value store with a query layer and a real congestion-aware RPC transport (pulls Phases 6/8/9/10 together).
- A **systems-level ML-serving stack**: a GPU-accelerated inference server with batching, a memory-managed runtime, and observability (pulls Phases 4/6/11/13 together — closest to your day job).
- A **real GrapheneOS contribution**: land a `hardened_malloc` or kernel-hardening change (converts this whole curriculum into your other track's MVP milestone).

**(d) Frontier tracking.** Venues: **ISCA, MICRO, ASPLOS** (architecture); **OSDI, SOSP** (systems); **NSDI, SIGCOMM** (networking); **VLDB, SIGMOD** (data); **PLDI, POPL** (languages). Reading lists: the **MIT 6.5840** and **CMU/Stanford advanced-systems** paper lists; "Papers We Love"; USENIX **[FREE]** proceedings; the annual **"A New Golden Age"**-style retrospectives.

**(e) Build.** The capstone itself, iterated to something you'd show.

**(f) Time.** Ongoing (3–6 months for a solid capstone).

**(g) MVP.** Ship a reduced version of one capstone option + start a standing paper-reading habit (one systems paper/week).

---

## Dependency Map

```
P1 Digital logic ─► P2 Architecture I ─► P4 Architecture II ─► P11 Accelerators
                        │                     │                      │
                        ▼                     ▼                      ▼
                   P3 CS:APP / C ───────────► (memory hierarchy)   P13 HPC/Parallel
                    │  │  │                                          ▲
        ┌───────────┘  │  └──────────────┐                          │
        ▼              ▼                 ▼                          │
   P5 OS ◄────► P6 Concurrency      P7 Compilers                    │
   (xv6 / Rust) │  (feeds 9,10,13) ──┘                              │
        │       │                                                   │
        │       └───────────────► P13 (parallel foundations)───────┘
        ▼
   P8 Networks ──┐
                 ▼
   P9 Databases ─► P10 Distributed Systems ─► P14 Capstone + Frontier
                        (needs P6, P8, P9)         (integrates most)

   P12 Embedded/Real-time: needs P2–P3 (+ some P5); otherwise standalone.
   Rust thread: begins in P3 → load-bearing in P5, P6, P8, P12.
```

**Sequential trunk:** P1 → P2 → P4, and P3 → P5 → (P6). Do P1–P6 roughly in order.
**Run early / in parallel:** P8 (Networks) any time after P3; P12 (Embedded) fairly standalone after P3; P7 (Compilers) after P3, parallel to the OS/networks work.
**Attach points:** P11 after P4; P9 after P3+P6; P10 after P8+P9; P13 after P4+P6+P11; capstone last.

---

## Overall MVP Fast-Path (~18–22 months part-time)
1. **Machine + logic (compressed):** nand2tetris projects 1–5 (Phase 1) + CS:APP machine/memory/linking chapters and the Attack + Malloc labs (Phase 3) + *The Rust Book* chs. 1–10.
2. **Architecture core:** P&H COD ISA + pipeline (Phase 2) and H&P *CA:AQA* ILP + memory-hierarchy + coherence chapters (Phase 4), with the RISC-V emulator and cache simulator.
3. **OS + concurrency:** OSTEP (all three pieces) + core xv6 labs (Phase 5) + Herlihy–Shavit linearizability/lock-free + Bos's atomics + the Treiber/Michael–Scott builds (Phase 6).
4. **Data + distribution:** DDIA (storage/transactions/replication/consensus chapters) + the BusTub buffer-pool/B+-tree labs (Phase 9) + the 6.5840 Raft lab and the core distributed papers (Lamport 1978, Raft, FLP, CAP) (Phase 10).
5. **One boundary area at depth** — given your profile, **Phase 11 (GPU/accelerators)** is the highest-leverage (direct ML transfer); **Phase 13 (HPC)** is second (leverages your physics-simulation background most directly).
6. **Capstone:** the ML-serving-stack option, reduced.

---

## Recommendations

**Staged plan (assuming ~10–15 hrs/week).**
1. **Months 0–8:** Phases 1–3 (logic → architecture I → CS:APP + Rust). *Benchmark:* your RISC-V emulator runs a compiled C program; you pass the Attack and Malloc labs.
2. **Months 8–20:** Phase 4 + Phase 5, with Phase 6 interleaved. *Benchmark:* the core xv6 labs pass; you've implemented a correct lock-free queue in Rust and can explain every memory-ordering annotation.
3. **Months 20–34:** Phases 7, 8, 9 (compilers, networks, databases) — these can rotate. *Benchmark:* Crafting Interpreters' bytecode VM works; your UDP-reliable-transport passes a loss test; BusTub's B+-tree passes.
4. **Months 34–46:** Phase 10 (distributed — the Raft lab is the centerpiece) + Phase 11 (GPU). *Benchmark:* your Raft passes the election + log-replication tests; your tiled CUDA matmul hits a respectable fraction of peak.
5. **Months 46+:** Phases 12–13 (embedded, HPC) as interest dictates, then the capstone. *Benchmark:* ship one capstone option.

**Where the forks you chose change the plan.** *Balanced* emphasis means the labs are non-negotiable, not optional — budget roughly half your time for building. *C + Rust* means Rust threads from Phase 3 onward and becomes the default for the OS-in-Rust, concurrency, TCP-stack, and embedded builds, while C remains for CS:APP/xv6 (and feeds GrapheneOS). *All four boundary areas in* is ambitious — if time compresses, keep **Phase 11 (accelerators)** and **Phase 13 (HPC)** at full depth (highest transfer to your work) and treat **Phase 12 (embedded)** as the one to trim, since your Electronics/GrapheneOS tracks already touch adjacent ground.

**Best free lecture courses (all [FREE]).** MIT 6.1810 (OS/xv6), MIT 6.5840 (distributed/Raft), CMU 15-445 (databases, Pavlo), CMU 15-213 (CS:APP), Stanford CS149 (parallel), Berkeley CS152/CS252 (architecture), MIT 6.004 (computation structures), nand2tetris (Coursera), Kleppmann's distributed-systems series (YouTube).

**Frontier-tracking shortlist.** USENIX (OSDI/NSDI/ATC) open-access proceedings; ACM DL for ISCA/MICRO/ASPLOS/SOSP/SIGCOMM/VLDB/SIGMOD/PLDI; "Papers We Love"; the systems reading lists attached to 6.5840 and the CMU advanced-systems courses; LWN.net for the Linux-kernel frontier (and your GrapheneOS track).

---

## Caveats
- **Editions not live-verified this pass.** The editions above reflect my knowledge as of early 2026; I could not run a live check this turn. Verify especially: **DDIA** (a 2nd edition has been in progress/early-release — check before buying the 1st), **Tanenbaum & Bos *Modern Operating Systems*** (4th vs 5th ed.), **Cooper & Torczon *Engineering a Compiler*** (3rd ed. year), **van Steen & Tanenbaum *Distributed Systems*** (4th ed. — free, confirm the current PDF), **Hager & Wellein** and **White *Making Embedded Systems*** (possible newer editions). If you re-enable the Research toggle I'll verify the whole list and update links.
- **Free-vs-paid.** The **[FREE]** items are legitimately free from authors/publishers/universities (OSTEP, nand2tetris course, Crafting Interpreters online, *The Rust Book*, *Rust Atomics and Locks* online, Writing an OS in Rust, Embedded Rust Book, Peterson–Davie open edition, van Steen–Tanenbaum, Kleppmann's videos, Hellerstein's paper, the MIT/CMU/Stanford labs, most seminal papers via authors' pages or DOI). In-copyright **[BUY]** books (H&P, P&H, CS:APP, Tanenbaum, Dragon Book, DDIA, Herlihy–Shavit, PMPP, Buttazzo, etc.) should be purchased — I don't endorse pirated PDFs.
- **Overlap boundaries.** Digital logic here stops at the gate/HDL level (Electronics owns transistors/analog/RF); the OS/architecture/security phases are the general foundations feeding your GrapheneOS kernel track, not a substitute for it; the embedded phase is software/systems-side only.
- **Calibration.** I've tagged the genuinely contested/oversimplified spots — the post-Dennard architectural trajectory **[CONTESTED]**, CAP-as-slogan and NoSQL-replaces-SQL and RISC-vs-CISC **[HYPE-WATCH]**, and the real-but-bounded scope of Rust's concurrency guarantees. Treat any source that presents these as settled with suspicion.
- **Scope realism.** This is a genuine multi-year, build-heavy program; the estimates assume a mathematically mature learner at ~10–15 hrs/week. Depth-over-breadth (full spine + accelerators + HPC at depth, embedded trimmed if needed) is the realistic route to the frontier.