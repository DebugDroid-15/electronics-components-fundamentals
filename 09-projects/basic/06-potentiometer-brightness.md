# Basic Project 6: LED Brightness Control with Potentiometer

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 20 minutes  
**Concept**: Variable voltage divider, analog control, LED brightness dimming

## What You'll Learn

- Potentiometer as variable voltage divider
- How to control LED brightness with voltage
- Analog input devices (how sensors work)
- Relationship between voltage and brightness

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 1 | Adjustable brightness |
| 220Ω Resistor | 1 | Current limiting |
| Potentiometer | 1 | 10kΩ recommended (B type/linear) |
| Multimeter | 1 | Measure potentiometer voltage |
| Jumper wires | 6 | Breadboard connections |
| Breadboard | 1 | Same as previous |

## Theory: Potentiometer as Voltage Divider

A **potentiometer** is a three-terminal variable resistor that acts as an adjustable voltage divider.

**Pinout** (typical 10kΩ potentiometer):
- Pin 1: +5V input
- Pin 2: Wiper (sliding tap, variable voltage output)
- Pin 3: Ground

**As slider moves**:
- Resistance from Pin 1→2 changes: 0Ω to 10kΩ
- Resistance from Pin 2→3 changes: 10kΩ to 0Ω
- But sum always = 10kΩ

**Voltage divider formula** (from Project 4):
$$V_{wiper} = V_{in} \times \frac{R_2}{R_1 + R_2}$$

Where R1 = resistance to +5V, R2 = resistance to GND.

**As you turn knob**:
- Fully CCW (left): R1=0Ω, R2=10kΩ → V_wiper = 5V × 10k/10k = 5.0V
- Middle: R1=5kΩ, R2=5kΩ → V_wiper = 5V × 5k/10k = 2.5V
- Fully CW (right): R1=10kΩ, R2=0Ω → V_wiper = 5V × 0k/10k = 0V

**LED brightness control**:
- At 5V: LED very bright (maximum allowed current)
- At 2.5V: LED medium brightness
- At 0V: LED off (no voltage)

## Breadboard Layout

```
        +5V
         |
    [Pot Pin 1]
         |
    [Pot Pin 2] ---- to LED (via 220Ω R)
         |
         |
    [Pot Pin 3]
         |
        GND
```

Current path: +5V → Pot → 220Ω R → LED → GND

## Building Instructions

### Step 1: Insert Potentiometer
1. Identify three pins (often labeled 1, 2, 3 or A, W, B)
   - Outer pins go to +5V and GND
   - Middle pin is wiper (variable tap)
2. Insert left pin into +5V rail
3. Insert middle pin into Row 2 (this is variable voltage)
4. Insert right pin into GND rail

### Step 2: Insert Current-Limiting Resistor
1. Insert 220Ω resistor from Row 2 (potentiometer wiper) to Row 3

### Step 3: Insert LED
1. Insert LED anode (long leg) into Row 3
2. Insert LED cathode (short leg) into Row 4

### Step 4: Complete Circuit
1. Connect Row 4 (LED cathode) to GND with jumper wire
2. Power up

### Step 5: Adjust and Test
1. Slowly turn potentiometer knob
2. LED brightness changes smoothly from dim to bright
3. Find "sweet spot" for comfortable brightness

## Measurement Plan

**Essential measurement**: Voltage at potentiometer wiper as you turn it.

1. **Wiper voltage across range**:
   - Black probe: GND
   - Red probe: Potentiometer middle pin (wiper)
   
   | Knob Position | Expected V | Actual V |
   |---|---|---|
   | Fully CCW (left) | 5V | _____ |
   | Quarter turn | 3.75V | _____ |
   | Middle | 2.5V | _____ |
   | Three-quarter | 1.25V | _____ |
   | Fully CW (right) | 0V | _____ |

2. **Correlate voltage with LED brightness**:
   - At each voltage, note LED brightness (dim/medium/bright)
   - Is relationship linear? (brightness proportional to voltage)
   - Actually: brightness is approximately linear with voltage

3. **Voltage across LED**:
   - At maximum (wiper = 5V): Voltage across LED = ~2V (rest across 220Ω)
   - At minimum (wiper = 0V): Voltage across LED = ~0V (LED off)

## Visual Verification

- ✓ Turning potentiometer knob changes LED brightness
- ✓ Full range: off (fully CW) to full bright (fully CCW)
- ✓ Smooth adjustment (no sudden jumps)
- ✓ Brightness proportional to knob position

## Key Insight: Analog Control

Unlike Project 5 (digital: button on/off):
- Potentiometer provides continuous range (0V to 5V)
- LED brightness varies smoothly
- No discrete steps (analog, not digital)

This is **analog input**—same principle used for:
- Volume knobs
- Brightness controls
- Temperature sensors
- Microphone input

## Potentiometer Specifications

**Common values**:
- 10kΩ: Most common, good for analog control
- 100kΩ: Higher impedance, less loading
- 1kΩ: Lower impedance, draws more current

**Taper types**:
- Linear (B): Voltage changes evenly with rotation (what you want)
- Logarithmic (A): Voltage changes curve with rotation (for audio)

**Lifespan**:
- Mechanical wear (100k-1M cycles typical)
- Scratchy potentiometers indicate wear
- Still functional, just noisier

## Troubleshooting

**LED doesn't respond to potentiometer**:
- Check that middle pin is properly inserted
- Measure voltage at wiper: should vary 0-5V as you turn
- If voltage doesn't change, potentiometer not making contact

**LED stuck at one brightness**:
- Potentiometer pin loose
- Reinsert more firmly into breadboard

**Voltage doesn't go to 0V or 5V**:
- This is normal for some potentiometers (not perfectly linear at extremes)
- Range might be 0.3V to 4.8V (good enough)

**Scratchy/noisy adjustment**:
- Normal sign of mechanical wear
- Still usable for learning

## Challenge Extensions

1. **Dual potentiometers**:
   - Use two pots on two different LEDs
   - Independent brightness control on each
   - Tests your breadboarding skills

2. **Inverted control**:
   - Swap +5V and GND connections on pot
   - Now fully CW = bright, fully CCW = dim (reversed)
   - Demonstrates how polarity matters

3. **Logarithmic vs. Linear**:
   - If you have a logarithmic pot, compare brightness curve
   - Linear pot: brightness proportional to rotation
   - Log pot: brightness curve follows perception

4. **Potentiometer as sensor**:
   - Potentiometer is essentially variable resistor
   - In real sensors (light, temperature), resistance varies with measured quantity
   - This project demonstrates sensor interfacing principle

## Real-World Applications

- **Volume knobs**: Potentiometer controls amplifier gain
- **Brightness controls**: Monitor/TV brightness adjustment
- **Joysticks**: Two potentiometers (X and Y axes)
- **Throttle controls**: Robot speed, motor control
- **Sensor interfaces**: Temperature sensor output voltage varies like pot

## Mathematical Relationship

**LED brightness** not perfectly linear with voltage:

Brightness ≈ (V_LED / V_max)^1.5 (approximately)

Why nonlinear?
- LED has exponential V-I curve
- Human eye perception is nonlinear

But for practical purposes: "More voltage = Brighter" is good enough.

## Key Concepts Reinforced

- **Potentiometer**: Variable voltage divider with three terminals
- **Analog control**: Continuous voltage variation for proportional effect
- **Voltage-to-brightness**: Direct relationship for LED control
- **Range**: Maximum voltage determines maximum brightness
- **Smooth adjustment**: No discrete steps, continuous spectrum

## Next Steps

1. **Project 7: Capacitor Charging** - Add time constant element
2. **Project 8: RC Oscillator** - Combine pot with capacitor for timing
3. **Project 10: LED Flasher** - Use timing for automatic brightness pulsing

---

**Key Takeaway**: Potentiometers enable analog control by acting as variable voltage dividers. By varying the output voltage, you can proportionally control LED brightness from completely off to maximum brightness. This principle—analog input controlling an output—is fundamental to all sensor-based and user-interactive circuits.
