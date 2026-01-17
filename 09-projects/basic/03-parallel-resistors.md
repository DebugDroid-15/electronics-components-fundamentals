# Basic Project 3: Parallel Resistors

**Difficulty**: ⭐ (Absolute beginner)  
**Time**: 20 minutes  
**Concept**: Parallel resistance, current division, voltage across parallel components

## What You'll Learn

- Resistances are reciprocal in parallel: 1/R_total = 1/R1 + 1/R2 + ...
- Voltage is same across all parallel components
- Current splits based on resistance (lower R gets more current)
- Difference between series and parallel

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 2 | Two parallel loads |
| 220Ω Resistor | 2 | One for each LED |
| Jumper wires | 8 | More connections needed |
| Breadboard | 1 | Same as Projects 1&2 |

## Theory: Parallel Resistors

**Parallel connection**: Components share the same voltage, current splits between them.

**Total resistance** (reciprocal rule):
$$\frac{1}{R_{total}} = \frac{1}{R_1} + \frac{1}{R_2} + ... + \frac{1}{R_n}$$

**Example**: Two 1kΩ resistors in parallel:
$$\frac{1}{R_{total}} = \frac{1}{1k} + \frac{1}{1k} = \frac{2}{1k}$$
$$R_{total} = \frac{1k}{2} = 500Ω$$

**Practical insight**: Two equal resistors in parallel = half the resistance.

**Voltage**: All parallel branches see same voltage (5V in this project).

**Current division** (inverse proportion to resistance):
$$\frac{I_1}{I_2} = \frac{R_2}{R_1}$$

Example: If R1 = 220Ω and R2 = 1kΩ in parallel:
$$\frac{I_1}{I_2} = \frac{1000}{220} = 4.5$$

R1 carries 4.5× more current (lower resistance = more current).

**Total current** = sum of branch currents:
$$I_{total} = I_1 + I_2 + I_3 + ... + I_n$$

## Breadboard Layout

```
        +5V
        |
    +---+---+
    |       |
   [R1]   [R2]
    |       |
   [L1]   [L2]
    |       |
    +---+---+
        |
       GND
```

**Both branches**: Same voltage (5V), separate current paths.

## Building Instructions

### Step 1: Create First Branch
1. Insert 220Ω resistor from +5V to a middle column (Row 2)
2. Insert first LED anode into Row 2 (same junction)
3. Insert first LED cathode into Row 3

### Step 2: Create Second Branch (Parallel to First)
1. Insert second 220Ω resistor from +5V to Row 2 (same junction as first resistor)
2. Insert second LED anode into Row 2
3. Insert second LED cathode into Row 3 (same column as first LED cathode)

### Step 3: Complete Circuit
1. Connect Row 3 to GND with jumper wire
2. Power up
3. Both LEDs light up with equal brightness (identical resistors and LEDs)

**Note**: Both branches are in parallel = both see 5V.

## Measurement Plan

**Predictions**:
- Voltage across each LED: 2.0V (same as series, LEDs in parallel)
- Voltage across each resistor: 3.0V (5V - 2V)
- Current through each branch: (5V - 2V) / 220Ω = 13.6mA
- Total current: 13.6 + 13.6 = 27.2mA (double single branch)

**Measurements**:
1. **Voltage across resistor 1**: Place probes across first 220Ω resistor
   - Expected: ~3.0V
   - Actual: ______

2. **Voltage across resistor 2**: Place probes across second 220Ω resistor
   - Expected: ~3.0V
   - Actual: ______

3. **Verify same voltage**: Both should be 3.0V (parallel characteristic)
   - Difference: ______ (should be < 0.1V)

4. **Total current** (if multimeter supports): Use ammeter mode in series with power supply
   - Expected: ~27mA (both branches)
   - Actual: ______

5. **Compare to Project 1**:
   - Project 1 (single LED): ~13mA
   - Project 3 (two parallel): ~27mA (double)
   - This demonstrates current addition in parallel

## Visual Verification

- ✓ Both LEDs glow equally bright (same conditions)
- ✓ Resistors warm to touch (more total current than Project 1)
- ✓ Brighter overall (two LEDs contributing light)

## Key Differences: Series vs. Parallel

| Property | Series | Parallel |
|----------|--------|----------|
| **Voltage** | Divides | Same across all |
| **Current** | Same everywhere | Divides |
| **Total R** | R_total = R1 + R2 | 1/R_total = 1/R1 + 1/R2 |
| **Example** | Dimmer load | Brighter load |

## Troubleshooting

**LEDs have different brightness**:
- Check resistor values (use multimeter to verify)
- Check LED polarity (both anodes must go to positive rail)
- Check connections (both must see same voltage)

**Both LEDs very bright**:
- Resistor value wrong (check color code)
- Should be 220Ω, not 22Ω

**One LED is much dimmer**:
- Branch not properly in parallel
- Use multimeter to verify voltage (should be 3V across each)

## Challenge Extensions

1. **Add third LED in parallel**:
   - Predict total current: 3 × 13.6mA = ~40.8mA
   - All three should light equally
   - Measure and verify

2. **Parallel different resistors**:
   - Try 220Ω in one branch, 470Ω in other
   - Use current division: I_220 / I_470 = 470 / 220 = 2.1
   - 220Ω branch should carry 2.1× more current
   - Measure LED brightness (brightness ∝ current, but nonlinear)

3. **Calculate equivalent resistance**:
   - Two 220Ω: 1/R = 1/220 + 1/220 = 2/220 → R = 110Ω
   - Two 1kΩ: R = 500Ω
   - Measure with multimeter (turn off power first!)

4. **Power comparison**:
   - Single LED: P = 13.6mA × 2V ≈ 27mW
   - Two parallel: P = 27.2mA × 2V ≈ 54mW (double power)
   - Why? More current due to lower total resistance

## Key Concepts Reinforced

- **Parallel circuit**: Multiple paths, voltage same, current splits
- **Reciprocal formula**: 1/R_total for parallel circuits
- **Current division**: Lower R branches carry more current
- **Load effect**: More branches = lower total R = higher total current
- **Power addition**: P_total = P_1 + P_2 + ... (total power increases)

## Real-World Example

**Household outlets in parallel**:
- All outlets see 120V (parallel to wall supply)
- Each device draws own current based on its resistance
- Total house current = sum of all device currents
- This is why breaker trips if too many devices run simultaneously

## Next Steps

1. **Project 4: Voltage Divider** - Combine series + parallel concepts
2. **Project 5: Pushbutton Control** - Add switches to parallel circuits
3. **Project 8: Potentiometer Brightness** - Vary parallel loads

---

**Key Takeaway**: In parallel circuits, voltage is constant across all branches, current divides inversely with resistance, and total resistance decreases. This enables independent control of multiple loads—foundation for many practical circuits.
