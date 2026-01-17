# Diode Types: Classifications and Applications

## Overview

Diodes come in many varieties, each optimized for different purposes. This section covers the most common types and when to use each.

## Rectifier Diodes (General Purpose)

### Examples
1N4148 (fast), 1N4007 (standard), 1N5407 (high current)

### Purpose
Convert AC to DC, general current path protection

### Characteristics
- Forward voltage: 0.6–0.7V
- Reverse voltage rating: 50–1000V
- Current rating: 100mA to 3A+
- Speed: Medium (recovery time ~100ns)

### When to Use
- Power supply rectification
- Reverse polarity protection
- General-purpose diodes

## Zener Diodes

### Purpose
Voltage regulation and overvoltage protection

### How It Works
Conducts in **reverse direction** at a specific voltage (Zener voltage). Used as voltage regulator or protection device.

### Characteristics
- Zener voltage: 3.3V to 200V common
- Power rating: 0.25W to 50W+
- Temperature coefficient: 0.1%/°C typical

### When to Use
- Voltage reference circuits
- Overvoltage protection (across sensitive circuits)
- Power supply bias point stabilization

### Example Circuit
Connect Zener in series with resistor across 12V supply. If voltage exceeds Zener voltage (say 5.1V), Zener conducts and clamps voltage.

## Schottky Diodes

### Purpose
Fast switching, low voltage drop, power applications

### Characteristics
- Forward voltage: 0.2–0.4V (much lower than silicon)
- Speed: Very fast (nanoseconds recovery)
- Higher leakage: More reverse leakage than silicon
- Current rating: 1A to 50A+

### When to Use
- High-frequency switching (MHz+)
- Power supply output rectification (efficiency)
- Fast logic circuits
- Reverse polarity protection where low voltage drop is critical

### Advantage
Lower voltage drop saves power and reduces heating in high-current applications.

## LEDs (Light Emitting Diodes)

### Purpose
Light emission

### Characteristics
- Forward voltage: 1.5–3.5V (depends on color)
  - Red: 1.8–2.1V
  - Green: 1.9–2.5V
  - Blue: 3.0–3.5V
  - White: 3.0–3.5V
- Current rating: 5–20mA typical
- Power consumption: 10–100mW typical

### Important Notes
- **Never** connect LED directly to power supply
- **Always** use series resistor to limit current
- **Polarity matters**: Long lead is positive (anode)

### LED Circuit Design

To limit LED current to 10mA from 5V supply:
1. LED forward voltage: ~2V (red)
2. Voltage remaining: 5V – 2V = 3V
3. Current: I = 10mA
4. Resistor: R = 3V / 10mA = 300Ω
5. Power dissipated in resistor: P = 3V × 10mA = 30mW (use 1/4W resistor)

## Photodiodes

### Purpose
Convert light to electric current

### Characteristics
- Reverse biased operation (acts like current source)
- Output current proportional to light intensity
- Very high impedance (requires amplification)
- Response time: Nanoseconds to microseconds

### Applications
- Light sensors
- Optical receivers
- Camera sensors
- Sun tracking

## PIN Diodes

### Purpose
Fast switching, RF applications

### Characteristics
- Intrinsic (i) semiconductor layer between P and N
- Faster switching than regular diodes
- Lower capacitance variation

## Bridge Rectifier Diodes

### Purpose
Full-wave AC to DC conversion using 4 diodes

### Configuration
Four diodes arranged so AC input converts to DC output regardless of polarity

### Advantage
Uses all 4 phases of AC waveform (more efficient than half-wave)

## TVS Diodes (Transient Voltage Suppressors)

### Purpose
Protection from voltage spikes and ESD

### Characteristics
- Fast response (nanoseconds)
- Can conduct large currents briefly (amps, even kilowatts)
- Clamping voltage: Typically 5V–100V

### Applications
- ESD protection on inputs
- Overvoltage spike suppression
- Protection on sensitive circuits

## Tunnel Diodes

### Purpose
Specialized RF and oscillator applications (rare)

### Characteristics
- Negative resistance region
- Used for oscillators and amplifiers at RF frequencies
- Mostly historical (superceded by transistors)

## Step Recovery Diodes

### Purpose
Specialized pulse generation (rare)

## Comparison Table

| Type | Forward V | Speed | Leakage | Cost | Use |
|------|-----------|-------|---------|------|-----|
| Rectifier | 0.7V | Medium | Low | $ | General rectification |
| Zener | Reverse V | — | Higher | $ | Regulation |
| Schottky | 0.3V | Very Fast | Higher | $$ | High-speed, low-loss |
| LED | 2–3V | — | — | $ | Indicators |
| Photodiode | — | Very Fast | — | $$ | Light sensing |
| TVS | Variable | Nanosec | — | $ | Protection |

## Diode Specifications: What to Check

For any diode application, verify:
- **Forward voltage**: Affects circuit voltage drop and power dissipation
- **Reverse voltage rating**: Must exceed maximum reverse voltage in application
- **Current rating**: Must handle peak current without exceeding
- **Speed**: Fast enough for application frequency?
- **Temperature range**: Covers operating environment?
- **Package**: Surface mount (SMD) or through-hole?

## Key Takeaway

**Choose diode type based on application requirements: general purpose (rectifier), voltage reference (Zener), speed (Schottky), light (LED), or light detection (photodiode).**

Most common choices:
- **1N4007**: Universal rectifier diode
- **1N4148**: Fast switching diode
- **BZX55**: Zener diode for regulation
- **LED**: For indicators (choose by color and brightness)

Next: Real-world diode characteristics (non-ideal behavior).
