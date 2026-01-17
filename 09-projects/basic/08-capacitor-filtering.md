# Basic Project 8: Capacitor Filtering (Power Supply Smoothing)

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 20 minutes  
**Concept**: Capacitor filtering, ripple reduction, voltage smoothing

## What You'll Learn

- How capacitors smooth noisy voltages
- Filtering concept (blocks noise, passes DC)
- Ripple reduction in power supplies
- Why power supplies need large capacitors

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 2 | Compare brightness |
| 220Ω Resistor | 2 | Current limiting |
| 1000µF Capacitor | 1 | Filter capacitor |
| 100nF Capacitor | 1 | High-frequency filter |
| Jumper wires | 8 | Breadboard connections |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Measure voltage stability |

## Theory: Capacitor Filtering

A **filter** is a circuit that blocks unwanted frequencies while passing desired ones.

**High-pass filter concept** (capacitor blocks DC, passes AC):
- Capacitor acts as open circuit to DC (fully charged, no current)
- Capacitor acts as short circuit to AC/noise (charges/discharges rapidly)

**Low-pass filter concept** (capacitor passes DC, blocks high-frequency noise):
- Large capacitor in parallel with load
- Capacitor voltage can't change instantly (V = V_0 + 1/C ∫ I dt)
- When voltage tries to fluctuate (noise), capacitor resists change
- Result: Noise smoothed out, DC signal remains

**Ripple**: Unwanted AC voltage component in power supply.

**Typical ripple**: From rectified AC (120Hz component in North America, 100Hz in Europe).

**Filtering in power supply**:
1. Transformer (steps down voltage)
2. Rectifier (converts AC to pulsating DC)
3. Filter capacitor (smooths pulsations)
4. Load (draws current)

## Breadboard Layout - Comparison Circuit

```
Option 1: WITHOUT filter
+5V → [R220] → [LED1] → GND

Option 2: WITH filter
+5V → [C1000µ] → (parallel point)
                  ↓
              [R220] → [LED2] → GND
```

LED1 without filter capacitor receives all noise.
LED2 with capacitor receives smoothed voltage.

## Building Instructions

### Part 1: Build Circuit WITHOUT Filter

1. Insert 220Ω resistor from +5V to Row 2
2. Insert LED anode into Row 2
3. Insert LED cathode into Row 3
4. Connect Row 3 to GND
5. **This LED gets unfiltered power**

### Part 2: Build Circuit WITH Filter

1. Insert 1000µF capacitor from +5V (positive lead) to Row 5
2. Insert negative lead to Row 6
3. Insert second 220Ω resistor from Row 5 to Row 7
4. Insert second LED anode into Row 7
5. Insert LED cathode into Row 8
6. Connect Row 8 to GND
7. **This LED gets filtered power through capacitor**

### Part 3: Optional High-Frequency Filter

1. Insert 100nF capacitor in parallel with 1000µF (across Row 5-6)
2. This filters higher frequencies (1000µF handles low freq, 100nF handles high)

## Measurement Plan

**For USB/battery power** (usually clean):

You won't see much difference in LED brightness because USB outputs clean DC.

But you can demonstrate the principle:

1. **Measure voltage stability**:
   - Without filter (LED1): Measure voltage at Row 2
   - Expected: 5.0V (steady, clean signal)

   - With filter (LED2): Measure voltage at Row 5
   - Expected: 5.0V (same, but capacitor actively smoothing)

2. **Simulate noise**:
   - Press button or move jumper wires while measuring
   - Unfiltered side shows voltage fluctuations
   - Filtered side shows more stable voltage (capacitor absorbs changes)

3. **Transient response**:
   - Suddenly disconnect +5V
   - Watch voltage decay
   - Filtered side: Capacitor provides voltage for brief moment
   - Unfiltered side: Voltage drops instantly

## Visual Verification

- ✓ Both LEDs glow (both receive adequate power)
- ✓ **Unfiltered LED**: May flicker slightly if noisy power
- ✓ **Filtered LED**: Steady brightness (noise absorbed by capacitor)

In clean USB power, difference is subtle.

## Real-World Filtering Demonstration

Where filtering matters most:

1. **Switched power supplies**: Noise from switching transistors
2. **Motors**: Create electrical noise when running
3. **High-frequency circuits**: Sensitive to RF interference
4. **Audio circuits**: Noise becomes audible hum/buzz

## Filtering Principle: Impedance

**Capacitive impedance**:
$$Z_C = \frac{1}{2\pi f C}$$

Where:
- f = frequency (Hz)
- C = capacitance (F)
- Z_C = impedance (Ω)

**DC** (f = 0):
- Z_C = ∞ (capacitor is open circuit)
- Capacitor blocks DC

**AC noise** (f = 1kHz):
- Z_C = 1/(2π × 1000 × 0.001) ≈ 159Ω
- Much lower impedance, noise passes through capacitor to ground
- Noise is shorted to ground (attenuated)

**Higher frequency**:
- Z_C decreases further
- Better noise rejection

This is why **larger capacitors filter lower frequencies** and **smaller capacitors filter higher frequencies**.

## Multi-Stage Filtering

Professional power supplies use multiple capacitors:

| Capacitor | Size | Purpose |
|-----------|------|---------|
| Bulk capacitor | 1000µF+ | Low frequency ripple |
| Ceramic bypass | 100nF | High frequency noise |
| Tantalum/film | 10µF | Medium frequency |

**Advantage**: Each handles its frequency range optimally.

## Troubleshooting

**LEDs have same brightness**:
- This is normal with clean USB power
- Difference shows up with noisy supplies

**Capacitor becomes warm**:
- Normal for charged capacitor under load
- Or indicates capacitor failure (internal leakage)

**LED with filter gets dimmer** (unexpected):
- Capacitor might be leaky (internal resistance)
- Or capacitor voltage hasn't built up yet (try powering for 10 seconds)

## Challenge Extensions

1. **Load current demand**:
   - Add more LEDs to filtered side
   - Capacitor can supply brief current during supply interruptions
   - Demonstrates "voltage regulator" behavior

2. **Three capacitor comparison**:
   - Build three branches: no filter, 100nF, 1000µF
   - Compare brightness in noisy environment
   - (Requires separate noisy power source)

3. **Transient hold-up time**:
   - Disconnect power while measuring filtered voltage
   - Capacitor voltage decays slowly (exponential)
   - Unfiltered drops instantly
   - Voltage decay time = RC time constant

4. **ESR effect** (advanced):
   - Equivalent Series Resistance (ESR) of capacitors
   - Lower ESR = better high-frequency filtering
   - Ceramic capacitors have very low ESR
   - Electrolytic capacitors have higher ESR

## Real-World Applications

- **Laptop charger**: Filters switching noise from converter
- **Audio amplifier**: Removes power supply hum and buzz
- **Digital circuits**: Keeps logic power supply clean
- **LED strips**: Filters power spikes from switching transistors
- **Microcontroller**: Decoupling capacitors near power pins

## Advanced: Ferrite Beads

For even better high-frequency filtering:

**Ferrite bead**: Small inductor that blocks high-frequency noise.

Often used **in series** with capacitors for comprehensive filtering:
- Ferrite: Blocks high frequency
- Capacitor: Passes DC, filters medium frequency

## Key Concepts Reinforced

- **Filtering**: Blocking unwanted frequency while passing desired signal
- **Capacitive impedance**: Depends on frequency (lower for higher f)
- **Ripple**: AC component in power supply
- **Multi-stage approach**: Different capacitors for different frequencies
- **Real-world circuits**: All power supplies include filter capacitors

## Next Steps

1. **Project 9: Diode Protection** - Understand diode's role in power supplies
2. **Project 11: Power Dissipation** - Understand heat from power supply
3. **Project 14: Power Supply Build** - Full filtered power supply (intermediate)

---

**Key Takeaway**: Capacitors in parallel with loads smooth noisy power supplies by absorbing voltage fluctuations. Large capacitors filter low frequencies, small capacitors filter high frequencies. This is why every electronic device contains filter capacitors near its power inputs—they're essential for reliable circuit operation in real-world noisy environments.
