# Presentation Setup — Rock Your Music With Code

> Fill this in as you build and test. Pin your versions, document audio config, and note rescue steps.

## Version Pinning

| Tool | Version | Date Tested | Notes |
|---|---|---|---|
| Bespoke Synth | | | |
| Cmajor | | | |
| OS | macOS Tahoe | | |
| Audio Interface | Built-in / External | | |

## Audio Configuration

| Setting | Value | Notes |
|---|---|---|
| Sample rate | 48000 Hz | Match Cmajor patches |
| Buffer size | 256 | Lower = less latency, higher = more stable |
| Output device | | Built-in speakers? External interface? |
| MIDI input device | | Keyboard controller name |

## Window Layout (Presentation Mode)

```
┌─────────────────┬─────────────────┐
│    Slides        │   Bespoke       │
│  (Presenter     │   (Patch view)  │
│   Display)      │                 │
├─────────────────┼─────────────────┤
│   Cmajor IDE    │   Terminal      │
│   (Code editor) │   (if needed)   │
└─────────────────┴─────────────────┘
```

Run Bespoke in fullscreen mode. Have Cmajor IDE in a window you can alt-tab to quickly.

## Rescue Checklist

- [ ] Build rescue patches (pre-compiled `.cmajor` files saved in `bespoke-saves/`)
- [ ] Record 30-sec screencast fallbacks → `screencasts/` folder
- [ ] Test without internet (Cmajor compile + Bespoke load)
- [ ] Venue audio test — arrive early, buffer settings, know the PA system

## Rescue Patch Locations

| Demo Step | Rescue Patch | Load Time |
|---|---|---|
| Step 1: Oscillator | `bespoke-saves/oscillator-rescue.bsk` | ~3 sec |
| Step 2: Oscillator + FX | `bespoke-saves/osc-fx-rescue.bsk` | ~3 sec |
| Step 3: Full song | `bespoke-saves/song-rescue.bsk` | ~5 sec |

## Cut Points (Time Management)

| If behind at... | Action |
|---|---|
| 12:00 mark | Skip arpeggiator entirely → go straight to song |
| 15:00 mark | Skip FX deep-dive → show FX briefly → go to song |
| 18:00 mark | Abandon live demo → play fallback screencast → CTA |

## Post-Presentation

- [ ] Export slides to PDF → `slides/` folder
- [ ] Push all patches to this repo
- [ ] Share links in meetup chat