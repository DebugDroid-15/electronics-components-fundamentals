# Basic Project 7: Capacitor Charging

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 25 minutes  
**Concept**: Capacitor charge/discharge, RC time constant, energy storage

## What You'll Learn

- How capacitors charge and discharge
- RC time constant (τ = R × C)
- Capacitor voltage behavior over time
- Difference between DC and capacitive response

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 1 | Visual indicator |
| 220Ω Resistor | 1 | Charging resistor (R) |
| 470µF Capacitor | 1 | Storage capacitor (C) |
| Pushbutton | 1 | Charge/discharge trigger |
| Jumper wires | 6 | Breadboard connections |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Measure capacitor voltage |

## Theory: Capacitor Charging

A **capacitor** stores electrical charge. When connected to a voltage source through a resistor, it charges gradually (not instantly like resistors).

**Charging equation** (exponential):
$$V_C(t) = V_{supply} \times (1 - e^{-t/\tau})$$

Where:
- $V_C(t)$ = capacitor voltage at time t
- $\tau$ = RC time constant (in seconds)
- $R$ = charging resistance (ohms)
- $C$ = capacitance (farads)

**Time constant** $\tau$:
$$\tau = R \times C$$

Example: 220Ω × 470µF = 0.104 seconds = 104ms

**Key times**:
- At t = τ: Capacitor charged to 63% of supply voltage
- At t = 5τ: Capacitor charged to 99% (essentially full)

**Discharging equation** (exponential decay):
$$V_C(t) = V_{initial} \times e^{-t/\tau}$$

Capacitor discharges through same time constant.

## Breadboard Layout - Charging Circuit

```
       +5V
        |
      [R220]
        |
        +---[LED Anode]---[220Ω LED R]---GND
        |
      [C470µ]
        |
      [Button]
        |
       GND
```

Capacitor charges through 220Ω resistor. LED indicates current flow during charging.

## Building Instructions

### Step 1: Insert Capacitor
1. Identify capacitor polarity (stripe marks negative side)
2. Insert longer lead into Row 2
3. Insert shorter lead (stripe side) into Row 3

### Step 2: Insert Charging Resistor
1. Insert 220Ω resistor from +5V to Row 2 (junction with capacitor positive)
2. This 220Ω resistor controls charging rate

### Step 3: Insert LED and Protection
1. Insert 1kΩ resistor from Row 3 to Row 4 (capacitor side to control current to LED)
2. Insert LED anode into Row 4
3. Insert LED cathode to Row 5

### Step 4: Insert Pushbutton (Discharge Control)
1. Insert pushbutton from Row 3 to Row 6
2. Connect Row 6 to GND with jumper wire
3. This allows you to discharge capacitor (press to discharge)

### Step 5: Connect Ground
1. Connect Row 5 (LED cathode) to GND

## Measurement Plan - Charging Behavior

**Phase 1: Observe charging**

1. **Initially** (capacitor uncharged):
   - Press button to discharge any residual charge
   - Release button
   - Voltage at capacitor (Row 2): should be 0V

2. **Charge the capacitor**:
   - Remove jumper wire from discharge path (or just wait)
   - Capacitor charges through 220Ω resistor from +5V
   - LED glows during charging (current flowing through charging resistor)

3. **Measure voltage over time**:
   - Start timing when you first see LED glow
   - Record voltage at capacitor (Row 2, use multimeter):

   | Time (sec) | Voltage | % of 5V |
   |---|---|---|
   | 0 | 0V | 0% |
   | 0.1 | ____ | ____ |
   | 0.2 | ____ | ____ |
   | 0.3 | ____ | ____ |
   | 0.5 | ____ | ____ |
   | 1.0 | ____ | ____ |

4. **Verify time constant**:
   - At t = 104ms (one time constant): voltage should be ~3.15V (63% of 5V)
   - Actual measurement: ______ V
   - Close? Yes/No

**Phase 2: Observe discharging**

1. **Fully charge capacitor**:
   - Wait until voltage reaches ~5V (capacitor fully charged)

2. **Discharge through button**:
   - Press button to create discharge path
   - Voltage drops (exponential decay)
   - LED may briefly glow (discharge current)

3. **Measure discharge time**:
   - Release button, capacitor discharges through internal resistance
   - Measure how long until voltage drops to 50% (2.5V)
   - Expected: approximately 0.07 seconds (since RC = 104ms, 0.5τ)

## Visual Verification

- ✓ **During charging**: LED glows dimly (current flowing)
- ✓ **Charging slows**: LED gradually dims as current drops
- ✓ **When charged**: LED off (no more charging current)
- ✓ **During discharge**: Capacitor voltage drops (measure with meter)

## Key Insight: Exponential Charging

Unlike resistor circuits (ohm's law, instant response):
- Capacitor voltage doesn't jump to 5V instantly
- Rises gradually following exponential curve
- After 5 time constants (~520ms), essentially full

This **exponential behavior** is foundational for:
- Timing circuits
- Filters
- Power supply stabilization
- Analog processing

## Charging vs. Discharging Current

**Charging current** (through 220Ω resistor):
- Initially: I = (5V - 0V) / 220Ω = 22.7mA (maximum)
- Decreases as capacitor charges
- Follows: $I(t) = \frac{V_{supply}}{R} \times e^{-t/\tau}$

**Discharging current**:
- Similar exponential decay
- Flows until capacitor fully discharged

**LED glow**:
- Proportional to charging current
- Visible only while current significant
- Dims as capacitor charges

## Energy in Capacitor

**Energy stored**:
$$E = \frac{1}{2} C V^2$$

For fully charged 470µF at 5V:
$$E = \frac{1}{2} \times 0.00047F \times 25V^2 = 0.029 \text{ Joules} = 29 \text{ millijoules}$$

Small amount of energy (enough to power LED briefly during discharge).

## Troubleshooting

**Capacitor won't charge**:
- Check polarity (longer lead = positive)
- Verify 220Ω resistor connected properly
- Measure voltage directly: should rise toward 5V

**LED doesn't glow during charging**:
- Current might be too low for visible glow
- Try removing LED protection resistor (1kΩ) to increase current
- Or use smaller capacitor for faster charging (shorter time constant)

**Charging takes too long**:
- This is normal for 470µF with 220Ω (104ms time constant)
- Could use smaller capacitor (100µF) for faster response
- Or smaller resistor (but reduces charging voltage safety)

**Voltage doesn't reach 5V**:
- Could be multimeter loading effect
- Or capacitor has internal resistance
- Check if capacitor is defective

## Challenge Extensions

1. **Different resistor values**:
   - Try 1kΩ instead of 220Ω
   - Time constant increases: τ = 1000Ω × 470µF = 470ms
   - Charging takes longer, LED stays on longer
   - Measure to verify

2. **Different capacitor values**:
   - Try 100µF (faster) or 1000µF (slower)
   - Calculate new time constant
   - Observe charging time change

3. **RC = constant experiment**:
   - Adjust R and C to maintain same τ
   - Example: 100Ω × 1000µF = 100ms (same as original)
   - Does behavior match? (It should)

4. **Voltage divider + capacitor**:
   - Add potentiometer to control charging voltage
   - Capacitor charges to potentiometer voltage instead of 5V
   - Creates adjustable voltage source

## Real-World Applications

- **Power supply filters**: Capacitor + resistor smooth voltage ripple
- **Timing circuits**: RC time constant creates deliberate delays
- **Flash photography**: Capacitor stores energy, releases for flash
- **Smoothing circuits**: Audio filters, noise reduction
- **Coupling**: Block DC, pass AC using capacitor

## Advanced Concept: Differentiators

In Project 7, you observed charging current (proportional to dV/dt).

This is the basis for **differentiation** circuits:
- Output is proportional to rate of voltage change
- Fast changes produce large output
- Slow changes produce small output
- Useful for edge detection, pulse shaping

## Key Concepts Reinforced

- **Capacitor charging**: Exponential rise following RC time constant
- **Time constant**: τ = R × C determines charging rate
- **Exponential function**: Fundamental behavior of reactive circuits
- **Energy storage**: Capacitors store electrical energy
- **Current during charging**: Decreases as capacitor charges

## Next Steps

1. **Project 8: Capacitor Filtering** - Use capacitor to smooth voltage
2. **Project 10: LED Flasher** - Combine capacitor with transistor for timing
3. **Project 12: RC Oscillator** - Use RC to generate oscillating signal

---

**Key Takeaway**: Capacitors charge and discharge exponentially with a time constant τ = RC. This exponential behavior, unlike the instant response of resistors, enables timing, filtering, and energy storage applications fundamental to all electronic circuits.
