# Intermediate Project 3: Zener Voltage Regulator

**Difficulty**: ⭐⭐ (Intermediate)  
**Time**: 30 minutes  
**Concept**: Voltage regulation, Zener diodes, reference voltages, load regulation

## What You'll Learn

- How Zener diodes regulate voltage
- Zener reverse breakdown characteristics
- Load regulation principles
- Why voltage regulators are essential
- Limitations of passive Zener regulation

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| Zener Diode | 1 | 5.1V 0.5W (or similar) |
| Resistor (1kΩ) | 1 | Series limiting resistor |
| Resistor (10kΩ) | 1 | Variable load resistor |
| Capacitor (100µF) | 1 | Output filtering |
| Power Supply | 1 | 5-12V adjustable (variable voltage source) |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Measure voltage and current |

**Alternative**: Use previous rectifier output (Project 2) with varying input as supply.

## Theory: Zener Regulation

### Zener Diode Characteristics

**Normal diode operation**:
- Forward bias: Conducts ~0.7V
- Reverse bias: Blocks (open circuit)

**Zener diode operation**:
- Forward bias: Same as normal (~0.7V)
- **Reverse bias: CONDUCTS at specific voltage** (reverse breakdown)

This is the opposite of normal diodes!

**Zener voltage** (V_Z):
- 5.1V Zener: Conducts in reverse at exactly 5.1V
- Current increases, but voltage stays ~5.1V
- This is called **Zener breakdown** or **avalanche breakdown**

**Voltage regulation principle**:
- Supply varies 7V → 15V
- Zener maintains output at 5.1V ± 5%
- Excess voltage drops across series resistor

### Zener Voltage Equation

**Current through series resistor**:
$$I_S = \frac{V_{in} - V_Z}{R_s}$$

Where:
- V_in = input voltage
- V_Z = Zener voltage (5.1V)
- R_s = series resistor

**Current splits**:
$$I_S = I_Z + I_L$$

Where:
- I_Z = current through Zener
- I_L = current to load

**Load regulation** (Zener automatically adjusts):
- If load increases: More current needed, Zener current decreases
- If load decreases: Less current needed, Zener current increases
- But output voltage stays constant at V_Z

### Limitations

**Cannot supply current more than**:
$$I_{max} = \frac{V_{in,max} - V_Z}{R_s}$$

Example with V_in = 15V, V_Z = 5.1V, R_s = 1kΩ:
$$I_{max} = \frac{15V - 5.1V}{1000Ω} = 9.9mA$$

This is a key limitation: Zener regulators can only supply modest current.

## Breadboard Layout - Zener Regulator

```
        V_in (7-15V)
         |
       [R_s 1kΩ]
         |
    +----+----+
    |         |
   [Z]       [R_load]
   5.1V      10kΩ
    |         |
    +----+----+
         |
        GND
```

Zener in parallel with load, series resistor limits current.

## Building Instructions

### Part 1: Build Basic Regulator

1. **Insert series resistor**:
   - Insert 1kΩ resistor from V_in to Row 2

2. **Insert Zener diode**:
   - Identify Zener 5.1V (cathode marked with stripe)
   - Insert cathode (stripe) to Row 2 (same as resistor)
   - Insert anode to Row 3 (GND)
   - **Note**: Reversed orientation compared to normal diode (anode to ground)

3. **Insert load resistor**:
   - Insert 10kΩ resistor from Row 2 to Row 3 (parallel with Zener)
   - This represents the load

4. **Insert filter capacitor** (optional):
   - Insert 100µF capacitor across Zener: positive to Row 2, negative to Row 3
   - Reduces noise on output

### Part 2: Set Up Variable Supply

1. **Use adjustable power supply** (or Project 2 rectifier):
   - Start at 7V (just above Zener voltage)
   - Have ability to increase to 15V

2. **Test across range**:
   - Measure output voltage at each input level

## Measurement Plan

### Output Voltage vs. Input Voltage

Vary V_in and record output voltage:

| V_in | Expected V_out | Actual V_out | Change |
|---|---|---|---|
| 7V | 5.1V | _____ | _____ |
| 8V | 5.1V | _____ | _____ |
| 10V | 5.1V | _____ | _____ |
| 12V | 5.1V | _____ | _____ |
| 14V | 5.1V | _____ | _____ |

**Expected**: Output stays constant at ~5.1V across entire input range.

**Actual**: May vary slightly (0.05V typical) due to Zener internal resistance.

### Line Regulation

**Line regulation** = change in output per change in input.

Formula:
$$\text{Line Reg} = \frac{\Delta V_{out}}{\Delta V_{in}}$$

Example:
- If V_in goes 7V → 14V (7V change)
- If V_out goes 5.08V → 5.12V (0.04V change)
- Line Reg = 0.04 / 7 = 0.57% (excellent)

### Current Measurements

**Measure Zener current**:
- Remove Zener temporarily
- Insert ammeter in its place
- Measure current as V_in varies

**At 7V input** (minimum):
- I_Z = (7V - 5.1V) / 1000Ω = 1.9mA

**At 15V input** (maximum):
- I_Z = (15V - 5.1V) / 1000Ω = 9.9mA

Zener current increases with input (correct regulation behavior).

### Load Regulation

**Load regulation** = change in output voltage when load changes.

1. **Measure with no load**:
   - Remove 10kΩ load resistor
   - Output voltage: _______ V

2. **Measure with 10kΩ load**:
   - Reinsert 10kΩ resistor
   - Output voltage: _______ V

3. **Calculate load regulation**:
   - Expected change: <0.1V
   - Actual change: _______ V

Better regulators show minimal load regulation.

## Visual Verification

- ✓ Output voltage steady across input range
- ✓ Load resistor draws current (not affecting output much)
- ✓ No oscillation (clean DC output)

## Key Insight: Passive Regulation

This is called "**passive regulation**" because:
- Zener diode itself does the work
- No active feedback
- Simple but limited

**Limitations**:
1. Low current capacity (mA range)
2. Line/load regulation not perfect
3. Series resistor wastes power (P = I² × R)
4. Only 10-20% efficient for wide input range

**Why use despite limitations?**
- Very simple (no feedback loop)
- Reliable (no oscillation risk)
- Low noise (simple circuit)
- Good for low-current, stable applications

## Active Regulation (Preview)

**Series regulators** (LM7805, etc.) overcome Zener limitations:
- Use transistor as variable series resistor
- Active feedback maintains voltage to <1% regulation
- Can supply 1A+ current
- Much better efficiency

Project later: Build active regulator using op-amp feedback.

## Troubleshooting

**Output voltage not stable**:
- Zener inserted wrong direction (anode must go to GND)
- Zener might be shorted (test with multimeter)
- Check series resistor value

**Output voltage too low**:
- Wrong Zener value (might be 3.3V instead of 5.1V)
- Check Zener markings
- Verify with multimeter in diode test mode

**Output voltage tracks input** (not regulating):
- Zener not conducting (might be in forward direction)
- Flip Zener orientation
- Or Zener is open (defective)

**Large ripple on output**:
- Filter capacitor missing or disconnected
- Try larger capacitor (470µF)
- Or add series RC filter

## Challenge Extensions

1. **Different Zener values**:
   - Try 3.3V Zener (if available)
   - Output should be ~3.3V instead of 5.1V
   - Verify regulation works at different voltage

2. **Maximum load current**:
   - Progressively reduce 10kΩ load resistor
   - At what point does output voltage drop significantly?
   - Calculate maximum load current from measurements

3. **Efficiency comparison**:
   - Measure input power: P_in = V_in × I_in
   - Measure output power: P_out = V_out × I_load
   - Efficiency = P_out / P_in × 100%
   - Typically 20-50% (very low due to wasted series current)

4. **Add active feedback** (advanced):
   - Use comparator to sense output voltage
   - Control series transistor via comparator
   - Improves regulation significantly
   - Preview of active regulator concept

## Real-World Applications

- **Reference voltage source**: 5.1V Zener used as 5V reference
- **Over-voltage protection**: Zener clamps output when supply spikes
- **Simple regulators**: Low-current applications (bias circuits, LED drivers)
- **Bench power supplies**: Often include Zener pre-regulation

## Why LDO Regulators Replaced Zeners

**LDO (Low DropOut) regulators** (LM7805, AMS1117, etc.):
- Active feedback
- Much higher current capacity (100mA to 3A+)
- Better line and load regulation (<1%)
- Lower dropout voltage (less power waste)
- Cost: ~$0.50 per IC vs. ~$0.10 per Zener

For any serious power supply work, ICs win.

But Zeners still useful for:
- Very simple circuits
- Reference voltages
- Protection circuits
- Educational understanding

## Key Concepts Reinforced

- **Zener breakdown**: Reverse conducting at specific voltage
- **Voltage regulation**: Output constant despite input/load changes
- **Line regulation**: Response to input voltage changes
- **Load regulation**: Response to load current changes
- **Passive regulation**: Simple but limited current capacity

## Next Steps

1. **Project 4: 555 Timer** - Use regulated DC supply
2. **Project 5: Load Switching** - Add transistor for higher current
3. **Advanced: Active Regulator** - Op-amp feedback for precision

---

**Key Takeaway**: Zener diodes maintain constant voltage across a wide input range by automatically adjusting current flow—a process called passive regulation. While simple and reliable, Zeners can supply only modest current and have significant power losses. Understanding Zener operation provides foundation for active regulators used in real power supplies.
