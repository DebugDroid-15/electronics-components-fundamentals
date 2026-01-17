# MOSFETs: Complete Overview

## What Is a MOSFET?

**MOSFET** stands for "Metal-Oxide-Semiconductor Field-Effect Transistor." It's a voltage-controlled switch/amplifier where a voltage on the **gate** controls current flow between **drain** and **source**.

## Three Terminals

- **Gate (G)**: Control signal input (voltage)
- **Drain (D)**: Main current output
- **Source (S)**: Main current return

## Two Types

### N-Channel (NMOS)
- Current flows from drain to source
- Gate positive (relative to source) turns it on
- More common due to better performance
- Example: IRF510

### P-Channel (PMOS)
- Current flows from source to drain
- Gate negative (relative to source) turns it on
- Complementary to NMOS
- Used when polarity inversion needed

## Key Advantage Over BJTs

**BJT**: Requires continuous base current to stay on → current control
**MOSFET**: Requires only gate voltage → voltage control

Practical implication: MOSFET needs almost no gate current (easier to drive)

## Operating Modes

### Off (Cutoff)
- Gate voltage below threshold (Vth)
- Drain-source path blocked
- Current ≈ 0
- Used for switch off state

### Linear (Triode)
- Gate voltage above threshold
- Drain-source acts like variable resistor
- Current varies with both gate voltage and drain-source voltage
- RDS(on) = on-state resistance (few milliohms to ohms)

### Saturation (Active)
- Gate voltage well above threshold
- Drain-source voltage low
- Current determined primarily by gate voltage and source resistance
- Used for switching on state
- Drain-source voltage can be as low as few millivolts

## Key Specification: RDS(on)

**RDS(on)** = resistance when MOSFET is fully on.

Typical values: 1mΩ to 10Ω depending on type and current rating.

**Power dissipation when on**: P = I² × RDS(on)

**Example**: 10A through 0.1Ω MOSFET → P = 100 × 0.01 = 10W

## Threshold Voltage (Vth)

**Vth** = gate-source voltage needed to turn MOSFET on.

Typical values: 1–5V depending on type

If gate voltage < Vth: MOSFET is off
If gate voltage > Vth + margin: MOSFET is on

## Gate Charge

Unlike BJT (base current), MOSFET gate draws very little DC current. However, turning it on/off requires charging/discharging the gate capacitance.

**Gate charge (Qg)**: Energy needed to fully switch MOSFET.

Affects switching speed and drive requirements.

## Switching Speed

MOSFETs switch **much faster** than BJTs:
- BJTs: Microseconds
- MOSFETs: Nanoseconds

This speed advantage makes MOSFETs ideal for:
- High-frequency switching power supplies
- Class D audio amplifiers
- Digital logic
- RF applications

## Power MOSFETs vs. Small Signal

### Small Signal MOSFETs
- Current: <1A
- Voltage: 30–100V typically
- Examples: 2N7000, BS170
- Used in analog circuits, logic switching

### Power MOSFETs
- Current: 1–100A+
- Voltage: 12V–600V typically
- Examples: IRF510, IRFZ44, IPP70R280CE
- Used in power converters, motor drives
- Require heatsinks

## Real-World Effects

### Temperature
- Vth increases ~4mV/°C (turns on at higher voltage when hot)
- RDS(on) increases with temperature (~0.5%/°C)
- Maximum current decreases with temperature

### Frequency
- MOSFETs work excellently at high frequency (MHz to GHz)
- Some RF MOSFETs rated for GHz operation
- Switching losses increase at high frequency

### Gate Drive Requirements
- NMOS gate needs high voltage relative to source
- PMOS gate needs low voltage relative to source
- Bootstrap circuits sometimes needed for gate driving
- Gate voltage must be within specified range or damage occurs

## Common MOSFET Mistakes

1. **Exceeding gate voltage**: Gate oxide breaks down
2. **Gate floating**: Noise on gate causes unpredictable switching
3. **No gate resistor**: Gate oscillates, causes ringing
4. **Inductive load without flyback diode**: Switch stress catastrophic
5. **Exceeding maximum ratings**: Thermal or voltage stress
6. **Not considering RDS(on) heating**: Power dissipation not accounted for

## MOSFET vs. BJT Summary

| Feature | BJT | MOSFET |
|---------|-----|--------|
| Control | Current | Voltage |
| Input impedance | Medium | Very high |
| Gate/Base current | Continuous | Only switching transient |
| Switching speed | Medium | Very fast |
| Power dissipation | Higher | Lower (especially at low on-resistance) |
| On-state voltage | ~0.2V | RDS(on) × I (mV to V) |
| Frequency range | Audio to low MHz | DC to GHz |
| Complexity | Moderate | Moderate (need drive circuit) |
| Modern preference | Declining | Increasing |

## When to Use MOSFETs

- **Power supplies**: Switching regulators
- **Motor control**: PWM (pulse width modulation)
- **Audio amplifiers**: Class D designs
- **Digital switching**: TTL/CMOS level interfacing
- **High-frequency circuits**: MHz and above
- **Battery-powered devices**: Low power dissipation
- **Modern designs**: Essentially all modern power electronics

## Professional MOSFET Design

1. **Choose appropriate voltage/current rating** with margin (1.5–2×)
2. **Calculate gate drive requirements** (charge, frequency, current)
3. **Size gate resistor** to balance speed and noise
4. **Plan thermal management** (heatsink if necessary)
5. **Add snubber/flyback protection** for inductive loads
6. **Test at temperature extremes**
7. **Verify switching frequency** doesn't exceed capability
8. **Measure actual behavior** on prototype before production

## Key Takeaway

**MOSFETs are voltage-controlled switches that are faster, more efficient, and easier to drive than BJTs. They're the standard choice for modern power electronics and high-frequency applications.**

---

Complete coverage includes files on basics, enhancement vs. depletion modes, switching vs. amplification, real-world behavior, and common mistakes. MOSFETs form the foundation of modern power electronics and are essential knowledge for any electronics engineer.
