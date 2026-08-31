# Music Analysis ML Reading List
## Fingerprinting, Similarity Search, and Song Description

**Scope**: Audio fingerprinting (Shazam-style exact matching), fuzzy music similarity (embedding-based search), and automatic music description (genre, mood, tempo, instrumentation). Self-contained, ~35-40 hours over one week.

---

## Part 1: Audio Fingerprinting — Exact Match Recognition

The goal here is understanding how systems like Shazam identify a specific recording from a noisy audio snippet. This is **not** machine learning — it's algorithmic signal processing with hash-based retrieval.

### Day 1: The Shazam Algorithm (4-5 hours)

| Resource | Time | Focus |
|----------|------|-------|
| [An Industrial-Strength Audio Search Algorithm](https://www.ee.columbia.edu/~dpwe/papers/Wang03-shazam.pdf) (Wang, 2003) | 60 min | **The foundational paper**. Constellation maps, combinatorial hashing, time-frequency peak pairing |
| [How Does Shazam Work?](https://www.toptal.com/developers/algorithms/shazam-it-music-processing-fingerprinting-and-recognition) (Toptal) | 45 min | Accessible walkthrough with code intuition |
| [The Five-Second Fingerprint](https://towardsdatascience.com/the-five-second-fingerprint-inside-shazams-instant-song-id/) | 30 min | Modern explanation with visualizations |
| [I Built the Shazam Algorithm from Scratch](https://danztee.medium.com/i-built-the-shazam-algorithm-from-scratch-in-go-and-it-actually-works-041beb16258e) | 45 min | Implementation walkthrough (Go, but concepts transfer) |

**Key concepts**:
- **Spectrogram peak detection**: Extract local maxima in time-frequency space as "landmarks"
- **Anchor-target pairing**: Create fingerprints from pairs of peaks with relative timing
- **Combinatorial hashing**: Hash = (f1, f2, Δt) enables O(1) lookup
- **Histogram voting**: Matching fingerprints must align temporally — histogram of time offsets reveals true matches

**Why it works**: The algorithm is robust to noise because it only uses the strongest spectral peaks. Background noise adds random peaks, but the consistent peaks from the actual song produce a sharp histogram spike.

### Day 2: Chromaprint and Open-Source Alternatives (3-4 hours)

| Resource | Time | Focus |
|----------|------|-------|
| [How Does Chromaprint Work?](https://oxygene.sk/2011/01/how-does-chromaprint-work/) | 30 min | Chroma-based fingerprinting, learned filters via AdaBoost |
| [AcoustID Documentation](https://acoustid.org/chromaprint) | 20 min | API overview, integration patterns |
| [Chromaprint GitHub](https://github.com/acoustid/chromaprint) | 30 min | Source code, referenced papers |
| [Essentia Chromaprint Tutorial](https://essentia.upf.edu/tutorial_fingerprinting_chromaprint.html) | 45 min | Hands-on: fingerprint extraction, AcoustID queries |
| [Comparative Analysis of Fingerprinting Algorithms](https://www.ijcset.com/docs/IJCSET17-08-05-021.pdf) | 45 min | Chromaprint vs Echoprint vs Panako |

**Chromaprint differs from Shazam**:
- Uses **chroma features** (pitch class energy) instead of raw spectral peaks
- Applies **learned filters** (AdaBoost-selected Haar-like features on chroma)
- Produces compact **32-bit integers** per time window
- Designed for **full-track matching**, less robust to short noisy queries

**Practical note**: Chromaprint is the backbone of MusicBrainz Picard and powers open music identification. Good for duplicate detection and catalog management.

---

## Part 2: Music Similarity — Fuzzy Embedding-Based Search

Unlike fingerprinting (exact match), similarity search finds music that "sounds like" a query — different performances, covers, or stylistically similar tracks. This requires **learned representations**.

### Day 3: Music Embeddings Foundations (4-5 hours)

| Resource | Time | Focus |
|----------|------|-------|
| [CLMR: Contrastive Learning of Musical Representations](https://arxiv.org/abs/2103.09410) | 60 min | **Foundational paper**. SimCLR adapted for music, audio augmentations, self-supervised learning |
| [CLMR GitHub & Demo](https://github.com/Spijkervet/CLMR) | 45 min | Run pretrained model, understand training pipeline |
| [Contrastive Learning: A New Paradigm for Music?](https://medium.com/@juj_guinot/contrastive-learning-a-new-paradigm-for-machine-learning-in-music-ffcc17fb31ab) | 30 min | Intuitive explanation of contrastive learning for music |
| [MusCALL: Contrastive Audio-Language Learning for Music](https://www.turing.ac.uk/sites/default/files/2022-09/ismir_2022_camera_ready.pdf) | 45 min | Audio-text joint embeddings, zero-shot classification |

**Key insight**: Contrastive learning creates embeddings where **augmented versions of the same track are close**, while different tracks are far apart. This naturally captures musical similarity without explicit labels.

**CLMR augmentations** (music-specific):
- Pitch shift, time stretch
- Gaussian noise, gain variation
- High/low-pass filtering
- Random cropping

### Day 4: Cover Song Detection (4-5 hours)

Cover detection is the bridge between fingerprinting and similarity — finding different performances of the same composition despite changes in key, tempo, instrumentation, and arrangement.

| Resource | Time | Focus |
|----------|------|-------|
| [Audio Cover Song Identification using CNN](https://arxiv.org/abs/1712.00166) | 45 min | Cross-similarity matrices as CNN input |
| [Key-Invariant CNN for Cover Song ID](https://www.researchgate.net/publication/328245929_Key-Invariant_Convolutional_Neural_Network_Toward_Efficient_Cover_Song_Identification) | 45 min | Handling key transposition |
| [CoverHunter](https://arxiv.org/abs/2306.09025) | 60 min | **Current SOTA**: Conformer architecture, coarse-to-fine alignment |
| [Da-TACOS Dataset Paper](https://repositori.upf.edu/handle/10230/42771) | 30 min | Standard benchmark for cover detection |

**Why covers are hard**:
- Key changes shift all chroma features
- Tempo changes compress/stretch time
- Arrangement changes alter instrumentation
- Live versions add noise, crowd, variations

**Solution patterns**:
1. **Chroma-based**: Use pitch-class features (key-invariant with transposition)
2. **Cross-similarity matrices**: Compare two songs' feature sequences as 2D images
3. **Temporal pooling**: Aggregate over time to handle tempo variation
4. **Learned embeddings**: Train networks to map covers to similar vectors

---

## Part 3: Music-Specific Features and Libraries

### Day 5: Hands-On Feature Extraction (4-5 hours)

| Resource | Time | Focus |
|----------|------|-------|
| [Librosa Tutorial](https://librosa.org/doc/latest/tutorial.html) | 60 min | Beat tracking, harmonic-percussive separation, chroma, MFCCs |
| [Librosa Feature Documentation](https://librosa.org/doc/latest/feature.html) | 45 min | Reference for all extractable features |
| [Music Feature Extraction Guide](https://medium.com/@swilliam.productions/music-extraction-7eb352d92bff) | 30 min | Practical walkthrough with visualizations |
| [Audio Feature Extraction Deep Dive](https://rramnauth2220.github.io/blog/posts/code/200525-feature-extraction.html) | 60 min | Comprehensive: time-domain, frequency-domain, chroma, rhythm |

**Music-specific features** (beyond general audio):

| Feature | What it captures | Use case |
|---------|------------------|----------|
| **Chroma** | Pitch class energy (12 bins) | Harmony analysis, cover detection |
| **Tonnetz** | Tonal centroid (6D) | Key/chord relationships |
| **Tempogram** | Tempo over time | Rhythm analysis, beat tracking |
| **HPSS** | Harmonic vs percussive | Separate melody from drums |
| **Onset strength** | Note attack times | Beat/downbeat detection |

**Code pattern for music analysis**:
```python
import librosa

y, sr = librosa.load('song.mp3')
y_harm, y_perc = librosa.effects.hpss(y)  # Separate harmonic/percussive

# Rhythm features from percussive
tempo, beats = librosa.beat.beat_track(y=y_perc, sr=sr)

# Tonal features from harmonic
chroma = librosa.feature.chroma_cqt(y=y_harm, sr=sr)
tonnetz = librosa.feature.tonnetz(y=y_harm, sr=sr)

# Sync features to beats
beat_chroma = librosa.util.sync(chroma, beats, aggregate=np.median)
```

---

## Part 4: Automatic Music Tagging and Description

### Day 6: Genre, Mood, and Instrumentation Classification (5-6 hours)

| Resource | Time | Focus |
|----------|------|-------|
| [musicnn: Pre-trained CNNs for Music Tagging](https://arxiv.org/abs/1909.06654) | 45 min | **Practical starting point**. Musically-motivated architecture, pretrained weights |
| [musicnn GitHub](https://github.com/jordipons/musicnn) | 45 min | Out-of-box tagging, feature extraction, transfer learning |
| [Evaluation of CNN-based Music Tagging Models](https://arxiv.org/pdf/2006.00751) | 60 min | Comprehensive comparison: FCN, CRNN, sample-level, harmonic CNN |
| [Music Tagging with CNNs](https://towardsdatascience.com/music-tagging-using-convolutional-recurrent-neural-networks-e26a9856f9f5/) | 30 min | Practical overview of CNN vs CRNN for tagging |
| [sklearn-audio-transfer-learning](https://github.com/jordipons/sklearn-audio-transfer-learning) | 60 min | **Hands-on**: Use pretrained embeddings + simple classifiers |

**Architecture comparison**:

| Model | Input | Key feature | Best for |
|-------|-------|-------------|----------|
| **musicnn** | Mel-spectrogram | Musically-motivated filters (timbral + temporal branches) | General tagging |
| **Short-chunk CNN** | Mel-spectrogram | 3×3 filters on short segments | Robustness to perturbations |
| **Sample-level CNN** | Raw waveform | Learns filterbanks from scratch | End-to-end when data is plentiful |
| **Harmonic CNN** | Harmonic tensor | Pitch-invariant features | Tonal classification |

**Key datasets**:
- **MagnaTagATune**: 25k clips, 188 tags (instrument, genre, mood)
- **Million Song Dataset**: 1M tracks, metadata + audio features
- **MTG-Jamendo**: 55k tracks, 195 tags, Creative Commons licensed
- **GTZAN**: 1000 tracks, 10 genres — **use fault-filtered version**

### Day 7: Music Captioning and Language Models (4-5 hours)

| Resource | Time | Focus |
|----------|------|-------|
| [MusCaps: Generating Captions for Music](https://arxiv.org/abs/2104.11984) | 45 min | **First music captioning model**. Encoder-decoder with temporal attention |
| [LP-MusicCaps: LLM-Based Pseudo Captioning](https://arxiv.org/abs/2307.16372) | 45 min | Using GPT to generate training captions from tags |
| [LP-MusicCaps GitHub](https://github.com/seungheondoh/lp-music-caps) | 60 min | Run captioning model, understand tag-to-caption pipeline |
| [MU-LLaMA: Music Understanding LLM](https://arxiv.org/pdf/2308.11276) | 45 min | Question-answering about music content |

**Caption vs Tags**:
- **Tags**: Fixed vocabulary, multi-label classification ("rock", "guitar", "energetic")
- **Captions**: Free-form natural language ("An upbeat rock track featuring distorted electric guitar and driving drums")

**LP-MusicCaps pipeline**:
1. Extract tags from existing datasets (MagnaTagATune, Million Song Dataset)
2. Use LLM (GPT-3.5) to convert tags → natural language captions
3. Train encoder-decoder on (audio, caption) pairs
4. Fine-tune on human-written captions (MusicCaps) for quality

---

## Benchmark Datasets Reference

| Dataset | Size | Task | Notes |
|---------|------|------|-------|
| **MagnaTagATune** | 25,863 clips | Auto-tagging | 188 tags, 29s clips |
| **Million Song Dataset** | 1M tracks | Metadata prediction | Audio features only (no raw audio) |
| **GTZAN** | 1,000 tracks | Genre classification | 10 genres, **use fault-filtered split** |
| **MTG-Jamendo** | 55,000 tracks | Multi-label tagging | 195 tags, CC licensed |
| **MusicCaps** | 5,521 clips | Captioning | Human-written descriptions |
| **Da-TACOS** | 15,000+ tracks | Cover detection | Covers80, SHS100K subsets |
| **SecondHandSongs** | 12,000+ cliques | Cover detection | Real-world cover relationships |
| **FMA** | 106,574 tracks | Genre classification | CC licensed, multiple sizes |

---

## Recommended Reading Order

**Week 1 Schedule**:

| Day | Focus | Hours |
|-----|-------|-------|
| 1 | Shazam algorithm (Wang paper + tutorials) | 4-5 |
| 2 | Chromaprint + fingerprinting comparison | 3-4 |
| 3 | CLMR + contrastive learning for music | 4-5 |
| 4 | Cover song detection papers | 4-5 |
| 5 | Librosa hands-on + music features | 4-5 |
| 6 | musicnn + auto-tagging models | 5-6 |
| 7 | Music captioning + consolidation | 4-5 |

---

## Implementation Starting Points

**For Shazam-style fingerprinting**:
- Use Chromaprint/AcoustID for production
- Implement Wang algorithm for learning (see linked tutorials)

**For music similarity/search**:
- Start with CLMR pretrained embeddings
- Use cosine similarity for nearest-neighbor search
- Consider FAISS for large-scale retrieval

**For music description/tagging**:
- Start with musicnn pretrained models
- Fine-tune on your specific taxonomy
- For captioning: LP-MusicCaps provides working pipeline

**For cover detection**:
- Use chroma features + cross-similarity matrices
- CoverHunter for SOTA performance
- Da-TACOS for benchmarking