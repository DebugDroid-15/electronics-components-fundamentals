# Practical BJT Usage: Switching and Amplification

## BJT as a Switch

### Basic Switch Configuration

```
        VCC (supply voltage)
         |
         | RL (load resistor)
         |
    Collector (C)
         |
    [  BJT  ]
         |
    Emitter (E)
      (to GND)
         
    Base (B) <- Control signal
```

### How BJT Switching Works

**When base current = 0** (cutoff):
- Collector current ≈ 0
- Voltage from collector to ground ≈ VCC (full supply voltage)
- Output signal: HIGH (logic 1)

**When base current is large** (saturation):
- Collector current ≈ (VCC - VCE(sat)) / RL
- Voltage from collector to ground ≈ 0.2–0.3V
- Output signal: LOW (logic 0)

### Output Voltage Swing

In switching application, output voltage swings between:
- **Off state**: VCC (when IB ≈ 0)
- **On state**: VCE(sat) ≈ 0.2V (when IB is saturating)

This ~VCC swing is why transistor switches are useful.

## Calculating Base Current for Saturation

**Goal**: Saturate collector current to a desired level.

**Design steps**:

1. **Determine desired collector current**:
   $$I_C = \frac{V_{CC} - V_{CE(sat)}}{R_L}$$
   
   Example: VCC = 5V, RL = 50Ω, VCE(sat) = 0.2V
   $$I_C = \frac{5 - 0.2}{50} = 96 \text{mA}$$

2. **Calculate base current for saturation** (with 2–3× margin):
   $$I_B = \frac{I_C}{h_{FE} \times 2.5}$$
   
   Example: IC = 96mA, hFE = 100
   $$I_B = \frac{96}{100 \times 2.5} = 0.384 \text{mA}$$
   
   With 2.5× margin, we need ~0.4mA base current.

3. **Calculate base resistor** (if driven from logic signal):
   $$R_B = \frac{V_{input} - V_{BE}}{I_B}$$
   
   Example: VInput = 5V, VBE = 0.7V, IB = 0.4mA
   $$R_B = \frac{5 - 0.7}{0.4mA} = 10.75k\Omega$$
   
   Use standard resistor: 10kΩ

## Practical Example: LED Switch

### Circuit
```
VCC (5V)
  |
  [220Ω RL]  <- Current limits LED
  |
  [> LE (red)
  |
  | C (collector)
[NPN transistor]
  | E (emitter)
  |
 GND

Base (B) <- Control signal (0V off, 5V on)
```

### Design

**LED specs**: 2V forward, 20mA max

**Circuit analysis**:
- VCC = 5V
- LED voltage drop: 2V
- Voltage across RL: 5V - 2V = 3V
- Desired LED current: 20mA
- RL = 3V / 20mA = 150Ω (use 150Ω resistor)
- IC needed: 20mA

**Base current**:
- Using 2N3904 (hFE ≈ 100)
- IB = 20mA / (100 × 2.5) = 0.08mA
- RB = (5V - 0.7V) / 0.08mA ≈ 54kΩ (use 47kΩ standard)

**Result**: Small 5V logic signal switches 20mA LED on/off.

## Flyback Diode Protection

When switching inductive loads (relays, motors, solenoids), an inductive spike occurs when turning off. This can destroy the transistor.

### Protection Circuit
```
        VCC
         |
      [Relay]
         |
    Collector (C)
         |
    [  BJT  ]
         |
    Emitter (E) -- [Diode cathode]
      (to GND)     [Diode anode] -- back to collector
         
    Base (B) <- Control signal
```

The **flyback diode** (also called freewheeling diode):
- Blocks current during normal operation
- When transistor turns off, inductive spike tries to raise collector voltage
- Diode conducts, dumps inductive energy to ground
- Protects transistor from excessive VCE

**Diode selection**: 1N4148 (small signal) or 1N4007 (general purpose)

## BJT as an Amplifier

### Linear Amplification

In **active region**, small input signal is amplified to larger output signal.

```
Input signal (small AC)
  |
  [Rin] -- Base (B)
           |
      [  BJT  ]
           |
      Collector (C)
           |
        [RL]
         |
      Output (large AC)
```

### Voltage Gain

Approximate voltage gain:

$$A_v = -g_m \times R_L$$

Where:
- gm = transconductance (depends on collector current)
- RL = collector resistor
- Negative sign means output is inverted from input

For practical circuits: Gain typically 10–100 (20–40dB)

### Common Emitter Amplifier

Most basic audio amplifier topology:
- Input applied to base
- Output taken from collector
- Emitter to ground (sometimes via resistor)
- Provides good gain with reasonable impedance

### Frequency Response

BJTs work well for:
- **Audio frequencies**: 20Hz–20kHz (excellent)
- **Low RF**: kHz range (fine)
- **Higher RF**: MHz (limited; requires optimization)

High-frequency limitations:
- Base-collector junction capacitance
- Transit time of charge carriers
- At MHz, special RF transistors needed

## Biasing for Amplification

To operate BJT as amplifier, must establish **Q-point** (quiescent point):

**Q-point** = operating point when no signal applied.

Typical choice: VCE(Q) ≈ VCC/2 (maximum output swing)

### Biasing Methods

**Fixed base bias** (simplest):
- Base connected to VCC through resistor
- Simple but hFE variation causes Q-point drift

**Voltage divider bias** (common):
- Base biased from voltage divider
- More stable, compensates somewhat for temperature
- Used in most practical circuits

**Emitter stabilization**:
- Resistor in emitter path
- Negative feedback stabilizes Q-point
- Best stability against temperature and hFE variation

## Real Amplifier Considerations

### Coupling Capacitors

AC input/output often coupled through capacitors:
- Blocks DC component
- Passes AC signal
- Sizes: Larger for lower frequencies

### Input/Output Impedance

- Input impedance: Moderate (kΩ range typical)
- Output impedance: RL (few kΩ typical)
- May need impedance matching for some applications

### Frequency Response

Determined by:
- Coupling capacitors (high-pass filter)
- Emitter bypass capacitor (if present)
- Transistor junction capacitances (low-pass roll-off)

Typical -3dB bandwidth: 100Hz to 100kHz depending on design

### Noise

BJT amplifiers have moderate noise:
- Better than MOSFET (due to lower input impedance)
- Worse than op-amps
- Base current noise significant
- Shot noise from collector current

## Power Dissipation in Amplification

Unlike switching (where power is minimal), amplification generates continuous heat:

$$P = V_{CE} \times I_C$$

If VCE = 2V and IC = 50mA: P = 100mW (noticeable heat)

At higher power levels, heatsink required.

## BJT vs. Op-Amp Amplification

| Feature | BJT | Op-Amp |
|---------|-----|--------|
| Gain | Moderate | Very high |
| Impedance | Moderate | Very high (non-inverting input) |
| Frequency | Limited to MHz | kHz to low MHz |
| Noise | Moderate | Low (with right device) |
| Simplicity | Simple (3 components) | Requires feedback |
| Power supply | Single or dual | Single or dual |
| Use | Low-level, audio | Almost everything else |

## Key Takeaway

**BJTs can switch (on/off) or amplify (analog). Switching uses saturation/cutoff regions with minimal power. Amplification uses active region with continuous power dissipation. Professional designs include safety margins for temperature and component variation.**
