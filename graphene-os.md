# From Python to GrapheneOS Contributor: A Phased Self-Study Curriculum Design Brief

## TL;DR
- **The two target tracks map onto concrete, currently-active GrapheneOS repositories**: the NATIVE/SYSTEMS track centers on `GrapheneOS/hardened_malloc` (C, MIT-licensed, 1.9k stars and 147 forks per its GitHub repo as of Sept 2026, latest release tag "14" signed by Daniel Micay dated 22 Feb 2026 — its README is the primary design doc), `platform_bionic` (hardened libc), and the kernel repos (`kernel_common-6.1/6.6/6.12` LTS forks plus the Pixel kernel monorepos on GitLab); the FRAMEWORK/PLATFORM track centers on `platform_frameworks_base`, `platform_packages_modules_Permission`, and `platform_system_sepolicy`. Contribution is via GitHub pull requests to github.com/GrapheneOS with communication on Discord/Matrix/the Flarum forum — there is no formal CLA gate visible in public docs, and their published code-style guide is short and language-specific.
- **You already own the single most important asset — a supported Pixel — and the build-flash-iterate loop is officially documented and reproducible**, but it is heavyweight: an x86-64 Linux host (Debian/Ubuntu/Arch officially supported), 32 GiB+ RAM (mandatory for LTO+CFI links), ~136 GiB for source with history plus ~100 GiB+ build space, tracking Android 17 (the `17` branch) as of 2026. Pixel 8–10 are the best development devices because they have ARM MTE hardware, which is essential for hardened_malloc's most important modern feature.
- **The realistic timeline is 12–18 months of serious part-time study before a merged non-trivial contribution**, front-loaded with C and systems fundamentals (the learner's genuine gap), then split into the two tracks. The stable/settled foundations (C, POSIX, OS concepts, the Android multi-party consent security model) are safe to learn from classic textbooks; the moving parts (AOSP release cadence, device list, kernel LTS versions, MTE availability, build toolchain) must be learned from live official docs and re-checked each cycle.

## Key Findings

### 1. Contribution logistics (verified against grapheneos.org, 2026)
- **Source of truth for repos**: All OS sources live in the GitHub organization **github.com/GrapheneOS**, catalogued at **grapheneos.org/source**. A few dozen repos are GrapheneOS forks of AOSP or unique to GrapheneOS; the rest are unmodified AOSP referenced by the **`platform_manifest`** repo (`default.xml`). Note two repos have moved to GitLab: `platform_packages_modules_Connectivity` and the Pixel kernel monorepos (`kernel_pixel_6.1`, `kernel_pixel_6.6`).
- **Build/dev guide**: **grapheneos.org/build** is the canonical "building, modifying and contributing" document. It includes a "Development guidelines" section covering **Programming languages, Code style, and Library usage**.
- **Coding standards (verbatim from grapheneos.org/build)**: New low-level code should be **Rust with `no_std`** for hypervisor/kernel/daemon/system-library code; **C only in rare cases for very small, particularly low-level projects** such as hardened_malloc; **arm64 assembly in extremely rare cases**; **Python 3 for dev scripts under 500 lines**. The project explicitly aims to *avoid* writing new manual memory-management code and prefers memory-safe languages. Style: follow each language's official style (PEP8 for Python, rustfmt for Rust); otherwise 4-space indents, no tabs, `function_name`/`variable_name`/`TypeName`/`CONSTANT_NAME`.
- **Communication channels**: Official **Discord** (discord.com/invite/grapheneos), **Matrix** space `#community:grapheneos.org`, and a **Flarum forum at discuss.grapheneos.org** for long-form posts. The chat platforms are **no longer bridged** to each other. Issues go to the relevant GitHub issue tracker (see grapheneos.org/contact#reporting-issues). The project explicitly asks people **not to contact developers directly** for support/bugs/feature requests.
- **Stance on contributors / paid work**: GrapheneOS runs a **grapheneos.org/hiring** page for paid contractor roles (minimum 80 hours/month, fully remote, async). Stated expectations: strong command of (most→least common) Java, Kotlin, C++, C, Rust, JavaScript, TypeScript, arm64 assembly, Bash, Python; prior experience with AOSP-based OSes, the Linux kernel and its hardening, memory allocators, or Android app development; comfort with legacy codebases. This page is a useful proxy for the skill bar the project values even for volunteer contributions.

### 2. The technical stack, mapped to the two tracks

**NATIVE / SYSTEMS track (C/C++/Rust, kernel):**
- **`hardened_malloc`** (C, ~80% C) — the flagship native project. Its README (github.com/GrapheneOS/hardened_malloc/blob/main/README.md, ~1000 lines) is the authoritative design document. Design ideas to turn into curriculum objectives:
  - Security-focused general-purpose malloc; successor to an OpenBSD-malloc-based allocator. Per the README: *"It's still heavily based on the OpenBSD malloc design, albeit not on the existing code other than reusing the hash table implementation."* **64-bit only**; supports Bionic (Android), musl, glibc.
  - **Fully out-of-line metadata** in a separate protected region (rules out traditional allocator metadata-corruption exploitation).
  - **Separate memory regions** per size class / large allocations / metadata, each with high-entropy random bases and **no address-space reuse** between regions.
  - **Slab allocation** with fine-grained size classes and slabs beyond 4k to cut fragmentation.
  - **Guard pages/slabs**: guard regions around allocations >16k (randomized sizes for ≥128k); sub-16k allocations sit in slabs with guard slabs before/after.
  - **Random canaries with a leading zero** on small allocations (block C-string overflows, detect linear overflows, checked on free).
  - **Zero-on-free** with write-after-free detection (checks memory is still zero before reuse).
  - **Deterministic detection of invalid/double free**; delayed reuse via deterministic + randomized **quarantines** (mitigates use-after-free).
  - **Memory tagging (ARM MTE)** for slab allocations ≤128k: probabilistic detection of all use-after-free and inter-object overflows, deterministic detection of small/linear overflows.
  - Uses a ChaCha-based CSPRNG for randomness; no thread caching (security tradeoff); `default` vs `light` build variants.
  - Current dependency baseline (Debian 13): glibc 2.41, Linux 6.12, Clang 19.1.7 / GCC 14.2.0. Per the README, for Android *"the Linux GKI 6.1, 6.6 and 6.12 branches are supported. However, using more recent releases is highly recommended."* Latest release tagged "14" (Feb 2026).
- **`platform_bionic`** — hardened libc; the hardened_malloc↔Bionic integration commit lives here.
- **Kernel**: GrapheneOS forks AOSP's Generic Kernel Image (GKI) branches as **`kernel_common-6.1`, `-6.6`, `-6.12`** (Linux 6.1/6.6/6.12 LTS) with per-generation Pixel kernel prebuilt repos and the Pixel kernel *source* monorepos on GitLab (`kernel_pixel_6.1` for 6th–9th-gen Pixels, `kernel_pixel_6.6` for 10th-gen). Historically GrapheneOS ran the **linux-hardened** patchset (they state intent to revive it as a more active project). Kernel hardening features: 4-level page tables on arm64 (48-bit AS, 33-bit ASLR entropy vs 24-bit), MTE in slab/page_alloc/vmalloc allocators, leading-zero heap canaries in slub, zero-on-free in page allocator and slub, zeroed stack allocations, forced module signing (RSA-4096/SHA-256), lockdown confidentiality mode, BTI+CFI and PAC+SCS on ARMv9.
- **`Vanadium`** (Chromium fork) — exists, included as a prebuilt (too complex for the AOSP build system); **lower priority** for this learner.

**FRAMEWORK / PLATFORM track (Java/Kotlin, SELinux policy):**
- **`platform_frameworks_base`** — core of the app-sandbox/permission changes.
- **`platform_packages_modules_Permission`** — the Permission mainline module; likely home of Network/Sensors toggles and Scopes plumbing.
- **`platform_system_sepolicy`** — GrapheneOS's SELinux policy fork (they harden the app-sandbox SELinux + seccomp-bpf policy). Also `platform_external_selinux` (userspace SELinux libraries/tools).
- **`platform_packages_apps_Settings` / `SettingsIntelligence`** — UI surfaces for toggles/scopes.
- **`platform_packages_providers_ContactsProvider` + `platform_packages_apps_Contacts`** — Contact Scopes touch these.
- **`platform_system_vold`, `MediaProvider`, `DocumentsUI`** — Storage Scopes touch these.

### 3. Security features as learning objectives, sorted by layer

| Feature | Layer | Track |
|---|---|---|
| App sandbox (extends AOSP's UID isolation + SELinux) | Framework + kernel | Both |
| hardened_malloc integration | Native (libc/kernel-adjacent) | Native |
| Hardened kernel config / linux-hardened | Kernel | Native |
| Memory tagging (ARM MTE) | Hardware/kernel/allocator | Native |
| Exec-based ("secure") app spawning (replaces Zygote fork model) | Framework/runtime | Framework (with native implications) |
| Network permission toggle | Framework (INTERNET permission + second enforcement layer) | Framework |
| Sensors permission toggle | Framework | Framework |
| Storage Scopes | Framework (storage permission shim) | Framework |
| Contact Scopes | Framework (ContactsProvider) | Framework |
| SELinux policy hardening | Kernel-enforced, policy authored in userspace | Both (policy skills = framework track) |
| Verified boot / attestation (Auditor / AttestationServer) | Firmware + framework | Out of primary scope |
| Sandboxed Google Play | Framework compatibility layer | Framework |
| USB-C port control | Kernel + HAL + framework | Native-leaning |

**Exec-spawning detail (from grapheneos.org/usage)**: GrapheneOS spawns fresh processes via `exec` instead of cloning the Zygote template, so each app gets fresh ASLR/stack-canary/heap-canary/MTE secrets rather than sharing the boot-time Zygote's randomized values. Per grapheneos.org/usage, exec spawning *"adds somewhere in the ballpark of 200ms to app spawning time on the flagship devices and is only very noticeable on lower-end devices with a weaker CPU and slower storage."* Note the 2026 release notes mention Android 17 added a *native* zygote spawning system that GrapheneOS's secure spawning will need to be ported to — a live, moving area.

### 4. Build environment & device support (as of 2026 — VERSION-SENSITIVE)
- **Officially supported build targets** (from grapheneos.org/build, "Build targets"): Pixel 10a (stallion), Pixel 10 Pro Fold (rango), Pixel 10 Pro XL (mustang), Pixel 10 Pro (blazer), Pixel 10 (frankel), Pixel 9a (tegu), Pixel 9 Pro Fold (comet), Pixel 9 Pro XL (komodo), Pixel 9 Pro (caiman), Pixel 9 (tokay), Pixel 8a (akita), Pixel 8 Pro (husky), Pixel 8 (shiba), Pixel Fold (felix), Pixel Tablet (tangorpro), Pixel 7a (lynx), Pixel 7 Pro (cheetah), Pixel 7 (panther), Pixel 6a (bluejay), Pixel 6 Pro (raven), Pixel 6 (oriole). Plus the `sdk_phone64_x86_64` emulator target. **This list changes** — Google's five-year update window for the Pixel 6/6 Pro closes in October 2026 (Android 17 QPR1 being the final quarterly update), after which grapheneos.org/faq notes GrapheneOS provides only "extended support releases as a stopgap" that "cannot provide full security patches." Separately, Motorola announced a long-term partnership with the GrapheneOS Foundation at MWC 2026 on March 2, 2026; per The Register, GrapheneOS said the first supported devices "will be the 2027 devices meeting our requirements including the expected updates and hardware memory tagging" (flagships similar to the Motorola Signature / razr fold / razr ultra) — **not** current models.
- **"Best development devices are Pixels series 8 to 10"** (official) — these have MTE; older devices cannot exercise the most important hardened_malloc features.
- **Host requirements**: x86-64 Linux (Arch, Debian bookworm/12, Ubuntu 24.04 LTS or 24.10 officially supported); **32 GiB+ RAM** (LTO peaks during Vanadium/kernel CFI links are the constraint); **136 GiB+** storage for full sync with history (90 GiB+ lightweight), plus **100 GiB+** build space; `repo`, `python3`, `git`, `gnupg`, `openssh`, Node.js 24 LTS + yarn (for adevtool vendor extraction).
- **Current Android version**: GrapheneOS `17` branch = **Android 17**; `repo init -u https://github.com/GrapheneOS/platform_manifest.git -b 17`.
- **Toolchain / flow**: `repo` tool → `source build/envsetup.sh` → extract vendor files with **adevtool** → `lunch husky-cur-user` (Soong/Blueprint build system, `.bp` files) → `m target-files-package` → generate signing keys (`make_key`) → `script/generate-release.sh` → flash factory images. For a dev device you can `m` the default target and flash test-key-signed raw images with an unlocked bootloader. Emulator/userdebug is recommended for most development.
- **MTE**: available on Pixel 8/9/10-era Tensor devices (ARMv8.5-A+); enabled by default for parts of the OS on GrapheneOS.

### 5. Authoritative learning resources (full citations, free/paid flags, currency notes)

**C programming (stable core; C23 is the moving edge):**
- Brian W. Kernighan & Dennis M. Ritchie, *The C Programming Language*, 2nd ed., Prentice Hall, 1988, ISBN 978-0-13-110362-7. **PAID.** Currency: pre-ANSI-C99 classic; canonical for style/mental model, dated on modern standards — do not use as your only C source.
- Jens Gustedt, *Modern C*, 3rd ed. (covers C23), Manning, 2024 (2nd ed. 2019 ISBN 978-1-61729-581-2). **FREE** PDF from the author (gustedt.gitlabpages.inria.fr / Manning); print is paid. Currency: the best current free rigorous C book; 3rd ed. is C23-current.
- Robert C. Seacord, *Effective C: An Introduction to Professional C Programming*, 2nd ed. (C23), No Starch Press, 2025, ISBN 978-1-7185-0412-7. **PAID.** Currency: current; security-minded author (convenor of the C standards committee).
- K. N. King, *C Programming: A Modern Approach*, 2nd ed., W. W. Norton, 2008, ISBN 978-0-393-97950-3. **PAID.** Currency: C99-era but excellent pedagogy/exercises.

**Secure C coding (for hardened_malloc):**
- *SEI CERT C Coding Standard*, 2016 Edition, Carnegie Mellon University SEI, 2016. **FREE** PDF (resources.sei.cmu.edu). Currency: 2016 print snapshot of a live wiki (wiki.sei.cmu.edu/confluence/display/c) — use the wiki for current rules.
- Robert C. Seacord, *Secure Coding in C and C++*, 2nd ed., Addison-Wesley (SEI Series), 2013, ISBN 978-0-321-82213-0. **PAID** (out of print new; e-book/used available). Currency: dated on toolchain specifics but conceptually foundational.

**Systems programming / how computers work (stable):**
- Randal E. Bryant & David R. O'Hallaron, *Computer Systems: A Programmer's Perspective*, 3rd ed., Pearson, 2016 (2023 update), print ISBN 978-0-13-409266-9. **PAID.** Currency: current; x86-64-based — the single best bridge from "high-level programmer" to systems thinking.
- Michael Kerrisk, *The Linux Programming Interface*, No Starch Press, 2010, ISBN 978-1-59327-220-3. **PAID** (author hosts errata/code at man7.org/tlpi). Currency: 2010 but still the definitive Linux syscall/userspace-API reference; complements live man pages.

**Operating systems concepts (stable):**
- Remzi H. & Andrea C. Arpaci-Dusseau, *Operating Systems: Three Easy Pieces*, v1.10, University of Wisconsin, 2018+. **FREE** online (ostep.org). Currency: evergreen; ideal for a physics/AI background — virtualization, concurrency, persistence.

**Linux kernel development (moving; note dated texts):**
- Robert Love, *Linux Kernel Development*, 3rd ed., Addison-Wesley, 2010, ISBN 978-0-672-32946-3. **PAID.** Currency: **DATED (Linux 2.6-era)** — good for conceptual architecture, wrong on specifics; pair with kernel.org.
- Daniel P. Bovet & Marco Cesati, *Understanding the Linux Kernel*, 3rd ed., O'Reilly, 2005, ISBN 978-0-596-00565-8. **PAID.** Currency: **VERY DATED (2.6.11)** — reference only for deep subsystem intuition.
- **kernel.org / docs.kernel.org** — the authoritative moving target. Key process docs: `Documentation/process/submitting-patches.rst` (docs.kernel.org/process/submitting-patches.html), the Developer's Certificate of Origin / **Signed-off-by (DCO)** requirement, `submit-checklist.rst`, `coding-style.rst`. **FREE.**
- **kernelnewbies.org** — FirstKernelPatch, PatchPhilosophy tutorials. **FREE.**

**Memory allocators & exploitation/mitigation (defensive framing):**
- hardened_malloc README (GrapheneOS) — **primary design doc, FREE** (MIT).
- Otto Moerbeek, "A new malloc(3) for OpenBSD," EuroBSDCon 2009. **FREE** PDF (openbsd.org/papers/eurobsdcon2009/otto-malloc.pdf) — hardened_malloc's design ancestor.
- glibc Wiki, "Malloc Internals" (sourceware.org/glibc/wiki/MallocInternals, DJ Delorie). **FREE**, official. Plus sploitfun "Understanding glibc malloc" (2015). **FREE.**
- Michel Kaempf ("MaXX"), "Vudo malloc tricks," and anonymous, "Once upon a free()," *Phrack* #57, Aug 2001 (phrack.org/issues/57/8 and /9). **FREE** — historical/defensive heap-exploitation primers.
- Shellphish, **how2heap** (github.com/shellphish/how2heap). **FREE** — glibc heap-exploitation techniques organized by glibc version; defensive study.
- Maria Markstedter, **Azeria Labs** tutorials (azeria-labs.com). **FREE** — ARM assembly + heap/stack exploitation.

**Exploit-mitigation & ARM architecture background:**
- *Arm Architecture Reference Manual for A-profile architecture*, ARM DDI 0487 (latest issue; **M.b** as of 2026, prior L.b). **FREE** (developer.arm.com/documentation/ddi0487/latest). Currency note: Arm revises ~twice yearly and "latest" always redirects — cite the specific issue letter you download.
- Arm, "Armv8.5-A Memory Tagging Extension" white paper, 2019. **FREE** (developer.arm.com). Covers the 4-bit-tag/16-byte-granule lock-key model, TBI, sync/async modes.
- Arm, "Providing protection for complex software" (Learn the Architecture; PAC + BTI + MTE), 2019. **FREE** (developer.arm.com).
- Maria Markstedter, *Blue Fox: Arm Assembly Internals and Reverse Engineering*, Wiley, 2023, ISBN 978-1-119-74530-3. **PAID.** Currency: current, ideal AArch64 on-ramp for reading disassembly.

**Android internals / AOSP (mix of official-current and dated-respected):**
- **source.android.com** — official AOSP docs (build system, HALs, framework, security model, SELinux). **FREE**, the authoritative moving target. Note: from 2026 AOSP source publishes to `android-latest-release` in Q2/Q4 (trunk-stable model).
- Nikolay Elenkov, *Android Security Internals: An In-Depth Guide to Android's Security Architecture*, No Starch Press, 2014/2015, ISBN 978-1-59327-581-5. **PAID.** Currency: **DATED (≈Android 4.4/5)** but the most rigorous single treatment of the security model, permissions, Binder IPC, SELinux (Ch. 12) — concepts hold, specifics have drifted.
- Jonathan Levin, *Android Internals: A Confectioner's Cookbook, Volume I — The Power User's View*, 2nd ed. (Android 13), Technologeeks Press, 2021/2022, ISBN 978-0-9910555-8-6 (Vol II "Developer's View," ISBN 978-0-9910555-4-8). **PAID**, expensive. Currency: respected, deeply detailed; 2nd ed. is reasonably current (Android 13), still pre-17.
- René Mayrhofer, Jeffrey Vander Stoep, Chad Brubaker, Dianne Hackborn, Bram Bonné, Güliz Seray Tuncay, Roger Piqueras Jover, Michael A. Specter, **"The Android Platform Security Model (2023),"** arXiv:1904.05572 (v3, Jan 2024). **FREE** (arxiv.org/abs/1904.05572). The canonical academic statement of Android's multi-party-consent threat model — foundational reading for the framework track.

**SELinux / Android sepolicy:**
- **source.android.com/docs/security/features/selinux** (concepts, implement, customize, build, validate). **FREE**, official/current. Core rule form: `allow source target:class permissions;`; `.te` files; CIL; per-domain permissive; `getenforce`/`sepolicy-analyze`.
- Richard Haines, *The SELinux Notebook*, 4th ed. (freely distributed; also mirrored via the SELinux project / GitHub). **FREE.** Currency: comprehensive reference maintained alongside upstream SELinux.
- Frank Mayer, Karl MacMillan & David Caplan, *SELinux by Example: Using Security Enhanced Linux*, Prentice Hall, 2006, ISBN 978-0-13-196369-6. **PAID.** Currency: DATED but still the clearest policy-language tutorial.

### 6. Calibration: stable vs moving vs contested
- **STABLE / SETTLED** (learn once from books): core C language and POSIX APIs; fundamental OS concepts (virtual memory, scheduling, processes/threads); computer-architecture fundamentals; heap-allocator first principles; the *abstract* Android security model (multi-party consent, UID sandboxing, SELinux MAC over DAC); SELinux policy language semantics.
- **MOVING / VERSION-SENSITIVE** (re-check every cycle from live docs): AOSP release (Android 17 now; annual + 2026 Q2/Q4 trunk-stable drops), supported Pixel list, kernel LTS versions (6.1/6.6/6.12), the Soong/`m`/`lunch` toolchain details, adevtool vendor extraction, C23 features, the ARM ARM revision letter, MTE hardware availability, and the exec-spawning port to Android 17's native zygote.
- **CONTESTED / HYPE-PRONE** (flag in curriculum, reason from primary sources):
  - *MTE effectiveness*: probabilistic for use-after-free/inter-object overflows (4-bit tags → ~1/16 chance a random collision evades detection), deterministic only for specific linear-overflow/adjacent cases — powerful but not absolute; GrapheneOS's own README is careful about this, marketing summaries often are not.
  - *"Military-grade"/absolute-security marketing* around GrapheneOS features (seen on third-party/reseller sites) — not the project's own framing; the project explicitly positions itself as raising exploitation *difficulty/cost*, defense-in-depth, not invulnerability.
  - *Zygote vs exec-spawning tradeoff* is a real, debated performance/security compromise, not a free win.
  - Third-party "supported devices" and feature blogs drift out of date fast; treat only grapheneos.org as authoritative.

### 7. Realistic first-contribution on-ramps

**Both tracks first (weeks, not skipped):** Get the build-flash loop working on the emulator and on your Pixel; read grapheneos.org/build, grapheneos.org/source, grapheneos.org/features and grapheneos.org/usage end-to-end; lurk the forum + Discord #dev; read closed PRs in the target repos to learn review norms.

**Native/systems on-ramp:**
1. Build hardened_malloc standalone (`make`), run `make test`, run apps under `preload.sh` on a normal Linux box — no phone needed. Read the entire README and correlate each security property to code in `h_malloc.c`, `slab.c`, guard/quarantine logic, `arm_mte.h`.
2. Approachable first work: documentation/README clarifications; portability/build fixes; new automated tests; small config-plumbing; triaging/reproducing issues on the open issue tracker (31 open issues as of Sept 2026). hardened_malloc is deliberately small and self-contained — the best possible native entry point.
3. Kernel: reproduce a kernel-config hardening option, study a linux-hardened patch, then attempt a genuinely trivial upstream-style fix following kernel.org's submitting-patches + DCO before touching GrapheneOS kernels.

**Framework/SELinux on-ramp:**
1. Read the Mayrhofer security-model paper + source.android.com SELinux docs + Elenkov (concepts).
2. Approachable first work: SELinux `.te` policy refinements (denials show up in `dmesg`/`logcat` — a concrete, testable feedback loop); Settings UI strings/behavior around existing toggles; small bug fixes in the Contacts/Storage scope plumbing reproduced against a real denial or crash.
3. Study how an existing toggle (e.g., Network permission's second enforcement layer) threads through `frameworks_base` + `packages_modules_Permission` + Settings as a worked example before proposing changes.

## Details

### Suggested phasing (for the eventual markdown curriculum)
- **Phase 0 — Environment (2–4 wks):** Linux host, `repo`, build hardened_malloc standalone + one full AOSP emulator build + one flash to the Pixel. Deliverable: a working build-flash-iterate loop. *Free resources: all official docs + OSTEP.*
- **Phase 1 — C & systems fundamentals (3–5 mo, the learner's real gap):** *Modern C* (free) as spine + K&R for idiom + CS:APP (the crucial bridge) + OSTEP (free) in parallel. Exercises in C daily. Add SEI CERT C (free) once comfortable. Benchmark to advance: can read/modify `h_malloc.c` and explain guard slabs, canaries, quarantines.
- **Phase 2 — Track split.**
  - *Native:* TLPI + hardened_malloc deep dive + OpenBSD-malloc paper + glibc internals + how2heap (defensive) + ARM ARM/MTE/PAC docs + *Blue Fox*; then Love/kernel.org for kernel work. Benchmark: a merged doc/test/portability PR to hardened_malloc.
  - *Framework/SELinux:* Mayrhofer paper + Elenkov + source.android.com (framework + SELinux) + *SELinux by Example*/Notebook; read GrapheneOS's sepolicy + Permission module. Benchmark: a reproduced SELinux denial fixed locally and proposed upstream.
- **Phase 3 — Sustained contribution:** pick issues, engage on Discord #dev/forum, iterate on review.

### MVP fast-track (compressed, if the learner wants a native contribution ASAP)
Modern C (skim, do exercises) → CS:APP chapters 1–3, 6, 9 (machine code, memory hierarchy, virtual memory) → hardened_malloc README + code + `make test` → ARM MTE whitepaper → a documentation/test/portability PR. This skips the kernel and framework entirely and exploits hardened_malloc's small, self-contained nature.

## Recommendations
1. **Start the build loop in week 1, in parallel with C study — do not wait until you "know enough."** The heavyweight toolchain (32 GiB RAM, ~236 GiB disk, Android 17 `17` branch) is itself a multi-day learning curve; getting an emulator build + a Pixel flash working early de-risks everything. Threshold to proceed: a reproducible `m` build and a successful flash.
2. **Choose hardened_malloc as the anchor for the native track.** It is the rare GrapheneOS component that is small, MIT-licensed, self-documenting, buildable without a phone, and central to the project's identity. It is the highest-leverage place for a strong-fundamentals newcomer to reach a first merged PR.
3. **For the framework track, make SELinux policy your wedge.** Denials produce concrete `dmesg`/`logcat` signals, giving a tight, testable feedback loop that suits a formally-minded learner, and sepolicy is a discrete, well-bounded skill.
4. **Treat every version-sensitive fact as perishable.** Re-verify the supported-device list, Android version, kernel LTS, and toolchain from grapheneos.org each time you sync. Do not trust third-party "supported devices" blogs.
5. **Lead with your strengths.** Your Python/Bash and mathematical-reasoning skills map directly onto the project's scripting needs and onto threat-model/formal-property reasoning (MTE probabilities, quarantine guarantees). Frame your ML/fraud background as adversarial-thinking experience.
6. **Prefer Rust for any *new* non-trivial code you propose.** The project's own guidelines push new low-level code toward Rust `no_std`; C is reserved for rare cases like hardened_malloc. Learning enough Rust alongside C will align you with where the project is going.
7. **Benchmarks that should change your plan:** if you cannot comfortably read `h_malloc.c` after Phase 1, extend C fundamentals before attempting a PR; if MTE hardware matters to your work and your Pixel is pre-Pixel-8, budget for a Pixel 8–10; if the kernel track stalls, pivot to hardened_malloc or SELinux where the feedback loops are faster.

## Caveats
- **Version snapshot:** all device lists, Android/kernel versions, dependency baselines, and the ARM ARM revision are as of 2026 and will drift; the report flags each. GrapheneOS was tracking **Android 17** and Linux **6.1/6.6/6.12** LTS at the time of research.
- **No explicit CLA/DCO for GrapheneOS itself was found in public docs.** The project uses GitHub PRs and permissive licensing (MIT/Apache-2.0); contributors should confirm current signoff/licensing expectations in each repo's CONTRIBUTING/README and via the forum before submitting. (The kernel.org DCO/Signed-off-by requirement applies specifically to *upstream Linux* patches.)
- **Some supporting details came from secondary sources** (Wikipedia for the written-in-languages summary and release dates; The Register/Android Police for the Motorola and Pixel-6-EOL items; third-party guides for feature explanations). Where possible these were corroborated against grapheneos.org primary pages; treat marketing-flavored third-party claims (especially "military-grade"/absolute-security language) with skepticism.
- **The paid Android-internals books (Elenkov, Levin) are respected but dated** relative to Android 17; use them for durable concepts and always cross-check specifics against source.android.com.
- **Heap-exploitation resources (Phrack, how2heap, Azeria) are included strictly for defensive understanding** of the vulnerability classes hardened_malloc mitigates — appropriate for security engineering, not offensive use.
- **Timeline estimates assume serious part-time study** (~8–12 h/week) by someone strong in another language; they are planning aids, not guarantees.