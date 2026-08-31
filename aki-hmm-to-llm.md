# HMMs, Language Models, and Modern Sequence Decoders in Physical Side-Channel & Keystroke-Inference Attacks — An Annotated, Well-Cited Curriculum Module

## TL;DR
- **Keystroke inference is structurally a speech-recognition / sequence-decoding problem**, and the field's history maps cleanly onto ASR's: an *acoustic/observation model* (a per-key classifier or an inter-keystroke-timing distribution) feeds a *decoder* (Viterbi/beam search) constrained by a *language model* (n-gram → LLM). The single most important applied primary source is Song, Wagner & Tian (USENIX Security 2001), which models inter-keystroke timing with an HMM and an n-Viterbi decoder ("Herbivore") and, in their words, "for passwords that are chosen uniformly at random with length of 7 to 8 characters, Herbivore can reduce the cost of password cracking by a factor of 50."
- **Part A** gives you the canonical, mostly-FREE foundations: Rabiner (1989) for the HMM triad (Forward-Backward, Viterbi, Baum-Welch/EM); the primary algorithm papers (Viterbi 1967; Baum-Petrie-Soules-Weiss 1970); Jurafsky & Martin *SLP3* (free) for n-grams, noisy-channel decoding, and HMMs; and the successors (CTC 2006, seq2seq 2014, attention 2015, Transformer 2017).
- **Part B** traces the applied through-line: HMM+LM acoustic attacks (Zhuang-Zhou-Tygar 2005/2009; Berger-Wool-Yeredor 2006), timing attacks (Song 2001; Zhang-Wang 2009), the deep-learning turn (Harrison-Toreini-Mehrnezhad 2023, CoAtNet), and the 2025 LLM-as-language-model SOTA (Ayati et al., USENIX WOOT '25), where an LLM plays exactly the role the n-gram LM played in 2005. Most attack results are lab-calibrated; treat headline accuracies as upper bounds.

---

## Key Findings

1. **The ASR analogy is not a metaphor — it is the actual architecture.** Automatic speech recognition decomposes recognition as argmax over word sequences of P(acoustics | words) · P(words) — an acoustic model times a language model, searched by a Viterbi/beam decoder. Every serious keystroke-inference paper since 2001 instantiates this same product: a physical-observation model (timing Gaussians, cepstral/FFT features, or a CNN over spectrograms) times a prior over text (n-gram, dictionary, or LLM), decoded by Viterbi/beam/search-and-prune.

2. **Classical solution = HMM + n-gram/dictionary LM.** Song 2001 (timing) and Zhuang 2005/2009 (acoustic) are the canonical instances; the latter explicitly borrows cepstrum features, HMMs, and unsupervised EM-style bootstrapping straight from speech recognition, "recovering up to 96% of typed characters" with no labeled training data.

3. **Modern solution = deep sequence classifier + LLM prior.** The 2023 CoAtNet attack replaced hand-built acoustic models with a CNN-transformer hybrid on mel-spectrograms; the 2025 WOOT paper replaced the n-gram LM with a fine-tuned LLM doing "typo correction," restoring accuracy under noise. This is the same pipeline with each block upgraded.

4. **HMMs also appear in power/EM analysis** — notably for defeating random-delay countermeasures via Viterbi decoding and for modeling randomized countermeasures as HMMs — so the module's HMM content transfers beyond keystrokes.

5. **Calibration matters.** Almost every headline number (96% characters; factor-50 password speedup; 95%/93% CoAtNet; BLEU 0.07→0.89) comes from controlled lab conditions — a single keyboard, a quiet room, or synthetic Gaussian noise. Real-world ambient noise, cross-keyboard/typist transfer, and modern network defenses substantially degrade them.

---

## Details

### PART A — HMM and NLP / Sequence-Modeling Foundations

#### A1. The canonical HMM tutorial (START HERE)
- **Lawrence R. Rabiner, "A Tutorial on Hidden Markov Models and Selected Applications in Speech Recognition," *Proceedings of the IEEE*, vol. 77, no. 2, pp. 257–286, February 1989. DOI: 10.1109/5.18626.**
  - *Role:* THE reference. Defines the "three problems" of an HMM and their solutions: (1) likelihood via the **Forward-Backward** algorithm; (2) best state sequence via **Viterbi**; (3) parameter learning via **Baum-Welch** (an EM instance). Introduces the doubly-embedded stochastic process view and LPC/cepstral features. As the Wharton course notes observe, the "plain-vanilla situation is well covered by the first ten pages."
  - *Why it matters for the course:* The speech-recognition framing is directly analogous to acoustic keystroke attacks; read §I–III before any Part B paper.
  - *FREE:* Widely available as PDF via university mirrors; the IEEE version is paywalled. Errata are maintained online (Rahimi's errata page).

#### A2. The three core algorithms (primary sources)
- **Andrew J. Viterbi, "Error Bounds for Convolutional Codes and an Asymptotically Optimum Decoding Algorithm," *IEEE Transactions on Information Theory*, vol. 13, no. 2, pp. 260–269, April 1967. DOI: 10.1109/TIT.1967.1054010.**
  - *Role:* Origin of the **Viterbi algorithm** — dynamic-programming max-probability path decoding. Song 2001's "n-Viterbi" is a direct descendant. FREE PDF via the WUSTL mirror (essrl.wustl.edu/~jao/itrg/viterbi.pdf). Calibration: the paper is framed in coding theory; the DP recursion is what carries over (Forney's 1973 *Proc. IEEE* exposition is the readable bridge).
- **Leonard E. Baum, Ted Petrie, George Soules, Norman Weiss, "A Maximization Technique Occurring in the Statistical Analysis of Probabilistic Functions of Markov Chains," *The Annals of Mathematical Statistics*, vol. 41, no. 1, pp. 164–171, 1970. DOI: 10.1214/aoms/1177697196.**
  - *Role:* The **Baum-Welch** parameter-estimation result (EM for HMMs). FREE via Project Euclid. Prereq context: Baum & Petrie 1966 (same journal, 37:1554–1563) introduce the statistical-inference framing.
- **Forward-Backward:** best learned from Rabiner §III and Jurafsky-Martin Appendix A rather than a single origin paper; it is the E-step of Baum-Welch. A useful free companion is Jeff Bilmes, "A Gentle Tutorial of the EM Algorithm and its Application to Parameter Estimation for Gaussian Mixture and Hidden Markov Models" (ICSI-TR-97-021, 1997).

#### A3. Modern textbook treatments (chapters)
- **Daniel Jurafsky & James H. Martin, *Speech and Language Processing*, 3rd ed. draft — FREE at web.stanford.edu/~jurafsky/slp3/.** Cite as: "Online manuscript released January 6, 2026." Key units for this module:
  - **Appendix A, "Hidden Markov Models"** (the ice-cream/weather example; Forward, Viterbi, Forward-Backward) — free PDF `A.pdf`.
  - **N-gram Language Models** chapter (probabilities, perplexity, smoothing).
  - **"Spelling Correction and the Noisy Channel"** (older-draft `B.pdf`) — argmax P(word)·P(typo|word), the exact Bayesian structure reused in acoustic attacks.
  - **Sequence Labeling** (HMM/CRF POS-tagging) and the ASR/CTC chapter.
  - *Why:* Your single best free source for the "acoustic model + language model + decoder" structure and how it maps onto side-channel decoding.
- **Christopher M. Bishop, *Pattern Recognition and Machine Learning*, Springer, 2006 — Chapter 13, "Sequential Data"** (Markov models, HMMs, forward-backward as sum-product, linear dynamical systems). Bishop released a free authorized PDF via microsoft.com. Rigorous graphical-model treatment.
- **Kevin P. Murphy, *Machine Learning: A Probabilistic Perspective*, MIT Press, 2012 (HMM ch. 17, state-space ch. 18); and *Probabilistic Machine Learning: An Introduction / Advanced Topics*, MIT Press, 2022/2023 — FREE at probml.github.io.** The newer books are free and cover HMMs and inference with modern notation.

#### A4. Statistical / n-gram language models — decoding & error correction
- **Claude E. Shannon, "Prediction and Entropy of Printed English," *Bell System Technical Journal*, 30:50–64, 1951.** Shannon obtained an estimate of the entropy of English as **between 0.6 and 1.3 bits per letter** (his cognitive experiment yielded h≈1.3 bpc at context length n=100). This figure quantifies *why* language priors make text recoverable; Song 2001 explicitly compares its per-keystroke-pair timing leakage against Shannon's entropy of English. FREE via Princeton mirror / Internet Archive.
- **Mark D. Kernighan, Kenneth W. Church, William A. Gale, "A Spelling Correction Program Based on a Noisy Channel Model," COLING 1990, vol. 2. FREE at ACL Anthology (C90-2036).** The canonical noisy-channel spelling corrector; its confusion-matrix EM re-estimation is a template for unsupervised acoustic-class→character mapping (and is itself presented in SLP3's noisy-channel chapter as an EM instance).
- **Stanley F. Chen & Joshua Goodman, "An Empirical Study of Smoothing Techniques for Language Modeling," Harvard TR-10-98, 1998 (and *Computer Speech & Language* 13(4):359–394, 1999).** The definitive smoothing study; **Kneser-Ney** emerges as best. Explains why smoothing/back-off matters when priors meet unseen n-grams.
- *Decoding structure:* ASR = acoustic model P(O|W) × language model P(W), searched by Viterbi or **beam search**; Jurafsky-Martin is the free primary text. This maps onto side channels as: observation model (timing/acoustic/EM) × text prior, searched by Viterbi/beam/search-and-prune.

#### A5. The successors to HMMs (foundational papers for modern SOTA attacks)
- **Alex Graves, Santiago Fernández, Faustino Gomez, Jürgen Schmidhuber, "Connectionist Temporal Classification: Labelling Unsegmented Sequence Data with Recurrent Neural Networks," ICML 2006, pp. 369–376.** CTC removes the need for pre-segmented alignment — directly relevant to segmenting continuous typing audio, and (per Graves' 2012 monograph, ch. 7) it "does not require the network to be combined with a hidden Markov model." FREE (cs.toronto.edu/~graves/icml_2006.pdf).
- **Ilya Sutskever, Oriol Vinyals, Quoc V. Le, "Sequence to Sequence Learning with Neural Networks," NIPS 2014, pp. 3104–3112.** Encoder-decoder seq2seq. FREE (arXiv:1409.3215).
- **Dzmitry Bahdanau, Kyunghyun Cho, Yoshua Bengio, "Neural Machine Translation by Jointly Learning to Align and Translate," ICLR 2015.** Introduces (soft) **attention**. FREE (arXiv:1409.0473). Cho et al. 2014 (RNN encoder-decoder, EMNLP) is the companion.
- **Ashish Vaswani et al., "Attention Is All You Need," NIPS 2017, pp. 5998–6008.** The **Transformer** — backbone of every modern LLM used as a decoder/prior. FREE (arXiv:1706.03762; NeurIPS proceedings).
- *Through-line:* HMMs, CTC, seq2seq+attention, and Transformers are successive answers to the same sequence-transduction problem. Modern attacks use LLMs (Transformer decoders) as the language-model prior, exactly where 2005-era work used n-grams.

### PART B — HMMs and Sequence Models Inside Side-Channel / Keystroke Attacks

#### B1. TIMING side channels with HMMs (the anchor)
- **Dawn Xiaodong Song, David Wagner, Xuqing Tian, "Timing Analysis of Keystrokes and Timing Attacks on SSH," 10th USENIX Security Symposium, 2001. FREE at usenix.org and people.eecs.berkeley.edu/~daw/papers/ssh-use01.pdf.**
  - *Method:* SSH in interactive mode sends each keystroke in its own packet immediately, leaking exact inter-keystroke timings. They model the latency of each character pair as a **Gaussian** N(μ,σ), build a **Hidden Markov Model** whose hidden states are character pairs, and develop an **n-Viterbi algorithm** to infer the most likely key sequence from the observed latency sequence. They build **Herbivore**, an attacker system that monitors SSH and predicts passwords.
  - *Reported results (verbatim):* "Estimated information gain available from latency information is about **1.2 bits per characteristic pair** — significant compared to the 0.6–1.3 bits per character entropy of written English"; and "for passwords that are chosen uniformly at random with length of 7 to 8 characters, Herbivore can **reduce the cost of password cracking by a factor of 50** and hence speed up exhaustive search dramatically." Their character-pair prediction reaches ~90% success when the correct pair is among the top n≈70 candidates.
  - *Role in learning sequence:* THE primary source for HMMs in side channels — read immediately after Rabiner §I–III and the Viterbi 1967 paper. Calibration: strong assumptions (independent Gaussian per pair; random-password typing; SSH's now-largely-mitigated per-keystroke packetization).

#### B2. Follow-on timing attacks using HMMs / Markov / n-gram priors
- **Kehuan Zhang, XiaoFeng Wang, "Peeping Tom in the Neighborhood: Keystroke Eavesdropping on Multi-User Systems," 18th USENIX Security Symposium, 2009, pp. 17–32. FREE at usenix.org.**
  - *Method:* A local unprivileged "shadow" program samples a victim process's stack pointer (ESP) via Linux **procfs** on a multi-core system to detect keystroke events and recover precise inter-keystroke timings — then applies Song-style timing/HMM inference to infer typed characters. Extends Song 2001 from the network to the local multi-user setting.
  - *Role:* Shows the timing-HMM template generalizes across channels; good second timing paper. Calibration: depends on procfs stack disclosure (since hardened in Linux).

#### B3. ACOUSTIC keyboard attacks with HMMs + language models (the core linkage)
- **Dmitri Asonov, Rakesh Agrawal, "Keyboard Acoustic Emanations," IEEE S&P 2004, pp. 3–11. DOI: 10.1109/SECPRI.2004.1301311.** The founding acoustic attack: FFT features + a **neural network** classifier, but it requires *labeled* training (a "known-plaintext" analogue) and gets ~79% top-1 / ~88% top-3; cross-keyboard transfer drops to ~25%. FREE via university mirrors. Read first for context.
- **Li Zhuang, Feng Zhou, J. D. Tygar, "Keyboard Acoustic Emanations Revisited," ACM CCS 2005; extended in *ACM TISSEC* 13(1), Article 3, October 2009. DOI: 10.1145/1609956.1609959. FREE (berkeley.edu, cornell.edu mirrors).**
  - *Method (the ASR pipeline, explicitly):* (1) extract **cepstrum** features per keystroke (they show cepstrum beats FFT and linear classification beats NN); (2) **unsupervised clustering** into acoustic classes; (3) an **HMM with a language model** (letter/word n-gram English constraints) recovers the class→character mapping — analogous to cryptanalysis of a substitution cipher; (4) **feedback-based incremental / EM-style bootstrapping** plus a spelling/grammar-correction pass refines the recognizer. No labeled training data needed.
  - *Reported results (verbatim):* "recovering up to **96% of typed characters**" and a 75–90% word accuracy rate; a bootstrapped recognizer then reads random text/passwords at ~90% character accuracy; "**90% of 5-character random passwords using only letters can be generated in fewer than 20 attempts** by an adversary; **80% of 10-character passwords can be generated in fewer than 75 attempts**."
  - *Role:* THE keystone Part B paper — the clearest instance of "keystroke inference = speech recognition." The authors explicitly note the framework extends to power/EM emanations. Calibration: single quiet environment; the English-text prior does heavy lifting (random passwords rely on the bootstrapped acoustic model only).
- **Yigael Berger, Avishai Wool, Arie Yeredor, "Dictionary Attacks Using Keyboard Acoustic Emanations," ACM CCS 2006, pp. 245–254. DOI: 10.1145/1180405.1180436.**
  - *Method:* A **dictionary/constraint-based** (language-model-like) reconstruction combining cross-correlation of key-press sounds (keys physically close on the keyboard have higher cross-correlation) with a **dictionary constraint** and edit-distance-style matching to reconstruct single words. Requires **no training** and works on a single ~5-second recording of one word (~20 seconds/word on a standard PC).
  - *Reported results (verbatim):* "a **90% or better success rate of finding the correct word in the top 50 candidates** identified by the attack, for words of 10 or more characters, and a **success rate of 73% over all the words** we tested."
  - *Role:* Shows the "language model" can be as simple as a lexicon + constraints; contrast with Zhuang's HMM. Calibration: single-word, dictionary-word only (fails on random passwords by design).

#### B4. MODERN acoustic SOTA — deep sequence models replace the HMM, LLMs replace the n-gram
- **Joshua Harrison, Ehsan Toreini, Maryam Mehrnezhad, "A Practical Deep Learning-Based Acoustic Side Channel Attack on Keyboards," IEEE EuroS&PW 2023, pp. 270–280.**
  - *Method:* Mel-spectrogram images of keystrokes classified by **CoAtNet** (a CNN + self-attention hybrid), replacing the hand-crafted acoustic model of 2005 with a learned deep classifier. Dataset: MacBook Pro 16" (2021), 36 keys, 25 samples/key.
  - *Reported results (verbatim):* "the classifier achieved an accuracy of **95%**, the highest accuracy seen without the use of a language model. When trained on keystrokes recorded using the video-conferencing software Zoom, an accuracy of **93%** was achieved, a new best for the medium." FREE dataset/code (github.com/JBFH-Dev/Keystroke-Datasets).
  - *Calibration:* clean recordings; per-key classification, not full-sentence decoding; accuracy collapses (often <40%) under noise — the gap the 2025 paper targets.
- **Seyyed Ali Ayati, Jin Hyun Park, Yichen Cai, Marcus Botacin, "Making Acoustic Side-Channel Attacks on Noisy Keyboards Viable with LLM-Assisted Spectrograms' 'Typo' Correction," 19th USENIX WOOT Conference on Offensive Technologies (WOOT '25), 2025. arXiv:2504.11622; ACM DL handle 10.5555/3769714.3769720. Authors at Texas A&M (Ayati, Park, Botacin) and Toronto (Cai). FREE (arXiv; code at github.com/Botacin-s-Lab/EchoCrypt; weights on Hugging Face).**
  - *Method (LLM = the language model):* Two complementary upgrades — (1) **Vision Transformers** (ViT/Swin/BEiT) classify keystroke spectrograms; (2) an **LLM performs contextual "typo" correction** on the noisy predicted text, exactly the role the n-gram/HMM language model played in Zhuang 2005. They test GPT-4o and LLaMA-3.2 (1B/3B/8B), fine-tuning LLaMA-3.2-3B with **LoRA/QLoRA** on a progressive noise curriculum (one epoch each at low, medium, high synthetic noise).
  - *Reported results:* Their CoAtNet re-implementation reaches ~96.5% (Phone) / 96.7% (Zoom) *mean* accuracy, and the best VTs hit up to 100% *max* accuracy on Phone (a claimed +5.0% Phone / +5.9% Zoom absolute over the CoAtNet baseline). The headline is the noise-robustness gain from LLM correction: on the 1,000-sentence EnglishTense set, the pipeline "increases BLEU metric **from 0.07 to 0.89**, and adds **18–26% accuracy** due to LLM contextual correction, while maintaining an inference latency of **~120 ms per key**"; text-recovery accuracy rises from ~50% to >90% in noisy conditions. Efficiency claim (verbatim): "Our proposed fine-tuned LLM (Llama-3.2-3B), via Low-Rank Adaptation (LoRA), achieves accuracy scores closely comparable to GPT-4o (**98-99% of it) while being 67x smaller**."
  - *Role:* The explicit modern realization of the through-line; read last. Calibration: **noise is synthetic Gaussian, not real ambient noise** (authors' acknowledged limitation); the GPT-4o "~200B params" (basis of the 67× claim) is the authors' estimate; the VT "SOTA" claim rests on maximum, not mean, accuracy (Zoom VT std devs up to ~48% under one transformation).
- **Related modern context (2024–2026):** the field is extending to other physical channels with LLM/DL decoders — e.g., RF-backscatter through-wall keystroke inference ("RadKey," arXiv:2606.10148), VR/AR keylogging from head/controller motion (USENIX Security 2023; NDSS 2024), and speech-representation-learning models applied to ASCA (arXiv:2606.21210). These confirm the "deep classifier + LLM prior" pattern is now standard.

#### B5. HMMs / sequence models in POWER / EM side-channel analysis
- **François Durvaux, Mathieu Renauld, François-Xavier Standaert, et al., "Efficient Removal of Random Delays from Embedded Software Implementations Using Hidden Markov Models," CARDIS 2012, LNCS 7771, pp. 123–140.** Models a device executing instructions (with random-delay countermeasures) as an HMM whose observable is physical leakage, then uses **Viterbi decoding** + pattern recognition to strip the delays and recover the AES key "with the same data complexity as against an unprotected implementation." The clearest power-SCA analogue of Song's HMM decoder.
- **CHES-2003-era "HMM attacks"** modeled randomized side-channel countermeasures as HMMs and applied maximum-likelihood/template methods; and **Input-Driven HMMs (IDHMM)** have been used to attack square-and-multiply exponentiation from leaked square/multiply sequences (see the Oxford Nuffield report and the search-and-prune RSA sliding-window analysis, e.g., the leakage-modeling discussion in arXiv:1709.09699). *Role:* Shows the HMM machinery transfers from keystrokes to cryptographic-hardware leakage; include as an "HMMs beyond keystrokes" reading. Calibration: mostly profiled / known-implementation settings.

---

## Recommendations

**Staged reading path (free-first ordering):**

1. **Foundations week (all free):** Rabiner 1989 §I–III → Viterbi 1967 (skim the DP recursion) → Baum-Petrie-Soules-Weiss 1970 (skim) → Jurafsky-Martin *SLP3* Appendix A (HMM) + N-gram + Noisy-Channel chapters. **Deliverable:** implement Forward, Viterbi, and Baum-Welch on the SLP3 ice-cream HMM in pure Python (no libraries).

2. **Classical attacks week (all free):** Song-Wagner-Tian 2001 → Zhuang-Zhou-Tygar 2009 (TISSEC full version) → Berger-Wool-Yeredor 2006 → Asonov-Agrawal 2004 for context. **Deliverable:** reproduce a *timing* HMM on synthetic inter-keystroke data (Gaussian per key-pair + n-Viterbi), then add a bigram English prior and measure the lift — this literally rebuilds Herbivore in miniature and demonstrates the acoustic-model × language-model product.

3. **Modern successors week (all free):** CTC 2006 → seq2seq 2014 → attention 2015 → Transformer 2017. **Deliverable:** a small CTC or seq2seq decoder over the Harrison keystroke dataset.

4. **Modern SOTA / capstone (all free):** Harrison-Toreini-Mehrnezhad 2023 → Ayati et al. WOOT '25, then clone the **EchoCrypt** repo and reproduce the LLM typo-correction lift (BLEU under injected noise). **Deliverable:** swap the fine-tuned LLaMA prior for a plain n-gram prior and quantify how much of the 2025 gain is "just a better language model" — the clearest empirical demonstration of the through-line.

5. **Optional extension:** Durvaux et al. 2012 to watch the same Viterbi/HMM decoder defeat a power-analysis countermeasure.

**Thresholds that should change your emphasis:**
- If the learner cares about *current operational risk*, weight B4 (deep + LLM) heavily and treat B1–B3 as historical grounding.
- If the goal is *rigorous mechanism understanding*, invest most in the Part A implementations; the attacks then become straightforward applications.
- If reproduction hardware/time is limited, prefer the FREE public datasets (Harrison Keystroke-Datasets; EchoCrypt) over collecting your own audio, which removes the hardest calibration variable.

## Caveats
- **Lab vs. field gap:** Nearly all headline metrics (96% chars, factor-50 password speedup, 95%/93% CoAtNet, BLEU 0.07→0.89) are from controlled conditions. Real ambient noise, unknown keyboards/typists, VoIP codec compression, and modern countermeasures (SSH timing padding/traffic shaping, procfs hardening) degrade them, sometimes drastically.
- **The language-model prior does much of the work:** high character/word accuracies on *English text* partly reflect the strength of the LM; *random passwords* rely on the raw observation model and are markedly harder (evident in Zhuang's password numbers and Berger's dictionary-only scope, which explicitly cannot handle random strings).
- **Source-quality notes:** Rabiner, Song, Zhuang (TISSEC), Berger, Harrison, Durvaux, and the foundational algorithm/NLP papers are peer-reviewed primary sources. The Ayati 2025 paper is peer-reviewed (WOOT '25) but relies on synthetic Gaussian noise and an estimated GPT-4o parameter count; its VT-"SOTA" claim rests on maximum (not mean) accuracy with high variance. Springer/IEEE versions of several papers are paywalled, but author or university PDFs are free for essentially all Part A and Part B items listed.
- **Exact page numbers** for the WOOT '25 paper were not confirmed from a primary listing (ACM DL handle 10.5555/3769714.3769720; a USENIX presentation page exists).