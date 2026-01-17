# Real-World Inductor Behavior

## Temperature Effects

Like all components, inductors change with temperature.

### Inductance vs. Temperature

The inductance of a ferrite or iron core inductor changes with temperature due to permeability variation:

- **Ferrite**: ±20% typical change over -40°C to +85°C
- **Iron**: ±10% typical change

Unlike resistors (linear temperature coefficient), inductance change is often nonlinear.

**Example**: Ferrite inductor at 25°C = 100 µH
- At 0°C: Might be 105 µH (permeability increases at lower temp for some materials)
- At 85°C: Might be 90 µH (permeability decreases at higher temp)

### Saturation Current vs. Temperature

Saturation current decreases at higher temperature (permeability decreases):

- At 25°C: Isat = 10A
- At 85°C: Isat ≈ 8A (loses 20%)
- At 125°C: Isat ≈ 6A (loses 40%)

**Design impact**: Must derate saturation current for hot operating conditions.

### DC Resistance vs. Temperature

Wire resistance increases with temperature:
- Copper: ~0.4% per °C
- At 85°C vs. 25°C: Resistance might be 24% higher
- Increases power loss and heat

## Frequency Effects

### Self-Resonant Frequency (SRF)

Every inductor becomes ineffective above its SRF due to parasitic capacitance:

- Small signal inductors: SRF might be 100 MHz+
- Power inductors: SRF might be 1–10 MHz
- Large inductors: SRF might be 100 kHz or less

**Practical implication**: Don't use an inductor above its SRF. It won't work as intended.

### Skin Effect

At very high frequencies, current flows only on the outer "skin" of wires:

- Increases effective wire resistance
- Reduces conductivity
- Makes inductor more lossy

Skin depth in copper at 1 MHz: ~66 micrometers. Wire thinner than this is affected.

### Core Saturation Behavior at Different Frequencies

Iron core saturation current is frequency-dependent:
- DC: Maximum current before saturation
- 60 Hz: Might be 90% of DC saturation
- 1 kHz: Might be 80% of DC saturation
- Higher frequency: Lower saturation current

## Parasitic Capacitance Effects

Every inductor has some parasitic capacitance between turns and leads.

This creates impedance effects:
- At resonance (SRF): Minimum impedance
- Below SRF: Inductive
- Above SRF: Capacitive

## Magnetic Coupling Between Inductors

If two inductors are physically close:
- Magnetic field from one affects the other
- **Mutual inductance** develops
- Can be helpful (transformers) or harmful (crosstalk)

**Professional design**: Keep inductors away from sensitive circuits or shield them to prevent coupling.

## Thermal Cycling

Repeated heating and cooling stresses inductors:
- Core material expands and contracts
- Solder joints can crack
- Wire-core interface degrades
- Accelerates aging and failure

## Humidity Effects

Moisture affects inductors:
- Absorbs into insulation
- Increases leakage between turns
- Can cause short circuits in extreme humidity
- Sealed inductors are more reliable

## AC Ripple vs. DC Magnetization

Many inductors have both DC bias current (main purpose) and AC ripple (signal):

- DC magnetizes the core
- AC ripple adds additional magnetization
- Combined: Total magnetization = DC + AC peak
- If total exceeds saturation, inductor saturates

**Design**: Account for both DC and AC when calculating saturation margin.

**Example**:
- Average DC current: 8A
- AC ripple: ±2A (peak to peak)
- Peak current: 8 + 2 = 10A
- Inductor Isat must be > 10A (with margin)

## Thermal Runaway in Inductors

Loss generates heat → increases resistance → more loss → more heat

**Thermally stable inductors**: Losses decrease with temperature (ferrite can show this)

**Thermally unstable inductors**: Losses increase with temperature (iron can show this)

This matters in power supplies: An unstable inductor might cause thermal runaway.

## Aging and Reliability

Unlike capacitors, inductors don't have a specific "lifetime" rating. But they do age:

- Core material properties degrade slowly
- Insulation can break down
- Solder joints can fatigue

**Typical reliability**: Tens of years in stable environment, shorter in thermal cycling.

## Key Takeaway

**Real inductors are affected by temperature, frequency, thermal cycling, and aging.**

Professional design accounts for:
- Temperature derating of saturation current
- Operating frequency below SRF
- Thermal management
- AC + DC combined magnetization
- Magnetic coupling to other components

Next: Common mistakes with inductors.
