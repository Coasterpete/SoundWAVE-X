# SoundWAVE X — Product Roadmap

> **North star:** Start creating immediately. Go professional when ready.
>
> **Stage:** Foundation / pre-alpha fork. **Status of this document:** proposed product roadmap, not a release announcement. No dates or percentages below imply delivery.

## 1. Why SoundWAVE X exists

The project is not a Pro Tools-parity race. Its aim is to unite **Audacity/WavePad-like accessibility**, **GarageBand/Logic-style creative starting content**, and **advanced studio capability** in a free, open-source Rust application.

Users should be able to succeed immediately with an audio file *or* a premade musical idea. Advanced editing, MIDI, routing, automation, plugin hosting, and mastering should remain available once needed.

## 2. Current baseline vs. SoundWAVE X goals

| Area | Imported SoundCraft foundation | SoundWAVE X-specific work |
|---|---|---|
| Rust audio/session engine | Present; needs fork validation | Preserve, harden, extend |
| Multitrack editing/mixing | Present in upstream; usability varies | Make common tasks clear and approachable |
| Waveform editing | Existing edit operations | Simple Quick Edit entry point and effect preview |
| MIDI/instruments | Existing support, with upstream limitations | Easy creation flows and guided patterns |
| Factory loops / samples | No substantial redistributable music-loop library established in this fork | Curate and ship real legal content + metadata |
| Audio devices | Existing playback/device code; coverage and resilience require testing | Reliable Windows selection, loss recovery, appropriate defaults |
| App identity | Imported SoundCraft names and ArtCraft references | Original SoundWAVE X branding, app IDs, preferences, docs |
| Source/license | MIT OR Apache-2.0 code with upstream notices | Keep provenance and license obligations; license assets separately |

**Evidence rule:** A compiled crate, README claim, or menu item is not proof of an end-to-end user workflow. Verify functionality on the fork and publish reproducible outcomes.

## 3. Product acceptance measures

We will evaluate the product by outcomes rather than an inherited competitor's menu count:

1. **First sound:** a user can select a starter project/loop and hear audio through a working device without manual signal routing.
2. **First edit:** a user can open their own audio file, make a reversible edit, preview an effect, and export.
3. **First song:** a user can audition, drag in, duplicate, and arrange multiple ready-made loops, save, reopen, and export.
4. **Factory library:** assets are real, discoverable, useful, nonplaceholder, clearly licensed for raw-asset redistribution, and auditable.
5. **Recording resilience:** common Windows outputs and inputs work, device interruptions are recoverable, and recordings/sessions are safeguarded.
6. **Depth and performance:** professional features remain available without making basic tasks confusing or degrading interactive audio reliability.

## 4. Integrated development passes

### Pass A — Independent identity + first complete creator journey

**Goal:** Turn the imported codebase into an honestly branded SoundWAVE X *development build* with a useful first-time workflow.

**Scope:**

- Establish a clean new brand and app identity: application title, original icon and splash/welcome experience, repository metadata, consistent documentation, independent settings paths where practical, without losing attribution to SoundCraft contributors.
- Remove protected ArtCraft branding from the derivative interface/distributed assets; preserve `NOTICE`, copyright notices, original commit history, and attribution.
- Verify a clean Windows build, tests, audio playback and core edit/import/export behavior in the imported repository; preserve the command architecture.
- Build a beginner-friendly start screen offering **Edit Audio**, **Make Music**, **Open Project**, and **Advanced Studio** (or equivalently clear workflows). Buttons must open actual functional destinations, not decorative placeholders.
- Deliver a focused **Quick Edit** journey: open audio, see waveform, select/trim/split, apply or preview a straightforward effect safely, undo, export.
- Deliver a first **Create Music** journey: load a small verified seed library with searchable categories and audition, drag a sound into the timeline, playback, save/reopen, and export. The seed should contain actual licensed audio, not only the code-generated demo.
- Add tests and UI validation for complete user journeys, including empty/missing/corrupt library entries.

**Exit gate:** Both journeys work on the stated test system, and the UI makes it clear how a beginner starts. A README build/test recipe reproduces results. No unsupported branding or unlicensed bundled sounds.

### Pass B — Meaningful factory library and approachable music tools

**Goal:** Make creating something musical easy without personally programming or composing every sound.

**Scope:**

- Versioned sound-pack manifest (creator/source/license, type, key, tempo, bars, tags, preview duration, checksum where appropriate); reliable indexing, search, favorites, preview, and user/optional pack locations.
- Build an initial **curated** library with original/verified redistributable loops, one-shots, drum kits, ambient audio, and sample instrument presets. Publish an actual audited asset count, not a target marketed as complete.
- Add optional **free** expansion packs so the core installer stays manageable; handle missing/outdated packs gracefully.
- Offer premade MIDI beats, basslines and chord patterns, simple drum sequencing, template sessions, and ready-to-play presets.
- Implement visible project tempo/key controls and safe, tested tempo synchronization for properly tagged loops. Clearly mark unsupported cases.
- Make the library tightly integrated with the arrangement/timeline; avoid content that requires external setup.

**Candidate content target (aspirational, subject to rights and quality review):** ~200 one-shots, 100 audio loops, 100 MIDI patterns, 40 presets, 60 SFX/ambiences, and 5 starter projects. **None of these are counted as shipped yet.** A smaller excellent legal library beats a huge low-quality or unlicensed one.

**Exit gate:** A beginner can make and export a short multi-track piece from included content, with no additional sample purchase or programming.

### Pass C — Reliable editing, recording, and audio hardware

**Goal:** Make real projects dependable, not just impressive demos.

**Scope:**

- Streamline familiar edit actions, intuitive effects, non-destructive processing, reusable presets, selection behavior, history, backup, and session reopen.
- Device discovery/selection and persistence; reliable playback/recording through working speakers, wired and Bluetooth headphones, USB interfaces, plus diagnostics and device-loss recovery.
- Improve recording workflows, disk persistence, latency and buffer handling, monitoring, and clear routing defaults.
- Expand importer/exporter tests and large-file/session robustness; keep projects stable under missing media and plugin errors.
- Add beginner-focused in-product help, useful tooltips, discoverable shortcuts, and quick-start templates.

**Exit gate:** Recording, editing, mixing, exporting, and restoring sessions succeed in repeatable real-world tests on the claimed supported configurations.

### Pass D — Advanced Studio without added beginner friction

**Goal:** Keep the full professional ceiling.

**Scope:**

- Mature plugin workflow, buses, sends, automation, mixer customization, MIDI recording/authoring, routing, advanced monitoring, and mastering.
- Flexible docking/multidisplay workflows, high-contrast UI, keyboard-first editing, accessibility review.
- Improve sound-design tasks, batch workflows, and advanced project interoperability based on demonstrated creator demand.
- Preserve advanced engine APIs/CLI control where useful, but do not prioritize parity metrics over creative workflows.

**Exit gate:** Advanced functions are discoverable and powerful while Quick Edit and Create Music remain simple and performant.

## 5. Alpha → Beta → 1.0 gates

| Gate | Required evidence |
|---|---|
| **Alpha** | Independent branding/licensing compliance; usable Quick Edit and sample-based Create Music journeys; verified Windows build; clear bug/limitations list |
| **Beta** | Robust legal factory library + expansion path; project persistence; stable major edit/music workflows; repeated hardware/device and import/export testing; sensible onboarding |
| **1.0** | Meaningful ready-made creative collection; dependable audio-editing and music workflow; polished usability and accessibility; reliable save/recovery/export; release packaging and transparent platform support |

All gates are **provisional** and based on working outcomes, not fixed dates or an inherited Pro Tools parity percentage.

## 6. Technical and quality foundations

- **Primary platform for initial testing:** Windows 11. Preserve existing cross-platform Rust boundaries; claim macOS/Linux/web support only when validated for the changed build.
- Preserve stable existing crates for DSP, mixing, editing, MIDI, audio I/O, UI, and commands unless a targeted replacement demonstrably improves the product.
- Keep real-time audio callback allocation-free and nonblocking; protect user recordings, undo data, and session integrity.
- Required recurring checks: Rust format/lints/tests as applicable, `cargo test --workspace`, `cargo xtask ci` after inherited checks are brought into scope, and interactive validation of the specific workflows changed.
- Incremental crate renaming only with passing builds and compatibility plan. Do not spend early development exclusively on cosmetic renaming.
- Track upstream security fixes and useful engine improvements deliberately, not via uncontrolled merges.

## 7. Licensing and content sourcing policy

- Imported SoundCraft code: preserve applicable `MIT OR Apache-2.0`, `LICENSE-*`, `NOTICE`, `ATTRIBUTION.md`, and contributor credit/history.
- ArtCraft visual trademarks are not permitted as SoundWAVE X product branding. Retain accurate textual upstream credit.
- Factory sounds must be original or specifically licensed for **redistribution of the raw audio as a bundled sound library**. Prefer verified CC0; compatible permissive licenses require their own checks and attribution.
- Track every asset's provenance, license, pack and checksum; exclude dubious rights or noncommercial/restricted material.
- An allowed-to-use loop from an existing commercial DAW does **not** automatically carry permission to bundle or redistribute it.

## 8. Immediate first work package

**Before feature development:** validate the imported fork from a clean Windows build and document results; inventory ArtCraft-only branding/assets and verify license files remain intact.

**Then pursue Pass A as a single integrated implementation effort**: identity, two real beginner journeys, seed licensed sounds/library browser, end-to-end playback/save/export, tests, and updated documentation. Avoid a sequence of prompts that each produce only scaffolding or isolated UI mockups.

**Success is not a prettier empty SoundCraft window.** Success is a new user opening SoundWAVE X and making something immediately.
