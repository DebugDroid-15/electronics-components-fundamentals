# Diodes: Complete Reference

This is a comprehensive guide combining all diode topics.

## Section Overview

Files: README, diode-basics, diode-types, real-characteristics, common-mistakes

## Complete Diode Knowledge Base

Diodes are semiconductor devices that conduct current in one direction (forward bias) and block it in the other (reverse bias).

### Key Characteristics
- Forward voltage drop: 0.6–0.7V (silicon), 0.2–0.3V (germanium)
- Reverse breakdown voltage: 50V to 1000V+ depending on type
- Current rating: microamps to tens of amps
- Temperature coefficient: Forward voltage decreases ~2mV/°C

### Common Types

**Rectifier Diodes** (1N4148, 1N4007):
- General purpose, medium current
- Used for power supply rectification
- Voltage: 50–1000V
- Current: 0.1–3A

**Zener Diodes** (1N4733, BZX55):
- Voltage regulation
- Conduct in reverse at specific voltage
- Used for protection and reference
- Voltage: 3.3V–200V

**LEDs** (Various):
- Light emission at specific wavelengths
- Forward voltage: 1.5–3.5V
- Current: 2–20mA typical
- Colors: Visible and infrared

**Photodiodes** (BPW34, S1223):
- Reverse biased light sensor
- Generate current proportional to light
- High impedance
- Used in optical applications

### Real Characteristics

**Temperature Effects**:
- Forward voltage drops ~2mV/°C
- Leakage current increases with temperature
- Reverse breakdown voltage decreases slightly

**Frequency Effects**:
- Switching diodes have limited frequency response
- Recovery time (how fast it switches) matters at high frequencies
- Schottky diodes faster than silicon diodes

**Parasitic Effects**:
- Junction capacitance (affects switching speed)
- Series resistance (voltage drop at high current)
- Parasitic inductance in leads

### Common Mistakes

1. **No current limiting resistor**: Diode current must be limited
2. **Wrong polarity**: Diode conducts only one way
3. **Exceeding reverse voltage**: Breakdown causes failure
4. **Forward voltage drop ignored**: LED circuits must account for ~2V drop total
5. **Reverse recovery time**: Matters in fast-switching circuits

### When to Use

- **Rectification**: Convert AC to DC in power supplies
- **Reverse polarity protection**: Prevents damage if powered backward
- **LED indicators**: Visual feedback
- **Voltage regulation**: Zener diode reference
- **Photosensing**: Photodiode light detection
- **Fast switching**: Schottky diodes for MHz+ applications

### Professional Design Practices

1. Always include current-limiting resistor with LEDs
2. Add protection diodes across inductive loads
3. Account for forward voltage drop in calculations
4. Verify reverse voltage ratings exceed worst-case voltage
5. Use proper diode type for frequency/temperature range

## Key Takeaway

Diodes are electronic one-way valves. They conduct in forward direction (with ~0.6–0.7V drop) and block in reverse direction. Proper use requires understanding forward voltage, current rating, and reverse breakdown voltage.

---

Next sections: BJTs and MOSFETs (more complex active components).
