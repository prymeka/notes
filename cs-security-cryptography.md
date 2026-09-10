# A Multi-Year Graduate Self-Study Curriculum in Security & Cryptography

*Self-contained · balanced offensive + defensive · balanced read + build · graduate / qualifying-exam depth · resources current as of early 2026 (editions, tool versions, and standards NOT live-verified this pass — see Caveats; security moves fast)*

## TL;DR
- A **15-phase, ~4–5 year** curriculum (compressible to ~20–24 months via the MVP fast-path) spanning the whole cluster: cryptography (foundations → applied engineering → post-quantum), software & systems security (exploitation and defense), network & web security, hardware & side-channel attacks, reverse engineering & malware, digital forensics & incident response, and adversarial ML — canonical texts + seminal papers, with an offensive-and-defensive lab in every phase.
- Structured as **parallel strands over a shared foundation**: after a security-foundations phase, the crypto strand, the software/systems-security strand, and the adversarial-ML strand can run largely in parallel; the hardware/side-channel strand attaches after crypto; forensics attaches after RE. The dependency map makes this explicit.
- This cluster is **exceptionally well-matched to your background**: power analysis is signal extraction from noise (SNR, correlation, matched filtering); TEMPEST is electromagnetics; acoustic side channels are acoustics + DSP; Rowhammer is DRAM charge-leakage physics; fault injection is device physics; and cryptographic hardness is the computational complexity from your theory track. And the whole discipline is *adversarial* — the same frame as your fraud work. Bridges marked ⚛.
- **Calibration is central to security**, where the gap between claimed and proven is wide: I tag the genuinely open/contested spots — one-way-function existence `[OPEN]`, post-quantum migration `[EVOLVING]` (with the SIKE break as the cautionary tale), adversarial-ML robustness `[OPEN/HYPE-WATCH]` (no robust defense survives adaptive attacks), speculative-execution mitigation `[OPEN]` — and the marketing to discount (confident attribution, "AI-powered security", "unhackable" blockchains, compliance-as-security).
- **Self-contained by your choice, but coordinated:** the crypto strand references your existing crypto track for ZK/MPC/FHE/pairing/PQC *depth* rather than re-deriving it; the systems-security phases are the general foundations that feed your **GrapheneOS** hardening work; the microarchitectural-attack material builds on your **systems** curriculum's speculation chapter; and adversarial ML is flagged where it overlaps your **ML** track.

---

## Key orientation

**Parallel strands, one mindset.** Security is not one field — it's cryptography, systems exploitation, network/web defense, hardware attacks, malware RE, forensics, and ML security, each with its own literature and venues. What unifies them is the **adversarial mindset**: assume an intelligent, adaptive attacker, reason about the weakest link, and never confuse "we couldn't break it" with "it's secure." This curriculum front-loads that mindset (Phase 1) and then lets the strands run in the order that suits you. Because you work in fraud — an adversarial domain — this frame is already native to you; the curriculum makes it rigorous and extends it to the systems, hardware, and cryptographic layers.

**Offense and defense, together, every phase.** "Balanced" here means each phase pairs the attack with its defense: you write the stack-overflow exploit *and* implement/评估 the mitigation; you run the padding-oracle attack *and* build the constant-time comparison; you craft the adversarial example *and* try (and watch fail) to defend against it. Attacking teaches you where the real boundaries are; defending teaches you why they hold or don't. Tooling follows the task — Python for crypto/tooling/ML, C for exploitation and side-channel, Rust for secure-systems builds (and your GrapheneOS work).

**Physics scaffolding (⚛).** This cluster has the richest physics payoff after graphics. The headline bridges: **power analysis** (DPA/CPA) is signal-from-noise extraction — SNR, correlation, matched filtering, hypothesis testing; **TEMPEST/compromising emanations** are electromagnetics and **acoustic side channels** are acoustics + DSP (both your turf, and TEMPEST/acoustic-keystroke inference is on your interest list); **Rowhammer** is DRAM cell charge-leakage/disturbance (solid-state physics); **fault injection** (voltage/clock glitching, laser fault injection) is device physics; **cryptographic hardness** is computational complexity (one-way functions ↔ the Liu–Pass meta-complexity result from your theory track); **information-theoretic security** is Shannon perfect secrecy and entropy; and **quantum attacks** (Shor) tie to your quantum/theory knowledge.

**Free-resource density.** An unusual amount of the best material is legitimately free — Ross Anderson's *Security Engineering* (3rd ed.), Boneh–Shoup's *A Graduate Course in Applied Cryptography*, the CryptoPals/CryptoHack platforms, MIT 6.858, the PortSwigger Web Security Academy, pwn.college, OverTheWire, Yurichev's RE book, Ghidra, ChipWhisperer, Volatility, and MITRE ATT&CK. Each is flagged **[FREE]**; in-copyright books are **[BUY]**, pirated PDFs not endorsed.

---

## The Phased Curriculum

**Legend.** Per phase: (a) Goal · (b) Prerequisites · (c) Primary (canonical texts + seminal papers) · (d) Supplementary · (e) Exercises + **Build/Lab** (offensive + defensive) · (f) Time · (g) MVP. Status tags: **[SETTLED]**, **[OPEN]**, **[CONTESTED]**, **[EVOLVING]**, **[HYPE-WATCH]**. Physics bridges: ⚛.

---

### PHASE 1 — Security Foundations & the Adversarial Mindset
**(a) Goal.** The conceptual bedrock: the CIA triad and its limits, threat modeling and attack trees, the classic design principles, trust and the TCB, security economics, and the offense/defense asymmetry. A working adversarial mindset.

**(b) Prerequisites.** None internal. Feeds everything.

**(c) Primary.**
- **Ross Anderson, *Security Engineering: A Guide to Building Dependable Distributed Systems*, 3rd ed. (Wiley, 2020) — [FREE online]** (cl.cam.ac.uk/~rja14/book.html). The single best security-engineering book; read broadly here and return to specific chapters throughout. This is the spine of the whole curriculum.
- Seminal: **Saltzer & Schroeder, "The Protection of Information in Computer Systems" (1975)** — the eight design principles (least privilege, fail-safe defaults, complete mediation, open design/Kerckhoffs, separation of privilege, least common mechanism, psychological acceptability, economy of mechanism); read the original.

**(d) Supplementary.** Bishop, *Computer Security: Art and Science*, 2nd ed. (Addison-Wesley, 2018) **[BUY]** for the academic/formal treatment (policy models: Bell–LaPadula, Biba, Clark–Wilson).

**(e) Exercises + Lab.** Build a **threat model** (STRIDE + attack tree) for a real system you know — ideally a fraud/ML pipeline from your work — and identify its trust boundaries and weakest links. Write the corresponding defensive requirements.

**(f) Time.** 4–6 weeks.

**(g) MVP.** Anderson chs. 1–3 + Saltzer–Schroeder 1975 + one threat model.

⚛ *Bridge:* security economics and the **defender's dilemma** (the attacker needs one hole; the defender must cover all) is an asymmetry you'll recognize from fraud — the adversary adapts to your controls, so static defenses decay. **[SETTLED as framing.]**

---

### PHASE 2 — Cryptography I: Symmetric Primitives & Provable-Security Foundations
**(a) Goal.** The foundations (one-way functions, PRGs/PRFs/PRPs, the notion of provable/reduction-based security, the random-oracle model) and the symmetric toolkit (AES and modes, ChaCha20, SHA-2/SHA-3, MACs, AEAD). Reason about what a security definition *means*.

**(b) Prerequisites.** Phase 1; the computational-complexity intuition from your theory curriculum (this strand also overlaps your crypto track — this is the self-contained on-ramp).

**(c) Primary.**
- **Boneh & Shoup, *A Graduate Course in Applied Cryptography* — [FREE]** (cryptobook.us). The modern applied-crypto spine; Parts I–II here.
- Katz & Lindell, *Introduction to Modern Cryptography*, 3rd ed. (CRC Press, 2020) **[BUY]** — the rigorous provable-security textbook (definitions, reductions, the symmetric constructions).
- Seminal: **Goldwasser & Micali, "Probabilistic Encryption" (1984)** — semantic security; **Bellare & Rogaway, "Random Oracles are Practical" (1993)**.

**(d) Supplementary.** Aumasson, *Serious Cryptography*, 2nd ed. (~2024 — **verify**) **[BUY]** — the best practitioner's book; **CryptoHack** **[FREE]** (cryptohack.org) for interactive problems.

**(e) Exercises + Lab.** **CryptoPals Sets 1–2 [FREE]** (attack side); implement (defensive side, Python) **AES** with a mode, **SHA-256**, and **HMAC** from primitives, plus a **constant-time comparison** — and demonstrate why the naive one leaks.

**(f) Time.** 8–10 weeks.

**(g) MVP.** Katz–Lindell symmetric chapters + Boneh–Shoup Part I + CryptoPals Set 1.

⚛ *Bridge:* **cryptographic hardness is computational complexity** — a one-way function is easy to compute, hard to invert; provable security is a reduction (break the scheme ⇒ solve the hard problem). This connects directly to the **Liu–Pass characterization** (OWFs exist iff time-bounded Kolmogorov complexity is mildly hard-on-average) from your theory curriculum. **[SETTLED framework; foundational assumption OPEN — see Phase 4.]**

---

### PHASE 3 — Cryptography II: Public-Key & Applied Cryptographic Engineering
**(a) Goal.** Public-key crypto (RSA, Diffie–Hellman/discrete log, elliptic curves — ECDH, Ed25519) and — critically — how to *use* crypto correctly: TLS 1.3, PKI and certificates, key management, and the canonical implementation pitfalls that break real systems.

**(b) Prerequisites.** Phase 2.

**(c) Primary.**
- Boneh–Shoup Parts III–IV **[FREE]**; Katz–Lindell public-key chapters.
- Ferguson, Schneier & Kohno, *Cryptography Engineering* (Wiley, 2010) **[BUY]** — the engineering-pitfalls perspective.
- Seminal: **Diffie & Hellman, "New Directions in Cryptography" (1976)**; **Rivest, Shamir & Adleman (1978)**; the **TLS 1.3 RFC 8446**.

**(d) Supplementary.** Nakov, *Practical Cryptography for Developers* **[FREE]** (cryptobook.nakov.com); Bernstein's Curve25519/Ed25519 papers.

**(e) Exercises + Lab.** **CryptoPals Sets 3–4 [FREE]** — the **padding-oracle attack** and **CBC bit-flipping** (attack side); implement **ECDH + Ed25519** from a curve (defensive/engineering side); analyze a real **TLS configuration** (cipher suites, cert chain) and identify misconfigurations.

**(f) Time.** 9–11 weeks.

**(g) MVP.** Boneh–Shoup public-key chapters + the padding-oracle attack + a TLS-config analysis + Diffie–Hellman 1976 & RSA 1978.

⚛ *Bridge:* RSA/ECC security rests on **number-theoretic hardness** (factoring, discrete log); the padding-oracle attack is an **information-leak channel** — each oracle query yields one bit, and you decode the plaintext bit by bit (an adaptive information-extraction process).

---

### PHASE 4 — Cryptography III: Advanced Protocols & Post-Quantum (with your crypto track)
**(a) Goal.** A working understanding of the advanced protocols (zero-knowledge, MPC, FHE, pairings) and the current post-quantum landscape (lattice/code/hash/isogeny, and the NIST standards). Deep derivations are deferred to your existing crypto track; this phase gives the security-engineer's view.

**(b) Prerequisites.** Phase 3. **This is the primary hand-off to your existing graduate crypto track** — treat that as the depth source for ZK/MPC/FHE/pairings/PQC.

**(c) Primary.**
- For the applied/overview level: Boneh–Shoup's advanced chapters **[FREE]**; the NIST PQC standards documents (**FIPS 203 ML-KEM, FIPS 204 ML-DSA, FIPS 205 SLH-DSA** — **verify current status**).
- Seminal: **Goldwasser, Micali & Rackoff, "The Knowledge Complexity of Interactive Proof-Systems" (1985)** — ZK; **Yao** (garbled circuits / MPC); **Gentry (2009)** FHE; and the **SIKE break** (Castryck & Decru, "An efficient key recovery attack on SIDH", 2022).

**(d) Supplementary.** Your crypto track's ZK/MPC/FHE/pairing/PQC materials (the depth source); the CryptoPals Sets 5–8 for advanced attacks.

**(e) Exercises + Lab.** Implement a **toy ZK proof** (e.g., a Schnorr identification / Sigma protocol) and a **toy lattice KEM** (Kyber-like) in Python; study the SIKE break as a case study in "believed-hard ≠ proven-hard."

**(f) Time.** 8–10 weeks (lighter here; depth lives in the crypto track).

**(g) MVP.** The NIST PQC overview + a Schnorr ZK implementation + the SIKE case study; defer the rest to the crypto track.

**[OPEN] The existence of one-way functions** — cryptography's foundational assumption — remains unproven (its existence would imply P≠NP). **[EVOLVING/CONTESTED] Post-quantum migration:** NIST standardized lattice- and hash-based schemes (2024), but **which schemes endure is not settled** — the **2022 break of SIKE** (an isogeny scheme that had reached NIST's 4th round) is the field's sharpest recent reminder that a hardness assumption believed solid for years can collapse. Treat PQC confidence proportionally.

⚛ *Bridge:* **Shor's algorithm** (from your quantum/theory knowledge) is *why* RSA/ECC fall to quantum computers; lattice hardness (LWE/SVP) is the leading replacement, and lattices are the same objects you met via crystallography in physics.

---

### PHASE 5 — Software Security I: Memory-Safety Vulnerabilities & Exploitation
**(a) Goal.** The memory-corruption vulnerability classes (stack/heap overflows, use-after-free, type confusion, integer issues) and modern exploitation (return-to-libc, ROP/JOP, heap grooming). Write working exploits.

**(b) Prerequisites.** Phase 1; **C and the machine-level view from your systems curriculum (CS:APP)** — this is where the Attack/Malloc labs pay off.

**(c) Primary.**
- Erickson, *Hacking: The Art of Exploitation*, 2nd ed. (No Starch, 2008) **[BUY]** — the classic hands-on intro.
- Seminal: **Aleph One, "Smashing the Stack for Fun and Profit" (Phrack 49, 1996)** — read the founding text; **Shacham, "The Geometry of Innocent Flesh on the Bone: Return-into-libc without Function Calls (on the x86)" (CCS 2007)** — ROP.

**(d) Supplementary.** **pwn.college [FREE]** (the best structured binary-exploitation curriculum), **picoCTF** and **OverTheWire** wargames **[FREE]**, **LiveOverflow's binary-exploitation series [FREE]**, and the "Nightmare" course **[FREE]**.

**(e) Exercises + Lab.** Work **pwn.college / picoCTF pwn** tracks; write, from scratch, a **stack-overflow → shellcode → then ROP** exploit chain against a deliberately vulnerable C binary (offense). Defensively, annotate exactly which mitigation (Phase 6) would have stopped each step.

**(f) Time.** 10–13 weeks.

**(g) MVP.** Erickson (exploitation chapters) + Aleph One 1996 + Shacham 2007 + the pwn.college fundamentals.

⚛ *Bridge (light):* exploitation is precise reasoning about **memory layout and machine state** — the discipline is closer to physics problem-solving (exact accounting of a system's configuration) than most software work.

**GrapheneOS synergy flag:** this and Phase 6 are the direct on-ramp to `hardened_malloc` and exploit-mitigation work — understanding heap exploitation is understanding what hardened allocators defend against.

---

### PHASE 6 — Software Security II: Mitigations, Fuzzing & Secure Coding
**(a) Goal.** The defensive counterpart: exploit mitigations (NX/DEP, stack canaries, ASLR, CFI, shadow stacks, and memory-safe languages) and *how they're bypassed*; automated bug-finding via fuzzing; and secure coding.

**(b) Prerequisites.** Phase 5.

**(c) Primary.**
- **Szekeres, Payer, Wei & Song, "SoK: Eternal War in Memory" (IEEE S&P 2013)** — the definitive systematization of memory-safety attacks and defenses; read it closely.
- **Abadi, Budiu, Erlingsson & Ligatti, "Control-Flow Integrity" (CCS 2005)**.
- Dowd, McDonald & Schuh, *The Art of Software Security Assessment* (Addison-Wesley, 2006) **[BUY]** — the code-auditing bible.

**(d) Supplementary.** The AFL/AFL++ and libFuzzer documentation **[FREE]**; the "Fuzzing Book" **[FREE]** (fuzzingbook.org); Rust's memory-safety guarantees (from your systems/Rust work) as the language-level defense.

**(e) Exercises + Lab.** Build/run a **coverage-guided fuzzer (AFL++)** against a real C target and triage a crash (offense/discovery). Defensively, **implement a mitigation** (e.g., a stack canary or a shadow stack in a toy runtime) and then demonstrate a bypass — the attack/defense loop in one exercise.

**(f) Time.** 8–10 weeks.

**(g) MVP.** SoK Eternal War 2013 + CFI 2005 + one AFL++ fuzzing campaign.

**[OPEN]** Whether the memory-safety war is "winnable" via mitigations alone, or requires wholesale migration to memory-safe languages (Rust), is an active industry debate — the trend (CISA, major vendors) leans toward the latter. **[SETTLED]** that no deployed mitigation is a complete defense; each has documented bypasses.

---

### PHASE 7 — Systems Security: OS/Kernel Security, Sandboxing & Trusted Execution
**(a) Goal.** Security at the OS layer: privilege separation, access control (DAC/MAC, capabilities, SELinux), sandboxing and isolation (seccomp, namespaces, containers), kernel attack surface, and trusted execution (Intel SGX, ARM TrustZone, TPMs) with their limits.

**(b) Prerequisites.** Phases 1, 5–6; **the OS foundations from your systems curriculum**.

**(c) Primary.**
- **MIT 6.858 "Computer Systems Security" (OCW) — [FREE]** — the canonical academic course; lectures + labs.
- Anderson, *Security Engineering* (access-control and OS chapters) **[FREE]**.
- Seminal: the **seL4** verified-microkernel work (Klein et al., "seL4: Formal Verification of an OS Kernel", SOSP 2009) — the high-assurance end; the SGX papers (and the SGX-attack literature).

**(d) Supplementary.** Stanford CS155 **[FREE]**; the SELinux and seccomp documentation.

**(e) Exercises + Lab.** Write a **seccomp-bpf sandbox policy** and a minimal privilege-separated service (defense); explore an **SGX enclave** and read one enclave-attack paper. Connect explicitly to **GrapheneOS's sandboxing/SELinux model** (your other track).

**(f) Time.** 8–10 weeks.

**(g) MVP.** MIT 6.858 core lectures + Anderson's access-control chapters + a seccomp sandbox.

**GrapheneOS synergy flag:** this phase is the general theory behind your GrapheneOS framework track (sandboxing, SELinux policy, isolation) — the two reinforce each other directly.

---

### PHASE 8 — Network Security
**(a) Goal.** Security of the network stack in practice: TLS/PKI operationally, authentication and authorization (OAuth 2.0, OIDC, mutual TLS), DNS security (DNSSEC, DoH/DoT), intrusion detection, DDoS, and the zero-trust model.

**(b) Prerequisites.** Phase 3 (TLS/crypto); **the networking foundations from your systems curriculum**.

**(c) Primary.**
- Anderson, *Security Engineering* (network and distributed-systems security chapters) **[FREE]**.
- Seminal: the **TLS 1.3 RFC 8446**; **Kaminsky's DNS cache-poisoning** work (2008); the OAuth 2.0 / OIDC specs.

**(d) Supplementary.** Bishop (network-security chapters); practical TLS references (e.g., "Bulletproof TLS").

**(e) Exercises + Lab.** A **MITM lab** (intercept and analyze TLS with a local proxy, then observe what certificate pinning prevents — attack + defense); a **DNS-spoofing lab**; instrument and reason about an IDS ruleset.

**(f) Time.** 7–9 weeks.

**(g) MVP.** Anderson's network chapters + TLS 1.3 RFC + the MITM lab.

⚛ *Bridge (light):* protocol security is about **adversarial state machines** — many attacks are confused-deputy or state-confusion bugs, reasoning that rhymes with the distributed-systems consistency work in your systems curriculum.

---

### PHASE 9 — Web & Application Security
**(a) Goal.** The web platform's security model (same-origin policy, cookies, CSP) and the vulnerability classes (XSS, CSRF, SQLi, SSRF, insecure deserialization, auth flaws) via the OWASP framework — attack and defense.

**(b) Prerequisites.** Phase 8.

**(c) Primary.**
- **PortSwigger Web Security Academy — [FREE]** (portswigger.net/web-security). The modern, hands-on spine for web security; work its labs.
- Stuttard & Pinto, *The Web Application Hacker's Handbook*, 2nd ed. (Wiley, 2011) **[BUY]** — foundational (aging but still the reference).
- Seminal: the **OWASP Top 10** (2021 edition — **verify for a newer revision**) and the OWASP Testing Guide/ASVS **[FREE]**; Zalewski, *The Tangled Web* (No Starch, 2011) **[BUY]** for the browser security model.

**(d) Supplementary.** The OWASP Cheat Sheet Series **[FREE]**.

**(e) Exercises + Lab.** Work the **PortSwigger Academy** XSS/SQLi/SSRF/CSRF labs (offense); then **build a small vulnerable web app and fix each class** (defense) — implement CSP, parameterized queries, anti-CSRF tokens, and output encoding, and re-test.

**(f) Time.** 8–10 weeks.

**(g) MVP.** PortSwigger Academy core paths + the OWASP Top 10 + the build-and-harden exercise.

**[HYPE-WATCH]** "Passing a vulnerability scanner / being compliant = secure" is a common and dangerous conflation — automated scanners miss logic flaws and compliance is a floor, not a guarantee.

---

### PHASE 10 — Side-Channel & Hardware Security I: Timing & Power Analysis
**(a) Goal.** Extracting secrets from physical leakage: timing attacks, and power analysis — simple (SPA), differential (DPA), and correlation (CPA). Mount a real power-analysis attack. **This is your strongest physics-leverage phase.**

**(b) Prerequisites.** Phases 2–3 (the crypto being attacked); **your statistics and signal-processing background**.

**(c) Primary.**
- Mangard, Oswald & Popp, *Power Analysis Attacks: Revealing the Secrets of Smart Cards* (Springer, 2007) **[BUY]** — the DPA/CPA textbook.
- Seminal: **Kocher, "Timing Attacks on Implementations of Diffie-Hellman, RSA, DSS, and Other Systems" (CRYPTO 1996)**; **Kocher, Jaffe & Jun, "Differential Power Analysis" (CRYPTO 1999)** — the founding DPA paper, read it.

**(d) Supplementary.** **ChipWhisperer (NewAE) tutorials and hardware — [FREE tutorials]** — the standard hands-on side-channel platform; the CHES proceedings for the frontier.

**(e) Exercises + Lab.** **Mount a DPA/CPA attack on AES using ChipWhisperer** (recover the key from power traces — offense); implement a **timing attack** on a naive string/MAC comparison in C, then implement the **constant-time** fix (defense). This is signal processing applied to secrets.

**(f) Time.** 9–12 weeks.

**(g) MVP.** Kocher DPA 1999 + Mangard–Oswald–Popp core chapters + one ChipWhisperer CPA-on-AES attack.

⚛ *Bridge (headline):* **DPA/CPA is signal extraction from noise** — you correlate a leakage model (Hamming weight of an intermediate) against measured power over many traces; the machinery is **SNR, correlation, matched filtering, and hypothesis testing**, exactly your statistics/DSP toolkit. Averaging traces to pull signal from noise is the same √N improvement you know from measurement physics. **[SETTLED and well-understood.]**

---

### PHASE 11 — Side-Channel & Hardware Security II: EM/Acoustic (TEMPEST), Microarchitectural Attacks, Rowhammer, Fault Injection
**(a) Goal.** The rest of the physical/architectural attack surface: electromagnetic (TEMPEST/Van Eck) and **acoustic** side channels, microarchitectural attacks (cache attacks, Spectre/Meltdown), Rowhammer, and fault injection/glitching. Directly hits your TEMPEST/acoustic-inference interest.

**(b) Prerequisites.** Phase 10; **the CPU-microarchitecture/speculation material from your systems curriculum**; **your EM and solid-state physics**.

**(c) Primary.**
- Seminal (read as a set): **van Eck, "Electromagnetic Radiation from Video Display Units: An Eavesdropping Risk?" (1985)** — founding TEMPEST; **Asonov & Agrawal, "Keyboard Acoustic Emanations" (IEEE S&P 2004)** and **Genkin, Shamir & Tromer, "RSA Key Extraction via Low-Bandwidth Acoustic Cryptanalysis" (CRYPTO 2014)** — acoustic side channels; **Yarom & Falkner, "FLUSH+RELOAD: A High Resolution, Low Noise, L3 Cache Side-Channel Attack" (USENIX Security 2014)**; **Kim et al., "Flipping Bits in Memory Without Accessing Them: An Experimental Study of DRAM Disturbance Errors" (Rowhammer, ISCA 2014)**; **Kocher et al., "Spectre Attacks" (2019)** and **Lipp et al., "Meltdown" (2018)**.

**(d) Supplementary.** The Prime+Probe and cache-attack survey literature; fault-injection surveys (voltage/clock glitching, laser fault injection).

**(e) Exercises + Lab.** Implement a **Flush+Reload cache side-channel** in C and use it to leak across a boundary; reproduce a **Spectre proof-of-concept** (building on your systems curriculum's speculation knowledge). For your specific interest: run a small **acoustic-emanation experiment** (record keystrokes and attempt classification with classical signal processing — an ideal fusion of your DSP and adversarial-ML interests). Defensively, reason about mitigations (constant-time, cache partitioning, speculation barriers) and their costs.

**(f) Time.** 10–13 weeks.

**(g) MVP.** van Eck 1985 + Yarom–Falkner 2014 + Spectre/Meltdown 2018–19 + a Flush+Reload lab.

⚛ *Bridge (rich):* **TEMPEST is electromagnetics** (compromising emanations as radiated EM you can pick up and demodulate); **acoustic side channels are acoustics + DSP** (the acoustic-keystroke work is a classification problem over spectral features); **Rowhammer is solid-state device physics** (repeated row activation induces charge leakage/disturbance in adjacent DRAM cells); **fault injection is device physics** (glitching pushes the device outside its safe operating envelope; laser fault injection is the photoelectric effect wielded as a weapon). Your physics is not incidental here — it's the core of the phase. **[SETTLED physics; specific attacks EVOLVING.]**

**[OPEN]** Whether speculative-execution side channels (Spectre-class) are **fully mitigable without significant performance cost** remains open — mitigations are partial and costly, and new variants keep appearing.

---

### PHASE 12 — Reverse Engineering & Malware Analysis
**(a) Goal.** Understanding binaries and malicious code without source: static and dynamic RE, disassembly/decompilation, debugging, malware behaviors and families, unpacking and anti-analysis evasion, and detection engineering (YARA).

**(b) Prerequisites.** Phases 5–6 (exploitation/binaries); **assembly and the machine-level view from your systems curriculum**.

**(c) Primary.**
- Sikorski & Honig, *Practical Malware Analysis* (No Starch, 2012) **[BUY]** — the malware-RE bible.
- Andriesse, *Practical Binary Analysis* (No Starch, 2018) **[BUY]** — modern binary analysis (instrumentation, taint, symbolic execution).
- Seminal/tooling: **Ghidra (NSA) — [FREE]**; Eagle, *The IDA Pro Book*, 2nd ed. (2011) **[BUY]**.

**(d) Supplementary.** **Yurichev, *Reverse Engineering for Beginners* (RE4B) — [FREE]** (beginners.re); **Flare-On** and **crackmes.one** challenges **[FREE]**; Malware-Traffic-Analysis.net **[FREE]**.

**(e) Exercises + Lab.** Work **Flare-On / crackmes** (offense/analysis); **reverse a real (sandboxed) malware sample** in Ghidra — identify its capabilities, unpack it, and **write YARA rules** to detect the family (defense). Do all malware work in an isolated VM/sandbox.

**(f) Time.** 10–13 weeks.

**(g) MVP.** *Practical Malware Analysis* core chapters + RE4B + a Ghidra RE of one crackme + one YARA ruleset.

⚛ *Bridge (light):* RE is **empirical reverse-inference** — you observe behavior and reconstruct the underlying mechanism, the same inferential loop as experimental physics (hypothesize the model, test against observations).

---

### PHASE 13 — Digital Forensics & Incident Response
**(a) Goal.** Investigating compromises and reconstructing events: disk, **memory**, and network forensics; the incident-response lifecycle; threat hunting and log analysis; and the MITRE ATT&CK framework as the shared language of adversary behavior.

**(b) Prerequisites.** Phases 7 (OS internals), 12 (RE/malware).

**(c) Primary.**
- Ligh, Case, Levy & Walters, *The Art of Memory Forensics* (Wiley, 2014) **[BUY]** — the memory-forensics standard (Volatility).
- Luttgens, Pepe & Mandia, *Incident Response & Computer Forensics*, 3rd ed. (McGraw-Hill, 2014) **[BUY]** — the DFIR process reference.
- Framework: **MITRE ATT&CK — [FREE]** (attack.mitre.org).

**(d) Supplementary.** **Volatility** and **Autopsy** documentation **[FREE]**; the SANS DFIR posters/cheat-sheets **[FREE]**; Carrier, *File System Forensic Analysis*.

**(e) Exercises + Lab.** Perform **memory forensics with Volatility** on a compromised-image sample (find the malicious process, injected code, and network artifacts); run a **DFIR exercise** end-to-end (detect → contain → eradicate → recover → report) and **map the adversary's actions to ATT&CK**; do a log-analysis threat-hunt.

**(f) Time.** 8–10 weeks.

**(g) MVP.** *The Art of Memory Forensics* core + MITRE ATT&CK + one Volatility investigation.

**[HYPE-WATCH] Attribution is inherently uncertain.** Confident public attribution of an intrusion to a specific actor is often overstated — indicators are forgeable, false flags exist, and attribution mixes technical evidence with lower-confidence intelligence. Treat "we know who did it" claims with calibrated skepticism.

---

### PHASE 14 — Adversarial ML / ML Security
**(a) Goal.** Attacks and defenses on learning systems: evasion (adversarial examples), poisoning and backdoors, model extraction, model inversion and membership inference, the (limited) state of robustness, and LLM-specific issues (prompt injection, jailbreaks). Connect to fraud-model evasion.

**(b) Prerequisites.** Phase 1; **your ML background and ML track** (this strand overlaps it — framed security-first here).

**(c) Primary.**
- Seminal (read as a set): **Szegedy et al., "Intriguing Properties of Neural Networks" (2014)**; **Goodfellow, Shlens & Szegedy, "Explaining and Harnessing Adversarial Examples" (2015)** — FGSM; **Carlini & Wagner, "Towards Evaluating the Robustness of Neural Networks" (IEEE S&P 2017)**; **Madry et al., "Towards Deep Learning Models Resistant to Adversarial Attacks" (2018)** — PGD/adversarial training; **Athalye, Carlini & Wagner, "Obfuscated Gradients Give a False Sense of Security" (ICML 2018)** — why most defenses fail.
- Survey: **Biggio & Roli, "Wild Patterns: Ten Years After the Rise of Adversarial Machine Learning" (2018)**.

**(d) Supplementary.** **Shokri et al., "Membership Inference Attacks Against Machine Learning Models" (2017)**; **Gu et al., "BadNets" (2017)** (backdoors); the recent LLM-security literature (prompt injection/jailbreak — **rapidly evolving, verify current**); NIST's AI risk/adversarial-ML taxonomy.

**(e) Exercises + Lab.** Implement **FGSM and PGD** attacks against an image classifier (offense); run a **data-poisoning** attack; **evaluate a proposed defense and then break it with an adaptive attack** (the Athalye et al. lesson, hands-on); implement **membership inference**. Then connect to your domain: reason about how an adversary **evades a fraud model** and what defenses actually help.

**(f) Time.** 9–12 weeks.

**(g) MVP.** Goodfellow 2015 + Madry 2018 + Athalye 2018 + an FGSM/PGD-and-adaptive-attack lab.

**[OPEN / HYPE-WATCH] There is no known robust defense against adaptive adversarial attacks.** Adversarial training (PGD) raises the bar but does not solve it; most published defenses have been broken, often by their own authors' follow-ups (the Athalye–Carlini–Wagner result is the canonical warning), and **certified** robustness covers only narrow threat models. Treat any "robust/secure AI" or "we solved adversarial examples" claim with strong skepticism — this is the single most over-hyped area in the cluster. The fraud connection is direct: adversaries adapt to deployed models, so robustness is an ongoing arms race, not a solved property.

⚛ *Bridge:* adversarial examples are an **optimization/geometry** phenomenon — high-dimensional decision boundaries are close to most inputs, and gradient-based attacks find the nearest crossing; membership inference and model inversion are **statistical-inference** attacks (distinguishing distributions), and **differential privacy** (calibrated noise) is the principled defense, tying to the information-theoretic material from your theory curriculum.

---

### PHASE 15 (Capstone) — Integrative Project + the Frontier
**(a) Goal.** Combine strands into one substantial artifact and transition to reading (and optionally producing) frontier security research.

**(b) Prerequisites.** Most of Phases 1–14.

**(c) Capstone options (pick one).**
- **A full vulnerability-research project:** find, exploit, and then propose/implement a fix for a bug in a real (in-scope) open-source target — end-to-end offense→defense.
- **A side-channel research reproduction:** reproduce a CHES/S&P side-channel or microarchitectural attack and analyze a mitigation (leans on your physics).
- **An adversarial-fraud study:** a rigorous evaluation of evasion attacks against a fraud/anomaly model and the defenses that measurably help — closest to your work.
- **A GrapheneOS security contribution:** land a hardening or exploit-mitigation change (converts this curriculum into your GrapheneOS track's milestone).

**(d) Frontier tracking.** Venues: **IEEE S&P ("Oakland"), USENIX Security, ACM CCS, NDSS** (systems security); **CRYPTO, EUROCRYPT, TCC** (crypto); **CHES** (hardware/side-channel); **RAID, DIMVA** (intrusion/malware); adversarial ML at **IEEE S&P, USENIX Security, NeurIPS, ICML**. Use the **"SoK" (Systematization of Knowledge) papers** as the best entry points into any subfield; follow the ePrint archive (eprint.iacr.org) for crypto preprints.

**(e) Build.** The capstone itself, iterated and written up.

**(f) Time.** Ongoing (3–6 months for a solid capstone).

**(g) MVP.** A reduced capstone + a standing habit of reading one SoK/top-venue paper per week.

---

## Dependency Map

```
                         PHASE 1 — Security Foundations & Adversarial Mindset
                                              │
        ┌───────────────────────┬─────────────┼──────────────────────┬─────────────────────┐
        ▼                       ▼             ▼                      ▼                     ▼
  CRYPTO STRAND          SOFTWARE/SYSTEMS   NETWORK/WEB          HARDWARE/SIDE-CHANNEL   ADVERSARIAL ML
  P2 Symmetric ─►        P5 Exploitation ─► P8 Network ─►        (needs crypto: P2–3)    P14 (needs your
  P3 Public-key/ ─►      P6 Mitigations ─►  P9 Web/App           P10 Timing/Power ─►      ML background;
     applied crypto      P7 Systems/OS/                          P11 EM/Acoustic/         otherwise
  P4 Advanced/PQC          Sandbox/TEE                             µarch/Rowhammer/        ~standalone)
     (→ your crypto                                                Fault
      track for depth)         │                                       ▲
                               ▼                                       │ (builds on systems-
                          P12 RE & Malware ──► P13 Forensics & IR      │  curriculum µarch)
                                                                       
        └───────────────── all strands feed ─────────────────► P15 Capstone + Frontier
```

- **Foundation first:** P1 before everything.
- **Sequential within strands:** crypto P2→P3→P4; software/systems P5→P6→P7; web P8→P9; hardware P10→P11; RE/forensics P12→P13.
- **Parallel across strands:** after P1, the crypto, software/systems, web, and adversarial-ML strands can proceed **in parallel**. The **hardware/side-channel strand (P10–P11) requires the crypto strand (P2–P3)** as prerequisite (it attacks crypto implementations).
- **Cross-curriculum:** P5/P12 lean on your systems curriculum's machine-level/assembly material; P7 on its OS material; P8 on its networking; P11 on its microarchitecture/speculation; P4 hands off to your crypto track; P14 overlaps your ML track.

---

## Overall MVP Fast-Path (~20–24 months part-time)
1. **Foundations + crypto core:** Anderson chs. 1–3 + Saltzer–Schroeder (Phase 1) → Katz–Lindell/Boneh–Shoup symmetric + public-key + **CryptoPals Sets 1–4** (Phases 2–3).
2. **Software/systems security:** Erickson + Aleph One + Shacham + **pwn.college fundamentals** (Phase 5) → SoK Eternal War + one AFL++ campaign (Phase 6) → MIT 6.858 core + a seccomp sandbox (Phase 7).
3. **Web:** the **PortSwigger Academy** core paths + build-and-harden a vulnerable app (Phase 9).
4. **The physics-leverage phase:** Kocher DPA + **one ChipWhisperer CPA-on-AES attack** + a Flush+Reload lab (Phases 10–11) — highest transfer from your background.
5. **One of {RE (Phase 12) or Adversarial ML (Phase 14)}** at depth — given your work, **Adversarial ML** (the fraud-evasion connection) is the highest-leverage choice.
6. **Capstone:** the adversarial-fraud study or a GrapheneOS contribution, reduced.

---

## Recommendations

**Staged plan (~10–15 hrs/week), braiding strands.**
1. **Months 0–10:** P1 → P2–P3 (crypto core) **‖** P5 (exploitation). *Benchmark:* CryptoPals Sets 1–4 complete; a working ROP exploit.
2. **Months 10–22:** P4 (advanced crypto/PQC, light) **‖** P6–P7 (mitigations, systems security) **‖** P9 (web). *Benchmark:* an AFL++ crash triaged; the PortSwigger core done; a seccomp-sandboxed service.
3. **Months 22–36:** P10–P11 (side-channel/hardware — the physics phases) **‖** P8 (network). *Benchmark:* a ChipWhisperer CPA key recovery; a Flush+Reload PoC; the acoustic-emanation experiment.
4. **Months 36–48:** P12–P13 (RE, forensics) **‖** P14 (adversarial ML). *Benchmark:* a malware sample reversed with YARA rules; a Volatility investigation; an adaptive attack that breaks a defense.
5. **Months 48+:** the capstone + a weekly SoK/top-venue reading habit.

**Where your choices shape the plan.** *Self-contained* means the crypto strand is present, but Phase 4 stays light and hands depth to your crypto track — don't re-derive ZK/MPC/FHE here. *Balanced offense+defense* means every phase carries both, so budget the lab time accordingly. *All four boundary areas in* is broad; if time compresses, the two highest-transfer phases for you are **P10–P11 (side-channel/hardware — your physics)** and **P14 (adversarial ML — your fraud work)**; forensics (P13) is the most self-contained to time-slice or defer.

**Best free lecture courses / platforms (all [FREE]).** MIT 6.858 and Stanford CS155 (systems security); the CryptoPals and CryptoHack platforms (crypto); pwn.college, picoCTF, OverTheWire, and the Nightmare course (binary exploitation); the PortSwigger Web Security Academy (web); ChipWhisperer tutorials (side-channel); RE4B and Flare-On (RE); Volatility labs (forensics); LiveOverflow's videos (broad).

**Frontier-tracking shortlist.** IEEE S&P, USENIX Security, ACM CCS, NDSS; CRYPTO/EUROCRYPT/TCC and the IACR ePrint archive; CHES (hardware/side-channel); RAID/DIMVA; and adversarial ML at S&P/USENIX Security/NeurIPS/ICML. Read the **SoK papers** as subfield entry points.

---

## Caveats
- **Editions, tool versions, and standards NOT live-verified this pass — and security moves fast.** Built from my knowledge as of early 2026; I couldn't run a live check. Verify especially: the **NIST post-quantum standards** status (FIPS 203/204/205 — ML-KEM/ML-DSA/SLH-DSA — and any 4th-round/additional-signature outcomes), the current **OWASP Top 10** edition (2021 vs a newer revision), the LLM-security literature (moving monthly), and tool/book editions (Aumasson *Serious Cryptography* edition; the currency of *The Web Application Hacker's Handbook* given its age; Ghidra/Volatility/AFL++ versions). **This is the cluster most worth re-running with live research** — re-enable the Research toggle and I'll verify standards, editions, and tools and refresh links.
- **Free-vs-paid.** The **[FREE]** items are legitimately free from authors/publishers/institutions (Anderson's *Security Engineering* 3rd ed., Boneh–Shoup, CryptoPals/CryptoHack, MIT 6.858, PortSwigger Academy, pwn.college, OverTheWire, RE4B, Ghidra, ChipWhisperer tutorials, Volatility, MITRE ATT&CK, OWASP guides, and most seminal papers via IACR ePrint / authors' pages). In-copyright **[BUY]** books (Katz–Lindell, Aumasson, Ferguson–Schneier–Kohno, Erickson, Dowd et al., Stuttard–Pinto, Zalewski, Sikorski–Honig, Andriesse, Eagle, Ligh et al., Mangard–Oswald–Popp, Bishop) should be purchased — pirated PDFs aren't endorsed.
- **Legal/ethical boundary.** Everything here assumes **authorized** targets only — your own labs, deliberately-vulnerable training targets (pwn.college, PortSwigger, picoCTF, crackmes), sanctioned CTFs, and in-scope bug-bounty/open-source work. Analyze malware only in isolated VMs/sandboxes. Reverse engineering, exploitation, and side-channel work against systems you don't own or lack permission to test can be illegal regardless of intent — stay inside authorized scope.
- **Overlap boundaries.** The crypto strand is self-contained through Phase 3 but hands ZK/MPC/FHE/pairing/PQC *depth* to your existing crypto track (Phase 4); the systems-security phases are the general foundations feeding your GrapheneOS work; the microarchitectural-attack material builds on your systems curriculum's speculation chapter; adversarial ML overlaps your ML track (framed security-first here).
- **Calibration.** The genuinely open/contested/over-hyped spots are tagged: one-way-function existence `[OPEN]`, post-quantum durability `[EVOLVING]` (SIKE break), adversarial-ML robustness `[OPEN/HYPE-WATCH]` (no robust defense vs. adaptive attacks — the most over-hyped area here), speculative-execution mitigation `[OPEN]`, and the marketing to discount (confident attribution, "AI-powered security", "unhackable" blockchains, compliance-as-security). Treat sources presenting these as settled with suspicion.
- **Scope realism.** This is a genuine multi-year, lab-heavy, multi-strand program — the broadest in the series; estimates assume a mathematically mature learner at ~10–15 hrs/week. The strands are parallelizable, so pick the one that fits your current appetite (your physics makes the side-channel strand unusually efficient; your fraud work makes adversarial ML unusually relevant) and let the others wait.