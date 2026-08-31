# Reading Guide: Learning a Controllable 3D Cassowary Prior from 2D Image Collections

This is the "Stage A" literature from the project plan — the papers that teach a model to turn a pile of ordinary 2D animal photos into a controllable, poseable 3D asset, with no CT scans, no CAD, and no 3D ground truth. The field moved fast between 2022 and 2024, and each paper is a direct response to a limitation in the one before it. Read them in this order — it's also roughly the field's own chronological lineage.

**Suggested reading order:** LASSIE → Hi-LASSIE → DOVE → MagicPony → ARTIC3D → 3D-Fauna → Farm3D → SyncDreamer-for-endangered-species (read this one last — it's the only one that isn't part of the direct lineage, but it's the closest thing to your exact use case).

---

## 1. LASSIE — the paper that defines the whole problem setting

**Yao, Hung, Li, Rubinstein, Yang & Jampani, *LASSIE: Learning Articulated Shapes from Sparse Image Ensemble via 3D Part Discovery*, NeurIPS 2022.** arXiv:2207.03434

**The problem it poses:** can you estimate the 3D pose and shape of an animal species given <cite index="61-1">only a sparse set of image ensembles — as few as 10-30 in-the-wild images — without using any 2D or 3D ground-truth annotations, multi-view captures, or temporal information</cite>? This sparse-image, no-annotation setting is the constraint every later paper in this list inherits.

**How it works:** rather than modeling the whole animal as one mesh, LASSIE builds it from parts. <cite index="63-1">Each part surface is represented as a multi-layer perceptron that predicts the 3D deformation of a continuous UV coordinate on a unit sphere</cite> — i.e., a deformed sphere per limb/body segment, scaled and rotated onto a skeleton bone. This is the key trick: whole-animal shapes are hard to model directly, but individual parts are close to simple convex primitives, so an MLP can represent each one at arbitrary resolution without needing a fixed mesh template.

**The catch:** you have to hand the model a rough 3D skeleton template yourself. <cite index="59-1">Manually specifying a rough skeleton is described as a trivial task taking only a few minutes</cite>, but it's still a human-in-the-loop step — the very thing Hi-LASSIE removes next.

**Why it matters for cassowary:** the "10–30 images, no annotations" regime is almost certainly your real data budget. But LASSIE's part-based decomposition assumes a *quadruped-like* skeleton in its published experiments (horses, zebras, etc.) — you'd need to hand-specify a bipedal, long-necked skeleton template for a cassowary, which is untested territory for this specific method.

---

## 2. Hi-LASSIE — removes the human-provided skeleton

**Yao, Hung, Li, Rubinstein, Yang & Jampani, *Hi-LASSIE: High-Fidelity Articulated Shape and Skeleton Discovery from Sparse Image Ensemble*, CVPR 2023.** arXiv:2212.11042

**What it fixes:** LASSIE's one remaining manual step. Hi-LASSIE makes two advances over LASSIE: <cite index="60-1">first, instead of relying on a manually annotated 3D skeleton, it automatically estimates a class-specific skeleton from a single selected reference image; second, it improves shape reconstructions with instance-specific optimization strategies that let each instance fit faithfully while preserving the class-specific prior learned across all images</cite>.

**How it works, concretely:** you pick one reference photo where most body parts are visible, and the algorithm discovers the skeleton topology itself, then reuses LASSIE's neural-part-surface representation to fit shape and pose across the rest of the ensemble.

**Why it matters for cassowary:** this is the more practical entry point of the two, precisely because it removes the skeleton-authoring step — you wouldn't need to hand-design a cassowary-specific bone structure. A single good reference photo showing the casque, neck, legs, and tail feathers clearly would be your reference image.

---

## 3. DOVE — the bird-specific alternative, using video instead of skeletons

**Wu, Jakab, Rupprecht & Vedaldi, *DOVE: Learning Deformable 3D Objects by Watching Videos*, IJCV 2023 (originally CVPR-track arXiv 2021).** arXiv:2107.10844

**The core idea:** instead of a hand-specified or auto-discovered skeleton, use *video* as the supervisory signal. <cite index="69-1">By resolving symmetry-induced pose ambiguities and leveraging temporal correspondences in videos, the model automatically learns to factor out 3D shape, articulated pose, and texture from each individual RGB frame, and is ready for single-image inference at test time</cite> — meaning you train on video clips, but at inference time it works on a single photo.

**Why this one is special for your project:** it's explicitly bird-trained. <cite index="67-1">The method successfully learns good 3D shape predictors from videos of animals such as birds and horses</cite>, and the public codebase ships bird-video training data directly (`download_bird_videos.sh`) — this is the single most directly relevant precedent on this whole list, since it's proof the general approach works on avian body plans, not just quadrupeds.

**The catch:** it needs *video*, not just photo collections — a real practical constraint, since your cassowary data source (iNaturalist) is overwhelmingly still photos, not video clips.

---

## 4. MagicPony — the mainstream, best-supported method (and it's already been trained on birds)

**Wu, Li, Jakab, Rupprecht & Vedaldi, *MagicPony: Learning Articulated 3D Animals in the Wild*, CVPR 2023.** arXiv:2211.12497

**The core idea:** <cite index="96-1">given a collection of single-view images of an animal category, the model learns a category-specific prior shape using an implicit-explicit representation, together with a feature field that fuses self-supervised correspondences through a feature-rendering loss</cite>. In plain terms: it combines a neural implicit field (flexible, but hard to control) with an explicit mesh (easy to pose and render, but less flexible) to get the best of both, and it uses a pretrained self-supervised vision transformer (DINO-ViT) to figure out which pixels across different photos correspond to the same body part — without anyone labeling keypoints.

**Why this is probably your default choice:** it's the most mature, best-documented, and most actively maintained codebase in this list (`github.com/elliottwu/MagicPony`, folded into the `3DAnimals` umbrella repo). Crucially, the public release <cite index="81-1">has already been trained on image collections of horses, giraffes, zebras, cows, and birds</cite>, using bird data sourced from DOVE. That's a strong signal the method's assumptions hold for birds specifically, not just quadrupeds — directly de-risking the "will this even work on a cassowary" question.

**A subtlety worth understanding:** MagicPony <cite index="97-1">distills the knowledge captured by an off-the-shelf self-supervised vision transformer and fuses it into the 3D model, and introduces a new viewpoint-sampling scheme to overcome common local optima in viewpoint estimation</cite> — viewpoint ambiguity (is the bird facing left or right, toward or away from camera) is one of the hardest sub-problems in this entire literature, and it's worth understanding this scheme specifically before you start.

---

## 5. ARTIC3D — adds robustness to messy, real web photos (via diffusion priors)

**Yao, Raj, Hung, Li, Rubinstein, Yang & Jampani, *ARTIC3D: Learning Robust Articulated 3D Shapes from Noisy Web Image Collections*, NeurIPS 2023.** arXiv:2306.04619

**What it fixes:** MagicPony and LASSIE-family methods assume relatively clean input photos. ARTIC3D targets the messier reality of scraped web images. <cite index="112-1">It uses the articulated part surface and skeleton from Hi-LASSIE, and proposes a novel Decoder-based Accumulative Score Sampling module that effectively leverages 2D diffusion model priors from Stable Diffusion for 3D optimization</cite>. Concretely: <cite index="108-1">it first enhances input images with occlusions or truncation via 2D diffusion to obtain cleaner mask estimates and semantic features, then performs diffusion-guided 3D optimization to estimate shape and texture that are high-fidelity and faithful to the input images</cite>.

**Why it matters for cassowary:** iNaturalist/GBIF photos of a wild, shy rainforest bird are exactly the "noisy web image" case this paper targets — partial occlusion by foliage, birds walking out of frame, awkward angles. This is likely your most realistic real-world starting point among the LASSIE-family methods, precisely because it was built for messy inputs rather than curated ones.

---

## 6. 3D-Fauna — pan-species generalist (read the caveat closely — it doesn't apply to cassowary)

**Li, Litvak, Li, Zhang, Jakab, Rupprecht, Wu & Vedaldi, *Learning the 3D Fauna of the Web*, CVPR 2024.** arXiv:2401.02400

**The ambition:** one model, not one-per-species. <cite index="77-1">3D-Fauna learns a pan-category deformable 3D model of more than 100 different animal species using only 2D Internet images as training data</cite>, via a "Semantic Bank of Skinned Models" that automatically discovers a small set of base animal shapes shared across species, combining geometric priors with semantic knowledge from a self-supervised feature extractor. Technically, <cite index="86-1">it builds on MagicPony but introduces a learnable prior shape bank that dynamically combines basis shapes during training and inference to generate diverse instance-specific prior 3D shapes</cite>, removing the "one model per category" constraint.

**The important caveat, stated plainly by the authors:** <cite index="79-1">despite modeling diverse animals, the current model is still limited to quadruped species that share the same skeletal structure</cite>. **A cassowary is not a quadruped.** This paper is genuinely impressive and worth understanding for the "shared shape bank" idea, but it is explicitly out of scope for a bipedal bird — good to cite as "adjacent, inapplicable-as-is" rather than as a direct tool.

---

## 7. Farm3D — the one that might let you skip needing many real cassowary photos at all

**Jakab, Li, Wu, Rupprecht & Vedaldi, *Farm3D: Learning Articulated 3D Animals by Distilling 2D Diffusion*, 3DV 2024.** arXiv:2304.10535

**The idea, and it's a genuinely clever one:** instead of curating real photos as training data, use a text-to-image diffusion model to generate them. <cite index="88-1">Via prompt engineering, Stable Diffusion can be induced to generate a large training set of relatively clean images of an object category, and these images can be used to bootstrap MagicPony</cite> — i.e., Farm3D is a *training-data generator* for MagicPony's own architecture. On top of that, <cite index="89-1">the diffusion model is also used as a scoring mechanism during training: aspects of the reconstruction like viewpoint and illumination are randomized, virtual views of the reconstructed 3D object are rendered, and the 2D diffusion network assesses the quality of the resulting image to provide feedback to the reconstructor</cite> — this is a Score Distillation Sampling loss, extended to supervise a reusable reconstruction network rather than a single one-off 3D asset. The result, notably, <cite index="87-1">is a monocular reconstruction network capable of generating controllable 3D assets from a single input image, real or generated, in a matter of seconds</cite> — not hours, unlike most diffusion-to-3D pipelines.

**Why this is the most exciting paper on the list for your specific bottleneck:** if real cassowary photos turn out to be too scarce or too messy even for ARTIC3D, Farm3D suggests a path around the data problem entirely — generate the training images yourself. **The honest caveat:** this depends on Stable Diffusion already having a decent internal representation of what a cassowary looks like, which is far less certain for a rare rainforest bird than for the common farm/domestic animals (cows, horses, sheep, pigs, dogs) the paper actually tested on. Worth a fast, cheap sanity check — just prompt an image generator for "southern cassowary" and see how anatomically correct the casque, wattles, and leg structure come out — before committing to this route.

---

## 8. SyncDreamer-for-endangered-species — not part of the lineage above, but the closest match to your actual use case

**Ornek, Sen & Civil (Huawei Türkiye R&D Center), *SyncDreamer for 3D Reconstruction of Endangered Animal Species with NeRF and NeuS*, 2023.** arXiv:2312.13832

**Why it's grouped separately:** this paper doesn't descend from the LASSIE/MagicPony lineage at all — it takes a single-object novel-view-synthesis diffusion model (SyncDreamer) and feeds its synthesized views into standard 3D reconstruction backends (NeRF and NeuS), rather than learning a category-level articulated prior. It's a different technical family, but it's the only paper in this entire list whose explicit motivation is your exact problem: <cite index="121-1">demonstrating how innovative view synthesis and 3D reconstruction techniques can be used to create models of endangered species using monocular RGB images</cite>, precisely because of image scarcity.

**What they found, and it's a useful, honest result to know before you pick a backend:** <cite index="116-1">the combination of SyncDreamer, NeRF, and NeuS could successfully create 3D models of endangered animals, but NeuS produced blurry outputs while NeRF produced sharper but noisier results</cite> — tested on <cite index="122-1">oriental stork, frog, dragonfly, and tiger</cite>. No bird-specific articulation modeling here (a stork is reconstructed as a static rigid shape from one pose, not an articulated, poseable model) — this is a real limitation relative to MagicPony/Farm3D, but the paper is valuable as direct evidence that the "too few images for standard 3D reconstruction" problem is solvable via generative view synthesis, for a bird-like species, in a conservation-motivated context.

---

## How the papers relate to each other (lineage summary)

```
LASSIE (2022)
  → needs a hand-authored skeleton
  ↓
Hi-LASSIE (2023)
  → auto-discovers the skeleton from one reference image
  ↓
ARTIC3D (2023)
  → adds Stable Diffusion priors on top of Hi-LASSIE's parts, for noisy/occluded web photos

DOVE (2021/2023)                    MagicPony (2023)
  → video-supervised,                 → single-view-photo-supervised,
    bird + horse trained                 already bird-trained,
                                          implicit-explicit representation
        ↘                           ↙
          both are "one model per category"
                    ↓
        3D-Fauna (2024)
          → one model for 100+ species — but quadrupeds only, doesn't cover cassowary
                    ↓
        Farm3D (2024)
          → bootstraps MagicPony using Stable-Diffusion-generated
            training images instead of curated real photos

SyncDreamer-for-endangered-species (2023)
  → a separate, simpler technical family (novel-view diffusion + NeRF/NeuS),
    but the only paper explicitly aimed at scarce-image conservation use cases
```

## What to take away, concretely

- **Most likely starting point:** Hi-LASSIE or ARTIC3D — both remove the manual-skeleton burden and are built for exactly the "sparse, imperfect real photos" regime you'll actually have.
- **Most mature, best-supported codebase:** MagicPony (via the `3DAnimals` GitHub org), with the reassurance that it's already been run successfully on bird image collections.
- **Best fallback if real cassowary images prove too scarce:** Farm3D's diffusion-bootstrapping trick — worth a cheap sanity check on whether Stable Diffusion "knows" what a cassowary looks like before relying on it.
- **Don't use as-is:** 3D-Fauna — genuinely relevant ideas (shared shape bank across species), but its own authors state it's limited to quadrupeds sharing a skeletal structure, which a cassowary doesn't.
- **Read for framing, not for a tool you'll run:** SyncDreamer-for-endangered-species — the closest thing to a "why this matters for conservation" citation, and a useful honest data point on NeRF-vs-NeuS output quality trade-offs.

---

## 2025–2026 Update: Yes, There's Real New Work — Including a Bird-Specific SOTA

The original guide above stopped at early-2024 work, and the field has kept moving. Here's what's changed, and one addition in particular reframes the whole project.

### Start here: a survey that does the catch-up for you

**Li, Amrani, Rai & Laga, *Advances and Trends in the 3D Reconstruction of the Shape and Motion of Animals*, arXiv:2508.16062 (Aug 2025).** This is a proper field survey — <cite index="134-1">it categorizes and discusses state-of-the-art methods based on their input modalities, how 3D geometry and motion are represented, the reconstruction techniques used, and training mechanisms, and analyzes strengths, limitations, and open challenges</cite>. Read this first; it'll orient you faster than re-deriving the lineage from individual papers, and it covers everything below plus much more.

### The most important new development for your project specifically: birds now have their own SOTA parametric model

This is the update that actually changes your options, not just adds papers to a list.

**Wang et al., *Birds of a Feather: Capturing Avian Shape Models from Images*, CVPR 2021** (earlier than it sounds, but foundational to what follows) introduced **AVES**, <cite index="152-1">a multi-species statistical shape model extracted from reconstructions of 17 bird species</cite>, showing <cite index="153-1">the model generalizes to held-out species not seen during training</cite> via k-fold cross-validation. This is a parametric bird model — the avian equivalent of SMAL for quadrupeds — and it's directly relevant because it's species-general by design, tested for exactly the "does it work on a species I didn't train it on" question that matters for a cassowary.

**An, Li et al., *AniMer+: Unified Pose and Shape Estimation Across Mammalia and Aves via Family-Aware Transformer*, Aug 2025 (extending AniMer, CVPR 2025).** arXiv:2508.00298. This is the current SOTA, and it's strikingly close to your own project's logic. Three things matter here:

1. **It unifies mammals and birds in one model**, using <cite index="154-1">a Mixture-of-Experts Vision Transformer that partitions network layers into taxa-specific components for mammalia and aves, plus taxa-shared components, enabling effective handling of both taxonomic groups within a single framework</cite>.
2. **It solves the exact data-scarcity problem you're solving, but for birds specifically, already, in 2025:** <cite index="151-1">to overcome the critical shortage of 3D training data, especially for birds, they introduce a diffusion-based conditional image generation pipeline producing two synthetic datasets — CtrlAni3D for quadrupeds and CtrlAVES3D for birds — with CtrlAVES3D described as the first large-scale, 3D-annotated dataset for birds, crucial for resolving single-view depth ambiguity</cite>.
3. **It's already state-of-the-art on held-out data:** <cite index="155-1">trained on an aggregated collection of 41,300 mammalian and 12,400 avian images combining real and synthetic data, it demonstrates superior performance over existing approaches across benchmarks including the challenging out-of-domain Animal Kingdom dataset</cite>.

**Why this matters for your pitch:** AniMer+ is essentially a published, peer-reviewed proof that "generate synthetic 3D-annotated training data via diffusion to fix bird data scarcity" works, in 2025, for birds in general. That's both good and slightly deflating news — good, because it validates your core hypothesis with real evidence; deflating, because "does synthetic generation help bird 3D reconstruction" is no longer an open question in general terms. **Your actual novel contribution needs to shift one level down:** not "does this work for birds" (AniMer+ answered that), but "does the AVES/AniMer+ parametric approach — built and validated on typical perching/wading birds — actually transfer to a cassowary's very atypical body plan (flightless, heavy-bodied, casqued, no keeled sternum for flight muscles)," and whether cassowary-specific fine-tuning or a template-free approach (MagicPony/ARTIC3D-style) does better on a bird this unusual. That's a sharper, more defensible research question than the one in the original plan.

### The newest quadruped-focused SOTA (useful for comparison, not directly applicable)

**Hu et al., *SAM 3D Animal: Promptable Animal 3D Reconstruction from Images in the Wild*, arXiv:2605.07604 (May 2026).** The newest, most "foundation-model" entry in this space — likely from the SAM lineage given the naming and framing. <cite index="143-1">It's the first promptable framework for multi-animal 3D reconstruction from a single image, built on the SMAL+ parametric model, jointly reconstructing multiple instances and supporting keypoint and mask prompts for disambiguation in crowded, occluded scenes, trained using a new Herd3D dataset of over 5,000 images</cite>. **Explicit limitation, stated by the authors themselves:** <cite index="142-1">it remains limited by the SMAL+ shape space and is therefore mainly applicable to quadruped-like animals</cite> — so, like 3D-Fauna, genuinely impressive but not a cassowary tool. Worth knowing about for the "promptable, multi-instance" framing, which is a design pattern you could borrow even if the underlying shape model doesn't fit.

### Newest extensions of the template-free (MagicPony/LASSIE) lineage

- **Zhao, Wu & Wu, *Web-Scale Collection of Video Data for 4D Animal Reconstruction*, NeurIPS 2026 Datasets and Benchmarks Track.** arXiv:2511.01169. Directly addresses the "where do we even get enough animal video/image data" problem at the data-collection-pipeline level — relevant if you go the DOVE/3D-Fauna video route rather than still-photo route.
- ***BAT3R: Bootstrapping Articulated 3D Reconstruction from 2D Image Collections*, 2026.** arXiv:2607.03891. A recent extension of the DualPM/MagicPony lineage to new species (chimpanzees, elephants), useful as a current example of how the field is handling species the original papers never tested.
- ***CORGI: Consistency-Aware 3D Dog Reconstruction from a Single Image in the Wild*, 2026.** arXiv:2607.00321. Single-species-specialized, single-image reconstruction — a good current example of the "go deep on one species" strategy as opposed to AniMer+'s "unify many species" strategy; worth reading for the design trade-off discussion alone.

### Revised takeaway

The honest picture: the *general* question "can diffusion-generated synthetic data fix 3D animal data scarcity for birds" was answered — yes — by AniMer+ in 2025, which changes what counts as novel in your pitch. The gap that's still genuinely open is species-specific: nothing in this literature, from 2022 through the May 2026 SAM 3D Animal release, has been built or tested on a cassowary or a comparably atypical flightless ratite. Positioning your project as a stress test of AVES/AniMer+ on a body plan its authors never saw — rather than as the first application of synthetic 3D data to birds — is both more accurate and a stronger, more specific research question for a senior audience.