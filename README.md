# SoundWAVE X

**Start creating immediately. Go professional when ready.**

SoundWAVE X is an early-stage, **free and open-source digital audio workstation (DAW)** built in Rust. Our goal is to make everyday audio editing feel straightforward while bringing ready-to-use loops, samples, instruments, and full multitrack production into one creative workspace.

**Project status: Early development / SoundCraft-based foundation.** The repository currently contains an imported version of SoundCraft. Much of the executable and source code is still named `soundcraft`. The content-first SoundWAVE X experience described below is **a direction and planned product**, not a finished feature set.

## What we're building

SoundWAVE X combines three experiences in one application:

| Workspace direction | What it should feel like | Intended tasks |
|---|---|---|
| **Quick Edit** | Straightforward waveform editing | Open, cut, trim, fade, process, preview, export |
| **Create Music** | Inspiring from the moment you start | Browse and audition factory loops, drag them into a song, add drums/instruments/MIDI |
| **Advanced Studio** | Detailed when you need it | Record, automate, route buses/sends, host plugins, mix, master |

These are **proposed user workflows**, not claims that separate SoundWAVE X workspaces are implemented today.

### Content-first, not blank-canvas-only

A central goal is a **genuinely useful, redistributable factory sound library**: ready-made loops, drum one-shots, musical phrases, virtual instrument presets, sound effects, and starter projects. Content should be easy to search, preview, and drag into a session. Procedural beat/MIDI tools can supplement those sounds, but must not substitute for real ready-made assets.

We intend to ship a curated starter collection and allow optional free library expansions. Factory content will be original or properly licensed for redistribution; different audio assets may have different licenses and attribution requirements.

## What's available now?

The imported SoundCraft foundation provides substantial Rust implementations and existing interfaces for multitrack editing, a mixer, MIDI and instruments, effects, recording-related functions, file I/O, plugin hosting, and automation. **Some workflows are incomplete or rough.** A compiled feature is not automatically a validated, reliable user experience.

**Not yet delivered as a SoundWAVE X feature:** the beginner-first Quick Edit workflow, a curated factory loop/sample library, a unified beginner-first welcome screen, and the production-ready SoundWAVE X identity. These are planned workstreams.

## Build the current foundation on Windows

Prerequisites:

- Windows 11 (primary development/test environment)
- Git
- Rust toolchain with Cargo (the imported desktop UI currently expects Rust **1.95 or later**)
- Visual Studio C++ build tools / Windows SDK for the MSVC target

In PowerShell:

```powershell
cd C:\DEV1
git clone https://github.com/Coasterpete/SoundWAVE-X.git
cd SoundWAVE-X
cargo run --release -p soundcraft -- --demo
```

`--demo` loads the inherited SoundCraft **Midnight Groove** generated demonstration, **not** the planned SoundWAVE X sound library. The build target and executable remain `soundcraft` until the rebrand is implemented safely.

To validate the imported workspace:

```powershell
cargo test --workspace
cargo xtask ci
```

Some inherited checks or platform-specific tests may require adjustment as the fork evolves; document failures accurately rather than suppressing them.

## Development direction

Our first integrated development goals are:

1. Establish a legally clean SoundWAVE X identity while maintaining a working build and preserving upstream attribution.
2. Make the first editing and music-creation sessions dramatically easier to start and understand.
3. Introduce a real, license-verified sound-library browser and an initial usable set of loops, one-shots, patterns, and presets.
4. Connect browsing, auditioning, drag-and-drop, editing, playback, save/reopen, and export into cohesive user workflows.
5. Improve recording, plugin, hardware-device reliability, and advanced studio tools over time.

See [ROADMAP.md](ROADMAP.md) for **proposed**, **in progress**, and **validated** outcomes. Contributors and coding agents should read [AGENTS.md](AGENTS.md).

## Principles

- **Create first, configure later.** A beginner should not need to understand buses to edit one audio file or build a basic beat.
- **Real content, not pretend features.** Do not advertise placeholder packs or generated demo music as an extensive factory library.
- **Power stays available.** Simple workflows and advanced mixing/recording can coexist.
- **Fast, safe, reliable.** Protect users' recordings and sessions; maintain real-time audio safety and undo/redo.
- **Accessible and flexible.** Good defaults, a legible professional interface, shortcuts, and sensible help.
- **Honest status.** Label planned functionality as planned until it is tested and working.

## Open source, licensing, and upstream credit

SoundWAVE X is derived from [SoundCraft](https://github.com/storytold/soundcraft), originally created by the **ArtCraft team and SoundCraft contributors**. We retain their applicable copyright/license notices and Git history. Imported code is dual-licensed under **MIT OR Apache-2.0**; see [LICENSE-MIT](LICENSE-MIT), [LICENSE-APACHE](LICENSE-APACHE), and [NOTICE](NOTICE).

Audio assets and other third-party materials may have their **own licenses**. Consult [ATTRIBUTION.md](ATTRIBUTION.md) and any future sound-pack manifests before redistribution. A sound that is free to use *in a composition* is not necessarily legal to redistribute as a standalone factory sample.

SoundWAVE X is **not affiliated with or endorsed by** Avid, Apple, SoundCraft, or the ArtCraft team. ArtCraft names and visual trademarks are not SoundWAVE X branding and will be removed from modified distributable artwork in accordance with applicable license terms.

## Early project notice

The repository is currently a development foundation and not a finished, polished SoundWAVE X release. If your goal is to make music today, you may find its inherited SoundCraft controls unfamiliar; the beginner-first and content-first experience is precisely what this project intends to improve.
