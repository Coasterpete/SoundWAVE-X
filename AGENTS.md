# SoundWAVE X — Development Instructions for Coding Agents

> **Product mission:** Start creating immediately. Go professional when ready.
>
> **Status:** SoundWAVE X is an early, independent Rust DAW project derived from SoundCraft. Many crates, package names, file names, commands, and screens still say `soundcraft`. Do not confuse inherited functionality with a finished SoundWAVE X feature.

## 1. Product identity and non-negotiable goals

SoundWAVE X is a **free, open-source, content-first digital audio workstation** combining:

1. **Easy audio editing** inspired by the *accessibility* of Audacity and WavePad: open a file, select a waveform, trim or repair audio, preview an effect, and export without learning studio routing first.
2. **Immediate music creation** inspired by the *creative readiness* of GarageBand and Logic Pro: ready-made, properly licensed loops, one-shots, drum kits, instrument presets, starter songs, and sound effects. A blank timeline is an option, not the only starting point.
3. **Professional depth on demand:** multitrack production, MIDI, plugin hosting, automation, sends, buses, advanced routing, and mastering tools remain accessible as users grow.

The tagline is **“Start creating immediately. Go professional when ready.”** This is a product requirement, not only marketing copy.

**Do not** treat Pro Tools menu parity, reproducing another application's UI, agent automation, or sheer feature count as the primary objective. Those are inherited SoundCraft concerns and are secondary to usable creation workflows. Observe common interaction patterns, but build an original SoundWAVE X interface and identity.

### Experience requirements

- A new user must be able to open/import an audio file, edit it, audition an effect, and export without configuring buses, plugins, or a complex session first.
- A new user must be able to launch a music project, browse useful sounds, preview one, place it on a track, press play, save, and reopen successfully.
- Avoid modal friction, hidden prerequisite setup, jargon-only labels, and empty screens with no suggested next action.
- Do not hide or delete advanced systems to make the interface simpler; make them discoverable progressively.
- Preserve keyboard shortcuts, undo/redo, accessible labels, tooltips, visible state, and sensible defaults. Aim for an efficient high-contrast professional application, not a toy/game aesthetic.
- Prefer a coherent workflow over a collection of disconnected demo screens.

## 2. How to start a coding session

1. Read **this file**, `README.md`, and `ROADMAP.md`. Inspect the actual source, manifests, tests, and relevant `docs/` pages before proposing changes.
2. Establish what exists by running code or examining tests. Distinguish **working**, **partial**, **stub**, and **planned**. Do not claim a feature exists merely because a menu item or module exists.
3. Inspect `git status`, the current branch, and any uncommitted user work. Do not discard it.
4. For substantial tasks, write a concise implementation plan with measurable outcomes, then implement an **integrated, end-to-end working pass** rather than stopping after scaffolding or multiple tiny placeholder milestones.
5. After implementation, build, exercise the relevant UI and audio path when possible, run tests, and update documentation with actual results and limitations.

**Owner preference:** Substantial one-shot Codex work is welcome when well scoped. An integrated pass may span UI, engine, data model, content, and tests. Keep logical commits, but don't split usable functionality into endless micro-prompts.

## 3. Existing foundation: preserve and evolve

The imported SoundCraft Cargo workspace includes these main layers (verify current paths before editing):

| Area | Existing crates | Role |
|---|---|---|
| Time, formats, MIDI | `crates/time`, `crates/audio-io`, `crates/midi` | Timebases, import/export, MIDI data |
| DSP | `crates/dsp` | Audio processing, instruments, effects |
| Session data | `crates/model` | Tracks, clips, automation, routing |
| Mixing | `crates/mix` | Realtime/offline mixing |
| Operations | `crates/engine`, `crates/playback` | Commands, editing, recording, devices |
| Plugin hosts | `crates/clap-host`, `crates/vst3-host`, `crates/au-host` | Third-party plugin integration |
| Automation | `crates/automation` | Command/control interfaces |
| GUI | `crates/ui-egui` | egui/eframe application interface |
| Apps | `apps/*` | Desktop, CLI, web entry points |

- Prefer extending existing stable subsystems to reinventing audio, MIDI, or mixing engines.
- Preserve the separation between the UI and audio/session engine. The UI should dispatch engine commands rather than duplicate edit logic.
- Inherited command IDs and crate names may remain during the transition. Rename incrementally and atomically with tests; do not perform a cosmetic mass rename that breaks working builds.
- Preserve cross-platform architecture where feasible. **Windows 11 is the primary initial development and validation platform**, not the only long-term target.
- Existing SoundCraft documentation can remain as historical/technical reference where relevant, but SoundWAVE X's roadmap and acceptance gates are authoritative for new product priorities.
- Do not depend on a sibling checkout such as `../craftrules`, local Pro Tools installations, macOS screenshots, or directories outside this repository to perform routine development. Document optional upstream context instead.

## 4. Integrated product workstreams

### A. Quick Edit (beginner-friendly waveform workflow)

- Open/import WAV and other supported formats directly into an obvious edit view.
- Select, split, trim, move, crop, fade, normalize/gain, undo, preview effects, and export.
- Make destructive vs. nondestructive operations explicit and safe; preserve originals and undo history.
- Reduce confusion between AudioSuite-style offline rendering and realtime mixer inserts by explaining the distinction in UI language.

### B. Factory Library and creative content (core differentiator)

- Build a scalable first-party **Library Browser**: categories, tags, text search, audition, favorites, metadata, file availability, and drag-and-drop import.
- Plan native support for one-shots, tempo-labeled loops, MIDI patterns, presets, and full starter projects.
- Provide tempo/key metadata and transparent stretching/tuning controls where supported; do not silently damage audio or pretend tempo matching exists if it does not.
- Seed with a **small, useful, verified, redistributable** set, then expand curated content and optional free packs. Do not ship a fake browser with placeholder sounds or merely relabel the generated demo as a factory library.
- Treat organized, ready-to-use **actual audio content** as a release requirement, not an optional enhancement or something users must create themselves.
- Keep content separate from executable code where practical, with explicit versioned manifests and optional pack installation. Avoid making the initial executable unnecessarily massive.

### C. Create Music

- Starter project templates for drums, songs, podcasts, and sound design.
- Intuitive MIDI piano roll, step sequencing, drum patterns, preset-driven instruments, easy loop arrangement.
- Generative/procedural patterns are welcome as **additions to**, not replacements for, real premade loops and samples.

### D. Advanced Studio

- Retain and improve routing, buses, sends, plugin chains, MIDI, recording, automation, multitrack mixing, and mastering.
- Progressive disclosure: discoverable advanced panels/workspaces without blocking simple editing.

### E. Hardware and platform resilience

- Good defaults, device enumeration and selection, sample rate/buffer controls, loss/reconnect handling, useful errors, and durable user preferences.
- Exercise speakers, wired/Bluetooth headphones, USB interfaces, and other ordinary working Windows outputs where available. Never require switching to a different device as the only workaround.

## 5. Real-time audio and data-safety rules

These inherited SoundCraft safeguards remain critical:

- **Audio callback:** no allocations, locks, waiting, disk I/O, panic, or logging in steady-state real-time paths.
- Validate external files, metadata, plugin parameters, sizes, audio sample counts, and numeric input. Reject invalid operations safely; avoid unbounded allocations and NaNs.
- Avoid panics in production code; prefer fallible APIs and actionable errors. Isolate any necessary `unsafe` for plugin FFI with documented invariants.
- Recording should prioritize data retention, recoverability, autosave, consistent session state, and handling unexpected device loss.
- Test nondestructive editing, undo/redo, import/export roundtrips, waveform bounds, sample-rate changes, loop boundaries, session reopen, and missing-media scenarios.
- Do not remove existing regression coverage for styling or rebranding work.

## 6. Copyright, attribution, trademarks, and factory assets

- Preserve the imported SoundCraft copyright notices, commit history, applicable `LICENSE-MIT`, `LICENSE-APACHE`, `NOTICE`, and `ATTRIBUTION.md` terms. The software code currently declares `MIT OR Apache-2.0`; independently licensed third-party assets do **not** inherit that license automatically.
- **Do not use ArtCraft names/logos/wordmarks/icons as SoundWAVE X branding.** Remove protected brand assets from modified product distributions as required by their separate license; keep truthful textual credit to the SoundCraft/ArtCraft contributors.
- Do not copy Avid, Apple, Adobe, or other proprietary samples, loops, presets, icons, screenshots, fonts, bundled instruments, or application assets.
- Bundle an asset only when the rights to **redistribute that raw asset in a DAW/library** are documented, not merely permission to use it inside a song. Prefer original material and verified CC0; CC-BY and other compatible content need attribution and term review.
- For every bundled asset, record at least `path`, `name`, `creator`, `source URL/provenance`, `license`, `version/date`, and any attribution requirements in an auditable manifest. Keep `ATTRIBUTION.md` updated and preserve existing asset checks.
- Do not assume an online uploader owns their audio or that a label like “royalty-free” grants sample-pack redistribution rights. Handle ambiguous licensing by excluding the asset.
- Track factory sounds, user files, and third-party downloaded packs distinctly. Never silently upload or transmit user recordings.

## 7. Working commands (current imported baseline)

From the repository root on Windows PowerShell:

```powershell
cargo run --release -p soundcraft -- --demo
cargo test --workspace
cargo xtask ci
```

These are **inherited commands**, not the final SoundWAVE X executable names. Verify any changes to Cargo manifests and launch commands. `cargo xtask ci` may contain inherited parity/branding checks that need to be re-scoped as part of the migration; report baseline failures rather than bypassing them.

When building UI work, inspect actual visual results and user flows, not only compiler output. Record explicit pass/fail evidence. Do not imply Windows validation proves other platforms.

## 8. Completion criteria for integrated passes

A pass is not complete unless it:

1. Delivers a usable end-to-end user workflow, not only architecture or a mock screen.
2. Preserves existing supported audio/edit functionality and upstream legal notices.
3. Includes error handling, tests, and at least a manual validation checklist for GUI/audio behaviors.
4. Builds on its stated platforms (or explicitly documents blockers).
5. Updates `README.md`, `ROADMAP.md`, and relevant technical docs to distinguish **done**, **partial**, and **planned**.
6. Reports source files changed, executed validation, known limitations, and next dependencies truthfully.

## 9. Release philosophy

Release quality is measured by: **time to first sound**, **first successful edit/export**, **first loop-based musical arrangement**, **reliability with everyday audio devices**, **content quality/licensing**, and **professional depth without beginner friction**.

Do **not** report SoundCraft's Pro Tools parity percentages as SoundWAVE X readiness. Treat SoundWAVE X as its own product with its own measured acceptance gates. Never market an unimplemented loop library, feature, or supported platform as shipped.
