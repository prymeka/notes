# A one-week audio ML reading list for the physics-minded engineer

**Start with mel-spectrograms, end with transformers—here's the fastest path from signal processing fundamentals to modern audio embeddings for sound recognition.**

For ML engineers with mathematical foundations already in place, audio ML presents a unique challenge: the field sits at the intersection of digital signal processing, psychoacoustics, and deep learning, with terminology and conventions inherited from all three. This reading list provides a curated 30-35 hour curriculum designed to build practical competence in **seven days**, prioritizing hands-on understanding over exhaustive theory.

The reading order follows a deliberate progression: **representations → features → pretrained models → research literature**. Each section builds on the previous, so a spectrogram becomes intuitive before you extract MFCCs, and MFCCs make sense before you understand why modern models learn their own features.

---

## Day 1: Why audio becomes images (3-4 hours)

The fundamental insight of modern audio ML is treating spectrograms as images—but understanding *why* this works requires grasping what information spectrograms preserve and discard.

**Primary reading:**

| Resource | Time | Focus |
|----------|------|-------|
| [Audio Deep Learning Made Simple: Part 1](https://towardsdatascience.com/audio-deep-learning-made-simple-part-1-state-of-the-art-techniques-da1d3dff2504/) | 20 min | Why convert audio to spectrograms for deep learning |
| [Audio Deep Learning Made Simple: Part 2 - Mel Spectrograms](https://towardsdatascience.com/audio-deep-learning-made-simple-part-2-why-mel-spectrograms-perform-better-aad889a93505/) | 25 min | Mel scale, decibel scale, perceptual basis |
| [Hugging Face Audio Course: Chapter 1](https://huggingface.co/learn/audio-course/en/chapter1/audio_data) | 60 min | Sampling, Nyquist, waveform → spectrum → spectrogram progression |
| [Understanding the Mel Spectrogram](https://medium.com/analytics-vidhya/understanding-the-mel-spectrogram-fca2afa2ce53) | 15 min | Quick reference on mel filterbanks |

**Key concepts to internalize:**
- Why CNNs work on spectrograms (2D time-frequency representation preserves relevant structure)
- The mel scale compresses high frequencies because human hearing is logarithmic—**this is why mel-spectrograms outperform linear spectrograms** for most tasks
- Critical practical note: different libraries compute mel-spectrograms differently (HTK vs Slaney formulas). When using pretrained models, matching their preprocessing exactly is essential.

**Supplementary (if time permits):**
[Brian McFee's Digital Signals Theory - Chapter 2](https://brianmcfee.net/dstbook-site/content/ch02-sampling/Nyquist.html) provides a rigorous but intuitive treatment of sampling theory, written by librosa's creator—ideal for someone who appreciates mathematical precision.

---

## Day 2: STFT parameters and feature extraction theory (4-5 hours)

With the "why" established, Day 2 focuses on the mechanical details that determine spectrogram quality: window functions, hop length, and the time-frequency resolution tradeoff.

**Primary reading:**

| Resource | Time | Focus |
|----------|------|-------|
| [Source Separation Tutorial: Audio Representations](https://source-separation.github.io/tutorial/basics/representations.html) | 45 min | STFT parameters visualized, trade-offs explained |
| [Audio Deep Learning Made Simple: Part 3](https://towardsdatascience.com/audio-deep-learning-made-simple-part-3-data-preparation-and-augmentation-24c6e1f6b52/) | 25 min | Hyperparameter tuning (n_fft, hop_length, n_mels), SpecAugment |
| [Haytham Fayek: Speech Processing for ML](https://haythamfayek.com/2016/04/21/speech-processing-for-machine-learning.html) | 45 min | MFCCs from first principles: framing → windowing → FFT → mel filterbanks → DCT |

**Key concepts to internalize:**
- **n_fft** (window size) controls frequency resolution; **hop_length** controls time resolution. You cannot maximize both simultaneously.
- MFCCs apply DCT to decorrelate mel filterbank energies—useful for traditional ML but **often inferior to raw mel-spectrograms for deep learning** because CNNs can learn decorrelation.
- The distinction between power spectrograms, log-mel spectrograms, and MFCCs matters for matching pretrained model expectations.

**Why Haytham Fayek's post matters:** This is the most-cited tutorial for understanding MFCCs from scratch. It's referenced by PyTorch's documentation and clarifies when filter banks outperform MFCCs (spoiler: usually with deep learning).

---

## Day 3: Hands-on feature extraction with librosa and torchaudio (4-5 hours)

Theory becomes practical. Day 3 is code-focused, building muscle memory for the two dominant audio libraries.

**Primary tutorials:**

| Resource | Time | Focus |
|----------|------|-------|
| [Librosa Official Tutorial](https://librosa.org/doc/latest/tutorial.html) | 45 min | MFCCs, chromagrams, beat synchronization, harmonic-percussive separation |
| [TorchAudio Feature Extraction Tutorial](https://pytorch.org/audio/stable/tutorials/audio_feature_extractions_tutorial.html) | 60 min | GPU-accelerated spectrograms, MFCCs, comparison with librosa |
| [The Sound of AI GitHub Repository](https://github.com/musikalkemist/AudioSignalProcessingForML) | 2-3 hrs | Work through notebooks on spectrogram extraction and MFCC implementation |

**Recommended workflow:**
1. Start with librosa's quickstart—it's the most intuitive API
2. Run the torchaudio tutorial in parallel to see equivalent operations
3. Clone The Sound of AI repo and run the spectrogram/MFCC notebooks

**Library choice guidance:**
- **librosa**: Best for research and prototyping. NumPy-based, extensive documentation, standard in academic work.
- **torchaudio**: Best for production PyTorch pipelines. GPU acceleration, TorchScript serialization, native integration with PyTorch models.
- **For sound recognition work**, torchaudio is often preferable because features can be computed on GPU as part of the training loop.

---

## Day 4: Benchmark datasets and foundational papers (3-4 hours)

Before diving into models, understanding the datasets that define the field provides essential context for interpreting results.

**Papers to read:**

| Paper | Year | Reading Time | Why Essential |
|-------|------|--------------|---------------|
| [ESC: Dataset for Environmental Sound Classification](https://www.karolpiczak.com/papers/Piczak2015-ESC-Dataset.pdf) | 2015 | 30 min | Defines ESC-50, the standard benchmark. Human accuracy is **81.3%**—models now exceed 98% |
| [AudioSet: An Ontology and Human-Labeled Dataset](https://research.google.com/pubs/archive/45857.pdf) | 2017 | 45 min | The ImageNet of audio. **2M+ clips, 632 classes**. Nearly all modern audio models benchmark here |
| [CNN Architectures for Large-Scale Audio Classification](https://arxiv.org/abs/1609.09430) | 2017 | 45 min | Introduced VGGish. Proved CNNs transfer from images to audio spectrograms |

**Key takeaways:**
- **ESC-50** (50 classes, 2000 clips) is your go-to for quick experiments and sanity checks
- **AudioSet** (632 classes, 2M clips) is the pretraining dataset for most modern models
- The VGGish paper established that image classification architectures work remarkably well on log-mel spectrograms—a non-obvious result that enabled the field's rapid progress

**Supplementary datasets to know:**
- **UrbanSound8K**: 8732 urban sound clips, 10 classes. Good for practical applications.
- **FSD50K**: Freesound-derived, openly licensed, cleaner labels than AudioSet

---

## Day 5: Pretrained audio embeddings (5-6 hours)

This is the highest-leverage day for a practicing ML engineer. Modern audio ML is dominated by transfer learning from large pretrained models.

**Papers to read in order:**

| Paper | Year | Time | Key Contribution |
|-------|------|------|------------------|
| [PANNs: Large-Scale Pretrained Audio Neural Networks](https://arxiv.org/abs/1912.10211) | 2020 | 60 min | **The practical workhorse**. CNN14 achieves 0.431 mAP on AudioSet. Released weights are the most widely-used transfer learning starting point |
| [AST: Audio Spectrogram Transformer](https://arxiv.org/abs/2104.01778) | 2021 | 45 min | First pure-attention audio model. **0.485 mAP** on AudioSet. Proved Vision Transformers transfer to audio |
| [BEATs: Audio Pre-Training with Acoustic Tokenizers](https://arxiv.org/abs/2212.09058) | 2023 | 60 min | **Current SOTA**: 0.506 mAP on AudioSet, 98.1% on ESC-50. Self-supervised with discrete tokenization |

**Practical guides to work through:**

| Resource | Time | Focus |
|----------|------|-------|
| [TensorFlow YAMNet Transfer Learning Tutorial](https://www.tensorflow.org/tutorials/audio/transfer_learning_audio) | 90 min | End-to-end: load YAMNet → extract embeddings → train custom classifier |
| [Hugging Face Audio Classification (Wav2Vec2)](https://huggingface.co/docs/transformers/tasks/audio_classification) | 60 min | Modern transformer workflow with Trainer API |

**Model selection guidance for sound recognition:**

| Use Case | Recommended Model | Why |
|----------|-------------------|-----|
| General sound events | **PANNs CNN14** | Best balance of performance, ease of use, and documentation |
| State-of-the-art results | **BEATs** | Highest AudioSet mAP, but heavier compute |
| Edge/mobile deployment | **YAMNet** | Only 3.7M parameters (1/20th of VGGish) |
| Zero-shot classification | **CLAP** | Text-audio joint embedding enables natural language queries |
| Quick baseline | **VGGish** | Simplest to set up, adequate for many tasks |

---

## Day 6: Advanced models and multimodal approaches (4-5 hours)

With CNN and transformer-based models understood, Day 6 covers specialized architectures and the emerging multimodal paradigm.

**Papers to read:**

| Paper | Year | Time | Focus |
|-------|------|------|-------|
| [HTS-AT: Hierarchical Token-Semantic Audio Transformer](https://arxiv.org/abs/2202.00874) | 2022 | 45 min | Efficient transformer (35% of AST's parameters), enables temporal localization |
| [CLAP: Learning Audio Concepts from Natural Language](https://arxiv.org/abs/2206.04769) | 2023 | 45 min | CLIP for audio. **90%+ zero-shot ESC-50** without any labeled audio training |
| [wav2vec 2.0](https://arxiv.org/abs/2006.11477) | 2020 | 45 min | Self-supervised from raw waveforms. Primarily speech-focused but architecturally influential |

**Key insight on CLAP:** For sound recognition applications, CLAP's zero-shot capability is transformative. Instead of collecting and labeling data for each new sound class, you can query the model with natural language descriptions. The LAION-CLAP variant trained on 630K audio-text pairs achieves competitive results without task-specific fine-tuning.

**GitHub repositories to explore:**

| Repository | Stars | Use |
|------------|-------|-----|
| [PANNs](https://github.com/qiuqiangkong/audioset_tagging_cnn) | 2.5k+ | Pretrained CNN14, inference scripts |
| [AST](https://github.com/YuanGongND/ast) | 1k+ | Audio Spectrogram Transformer weights |
| [BEATs](https://github.com/microsoft/unilm/tree/master/beats) | Part of UniLM | Current SOTA weights |
| [LAION-CLAP](https://github.com/LAION-AI/CLAP) | 1k+ | Zero-shot audio classification |

---

## Day 7: Sound event detection and integration (4-5 hours)

The final day shifts from classification (what sounds are present?) to detection (when do they occur?)—a critical capability for real-world sound recognition systems.

**Papers and resources:**

| Resource | Time | Focus |
|----------|------|-------|
| [Sound Event Detection: A Journey Through DCASE](https://www.nowpublishers.com/article/Details/SIP-090) | 60 min | Comprehensive survey of SED evolution 2013-2023 |
| [DCASE 2024 Task 4 Overview](https://arxiv.org/abs/2406.08056) | 45 min | Current state of the art: CRNN+BEATs baselines, soft labels |
| [sklearn-audio-transfer-learning](https://github.com/jordipons/sklearn-audio-transfer-learning) | 90 min | Practical: VGGish/OpenL3 embeddings + sklearn classifiers |

**End-to-end project (consolidation):**

| Resource | Time | Focus |
|----------|------|-------|
| [Audio Deep Learning Made Simple: Part 4](https://towardsdatascience.com/audio-deep-learning-made-simple-sound-classification-step-by-step-cebc936bbe5/) | 60 min | Complete CNN classification pipeline |
| [Neuromatch Academy: Spectrogram Classification](https://deeplearning.neuromatch.io/projects/ComputerVision/spectrogram_analysis.html) | 90 min | Hands-on notebook: GTZAN genre classification |

---

## Quick reference: The complete reading list

### Foundational tutorials (Days 1-3)
1. Audio Deep Learning Made Simple series, Parts 1-3
2. Hugging Face Audio Course, Chapter 1
3. Source Separation Tutorial: Audio Representations
4. Haytham Fayek: Speech Processing for ML
5. Librosa Official Tutorial
6. TorchAudio Feature Extraction Tutorial
7. The Sound of AI notebooks (selective)

### Essential papers (Days 4-6)
1. ESC-50 Dataset Paper (Piczak, 2015)
2. AudioSet Paper (Gemmeke et al., 2017)
3. CNN Architectures for Audio (Hershey et al., 2017)
4. PANNs (Kong et al., 2020)
5. AST (Gong et al., 2021)
6. BEATs (Chen et al., 2023)
7. HTS-AT (Chen et al., 2022)
8. CLAP (Elizalde et al., 2023)

### Practical integration (Day 7)
1. TensorFlow YAMNet Transfer Learning Tutorial
2. Hugging Face Audio Classification Guide
3. DCASE Survey or 2024 Task 4 Overview
4. sklearn-audio-transfer-learning repository

---

## What this curriculum deliberately excludes

This reading list optimizes for a working ML engineer's time. Intentionally omitted:

- **Deep DSP theory**: Filter design, z-transforms, convolution theorem proofs. Unnecessary for practical audio ML.
- **Speech-specific content**: ASR architectures, phoneme models, language modeling. The user specified non-speech sound recognition.
- **Music information retrieval**: Beat tracking, chord recognition, source separation. Tangential unless working on music specifically.
- **Audio generation**: WaveNet, diffusion models, neural vocoders. Different problem domain.

## After the week: Suggested next steps

With this foundation, you'll be equipped to:
1. **Fine-tune PANNs or AST** on your specific sound recognition task
2. **Evaluate CLAP** for zero-shot classification of new sound categories
3. **Participate in DCASE challenges** (annual sound event detection competitions)
4. **Read new audio ML papers** with full comprehension of architectural choices

For deeper exploration, [The Sound of AI YouTube channel](https://www.youtube.com/c/ValerioVel662) offers 20+ hours of video lectures covering everything from Fourier transforms to generative models, and the [ml-audio-start](https://github.com/drscotthawley/ml-audio-start) repository maintains a curated list of researchers, datasets, and emerging techniques to follow.