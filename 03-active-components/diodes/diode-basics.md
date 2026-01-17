# Diodes: Section Overview & Basics

## What This Section Covers

Diodes are the first **active components**—they don't just resist or store energy, they **control** current flow based on applied voltage. Think of a diode as an electronic one-way valve.

In this section:
- What a diode is and how it works
- Types of diodes (rectifier, Zener, LED, photodiode, etc.)
- Real characteristics vs. ideal models
- Common mistakes

## Section Structure

1. **diode-basics.md** (this file) — What diodes do
2. **diode-types.md** — Different diodes and their purposes
3. **real-characteristics.md** — Non-ideal behavior
4. **common-mistakes.md** — Where people struggle

## Diode Fundamentals

### What Is a Diode?

A diode is a two-terminal semiconductor device that:
- **Conducts easily** in one direction (forward direction)
- **Blocks** current in the opposite direction (reverse direction)

This is the one-way valve concept. Current flows one way, gets blocked the other way.

### How It Works (Intuitive Model)

Think of a diode as a gate:
- Apply positive to anode, negative to cathode: Gate opens, current flows (forward biased)
- Apply negative to anode, positive to cathode: Gate closes, current blocked (reverse biased)

The circuit symbol shows this: the arrow points in the direction current flows (forward direction).

### Forward Bias vs. Reverse Bias

**Forward Bias** (anode positive, cathode negative):
- Diode conducts
- Current flows from anode to cathode
- Voltage drop across diode: 0.3–0.7V typical (depends on type and current)

**Reverse Bias** (anode negative, cathode positive):
- Diode blocks current
- Very little current flows (ideally zero)
- Diode withstands voltage (up to reverse breakdown voltage)

### IV Characteristic

A diode's behavior is shown by its **I-V curve** (current vs. voltage):

**Forward direction**:
- Below ~0.3V: Minimal current (off state)
- 0.3–0.7V: Current increases sharply (exponentially)
- Above 0.7V: Full conduction (acts like small resistor)

**Reverse direction**:
- Tiny leakage current until reverse breakdown
- At breakdown: Sudden current surge (unless limited by resistor)

### Ideal vs. Real Model

**Ideal diode**:
- Conducts perfectly in forward direction (zero resistance, zero voltage drop)
- Blocks perfectly in reverse direction (infinite resistance, no current)

**Real diode**:
- Forward direction: ~0.6–0.7V voltage drop (silicon), ~0.3V (germanium)
- Reverse direction: Small leakage current (microamps to nanoamps)
- Reverse breakdown voltage: Finite limit

## Common Diode Types

### Rectifier Diodes
- Purpose: Convert AC to DC (rectification)
- Example: 1N4007
- Current handling: Moderate (amps)
- Voltage rating: 50V to 1000V+
- Forward voltage: ~0.7V

### Zener Diodes
- Purpose: Voltage regulation and protection
- Conducts in reverse direction at specific voltage (Zener voltage)
- Used for overvoltage protection, reference voltages
- Voltage ratings: 3.3V to 100V+ common

### LED (Light Emitting Diode)
- Purpose: Emit light
- Colors: Red, green, blue, white, infrared, etc.
- Forward voltage: 1.5–3.5V (depends on color)
- Current: Limited to ~20mA typical

### Photodiode
- Purpose: Detect light
- Reverse biased, generates current when light hits
- Used in light sensors, optical receivers

## Key Concepts

✓ **One-way valve**: Conducts forward, blocks reverse  
✓ **Voltage drop**: ~0.7V in forward direction (unavoidable in real diodes)  
✓ **Current limiting**: Resistor required to limit current (current will surge without it)  
✓ **Reverse breakdown**: There's a limit to how much reverse voltage a diode handles  
✓ **Temperature dependence**: Forward voltage changes with temperature  

## Next Steps

Learn about specific diode types and their applications.
