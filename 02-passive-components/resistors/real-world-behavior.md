# Real-World Resistor Behavior

## The Ideal Model vs. Reality

**Ideal model**: A resistor has a constant resistance value. Ohm's law applies perfectly.

**Real world**: Resistors are affected by temperature, frequency, manufacturing variation, aging, and voltage.

This section explains the non-ideal behaviors you'll encounter in actual circuits.

## Temperature Effects

### Resistance Variation with Temperature

Almost all resistors change resistance with temperature. This is quantified by **temperature coefficient of resistance (TCR)**, measured in ppm/°C (parts per million per degree Celsius).

Example calculation:
- Nominal resistance: 1kΩ
- TCR: ±100 ppm/°C
- Temperature change: +50°C
- Resistance change: 1kΩ × 100 ppm × 50 = 1000Ω × 0.0001 × 50 = 5Ω
- New resistance: 1kΩ ± 5Ω

**Carbon film resistors** (worst):
- TCR: ±500–1000 ppm/°C
- Temperature change of 50°C can change value by 2.5–5%

**Metal film resistors** (good):
- TCR: ±25–100 ppm/°C
- Temperature change of 50°C changes value by 0.125–0.5%

**Wirewound resistors** (moderate):
- TCR: ±50–200 ppm/°C
- Similar to metal film

### Temperature-Sensitive Applications

Precision circuits are affected significantly:

**Voltage divider example**:
- Two 10kΩ resistors divide 10V to 5V (exactly)
- Temperature rises 50°C
- If both are carbon film (worst case):
  - Each changes by 2.5%
  - One might increase, one might decrease
  - Worst case: 5% total error
  - 5V output now ranges 4.75V to 5.25V (unacceptable for many applications)

**Solution**: Use matched resistor pairs (same TCR, or better, use metal film with ±100 ppm/°C).

### Thermal Cycling

Repeated heating and cooling can:
- Cause resistor materials to expand and contract
- Create internal cracks in the resistive element
- Degrade performance permanently
- Eventually cause failure

This is why equipment in temperature-cycling environments (cars, outdoor gear) needs more robust components.

## Frequency Effects

### Parasitic Inductance and Capacitance

Real resistors are not purely resistive. They have:
- **Parasitic inductance**: From the leads and resistive element coil
- **Parasitic capacitance**: Between turns of the resistive coating and leads

At DC and low frequencies: These parasitic effects are negligible.

At high frequencies: These parasitic effects dominate.

### Wirewound Resistors at High Frequency

Wirewound resistors are most problematic because:
- The resistive element is literally a coil (inductor!)
- At high frequencies, inductive reactance takes over
- The resistor doesn't behave like a resistor anymore

Example:
- 100Ω wirewound resistor
- Frequency: 10 MHz
- Parasitic inductance: ~10 nH (typical)
- Inductive reactance at 10 MHz: XL = 2π × f × L = 2π × 10×10⁶ × 10×10⁻⁹ ≈ 628Ω
- **At 10 MHz, the inductive reactance (628Ω) dominates the resistance (100Ω)!**

### Film Resistors at High Frequency

Film resistors (carbon and metal):
- Less inductive because they're not coiled
- Better performance at high frequencies
- **Reason**: Film is deposited spirally around a rod, not wound as a coil

### When Frequency Effects Matter

- RF (radio frequency) circuits: High MHz to GHz
- Fast digital circuits: Switching edge rates create high frequencies
- Audio circuits: Less critical but can affect high-frequency response

### Resonance and Oscillation

Parasitic inductance and capacitance can form **LC resonant circuits**:
- At the resonant frequency, impedance spikes
- Can cause oscillation
- Can cause filtering effects

This is why real resistors in precision circuits are tested at multiple frequencies.

## Aging and Drift

### Long-Term Value Change

Resistors aren't perfectly stable forever:
- **Carbon film**: Drift of ±2–5% over 10 years (normal conditions)
- **Metal film**: Drift of ±0.5–1% over 10 years
- **Wirewound**: Generally very stable

Causes:
- Chemical reactions in the resistive material
- Moisture absorption (in non-sealed components)
- Mechanical stress from thermal cycling
- Electromigration at high temperatures

### Carbon Film Degradation

Carbon film resistors are most affected by:
- **Humidity**: Moisture absorption changes resistance
- **Temperature cycling**: Causes cracking and internal changes
- **Age**: Chemical degradation of resistive material

This is why carbon film resistors are disfavored in precision or long-term applications.

### Reliability Data

Typical failure rates (FIT: failures in time, per billion device hours):

| Type | Failure Rate |
|------|--------------|
| Metal film, 70°C | 0.1–0.5 FIT |
| Carbon film, 70°C | 1–5 FIT |
| Wirewound, 70°C | 0.1–1 FIT |

At 125°C: Rates increase by 10-100×

This means:
- A metal film resistor: ~1 failure per 20 billion hours (extremely reliable)
- A carbon film resistor: ~1 failure per 4 billion hours (still very reliable, but worse)

Professional equipment designers use FIT rates to predict mean time between failures (MTBF).

## Voltage Coefficient

Some resistors' resistance changes with applied voltage. This is called **voltage coefficient** and is usually small but can matter in high-voltage applications.

**Thin film resistors**: ~0.1 ppm/V (very stable)  
**Carbon film**: Can be 100+ ppm/V (voltage-dependent)

At 500V with carbon film resistor having 100 ppm/V:
- Change: 500V × 100 ppm = 5% change in resistance!

This is why high-voltage applications require quality resistors.

## Noise

Resistors generate **thermal noise** (Johnson noise) due to random thermal motion of electrons.

Higher resistance = more noise.

At 1kΩ: noise is ~4 nanovolt/√Hz (imperceptible in most circuits)  
At 1MΩ: noise is ~130 nanovolt/√Hz (can be problematic in sensitive applications)

**Carbon film resistors**: Slightly noisier than metal film
**Metal film resistors**: Lower noise, better for audio

In high-gain audio amplifiers, resistor noise can be audible if using very high values (10MΩ+).

## Moisture Effects

Many resistor types are affected by humidity:

**Sealed resistors**: Little moisture effect  
**Unsealed carbon film**: Significant moisture effect  
**Wirewound with epoxy coating**: Well sealed

In humid environments (coastal areas, tropical climates):
- Carbon film resistors can drift 2–3%
- Metal film with good coating: minimal effect
- Unsealed electrolytic components: catastrophic effect

This is why military and harsh-environment equipment uses sealed, conformal-coated components.

## Power Supply Noise

Resistors don't cause noise, but they interact with noise:
- A noisy voltage source connected across a resistor creates noise
- The resistor divides both the DC and the noise
- This is why **matched resistor pairs** are important in precision circuits (both resistors experience same noise)

## Tolerance Stack-Up

When multiple resistors are used (like voltage dividers), individual tolerances combine.

Example: Two resistors in voltage divider, each ±5%

Worst case for divider accuracy: **±10%** (not ±5%)

This is why precision designs:
- Use tighter individual tolerances
- Match resistor pairs with tight relative tolerance
- Add trimmer potentiometers for fine adjustment
- Test after assembly

## Practical Testing: Measuring Real Resistors

If you measure resistor values with a multimeter:
- Most resistors are within stated tolerance
- Some are at extremes of tolerance
- A few might exceed tolerance (rare, but happens)
- Values vary slightly with temperature of measurement

Professional quality control:
- Measures 100% of resistors in critical applications
- Tests at multiple temperatures
- Discards out-of-tolerance units

Hobbyists typically:
- Trust stated tolerance
- Measure a few if precision matters
- Accept that some variation is normal

## Key Takeaway

**Real resistors are affected by temperature, frequency, humidity, age, and component variations.** Understanding these effects is what separates hobbyist design from professional engineering.

For most circuits:
- Carbon film resistors work fine
- Temperature effects are minor
- Frequency effects don't matter

For precision, reliability, or harsh environments:
- Use metal film resistors
- Consider temperature coefficients
- Implement matched pairs
- Account for aging and drift
- Test designs across real-world conditions

Next: Common mistakes people make with resistors.
