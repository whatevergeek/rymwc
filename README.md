# Rock Your Music With Code

> Live-Coding Instruments & Effects with Bespoke + Cmajor

> *Junior Dev Singapore Meetup Demo Repo*

## Structure

```
rymwc/
├── patches/                    # Cmajor patch folders (each is a plugin)
│   ├── 01-oscillator/          # Step 1: Sine wave oscillator (instrument)
│   │   ├── 01-oscillator.cmajorpatch       # Manifest (JSON)
│   │   ├── 01-oscillator.cmajor            # Source code
│   │   ├── 01-oscillator-multi.cmajorpatch # Step 1b: Sine/square switchable oscillator
│   │   ├── 01-oscillator-multi.cmajor
│   │   └── simple_sine_patch.md            # Walkthrough doc for this patch
│   ├── 02-fx/                  # Step 2: Low-pass filter (effect)
│   │   ├── 02-fx.cmajorpatch
│   │   └── 02-fx.cmajor
│   ├── 03-arpeggiator/         # Step 3: MIDI arpeggiator with BPM control
│   │   ├── 03-arpeggiator.cmajorpatch
│   │   └── 03-arpeggiator.cmajor
│   └── amorph_sample_prompt.md # Prompt for generating amorphous soundscape patches
└── slides/                     # Presentation slides (PDF)
    └── rymwc.pdf
```

## Quick Start

### Prerequisites
1. Install the [Cmajor VScode extension](https://marketplace.visualstudio.com/items?itemName=CmajorSoftware.cmajor-tools) — it auto-installs the compiler
2. Download [Bespoke Synth](https://www.bespokesynth.com)
3. (Optional) Install the [Cmajor VST/AU plugin](https://cmajor.dev) for DAW use

### Run the oscillator patch
1. Open `patches/01-oscillator/01-oscillator.cmajorpatch` in VScode
2. Run `Cmajor: Run patch` from the command palette
3. A window opens with controls — hear a sine wave

### Load in Bespoke
1. Open Bespoke
2. Add a Cmajor VST/AU plugin module
3. Drag any `.cmajorpatch` file onto the plugin GUI
4. Connect a MIDI keyboard (or use Bespoke's built-in sequencer)
5. Connect audio output to your speakers
6. Play a note — hear a sine wave

### Chain patches in Bespoke
Wire patches together visually in Bespoke:
- **MIDI keyboard → Arpeggiator → Oscillator → Filter → Output**
- Switch the oscillator to square wave for richer harmonics through the filter

## Links

- [Bespoke Synth](https://www.bespokesynth.com)
- [Cmajor Language](https://cmajor.dev)
- [Cmajor Examples](https://github.com/cmajor-lang/cmajor/tree/main/examples)
- [Slides (PDF)](slides/rymwc.pdf)
- [Simple Sine Patch Walkthrough](patches/01-oscillator/simple_sine_patch.md)
- [Amorphous Soundscape Prompt](patches/amorph_sample_prompt.md)
- [Amorph Plugin](https://artistsindsp.gumroad.com/l/amorph) — prompt-driven DAW plugin that turns ideas into instruments and effects using AI. Just ask, compile, and play.
- [Voxengo SPAN](https://www.voxengo.com/product/span/) — free spectrum analyzer (used in the live demo)

## Previous Related Talks

| Year | Talk | Event | Links | Focus |
|------|------|-------|-------|-------|
| 2022 | Jamming with Guitars and Synths using Bespoke | FOSSAsia 2022 | [YouTube](https://www.youtube.com/watch?v=JlsZwlzh7vw) | Introduction to Bespoke Synth |
| 2023 | Your Code Rocks! An Intro To Live Coding Music with Sonic Pi | FOSSAsia 2023 | [YouTube](https://www.youtube.com/watch?v=ALsbGmxlJd4) · [GitHub](https://github.com/whatevergeek/yourcoderocks) | Live coding music with Sonic Pi (Ruby) |
| 2025 | Python Beats: Live Coding Music with Python | PyCon Singapore 2026 | [YouTube](https://www.youtube.com/watch?v=O08UVihsZ0M&t=1s) · [GitHub](https://github.com/whatevergeek/pythonbeats) | Live coding music with Python + Bespoke |

## Speaker Contact

- **Mastodon / X / GitHub**: [whatevergeek](https://github.com/whatevergeek)
- **Music**: [Soundcloud](https://soundcloud.com/whatevergeek)
