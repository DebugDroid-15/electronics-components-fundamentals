# BJTs (Bipolar Junction Transistors): Complete Overview

## What is a BJT?

A **BJT** is a three-terminal semiconductor device that **amplifies** or **switches** current. Unlike diodes (one-way valve), BJTs are controllable valves—the amount they conduct depends on a control signal.

## Basic BJT Operation

### Three Terminals
- **Emitter (E)**: Current exits (or enters)
- **Base (B)**: Control terminal (small current here controls large current)
- **Collector (C)**: Current enters (or exits)

### Two Types
- **NPN**: Majority carriers are electrons (more common)
- **PNP**: Majority carriers are holes (less common)

### The Fundamental Property

Small current into the base **controls** large current between collector and emitter:

$$I_C = h_{FE} \times I_B$$

Where:
- IC = collector current
- IB = base current
- hFE = current gain (typically 50–200 for silicon BJTs)

**Practical meaning**: 1mA base current can control 50–200mA collector current (amplification).

## Operating Regions

### Cutoff (Off)
- Base current ≈ 0
- Collector current ≈ 0
- BJT acts like open circuit
- Used for switching applications (off state)

### Active (Amplification)
- Base current present
- Collector current = hFE × base current
- Voltage between collector and emitter can be controlled
- Used for amplification

### Saturation (On)
- Base current is large enough to fully "open" the collector-emitter path
- Collector-emitter voltage drops to near zero (~0.2V)
- Collector current limited by external circuit resistance
- BJT acts almost like a closed switch
- Used for switching applications (on state)

## Collector-Emitter Voltage

In active region, there's always a voltage drop across collector-emitter:
- Minimum: ~0.2–0.3V when saturated
- Varies from 0.2V to near supply voltage depending on base current and load

This is why BJTs dissipate heat—they act like variable resistors with this voltage drop.

## Practical BJT Examples

**2N2222 (NPN)**:
- Small signal transistor
- Low power (few watts)
- hFE ≈ 100
- Used in audio, sensors, logic

**2N3904 (NPN)**:
- Very common small signal transistor
- Maximum IC ≈ 200mA
- Used everywhere in hobbyist circuits

**2N3055 (NPN)**:
- Power transistor
- Maximum IC ≈ 15A
- Requires heatsink for high power
- Audio amplifier output stage

**2N2907 (PNP)**:
- Complementary to 2N2222
- Used when PNP is needed

## BJT as Switch

### Switch Design (On/Off)

For switching application:
1. **Off**: Base current ≈ 0, no collector current
2. **On**: Large enough base current to fully saturate
3. **Voltage from collector to ground**: Switches between 0V (on) and supply voltage (off)

### Calculation for Saturation

To fully saturate BJT:
- Required base current: IB = IC_desired / hFE (or 2–3× this for safety margin)

**Example**: Switch 100mA at 5V with 2N3904 (hFE ≈ 100)
- Base current needed: 100mA / 100 = 1mA minimum
- For safety (3× margin): 3mA
- Using 5V logic, resistor from logic output to base: R = 5V / 3mA ≈ 1.5kΩ

## BJT as Amplifier

### Voltage Amplifier

BJT amplifies voltage changes at base to larger voltage changes at collector.

**Gain**: Depends on circuit configuration, typically 10–100×

**Used in**:
- Audio pre-amplifiers
- Sensor amplifiers
- Small-signal processing

### Common Configurations

**Common Emitter**: Most gain, inverts signal
**Common Collector**: Low gain, buffer (impedance matching)
**Common Base**: Very high frequency, rare

## Thermal Characteristics

### Power Dissipation

P = VCE × IC

Where:
- VCE = collector-emitter voltage
- IC = collector current

**Example**: VCE = 2V, IC = 50mA → P = 100mW

### Heat and Failure

- BJTs get hot when amplifying or switching high current
- Heat increases leakage, reduces gain, changes characteristics
- High-power BJTs require heatsinks
- Thermal runaway possible (heat increases leakage, which increases heat)

### Temperature Derating

Maximum collector current decreases at higher temperature:
- At 25°C: Max IC = 15A (for 2N3055)
- At 125°C: Max IC ≈ 6A (derated 60%)

## Frequency Response

BJT is fast enough for:
- Audio frequencies: Excellent
- Kilohertz to low MHz: Good
- High MHz to GHz: Requires special RF transistors

**Limitations**:
- Base-collector capacitance limits high-frequency operation
- At MHz, additional considerations needed
- Can't be used directly at GHz (need specialized RF transistors or use as amplifier for FETs/MOSFETs which are faster)

## Real-World Effects

**Temperature**: Gain increases, leakage increases with temperature
**Frequency**: Gain decreases at high frequency
**Voltage**: VBE (base-emitter voltage) decreases ~2mV/°C
**Aging**: Characteristics drift slowly over decades

## Common Mistakes

1. **No base current limiting**: BJT will draw excessive base current
2. **Wrong polarity**: NPN vs. PNP confusion
3. **Exceeding maximum ratings**: Too much IC or VCE causes failure
4. **No heatsink**: Power BJTs get extremely hot
5. **No flyback protection**: Switching inductive loads needs protection diode

## BJT vs. MOSFET

| Property | BJT | MOSFET |
|----------|-----|--------|
| Control | Current (base) | Voltage (gate) |
| Input impedance | Medium | Very high |
| Switching speed | Medium | Very fast |
| Power dissipation | Higher | Lower |
| Use | Audio, low-frequency | Power switching, high-frequency |

## When to Use BJTs

- **Audio amplifiers**: Good frequency response, low noise
- **Sensor amplifiers**: Reasonable gain and impedance
- **Logic switching**: Adequate speed
- **Low-frequency switching**: Relays, solenoids
- **Historical designs**: Lots of existing circuits use them

## Modern Trend

MOSFETs are increasingly replacing BJTs:
- Faster switching
- Lower power dissipation
- Easier to use (voltage control instead of current)
- Better for modern high-speed circuits

But BJTs remain useful for specific applications.

## Key Takeaway

**BJTs are voltage/current controlled switches or amplifiers. Small base current controls large collector current. They work but are being superceded by MOSFETs in many modern designs.**

Next: MOSFETs (modern alternative with different properties).
