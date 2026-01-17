# Resistor Types: Why Different Resistors Exist

## Overview: Many Resistors, One Function

All resistors do the same basic job: oppose current flow. But they differ in:
- **Construction materials**
- **Power rating**
- **Tolerance**
- **Temperature stability**
- **Frequency response**
- **Cost**
- **Size**
- **Reliability**

This section explains the common types and why you'd choose one over another.

## Carbon Film Resistors

### Description
Thin film of carbon deposited on a ceramic rod. Leads are attached to the ends.

### Characteristics
- Very cheap
- Small size
- ±5% or ±10% tolerance typical
- Moderate temperature coefficient
- Low to moderate power ratings (typically 1/4W, 1/2W, 1W)

### Typical Specifications
- Resistance range: 10Ω to 10MΩ
- Temperature range: -55°C to +155°C
- Temperature coefficient: ±500 ppm/°C (parts per million per degree)

### When to Use
- General-purpose applications
- Hobby projects
- Non-critical circuits
- When cost is primary concern
- Prototyping

### When NOT to Use
- Precision applications (±5% isn't good enough)
- High-power applications
- High-temperature environments
- Very high-frequency circuits

### Real-World Behavior
- Resistance changes with temperature
- Resistance changes with humidity
- Colored bands can fade, making value hard to read
- Can burn if power rating exceeded
- Reliable for most non-critical uses

## Metal Film Resistors

### Description
Very thin film of metal alloy deposited on a ceramic substrate. Superior to carbon film.

### Characteristics
- Better tolerance: ±0.1% to ±1% (vs. ±5% for carbon)
- Lower temperature coefficient: ±25 to ±100 ppm/°C
- Better frequency response
- Low noise
- Slightly more expensive than carbon film
- Small size, available in various power ratings

### Typical Specifications
- Resistance range: 1Ω to 10MΩ
- Temperature range: -55°C to +155°C or wider
- Temperature coefficient: ±50 ppm/°C (excellent stability)

### When to Use
- Precision circuits (voltage dividers, measurement systems)
- Audio circuits (low noise)
- When temperature stability matters
- When ±5% tolerance is insufficient
- Modern designs (becoming standard)

### When NOT to Use
- Extreme high power (use wirewound instead)
- When cost is critical and tolerance isn't important

### Real-World Behavior
- Very stable across temperature
- Excellent frequency response up to MHz range
- Less susceptible to humidity than carbon
- More reliable long-term
- Bands are printed, not colored, so they don't fade

## Wirewound Resistors

### Description
Resistive wire wound around a ceramic or fiberglass core, coated with protective material.

### Characteristics
- Very high power ratings (5W, 10W, 25W, 50W or more)
- Very low resistance values possible (often 0.1Ω to 100kΩ)
- Good tolerance (±1% to ±5%)
- Excellent frequency stability
- **Major drawback**: Inductance due to wire coils

### Typical Specifications
- Power range: 5W to 500W+
- Temperature range: -55°C to +155°C
- Temperature coefficient: ±50 to ±200 ppm/°C

### When to Use
- High-power dissipation requirements
- Power supply current limiting
- Load resistors in test equipment
- Audio amplifier loads
- Precision applications needing low values

### When NOT to Use
- High-frequency circuits (inductance causes problems)
- When size is limited
- When cost is critical
- Where parasitic inductance must be minimized

### Real-World Behavior
- Acts partially like an inductor at high frequencies
- Can have resonant effects with capacitors
- Reliable and stable
- Excellent for thermals (metal construction dissipates heat better)

## Thick Film and Thin Film Resistors

### Description
Resistive material printed onto ceramic substrate. Used mostly in integrated circuits and hybrid circuits.

### When Encountered
- Built into chips
- Integrated circuits
- Module-level designs
- Industrial automation

### Characteristics
- Usually high precision
- Excellent temperature stability
- Very small size
- Cost-effective in volume

**Note**: You won't usually select these individually—they come built into components.

## Specialty Resistors

### Thermistors (Temperature-Dependent Resistors)
- Resistance changes dramatically with temperature
- Used for temperature sensing
- Not for current limiting or dividing

### Photoresistors (Light-Dependent Resistors)
- Resistance changes with light intensity
- Used for light detection
- Specialized application

### Varistors (Voltage-Dependent Resistors)
- Resistance changes dramatically when voltage exceeds a threshold
- Used for surge protection
- Specialized application

### Potentiometers (Variable Resistors)
- Resistance can be adjusted by turning a knob
- Used for volume controls, brightness adjustment
- Three terminals instead of two

## Practical Comparison Table

| **Type** | **Tolerance** | **Power Rating** | **Cost** | **Stability** | **Use Case** |
|----------|---------------|-----------------|----------|---------------|------------|
| Carbon Film | ±5–10% | 1/4–2W | $ | Fair | Hobby, non-critical |
| Metal Film | ±0.5–1% | 1/4–1W | $$ | Excellent | Precision circuits |
| Wirewound | ±1–5% | 5W–500W+ | $$$ | Good | High power |
| Thick Film | ±0.1–1% | Low | $ | Excellent | Integrated |

## How to Choose a Resistor

When designing a circuit:

1. **Determine the resistance value needed** using Ohm's law or voltage divider equations
2. **Calculate power dissipation** using P = I² × R or P = V × I
3. **Choose power rating**: Pick a rating at least 2× the calculated power (for safety margin)
4. **Choose tolerance** based on accuracy needs:
   - Non-critical circuits: ±5% or ±10% is fine
   - Precision: ±1% or better
   - Audio or measurement: ±0.5% or ±1%
5. **Check frequency considerations**:
   - Low frequency (<1 MHz): Any type works
   - High frequency: Avoid wirewound; use metal film
6. **Check temperature range** of your application and verify resistor specs cover it

## Real-World Selection Example

**Task**: Design an LED circuit with 5V supply, 2V LED forward voltage, 20mA target current

**Step 1**: Calculate resistance  
R = (5V - 2V) / 20mA = 150Ω

**Step 2**: Calculate power  
P = I² × R = (0.02A)² × 150Ω = 0.06W = 60mW

**Step 3**: Choose power rating  
Need 60mW, so pick ½W (500mW) resistor for safety

**Step 4**: Choose tolerance  
LEDs brightness varies slightly with current variation, so ±5% is acceptable

**Step 5**: Check frequency  
DC circuit, so frequency isn't a concern

**Result**: Use a ½W, 150Ω, ±5% carbon film or metal film resistor

Simple! But these decisions matter for reliability.

## Key Takeaway

**Different resistor types exist because different applications have different needs.** 

For learning purposes:
- **Carbon film**: Cheap, common, acceptable tolerance
- **Metal film**: Better stability, lower noise, precision
- **Wirewound**: High power dissipation
- **Specialty**: Temperature/light sensing, protection

Most hobbyist and learning circuits use **metal film resistors** today because they're affordable, reliable, and have good tolerance.

Next: How to read resistor values and understand their specifications.
