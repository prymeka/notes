# Modern Android Development — A Phased Curriculum (Kotlin + Jetpack Compose)
*Built for an ML engineer new to Kotlin/JVM. ~85% Android-Compose core, four woven emphasis tracks (on-device ML, backend/auth, testing/CI/publishing, offline-first), plus a lighter KMP/CMP orientation at the end. Official/Google-first resources with **[free]**/**[paid]** flags; version-sensitive items carry a ⚠ currency note. Verified against sources current as of early 2026 — re-check versions before pinning.*

---

## TL;DR
- The current de facto standard stack is settled: **Kotlin** (2.3.0 stable) · **Jetpack Compose** (BOM 2025.12.00, Compose 1.10) for UI · **Coroutines + Flow/StateFlow** for async · Google's **layered architecture with UDF + MVVM** (ViewModel state holders) · **Hilt** for DI · **Room + DataStore** for storage · **Retrofit + kotlinx.serialization** for networking · **WorkManager** for background work. Build with **Gradle Kotlin DSL + version catalogs**.
- The plan below is ~85% Android-Compose core on official free resources (Android Basics with Compose, the Compose pathway, the Guide to App Architecture, Now in Android), with four emphasis tracks woven in and a lighter KMP/CMP orientation module at the end.
- Highest-value cross-domain hook for your background: on-device inference via the **LiteRT CompiledModel API** — `litert_torch.convert()` (PyTorch → .tflite), then `CompiledModel.create()` with `writeFloat`/`readFloat` on numeric feature tensors — the natural path for on-device anomaly/fraud-signal scoring.

---

## The Standard Modern Stack (settled consensus)
- **Language:** Kotlin — the default, not an alternative. Over 95% of the top-1,000 Android apps use Kotlin, and it's the primary language for a majority of professional Android developers.
- **UI:** Jetpack Compose is the recommended toolkit for all new UI; more than 68% of the top-1,000 apps use it in production.
- **Async:** Kotlin coroutines + structured concurrency; Flow and StateFlow for reactive streams.
- **Architecture:** the official "Guide to app architecture" — UI layer (Compose + ViewModel state holder), optional Domain layer (use cases), Data layer (repositories + data sources). Unidirectional data flow (state down, events up); single source of truth.
- **DI:** Hilt (Google-recommended, built on Dagger, compile-time). Koin is the popular runtime alternative.
- **Navigation:** Navigation Compose (Nav2-era) is established; **Navigation 3 reached stable 1.0 on Nov 19, 2025** and is the new Compose-first direction.
- **Storage:** Room (relational DB / source of truth), DataStore (key-value & typed preferences, replaces SharedPreferences), file storage.
- **Networking:** Retrofit + OkHttp (Android standard) with kotlinx.serialization or Moshi; Ktor Client is the multiplatform-friendly alternative.
- **Background:** WorkManager for deferrable, guaranteed background work (e.g., sync).

## Current Versions (version-sensitive — verify at build time)
- **Kotlin:** 2.3.0 stable (Dec 16, 2025); 2.2.x still widely used; 2.4.x in EAP/RC.
- **Android Studio:** 2025.3.2 stable (~Mar 3, 2026).
- **Jetpack Compose:** BOM 2025.12.00 (Compose 1.10, Material 3 1.4), stable Dec 2025; Compose library 1.10.6 (~Mar 25, 2026).
- **Gradle / AGP:** AGP 8.10 (May 2025, supports up to API 36); AGP 8.8 (Jan 2025, API 35). Gradle 8.11+/9.x. AGP 9.x on the horizon.
- **Navigation 3:** 1.0.0 stable (Nov 19, 2025).
- **Compose Multiplatform:** 1.8.0 (May 2025) made iOS stable; 1.9.0 (Oct 2025) added Web beta (Wasm).
- **LiteRT:** 2.2.0 (Aug 14, 2026), CompiledModel API, min SDK 23; Interpreter line 1.4.2.
- **Hilt:** ~2.52+ era. **Coroutines** ~1.10.x, **Room** ~2.8.x, **DataStore** ~1.1.x (all move fast — verify).

## Calibration: Settled vs Contested vs Hype
- **SETTLED:** Kotlin as language; Compose for new UI; coroutines/Flow for async; layered architecture + UDF; Room + DataStore; WorkManager for background; AAB for publishing; Gradle Kotlin DSL + version catalogs.
- **SETTLED (mostly):** MVVM as the default screen-level pattern via ViewModel; repository pattern; DataStore over SharedPreferences.
- **CONTESTED:** MVVM vs MVI (both viable; MVI is a stricter UDF variant — often just "MVVM with a single immutable state object"); Hilt vs Koin (Hilt = Google-recommended, compile-time safety; Koin = simpler, Kotlin-first, runtime); Retrofit vs Ktor (Retrofit = Android standard; Ktor = needed for KMP); Nav3 vs Navigation Compose (Nav3 is stable and the future, but Navigation-Compose is still everywhere and battle-tested).
- **HYPE/OVERSTATED:** "Ktor is faster than Retrofit" (on Android both often ride OkHttp; latency is network-dominated); Compose Multiplatform for iOS being fully turnkey (stable since May 2025 but still has iOS perf/accessibility/native-look trade-offs); the "25x faster than CPU" LiteRT claim (Google's own official figure is far narrower — LiteRT delivers ~1.4x faster GPU performance than TFLite).
- **Do you still need XML/Views?** Mostly no for greenfield, but yes for maintaining existing codebases and reading older Stack Overflow answers. Treat Views as **read-only literacy**, not a build target.

## On-Device ML (detail — your high-value track)
- **LiteRT** is the rebranded TensorFlow Lite (announced Sept 2024); it now runs models authored in PyTorch, JAX, Keras, and TensorFlow.
- **CompiledModel API (LiteRT 2.x)** is the modern standard, replacing `tflite::Interpreter`/`InterpreterBuilder`. Kotlin flow: add `com.google.ai.edge.litert:litert:2.2.0` → `CompiledModel.create(assets, "model.tflite", CompiledModel.Options(Accelerator.CPU), env)` → `createInputBuffers()`/`createOutputBuffers()` → `writeFloat(...)` → `model.run(...)` → `readFloat()`.
- **Acceleration:** choose CPU/GPU/NPU via `CompiledModel.Options(Accelerator.X)`; GPU is built into the Maven package (no extra dependency); NPU supports vendor fallback (`Accelerator.NPU, Accelerator.GPU`). Read per-model latency off the official benchmark table rather than trusting secondhand multipliers.
- **PyTorch → .tflite:** `litert-torch` (formerly `ai-edge-torch`); `litert_torch.convert(model, sample_inputs).export("model.tflite")`. Built on `torch.export()`; the PyTorch converter is Beta. Requires Python 3.10–3.13, Linux, PyTorch ≥ 2.4.0.
- **ML Kit** provides turnkey on-device APIs (barcode, text recognition, image labeling, etc.) and custom-model support — but ML Kit custom models are **image-classification only**; custom numeric/tabular/text models must go through LiteRT (or the Task Library), not ML Kit.
- **On-device GenAI:** ML Kit GenAI APIs (summarization, proofreading, rewriting, image description, plus an alpha Prompt API) built on **Gemini Nano** running in the **AICore** system service; available on select devices (Pixel 8/9/10, some Snapdragon/MediaTek/Tensor).
- **Fraud/cross-domain reality:** there is no official turnkey anomaly/tabular/fraud API. The realistic path is a custom PyTorch model → `litert-torch` → CompiledModel with numeric feature tensors (`writeFloat`/`readFloat` map cleanly onto feature vectors). Run model load/compile and inference off the main thread via coroutines (`Dispatchers.IO` for file load, `Dispatchers.Default` for compute), or use `runAsync()` for GPU/NPU.

## KMP/CMP Maturity (detail — secondary module)
- **KMP** (business-logic sharing) is stable since Nov 2023; Google officially recommends it for sharing logic between Android/iOS.
- **CMP for iOS** is stable since May 2025 (v1.8.0); Web is in beta (Wasm, Oct 2025).
- Jetpack libraries (Room ~2.8.x, DataStore, ViewModel) now support KMP.
- Real production users: Netflix, McDonald's, Cash App, and others. KMP usage more than doubled in a year (roughly 7% → 18% per JetBrains' Developer Ecosystem Survey).
- Trade-offs: iOS still has perf/accessibility/native-look gaps; version mismatches between Kotlin and KMP libs can break builds; many teams share logic only and keep native UI.

## Publishing (2026)
- Google Play requires **AAB** (Android App Bundle) for new apps; **Play App Signing** is required.
- **Target SDK floor:** API 35 (Android 15) in force from Aug 31, 2025; from **Aug 31, 2026, new apps/updates must target API 36 (Android 16)**.
- Developer account: **$25 one-time** fee + identity verification.
- Store-listing assets: 512×512 icon, 1024×500 feature graphic, 2–8 screenshots, title (30 chars), short description (80), full description (4000).
- Release tracks: internal, closed, open testing, production.

---

## Design System & Best-Practices Backbone (keep open across all phases)
The single most useful follow-along pairing is **Now in Android** (a reference app that *shows* current best practice) plus the **Recommendations for Android architecture** checklist (which *codifies* it). If you bookmark only two things, bookmark these.

- **Now in Android** app + its **Material 3 Case Study** design files — `github.com/android/nowinandroid`. Canonical modern reference: Compose-first, official architecture, Material 3, adaptive layouts, baseline profiles, full test suite. **[free]**
- **Recommendations for Android architecture** — `developer.android.com/topic/architecture/recommendations`. A prioritized "strongly recommended / recommended / optional" rubric; use it as your best-practices scorecard. **[free]**
- **API Guidelines for Jetpack Compose** — `developer.android.com/develop/ui/compose/api-guidelines`. Idiomatic, stable composables (naming, parameter order, state hoisting, slot APIs). **[free]**
- **Compose performance best practices** — `developer.android.com/develop/ui/compose/performance/bestpractices` (+ the performance codelab). `remember`, stable lazy keys, `derivedStateOf`, deferred state reads, backwards-write pitfalls. **[free]**
- **Material 3 design site** — `m3.material.io`. The design spec: color roles, typography, components, motion. **[free]**
- **Material 3 in Compose** docs + the **Compose Material Catalog** (lives in AOSP, always current — a runnable gallery of every M3 component with a live theme picker), via `github.com/android/compose-samples`. **[free]**
- **Material 3 Design Kit (official, Figma)** + **Material Theme Builder** plugin — the Material Design team's Figma kit and `github.com/material-foundation/material-theme-builder`. Generate an HCT tonal palette from a seed color/image and export tokens straight into your Compose `Theme.kt`. **[free]** (Figma has a free tier)

> ⚠ **Design currency — Material 3 Expressive.** Announced at Google I/O (May 2025); rolled out on Pixel/Android 16 (QPR1, Sept 2025) with spring-based motion, shape morphing, flex fonts, and expanded tonal tokens. The design *language* is current — but the Compose `material3` APIs for the newest Expressive components were still in **alpha (1.4.x / 1.5.x-alpha)** as of early 2026. **Practical rule:** build on **stable Material 3** now, adopt Expressive components as they graduate to stable, and check the `material3` release notes before pinning a version.

---

## Learner Profile & Python → Kotlin Mapping
You're a strong ML engineer (Python, PyTorch, MSc AI, physics) new to Kotlin, the JVM, and Gradle. Design implications:

- **Extra runway on Kotlin fundamentals & the type system.** *Transfers:* static typing (conceptually familiar), functional style (map/filter/lambdas ≈ Python comprehensions/`lambda`), immutability preference. *New/different:* nullable types (`?`, `?.`, `!!`, Elvis `?:`) vs Python's implicit `None`; `val`/`var`; data classes (≈ `@dataclass` but with structural equality/`copy`); sealed classes (≈ tagged unions — ideal for UI state); extension functions (no Python equivalent — think safe monkeypatching); coroutines + structured concurrency (≈ asyncio but with `suspend` and scopes); generics + variance (`in`/`out` — stricter than duck typing); the JVM object model and the compile step (vs interpreted Python).
- **Gradle is the biggest "unknown unknown."** No Python analog to Gradle's build graph, configuration-vs-execution phases, plugins, and dependency resolution. Budget real time here (Phase 3).
- **UI mental-model shift:** Compose's "UI is a function of state" (declarative recomposition) will feel natural from a functional/data-pipeline mindset, and is arguably easier than the old imperative View system.
- **Cross-domain leverage:** on-device ML (Phase 6) is your genuine edge — front-load the motivation early, deliver the hands-on ML phase once the app scaffolding is in place.

---

## The Curriculum: Phase-by-Phase
**Dependency map:** Phase 0 is the root. 1 → 2 → 3 build the core (UI → architecture → build system). 4 (storage/offline) and 5 (networking/auth) depend on 2–3. 6 (on-device ML) depends on 4–5. 7 (testing/CI/publishing) depends on all. 8 (KMP/CMP) is a capstone add-on.

### Phase 0 — Tooling & Kotlin Foundations *(dependency root)*
- **Objectives:** install Android Studio; understand JVM/Gradle basics; write idiomatic Kotlin; master null safety, data/sealed classes, extension & higher-order functions, lambdas, generics/variance.
- **Primary [free]:** Kotlin docs (`kotlinlang.org`); Kotlin Koans (failing-unit-test exercises); Android Basics with Compose, Units 1–2.
- **Supplementary:** "Kotlin for Java Developers" (Coursera, JetBrains — free to audit); *Kotlin in Action, 2nd ed.* (Manning) **[paid]**; Marcin Moskała's *Kotlin Coroutines: Deep Dive* **[paid]**, for later.
- **Follow-along (best practices & design):** **Kotlin Tour** (interactive, in-browser) at `kotlinlang.org` — fastest hands-on ramp for syntax/null safety **[free]**; *Effective Kotlin* (Kt. Academy/Leanpub) — the Kotlin best-practices canon (idioms, null-handling, immutability, performance), the Kotlin analog to *Effective Java* **[paid]**; pair the coroutines deep-dive with the official **Coroutines guide** **[free]**.
- **Exercise:** work all Koans; write a small CLI-style Kotlin program.
- **Est.** 2–3 weeks part-time.

### Phase 1 — Compose UI Fundamentals *(builds on 0)*
- **Objectives:** composables, modifiers, layout, state, recomposition, state hoisting, Material 3, theming.
- **Primary [free]:** Jetpack Compose basics codelab; "Jetpack Compose for Android Developers" pathway (Compose essentials); Android Basics with Compose, Units 2–3.
- **Follow-along (best practices & design) — this is the design-heavy phase; anchor the whole Backbone here:** **Compose Samples** (Jetsnack, Jetchat, JetLagged, Reply, Crane) — `github.com/android/compose-samples`, production-grade design/pattern references you can read and run **[free]**; the **Compose Material Catalog** for live component behavior **[free]**; **workflow tip** — design your palette/typography in the **Material 3 Design Kit + Theme Builder** first, then export tokens into `Theme.kt` before writing UI.
- **Project:** build the Tip Calculator and an "Art Space" app.
- **Est.** 2–3 weeks.

### Phase 2 — App Architecture, State & Navigation *(builds on 1)*
- **Objectives:** ViewModel, UDF, UI-state modeling with sealed classes + StateFlow, state hoisting at scale, screen navigation & passing data.
- **Primary [free]:** Guide to app architecture + Recommendations; Architecture Components pathway; Navigation docs. Introduce **Nav3** as the current direction while noting Navigation-Compose is what most existing tutorials use.
- **Reference apps [free]:** **Now in Android** (`github.com/android/nowinandroid`) + **architecture-samples** (TODO app) + architecture-templates.
- **Follow-along (best practices & design):** **Guide to app architecture** (`developer.android.com/topic/architecture`) + the **Recommendations** checklist from the Backbone **[free]**; **architecture-samples** — single-activity, ViewModel-per-screen, Flow, Hilt, Room + fake remote, mock/prod flavors, full tests — the best compact end-to-end best-practices reference **[free]**; read **Now in Android's** "UI architecture" learning journey alongside **[free]**.
- **Project:** multi-screen app with a ViewModel per screen and typed navigation.
- **Est.** 3–4 weeks.

### Phase 3 — Gradle, Project Structure & Modularization *(builds on 2)*
- **Objectives:** Gradle Kotlin DSL, version catalogs (`libs.versions.toml`), modules, dependency management, build variants/flavors, KSP.
- **Primary [free]:** Android build docs; Now in Android modularization learning journey.
- **Follow-along (best practices & design):** **Guide to Android app modularization** (`developer.android.com/topic/modularization`) **[free]**; **Now in Android** modularization journey + its **convention plugins** — a real-world example of version catalogs + build-logic modules **[free]**.
- **Exercise:** convert a single-module app to Gradle Kotlin DSL + version catalog; split into feature/data modules.
- **Est.** 1–2 weeks.

### Phase 4 — Storage & Offline-First *(Track 4 · builds on 2–3)*
- **Objectives:** in-memory state vs DataStore vs Room vs files; Room as single source of truth; reactive DB→UI Flows; WorkManager sync; conflict resolution (server-version / optimistic UI, sync metadata like `pendingSync`/`lastModified`).
- **Primary [free]:** Room, DataStore, WorkManager docs; Now in Android (offline-first reference); "Build an offline-first app" guide.
- **Follow-along (best practices & design):** **Build an offline-first app** guide (`developer.android.com/topic/architecture/data-layer/offline-first`) — reads/writes/sync/conflict resolution **[free]**; **Now in Android** doubles as an offline-first reference (Room as source of truth + WorkManager sync) **[free]**.
- **Project:** offline-first notes/tasks app; Room + Flow + WorkManager background sync with a fake remote.
- **Est.** 3 weeks.

### Phase 5 — Networking, APIs & Auth *(Track 2 · builds on 2–4)*
- **Objectives:** Retrofit + kotlinx.serialization; coroutine-based calls; error/retry; Ktor as the KMP alternative; OAuth2; token storage/encryption; **Credential Manager** (replaces the deprecated Google Sign-In SDK); passkeys; biometric auth.
- **Primary [free]:** Android networking docs; Retrofit/OkHttp docs; Credential Manager docs + codelab; the "Get data from the internet" pathway (Retrofit + Coil).
- **Follow-along (best practices & design) — cross-domain relevance to your fraud/security work:** **Credential Manager** docs + codelab (`developer.android.com/identity/sign-in/credential-manager`) — the current unified API for passkeys, passwords, and Sign in with Google **[free]**; the **"Get data from the internet"** pathway (coroutine calls, error/loading states) **[free]**.
- ⚠ **Secure-storage currency:** Jetpack Security Crypto (`EncryptedSharedPreferences`) is deprecated — follow current guidance for token storage (Android Keystore-backed encryption / DataStore), not older tutorials. Verify the live recommendation before implementing.
- **Project:** add a REST backend with loading/retry/offline UX and Sign in with Google.
- **Est.** 3 weeks.

### Phase 6 — On-Device ML *(Track 1 · the cross-domain payoff · builds on 4–5)*
- **Objectives:** ML Kit turnkey APIs; a custom TFLite/LiteRT model via CompiledModel; input/output tensors; CPU/GPU/NPU; threading off the main thread; PyTorch → .tflite; Gemini Nano/AICore/ML Kit GenAI orientation.
- **Primary [free]:** LiteRT docs (`ai.google.dev/edge/litert`); CompiledModel Kotlin guide; `litert-torch` repo (`github.com/google-ai-edge/litert-torch`); ML Kit docs; Gemini Nano docs (`developer.android.com/ai/gemini-nano`); ML Kit GenAI docs.
- **Follow-along (best practices & design):** **LiteRT** docs + **CompiledModel** Kotlin guide **[free]**; **litert-torch** (PyTorch → .tflite) — maps directly onto your PyTorch workflow **[free]**; **ML Kit** (`developers.google.com/ml-kit`) and **Gemini Nano / ML Kit GenAI** (⚠ Gemini Nano is device-gated) **[free]**; **Google AI Edge** samples/Gallery (`google-ai-edge` on GitHub) for runnable on-device inference examples **[free]**.
- **Project:** (a) ML Kit image labeling; (b) convert a small PyTorch model and run it on-device with CompiledModel; (c) *stretch:* an on-device numeric anomaly/fraud-signal scorer with `writeFloat`/`readFloat`.
- **Est.** 2–3 weeks.

### Phase 7 — Testing, CI/CD & Publishing *(Track 3 · builds on all)*
- **Objectives:** unit testing (JUnit, kotlin.test, MockK, Turbine for Flow); Compose UI tests (ComposeTestRule, semantics); Robolectric (JVM Compose tests); Espresso/instrumentation; screenshot testing; CI/CD with GitHub Actions + Gradle; app signing, build variants/flavors; end-to-end Play Store publishing (Play Console, AAB, release tracks, target-SDK rules).
- **Primary [free]:** Testing in Compose docs; Now in Android tests; Play Console docs; app-bundle docs.
- **Follow-along (best practices & design):** **Testing in Compose** docs + **Compose testing cheat sheet** (`developer.android.com/develop/ui/compose/testing`) **[free]**; **What to test / test your app's architecture** (`developer.android.com/training/testing`) **[free]**; **Now in Android's** test suite (unit + Compose UI + screenshot/Macrobenchmark) as a working reference **[free]**; **App Bundle** + **Play Console** + **Launch checklist** (`developer.android.com/guide/app-bundle`, `play.google.com/console`) — ⚠ new/updated apps must target **API 36 (Android 16)** from **Aug 31, 2026** **[free]** (Play account: $25 one-time); **CI:** official **Gradle** + **setup-android** GitHub Actions to build/test on PRs **[free]**.
- **Project:** add unit + Compose UI tests, wire a GitHub Actions pipeline, produce a signed AAB, publish to an internal testing track.
- **Est.** 2–3 weeks.

### Phase 8 — KMP/CMP Orientation *(secondary, lighter · capstone add-on)*
- **Objectives:** understand what code shares (logic vs UI); `expect`/`actual`; when it's worth it; current maturity; how an Android-first Compose app migrates toward KMP (swap Retrofit → Ktor; use KMP-enabled Room/DataStore/ViewModel; move logic to `commonMain`).
- **Primary [free]:** KMP docs + "Get started with KMP" pathway; CMP docs; JetBrains KMP roadmap.
- **Follow-along (best practices & design):** **Kotlin Multiplatform** docs + **"Create your first cross-platform app"** tutorial + the **KMP web wizard** (`kmp.jetbrains.com`) **[free]**; **Compose Multiplatform** docs (JetBrains) + the official **KMP App Template** / KMP samples **[free]**; the **KMP roadmap** (JetBrains) to gauge what's stable vs in-progress before betting on it **[free]**.
- **Project:** extract the app's data/domain layer into a shared KMP module; optional small CMP screen.
- **Est.** 1–2 weeks.

---

## MVP / Time-Compressed Path
To ship a basic app fast, compress to: **Phase 0** (Kotlin essentials — null safety, data/sealed classes, lambdas, coroutine basics) → **Phase 1** (Compose basics + state) → the ViewModel/UDF slice of **Phase 2** + basic Navigation → the Room/DataStore slice of **Phase 4** → the Retrofit slice of **Phase 5** → the signing/AAB/Play slice of **Phase 7**. Skip modularization depth, MVI, Nav3 migration, on-device ML, and KMP until after v1 ships. **Realistic compressed timeline: ~4–6 weeks of focused effort to a publishable v1.**

## Concrete Project Arc
Trivial → non-trivial: (1) text/image "hello" app → (2) Tip Calculator (state) → (3) Art Space (navigation/layout) → (4) offline-first task manager (Room + Flow + WorkManager) → (5) + REST backend & auth → (6) + on-device ML feature (image labeling or a custom LiteRT scorer) → (7) tested, CI'd, published to Play internal track → (8) shared logic extracted to KMP.

## How to Use This Curriculum
- **Read reference apps, don't just skim docs.** For each phase, open the matching sample (`architecture-samples` for Phase 2, `nowinandroid` throughout) in Android Studio and trace one real feature end to end. Reading production Compose code is the fastest way to internalize idiom and structure.
- **Use the Recommendations checklist as a gate.** Before calling a phase "done," run your code against the relevant items in `topic/architecture/recommendations` — it's the closest thing to an official best-practices rubric.
- **Design before you build each screen.** The Theme Builder → `Theme.kt` token-export loop keeps you on-spec and minimizes rework once Expressive components stabilize.
- **Re-verify versions per phase.** Android tooling moves monthly; confirm current Kotlin / AGP / Compose BOM / Material3 / LiteRT versions at the start of each phase rather than trusting a pinned number.

## Recommendations
1. **Start with Kotlin + Gradle literacy before any Android UI.** Given the Python background, over-invest in null safety, sealed classes, coroutines, and Gradle. Advancement bar: complete Kotlin Koans and explain `val` vs `var`, nullable types, and a `sealed class` UI-state model without reference.
2. **Anchor the whole program on official free resources** (Android Basics with Compose, the Compose pathway, the Guide to App Architecture, Now in Android); use paid books (*Kotlin in Action*, *Effective Kotlin*, Moskała's *Coroutines*) only as scaffolding.
3. **Adopt the standard stack deliberately:** Compose + ViewModel/UDF + Hilt + Room/DataStore + Retrofit/kotlinx.serialization + WorkManager. Learn MVI as a variant, not a replacement. Learn Nav3 but read Navigation-Compose code.
4. **Sequence the ML track late (Phase 6) but sell it early** — it's your differentiator. Realistic use cases: on-device anomaly/fraud-signal scoring, image/text classification. Validate device availability before committing to a Gemini Nano/AICore-dependent project (it's device-gated).
5. **Version-pin and re-check at build time.** Use the Compose BOM and a version catalog; confirm current Kotlin/AGP/Gradle/Compose/Room/Coroutines versions before starting each phase.
6. **Publish something small early** (internal testing track) to internalize signing/AAB/target-SDK rules before the API 36 deadline (Aug 31, 2026) bites.
7. **Treat KMP as orientation, not a track** — extract shared logic once the Android app is solid; keep native UI unless there's a strong reason to share it. Threshold to go deeper: a second target (iOS/desktop/web) becomes a real product requirement.

## Caveats
- **Version churn:** Android tooling changes fast; the versions above are current as of research (mid-2026) and should be re-verified. The Compose library/BOM numbers and LiteRT 2.2.0 in particular are recent.
- **Doc lag:** official LiteRT Kotlin sample code still references `litert:2.1.0` while the version table lists 2.2.0 — expect docs to trail releases. A few deeper-link doc paths here (e.g., offline-first, modularization) are the standard `developer.android.com` locations but worth a quick click-check, since Google occasionally reorganizes the docs tree.
- **Deprecations to avoid in old tutorials:** XML Views-first tutorials, `synthetic` view binding, LiveData-only patterns, legacy Google Sign-In (`play-services-auth`), Groovy Gradle without version catalogs, `EncryptedSharedPreferences`, and pre-Compose navigation approaches.
- **Unofficial benchmarks:** performance multipliers from blogs/vendor posts (e.g., LiteRT "25x", DI "15–20% faster startup") are directional, not official. Google's only official LiteRT-vs-TFLite GPU figure is ~1.4x.
- **On-device GenAI is device-gated:** Gemini Nano/AICore only run on specific hardware; not a universal capability.
- **Adoption statistics vary by source:** Kotlin (~95% of top-1,000 apps) and Compose (~68% of top-1,000) figures come from official Google/JetBrains pages; KMP adoption (~7% → 18%) is from JetBrains' survey, while some third-party blogs cite higher numbers that the primary source doesn't corroborate.