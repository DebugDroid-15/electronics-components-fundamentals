# Losses and Q Factor: Understanding Inductor Efficiency

## The Problem: Real Inductors Aren't Perfect

**Ideal inductor**: Pure inductance, zero losses, all energy stored returns to circuit.

**Real inductor**: Has resistance, core losses, and radiates energy.

These losses are quantified by the **Q factor** (quality factor).

## Sources of Losses in Inductors

### 1. Wire Resistance (DCR)

The coil wire has resistance (even though it's a conductor):
- Thin wire has higher resistance than thick wire
- Longer coil has more resistance than shorter
- Current flowing through this resistance dissipates power: P = I²R

**Impact**:
- Causes heating
- Reduces efficiency
- Less energy returns to circuit

**Typical values**:
- Small signal inductor: 1–10Ω
- Power inductor: 0.1–1Ω (thick wire)
- Large power inductor: 0.01Ω or less

### 2. Core Loss

The magnetic core itself dissipates energy due to:

**Hysteresis loss**: Energy needed to magnetize/demagnetize the core as AC current reverses.

**Eddy current loss**: Induced currents in conductive core material that circulate and dissipate heat.

**Impact**:
- More significant at higher frequencies
- More significant with larger currents
- Iron cores have higher core loss than ferrite at same frequency

**Frequency dependence**:
- At 60 Hz: Minimal core loss
- At 10 kHz: Noticeable core loss
- At 1 MHz: Dominant loss for many cores

### 3. Radiation Loss

Magnetic field around inductor radiates energy (especially at high frequencies). The radiated energy is lost from the circuit.

**Impact**:
- Minimal at low frequencies
- Becomes significant at RF frequencies
- Shielded inductors (like toroidal) reduce radiation loss

## Quality Factor (Q): Measuring Efficiency

**Q factor** is the ratio of energy stored to energy dissipated per cycle:

$$Q = \frac{2\pi \times \text{Energy Stored}}{\text{Energy Dissipated per Cycle}}$$

Or more practically:

$$Q = \frac{X_L}{R_{total}} = \frac{2\pi f L}{R}$$

Where:
- XL = inductive reactance
- R = total losses (wire resistance + core loss)
- f = frequency
- L = inductance

### Practical Interpretation

- **High Q** (> 100): Efficient, minimal losses, good energy storage
- **Medium Q** (10–100): Moderate efficiency
- **Low Q** (< 10): Poor efficiency, lots of losses

### Q Factor Dependence on Frequency

Q changes dramatically with frequency:

**Low frequency**:
- Q limited by wire resistance (core loss minimal)
- Q relatively constant

**Mid frequency**:
- Q increases with frequency (XL increases faster than core loss)

**High frequency**:
- Q decreases (core loss increases faster than XL)
- Inductor becomes lossy

The frequency where Q is maximum depends on core material.

## Real Q Values by Type

**Air core inductor** (1 µH at 1 MHz):
- Q ≈ 100–200 (very good)

**Ferrite core inductor** (10 µH at 100 kHz):
- Q ≈ 50–100 (good)

**Iron core inductor** (100 mH at 60 Hz):
- Q ≈ 10–50 (moderate)
- At higher frequency (1 kHz): Q might drop to 5 (poor)

**Power supply inductor** (100 µH at 500 kHz):
- Q ≈ 20–50 (moderate, designed for power, not efficiency)

## Calculating Losses

### Example: Power Supply Inductor

- Inductance: L = 100 µH
- DC resistance: Rdc = 0.1Ω
- Frequency: f = 500 kHz
- Current: I = 10A

**Impedance**:
- XL = 2πfL = 2π × 500×10³ × 100×10⁻⁶ ≈ 314Ω

**Q Factor**:
- Q = 314 / 0.1 = 3,140 (excellent!)

**Power loss**:
- P = I² × Rdc = 100 × 0.1 = 10W

But wait—this doesn't include core loss! Adding core loss (say 5W for this frequency and current):
- Total loss ≈ 15W
- Efficiency: (Energy transferred – losses) / Energy transferred × 100%

In switching power supplies, 15W loss on a 100W supply is 15% loss—significant!

## Real-World Implications of Q

### High-Q Applications
- RF tuning circuits
- Precision resonators
- Frequency-selective filters

Here, high Q is good—means minimal losses, sharp frequency response.

### Low-Q Applications
- Power supply inductors
- Broadband filters
- EMI suppression

Here, Q doesn't matter as much. You want the inductance value and saturation current, not efficiency.

## Thermal Management

Inductor losses appear as heat:
- Small signal inductors: Losses negligible
- Power supply inductors: Losses are significant
- Must account for thermal rise

Example:
- Inductor dissipating 15W
- Thermal resistance to ambient: 50°C/W
- Temperature rise above ambient: 15W × 50°C/W = 750°C (failure!)

**Solution**: Must cool the inductor or reduce losses (use lower-resistance wire, better core).

## Frequency Response of Real Inductors

The impedance of a real inductor varies with frequency:

$$Z = \sqrt{R^2 + (2\pi f L)^2}$$

**Low frequency** (DC):
- Z ≈ R (just the DC resistance)
- Inductor looks like resistor

**Mid frequency**:
- Z increases with frequency (inductance dominates)

**High frequency**:
- Approach self-resonant frequency (SRF): Z peaks
- Above SRF: Parasitic capacitance dominates, impedance decreases

## Resonance in Real Inductors

Like capacitors, inductors have parasitic capacitance (between turns, leads, etc.).

This creates a **self-resonant frequency** (SRF):

$$f_{SRF} = \frac{1}{2\pi \sqrt{LC_{parasitic}}}$$

Above SRF:
- Inductor looks like capacitor
- Impedance decreases with frequency
- Inductance is no longer effective

## Q and Bandwidth

Q factor relates to **bandwidth** in resonant circuits:

$$BW = \frac{f_0}{Q}$$

Where f₀ is the resonant frequency.

- High Q → Narrow bandwidth (sharp response)
- Low Q → Wide bandwidth (gentle response)

This is useful for filters and oscillators.

## Key Takeaway

**Real inductors have losses that reduce efficiency and limit their useful frequency range.** 

Professional designers:
1. Calculate expected power dissipation
2. Verify thermal management is adequate
3. Account for Q factor in frequency-critical applications
4. Understand frequency limitations (SRF)
5. Choose inductor type appropriate for application

Q factor tells you the whole story: high Q means efficient, low Q means lossy. But for power applications, you often care more about saturation current and thermal management than Q.

Next: Real-world frequency and temperature effects.
