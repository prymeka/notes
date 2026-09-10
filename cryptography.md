# Cryptography for Computers & Communications
### A Graduate-Level Self-Study Curriculum with Strong Theoretical Foundations

**Target:** the full graduate theory arc (provable security → deep math → frontier theory) balanced with real-world communications protocols, plus three hands-on strands: build primitives in Python, break them (CryptoPals/CryptoHack), and a constant-time / side-channel discipline running throughout.

**Honest scope:** ~30–42 months at 8–12 h/week. This is a real graduate program, not a bootcamp. An MVP fast-track (§ *Fast-Track*) compresses the load-bearing 30% into ~7–9 months if you want a usable working knowledge first and depth later.

---

## How to read this document

**Calibration tags** (your standard SETTLED / CONTESTED / HYPE discipline):
- `[SETTLED]` — mature, unlikely to change; learn once from the canonical source.
- `[MOVING]` — version-sensitive; re-verify against the primary source each time you touch it (standards, deployments, library APIs).
- `[CONTESTED]` — genuine expert disagreement or marketing outrunning reality; reason from primaries, don't trust summaries.

**Access tags:** `[FREE]` (legally free from the author/publisher/standards body) · `[PAID]`.

**Strand tags** mark hands-on work:
- `[BUILD]` — implement from scratch in Python (learning only — see *Safety* below).
- `[BREAK]` — attack lab: CryptoPals sets and CryptoHack categories.
- `[SIDE]` — constant-time / side-channel focus.
- `[THEORY]` — proofs and reading (the spine; unmarked work is theory by default).

**Safety (non-negotiable):** everything you `[BUILD]` is a pedagogical toy. Self-rolled crypto must never touch production or real secrets. Validate toy implementations against **Project Wycheproof** and **NIST CAVP/ACVP** test vectors; ship only vetted libraries (`pyca/cryptography`, `liboqs`, `libsodium`).

---

## The physics/math accelerator

Your background collapses several prerequisites into review rather than new learning, and gives you intuition-transfer worth exploiting explicitly:

- **Linear algebra & lattices.** Lattices are discrete subgroups of ℝⁿ — literally the crystallography/Bravais-lattice picture you already own. LWE is "solve a noisy linear system over a finite field"; the geometry of SVP/CVP is the geometry-of-numbers you can visualize. This makes Phase 6 (PQC) far less alien than it is for most.
- **Probability & statistics.** The entire reductionist framework is a probability argument: advantage = |Pr[win] − ½|. Distinguishers, hybrid arguments, and the birthday bound are your daily bread already; your fraud-detection instinct for adversarial distributions transfers directly.
- **Information theory.** Shannon entropy is Gibbs/Boltzmann entropy with a different base. Perfect secrecy (one-time pad) is an entropy-conservation statement. You'll read Shannon's 1949 paper as a native, not a tourist.
- **Group/ring/field theory.** The one genuinely new algebra layer. Physics gave you groups via symmetry (Lie groups, representation theory); the crypto-relevant objects are *finite* groups (ℤ_n*, elliptic-curve groups, 𝔽_{p^k}). The abstraction is familiar; the finiteness and the *hardness* of the inverse problems are the new content.
- **Reductions ≈ physical reasoning.** A security reduction ("if you break the scheme, I break the assumption") is the same contrapositive-and-construction move as a physics no-go argument. You'll find provable security stylistically comfortable.

Callouts marked **» bridge:** appear per phase.

---

## Dependency map

```
Phase 0  Math Foundations
   │  (number theory, algebra, probability, information theory)
   ▼
Phase 1  Provable Security & Symmetric Crypto ──────► Phase 2  Side-Channel & Constant-Time
   │                                                        (strand kickoff; then runs alongside
   │                                                         every BUILD from here on)
   ▼
Phase 3  Number-Theoretic Public-Key (RSA, DH, DL)
   │
   ▼
Phase 4  Elliptic-Curve Crypto ──────────────┐
   │                                          │ (pairings introduced here,
   ▼                                          │  paid off in Phase 7)
Phase 5  Real-World Protocols (TLS 1.3, Signal, PKI, Noise)
   │
   ▼
Phase 6  Lattices & Post-Quantum ────────────┐ (needs Phase 0 algebra + your linear algebra)
   │                                          │
   ▼                                          ▼
Phase 7  Zero-Knowledge  ──►  Phase 8  MPC  ──►  Phase 9  FHE
   │        (Sigma protocols → SNARKs/STARKs; secret sharing → GC/OT → bootstrapping)
   ▼
Phase 10 Foundations Capstone (Goldreich Vols I–II; reading current research)
```

**The three strands, interleaved:**
- `[BREAK]` starts in Phase 1 (CryptoPals Sets 1–4 map exactly onto symmetric crypto) and continues set-by-set as the matching theory lands (Sets 5–6 in Phase 3, elliptic/lattice challenges via CryptoHack later). **CryptoHack** runs *continuously* from Phase 1 as spaced practice.
- `[SIDE]` formally kicks off in Phase 2 but is then a permanent overlay: every primitive you `[BUILD]` from Phase 3 on gets a constant-time review.
- `[BUILD]` shadows the theory one phase behind — you implement a primitive only after you can state its security definition.

---

# PART I — FOUNDATIONS

## Phase 0 — Mathematical Foundations
**~2–3 months.** Build the algebra/number-theory layer; review probability and information theory at speed.

**Objectives**
- Modular arithmetic, the CRT, Euler's theorem, quadratic residues, primality.
- Groups, rings, fields; finite fields 𝔽_{p^k}; the multiplicative group ℤ_n*; cyclic groups and generators.
- Discrete probability for crypto: distributions, statistical distance, the birthday problem, min-entropy.
- Information theory: Shannon entropy, perfect secrecy, the one-time pad and its impossibility limits.
- Complexity vocabulary: negligible functions, PPT algorithms, one-way functions (conceptual).

**Primary readings**
- Victor Shoup, *A Computational Introduction to Number Theory and Algebra*, 2nd ed., Cambridge UP, 2008. `[FREE]` (shoup.net/ntb). **The spine of this phase** — written by a cryptographer, algorithmically oriented, covers exactly the number theory + algebra crypto needs.
- Claude E. Shannon, "Communication Theory of Secrecy Systems," *Bell System Technical Journal* 28(4), 1949. `[FREE]`. Read for perfect secrecy and the birth of the field. `[SETTLED]`

**Supplementary**
- David S. Dummit & Richard M. Foote, *Abstract Algebra*, 3rd ed., Wiley, 2004, ISBN 978-0-471-43334-7. `[PAID]`. Reference for group/ring/field depth; dip in, don't read cover-to-cover.
- Thomas M. Cover & Joy A. Thomas, *Elements of Information Theory*, 2nd ed., Wiley, 2006, ISBN 978-0-471-24195-9. `[PAID]`. Chs. 1–2 only, unless you want the full treatment.
- Rudolf Lidl & Harald Niederreiter, *Introduction to Finite Fields and Their Applications*, rev. ed., Cambridge UP, 1994. `[PAID]`. Deep finite-field reference for later (AES field, ECC).

**Hands-on**
- `[BUILD]` Implement in Python: fast modular exponentiation, extended Euclid / modular inverse, Miller–Rabin primality, CRT reconstruction, a Tonelli–Shanks square-root. These become building blocks for RSA/DH later.
- `[BREAK]` **Begin CryptoHack** (cryptohack.org, `[FREE]`) — the "General" and "Mathematics" categories. Run it as spaced practice from here to the end.

**Checkpoint:** you can prove Euler's theorem, explain why ℤ_p* is cyclic, compute a discrete-log by hand in a tiny group, and state perfect secrecy formally.

**» bridge:** Shannon entropy = statistical-mechanics entropy (log base 2 vs ln). Finite fields are the algebra behind error-correcting codes you may have met in physics/EE.

---

## Phase 1 — Provable Security & Symmetric Cryptography
**~3–4 months.** The reductionist framework, and the symmetric world built on it. This phase sets your entire mental model.

**Objectives**
- Security *definitions* as games: IND-CPA, IND-CCA, EUF-CMA; the advantage formalism; concrete vs asymptotic security.
- One-way functions, PRGs, PRFs, PRPs; the PRP/PRF switching lemma.
- Block ciphers (AES internals, the 𝔽_{2^8} field), modes (CTR, CBC, GCM), stream ciphers (ChaCha20).
- Hash functions (Merkle–Damgård, sponge/Keccak/SHA-3), the random oracle model, birthday attacks, length-extension.
- MACs (CMAC, HMAC), and **authenticated encryption / AEAD** — the modern default; encrypt-then-MAC; the "cryptographic doom principle."
- Security *reductions*: reading and writing "if you break X, I break assumption Y."

**Primary readings**
- Jonathan Katz & Yehuda Lindell, *Introduction to Modern Cryptography*, 3rd ed., Chapman & Hall/CRC, 2020/2021, ISBN 978-0-8153-5436-9. `[PAID]`. **Primary text** for Part I (Chs. 1–6). The cleanest rigorous introduction to the definitional/reductionist style.
- Dan Boneh & Victor Shoup, *A Graduate Course in Applied Cryptography*, latest draft. `[FREE]` (crypto.stanford.edu/~dabo/cryptobook — check for the current version number). **Read in parallel** with Katz–Lindell; Part I covers symmetric crypto with a more applied flavor. This pairing (rigorous + applied) is the core of your theory diet.

**Supplementary**
- Jean-Philippe Aumasson, *Serious Cryptography*, 2nd ed., No Starch Press, 2024, ISBN 978-1-7185-0384-7. `[PAID]` (free ebook with print from nostarch.com). The best modern engineer's-eye companion; read the symmetric chapters alongside the theory for pitfalls and real-world framing. `[SETTLED]` core, with current PQC/TLS notes.
- **Free course anchor:** Dan Boneh, *Cryptography I* (Stanford, on Coursera), `[FREE]` audit — tracks this phase closely. (Note: a planned *Cryptography II* was never formally released; don't hunt for it.)

**Hands-on**
- `[BUILD]` Implement (toy) AES from the spec, then CTR and GCM modes; ChaCha20; SHA-256 and HMAC. Validate against **Project Wycheproof** and NIST vectors.
- `[BREAK]` **CryptoPals** (cryptopals.com, `[FREE]`) **Sets 1–4** — the canonical attack lab: fixed/repeating-key XOR, AES-ECB detection, the **CBC padding-oracle**, CTR bit-flipping, MAC forgery, hash length-extension. This is where the theory becomes visceral.

**Checkpoint:** you can write a full IND-CPA proof for CTR mode from a PRF assumption, and you have exploited a padding oracle with your own code.

**» bridge:** the hybrid argument (swap one component at a time, bound the total advantage) is a telescoping-sum / perturbation argument. Distinguisher = hypothesis test.

---

## Phase 2 — Side-Channel & Constant-Time Foundations *(strand kickoff)*
**~1.5–2 months focused, then permanent overlay.** Start this the moment you have symmetric primitives to attack, because implementation leakage is where real systems break.

**Objectives**
- Why "correct" ≠ "secure": timing, cache, power, and microarchitectural leakage.
- Constant-time coding discipline: no secret-dependent branches or memory indices; constant-time selects/compares.
- Cache-timing attacks on table-based AES; the case for bitsliced/AES-NI implementations.
- Differential power analysis (DPA) at a conceptual level.
- Microarchitectural attacks (Spectre/Meltdown) and why they matter for crypto secrets.
- The verification frontier: formally verified constant-time crypto.

**Primary readings**
- Paul C. Kocher, "Timing Attacks on Implementations of Diffie-Hellman, RSA, DSS, and Other Systems," *CRYPTO* 1996. `[FREE]`. The founding paper. `[SETTLED]`
- Paul Kocher, Joshua Jaffe & Benjamin Jun, "Differential Power Analysis," *CRYPTO* 1999. `[FREE]`. `[SETTLED]`
- Daniel J. Bernstein, "Cache-timing attacks on AES," 2005. `[FREE]` (cr.yp.to). Why lookup-table AES leaks. `[SETTLED]`
- BearSSL, "Constant-Time Crypto" (bearssl.org/constanttime.html). `[FREE]`. The practical coding guide — internalize this.

**Supplementary**
- Project Everest / **HACL\*** and **EverCrypt** docs; **Fiat-Crypto**; the **Jasmin** language. `[FREE]`. The state of the art in *proving* constant-time and functional correctness — aspirational reading now, genuinely relevant to your GrapheneOS ambitions later. `[MOVING]`

**Hands-on**
- `[SIDE]` Instrument your Phase-1 AES: demonstrate secret-dependent timing in a table-based implementation, then rewrite the vulnerable comparison/selection to be constant-time and show the timing signal vanish. Write a constant-time `memcmp`.
- `[SIDE]` Adopt a permanent rule: every primitive you `[BUILD]` from here on gets a constant-time audit before you move on.

**Checkpoint:** you can look at a snippet and spot the secret-dependent branch/index, and you've measured a timing leak you introduced and then closed.

**» bridge:** side channels are a measurement/signal-extraction problem — your physics-experiment instinct (noise floors, averaging, correlation) is exactly the attacker's toolkit (and DPA is literally correlation of power traces).

---

# PART II — PUBLIC-KEY & PROTOCOLS

## Phase 3 — Number-Theoretic Public-Key Cryptography
**~3 months.** RSA, Diffie–Hellman, and the discrete-log world, with the hardness assumptions underneath.

**Objectives**
- Trapdoor permutations; RSA (key gen, correctness, security caveats), RSA-OAEP, RSA-PSS.
- The discrete-log problem; Diffie–Hellman key exchange; CDH/DDH assumptions; ElGamal.
- Public-key encryption security (IND-CCA) and the random-oracle constructions.
- Digital signatures: full-domain hash, DSA/ECDSA (mechanics; ECC math lands next phase).
- Key-encapsulation (KEM) framing — the modern lens that generalizes cleanly to PQC.
- Classic attacks: small-exponent, common-modulus, Bleichenbacher's RSA-PKCS#1v1.5 padding oracle, nonce reuse in (EC)DSA.

**Primary readings**
- Katz & Lindell, 3rd ed. — Part III (public-key crypto, ~Chs. 11–14). `[PAID]`
- Boneh & Shoup, *A Graduate Course in Applied Cryptography* — Part II (public-key). `[FREE]`

**Supplementary**
- Christof Paar, Jan Pelzl & Tim Güneysu, *Understanding Cryptography: From Established Symmetric and Asymmetric Ciphers to Post-Quantum Algorithms*, 2nd ed., Springer, 2024, ISBN 978-3-662-69006-2. `[PAID]`. Excellent for public-key intuition; **free companion lecture videos** at crypto-textbook.com / YouTube (`[FREE]`).
- Rafael Pass & abhi shelat, *A Course in Cryptography* (lecture notes). `[FREE]`. A rigorous free supplement to the definitions.

**Hands-on**
- `[BUILD]` RSA (with OAEP), Diffie–Hellman, ElGamal, and a KEM wrapper, reusing your Phase-0 number-theory routines. `[SIDE]` audit the modular exponentiation for timing leakage (this is the Kocher attack made concrete).
- `[BREAK]` **CryptoPals Sets 5–6** — Diffie–Hellman MITM, parameter injection, RSA attacks, **DSA nonce-recovery**, Bleichenbacher. Continue CryptoHack "RSA" and "Diffie-Hellman" categories.

**Checkpoint:** you can recover a DSA private key from two signatures with a reused nonce (with code), and explain why textbook RSA is IND-CPA-broken.

**» bridge:** ℤ_p* and its cyclic structure from Phase 0 is now doing real work; the "hardness" of inverting exponentiation is the crux — connect to the physics intuition that some maps are easy forward, catastrophic to invert.

---

## Phase 4 — Elliptic-Curve Cryptography
**~2–3 months.** The dominant classical public-key math, and your first taste of pairings.

**Objectives**
- Elliptic curves over finite fields; the group law; the ECDLP.
- ECDH, ECDSA, and modern **EdDSA (Ed25519)** / **X25519**; the Curve25519 design philosophy (rigidity, safe curves).
- Montgomery/Edwards forms and why they enable fast constant-time implementations.
- Pairings (bilinear maps) — definitions and the problems they make easy/hard (paid off in Phase 7).

**Primary readings**
- Lawrence C. Washington, *Elliptic Curves: Number Theory and Cryptography*, 2nd ed., Chapman & Hall/CRC, 2008, ISBN 978-1-4200-7146-7. `[PAID]`. The standard crypto-oriented EC text.
- Steven D. Galbraith, *Mathematics of Public Key Cryptography*, Cambridge UP, 2012. `[FREE]` draft on the author's site. **Excellent and free** — covers ECC, pairings, *and* lattices, so it bridges Phases 4→6→7. `[SETTLED]`

**Supplementary**
- Joseph H. Silverman, *The Arithmetic of Elliptic Curves*, 2nd ed., Springer GTM 106, 2009, ISBN 978-0-387-09493-9. `[PAID]`. The deep pure-math reference; go here for the theory beneath the crypto.
- The "SafeCurves" criteria (safecurves.cr.yp.to) and the Ed25519 paper (Bernstein et al.). `[FREE]`.

**Hands-on**
- `[BUILD]` Implement the curve group law and a scalar-multiplication ladder for a small curve; then a toy X25519. `[SIDE]` implement it with the **Montgomery ladder** specifically for constant-time behavior — this is the canonical worked example of side-channel-aware design.
- `[BREAK]` CryptoHack "Elliptic Curves" category; invalid-curve and small-subgroup attacks.

**Checkpoint:** working toy X25519 with a constant-time ladder, and you can explain why nonce/curve validation failures break ECDSA/ECDH.

**» bridge:** the group law is geometry (chord-and-tangent) made algebraic — a satisfying place for a physicist; pairings are bilinear forms, structurally familiar from tensor/inner-product spaces.

---

## Phase 5 — Real-World Communication Protocols
**~3 months.** How the primitives compose into the systems that actually protect traffic. This is the "communications" half of your goal.

**Objectives**
- **TLS 1.3** end to end: handshake, key schedule, 0-RTT and its replay caveat, forward secrecy, downgrade protection.
- The **Signal protocol**: X3DH initial key agreement, the **Double Ratchet**, forward secrecy and post-compromise security; **PQXDH** (the post-quantum upgrade).
- **PKI / X.509**, certificate chains, **Certificate Transparency**, revocation, the WebPKI trust model.
- The **Noise Protocol Framework** as a clean modern design vocabulary.
- Secure-channel theory: AEAD composition, nonce management, nonce-misuse resistance (AES-GCM-SIV), replay/reorder handling.
- **Protocol verification**: symbolic analysis (Tamarin, ProVerif) and computational proofs (miTLS / Project Everest) — how we gain confidence protocols are correct.

**Primary readings (specs are primary — read them)**
- RFC 8446, *The Transport Layer Security (TLS) Protocol Version 1.3*. `[FREE]`. `[SETTLED]`
- Signal specifications: *X3DH*, *Double Ratchet*, and *PQXDH* (signal.org/docs). `[FREE]`. `[MOVING]` (PQXDH is recent).
- RFC 6962, *Certificate Transparency*. `[FREE]`.
- The Noise Protocol Framework spec (noiseprotocol.org). `[FREE]`.

**Supplementary**
- David Wong, *Real-World Cryptography*, Manning, 2021, ISBN 978-1-6172-9671-0. `[PAID]`. **The best single applied-protocols book** — TLS, Noise, PKI, end-to-end encryption, PQC, hardware. Make this the phase's narrative spine and read the specs against it.
- Niels Ferguson, Bruce Schneier & Tadayoshi Kohno, *Cryptography Engineering*, Wiley, 2010, ISBN 978-0-470-47424-2. `[PAID]`. Dated in specifics but excellent on how real systems fail; skim for judgment.

**Hands-on**
- `[BUILD]` Implement the Double Ratchet from the Signal spec in Python (a genuinely instructive, self-contained project). Build a minimal Noise handshake.
- `[BREAK]` Study historical TLS breaks as case studies (BEAST, CRIME, Lucky13, POODLE, Bleichenbacher/ROBOT) and map each to the primitive-level flaw you already understand.

**Checkpoint:** a working Double Ratchet, and you can trace the TLS 1.3 key schedule from the spec and explain each forward-secrecy guarantee.

**» bridge:** protocol state machines and their invariants are dynamical-systems reasoning; symbolic verification is model-checking a transition system — close to formal-methods intuition.

---

# PART III — POST-QUANTUM

## Phase 6 — Lattices & Post-Quantum Cryptography
**~3 months.** The standardized future of key exchange and signatures — and the phase your physics background most accelerates.

**Objectives**
- Lattices: bases, the SVP/CVP problems, LLL reduction, the geometry of numbers.
- **LWE, Ring-LWE, Module-LWE** and why they're believed quantum-hard.
- **ML-KEM** (Kyber → FIPS 203), **ML-DSA** (Dilithium → FIPS 204), **SLH-DSA** (SPHINCS+ → FIPS 205, hash-based), **FN-DSA** (Falcon → FIPS 206, NTRU lattices).
- Alternative families: hash-based signatures (XMSS/LMS), code-based KEMs (**HQC**, McEliece).
- **Hybrid deployment**: X25519+ML-KEM (X25519MLKEM768) in TLS 1.3; PQXDH in Signal; the "harvest now, decrypt later" threat and the migration timeline.

**Primary readings**
- Chris Peikert, "A Decade of Lattice Cryptography," *Found. & Trends in TCS*, 2016 (eprint 2015/939). `[FREE]`. The survey that ties LWE/SIS/Ring-LWE together. `[SETTLED]` as foundations.
- Oded Regev, "On Lattices, Learning with Errors, Random Linear Codes, and Cryptography," STOC 2005 / *JACM* 2009. `[FREE]`. The LWE paper. `[SETTLED]`
- **NIST FIPS 203 (ML-KEM), FIPS 204 (ML-DSA), FIPS 205 (SLH-DSA)** — the actual standards, published Aug 13 2024. `[FREE]` (csrc.nist.gov). `[MOVING]` for surrounding guidance; the standards themselves are stable.
- Galbraith, *Mathematics of Public Key Cryptography* (from Phase 4) — the lattice chapters. `[FREE]`.

**Supplementary**
- Daniele Micciancio & Shafi Goldwasser, *Complexity of Lattice Problems: A Cryptographic Perspective*, Springer, 2002, ISBN 978-0-7923-7688-0. `[PAID]`. The hardness-theory reference.
- Draft **FIPS 206 (FN-DSA)** and NIST IR 8545 (round-4 report) / IR 8547 (transition timelines). `[FREE]`. `[MOVING]` — FN-DSA and HQC are still landing; re-check status before relying on either.

**Hands-on**
- `[BUILD]` Implement toy LWE and Ring-LWE encryption; then a stripped-down Kyber-style KEM to feel the structure. `[SIDE]` note the constant-time and rejection-sampling subtleties that make real PQC implementations hard.
- `[BUILD]` Use **liboqs / Open Quantum Safe** (`[FREE]`) to run real ML-KEM/ML-DSA and a hybrid handshake; compare to your toy.

**Checkpoint:** you can explain LWE as a noisy linear-algebra problem, derive why decryption succeeds with high probability, and articulate the case for hybrid (classical+PQ) key exchange during migration.

**» bridge:** this is your home turf — lattices are crystallography, LWE is a noisy linear system over 𝔽_q, and the "closest vector" intuition is nearest-neighbor in a periodic structure. Expect to move fast here.

**Calibration note `[CONTESTED]`:** quantum-computer *timelines* and the true urgency of "harvest now, decrypt later" are genuinely debated; the standards are real and worth learning now, but treat specific "Q-Day by year X" claims skeptically and reason from the published migration deadlines (deprecation of 112-bit classical schemes ~2030, disallowed ~2035), not the marketing.

---

# PART IV — ADVANCED THEORY

## Phase 7 — Zero-Knowledge Proofs
**~3 months.** Proving statements while revealing nothing — from Sigma protocols to modern SNARKs/STARKs.

**Objectives**
- Interactive proofs; completeness, soundness, **zero-knowledge**; simulators.
- Commitment schemes; Sigma protocols (Schnorr); the **Fiat–Shamir** transform (interactive → non-interactive).
- ZK for all of NP (Goldreich–Micali–Wigderson).
- Modern succinct proofs: **SNARKs** and **STARKs**, polynomial commitments, the arithmetization pipeline; interactive oracle proofs.
- Where pairings (Phase 4) pay off: pairing-based SNARKs (Groth16).

**Primary readings**
- Justin Thaler, *Proofs, Arguments, and Zero-Knowledge*, Found. & Trends, 2022. `[FREE]` (people.cs.georgetown.edu/jthaler). **The modern spine** — sumcheck, IOPs, SNARKs, done rigorously.
- **Berkeley ZKP MOOC** (zk-learning.org). `[FREE]`. Lectures from the people building the field.

**Supplementary**
- Oded Goldreich, *Foundations of Cryptography, Vol. I: Basic Tools*, Cambridge UP, 2001, ISBN 978-0-521-79172-3. `[PAID]`. The rigorous ZK-for-NP treatment. Also seeds Phase 10.

**Hands-on**
- `[BUILD]` Implement a Schnorr Sigma protocol and its Fiat–Shamir NIZK; implement a small sumcheck protocol.
- `[BUILD]` Build a trivial circuit and prove it with a SNARK toolkit (e.g., a Circom/arkworks-style tutorial) to see the arithmetization end to end.

**Checkpoint:** you can construct a simulator for Schnorr ZK, and you understand the sumcheck-to-SNARK pipeline well enough to read a modern proof-system paper.

**Calibration note `[CONTESTED]`:** ZK is where blockchain marketing most outruns the cryptography. The *theory* is deep and settled; specific "production-ready, trustless, infinitely scalable" product claims deserve the skeptic's eye. Judge systems by their soundness assumptions and setup requirements.

---

## Phase 8 — Secure Multiparty Computation
**~2–3 months.** Computing on inputs no party will reveal.

**Objectives**
- Secret sharing (Shamir); the simulation paradigm; semi-honest vs malicious security.
- **Oblivious transfer** and OT extension; **garbled circuits** (Yao); the **GMW** and **BGW** protocols.
- Private set intersection and other applied MPC (directly relevant to fraud/privacy).

**Primary readings**
- David Evans, Vladimir Kolesnikov & Mike Rosulek, *A Pragmatic Introduction to Secure Multi-Party Computation*, Found. & Trends, 2018. `[FREE]` (securecomputation.org). **The spine** — modern, readable, rigorous.
- Ronald Cramer, Ivan Damgård & Jesper Buus Nielsen, *Secure Multiparty Computation and Secret Sharing*, Cambridge UP, 2015, ISBN 978-1-107-04305-3. `[PAID]`. The deeper theory.

**Hands-on**
- `[BUILD]` Implement Shamir secret sharing and a 2-party garbled-circuit evaluation of a small function (e.g., Yao's millionaires).

**Checkpoint:** you can state and use the simulation-based security definition, and you've run a garbled circuit end to end.

**» bridge:** the simulation paradigm ("real vs ideal world indistinguishable") is the same indistinguishability move from Phase 1, lifted to interactive multi-party settings.

---

## Phase 9 — Fully Homomorphic Encryption
**~2–3 months.** Computing on ciphertexts — the capstone application of the lattice machinery from Phase 6.

**Objectives**
- Partially → somewhat → fully homomorphic; noise growth; **Gentry's bootstrapping** blueprint.
- The modern schemes: **BGV/BFV** (exact integer arithmetic), **CKKS** (approximate/real arithmetic — of obvious interest for ML on encrypted data), **TFHE** (fast bootstrapping, arbitrary functions).
- Practical constraints and the standardization effort.

**Primary readings**
- Craig Gentry, "A Fully Homomorphic Encryption Scheme," PhD thesis, Stanford, 2009. `[FREE]`. The origin; read for the bootstrapping idea. `[SETTLED]` as foundations.
- *Homomorphic Encryption Standard* (homomorphicencryption.org). `[FREE]`. Parameters and security guidance. `[MOVING]`

**Supplementary**
- A current FHE survey (e.g., Halevi's) plus the docs for **Microsoft SEAL**, **OpenFHE**, and **Zama's TFHE-rs / Concrete**. `[FREE]`. `[MOVING]`

**Hands-on**
- `[BUILD]` Implement a toy leveled BFV-style scheme on your Phase-6 Ring-LWE code to watch noise grow; then use **OpenFHE or SEAL** to run CKKS on real data (compute an encrypted dot product — a direct bridge to your ML work).

**Checkpoint:** you can explain why bootstrapping is necessary and what it costs, and you've evaluated a nontrivial function homomorphically with a real library.

**Calibration note `[CONTESTED]`:** FHE performance and "run any ML model on encrypted data at scale" claims are the hype frontier. The math is sound and improving fast; production readiness is domain-specific. Benchmark before believing.

**» bridge:** CKKS is approximate arithmetic on encrypted vectors — encrypted linear algebra, i.e., your day job with a noise budget. This is the phase most likely to connect to your PayPal/ML work (private inference, privacy-preserving fraud signals).

---

## Phase 10 — Foundations Capstone
**~ongoing.** Consolidate the theory at full rigor and transition to reading current research.

**Objectives**
- The rigorous foundations, top to bottom: OWFs → PRGs → PRFs → the whole edifice.
- Reading eprint/IACR papers fluently; following a top venue (CRYPTO/EUROCRYPT/TCC).

**Primary readings**
- Oded Goldreich, *Foundations of Cryptography, Vol. I: Basic Tools* (2001, ISBN 978-0-521-79172-3) and *Vol. II: Basic Applications* (2004, ISBN 978-0-521-83084-3), Cambridge UP. `[PAID]`. The definitive theoretical treatment.
- **MIT 6.875 / 6.5620** (Foundations of Cryptography, Vaikuntanathan) lecture notes, and **Katz's** Maryland course notes. `[FREE]`.
- The **IACR ePrint Archive** (eprint.iacr.org). `[FREE]`. Your ongoing feed.

**Checkpoint:** you can read a current lattice/ZK/MPC paper and reconstruct its security argument.

---

## Fast-Track (MVP, ~7–9 months)

If you want a usable working knowledge before the full arc, do the load-bearing 30% and defer the rest:

1. **Provable security + symmetric** (Phase 1): Katz–Lindell Chs. 1–6 + Boneh–Shoup Part I. `[BREAK]` CryptoPals Sets 1–4. `[SIDE]` the constant-time comparison rewrite.
2. **Public-key essentials** (Phase 3, condensed): RSA + DH + KEM framing; `[BREAK]` CryptoPals Sets 5–6.
3. **ECC essentials** (Phase 4, condensed): X25519/Ed25519 mechanics + one constant-time ladder.
4. **Protocols** (Phase 5): Real-World Cryptography (Wong) cover-to-cover + skim RFC 8446 and the Signal specs; build the Double Ratchet.
5. **PQC awareness** (Phase 6, condensed): the FIPS 203/204/205 overview + one toy LWE + a liboqs hybrid handshake.

**Defer to the full track:** deep algebra/number-theory proofs, elliptic-curve pure math, ZK/MPC/FHE, pairings, and Goldreich. Anchor the whole fast-track with Dan Boneh's free *Cryptography I*.

---

## Calibration summary

| Domain | Status | Note |
|---|---|---|
| Reductionist/provable-security framework | `[SETTLED]` | Learn once, from Katz–Lindell + Boneh–Shoup. |
| AES, SHA-2, SHA-3/Keccak, AEAD | `[SETTLED]` | The symmetric bedrock. |
| RSA/DH/ECDLP hardness (classical) | `[SETTLED]` | But `[MOVING]` under the PQ-migration clock (deprecation ~2030). |
| TLS 1.3, Signal/Double Ratchet | `[SETTLED]` | Designs are stable and formally analyzed; PQXDH is `[MOVING]`. |
| PQC standards (FIPS 203/204/205) | `[SETTLED]` core, `[MOVING]` edges | 203/204/205 final (Aug 2024); FN-DSA (206) and HQC still landing — re-verify. |
| Hybrid PQC deployment (X25519MLKEM768, etc.) | `[MOVING]` | IETF/browser rollout ongoing; check current state before relying. |
| Quantum timelines / "harvest now, decrypt later" urgency | `[CONTESTED]` | Standards real; specific Q-Day dates are speculation. |
| ZK product/scalability claims | `[CONTESTED]` | Theory deep; judge systems by setup + soundness assumptions. |
| FHE production-readiness / "ML on encrypted data at scale" | `[CONTESTED]` | Improving fast; benchmark before believing. |
| Side-channel exploitability in practice | `[CONTESTED]` | Real but context-dependent; threat-model per deployment. |
| QKD (quantum key distribution) practicality | `[CONTESTED]` | Note the NSA/NCSC skepticism vs vendor claims; not a substitute for PQC. |

---

## Master resource list (grouped)

**Core theory** — Katz & Lindell 3e `[PAID]`; Boneh & Shoup (draft) `[FREE]`; Goldreich Vols I–II `[PAID]`; Pass & shelat notes `[FREE]`.

**Math** — Shoup, *Computational Intro to NT & Algebra* `[FREE]`; Dummit & Foote `[PAID]`; Lidl & Niederreiter `[PAID]`; Cover & Thomas `[PAID]`; Shannon 1949 `[FREE]`.

**ECC / pairings / lattices (math)** — Washington `[PAID]`; Silverman `[PAID]`; Galbraith `[FREE]`; Peikert survey `[FREE]`; Regev LWE `[FREE]`; Micciancio & Goldwasser `[PAID]`.

**Applied / protocols** — Aumasson, *Serious Cryptography* 2e (2024) `[PAID]`; Wong, *Real-World Cryptography* `[PAID]`; Paar/Pelzl/Güneysu 2e (2024) `[PAID]` + free videos; Ferguson/Schneier/Kohno `[PAID]`.

**Protocol specs (primary)** — RFC 8446 (TLS 1.3); Signal X3DH / Double Ratchet / PQXDH; RFC 6962 (CT); Noise framework. All `[FREE]`.

**PQC standards** — FIPS 203/204/205 (final); draft FIPS 206; NIST IR 8545/8547. All `[FREE]`, `[MOVING]`.

**Frontier theory** — Thaler, *Proofs, Arguments, and ZK* `[FREE]`; Berkeley ZKP MOOC `[FREE]`; Evans/Kolesnikov/Rosulek MPC `[FREE]`; Cramer/Damgård/Nielsen `[PAID]`; Gentry thesis `[FREE]`; HE Standard `[FREE]`; BLS + Boneh–Franklin papers `[FREE]`.

**Free courses** — Boneh *Cryptography I* (Coursera); Paar YouTube lectures; MIT 6.875/6.5620 notes; Katz Maryland notes. All `[FREE]`.

**Hands-on** — CryptoPals (8 sets) `[FREE]`; CryptoHack `[FREE]`; Project Wycheproof + NIST CAVP/ACVP vectors `[FREE]`; `pyca/cryptography` & PyCryptodome; liboqs `[FREE]`; SEAL / OpenFHE / TFHE-rs `[FREE]`.

**Side-channel** — Kocher 1996 (timing) `[FREE]`; Kocher/Jaffe/Jun 1999 (DPA) `[FREE]`; Bernstein 2005 (cache-timing) `[FREE]`; BearSSL constant-time guide `[FREE]`; HACL\*/EverCrypt, Fiat-Crypto, Jasmin `[FREE]`.

---

*Currency note (2026): PQC standardization is the fastest-moving part of this curriculum — FN-DSA (FIPS 206) and HQC are still in the pipeline, and hybrid-deployment specifics change quarterly. Re-verify anything PQC-related against csrc.nist.gov and the relevant IETF drafts before you rely on it. Book editions and library APIs also drift; confirm the latest before purchase/install.*