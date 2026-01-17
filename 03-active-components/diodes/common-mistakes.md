# Common Diode Mistakes

## Mistake 1: Forgetting Current-Limiting Resistor for LEDs

### The Error
Connecting LED directly to power supply without resistor.

**Result**: Excessive current through LED → LED burns out in seconds or explodes.

### Why
- LED conducts current limited only by its internal resistance (~10–20Ω)
- Current can reach 100mA+ (LED dies at ~20mA typical)
- Thermal damage or electro-migration failure

### The Fix
**Always use current-limiting resistor in series with LED**:

1. Calculate voltage drop across resistor: V_R = V_supply - V_LED
2. Calculate resistor: R = V_R / I_desired
3. Choose standard value equal or higher

**Example** (5V, 2V LED, 10mA desired):
- V_R = 5V – 2V = 3V
- R = 3V / 10mA = 300Ω
- Use 330Ω standard resistor

## Mistake 2: Wrong Polarity on Diodes

### The Error
Connecting diode backward (cathode to positive instead of anode).

**Result**: Diode doesn't conduct, or if current-limited, just leaks.

### Why
- Diodes only conduct one way
- Wrong polarity = reverse bias = blocking

### The Fix
1. **Remember**: Arrow on symbol points toward negative (cathode)
2. **For LEDs**: Long lead is positive (anode)
3. **Double-check before soldering**

## Mistake 3: Exceeding Reverse Voltage Rating

### The Error
Applying reverse voltage beyond what diode is rated for.

**Result**: Diode enters avalanche/Zener breakdown, conducts heavily, gets hot, fails.

### Why
- Every diode has maximum reverse voltage rating
- Exceeding it causes breakdown
- Breakdown current limited only by circuit resistance

### The Fix
1. **Find reverse voltage rating** on datasheet
2. **Verify circuit voltage** never exceeds this (even with spikes)
3. **Add margin**: Use diode rated for 1.5–2× the maximum voltage

## Mistake 4: Ignoring Temperature Effects on Forward Voltage

### The Error
Designing LED circuit at room temperature, not accounting for temperature change.

**Example**:
- Designed at 25°C: Forward voltage 2.0V
- At 85°C: Forward voltage 1.9V
- LED current increases 5%+
- LED brightness changes, circuit operates out of spec

### Why
- Forward voltage decreases ~2mV/°C
- In temperature-varying environments, this is significant

### The Fix
1. **Calculate at temperature extremes** (-10°C and +85°C)
2. **Verify LED current stays within spec** at both extremes
3. **Use active current control** if temperature variation is large

## Mistake 5: Diode Reverse Polarity Protection Without Resistor

### The Error
Using Schottky diode for reverse polarity protection but not accounting for forward voltage drop.

**Example**:
- Circuit needs 5V
- Schottky diode (0.3V drop) in power line
- Actual voltage: 4.7V
- Circuits operating at 5V don't work at 4.7V

### Why
- Any protection diode causes forward voltage drop
- 0.3V (Schottky) or 0.7V (silicon) might be too much

### The Fix
1. **Check that circuit tolerates voltage drop**
2. **Use lowest voltage drop diode possible** (Schottky)
3. **Or don't use series diode**, use parallel Schottky instead (conducts if reversed)

## Mistake 6: No Protection Diode on Inductive Load

### The Error
Switching off current through inductor (relay, motor) without flyback diode.

**Result**: Inductor generates huge reverse voltage spike, destroys transistor switching it off.

### Why
- When current through inductor switches off, energy must go somewhere
- Without diode, voltage spike appears across switching transistor
- Spike (hundreds of volts) instantly destroys transistor

### The Fix
**Always add flyback diode** across inductive load:
1. Cathode to positive (anode to negative) of coil
2. Diode provides path for energy dissipation
3. Prevents voltage spike

## Mistake 7: Zener Diode Without Series Resistor

### The Error
Using Zener diode for voltage regulation without current-limiting resistor.

**Result**: Zener draws excessive current, overheats, fails.

### Why
- Zener diode in series with power supply acts like short circuit at Zener voltage
- Without resistor, current limited only by supply
- Zener dissipates excessive power

### The Fix
**Always use series resistor** with Zener:
1. Calculate voltage drop across resistor: V_R = V_supply - V_zener
2. Calculate resistor: R = V_R / I_desired
3. Choose resistor to limit current to safe level

## Mistake 8: Fast Switching Diode for High-Frequency RF

### The Error
Using slow (1N4007) rectifier diode in high-frequency circuit where speed matters.

**Result**: 
- Diode doesn't switch fast enough
- Reverse recovery time causes conduction when supposed to be off
- Circuit doesn't work at design frequency

### Why
- Slow diodes have recovery times of 100+ nanoseconds
- At MHz frequencies, this is significant
- Leads to cross-conduction, efficiency loss, heat

### The Fix
1. **Identify circuit frequency**
2. **Choose appropriate diode speed**:
   - General purpose: 1N4007 (OK for DC/low freq)
   - 1 MHz+: Use 1N4148 (fast, 4ns recovery)
   - RF: Use Schottky (< 1ns recovery)

## Mistake 9: Ignoring Leakage Current at High Temperature

### The Error
Designing circuit assuming ideal diode reverse insulation, forgetting leakage at 85°C.

**Example**:
- Sample-and-hold circuit using diode as switch
- At 25°C: Leakage 1nA (perfect)
- At 85°C: Leakage 100nA (100× worse!)
- Hold capacitor leaks away in seconds instead of minutes

### Why
- Reverse leakage doubles every 25–30°C
- Becomes significant at high temperature

### The Fix
1. **Calculate leakage** at worst-case temperature
2. **Measure actual behavior** on prototype at temperature extremes
3. **Use precision diodes** if leakage must be minimized

## Mistake 10: Bridge Rectifier Connection Errors

### The Error
Misconnecting bridge rectifier (4 diodes), getting half-wave rectification instead of full-wave.

**Result**: Circuit gets DC but ripple frequency is half of intended (more noise).

### Why
- Bridge requires specific connection
- Wrong connection wastes half the AC wave

### The Fix
1. **Follow datasheet** carefully
2. **Mark AC, +, -, connections** clearly
3. **Verify with multimeter** before connecting load

## Mistake 11: Photodiode Without Bias and Amplifier

### The Error
Connecting photodiode directly to circuit, expecting it to work.

**Result**: No signal (output impedance too high to measure).

### Why
- Photodiodes are current sources (~100pA per lux typical)
- Current must be converted to voltage (with trans-impedance amplifier)
- Without amplifier, output impedance is too high

### The Fix
**Use transimpedance amplifier circuit** (op-amp with feedback resistor).

## Practical Diode Selection Checklist

- [ ] **Type**: Correct for application (rectifier, Zener, LED, etc.)
- [ ] **Forward voltage**: Acceptable for circuit
- [ ] **Reverse voltage rating**: Exceeds maximum expected voltage by 1.5–2×
- [ ] **Current rating**: Handles peak current with margin
- [ ] **Speed**: Fast enough for circuit frequency
- [ ] **Temperature range**: Covers operating environment
- [ ] **Polarity**: Correctly oriented (anode, cathode identified)
- [ ] **Auxiliary**: Flyback diode if needed? Current limiting resistor?

## Key Takeaway

**Most diode failures are due to:**
1. **No current limiting** (LEDs, Zener without resistor)
2. **Wrong polarity** (backward connection)
3. **Exceeding voltage rating** (lack of margin)
4. **Wrong type for frequency** (slow diode in fast circuit)
5. **Forgetting flyback diode** (inductor switching)

These are all preventable with basic care during design and assembly.

---

You've completed diodes. Next: BJTs (junction transistors).
