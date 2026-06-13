# Song Patch — Demo Closer

This is where your full song patch lives. It's the non-negotiable closer.

## What to Build Here

Combine everything from steps 1-3 into one Bespoke patch:

1. **Multiple oscillator instances** (bass, lead, pad)
2. **FX chain** on each (low-pass, reverb, delay)
3. **Arpeggiator** driving one oscillator
4. **Sequencer** in Bespoke for the bassline
5. **Mixer** to blend everything

## Structure Suggestion

```
Bespoke Patch: song.bsk
├── MIDI Input (keyboard)
│   ├── → Arpeggiator → Sine Oscillator (lead)
│   ├── → Bass Sequencer → Square Oscillator (bass)
│   └── → Chord Trigger → Saw Oscillator (pad)
├── FX Bus
│   ├── Lead → LowPassFilter + Reverb
│   ├── Bass → Distortion
│   └── Pad → LowPassFilter + Delay
└── Master Output → Limiter
```

## Saving

Save your working Bespoke patch to:
```
bespoke-saves/song.bsk