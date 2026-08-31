# A Self-Study Curriculum on Compromising Emanations & Physical Side-Channel Attacks

## TL;DR
- A complete, reproducible graduate-level curriculum can be assembled almost entirely from free primary sources: start with **power analysis** (the most mature, most reproducible channel via the open-source ChipWhisperer + ANSSI's ASCAD dataset), then move to **acoustic** (anchored on Harrison–Toreini–Mehrnezhad's 2023 CoAtNet keyboard attack — 95% accuracy from a nearby phone, 93% over Zoom), **EM/TEMPEST** (van Eck → Kuhn → Screaming Channels, reproducible with an RTL-SDR + gr-tempest), and **optical** (Loughry–Umphress → Lamphone/Glowworm → Video-Based Cryptanalysis).
- The learner's physics/ML background is an ideal fit: the math prerequisites (Fourier/DSP, EM near/far-field, CMOS switching power → Hamming-weight/distance leakage, statistical estimation) map directly onto stat-mech, electromagnetism, and Fourier analysis they already have; the main *new* skills are RF/SDR practice and side-channel-specific evaluation metrics (guessing entropy, key rank).
- Calibration is essential to reaching "read/evaluate/reproduce SOTA" level: many headline results are lab-bound (single keyboard, quiet room, chosen-ciphertext, short distances, anechoic chambers). Reported figures are real but come with strong assumptions this report flags per channel.

## Key Findings

**The field has a clear canonical spine.** Every channel has (1) a 1985–2006 foundational layer, (2) a 2014–2018 "physics-heavy demonstration" layer, and (3) a 2018–2026 deep-learning SOTA layer. Study them in that order per channel, because modern DL papers assume the earlier signal-processing framing.

**Power analysis is the best on-ramp** despite acoustic being the stated anchor, because it is the most reproducible at low cost/risk (ChipWhisperer), has the cleanest public benchmark (ASCAD), and its DL-SCA methodology literature (Cagli, Prouff, Picek) is the most rigorous in the whole field — the concepts (profiling, leakage models, guessing entropy) transfer directly to the other three channels.

**The single best "state of the field" documents** are: Picek, Perin, Mariot, Wu & Batina, "SoK: Deep Learning-based Physical Side-channel Analysis" (ACM Computing Surveys 2023) for power/EM; and for acoustic, the SoK "Acoustic Side Channels" (ACM Computing Surveys) plus the Taheritajar–Harris–Rahaeimehr survey (2023/2024).

---

## Details — Curriculum by Channel

### Module 0 — Foundations & Cross-Cutting Prerequisites

**Math/physics prerequisites (the learner largely has these):**
- **DSP / Fourier**: STFT, windowing, spectrograms, MFCCs/mel-spectrograms, cepstrum. Free canonical resource: **Steven W. Smith, *The Scientist and Engineer's Guide to Digital Signal Processing*** — fully free at dspguide.com, all 33 chapters downloadable. This is the DSP backbone for the acoustic and EM channels.
- **Statistics/estimation**: correlation, template/Gaussian modeling, guessing entropy, key rank, success rate — covered in the SCA textbook below and the Picek SoK.
- **EM theory**: near-field vs far-field, antennas, RF propagation — the learner's electromagnetism background covers the physics; the new practical layer is SDR.
- **CMOS/power**: dynamic switching power, Hamming-weight (bus precharge) and Hamming-distance (register transition) leakage models — covered in Mangard–Oswald–Popp.

**Cross-cutting textbooks / free lecture notes:**
- **Ross Anderson, *Security Engineering* (3rd ed.)** — the "Emission Security / Side Channels" chapters. The full text is FREE at cl.cam.ac.uk/~rja14/book.html. Best conceptual overview and calibration; Anderson was Kuhn's PhD advisor.
- **Markus Kuhn's Cambridge materials** (cl.cam.ac.uk/~mgk25/) — his PhD thesis and TEMPEST papers are all free PDFs; the anchor primary sources for EM/optical display eavesdropping.
- **Stefan Mangard, Elisabeth Oswald & Thomas Popp, *Power Analysis Attacks: Revealing the Secrets of Smart Cards*** (Springer, 2007) — the standard power-analysis textbook (DPA, CPA, templates, leakage models). Not free.

**Venues to monitor for ongoing SOTA:** IACR CHES / TCHES (the primary venue for power/EM DL-SCA), USENIX Security, IEEE S&P (Oakland), ACM CCS, NDSS, and COSADE (Constructive Side-Channel Analysis and Secure Design).

---

### Module 1 — Power Analysis (recommended starting channel)

**Foundational layer (all should be read):**
- **Paul C. Kocher, "Timing Attacks on Implementations of Diffie-Hellman, RSA, DSS, and Other Systems," CRYPTO 1996**, LNCS vol. 1109, pp. 104–113, DOI 10.1007/3-540-68697-5_9. The paper that founded timing side channels: *"By carefully measuring the amount of time required to perform private key operations, attackers may be able to find fixed Diffie-Hellman exponents, factor RSA keys, and break other cryptosystems."* Also introduces blinding countermeasures.
- **Kocher, Jaffe & Jun, "Differential Power Analysis," CRYPTO 1999**, LNCS 1666, pp. 388–397, DOI 10.1007/3-540-48405-1_25. The founding DPA paper. (See also the 2011 *J. Cryptographic Engineering* "Introduction to Differential Power Analysis" retrospective.)
- **Chari, Rao & Rohatgi, "Template Attacks," CHES 2002**, LNCS 2523, pp. 13–28. Introduces the profiled/Gaussian-template approach — the conceptual ancestor of DL-SCA.
- **Brier, Clavier & Olivier, "Correlation Power Analysis with a Leakage Model," CHES 2004**, LNCS 3156, pp. 16–29. Introduces CPA using the Hamming-distance model — still the workhorse non-profiled attack.

**Deep-learning SOTA layer:**
- **Cagli, Dumas & Prouff, "Convolutional Neural Networks with Data Augmentation Against Jitter-Based Countermeasures," CHES 2017**, LNCS 10529, pp. 45–68 (also IACR ePrint 2017/740, free). Shows CNNs defeat misalignment/jitter countermeasures without realignment or point-of-interest selection — the pivotal end-to-end DL-SCA paper.
- **Benadjila, Prouff, Strullu, Cagli & Dumas, "Deep learning for side-channel analysis and introduction to the ASCAD database," *Journal of Cryptographic Engineering* 10(2), 2020, pp. 163–188**, DOI 10.1007/s13389-019-00220-8 (extended preprint IACR 2018/053). Introduces the field's canonical benchmark: an 8-bit **ATMega8515** running **masked AES-128**, targeting the 3rd key byte's masked S-box output; **60,000 traces (50k profiling / 10k attack, 700 samples each)** plus desync=50/100 variants. Key finding: the VGG-style **"CNN_best"** outperforms MLPs and templates on desynchronized traces. Dataset + code free at github.com/ANSSI-FR/ASCAD. ASCADv2 (Cortex-M4, affine masking + shuffling, 800k traces) is the harder modern benchmark.
- **Picek, Perin, Mariot, Wu & Batina, "SoK: Deep Learning-based Physical Side-channel Analysis," ACM Computing Surveys 55(11):236, 2023** (free preprint IACR 2021/1092). The essential survey; also the key methodological warning that ML accuracy is misleading in SCA — use **guessing entropy / key rank / success rate** instead.
- Further methodology to skim: Zaid et al. "Methodology for Efficient CNN Architectures in Profiling Attacks" (TCHES 2020); Wu, Perin & Picek "I Choose You: Automated Hyperparameter Tuning" (TCHES 2022); Perin/Wu/Picek "Exploring Feature Selection Scenarios" (TCHES 2022); and recent transformer/state-space work (e.g., "Generalized Power Attacks against Crypto Hardware using Long-Range Deep Learning," arXiv 2306.07249).

**Physics foundation:** CMOS dynamic power ∝ switching activity → Hamming-weight and Hamming-distance leakage models. Read the relevant chapters of Mangard–Oswald–Popp alongside Kocher's DPA paper.

**Reproduction project:** Buy a **ChipWhisperer-Lite/Nano** (NewAE — fully open-source hardware, firmware, and Jupyter courses at chipwhisperer.readthedocs.io and github.com/newaetech/chipwhisperer). Progression: (1) capture AES power traces; (2) run CPA to recover an AES key; (3) build a template attack; (4) reproduce a CNN attack on ASCAD in PyTorch; (5) measure success with guessing entropy. This single track teaches ~70% of the transferable skills for all four channels.

---

### Module 2 — Acoustic Side Channels (the stated anchor)

**Foundational layer:**
- **Asonov & Agrawal, "Keyboard Acoustic Emanations," IEEE S&P 2004**, pp. 3–11, DOI 10.1109/SECPRI.2004.1301311. The origin paper. Uses **FFT features** from the keystroke "push/touch peak" (44.1 kHz sampling) classified by a backpropagation neural network; reports **~79% top-1 / 88% top-3 same-keyboard accuracy**.
- **Zhuang, Zhou & Tygar, "Keyboard Acoustic Emanations Revisited," ACM CCS 2005; extended in ACM TISSEC 13(1):3, 2009** (free PDFs at berkeley.edu and cornell.edu). Landmark: recovers up to **96% of characters from a 10-minute recording with NO labeled training data**, using cepstrum features + HMM + language model + unsupervised bootstrapping. Recovers 90% of 5-character random passwords in <20 attempts. This paper is also the source of the widely cited cross-keyboard degradation figure — *training on one keyboard and recognizing on another keyboard of the same model yields accuracy around 25%* — which is the single most important calibration datapoint in the acoustic literature.
- **Berger, Wool & Yeredor, "Dictionary Attacks Using Keyboard Acoustic Emanations," ACM CCS 2006**, pp. 245–254, DOI 10.1145/1180405.1180436. No training; reconstructs single words from one <5 s recording (<20 s compute/word). Reports **≥90% success finding the correct word in the top-50 candidates for words ≥10 characters, 73% overall** (words 7–13 chars).
- Halevi & Saxena work on acoustic eavesdropping (CCS 2010 and follow-ups) on constrained-device pairing / keystroke masking.

**Component acoustic cryptanalysis:**
- **Genkin, Shamir & Tromer, "RSA Key Extraction via Low-Bandwidth Acoustic Cryptanalysis," CRYPTO 2014**, LNCS 8616, pp. 444–461; extended in *Journal of Cryptology* 30(2):392–443, 2017; free IACR ePrint 2013/857. Exploits coil-whine/capacitor acoustic leakage: *"The attack can extract full 4096-bit RSA decryption keys from laptop computers (of various models), within an hour... using either a plain mobile phone placed next to the computer, or a more sensitive microphone placed 10 meters away"* (the CRYPTO 2014 conference version and ePrint 2013/857 quote 4 m; the extended Journal of Cryptology version quotes 10 m). **Strong assumptions: chosen ciphertext and a specific GnuPG version — patched in GnuPG 1.4.16 via blinding.**

**Deep-learning SOTA layer (2017–2026):**
- **Compagno, Conti, Lain & Tsudik, "Don't Skype & Type! Acoustic Eavesdropping in Voice-over-IP," ACM AsiaCCS 2017** (extended as "Skype & Type," ACM TOPS 22(4), 2019). Weak-adversary VoIP threat model; top-5 accuracy **91.7%** with typing-style/keyboard knowledge, **~41.9%** oblivious. Open-source tool: github.com/SPRITZ-Research-Group/Skype-Type.
- **Harrison, Toreini & Mehrnezhad, "A Practical Deep Learning-Based Acoustic Side Channel Attack on Keyboards," IEEE EuroS&PW 2023**, pp. 270–280, DOI 10.1109/EuroSPW59978.2023.00034 (free arXiv 2308.01074). The modern anchor: a **CoAtNet** (conv+transformer) on mel-spectrograms of MacBook Pro keystrokes. Verbatim: *"When trained on keystrokes recorded by a nearby phone, the classifier achieved an accuracy of 95%, the highest accuracy seen without the use of a language model. When trained on keystrokes recorded using the video-conferencing software Zoom, an accuracy of 93% was achieved, a new best for the medium."*
- 2024–2026 follow-ups: an **"Improved CoAtNet for robust acoustic side-channel attack classification on keyboards"** (Int. J. Information Security, 2025, DOI 10.1007/s10207-025-01194-x) trained on the Multi-Keyboard Acoustic (MKA) dataset (HP, Lenovo, MSI, Mac, Messenger, Zoom) reporting **99.8% accuracy, 99.81% precision, 99.8% recall, 99.99% specificity**; "Making Acoustic Side-Channel Attacks on Noisy Keyboards Viable with LLM-Assisted Spectrogram 'Typo' Correction" (arXiv 2504.11622, 2025); speech-representation-learning approaches (arXiv 2606.21210, 2026); NDSS 2024 VR-controller acoustic keystroke inference; ReflexNoop (CCS 2024, screen-induced sound reflection on NLOS laptops).

**Best surveys:** "SoK: Acoustic Side Channels" (ACM Computing Surveys, Wang et al.; free preprint arXiv 2308.03806); Taheritajar, Harris & Rahaeimehr, "A Survey on Acoustic Side Channel Attacks on Keyboards" (arXiv 2309.11012; ICICS 2024, LNCS 15056); and "A Survey on Acoustic Side-Channel Attacks: An AI Perspective" (MDPI *J. Cybersecurity & Privacy* 6(1):6, 2025).

**Physics/math foundation:** key-press sound generation (finger–plate impact, plate resonance), room acoustics/reverberation, microphone transduction, and the DSP of spectrograms/MFCCs/cepstrum (Smith's DSP guide). The learner's Fourier background covers most of this.

**Reproduction project:** Record your own keystrokes with a phone/laptop mic; segment keystrokes by energy onset; extract mel-spectrograms with **librosa**; train a CNN/CoAtNet in **PyTorch**. Start from open reproductions: github.com/shoyo/acoustic-keylogger (unsupervised pipeline) and the Skype-Type repo.

---

### Module 3 — Electromagnetic / TEMPEST

**Foundational layer:**
- **Wim van Eck, "Electromagnetic Radiation from Video Display Units: An Eavesdropping Risk?" *Computers & Security* 4(4), 1985.** The paper that made the risk public; reconstructs CRT screen content from RF emanations with a modified TV.
- **Kuhn & Anderson, "Soft Tempest: Hidden Data Transmission Using Electromagnetic Emanations," Information Hiding 1998**, LNCS 1525, pp. 124–142 (free PDF at cl.cam.ac.uk/~mgk25/ih98-tempest.pdf). Attack AND defense; introduces controlling emissions via specially designed fonts and covert channels.
- **Markus Kuhn, "Compromising Emanations: Eavesdropping Risks of Computer Displays," Cambridge PhD thesis / Tech Report UCAM-CL-TR-577, 2003** (free at cl.cam.ac.uk/techreports/). The definitive treatment of display emanations.
- **Kuhn, "Optical Time-Domain Eavesdropping Risks of CRT Displays," IEEE S&P 2002**, and **"Electromagnetic Eavesdropping Risks of Flat-Panel Displays," PET 2004**, LNCS 3424 (both free PDFs at his Cambridge page). Extends the risk to LCDs and, in the 2002 paper, to the optical channel. See also his 2006 survey "Eavesdropping attacks on computer displays."
- **Vuagnoux & Pasini, "Compromising Electromagnetic Emanations of Wired and Wireless Keyboards," USENIX Security 2009** (free at usenix.org). Detects four EM leakage modes; best practical attack **fully recovered 95% of PS/2 keystrokes at up to 20 m**, even through walls.

**Declassified/reference material:** NSA **NACSIM 5000 "TEMPEST Fundamentals"** (1982, declassified) and "TEMPEST: A Signal Problem" (NSA), available via cryptome.org — historical/contextual, not technical tutorials.

**Modern EM SCA SOTA:**
- **Camurati, Poeplau, Muench, Hayes & Francillon, "Screaming Channels: When Electromagnetic Side Channels Meet Radio Transceivers," ACM CCS 2018**, pp. 163–177, DOI 10.1145/3243734.3243802 (free preprint + project + code at eurecom-s3.github.io/screaming_channels). Mixed-signal chips (BLE/WiFi) re-broadcast digital EM leakage on the radio carrier, extending EM SCA into the far field: full-key recovery from tinyAES AES-128 on the **Nordic nRF52832 at 10 m using template attacks in an anechoic chamber**, and mbedTLS AES-128 **at 1 m with a correlation attack in an office**. The 2020 TCHES follow-up ("Understanding Screaming Channels," by Camurati, Francillon & Standaert) extends this to **15 m in an office** with key enumeration up to 2²³.
- Deep-learning EM: Wang, Wang & Dubrova, "Far Field EM Side-Channel Attack on AES Using Deep Learning" (ASHES@CCS 2020); portability studies (RAID 2024, "A Second Look at the Portability of Deep Learning SCA over EM Traces"); drone-based EM SCA frameworks (2025–2026 arXiv, e.g., "TriSweep").
- Also relevant: Genkin, Pachmanov, Pipman & Tromer, "ECDH Key-Extraction via Low-Bandwidth Electromagnetic Attacks on PCs" (CT-RSA 2016); Genkin, Pipman & Tromer, "Get Your Hands Off My Laptop" (CHES 2015).

**Physics/math foundation:** EM radiation, near-field vs far-field regions, antenna basics (dipole / log-periodic / directional), RF propagation and modulation (AM/PAM), and SDR fundamentals (IQ sampling, downconversion, IF filtering). Pair the learner's EM background with an SDR primer; the "gr-tempest" paper (Larroca et al.) derives the TEMPEST signal model mathematically.

**Reproduction project:** **RTL-SDR** (cheap) or **HackRF/USRP** (better) + **GNU Radio**. Reproduce van Eck phreaking with **TempestSDR** (Martin Marinov, github.com/martinmarinov/TempestSDR) or the GNU Radio port **gr-tempest** (github.com/git-artes/gr-tempest; see the GRCon21 talk and the "gr-tempest" IEEE paper for the math). Screaming Channels can be reproduced from the EURECOM repo with a Nordic BLE devkit.

---

### Module 4 — Optical Side Channels

**Foundational layer:**
- **Loughry & Umphress, "Information Leakage from Optical Emanations," ACM TISSEC 5(3):262–289, 2002** (free copies online; original C code at github.com/jloughry/optical_tempest). Founds "Optical TEMPEST": LED status indicators carry a modulated signal correlated with processed data, interceptable at distance; includes a taxonomy (Class I–III) and countermeasures. Appendix A demonstrates a keyboard-LED covert channel at ~150 bit/s.
- **Kuhn, "Optical Time-Domain Eavesdropping Risks of CRT Displays," IEEE S&P 2002** (see Module 3) — recovers CRT content from the diffuse light flicker in a room.
- **Backes, Dürmuth & Unruh, "Compromising Reflections — or — How to Read LCD Monitors Around the Corner," IEEE S&P 2008**, and the 2009 follow-up "Tempest in a Teapot: Compromising Reflections Revisited." Reads screen content from reflections in eyeglasses, teapots, spoons, even the user's eye — small fonts at up to **10 m (cheap, <$1,500 gear) / 30 m (expensive gear)**.

**Modern SOTA (Ben Nassi et al.):**
- **Nassi, Pirutin, Shamir, Elovici & Zadov, "Lamphone: Real-Time Passive Sound Recovery from Light Bulb Vibrations," 2020** (Black Hat / IACR ePrint; project at nassiben.com/lamphone). Recovers speech/music from a hanging bulb's sound-induced vibrations, **passively, from 25 m** — using a telescope + a Thorlabs PDA100A2 electro-optical sensor, with the eavesdropper positioned on a pedestrian bridge 25 m from the target office.
- **Nassi, Pirutin, Galor, Elovici & Zadov, "Glowworm Attack: Optical TEMPEST Sound Recovery via a Device's Power Indicator LED," ACM CCS 2021** (free IACR ePrint 2021/1064; project at nassiben.com/glowworm-attack). Recovers speech from a device's power LED (whose intensity tracks power consumption) **with good intelligibility from 15 m and fair intelligibility from 35 m**; roughly half of tested devices (e.g., Google Nest Audio, Logitech Z120, Sony SRS-XB43, Raspberry Pi 3/4) were vulnerable.
- **Nassi, Iluz, et al., "Video-Based Cryptanalysis: Extracting Cryptographic Keys from Video Footage of a Device's Power LED," 2023** — recovers ECDSA/SIKE keys from a smart-card reader's or phone's power LED filmed by an off-the-shelf camera (iPhone / internet-connected security camera), extending power SCA into the optical/video domain by exploiting rolling-shutter sampling.

**Physics/math foundation:** photodiode / electro-optical transduction and bandwidth, rolling-shutter vs global-shutter camera sampling (aliasing exploited as a sampling mechanism), optics of reflections / PSF deconvolution, and the same DSP/audio-recovery pipeline as the acoustic channel.

**Reproduction project:** A photodiode + ADC (or an oscilloscope) aimed at a device LED, plus the audio pipeline from Module 2. Lamphone-style recovery needs a telescope + electro-optical sensor (e.g., a Thorlabs PDA-series photodiode). The Loughry–Umphress C code is a working starting point for LED data leakage.

---

## Recommendations (staged)

**Stage 1 (Weeks 1–4) — Build the transferable core with Power Analysis.** Read Kocher (DPA), Brier (CPA), Chari (templates). Buy a ChipWhisperer. Reproduce CPA → template attack → guessing-entropy evaluation. *Benchmark to advance:* you can recover an AES key byte from your own traces and articulate why classification accuracy ≠ attack success.

**Stage 2 (Weeks 5–8) — DL-SCA on ASCAD.** Read Cagli (CHES 2017), Benadjila (ASCAD), Picek SoK. Reproduce CNN_best on ASCAD in PyTorch; then attack the desync=50/100 variants. *Benchmark:* reproduce a published guessing-entropy curve within a reasonable factor of the paper.

**Stage 3 (Weeks 9–12) — Acoustic (the anchor).** Read Asonov→Zhuang→Berger→Genkin, then Skype&Type and Harrison 2023. Record your own keystrokes; build a mel-spectrogram CoAtNet/CNN. *Benchmark:* >80% top-1 single-keyboard accuracy in a quiet room; then deliberately measure how much it degrades cross-keyboard and in noise (this *is* the calibration lesson — expect a collapse toward the ~25% Zhuang cross-keyboard regime).

**Stage 4 (Weeks 13–16) — EM/TEMPEST.** Read van Eck→Soft Tempest→Kuhn thesis→Vuagnoux→Screaming Channels. Reproduce van Eck with RTL-SDR + gr-tempest. *Benchmark:* recover recognizable text/image from your own monitor's emanations.

**Stage 5 (Weeks 17–20) — Optical + synthesis.** Read Loughry→Backes→Lamphone→Glowworm→Video-Based Cryptanalysis. Build an LED-to-audio recovery rig. Then write a critical literature review reconciling *reported* vs *realistic* feasibility across all four channels — the deliverable that demonstrates you can evaluate SOTA, not just reproduce it.

**Thresholds that change the plan:** If hardware budget is zero, do Stages 2, 3, and the LED half of Stage 5 entirely in software on public datasets / your own recordings, and use recorded I/Q captures for gr-tempest instead of buying SDR hardware. If the goal shifts toward *publishing*, prioritize the CHES/TCHES + USENIX pipeline and reproduce one SOTA result end-to-end before attempting novelty; monitor COSADE and NDSS for emerging cross-channel (RF-backscatter, VR, video-conferencing) keystroke work.

## Caveats & Calibration (contested / overstated feasibility)

- **Acoustic keystroke accuracy is fragile out of the lab.** The 95%+ figures assume a *single known keyboard*, a *quiet room*, and often *the same typist*. Asonov–Agrawal's same-keyboard ~79% collapses toward ~25% cross-keyboard (per Zhuang et al.). Generalization across keyboards, typists, microphones, and noise is the open problem the 2024–2026 LLM/self-supervised papers explicitly target — treat single-setup numbers as upper bounds, and note that the 99.8% "Improved CoAtNet" figure is measured on its own curated multi-keyboard dataset, not a live adversarial capture.
- **Genkin acoustic RSA** requires *chosen ciphertext* and a *specific vulnerable GnuPG version* (since patched via blinding in 1.4.16). It is a landmark demonstration, not a turnkey remote attack.
- **Screaming Channels' 10 m** result is in an *anechoic chamber*; the office-environment range is ~1 m (extended to ~15 m only with key enumeration up to 2²³). Distance claims across EM/optical are highly environment-dependent.
- **Optical bulb/LED speech recovery** (Lamphone at 25 m; Glowworm good-at-15 m / fair-at-35 m) needs *line of sight*, a telescope/electro-optical sensor, and sufficiently loud sound / a responsive LED; only about half of Glowworm's tested devices were vulnerable, and intelligibility degrades with distance and glazing.
- **Metric hygiene:** in power/EM DL-SCA, classification accuracy is *misleading* (Picek et al.); always report guessing entropy / key rank / success rate. Carry this discipline into acoustic and optical work too.
- **Source-type flags:** NSA NACSIM 5000 and "TEMPEST: A Signal Problem" are historical/declassified context, not method tutorials. Vendor/press write-ups (Hackaday, The Hacker News, rtl-sdr.com) are useful for reproduction logistics but should never be cited for quantitative claims — go to the primary PDF. Where a figure appears only in a secondary source (e.g., the "~25% cross-keyboard" number, which originates in Zhuang–Zhou–Tygar rather than Asonov–Agrawal), trace it to the primary before relying on it.