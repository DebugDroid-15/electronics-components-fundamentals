# Basic Project 12: Power Dissipation (Feel the Heat)

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 20 minutes  
**Concept**: Power, heat generation, thermal effects, resistor ratings

## What You'll Learn

- Power formula: P = I × V = V²/R = I² × R
- How resistors generate heat
- Resistor power ratings and why they matter
- Why circuit components get warm

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| 5V Power Supply | 1 | USB or battery |
| 1Ω Resistor | 1 | **NOT SAFE FOR MAIN** (use for calculation only) |
| 10Ω Resistor | 1 | Moderate heat generation |
| 100Ω Resistor | 1 | Low heat generation |
| 1kΩ Resistor | 1 | Minimal heat generation |
| 10Ω Power Resistor | 1 | Can handle more power (optional) |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Measure current and voltage |
| **Temperature probe or thermometer** | 1 | Measure heat (optional) |

**⚠️ WARNING**: 1Ω resistor draws 5A at 5V = 25W. **Never connect directly to 5V supply**—will melt the resistor and possibly the breadboard. Calculate only.

## Theory: Power Dissipation

**Power** is the rate of energy consumption.

**Key formulas**:
$$P = V \times I$$
$$P = \frac{V^2}{R}$$
$$P = I^2 \times R$$

Where:
- P = power (watts, W)
- V = voltage (volts, V)
- I = current (amps, A)
- R = resistance (ohms, Ω)

**Power converts to heat** in resistors (useful in heaters, wasteful elsewhere).

**Heat dissipation** (Joule heating):
$$Q = I^2 R t = P \times t$$

Where:
- Q = heat energy (joules, J)
- t = time (seconds, s)

### Example: 10Ω Resistor at 5V

$$I = \frac{V}{R} = \frac{5V}{10Ω} = 0.5A$$

$$P = V \times I = 5V \times 0.5A = 2.5W$$

Or: $P = \frac{V^2}{R} = \frac{25V^2}{10Ω} = 2.5W$

Or: $P = I^2 \times R = (0.5A)^2 \times 10Ω = 2.5W$

**Over 10 seconds**: $Q = 2.5W \times 10s = 25 \text{ joules}$

(Enough to heat the resistor noticeably.)

## Breadboard Layout

```
        +5V
         |
       [Test Resistor]
         |
        GND
```

Simple series circuit. Measure voltage and current.

## Building Instructions

### Step 1: Build 10Ω Resistor Test Circuit
1. Insert 10Ω resistor from +5V to Row 2
2. Connect Row 2 to GND with jumper wire
3. Power up

### Step 2: Test Circuit Safety
- Feel resistor after 5 seconds
- It should be noticeably warm (but not too hot to touch)
- This is expected: 2.5W power dissipation

### Step 3: Switch to Higher Resistance
1. Remove 10Ω resistor
2. Insert 100Ω resistor
3. Feel temperature difference (much cooler, less power)

### Step 4: Switch to Even Higher Resistance
1. Remove 100Ω resistor
2. Insert 1kΩ resistor
3. Feel minimal heat (10mW, barely warm)

## Measurement Plan

For each resistor tested, measure **voltage, current, and power**:

### 10Ω Resistor Test
1. **Voltage across resistor**:
   - Black probe: GND
   - Red probe: Row 2 (top of resistor)
   - Expected: 5V (full supply)
   - Actual: ______

2. **Current through resistor**:
   - Remove jumper at Row 2
   - Insert ammeter in series
   - Expected: 0.5A
   - Actual: ______
   - **WARNING**: If current > 1A, immediately disconnect (power too high)

3. **Calculate power**:
   - P = V × I = 5V × 0.5A = 2.5W
   - Or: P = V² / R = 25 / 10 = 2.5W
   - Or: P = I² × R = 0.25 × 10 = 2.5W

4. **Temperature measurement** (optional):
   - Thermometer or thermal camera on resistor
   - After 30 seconds: should be ~40-50°C (warm but safe)
   - Don't touch!

### 100Ω Resistor Test
1. Voltage: Expected ~5V
2. Current: I = 5V / 100Ω = 50mA
   - Actual: ______
3. Power: P = 5V × 50mA = 250mW (0.25W)
   - Actual: ______
4. Resistor feels barely warm

### 1kΩ Resistor Test
1. Voltage: Expected ~5V
2. Current: I = 5V / 1kΩ = 5mA
   - Actual: ______
3. Power: P = 5V × 5mA = 25mW (0.025W)
   - Actual: ______
4. Resistor feels cool (minimal heat)

## Comparison Table

| Resistor | Voltage | Current | Power | Temperature |
|----------|---------|---------|-------|-------------|
| 10Ω | 5V | 0.5A | 2.5W | Warm ~40°C |
| 100Ω | 5V | 50mA | 0.25W | Slightly warm |
| 1kΩ | 5V | 5mA | 0.025W | Cool |

**Pattern**: Resistance increases → current decreases → power decreases → temperature decreases

## Visual Verification

- ✓ **10Ω resistor**: Noticeably warm within 10 seconds
- ✓ **100Ω resistor**: Slightly warm after 30 seconds
- ✓ **1kΩ resistor**: Remains cool even after 1 minute

## Key Insight: Resistor Ratings

Every resistor has a **power rating** (0.25W, 0.5W, 1W typical).

**Power rating**: Maximum power the resistor can safely dissipate.

Example:
- 10Ω 0.25W resistor: Can safely dissipate 0.25W maximum
- If you try to dissipate 2.5W: Resistor overheats and fails (burns out)
- **Derating**: Use only 70% of rated power in practice (~0.175W for 0.25W resistor)

### Our 10Ω Experiment: Safe or Not?

2.5W power in typical 0.25W resistor = **10× rated power!**

**How can we do this safely?**
1. Short duration (seconds instead of continuous)
2. Air circulation (breadboard heat dissipates into air)
3. Small resistor size (more surface area than expected)
4. Stop before damage (pull resistor out quickly)

**If we left it on continuous**: Resistor would burn, catch fire, damage breadboard.

**Better approach for high power**: Use power resistor rated ≥ 5W.

## Why Components Get Warm

All power dissipation converts to heat via **Joule heating**:
$$Q = I^2 R$$

In real circuits:
- LEDs: Some power → light, rest → heat
- Transistors: Power dissipation creates thermal management challenges
- Power supplies: Transformers, regulators generate heat
- Motors: Copper resistance generates heat (wasted energy)

**Thermal management**:
- Heatsinks on power transistors
- Fans in computers
- Thermostat control in ovens

## Energy Efficiency

**Efficiency**: Fraction of power that does useful work (not wasted as heat).

Example:
- LED at 2V, 10mA: P = 20mW
  - Converted to light: ~15% = 3mW
  - Converted to heat: ~85% = 17mW
  - Efficiency: 15% (not great, but acceptable for indicator)

- Linear voltage regulator dissipating 2W:
  - All 2W → heat (no useful work except regulation)
  - Efficiency: 0% for power output (but necessary for circuit function)

**Switching regulators** (Project later):
- Much higher efficiency (~90%+)
- Less heat, better for batteries

## Troubleshooting

**Resistor becomes too hot too fast**:
- Unexpected short circuit
- Check connections with multimeter
- Verify resistor value (use color code)

**Resistor doesn't get warm at all**:
- Open circuit (broken resistor, loose connection)
- Verify continuity with multimeter
- Check power supply

**Resistor starts smoking**:
- **Immediately disconnect power**
- Resistor failure (overpower condition)
- Component is now damaged (discard safely)

## Challenge Extensions

1. **Compare LED vs. Resistor heating**:
   - Power dissipation in LED at same current
   - LED produces light + heat
   - Resistor produces only heat
   - Which gets hotter? (Resistor usually, since no light conversion)

2. **Temperature coefficient experiment**:
   - Measure resistance of resistor when hot vs cold
   - Resistance increases with temperature (typically +0.1% per °C)
   - 100Ω resistor: 100.1Ω at +1°C increase

3. **Multiple resistors in series**:
   - Two 500Ω resistors (total 1kΩ)
   - Power splits: 5V each
   - Each dissipates 25mW
   - Compare to single 1kΩ (same total power, same temperature)

4. **Heat transfer timing**:
   - Record temperature vs. time
   - Exponential rise (like RC charging)
   - Time constant depends on thermal capacity and cooling rate

## Real-World Applications

- **Electric heaters**: Intentionally maximize power dissipation
- **Soldering irons**: Controlled heat for melting solder
- **Ovens**: Heating elements for cooking
- **Thermal fuses**: Melt at specific temperature for protection
- **Thermostats**: Control heating with temperature feedback

## Advanced: Thermal Management

**Thermal resistance** (°C/W):
- Describes how much temperature rise per watt of power
- Lower is better (easier to cool)
- Air: ~100°C/W
- With heatsink: ~5-10°C/W

**Junction temperature**: Maximum safe operating temperature of semiconductor.
- Typical: 150°C
- Exceeding this destroys the device

**Thermal design**: Calculate power dissipation → select appropriate heatsinking.

## Key Concepts Reinforced

- **Power formulas**: P = VI = V²/R = I²R
- **Joule heating**: Electrical power converts to heat
- **Resistor ratings**: Every resistor has maximum power limit
- **Temperature rise**: Depends on power dissipation and cooling
- **Thermal efficiency**: Power not doing useful work becomes wasted heat

## Next Steps

1. **Review all 12 basic projects** - You now understand circuits from basics to timing to power
2. **Intermediate Project 1: Transistor Driver** - Handle higher power with active devices
3. **Intermediate Project 2: Heat Dissipation Challenges** - Manage thermal problems

---

**Key Takeaway**: Power dissipation in resistors follows fundamental formulas (P = VI, P = V²/R, P = I²R), and all this power converts directly to heat. Every component has a maximum power rating—exceed it and the component fails. Understanding power dissipation and thermal management is essential for reliable circuit design, from simple breadboard experiments to complex electronic systems.

## Completing Your Basic Projects Journey

Congratulations! You've now completed all 12 basic projects:

1. ✅ LED with resistor - Ohm's law
2. ✅ Series resistors - Voltage drops
3. ✅ Parallel resistors - Current division
4. ✅ Voltage divider - Analog intermediate voltages
5. ✅ Pushbutton control - Digital switching
6. ✅ Potentiometer brightness - Analog control
7. ✅ Capacitor charging - RC time constants
8. ✅ Capacitor filtering - Power supply smoothing
9. ✅ Diode protection - One-way valve properties
10. ✅ Transistor flasher - Electronic timing oscillation
11. ✅ Series-parallel capacitors - Capacitance combinations
12. ✅ Power dissipation - Heat generation and thermal effects

**You now understand**:
- Voltage and current (Ohm's law)
- Series and parallel circuits
- Digital switching with pushbuttons
- Analog control with potentiometers
- Capacitor behavior and RC timing
- Diodes and protection
- Transistor switching
- Power and thermal effects

**Next**: Intermediate projects combine these concepts into more complex, practical circuits. You're ready!
