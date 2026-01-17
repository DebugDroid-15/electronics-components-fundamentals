# Real Diode Characteristics: Non-Ideal Behavior

## Forward Direction: Real vs. Ideal

### Ideal Model
- Below forward voltage threshold: No current
- Above threshold: Perfect conduction (zero resistance)

### Real Behavior
- Forward voltage is not a sharp threshold; it's exponential
- Current increases smoothly from zero
- Never truly "zero" below threshold (leakage current exists)
- Never truly "infinite" conductivity (series resistance ~1–10Ω typical)

### Exponential Relationship

Current follows approximately:

$$I = I_s (e^{qV/kT} - 1)$$

Where:
- Is = saturation current (very small)
- q = electron charge
- V = voltage
- k = Boltzmann constant
- T = absolute temperature

**Practical implication**: Small voltage changes cause large current changes. At 0.6V, a 10mV increase doubles current.

## Temperature Effects

### Forward Voltage vs. Temperature

Forward voltage **decreases** with temperature (~2mV/°C for silicon):

- At 0°C: Forward voltage ~0.75V
- At 25°C: Forward voltage ~0.70V
- At 85°C: Forward voltage ~0.63V

**Implication for LED circuits**:
- LED brightness increases at higher temperature (less voltage drop, more current)
- LED brightness decreases at lower temperature
- Temperature-stable design requires active current regulation

### Reverse Leakage Current vs. Temperature

Leakage current approximately **doubles every 25–30°C increase** in temperature.

- At 25°C: Leakage might be 10nA
- At 85°C: Leakage might be 100nA to 1µA

**Implication**: At high temperature, reverse diode is not perfect insulator. Leakage becomes measurable.

### Reverse Breakdown vs. Temperature

Reverse breakdown voltage **decreases** slightly at higher temperature (~0.1%/°C):

- At 25°C: Breakdown at 1000V
- At 85°C: Breakdown at 994V (0.6% lower)

Most applications don't operate near breakdown, so this is minor.

## Switching Speed and Reverse Recovery

### What Is Reverse Recovery?

When forward current is switched off, diode doesn't immediately stop conducting. It takes time (reverse recovery time).

- Before recovery: Diode still conducts backward
- Recovery time: How long until diode fully blocks
- Typical: 10–100ns for general-purpose diodes, <1ns for Schottky

### Why It Matters

In high-frequency switching circuits:
- Residual conduction during "off" time wastes power
- Can cause crosstalk
- Limits switching frequency

**Solution**: Use fast diodes (Schottky or ultrafast recovery) for high frequencies.

## Capacitive Effects (Junction Capacitance)

Real diodes have **junction capacitance**:
- Forward biased: ~10–100pF typical
- Reverse biased: Higher (can be 100pF to 1nF depending on voltage)
- Affects high-frequency response

### Implication
At RF frequencies (MHz+), diode impedance is affected by this capacitance. Creates impedance mismatch and filtering effects.

## Reverse Leakage Current: The Non-Ideal Reverse Behavior

**Ideal model**: Perfect insulator in reverse direction (infinite resistance).

**Real behavior**: Small leakage current flows even when reverse biased.

**Causes**:
- Thermal generation of charge carriers
- Ionization in depletion region
- Contamination in semiconductor material

**Temperature dependence**: Leakage approximately **doubles every 25°C**.

**Practical implications**:
- At room temperature: Negligible (nanoamps)
- At 85°C: Microamps (measurable)
- At 125°C: Milliamps (significant)

## Series Resistance

Real diodes have series resistance (few ohms):

$$V_{diode} = V_{forward\_voltage} + I \times R_s$$

Where Rs = series resistance (~1–10Ω typical)

**Effect**:
- At low current: Series resistance effect negligible
- At high current: Voltage drop increases proportionally
- Power dissipation increases

## Voltage Coefficient

Forward voltage changes not only with temperature but also with current:
- Higher current → slightly higher forward voltage
- Relationship logarithmic

## Noise and Fluctuations

Real diodes exhibit **shot noise** due to discrete charge carriers:
- Thermal noise from resistance
- Proportional to current and bandwidth
- Negligible in most circuits, important in precision measurement

## Thermal Effects

### Self-Heating

High current through diode generates heat:

$$P = I \times V_{forward}$$

Example: 1A through 0.7V diode → 0.7W dissipation

This heat raises diode temperature, which affects forward voltage and leakage.

### Thermal Runaway Risk

In some scenarios (like Zener operation):
- Heat increases leakage
- Increased leakage increases heat
- Cascade effect possible

### Thermal Design

For high-current diodes:
- Must dissipate heat (heat sink)
- Check thermal resistance (°C/W) on datasheet
- Verify junction temperature stays below Tjmax

## Non-Linearity

Diode IV relationship is nonlinear. This is both advantage and disadvantage:

**Advantage**: Enables special functions (mixing, detection)

**Disadvantage**: Makes circuit analysis more complex, can't just use Ohm's law

## Breakdown Modes

### Avalanche Breakdown
- Electrons hit lattice, create more electrons
- Cascade effect at high reverse voltage
- Reversible (diode survives if current limited)

### Zener Breakdown
- Direct ionization at electric field
- Different mechanism, occurs at lower voltage
- Also reversible if current limited

**Implication**: If reverse voltage exceeds breakdown, diode conducts heavily (must be current-limited or damage results).

## Real vs. Ideal: Summary Table

| Property | Ideal | Real |
|----------|-------|------|
| Forward direction (below threshold) | Zero current | Leakage nanoamps |
| Forward threshold | Sharp step | Smooth exponential curve |
| Forward voltage | Fixed | Depends on current, temperature |
| Reverse direction | Infinite resistance | Leakage current (temperature dependent) |
| Reverse breakdown | Never | At specified voltage (voltage rating) |
| Series resistance | Zero | Few ohms |
| Capacitance | Zero | 10pF to 1nF depending on bias |
| Response time | Instant | Recovery time (nanoseconds to hundreds of ns) |

## Key Takeaway

**Real diodes are more complex than the simple "one-way valve" model suggests. Temperature, current, frequency, and voltage all affect behavior.**

Professional design accounts for:
- Temperature effects on forward voltage
- Leakage current at operating temperature
- Recovery time in switching circuits
- Heat dissipation for high-current applications
- Reverse breakdown voltage margins

The simple model (0.7V drop, acts as switch) works for basic circuits but breaks down in precision, high-frequency, or high-temperature applications.

Next: Common diode mistakes.
