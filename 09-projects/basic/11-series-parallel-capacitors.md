# Basic Project 11: Series and Parallel Capacitors

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 20 minutes  
**Concept**: Capacitance addition rules, timing control, energy storage

## What You'll Learn

- Capacitances add like resistors (reversed rules)
- Series capacitors: 1/C_total = 1/C1 + 1/C2...
- Parallel capacitors: C_total = C1 + C2 + ...
- How to tune timing circuits

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 2 | Visual indicators |
| 220Ω Resistor | 2 | LED current limiting |
| 1kΩ Resistor | 1 | Timing resistor |
| 470µF Capacitor | 2 | Series/parallel test |
| 100µF Capacitor | 1 | Alternative for comparison |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Measure capacitance and voltage |

## Theory: Capacitor Combinations

Capacitors combine in **opposite way** from resistors:

### Series Capacitors

$$\frac{1}{C_{total}} = \frac{1}{C_1} + \frac{1}{C_2} + ... + \frac{1}{C_n}$$

Example: Two 470µF in series:
$$\frac{1}{C_{total}} = \frac{1}{470µ} + \frac{1}{470µ} = \frac{2}{470µ}$$
$$C_{total} = \frac{470µ}{2} = 235µF$$

**Key insight**: Series capacitors = half the capacitance (opposite of resistors).

**Voltage across series capacitors**:
- Divides inversely with capacitance
- Identical capacitors split voltage evenly

**Use case**: Reduce capacitance, adjust timing, or handle higher voltages.

### Parallel Capacitors

$$C_{total} = C_1 + C_2 + ... + C_n$$

Example: Two 470µF in parallel:
$$C_{total} = 470µ + 470µ = 940µF$$

**Key insight**: Parallel capacitors = sum of capacitances.

**Voltage across parallel capacitors**:
- All see same voltage (parallel connection)

**Use case**: Increase capacitance, slower timing, more energy storage.

## Breadboard Layout - Series Configuration

```
        +5V
         |
       [1kΩ R]
         |
      [C470µ]
         |
      [C470µ]
         |
        GND
```

First capacitor top lead charged to +5V side.
Second capacitor bottom lead at GND.
Voltage divides between them.

## Breadboard Layout - Parallel Configuration

```
        +5V
         |
       [1kΩ R]
         |
    +----+----+
    |         |
  [C1]      [C2]
  470µ      470µ
    |         |
    +----+----+
         |
        GND
```

Both capacitors across full +5V.

## Building Instructions - Part 1: Series Capacitors

### Step 1: Build Series Circuit
1. Insert 1kΩ resistor from +5V to Row 2
2. Insert first 470µF capacitor: positive to Row 2, negative to Row 3
3. Insert second 470µF capacitor: positive to Row 3, negative to Row 4
4. Connect Row 4 to GND

### Step 2: Charge and Measure
1. Power up (capacitors charge through 1kΩ resistor)
2. Wait 5 seconds for full charge
3. Measure voltage between capacitors (Row 3, relative to GND)
   - Expected: ~2.5V (half of 5V due to equal capacitors)
   - Actual: ______

### Step 3: Calculate Capacitance
- Series: 1/C_total = 1/470 + 1/470 = 2/470
- C_total = 235µF
- Time constant: τ = 1kΩ × 235µF = 235ms

## Building Instructions - Part 2: Parallel Capacitors

### Step 1: Reconfigure to Parallel
1. Remove both capacitors
2. Insert first 470µF capacitor: positive to +5V via Row 2, negative to Row 3
3. Insert second 470µF capacitor: positive to Row 2 (same junction), negative to Row 3 (same junction)
4. Connect Row 3 to GND through 1kΩ resistor

### Step 2: Charge and Measure
1. Power up
2. Both capacitors charge in parallel
3. Voltage across both: ~5V (parallel characteristic)
4. Total charge: double the series case

### Step 3: Calculate Capacitance
- Parallel: C_total = 470µF + 470µF = 940µF
- Time constant: τ = 1kΩ × 940µF = 940ms (4× series time)
- Charging takes 4 times longer

## Measurement Plan - Series Configuration

1. **Voltage distribution**:
   - Black probe: GND
   - Red probe: Row 3 (junction between capacitors)
   - Expected: 2.5V (equal split)
   - Actual: ______
   
   - Voltage across first capacitor: 5V - 2.5V = 2.5V
   - Voltage across second capacitor: 2.5V - 0V = 2.5V
   - Sum: 5V (Kirchhoff's voltage law) ✓

2. **Total capacitance** (if multimeter has capacitance mode):
   - Measure directly: Expected ~235µF
   - Actual: ______

3. **Charging time**:
   - Discharge, then time to reach 2.5V at junction
   - Expected: ~235ms (one time constant)
   - Actual: ______

## Measurement Plan - Parallel Configuration

1. **Voltage across each capacitor**:
   - Both should measure 5V (parallel = same voltage)
   - Verify: Equal? Yes/No

2. **Total capacitance**:
   - Measure directly: Expected ~940µF
   - Actual: ______

3. **Charging time**:
   - Time to reach ~5V at capacitor
   - Expected: ~940ms (much slower than series)
   - Actual: ______

## Comparison Table

| Property | Series | Parallel |
|----------|--------|----------|
| **Total C** | 235µF | 940µF |
| **Voltage division** | Splits evenly | Same across both |
| **Charge stored** | Lower | Higher |
| **Time constant** | Faster | Slower |
| **Energy** | Lower | Higher |

## Visual Verification

- ✓ **Series**: Voltage at junction = ~2.5V
- ✓ **Parallel**: Voltage = 5V across both
- ✓ **Parallel charges slower** (more capacitance = longer τ)

## Key Insight: Opposite Rules

**Resistors**:
- Series: R_total = R1 + R2 (add directly)
- Parallel: 1/R_total = 1/R1 + 1/R2 (reciprocal)

**Capacitors** (opposite!):
- Series: 1/C_total = 1/C1 + 1/C2 (reciprocal)
- Parallel: C_total = C1 + C2 (add directly)

**Why opposite?**
- Current through series resistors same (resistance increases total)
- Voltage across series capacitors same (capacitance decreases total)
- Current through parallel resistors splits (equivalent resistance decreases)
- Voltage across parallel capacitors same (total capacitance increases)

## Energy Storage Comparison

**Energy in capacitor**: E = ½ C V²

**Series configuration** (235µF at 2.5V each):
- Total energy ≈ ½ × 235µF × (5V)² = 2.9mJ
- Divided between both capacitors

**Parallel configuration** (940µF at 5V each):
- Total energy ≈ ½ × 940µF × (5V)² = 11.75mJ
- 4× more energy (matches 4× capacitance)

## Troubleshooting

**Voltage doesn't divide in series**:
- Verify both capacitors properly connected in series
- Check capacitor polarity (should be series chain: + to -, + to -, + to -)
- If one reversed, circuit won't work as expected

**Parallel capacitors charge too slowly**:
- This is expected (4× time constant with series resistor)
- Normal behavior: more capacitance = slower charging

**Voltage not equal in parallel**:
- One capacitor might be leaky (internal resistance)
- Or capacitor value significantly different than expected
- Use multimeter to measure actual capacitance

## Challenge Extensions

1. **Three capacitors in series**:
   - 1/C = 1/470 + 1/470 + 1/470 = 3/470
   - C_total ≈ 157µF
   - Voltage divides into thirds: ~1.67V at each junction

2. **Three capacitors in parallel**:
   - C_total = 470 + 470 + 470 = 1410µF
   - Time constant: τ = 1kΩ × 1410µF = 1410ms (~1.4 seconds)
   - Much slower charging

3. **Mixed series-parallel**:
   - Two 470µF in parallel (940µF)
   - In series with one 470µF
   - 1/C = 1/940 + 1/470 = 3/940
   - C_total ≈ 313µF
   - Interesting intermediate value

4. **Adjustable capacitance**:
   - Switch between different configurations
   - Create adjustable timing circuit
   - Use relay or manual switch to reconfigure

## Real-World Applications

- **Power supplies**: Large parallel capacitors for energy storage
- **Timing circuits**: Series capacitors for precise timing
- **Energy harvesting**: Large capacitors for energy buffer
- **Filtering**: Multiple capacitors for broad frequency range

## Advanced: Capacitor Tolerance

Real capacitors have tolerance (±10%, ±20% typical).

**Series effect**: Tolerance multiplied by position
- First series capacitor: tight tolerance needed for equal split

**Parallel effect**: Tolerance adds
- Multiple parallel capacitors: total tolerance usually acceptable

## Key Concepts Reinforced

- **Series capacitors**: Reciprocal formula (1/C_total = 1/C1 + 1/C2)
- **Parallel capacitors**: Direct sum (C_total = C1 + C2)
- **Voltage division**: Series capacitors split voltage
- **Same voltage**: Parallel capacitors all see same voltage
- **Timing impact**: Parallel increases time constant, series decreases

## Next Steps

1. **Project 12: Power Dissipation** - Calculate heat from circuits
2. **Intermediate Project 2: RC Oscillator** - Use capacitor combinations for timing
3. **Intermediate Project 5: Active Filter** - Stack capacitors for complex filtering

---

**Key Takeaway**: Capacitors combine opposite to resistors—series capacitances add reciprocally (total decreases), while parallel capacitances add directly (total increases). This allows precise timing control by mixing series and parallel configurations in the same circuit.
