# Intermediate Project 2: Simple Rectifier (AC to DC Conversion)

**Difficulty**: ⭐⭐ (Intermediate)  
**Time**: 30 minutes  
**Concept**: AC to DC conversion, bridge rectifier, ripple reduction, power supply fundamentals

## What You'll Learn

- How rectification converts AC to pulsating DC
- Half-wave vs full-wave rectification
- Bridge rectifier configuration
- Ripple voltage and filtering necessity
- Foundation of all power supplies

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| Diodes (1N4007) | 4 | Full bridge configuration |
| Resistor (10kΩ) | 1 | Load resistor |
| Capacitor (470µF) | 1 | Filter capacitor |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Measure DC and AC ripple |
| Function generator | 1 | Generate AC signal (1kHz recommended) |
| Oscilloscope | 1 | View waveforms (recommended but optional) |

**Note**: This project simulates AC input using function generator (safer than 120V mains).

## Theory: Rectification

### AC to DC Conversion

**Alternating current (AC)**: Voltage oscillates positive-negative.
- Example: 5V peak AC (±5V oscillates at 50Hz or 60Hz)

**Direct current (DC)**: Voltage constant, always positive.
- Example: 5V DC (steady 5V)

**Rectification**: Process of converting AC to DC using diodes.

### Half-Wave Rectification

**Concept**: Allow only positive half-cycles to pass.

```
AC input:   Sine wave (positive and negative cycles)
            ~~~/~~~\___/~~~\___/
                    
Rectified:  Positive peaks only
            /~~~\_____/~~~\_____
```

**Circuit**: Single diode blocks negative half-cycles.

**Advantages**:
- Simplest (one diode)
- Minimal components

**Disadvantages**:
- 50% of power wasted
- Large ripple voltage (wide gaps between pulses)
- Transformer must handle full reverse voltage

### Full-Wave Rectification (Bridge Rectifier)

**Concept**: Convert both positive AND negative cycles to positive.

```
AC input:   Sine wave (positive and negative cycles)
            ~~~/~~~\___/~~~\___/
                    
Rectified:  Both peaks (inverted ones flipped)
            /~~~\/~~~\/~~~\/~~~\
```

**Circuit**: Four diodes in bridge configuration.

**Pinout**:
```
    AC input
      |
   +--+--+
   |     |
   D1    D3
   |     |
+-----+-----+
|           |
D2         D4
|           |
+--+  +--+
   |     |
  GND   +DC
```

**How it works**:
- Positive half-cycle: Current flows D1 → load → D4
- Negative half-cycle: Current flows D3 → load → D2
- Both cycles produce positive output

**Advantages**:
- 100% of AC power converted
- Smaller ripple (more frequent peaks)
- Transformer voltage utilization doubled

**Disadvantages**:
- Four diodes needed
- Two diodes always conducting (2 × 0.7V = 1.4V voltage loss)

## Breadboard Layout - Bridge Rectifier

```
AC Input
  A ~~
  B GND
  
    A +---- [D1 anode]
      |            |
      |        [Load R]
      |            |
    B +---- [D4 anode]
                   |
              +DC output
              
    (Simplified: actually four diodes in bridge)

Full bridge:
         +AC in
          |
        D1 D3
        |  |
    +-------+
    |       |
    D2 D4   |Load
    |   |   |
    +---+---+
        |
       GND
```

## Building Instructions

### Part 1: Build Bridge Rectifier

1. **Insert diodes in bridge configuration**:
   - D1: Anode to +AC, Cathode to +DC output (Row 2)
   - D2: Cathode to +AC, Anode to -DC output/GND (Row 3)
   - D3: Cathode to +AC, Anode to +DC output (Row 2)
   - D4: Anode to -AC, Cathode to GND (Row 4)

   **Simplified construction**:
   - Insert D1 cathode band at Row 2
   - Insert D2 (reversed) cathode at Row 3
   - D3 at Row 2 (same as D1)
   - D4 at Row 4

2. **Connect load resistor**:
   - Insert 10kΩ resistor from Row 2 (+DC) to Row 4 (GND)
   - This is the rectifier load

3. **Connect filter capacitor** (optional but recommended):
   - Insert 470µF capacitor: positive to Row 2, negative to Row 4 (GND)
   - This smooths ripple

### Part 2: Connect AC Input

1. **Set up function generator**:
   - Output: 5V peak sine wave (10V peak-to-peak)
   - Frequency: 1kHz
   - **WARNING**: Do NOT use wall outlet power (lethal voltage)

2. **Connect to breadboard**:
   - Generator output terminal A to +AC input (Row 1)
   - Generator ground to -AC input/GND (Row 3)

### Part 3: Verify Polarity

1. **Measure DC output voltage**:
   - Black probe: GND (Row 4)
   - Red probe: +DC (Row 2)
   - Expected: ~3.3V (5V peak - 1.4V diode loss × 2)
   - Actual: ______

## Measurement Plan

### DC Output Verification

1. **Average voltage** (DC measurement mode):
   - Black probe: GND
   - Red probe: +DC output
   - Expected: ~3.3V (with filter capacitor)
   - Expected: ~2.5V (without filter capacitor, ripple reduces average)
   - Actual: ______

2. **Ripple voltage** (AC measurement mode):
   - Same probes, switch to AC mode
   - Expected: ~0.1V RMS (with filter capacitor)
   - Expected: ~1V RMS (without filter capacitor)
   - Actual: ______

3. **Peak voltage** (with oscilloscope):
   - Vertical: 2V/division
   - Expected: Ripple between 2.5V and 3.5V (with capacitor)
   - Shape: Smooth bumps (rectified sine wave)

### Diode Voltage Drop Verification

1. **Measure diode forward drop** (one diode in circuit):
   - Across any diode in conducting path
   - Expected: ~0.7V per diode
   - Two diodes conduct simultaneously: ~1.4V total drop
   - Actual: ______

2. **Explain voltage loss**:
   - AC peak input: 5V
   - Subtract diode drops: 5V - 1.4V = 3.6V expected peak
   - With capacitor averaging: ~3.3V DC

## Visual Verification

- ✓ DC voltage positive (output never goes negative)
- ✓ Voltage relatively steady with capacitor
- ✓ Ripple visible but small with filter

## Key Insight: Diode Bridge Operation

**On positive half-cycle** (AC input = +5V):
- D1 forward biased (+5V → anode, ground at cathode) → conducts
- D4 forward biased (ground → anode, -AC at cathode) → conducts
- Path: +AC → D1 → load → D4 → -AC
- Output at load: positive

**On negative half-cycle** (AC input = -5V):
- D3 forward biased (-AC at anode, +ground at cathode) → conducts
- D2 forward biased (ground at anode, -AC at cathode) → conducts
- Path: -AC → D3 → load → D2 → +AC
- Output at load: still positive (inverted negative becomes positive)

Result: Both cycles produce positive output → rectified DC.

## Why Two Diodes Always Conduct

**Bridge diode loss**: Always two diodes in series with load.
- One from AC source
- One to AC return
- Total drop: 2 × 0.7V = 1.4V

This is why bridge rectifiers need higher AC voltage than desired DC output.

## Ripple Reduction with Capacitor

**Without capacitor**:
- Output pulses at 2kHz (100Hz AC full-wave rectified, or 2× input frequency)
- Voltage ripples between 0V and peak value
- Average: lower due to ripple

**With capacitor**:
- Capacitor charges during peak
- Discharges through load resistor between peaks
- Provides smoothing current during gaps
- Output much steadier

**Ripple frequency** (100Hz AC input):
- Half-wave: 100Hz ripple (one pulse per AC cycle)
- Full-wave: 200Hz ripple (two pulses per AC cycle)
- Higher ripple frequency = easier to filter

## Troubleshooting

**No DC output (0V)**:
- Diodes inserted wrong direction
- Check cathode band orientation (should match polarity diagram)
- Verify AC input present (measure at input with oscilloscope)

**DC output negative** (opposite polarity):
- Diodes reversed
- All cathodes should point toward +DC output

**Ripple too large**:
- Capacitor too small or missing
- Try larger capacitor (1000µF)
- Or reduce load current (increase load resistor)

**Voltage lower than expected**:
- Diode forward voltage loss (normal, 2 × 0.7V)
- Measure input voltage to confirm
- Measure across each diode (should be ~0.7V)

## Challenge Extensions

1. **Measure ripple frequency**:
   - With oscilloscope, measure ripple frequency
   - Expected: 2× AC input frequency (2kHz for 1kHz input)
   - Verify formula: ripple frequency = 2 × AC frequency

2. **Compare with half-wave**:
   - Remove D3, D4 (keep only D1, D2 in series)
   - Measure output: 50Hz ripple, larger voltage ripple
   - See why full-wave is better

3. **Calculate power delivery**:
   - Measure current through load: I = V / R
   - Power: P = V × I
   - With capacitor: measure steady voltage
   - Compare to AC power (half is wasted in rectification)

4. **Filter improvement**:
   - Try adding small series resistor (100Ω) + larger capacitor
   - Creates RC filter
   - Further reduces ripple

## Real-World Applications

- **All power supplies**: AC wall power converts to DC
- **Laptop chargers**: Internal bridge rectifier converts AC mains to DC
- **LED strips**: AC-powered LED drivers use bridge rectifier
- **Phone chargers**: AC to DC conversion step

## Why Bridge Rectifiers Win

**Alternatives**:
- **Half-wave**: Cheaper (1 diode), simpler, but only 50% efficient
- **Full-wave center-tap**: Requires special transformer with center tap
- **Bridge**: Standard approach, no special transformer needed, 100% efficient use of AC

This is why virtually all power supplies use bridge rectifiers.

## Advanced: Synchronous Rectification

For very high-current applications:
- Replace diodes with MOSFETs controlled by signal
- Synchronous switches reduce voltage drop from 1.4V to ~0.2V
- Increases efficiency significantly

Preview: Advanced project later.

## Key Concepts Reinforced

- **Rectification**: Converting AC to DC with diodes
- **Bridge configuration**: Four diodes enable full-wave rectification
- **Voltage loss**: Two diodes always conduct (2 × 0.7V = 1.4V)
- **Ripple**: AC component in rectified output
- **Filtering**: Capacitor smooths ripple voltage

## Next Steps

1. **Project 3: Voltage Regulator** - Stabilize rectifier output
2. **Project 4: 555 Timer** - Use regulated DC supply
3. **Intermediate Lab: Full Power Supply** - Combine rectifier + filter + regulator

---

**Key Takeaway**: Bridge rectifiers convert AC to DC efficiently by routing current through two conducting diodes in series. Although this creates a 1.4V voltage loss, it's the standard approach because it requires no special transformer and uses 100% of the AC power. Following rectification with a filter capacitor smooths the resulting ripple into clean DC.
