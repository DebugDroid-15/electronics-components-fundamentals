# Basic Project 4: Voltage Divider

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 25 minutes  
**Concept**: Voltage divider, proportional voltage distribution, fundamental building block

## What You'll Learn

- Voltage divider formula (fundamental circuit)
- How to get intermediate voltages from fixed supply
- Proportional voltage relationships
- Why potentiometers work (they're variable voltage dividers)

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 2 | Visual indicators |
| 1kΩ Resistor | 2 | Divider resistors |
| 220Ω Resistor | 2 | Current limiting |
| Multimeter | 1 | Essential for measuring |
| Jumper wires | 8 | Breadboard connections |
| Breadboard | 1 | Same as previous |

## Theory: Voltage Divider

A **voltage divider** uses two resistors in series to create intermediate voltages.

**Formula** (most important):
$$V_{out} = V_{in} \times \frac{R_2}{R_1 + R_2}$$

Where:
- V_in = input voltage (5V)
- R_1 = upper resistor (from +5V)
- R_2 = lower resistor (to ground)
- V_out = voltage at junction between resistors

**Example**: Two 1kΩ resistors with 5V input:
$$V_{out} = 5V \times \frac{1k}{1k + 1k} = 5V \times \frac{1}{2} = 2.5V$$

Output is half the input voltage.

**Why it matters**:
- Gets intermediate voltages without separate power supply
- Simplest circuit for analog measurement/control
- Basis for potentiometers, sensors, feedback systems
- Used in every analog-to-digital converter

## Breadboard Layout

```
        +5V
         |
       [R1]
         |
      [+]------- Measured voltage (V_out)
      [|]
       [R2]
         |
        GND
```

Measurement point between R1 and R2.

## Building Instructions

### Step 1: Build Basic Voltage Divider
1. Insert 1kΩ resistor from +5V to Row 2 (middle of breadboard)
2. Insert second 1kΩ resistor from Row 2 to Row 3
3. Connect Row 3 to GND with jumper wire

### Step 2: Add Load #1 (Optional Load)
1. Insert 220Ω resistor from Row 2 to Row 4
2. Insert first LED anode into Row 4
3. Insert first LED cathode to Row 5
4. Connect Row 5 to GND

### Step 3: Add Load #2 (After Ground Reference)
1. Insert another 220Ω resistor from Row 3 to Row 6
2. Insert second LED anode into Row 6
3. Insert LED cathode to Row 7
4. Connect Row 7 to GND

**Configuration**:
- Divider taps intermediate voltage (Row 2 ≈ 2.5V)
- Two LEDs: one at ~2.5V (dimmer), one at ~0V (off) or ground

## Measurement Plan

**Predictions** (before building):
- V_out at junction: 2.5V (with equal resistors)
- First LED (at 2.5V): May glow faintly if any current
- Second LED (at GND): Off

**Detailed measurements**:

1. **Voltage divider output** (Row 2): This is the fundamental measurement
   - Black probe: GND
   - Red probe: Row 2 (junction between resistors)
   - Expected: 2.5V
   - Actual: ______

2. **Verify formula**:
   - Measured R1: ______ Ω (measure with ohmmeter)
   - Measured R2: ______ Ω
   - Formula: V_out = 5V × R2/(R1+R2) = ______ V
   - Measurement matches formula? Yes/No

3. **Effect of load on divider**:
   - Voltage with LED load attached: ______ V (usually drops slightly)
   - This is **loading effect** (more on this later)

4. **Try different resistor ratio**:
   - Remove one 1kΩ, insert 470Ω instead
   - New R1 = 1kΩ, R2 = 470Ω
   - Predict: V_out = 5V × 470/(1000+470) = 5V × 0.32 = 1.6V
   - Measure: ______ V

## Visual Verification

- ✓ First LED glows faintly (2.5V isn't enough for full brightness)
- ✓ Second LED is off (at GND, 0V drop across it)
- ✓ Resistors cool to touch (low current through divider)

## Key Insight: Loading Effect

The voltage divider formula assumes **no load** (infinite input impedance).

With an LED load attached:
- Load draws current
- This affects the voltage at tap point
- Voltage drops more than predicted by formula

**Mathematical detail**:
- Ideal (no load): V_out = 2.5V
- With load: V_out might be 2.0V (lower)
- Difference = loading effect

This is why we specify "output impedance" of dividers.

## Interactive Variant: Variable Divider

In Project 8, you'll use a **potentiometer** (variable resistor), which is essentially a voltage divider where you slide the tap point.

The formula remains the same, but R2 changes as you turn the knob.

## Troubleshooting

**Output voltage not 2.5V**:
- Check resistor values (use multimeter ohms mode)
- Verify connections (should be series between +5V and GND)
- Measure both R1 and R2 voltage drops (should sum to 5V)

**LED at tap point is too bright or too dim**:
- Tap voltage may differ from expected 2.5V
- This is normal if resistors aren't perfectly 1kΩ
- Adjust 220Ω current-limit resistor if needed

**Voltage changes when touching probe**:
- This is real! Your body has resistance
- Demonstrates loading effect very clearly
- Higher impedance probe causes less loading

## Challenge Extensions

1. **Three-resistor divider**:
   - Add third resistor: 1kΩ between R2 and GND
   - Create voltage at two different tap points
   - Predict: ~1.67V at middle tap

2. **1/4 divider**:
   - Use 3kΩ for R1, 1kΩ for R2
   - Predict: V_out = 5V × 1k/(3k+1k) = 1.25V
   - Build and measure

3. **Sensitive to resistor ratio**:
   - Change to 10kΩ and 1kΩ
   - Predict: V_out = 5V × 1k/(10k+1k) = 0.45V
   - Very small output voltage
   - Measure to verify

4. **Potentiometer preview**:
   - Potentiometer is variable divider
   - As you turn it, tap point moves
   - This is why potentiometers are so useful

## Mathematical Deep Dive

**General formula**:
$$V_{out} = V_{in} \times \frac{R_2}{R_1 + R_2}$$

**Can be rewritten**:
$$\frac{V_{out}}{V_{in}} = \frac{R_2}{R_1 + R_2}$$

Output voltage is proportional to the lower resistor.

**Impedance**:
$$Z_{out} = R_1 \parallel R_2 = \frac{R_1 \times R_2}{R_1 + R_2}$$

For equal resistors (1k + 1k): Z_out = 500Ω

**Loading analysis**:
- If load impedance >> Z_out, negligible loading
- If load impedance similar to Z_out, voltage drops
- If load impedance << Z_out, divider collapses

This is why op-amp voltage followers exist (Project for later).

## Key Concepts Reinforced

- **Voltage divider formula**: Core analog circuit principle
- **Proportional division**: Output based on resistor ratio
- **Output impedance**: Lower means less loading effect
- **Practical limitation**: Loading causes deviation from ideal formula
- **Universal application**: Used in sensors, controls, measurements

## Real-World Applications

- **Potentiometers**: Variable voltage dividers (volume knobs, joysticks)
- **Analog sensors**: Light sensors, temperature sensors all use dividers
- **ADC inputs**: Preparing signals for measurement
- **Feedback networks**: Control systems rely on divided voltages
- **Current sensing**: Voltage drop across sense resistor is divided

## Next Steps

1. **Project 5: Pushbutton Control** - Add interaction to circuits
2. **Project 6: Potentiometer Brightness** - Dynamic voltage divider
3. **Project 8: Voltage divider with feedback** - Advanced concepts

---

**Key Takeaway**: Voltage dividers enable intermediate voltages from a fixed supply using just two resistors. The output is determined entirely by the resistance ratio, making this the foundation for analog electronics, sensor interface circuits, and feedback control systems.
