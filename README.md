# Rock Your Music With Code

> Live-Coding Instruments & Effects with Bespoke + Cmajor
> *Jr Dev Singapore Meetup Demo Repo*

## Structure

```
rymwc/
├── patches/                    # Cmajor patch folders (each is a plugin)
│   ├── 01-oscillator/          # Step 1: Sine wave oscillator (instrument)
│   │   ├── 01-oscillator.cmajorpatch  # Manifest (JSON)
│   │   └── 01-oscillator.cmajor       # Source code
│   ├── 01-oscillator-multi/    # Step 1b: Sine/square switchable oscillator
│   │   ├── 01-oscillator-multi.cmajorpatch
│   │   └── 01-oscillator-multi.cmajor
│   ├── 02-fx/                  # Step 2: Low-pass filter (effect)
│   │   ├── 02-fx.cmajorpatch
│   │   └── 02-fx.cmajor
│   └── 03-arpeggiator/         # Step 3: MIDI arpeggiator with BPM control
│       ├── 03-arpeggiator.cmajorpatch
│       └── 03-arpeggiator.cmajor
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