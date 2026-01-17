# Real-World Capacitor Behavior: Parasitic Effects and Frequency Response

## Beyond the Ideal Model

**Ideal capacitor**: Pure capacitance, no other properties.

**Real capacitor**: Complex impedance with capacitance, resistance, and inductance all playing roles.

## Equivalent Series Resistance (ESR)

**ESR** is the most important parasitic effect in real capacitors.

### What Is ESR?

ESR represents the effective series resistance of a capacitor:
$$Z = R_{ESR} + \frac{1}{j \omega C}$$

Where ESR includes:
- **Lead resistance**: Resistance of the metal leads
- **Plate resistance**: Resistance of the conductive plates
- **Dielectric resistance**: Very small, from the insulating material
- **Contact resistance**: Resistance at connections

### ESR Values by Type

| Type | Typical ESR |
|------|-----------|
| Ceramic | 1–50 mΩ (low) |
| Film | 0.1–10 mΩ (very low) |
| Aluminum electrolytic | 10–1000 mΩ (high, varies widely) |
| Tantalum | 1–100 mΩ (moderate) |
| Low-ESR aluminum (specialized) | 1–50 mΩ (good) |

## Why ESR Matters

### Power Dissipation from ESR

When current flows through a capacitor, ESR causes power dissipation:

$$P = I^2 \times R_{ESR}$$

**Example**: 
- 10 µF aluminum electrolytic with 100 mΩ ESR
- 1 amp of AC current at 1 kHz
- Power dissipated: 1² × 0.1 = 0.1W

This heating stresses the capacitor and reduces lifetime.

### High-Frequency Response

At high frequencies, ESR becomes the dominant impedance:
$$Z_{high-freq} \approx R_{ESR}$$

A "1000 µF" capacitor might have:
- At DC: Looks like a 1000 µF capacitor
- At 100 Hz: Mixed capacitive and resistive
- At 100 kHz: Looks like ~50 mΩ resistor (if ESR is 50 mΩ)

**Implication**: High-frequency noise is not filtered well by electrolytics. Use smaller film or ceramic capacitors in parallel for high-frequency filtering.

## Equivalent Series Inductance (ESL)

Real capacitors also have parasitic **inductance** from their leads and internal geometry.

### ESL Values
- Typical: 0.5–5 nanohenries
- Depends on lead length, geometry
- Shorter leads = lower ESL

### Self-Resonant Frequency

ESR and ESL combine to create a **resonant frequency**:

$$f_{SRF} = \frac{1}{2\pi \sqrt{LC}}$$

At this frequency, the capacitor has **minimum impedance**. Above this frequency, the capacitor looks inductive!

**Example**:
- 10 µF capacitor with 2 nH ESL
- SRF = 1/(2π √(2×10⁻⁹ × 10×10⁻⁶)) ≈ 1.1 MHz

Below 1.1 MHz: Capacitive impedance dominates (impedance decreases with frequency)  
At 1.1 MHz: Minimum impedance (most effective filtering)  
Above 1.1 MHz: Inductive impedance dominates (impedance increases with frequency, capacitor becomes ineffective)

## Implications for Real Circuits

### Power Supply Decoupling

A single large electrolytic capacitor is ineffective at high frequencies:
- Low capacitance types have lower SRF (larger capacitors = lower frequency)
- 100 µF electrolytic might have SRF at 100 kHz
- Above 100 kHz, it looks inductive
- High-frequency noise bypasses it

**Professional solution**: Use multiple capacitors in parallel:
- Large electrolytic (100 µF+): Low-frequency filtering, bulk energy storage
- Medium ceramic (10 µF): Mid-frequency filtering
- Small ceramic (0.1 µF): High-frequency filtering

Each capacitor resonates at a different frequency, together covering wide frequency range.

### RF Circuits

High-frequency circuits must:
- Use low-ESR capacitors
- Use components with short leads (minimize ESL)
- Use capacitors with high SRF (small capacitance or film types)
- Carefully route PCB to minimize parasitic inductance

## Temperature Dependence of ESR

ESR increases with temperature:
- Typically increases 2–5% per °C
- At 125°C, ESR might be 2–3× higher than at 25°C

This has practical implications:
- Power supply stability worsens at higher temperature (higher ESR reduces filtering)
- Thermal runaway risk: More ESR → More heat → Worse ESR

## Frequency-Dependent Capacitance

Some capacitors show **frequency dependence** of capacitance itself (beyond ESR effects).

Especially in dielectric materials with high loss (like some ceramics):
- Capacitance decreases at higher frequencies
- Effect more pronounced in lower-quality ceramics

**Example**:
- Ceramic capacitor rated 100 µF at 1 kHz
- At 100 kHz: Might be 95 µF
- At 1 MHz: Might be 80 µF

This is why datasheets often specify capacitance at a specific frequency (usually 1 kHz).

## Ripple Current Rating

When AC current flows through a capacitor (superimposed on DC), ESR causes heating.

Capacitors have a **ripple current rating**: Maximum AC current at a given frequency and temperature that the capacitor can handle.

**Significance**:
- Electrolytics in switching power supplies must handle ripple current
- Exceeding ripple current rating causes heating, accelerates aging
- Specifications matter: 85°C rated electrolytics can handle more ripple than 105°C types (lower resistance)

## Dielectric Absorption

Some capacitors exhibit **dielectric absorption** (memory effect):

1. Capacitor is charged
2. Capacitor is discharged
3. After a few seconds, voltage reappears (small) as trapped charge re-emerges

**Effect**: After an initial discharge, capacitor slowly re-charges itself to a small voltage.

**Why it matters**:
- Precision measurement circuits can be fooled
- Timing circuits might not discharge completely
- Audio circuits can develop strange artifacts

**Capacitors with low absorption**:
- Film capacitors: Very low
- High-quality ceramic: Low
- Electrolytics: Can be significant

This is why precision analog circuits prefer film capacitors.

## Voltage Reversal

If a capacitor is suddenly forced to reverse polarity (positive voltage becomes negative), it can:
- Develop internal stress
- Accelerate aging
- In worst cases, fail

**Protection**: Many circuits include diodes to prevent voltage reversal across capacitors.

## Real-World Measurement

Using a capacitor meter on a real capacitor:
- Reads lower than marked value (due to ESR and measurement frequency)
- Different meters give different readings (they measure at different frequencies)
- Temperature affects reading

**Example**:
- Marked: 100 µF
- Meter reads: 95 µF (at 1 kHz)
- Same meter at 10 kHz: 92 µF

This variation is normal and expected.

## Key Takeaway

**Real capacitors are not pure capacitance. They have ESR, ESL, and frequency-dependent behavior that dominates at high frequencies.**

Understanding parasitic effects means:
- Recognizing that a capacitor is ineffective above its self-resonant frequency
- Using multiple capacitors for wide-frequency filtering
- Accounting for ESR heating in power applications
- Choosing the right capacitor type for the frequency range

Next: Common mistakes with capacitors.
