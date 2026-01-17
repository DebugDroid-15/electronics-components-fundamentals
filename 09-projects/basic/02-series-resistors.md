# Basic Project 2: Series Resistors

**Difficulty**: ⭐ (Absolute beginner)  
**Time**: 20 minutes  
**Concept**: Series resistance, voltage drops, current conservation

## What You'll Learn

- Resistances add in series (R_total = R1 + R2 + R3...)
- Total voltage drops across all components
- Current is same everywhere in series circuit
- How to measure and verify predictions

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 1 | Current limiting load |
| 220Ω Resistor | 1 | First series resistor |
| 1kΩ Resistor | 1 | Second series resistor |
| Jumper wires | 5 | Breadboard connections |
| Breadboard | 1 | Same as Project 1 |

## Theory: Series Resistors

**Series connection**: Components connected one after another, same current flows through all.

**Total resistance**:
$$R_{total} = R_1 + R_2 + R_3 + ... + R_n$$

**Example**: 220Ω + 1kΩ = 1220Ω total

**Voltage drop across each resistor** (Ohm's law):
$$V_R = I \times R$$

**Total voltage constraint** (Kirchhoff's voltage law):
$$V_{supply} = V_{R1} + V_{R2} + V_{LED}$$

**Calculate circuit current**:
- Total resistance: 220Ω + 1kΩ = 1220Ω (plus LED ~10Ω, negligible)
- Current: I = 5V / 1220Ω = 4.1mA

**Voltage drops**:
- Across 220Ω: V = 4.1mA × 220Ω = 0.9V
- Across 1kΩ: V = 4.1mA × 1kΩ = 4.1V
- Across LED: V = 2.0V (LED voltage)
- Total: 0.9V + 4.1V + 2.0V = 7.0V (wait, that's > 5V, let me recalculate)

**Correct calculation**:
- Total R: 220 + 1000 = 1220Ω (LED ~2V fixed, not linear resistor)
- Approximate: (5V - 2V) / 1220Ω = 2.5mA

**Voltage drops (revised)**:
- Across 220Ω: 2.5mA × 220Ω = 0.55V
- Across 1kΩ: 2.5mA × 1kΩ = 2.5V
- Across LED: 2.0V (constant)
- Total: 0.55V + 2.5V + 2.0V = 5.05V ≈ 5V ✓

## Breadboard Layout

```
+5V
 |
[220Ω Resistor]
 |
[1kΩ Resistor]
 |
[LED Anode]
 |
[LED Cathode]
 |
GND
```

**All components in single column**, vertically connected.

## Building Instructions

### Step 1: Insert First Resistor (220Ω)
1. Insert one lead into +5V power rail
2. Insert other lead into Row 2 (any column)

### Step 2: Insert Second Resistor (1kΩ)
1. Insert one lead into Row 2 (same column as first resistor, Row 2)
2. Insert other lead into Row 3

### Step 3: Insert LED
1. Insert longer lead (anode) into Row 3 (same column as second resistor)
2. Insert shorter lead (cathode) into Row 4 (different column)

### Step 4: Complete Circuit with Jumper Wire
1. Use jumper wire from Row 4 to GND rail
2. Power up
3. LED should be dimmer than Project 1 (because more resistance)

## Measurement Plan

**Predictions** (before measuring):
- LED current: ~2.5mA (calculated above)
- LED brightness: Dimmer than Project 1 (~13mA)
- Voltage at Row 2 (between resistors): ~4.45V (5V - 0.55V)
- Voltage at Row 3 (LED anode): ~2.0V (LED forward voltage)

**Measurements** (use multimeter):
1. **Voltage at Row 2**: Place black probe on GND, red probe at junction of two resistors
   - Expected: ~4.4V
   - Actual: ______

2. **Voltage at Row 3** (LED anode): Place black probe on GND, red probe at LED longer lead
   - Expected: ~2.0V
   - Actual: ______

3. **Voltage across first resistor** (220Ω): Probe both sides
   - Expected: ~0.55V
   - Actual: ______

4. **Voltage across second resistor** (1kΩ): Probe both sides
   - Expected: ~2.5V
   - Actual: ______

5. **Sum check**: Add all voltage drops, should equal 5V
   - 0.55 + 2.5 + 2.0 = 5.05V ✓

## Visual Verification

- ✓ LED glows red but noticeably dimmer than Project 1
- ✓ 220Ω resistor: cool to touch
- ✓ 1kΩ resistor: warm to touch (most voltage drops here)
- ✓ No burning smell or smoke

## Key Insight: Voltage Divider Effect

The two resistors form a **voltage divider** (more on this in Project 4).

Large resistor (1kΩ) drops large voltage (2.5V).  
Small resistor (220Ω) drops small voltage (0.55V).

**Ratio of voltage drops equals ratio of resistances**:
$$\frac{V_{1k}}{V_{220}} = \frac{1000Ω}{220Ω} = 4.5 \approx \frac{2.5V}{0.55V}$$

This is **voltage division in action**.

## What's Happening

1. Current flows through all components (same path, series connection)
2. Each resistor "uses up" some voltage (V = I × R)
3. Larger resistor drops more voltage
4. Total voltage constraint: sum of drops = supply voltage
5. LED gets whatever voltage is left

## Troubleshooting

**LED doesn't light**:
- Check series connections (each component must be in same column path)
- Verify LED polarity (longer lead toward positive)

**LED very bright** (same as Project 1):
- Second resistor not properly connected
- Use multimeter to verify voltage across it (should be ~2.5V)

**LED doesn't get dimmer** (compared to Project 1):
- Resistor inserted in wrong place (parallel instead of series)
- Use multimeter to check connections

## Challenge Extensions

1. **Add third resistor**: Try 10kΩ in series
   - LED should be even dimmer
   - Predict and measure voltage drops

2. **Change resistor order**:
   - Try 1kΩ first, then 220Ω
   - Does order matter? (It shouldn't for DC)
   - Measure to verify

3. **Calculate any resistor value**:
   - Want exactly 5mA? What total R needed?
   - R = (5V - 2V) / 5mA = 600Ω
   - Use 220Ω + 390Ω to approximate (or series smaller values)

4. **Series capacitor effect** (advanced sneak peek):
   - How does adding capacitor in series affect LED?
   - Capacitor blocks DC → LED turns off
   - (Saves detailed explanation for capacitor projects)

## Key Concepts Reinforced

- **Series circuit**: Same current path through all components
- **Voltage drops**: Ohm's law predicts voltage across each resistor
- **Kirchhoff's voltage law**: Sum of voltage drops = supply voltage
- **Resistance addition**: Total = sum in series (unlike parallel)
- **Measurement verification**: Theory matches practice

## Next Steps

1. **Project 3: Parallel Resistors** - Learn how parallel is different
2. **Project 4: Voltage Divider** - Master this fundamental circuit
3. **Project 5: Pushbutton Control** - Add interaction to series circuits

---

**Key Takeaway**: In series circuits, resistances add, current is constant everywhere, and voltage divides based on resistance ratios. This understanding is foundational for all circuit design.
