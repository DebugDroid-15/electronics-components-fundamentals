# Basic Project 1: LED with Current-Limiting Resistor

**Difficulty**: ⭐ (Absolute beginner)  
**Time**: 15 minutes  
**Concept**: Ohm's law, LED forward voltage, current limiting

## What You'll Learn

- Why LEDs need current-limiting resistors
- How to calculate resistor value using Ohm's law
- Difference between LED on/off states
- Safe component handling

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery pack |
| Red LED (5mm) | 1 | Standard brightness |
| 220Ω Resistor | 1 | 1/4W carbon film |
| Jumper wires | 4 | Solid core 22 AWG |
| Breadboard | 1 | Solderless, any size |

## Theory: Why the Resistor?

**LED Characteristics**:
- Forward voltage (Vf): ~2V (red LED typical)
- Maximum current: ~20mA (typical safe value)
- If you supply 5V directly: I = 5V / 10Ω ≈ 500mA (destroys LED instantly)

**Current limiting via Ohm's law**:
$$V = I \times R$$

Rearranging for resistor:
$$R = \frac{V - V_f}{I} = \frac{5V - 2V}{20mA} = 150Ω$$

Standard 220Ω resistor is close (slightly lower current ~13mA, safer).

## Breadboard Layout

```
Power Rail (+5V)
    |
  [220Ω Resistor]
    |
  [LED Anode (longer lead)]
    |
  [LED Cathode (shorter lead)]
    |
Ground Rail (GND)
```

**Detailed pin-by-pin layout**:
```
BREADBOARD (top view):
     +5V   GND
     |     |
Row1 +--R--+ [220Ω resistor here]
     |     |
Row2 +--L--+ [LED anode here]
     |     |
Row3 +--L--+ [LED cathode here]
     |     |
     +--+--+ [Connect to GND]
```

## Building Instructions

### Step 1: Insert Resistor
1. Take 220Ω resistor (check color code: red-red-brown = 220)
2. Insert one lead into power row (positive +5V)
3. Insert other lead into an unused row (let's say Row 2)
4. Resistor bridges the gap

### Step 2: Insert LED
1. Look at LED (longer lead = anode/positive, shorter = cathode/negative)
2. Insert longer lead into Row 2 (where resistor connects)
3. Insert shorter lead into a different column
4. LED is now in series with resistor

### Step 3: Ground Connection
1. Use jumper wire from LED cathode row to ground rail
2. Use another jumper wire from ground rail to power supply negative

### Step 4: Power Supply
1. Connect 5V to the positive power rail
2. Connect GND to the negative power rail
3. LED should light up immediately (red glow)

## Verification Checklist

**Visual**:
- ✓ LED is glowing red (not too dim, not too bright)
- ✓ No smoke or burning smell
- ✓ Resistor is cool to touch (warm is okay, hot is bad)

**Measurement**:
- ✓ Voltage across LED: ~2V (using multimeter)
- ✓ Voltage across resistor: ~3V (5V - 2V)
- ✓ Current through circuit: ~13mA (use multimeter in series if possible)

## What's Happening

1. 5V power supply provides energy
2. Current flows through resistor (limited to ~13mA)
3. Resistor drops ~3V (uses voltage)
4. LED receives ~2V (its forward voltage requirement)
5. LED emits photons (light)

**If LED doesn't light**:
- Check polarity (longer lead must be to positive side)
- Check connections (use multimeter to verify continuity)
- Verify resistor isn't broken (measure with multimeter)

**If LED very dim**:
- Resistor value too high (use smaller value, try 150Ω)
- Check power supply voltage (should be 5V)

**If LED very bright then dims/goes out**:
- Resistor is wrong (got 10kΩ instead of 220Ω?)
- LED may be failing (turn off immediately, replace)

## What You've Learned

✓ LEDs are polarized (direction matters)  
✓ Current-limiting resistor is essential  
✓ Ohm's law predicts behavior accurately  
✓ Voltage drops across components in series  
✓ You can measure real circuits  

## Challenge Extensions

1. **Try different resistor values**: 150Ω (brighter), 470Ω (dimmer), 1kΩ (very dim)
   - Predict brightness first, measure current second

2. **Add second LED in series**:
   - Two LEDs drop 4V total (need ~1.5kΩ resistor)
   - Calculate resistor needed before trying

3. **Try different colors**:
   - Green/yellow LEDs have slightly different forward voltages (~2.2V)
   - Does brightness match red LED? Why?

4. **Measure actual current**:
   - Use multimeter in ammeter mode (in series with circuit)
   - Compare to calculated value

## Key Concepts Reinforced

- **Ohm's Law**: V = I × R (fundamental electronics equation)
- **Voltage Drops**: Sum of voltage drops = supply voltage (Kirchhoff's voltage law)
- **Current Limiting**: Resistor reduces current to safe level
- **Component Polarity**: Some components have direction (diodes, capacitors, LEDs)
- **Power Dissipation**: P = I²R (resistor gets warm because of power loss)

## Next Steps

Move to **Project 2: Series Resistors** to understand how resistances combine.

Then **Project 3: Parallel Resistors** to learn current division.

Finally **Project 4: Voltage Divider** to create adjustable reference voltages.

---

**Did you get it?** Great! You now understand the most fundamental circuit—the current-limiting resistor. This pattern appears in almost every circuit, protecting components and controlling current flow. Master this, and many circuits become clear.
