# Advanced Project 4: Precision Amplifier (Non-Inverting Configurable Gain)

**Difficulty**: ⭐⭐⭐ (Advanced)  
**Time**: 75 minutes  
**Concept**: Programmable gain amplifier, precision amplification, feedback design, gain equation

## What You'll Learn

- Non-inverting amplifier configuration
- Gain equation and design
- Frequency response with different gains
- Input/output impedance
- Gain-bandwidth product concept
- Precision measurement amplification

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| Op-Amp IC | 1 | TL072, OPA2134, or LM358 |
| Resistors | 3 | 1kΩ, 10kΩ, 100kΩ (1% tolerance) |
| Potentiometer | 1 | 100kΩ (adjustable gain) |
| Capacitor | 1 | 100nF (bypass) |
| Power Supply | 1 | ±5V to ±15V |
| Function Generator | 1 | 1Hz-100kHz |
| Oscilloscope | 2 channels | |
| Breadboard | 1 | Standard |

## Theory: Non-Inverting Amplifier

**Configuration**: Input to non-inverting (+) input, feedback from output to inverting (-) input.

**Gain equation** (fundamental):
$$A = 1 + \frac{R_f}{R_g}$$

Where:
- A = voltage gain (linear, not dB)
- R_f = feedback resistor
- R_g = ground resistor (to inverting input)

**Examples**:
- R_f = 1kΩ, R_g = 1kΩ → A = 2 (6dB)
- R_f = 9kΩ, R_g = 1kΩ → A = 10 (20dB)
- R_f = 99kΩ, R_g = 1kΩ → A = 100 (40dB)

**Input impedance**:
$$Z_{in} = Z_{in,opamp} \times (1 + A \times \beta)$$

Very high (10MΩ+ typical) due to feedback.

**Output impedance**:
$$Z_{out} = \frac{Z_{out,opamp}}{1 + A \times \beta}$$

Very low (mΩ range) due to feedback.

**Bandwidth**:
$$BW = \frac{GBW}{A}$$

Where GBW = gain-bandwidth product (constant for op-amp).

Higher gain → Lower bandwidth trade-off.

## Breadboard Layout - Adjustable Gain Amplifier

```
Signal In --[R_in]--+--[Non-Inv Input (+)]
                    |
                 [Op-Amp]
                    |
                 [Output]
                    |
              [R_f + R_g (pot)]
                    |
              [Inv Input (-)]
                    |
                   GND
```

Potentiometer varies R_f, changing gain continuously.

## Building Instructions

### Part 1: Fixed Gain Configuration (Gain = 10)

1. **Set up op-amp power**:
   - Pin 8: +15V (or +5V)
   - Pin 4: -15V (or GND for single supply)
   - Bypass capacitor on power pins

2. **Build input stage**:
   - Input signal to pin 3 (non-inverting input) through 1kΩ resistor
   - Pin 3 connected to GND through 1kΩ (input impedance definition)

3. **Build feedback network** (for Gain = 10):
   - R_g = 1kΩ: From pin 2 (inverting input) to GND
   - R_f = 9kΩ: From pin 6 (output) to pin 2 (inverting input)
   - Gain = 1 + 9k/1k = 10

4. **Test output**:
   - Function generator: 100mV peak sine wave
   - Expected output: 1V peak (100mV × 10)
   - Actual: ______

### Part 2: Variable Gain Configuration

1. **Replace feedback resistors with potentiometer**:
   - Remove fixed R_f and R_g
   - Insert 100kΩ potentiometer:
     - One end to pin 2 (inverting input)
     - Wiper to GND
     - Other end to pin 6 (output)
   - Potentiometer varies from 0Ω to 100kΩ

2. **Gain variation**:
   - Fully toward GND (Pot = 0): R_f = 100kΩ, A = 101
   - Middle (Pot = 50kΩ): R_f = 50kΩ, A = 51
   - Fully toward output (Pot = 100kΩ): R_f = 0, A = 1 (unity gain, follower)

## Measurement Plan

### Part 1: Frequency Response (Fixed Gain = 10)

Sweep function generator across frequency range, measure gain and phase:

| Frequency | Input V | Output V | Gain (V/V) | Gain (dB) | Phase |
|---|---|---|---|---|---|
| 10 Hz | 100mV | _____ | _____ | _____ | _____ |
| 100 Hz | 100mV | _____ | _____ | _____ | _____ |
| 1 kHz | 100mV | _____ | _____ | _____ | _____ |
| 10 kHz | 100mV | _____ | _____ | _____ | _____ |
| 100 kHz | 100mV | _____ | _____ | _____ | _____ |

**Calculate gain in dB**:
$$G_{dB} = 20 \log_{10}(G_{linear}) = 20 \log_{10}(10) = 20dB$$

Expected: 20dB flat across frequency range (limited by op-amp GBW).

### Part 2: Gain vs Potentiometer Position

Adjust potentiometer and measure output voltage:

| Pot Position | Expected R_f | Expected A | Input V | Output V | Actual A |
|---|---|---|---|---|---|
| Min (toward GND) | 100kΩ | 101 | 100mV | _____ | _____ |
| 1/4 | 75kΩ | 76 | 100mV | _____ | _____ |
| 1/2 | 50kΩ | 51 | 100mV | _____ | _____ |
| 3/4 | 25kΩ | 26 | 100mV | _____ | _____ |
| Max (toward output) | 0Ω | 1 | 100mV | _____ | _____ |

Verify gain equation matches measurements.

### Part 3: Input Impedance

**Method**: Place known impedance in series with input signal, measure attenuation.

1. **No source impedance** (function generator 50Ω output impedance):
   - Output voltage: V1 = ______

2. **With 1MΩ source impedance** (high impedance source):
   - Output voltage: V2 = ______
   - Ratio: V2/V1 = _____ (should be ≈1.0, no loading)

If ratio is 1.0, input impedance much higher than 1MΩ ✓

### Part 4: Output Impedance

**Method**: Load output with different resistances, measure voltage change.

1. **No load**:
   - Output voltage: V_NL = ______

2. **With 10kΩ load**:
   - Output voltage: V_10k = ______

3. **With 1kΩ load**:
   - Output voltage: V_1k = ______

4. **Calculate output impedance**:
   - Zout = ΔV / ΔI = (V_NL - V_1k) / [(V_NL - V_1k) / 1000]
   - Expected: <100Ω
   - Actual: ______Ω

## Visual Verification

**Oscilloscope observations**:
- ✓ Output amplitude scales linearly with input
- ✓ Gain value matches equation prediction
- ✓ No distortion or clipping (within supply rails)
- ✓ Phase shift minimal at low frequencies

## Key Insight: Gain-Bandwidth Product

**GBW constant** for any op-amp (spec sheet value).

Example: TL072 has GBW = 3MHz

**Bandwidth decreases as gain increases**:
- Gain = 10: BW = 3MHz / 10 = 300kHz
- Gain = 100: BW = 3MHz / 100 = 30kHz
- Gain = 1000: BW = 3MHz / 1000 = 3kHz

**Trade-off**: More gain = lower bandwidth (can't have both).

For this project with Gain = 10:
- Expected BW ≈ 300kHz (for TL072)
- Flat response expected up to 100kHz

## Slew Rate Limitation

**Slew rate**: Maximum rate voltage can change (V/µs).

Example: TL072 slew rate ≈ 13V/µs

**Limiting case**: 10V peak sine at 1MHz
- Required slew rate: 2πfV = 2π × 10^6 × 10 ≈ 63V/µs
- Exceeds TL072 limit (13V/µs)
- Output will not be sinusoidal (will show slew-rate distortion)

For this project:
- 10V peak, 100kHz: Required ≈ 6.3V/µs (within limit) ✓
- No slew-rate distortion expected

## Troubleshooting

**No output**:
- Power supply not connected
- Feedback resistors not connected properly
- Op-amp damaged

**Output distorted** (clipping):
- Input signal too large (exceeds op-amp output swing)
- Reduce input voltage
- Check power supply limits (rarely ±5V sufficient for 10V gain)

**Gain wrong**:
- Verify resistor values (measure with multimeter)
- Check feedback loop continuity
- Measure voltage at inverting input (should track input due to golden rule)

**Oscillation** (output shows high-frequency ringing):
- Feedback path has resonance
- Add small capacitor (10pF) across feedback resistor to stabilize
- Check for parasitic inductance in long wires

## Challenge Extensions

1. **Measure GBW product**:
   - Test gain-bandwidth trade-off for your op-amp
   - Build amplifier with Gain = 1, 10, 100
   - Measure bandwidth for each (-3dB point)
   - Verify GBW = constant across configurations

2. **Frequency response plot** (Bode plot):
   - Sweep 10Hz to 1MHz for Gain = 100
   - Plot magnitude and phase
   - Identify -3dB cutoff frequency
   - Compare to GBW prediction

3. **Adjustable load gain**:
   - Design for different applications
   - Microphone preamp: Gain = 100 (40dB)
   - Line-level buffer: Gain = 10 (20dB)
   - Unity amplifier: Gain = 1 (0dB)

4. **Precision matching test**:
   - Build two identical amplifiers
   - Supply same input signal
   - Measure output differences
   - Quantify precision (% error)

## Real-World Applications

- **Microphone preamplifier**: Gain = 40-60dB (100-1000 linear)
- **Instrumentation amp**: Gain = 1-1000 adjustable
- **Data acquisition**: Gain matched to ADC range
- **Audio mixing**: Adjustable channel gain
- **Sensor conditioning**: Amplify weak sensor signals

## Advanced: Rail-to-Rail Operation

Some op-amps (LM358, OPA2134) can use single supply:
- Power: +15V and GND (no negative supply)
- Input biased at +7.5V (midpoint)
- Can amplify AC signals riding on DC offset

More complex but useful in battery-powered systems.

## Key Concepts Reinforced

- **Non-inverting amplifier**: Output = Input × (1 + Rf/Rg)
- **Feedback determines gain**: Not op-amp gain (which is very high)
- **Gain-bandwidth trade-off**: Higher gain → lower bandwidth
- **High input impedance**: Due to negative feedback
- **Precision**: Gain accuracy depends on resistor tolerance (use 1%)

## Next Steps

1. **Project 5: Instrumentation Amp** - Differential measurement
2. **Project 6: Logarithmic Amp** - Exponential conversion
3. **Project 10: Complete Audio System** - Apply amplification

---

**Key Takeaway**: Non-inverting amplifiers provide precise, adjustable gain using simple resistor networks. Understanding the gain equation (A = 1 + Rf/Rg) and frequency response (GBW = constant) enables design of amplifiers optimized for any application—from microphone preamps to instrumentation systems.
