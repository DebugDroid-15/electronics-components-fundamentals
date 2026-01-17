# Intermediate Project 1: LED Driver Circuit (BJT vs MOSFET)

**Difficulty**: ⭐⭐ (Intermediate)  
**Time**: 45 minutes  
**Concept**: BJT vs MOSFET comparison, driver circuits, power delivery, base vs. gate drive

## What You'll Learn

- How to drive LEDs efficiently with transistor
- Difference between BJT and MOSFET characteristics
- Current gain and gate threshold concepts
- Why certain transistors suit certain applications
- Power efficiency comparison

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 2 | Load comparison |
| 220Ω Resistor | 2 | LED current limiting |
| 10kΩ Resistor | 2 | Base/gate drive limiting |
| BJT Transistor | 1 | 2N2222 or 2N3904 NPN |
| MOSFET Transistor | 1 | 2N7000 or IRF520 NMOS |
| Pushbutton Switch | 1 | Manual control |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Measure voltage and current |

## Theory: BJT vs MOSFET

### BJT (Bipolar Junction Transistor) Characteristics

**Control mechanism**: Current-driven (base current controls collector current).

**Key equation**:
$$I_C = \beta \times I_B$$

Example: 2N2222
- β (hFE) = 100-200 (typical 150)
- V_BE (base-emitter voltage) = 0.7V (on state)
- V_CE(sat) (saturation voltage) = 0.2V (on state)

**Power dissipation**: P = V_CE × I_C = 0.2V × 10mA = 2mW (when saturated)

**Advantages**:
- Low saturation voltage (0.2V, minimal loss)
- Simple base current requirement (small)
- Good for logic-level switching

**Disadvantages**:
- Needs base current continuously
- Base current drawn from signal source
- Requires current-limiting base resistor

### MOSFET (Metal-Oxide-Semiconductor FET) Characteristics

**Control mechanism**: Voltage-driven (gate voltage controls drain current).

**Key equation**:
$$I_D = k (V_{GS} - V_T)^2$$ (in saturation)

Where:
- k = transconductance parameter
- V_GS = gate-source voltage
- V_T = threshold voltage (~2V for 2N7000)

Example: 2N7000 (enhancement mode N-channel MOSFET)
- V_T (threshold) = ~2V minimum
- R_DS(on) = 5Ω (on-resistance)
- At 5V gate: V_DS(on) = ~0.1V (very low loss)

**Power dissipation**: P = V_DS × I_D = 0.1V × 10mA = 1mW (even lower than BJT!)

**Advantages**:
- Voltage-driven (negligible gate current in steady state)
- Very low gate current (no continuous drain from signal source)
- Lower on-resistance (even lower voltage drop)
- Faster switching (useful for PWM)

**Disadvantages**:
- Higher threshold voltage (need >2V to turn on)
- More complex drive circuit for high-frequency switching
- More sensitive to static electricity

## Breadboard Layout - Dual Test Circuit

```
+5V
 |
[Button]
 |
 +-----[10kΩ R]-----+-----[10kΩ R]-----+
 |                  |                  |
BJT Base           MOSFET Gate        GND
 |
 |
 +---- BJT Circuit         +---- MOSFET Circuit
 |                          |
[BJT Base]              [MOSFET Gate]
[BJT Collector]         [MOSFET Drain]
[BJT Emitter→GND]       [MOSFET Source→GND]
 |                       |
[R220→LED1→GND]     [R220→LED2→GND]
```

Two parallel driver circuits: one with BJT, one with MOSFET.

## Building Instructions

### Part 1: BJT LED Driver

1. **Insert BJT transistor**:
   - Identify 2N2222 or 2N3904
   - Pin 1 (Base) → Row 2
   - Pin 2 (Collector) → Row 3
   - Pin 3 (Emitter) → GND

2. **Connect base drive resistor**:
   - Insert 10kΩ resistor from button output to Row 2 (base)
   - This limits base current to safe level

3. **Connect LED**:
   - Insert 220Ω resistor from +5V to Row 4
   - Insert LED anode into Row 4
   - Insert LED cathode into Row 3 (with transistor collector)
   - Connect Row 3 to GND (completes circuit through transistor)

### Part 2: MOSFET LED Driver

1. **Insert MOSFET transistor**:
   - Identify 2N7000 or similar N-channel MOSFET
   - Pin 1 (Gate) → Row 5
   - Pin 2 (Drain) → Row 6
   - Pin 3 (Source) → GND

2. **Connect gate drive resistor**:
   - Insert 10kΩ resistor from button output to Row 5 (gate)
   - This limits gate current during switching

3. **Connect LED**:
   - Insert 220Ω resistor from +5V to Row 7
   - Insert LED anode into Row 7
   - Insert LED cathode into Row 6 (with transistor drain)
   - Connect Row 6 to GND (completes circuit through transistor)

### Part 3: Control Switch
1. Insert pushbutton switch
2. Connect one terminal to +5V
3. Connect other terminal to both 10kΩ resistors (feeding both base and gate)
4. Test: Press button → both LEDs turn on

## Measurement Plan

### BJT Operating Point

**When button PRESSED** (transistor ON):

1. **Base voltage**:
   - Black probe: GND
   - Red probe: BJT base (Row 2)
   - Expected: ~1.5V (through 10kΩ pull-down to GND)
   - Actual: ______

2. **Collector voltage** (LED side):
   - Expected: ~0.2V (saturation voltage)
   - Actual: ______

3. **Base current**:
   - Remove 10kΩ base resistor temporarily
   - Insert multimeter in current mode
   - Expected: ~0.1mA = 100µA
   - Actual: ______

4. **Collector current**:
   - Remove 220Ω LED resistor temporarily
   - Insert multimeter in current mode
   - Expected: ~10mA
   - Actual: ______

5. **Verify β**:
   - β = I_C / I_B = 10mA / 0.1mA = 100 ✓

### MOSFET Operating Point

**When button PRESSED** (transistor ON):

1. **Gate voltage**:
   - Black probe: GND
   - Red probe: MOSFET gate (Row 5)
   - Expected: ~1.5V (same as BJT, driven by same button)
   - Actual: ______

2. **Drain voltage** (LED side):
   - Expected: ~0.1V (very low, R_DS(on) voltage drop)
   - Actual: ______
   - **Note**: Lower than BJT! More efficient.

3. **Gate current** (in steady state):
   - Expected: Nearly 0A (capacitive only, no continuous current)
   - Actual: ______ (very small)

4. **Drain current**:
   - Expected: ~10mA (same as BJT)
   - Actual: ______

5. **Compare drain voltages**:
   - BJT: ~0.2V drop
   - MOSFET: ~0.1V drop
   - MOSFET is more efficient (half the loss)

## Visual Verification

- ✓ **Both LEDs bright** (when button pressed)
- ✓ **Both LEDs off** (when button released)
- ✓ **BJT LED possibly slightly dimmer** (0.2V loss vs 0.1V)
- ✓ **MOSFET LED possibly slightly brighter** (lower voltage drop)

Brightness difference often imperceptible to human eye, but measurable.

## Key Insights

### BJT Characteristics
- Current-controlled (needs continuous base current)
- Small V_CE(sat) = 0.2V
- Simple to interface with logic
- Power loss: P = 0.2V × I_C

### MOSFET Characteristics
- Voltage-controlled (needs only initial gate charging)
- Larger V_DS(on) at low voltage, but still low
- Negligible gate current in steady state
- Power loss: P = 0.1V × I_D

### Which to Use?
- **BJT**: Low-speed switching, simple circuits, when minimal components desired
- **MOSFET**: High-speed switching, PWM control, when efficiency matters, battery-powered circuits

## Comparison at Different Gate/Base Voltages

Try reducing 10kΩ resistor or button voltage:

| Drive Voltage | BJT Behavior | MOSFET Behavior |
|---|---|---|
| 0V | OFF | OFF |
| 1V | Mostly off | OFF (below threshold) |
| 2V | Weak on | Turning on (at threshold) |
| 5V | Fully saturated | Fully on |

MOSFET doesn't turn on until gate exceeds ~2V threshold.

## Troubleshooting

**BJT LED works, MOSFET LED doesn't**:
- Gate voltage too low (need >2V for 2N7000)
- Measure gate voltage: if <2V, increase button voltage or reduce gate resistor

**MOSFET LED very dim**:
- Slightly above threshold, not fully on
- Gate voltage in 2-3V range (insufficient)
- Increase voltage or reduce gate resistor

**Both LEDs dim or off**:
- Button not making good contact
- Power supply insufficient (measure supply voltage)

**Measuring gate current is impossible**:
- This is normal! MOSFET gate draws almost no DC current
- Any measurement shows negligible current

## Challenge Extensions

1. **PWM control**:
   - Replace button with 1kHz PWM signal
   - MOSFET handles PWM much better (lower frequency loss)
   - BJT also works but less efficient

2. **Load switching**:
   - Replace LED with small motor (5V)
   - MOSFET better suited (can handle inductive kick-back with protection diode)
   - Demonstrate with both, observe performance

3. **High current test**:
   - Add parallel LEDs to increase load (50mA total)
   - Observe which transistor handles better
   - MOSFET stays cooler (lower voltage drop)

4. **Efficiency measurement**:
   - Calculate power dissipated: P = V × I
   - BJT: P = 0.2V × 50mA = 10mW
   - MOSFET: P = 0.1V × 50mA = 5mW
   - MOSFET 2× more efficient

## Real-World Applications

- **BJT LED drivers**: Simple indicators, logic circuits
- **MOSFET LED drivers**: RGB LED PWM control, power switching
- **BJT power stages**: Audio amplifiers, linear regulators
- **MOSFET power stages**: Switch-mode supplies, motor control, high-power switching

## Advanced: Gate Drive Considerations

For high-speed switching (covered in advanced projects):

**BJT**:
- Base drive current must be actively removed
- Miller effect causes switching delays
- Collector current doesn't follow gate voltage instantly

**MOSFET**:
- Gate charge must be supplied/removed
- Gate capacitance ~1000pF typical
- At 1MHz, gate draws significant current (not DC-only)
- Requires dedicated gate driver IC for high frequencies

## Key Concepts Reinforced

- **Current-driven vs voltage-driven**: BJT needs base current, MOSFET needs gate voltage
- **Saturation vs on-state**: BJT V_CE(sat) vs MOSFET R_DS(on)
- **Power efficiency**: Lower voltage drop = less heat = better efficiency
- **Component selection**: Choose based on application requirements

## Next Steps

1. **Project 2: Simple Rectifier** - Use diodes (not transistors)
2. **Project 3: Voltage Regulator** - Use transistor + Zener feedback
3. **Project 6: PWM Control** - MOSFET excels at variable duty cycles

---

**Key Takeaway**: BJTs are current-controlled switches (need base current), while MOSFETs are voltage-controlled switches (need gate voltage). MOSFETs are more efficient for power switching due to lower on-resistance, while BJTs are simpler for logic-level circuits. Understanding both is essential for choosing the right transistor for your application.
