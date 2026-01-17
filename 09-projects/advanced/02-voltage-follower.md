# Advanced Project 2: Voltage Follower (High-Impedance Buffer)

**Difficulty**: ⭐⭐⭐ (Advanced)  
**Time**: 60 minutes  
**Concept**: Unity-gain buffer, impedance transformation, loading effects, high input impedance

## What You'll Learn

- Op-amp as voltage follower (unity-gain buffer)
- Input impedance boosting
- Output impedance reduction
- Loading effects and impedance matching
- Practical applications in signal conditioning

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| Op-Amp IC | 2 | TL072 or LM358 |
| Resistor (10kΩ) | 2 | Load resistance testing |
| Capacitor (100nF) | 2 | Bypass capacitors |
| Power Supply | 1 | Dual ±5V to ±15V |
| Function Generator | 1 | 1Hz-100kHz |
| Oscilloscope | 1 | 2-channel |
| Breadboard | 1 | Standard |

## Theory: Voltage Follower

**Basic concept**: Op-amp output follows input voltage with unity gain (Vout = Vin).

**Configuration**: Feedback from output directly to inverting input (100% feedback).

**Gain equation**:
$$A = \frac{Z_f}{Z_i} + 1$$

With 100% feedback (Zf = output, Zi = input):
$$A = 1 + 1 = 1$$ (approximately, actually slightly less than 1)

**Inverting input voltage** (golden rule):
$$V_- = V_+ = V_{in}$$

No current into op-amp inputs (ideal), so no voltage drop.

**Output voltage**:
$$V_{out} = V_{in}$$

### Input Impedance Transformation

**Without buffer**:
- Direct connection to load
- Input impedance = load impedance
- Example: 10kΩ source into 10kΩ load = voltage divider effect
- Output voltage reduced by 50%

**With voltage follower buffer**:
- Op-amp input impedance very high (1MΩ+ typical)
- Load sees high impedance input
- No loading effects
- Output voltage = input voltage (unity gain)

**Input impedance boost**:
$$Z_{in,buffered} = Z_{in,opamp} \times (1 + A \times \beta)$$

Where A = open-loop gain, β = feedback factor.

For typical op-amp: Z_in increases 1000× or more.

### Output Impedance Reduction

**Without buffer**:
- Source impedance = internal source resistance (high for some sources)
- Load affected by source impedance
- Signal divided by source:load impedance ratio

**With buffer**:
- Output impedance = Zout(opamp) / (1 + loop gain)
- Typically mΩ range (very low)
- Can drive loads without signal degradation

## Breadboard Layout - Dual Buffer Comparison

```
Input Signal
     |
     +---[10kΩ Source]---+
                         |
              (Path 1: Direct to Load)
              (Path 2: Through Buffer)
                         |
     +---------[Buffer OpAmp]---+
     |                          |
[Load 10kΩ]              [Buffered Load 10kΩ]
     |                          |
    GND                        GND
```

Two paths: direct (showing loading) and buffered (no loading).

## Building Instructions

### Part 1: Direct Connection (Baseline)

1. **Connect source resistor**:
   - Insert 10kΩ resistor from function generator output to Row 2

2. **Connect load resistor**:
   - Insert 10kΩ resistor from Row 2 to GND (Row 3)
   - This is the load

3. **Test baseline**:
   - Function generator: 5V peak sine wave, 1kHz
   - Measure voltage across load resistor (Row 2)
   - Expected: 2.5V (voltage divider effect, 50% loss)

### Part 2: Buffered Connection

1. **Insert op-amp (unity-gain configuration)**:
   - Pin 3 (non-inverting): Connect to Row 2 (input signal)
   - Pin 2 (inverting): Connect directly to Pin 6 (output) - 100% feedback
   - Pin 6 (output): Your buffered output
   - Pin 4, 8: Power supply (±15V)

2. **Connect second load**:
   - Insert 10kΩ resistor from Pin 6 (output) to GND
   - This is the buffered load

3. **Test buffered output**:
   - Measure voltage across buffered load resistor
   - Expected: ~5V (no voltage division, full signal)

## Measurement Plan

### Direct Connection Test

1. **Measure source voltage** (at Row 2, before load):
   - Black probe: GND
   - Red probe: Row 2
   - With no load: should be ~5V
   - Actual: ______

2. **Measure loaded voltage** (with 10kΩ load connected):
   - Black probe: GND
   - Red probe: Row 2 (across load)
   - Expected: ~2.5V (voltage divider: 10kΩ source ÷ 20kΩ total)
   - Actual: ______

### Buffered Connection Test

1. **Measure buffered output voltage**:
   - Black probe: GND
   - Red probe: Pin 6 (op-amp output)
   - With 10kΩ load connected
   - Expected: ~4.9V (nearly full value, no loading)
   - Actual: ______

### Loading Effect Comparison

| Configuration | Input Voltage | Output Voltage | Loading Effect |
|---|---|---|---|
| Direct (no load) | 5V | 5V | None |
| Direct (with 10kΩ load) | 5V | 2.5V | 50% drop |
| Buffered input | 5V | ~5V | ~2% drop |
| Buffered output | 5V | ~4.9V | Minimal |

### Frequency Response

Test both configurations across frequency range:

| Frequency | Direct V | Buffered V | Difference |
|---|---|---|---|
| 1 Hz | 2.5V | 4.9V | Buffered wins |
| 100 Hz | 2.5V | 4.9V | Buffered wins |
| 10 kHz | ~2.5V | ~4.9V | Buffered stable |
| 100 kHz | May sag | ~4.8V | Buffered better |

## Visual Verification

- ✓ Direct path shows voltage divider effect (reduced output)
- ✓ Buffered path shows full signal (no reduction)
- ✓ Buffer output stable across frequency range

## Key Insight: Impedance Matching

**Problem solved by voltage follower**:
- High source impedance → signal reduced by loading
- Multiple loads → signal degrades
- Cascade stages → each stage loads previous

**Solution**: Place voltage follower between source and loads.

**Real-world examples**:
- Microphone preamplifier (very high impedance input)
- Guitar amplifier input (high-impedance input stage)
- Sensor interface (prevents loading of delicate sensors)

## Output Impedance Measurement

**Method**: Measure output voltage with different load resistances.

1. **No load**:
   - Remove load resistor
   - Measure output voltage: ~5V
   - Current drawn: ~0µA

2. **With 10kΩ load**:
   - Connect 10kΩ to output
   - Measure voltage: ~4.9V
   - Current: ~0.49mA

3. **With 1kΩ load**:
   - Connect 1kΩ to output
   - Measure voltage: ~4.8V
   - Current: ~4.8mA

4. **Calculate output impedance**:
   - Zout = ΔV / ΔI
   - Zout ≈ (5V - 4.8V) / (0mA - 4.8mA) ≈ 42Ω

Very low output impedance (typically 10-100Ω for op-amp buffers).

## Input Impedance Verification

**Method**: Measure input current required.

**Ideal op-amp**: Input current ≈ 0 (both + and - inputs)
**Real op-amp**: Input bias current ~50-100pA (picoamps)

**Consequence**: Even with 1MΩ input resistor, voltage drop minimal.

## Gain Accuracy Test

**Measure gain across range**:

| Input V | Output V | Gain |
|---|---|---|
| 0.5V | 0.49V | 0.98 |
| 1V | 0.99V | 0.99 |
| 2V | 1.98V | 0.99 |
| 5V | 4.90V | 0.98 |

Gain ≈ 0.98-0.99 (slightly less than 1.0 due to non-ideal op-amp feedback).

## Troubleshooting

**Output doesn't follow input**:
- Feedback connection broken (pin 2 to pin 6)
- Power supply not connected
- Op-amp damaged

**Output oscillates**:
- Capacitive load too high
- Add small series resistor (100Ω) at output
- Check bypass capacitors on power supply

**Gain not 1.0**:
- Normal (real op-amps slightly less than unity)
- If gain > 1.0, feedback might not be 100%
- Check connection from output to inverting input

## Challenge Extensions

1. **Measure input impedance**:
   - Build parallel RC circuit representing input impedance
   - Calculate capacitive reactance at different frequencies
   - See how high impedance affects high-frequency response

2. **Buffer with gain**:
   - Add resistors between inverting input and output
   - Create non-unity gain (Gain = 1 + Rf/Rg)
   - Still maintains high input impedance

3. **Cascaded buffers**:
   - Chain multiple followers
   - Measure cumulative effect on output impedance
   - Should decrease with each stage

4. **Source impedance effect**:
   - Use different source resistors (1kΩ, 100kΩ, 1MΩ)
   - Without buffer: all show loading effects
   - With buffer: all show same output

## Real-World Applications

- **Microphone preamplifier**: Buffer high-impedance capsule
- **Guitar amplifier**: Prevent loading of guitar pickups
- **Data acquisition**: Isolate sensors from measurement circuit
- **Audio distribution**: Drive multiple loads without degradation
- **Sensor interface**: Protect delicate sensor circuits

## Advanced: JFET Input Op-Amps

For extremely high impedance (>1TΩ):
- Use op-amps with JFET input stage (TL071, OPA2134)
- Input current drops to femtoamps (10^-15 A)
- Essential for high-impedance sensor measurements

## Key Concepts Reinforced

- **Voltage follower**: Unity-gain buffer with high input impedance
- **Impedance transformation**: Isolate source from load
- **Loading effects**: Reduced without buffering
- **Golden rule**: V+ = V- (at equilibrium)
- **Output impedance**: Very low for op-amp outputs

## Next Steps

1. **Project 3: Comparator** - Switch from analog to digital
2. **Project 4: Precision Amplifier** - Add gain to buffering
3. **Project 5: Instrumentation Amp** - Differential measurement

---

**Key Takeaway**: Voltage followers solve impedance matching problems by presenting very high input impedance and very low output impedance. This prevents loading effects and allows a high-impedance source to drive multiple loads without signal degradation—essential for professional signal conditioning and measurement circuits.
