# Cmajor Standard Library Reference

> Source: `../../cmajor_stuff/cmajor/standard_library/`

---

## `std::oscillators`

### Available Shapes
```cmajor
enum Shape
{
    sine,           // Sine wave
    triangle,       // Triangle wave
    square,         // Square wave
    sawtoothUp,     // Rising sawtooth
    sawtoothDown,   // Falling sawtooth
    random          // Random sample & hold (LFO only)
}
```

### Processors

#### `std::oscillators::Sine (FrameType, initialFrequency)`
Sine wave generator. Most basic oscillator.

| Endpoint | Type | Description |
|---|---|---|
| `frequencyIn` | `input event float32` | Frequency in Hz (0–24000, init: 440) |
| `out` | `output stream FrameType` | Sine wave samples |

**Usage:** `node sine = std::oscillators::Sine (float);`

---

#### `std::oscillators::Phasor (FrameType, initialFrequency)`
Unipolar ramp (0→1) oscillator. Useful for phase modulation.

| Endpoint | Type | Description |
|---|---|---|
| `frequencyIn` | `input event float32` | Frequency in Hz |
| `out` | `output stream FrameType` | Ramp (0 → 1) |

---

#### `std::oscillators::PolyblepOscillator (FrameType, initialShape, initialFrequency)`
Alias-free oscillator with shape selection. The main one for demo 2+.

| Endpoint | Type | Description |
|---|---|---|
| `frequencyIn` | `input event float32` | Frequency |
| `shapeIn` | `input event float32` | Shape: 0=Sine, 1=Triangle, 2=Square, 3=Ramp Up, 4=Ramp Down |
| `out` | `output stream FrameType` | Audio output |

**Usage:**
```cmajor
node osc = std::oscillators::PolyblepOscillator (float, Shape::square, 220);
```

---

#### `std::oscillators::LFO (initialShape, initialFrequency, initialAmplitude, initialOffset)`
Full-featured low-frequency oscillator with tempo sync.

| Endpoint | Type | Description |
|---|---|---|
| `shapeIn` | `input event float32` | 0=Sine..5=Random |
| `rateHzIn` | `input event float32` | Rate in Hz (0.01–50) |
| `rateTempoIn` | `input event float32` | Rate in beats |
| `amplitudeIn` | `input event float32` | Output amplitude |
| `offsetIn` | `input event float32` | DC offset |
| `rateModeIn` | `input event float32` | 0=Hz, 1=Tempo |
| `syncIn` | `input event float32` | 0=Off, 1=On |
| `positionIn` | `input event std::timeline::Position` | Transport position |
| `transportStateIn` | `input event std::timeline::TransportState` | Play/stop |
| `tempoIn` | `input event std::timeline::Tempo` | BPM |
| `out` | `output stream float32` | LFO output |

### `std::oscillators::waveshape` (Functions)
For custom oscillator implementations:
- `waveshape::sine(phase)` / `sine(phase, amplitude)` / `sine(phase, amplitude, offset)`
- `waveshape::square(phase)`
- `waveshape::triangle(phase)`
- `waveshape::sawtoothUp(phase)` / `sawtoothDown(phase)`
- `waveshape::generate(Shape, phase)` — select shape at runtime
- `waveshape::polyblep(phase, increment)` — anti-aliasing correction

---

## `std::filters`

The filter namespace is parameterised:
```cmajor
namespace std::filters (using FrameType = float32,   // mono
                        using CoefficientType = float32,
                        int framesPerParameterUpdate = 32)
```

The `tpt` (topology-preserving transform) filters are:

### `std::filters::tpt::svf::Processor`
State-variable filter — **the main one for demos.**

| Endpoint | Type | Description |
|---|---|---|
| `in` | `input stream FrameType` | Audio input |
| `out` | `output stream FrameType` | Filtered output |
| `mode` | `input event int` | 0=Lowpass, 1=Highpass, 2=Bandpass |
| `frequency` | `input event float` | Cutoff (0–20000 Hz, init: 1000) |
| `q` | `input event float` | Resonance Q (0.01–100, init: 0.707) |

**Usage:**
```cmajor
graph Filter [[ main ]]
{
    input filter.frequency;    // Hoists filter.frequency as top-level param
    input filter.q;            // Hoists filter.q as top-level param

    input stream float in;
    output stream float out;

    node filter = std::filters::tpt::svf::Processor;

    connection
    {
        in -> filter.in;
        filter.out -> out;
    }
}
```

### `std::filters::tpt::svf::MultimodeProcessor`
Same as above but outputs all three modes simultaneously.

| Endpoint | Type | Description |
|---|---|---|
| `lowOut` | `output stream FrameType` | Low-pass output |
| `highOut` | `output stream FrameType` | High-pass output |
| `bandOut` | `output stream FrameType` | Band-pass output |

### `std::filters::tpt::onepole::Processor`
Simple one-pole filter. Lower CPU.

| Endpoint | Type | Description |
|---|---|---|
| `mode` | `input event int` | 0=Lowpass, 1=Highpass |
| `frequency` | `input event float` | Cutoff |

### Other Filters
- `std::filters::butterworth::Processor (Mode, frequency)` — Steeper rolloff
- `std::filters::dcblocker::Processor` — Removes DC offset
- `std::filters::simper::Processor` — Simple state-variable

---

## `std::envelopes`

### `std::envelopes::FixedASR (attackSeconds, releaseSeconds)`
Simple Attack-Sustain-Release envelope.

| Endpoint | Type | Description |
|---|---|---|
| `eventIn` | `input event (std::notes::NoteOn, std::notes::NoteOff)` | Gate events |
| `gainOut` | `output stream float` | Envelope amplitude (0→1) |

**Usage:** `node env = std::envelopes::FixedASR (0.01f, 0.1f);`

---

## `std::midi`

| Processor | Purpose |
|---|---|
| `std::midi::MPEConverter` | Converts `std::midi::Message` → `std::notes::NoteOn/NoteOff` |
| `std::midi::NoteToMIDI` | Converts `std::notes::NoteOn/NoteOff` → `std::midi::Message` |

---

## `std::voices`

### `std::voices::VoiceAllocator (voiceCount)`
Manages polyphonic voice assignment.

| Endpoint | Type | Description |
|---|---|---|
| `midiIn` | `input event std::notes::NoteOn` | Note events in |
| `voiceEventOut` | `output event (std::notes::NoteOn, std::notes::NoteOff)` | Routed to voice array |

---

## `std::notes`

### `std::notes::noteToFrequency (pitch)`
Converts MIDI note number to frequency in Hz.
```cmajor
let freq = std::notes::noteToFrequency (69);  // Returns 440.0 (A4)
```

---

## `std::levels`

| Processor | Purpose |
|---|---|
| `std::levels::ConstantGain (FrameType, gain)` | Fixed gain multiplier |
| `std::levels::DynamicGain (FrameType)` | Gain controlled by `gainIn` event |
| `std::levels::SmoothedGain (FrameType)` | Smooth gain changes (no zipper noise) |
| `std::smoothing::SmoothedValue` | Smoothed parameter slewing |

---

## Built-in constants
```cmajor
twoPi            // 2 * pi — for oscillator phase
processor.frequency  // Sample rate (e.g. 48000)
processor.period     // 1 / sample rate
processor.id         // Unique processor instance ID