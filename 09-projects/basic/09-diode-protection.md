# Basic Project 9: Diode Protection Circuit

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 20 minutes  
**Concept**: Diode as one-way valve, reverse polarity protection, rectification

## What You'll Learn

- Diodes conduct in forward direction (forward bias)
- Diodes block in reverse direction (reverse bias)
- How to protect circuits from reversed power
- Introduction to rectification (AC to DC conversion)

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 2 | Test and protection |
| 220Ω Resistor | 2 | Current limiting |
| Diode | 2 | 1N4007 or 1N4148 |
| Pushbutton | 1 | Reverse polarity test |
| Jumper wires | 8 | Breadboard connections |
| Breadboard | 1 | Same as previous |

## Theory: Diode as One-Way Valve

A **diode** conducts current easily in forward direction, blocks in reverse direction.

**Forward bias**: When anode is positive relative to cathode.
- Diode acts like short circuit (low resistance, ~0.7V drop for silicon)
- Current flows easily

**Reverse bias**: When cathode is positive relative to anode.
- Diode acts like open circuit (very high resistance)
- Current blocked (except tiny leakage current)

**Diode characteristics**:
$$I_D = I_S (e^{qV_D/kT} - 1)$$

Simplified:
- Forward: Current increases exponentially with voltage
- Reverse: Current essentially zero until breakdown voltage

**Diode markings**:
- Black band = cathode (negative, blocking end)
- No band side = anode (positive, conducting end)

## Breadboard Layout - Protection Circuit

```
Circuit WITHOUT protection (vulnerable):
+5V → [Diode] → [R220] → [LED] → GND
                    (optional forward path)

Circuit WITH protection (reverse voltage safe):
+5V → [Diode↓] → [R220] → [LED] → GND
      (must be forward bias)

Reverse polarity attempt:
GND → [Diode↑] → [R220] → [LED] → +5V
      (blocked by diode!)
```

Diode in series blocks reverse polarity.

## Building Instructions

### Part 1: Test Diode Forward Direction

1. Identify diode (black band = cathode end)
2. Insert cathode (black band) into Row 2
3. Insert anode (unmarked end) into +5V rail

### Part 2: Forward Conduction Path
1. Insert 220Ω resistor from Row 2 to Row 3
2. Insert LED anode into Row 3
3. Insert LED cathode into Row 4
4. Connect Row 4 to GND

### Step 3: Test Forward Bias
1. Power up
2. LED lights brightly (diode conducts, ~0.7V drop)

### Step 4: Test Reverse Bias (Optional, with separate test)
1. Remove diode
2. Flip orientation (anode now at +5V, cathode at Row 2)
3. Power up
4. LED doesn't light (diode blocks reverse voltage)

## Measurement Plan - Forward Conduction

1. **Voltage across diode**:
   - Black probe: Row 2 (cathode)
   - Red probe: +5V
   - Expected: ~0.7V (silicon diode forward voltage)
   - Actual: ______

2. **LED brightness with diode**:
   - Note: Slightly dimmer than without diode (voltage drop)
   - But LED still gets ~4.3V (5V - 0.7V drop)

3. **Current through circuit**:
   - Current = (5V - 0.7V - 2V) / 220Ω = 10.5mA
   - Expected: ~10.5mA

## Measurement Plan - Reverse Protection

**Simulate reverse polarity** (careful, switches should be off):

1. **Build alternate test circuit**:
   - Switch power OFF
   - Flip entire power supply connections (reversed)
   - Insert diode backward
   - Power ON
   - LED should NOT light (diode blocks reverse voltage)

2. **Voltage measurement (reversed)**:
   - Diode cathode now at positive
   - Diode blocks reverse voltage
   - Voltage at anode (should be near GND): ~0V
   - Diode supports full 5V across it (reverse bias)

## Visual Verification

**Forward bias**:
- ✓ LED glows normally
- ✓ Diode warm to touch (small power dissipation: P = 0.7V × 10mA = 7mW)
- ✓ No discoloration

**Reverse bias** (if tested):
- ✓ LED off (no current flow)
- ✓ Diode cool (no power dissipation)
- ✓ Full voltage across diode

## Key Insight: Reverse Polarity Protection

In real devices, reverse polarity is dangerous:
- Can damage components
- Can cause fires in battery-powered circuits
- Can destroy expensive microcontrollers

**Solution**: Add **protection diode** in series with power input.

**Cost**: ~$0.01 per diode
**Benefit**: Protection against $100+ damage

This is why every USB charger has internal diode protection.

## Diode Voltage Drop Impact

**Without diode**: V_LED = 5V - 2V = 3V, Current = 13.6mA

**With diode**: V_LED = 5V - 0.7V - 2V = 2.3V, Current = 10.5mA

LED slightly dimmer (20% reduction in current).

For many applications, this small voltage drop is acceptable for protection.

## Special Diodes

Different diodes for different purposes:

| Diode Type | Forward V | Current Rating | Speed | Use |
|-----------|----------|-----------------|-------|-----|
| 1N4007 | 0.7V | 1A max | Slow | Power supplies |
| 1N4148 | 0.7V | 200mA | Fast | Logic circuits |
| Schottky | 0.3V | Variable | Very fast | Low loss |

**Schottky diode**: Lower voltage drop (0.3V vs 0.7V), faster switching.

Cost: Higher than standard silicon diode.

## Reverse Recovery Time

When diode switches from conducting to blocking:
- Takes time to "turn off" (minority carrier removal)
- **Reverse recovery time**: ~10ns to 1µs
- Matters for high-speed circuits
- Negligible for DC circuits (this project)

## Troubleshooting

**LED doesn't light with diode**:
- Diode inserted backward (cathode must connect to ground side)
- Check orientation: black band should point toward ground
- Test: LED works without diode?

**LED works same with or without diode**:
- Diode might be shorted (defective)
- Measure voltage across diode: should be 0.7V in forward bias
- If near 0V, diode likely shorted

**LED dimmer with diode**:
- This is expected (0.7V drop)
- If too dim, use lower value resistor (150Ω instead of 220Ω)

## Challenge Extensions

1. **Compare diode types**:
   - Test 1N4007 vs 1N4148 (if available)
   - Measure voltage drop: both should be ~0.7V
   - Current rating differs but not visible in this project

2. **Schottky comparison**:
   - If available: measure Schottky voltage drop
   - Expected: ~0.3V (half of silicon)
   - LED much brighter with Schottky (less voltage lost)

3. **Dual diodes (OR logic)**:
   - Two diodes from two separate power sources
   - Either source can power LED (whichever higher voltage)
   - Demonstrates diode OR gate (power selection)

4. **Parallel diodes for current**:
   - Two diodes in parallel from same source
   - Each handles half the current
   - Increases total current capacity
   - (Rarely done in practice due to current sharing complexity)

## Real-World Applications

- **USB power supplies**: Protect against backwards connection
- **Battery-powered devices**: Protect against reversed battery
- **Solar panels**: Prevent discharge through panel at night
- **Motor circuits**: Protect from back-EMF spikes
- **AC rectification**: Convert AC to DC (multiple diodes)

## Bridge Rectifier Preview

Four diodes in "bridge" configuration:
- Converts AC to pulsating DC
- Used in all AC-powered power supplies
- You'll build this in intermediate projects

## Advanced: Zener Diode

**Zener diode**: Special diode designed to conduct in reverse direction at specific voltage.

Uses:
- Voltage regulation
- Overvoltage protection
- Reference voltage source

Preview: Will cover in intermediate projects.

## Key Concepts Reinforced

- **Diode as one-way valve**: Forward conducts, reverse blocks
- **Forward voltage drop**: ~0.7V for silicon diodes
- **Reverse bias**: Acts as open circuit
- **Protection application**: Guards against reversed polarity
- **Trade-off**: Small voltage loss in exchange for circuit protection

## Next Steps

1. **Project 10: LED Flasher** - Use diode with capacitor for timing
2. **Project 11: Power Dissipation** - Understand heat from diode
3. **Intermediate Project 1: Rectifier** - Use diodes to convert AC to DC

---

**Key Takeaway**: Diodes conduct easily in one direction (forward bias) but block in the reverse direction (reverse bias). This makes them ideal for protecting circuits against reversed power connections and for converting AC to DC. Every electronic device contains protective diodes—a small, inexpensive component that prevents catastrophic failure.
