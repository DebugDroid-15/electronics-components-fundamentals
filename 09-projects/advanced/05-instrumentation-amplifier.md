# Advanced Project 5: Instrumentation Amplifier (Differential Measurement)

**Difficulty**: ⭐⭐⭐ (Advanced)  
**Time**: 90 minutes  
**Concept**: Differential amplification, high CMRR, bridge measurement, sensor interface

## What You'll Learn

- Instrumentation amplifier architecture
- Common-mode rejection (CMRR)
- Differential vs common-mode signals
- Bridge sensor measurement
- Precision analog measurement

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| Op-Amp IC | 3 | TL072 or OPA2134 (for INA simulation) |
| Resistors | 8 | 1kΩ, 10kΩ, 100kΩ (1% tolerance critical) |
| Potentiometer | 1 | 100kΩ (gain adjust) |
| Capacitor | 2 | 100nF (bypass) |
| Power Supply | 1 | ±5V to ±15V |
| Function Generator | 2 | Dual channel (or 1 with splitter) |
| Oscilloscope | 2 channels | |
| Breadboard | 1 | Standard or large |

**Note**: This project builds an INA-like circuit from discrete op-amps (real INA chips available as INA125, INA128, etc.)

## Theory: Instrumentation Amplifier

### Problem: Differential Measurement

**Scenario**: Measure small voltage difference between two sensor outputs with large common-mode voltage.

Example: Bridge sensor with ±5mV signal riding on ±5V common-mode noise.

**Naive approach** (subtract with op-amp):
- Amplify difference, but common-mode also amplified
- Result: Noisy measurement

**Solution**: Instrumentation amp rejects common-mode while amplifying differential signal.

### CMRR (Common-Mode Rejection Ratio)

**Definition**: Ratio of differential gain to common-mode gain.

$$CMRR = \frac{A_d}{A_c}$$

Where:
- A_d = differential gain (desired)
- A_c = common-mode gain (undesired)

**Ideal**: CMRR = ∞ (rejects all common-mode)
**Real**: CMRR = 60-100dB (excellent noise rejection)

**Example**: Gain = 100, CMRR = 80dB (10,000:1)
- 100V common-mode input → 10mV noise output
- 100mV differential input → 10V desired output
- Signal-to-noise: 1000:1 (excellent)

### Three-Op-Amp Instrumentation Amplifier

**Stage 1: Input buffer stage** (two op-amps in non-inverting config)
- High input impedance (very high)
- Gain = 1 + 2R / R_gain
- Rejects common-mode at input

**Stage 2: Difference amplifier** (one op-amp)
- Takes buffered outputs
- Subtracts to get pure differential signal
- Further common-mode rejection

**Total differential gain**:
$$A_d = (1 + \frac{2R}{R_{gain}}) \times \frac{R_f}{R_g}$$

For well-matched resistors: CMRR > 80dB typical.

## Breadboard Layout - INA Simulation

```
+Input --[Buffer]--+-- [Diff Amp] --+-- Output
                   |                |
                   +-- [Precision R Network]
                   
-Input --[Buffer]--+
                   
(Three op-amps total)
```

Simplified representation (detailed pinout below).

## Building Instructions

### Part 1: Input Buffer Stages

1. **Configure first buffer (Op-Amp 1)**:
   - Non-inverting input (pin 3): +Input signal
   - Inverting input (pin 2): Through 10kΩ to output (pin 6)
   - Feedback creates non-inverting amp with Gain = 1 + 2R/R_gain
   - For unity gain: Short pin 2 to pin 6 (voltage follower)

2. **Configure second buffer (Op-Amp 2)**:
   - Non-inverting input (pin 3): -Input signal
   - Inverting input (pin 2): Through 10kΩ to output (pin 6)
   - Same configuration as first buffer

3. **Add gain resistor** (between the two input buffers):
   - 100kΩ potentiometer between the two inverting input nodes
   - This potentiometer controls overall gain

### Part 2: Difference Amplifier Stage

1. **Configure difference amp (Op-Amp 3)**:
   - Takes outputs from two buffers
   - Subtracts to get differential signal
   - Standard difference amp configuration:
     - Input 1 through 10kΩ to pin 3
     - Input 2 through 10kΩ to pin 2
     - Feedback resistor 10kΩ from output to pin 2

2. **Connect outputs**:
   - Final output from Op-Amp 3 pin 6

## Measurement Plan

### Part 1: Differential Signal Test

1. **Apply known differential signal**:
   - Generator 1: +50mV at input (+)
   - Generator 2: -50mV at input (-)
   - Total differential: 100mV

2. **Measure output voltage**:
   - Expected (with Gain = 100): 10V
   - Actual: ______

3. **Verify gain**:
   - Adjust gain resistor to achieve Gain = 100
   - Verify with different input signals

### Part 2: Common-Mode Rejection Test

1. **Apply common-mode signal** (both inputs same voltage):
   - Generator 1 and 2 both set to +1V (100% common-mode)
   - Differential component: 0V (no difference)

2. **Measure output voltage**:
   - Expected: ≈0V (perfect rejection)
   - Actual: ______ (will show small residual)

3. **Calculate CMRR**:
   - Common-mode gain = Output / Input = _____ / 1V
   - CMRR = A_diff / A_cm = 100 / A_cm
   - Expected CMRR: > 80dB (> 10,000:1 ratio)
   - Actual CMRR: ______dB

### Part 3: Bridge Sensor Simulation

Simulate Wheatstone bridge with small unbalance:

1. **Build simulation circuit**:
   - Two voltage dividers (representing bridge arms)
   - Top divider: 5kΩ and 5kΩ (nominally balanced)
   - Bottom divider: 5kΩ and 4.9kΩ (slightly unbalanced)
   - Difference between midpoints: ~5mV

2. **Connect to INA inputs**:
   - (+) input from top divider midpoint
   - (-) input from bottom divider midpoint
   - Differential voltage: ~5mV

3. **Measure and amplify**:
   - With Gain = 100: Output should be ~500mV
   - Without INA (direct amplification): Would amplify noise too
   - With INA: Clean measurement of small signal

### Part 4: Frequency Response

Test INA across frequency range:

| Frequency | Differential V | Output V | Gain | Phase |
|---|---|---|---|---|
| 10 Hz | 10mV | _____ | _____ | _____ |
| 100 Hz | 10mV | _____ | _____ | _____ |
| 1 kHz | 10mV | _____ | _____ | _____ |
| 10 kHz | 10mV | _____ | _____ | _____ |

Expected: Gain stable across frequency range (limited by slowest op-amp).

## Visual Verification

**Oscilloscope observations**:
- ✓ Differential signal amplified proportionally
- ✓ Common-mode signals rejected (minimal on output)
- ✓ No oscillation or instability
- ✓ Low output impedance (can drive loads)

## Key Insight: Resistor Matching

**CMRR depends critically on resistor matching**:

**1% tolerance resistors**: CMRR ≈ 80dB
**0.1% tolerance resistors**: CMRR ≈ 100dB+

**Why**? Gain matching error = CMRR error.

If top resistor 1% high and bottom 1% low:
- Gain mismatch ≈ 2%
- CMRR worst case ≈ 1/0.02 = 50:1 ≈ 34dB (poor)

**In practice**: Use 1% resistors minimum, preferably matched pairs.

## Real-World Bridge Measurement

**Wheatstone bridge**:
```
+5V
 |
[R1]---+---[R3]
       |
      IN+  OUT  IN-
       |
[R2]---+---[R4]
       |
      GND
```

When one resistor changes (sensor):
- Small differential voltage appears (IN+ - IN-) ≈ 5mV for typical sensor
- INA amplifies to measurable level (500mV to 5V)
- Can feed to ADC for digital measurement

## Troubleshooting

**Output always zero** (no gain):
- Verify differential signal present
- Check buffer outputs with oscilloscope
- Confirm difference amp connected properly

**Common-mode signal appears on output** (poor CMRR):
- Resistor matching critical
- Verify all resistor values with multimeter
- Replace with higher tolerance (0.1%) if available

**Oscillation or instability**:
- Check power supply bypass capacitors
- Add small capacitor (10pF) across feedback resistors
- Reduce signal frequency temporarily for stability

**Gain too low or too high**:
- Verify gain resistor value
- Adjust potentiometer to correct value
- Calculate expected gain from resistor values

## Challenge Extensions

1. **Measure actual CMRR**:
   - Apply 10V common-mode signal
   - Measure residual output
   - Calculate CMRR in dB: CMRR = 20 log(10V / Vout)

2. **Test with different gain settings**:
   - Build with Gain = 10, 100, 1000
   - Measure frequency response for each
   - Observe gain-bandwidth trade-off

3. **Simulate temperature sensor**:
   - Bridge with 1kΩ thermistor
   - Temperature change → resistance change → bridge unbalance
   - INA detects and amplifies signal
   - Relate output voltage to temperature

4. **Integrate with Arduino**:
   - Connect INA output to analog input
   - Read with analogRead()
   - Display temperature or measurement on serial

## Real-World Applications

- **Strain gauge measurement**: Bridge with strain sensor
- **Temperature measurement**: Bridge with thermistor
- **Pressure measurement**: Bridge with pressure transducer
- **Current measurement**: Sense resistor in power line
- **Medical instrumentation**: ECG, EMG amplification
- **Industrial sensors**: All bridge-based measurements

## Advanced: Programmable Gain INA

Real instrumentation amp ICs (INA125, INA128):
- Single IC replaces three op-amps
- Programmable gain (via single resistor)
- Superior CMRR (>100dB)
- Matched resistors internally
- Easier to use than discrete implementation

Cost: ~$3-5 per IC (vs $0.50 per op-amp × 3)

Trade-off: Discrete flexibility vs. integrated convenience.

## Key Concepts Reinforced

- **Differential signal**: Information in V+ - V-
- **Common-mode signal**: Noise common to both inputs
- **CMRR**: Rejection ratio of common-mode vs differential
- **Bridge sensor**: Converts physical quantity to small voltage difference
- **Instrumentation amp**: Specialty circuit for precision measurement

## Next Steps

1. **Project 6: Logarithmic Amp** - Exponential function conversion
2. **Project 10: Complete Audio System** - Apply to audio measurement
3. **Advanced lab: Data acquisition** - Build ADC system with INA frontend

---

**Key Takeaway**: Instrumentation amplifiers solve the problem of measuring small differential signals in the presence of large common-mode noise. By using three op-amps with carefully matched resistors, they achieve 80-100dB common-mode rejection while amplifying the desired differential signal—essential for precision measurement systems in industry and medicine.
