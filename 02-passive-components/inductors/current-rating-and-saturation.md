# Current Rating and Saturation

## What Is Saturation?

**Saturation** is unique to inductors with magnetic cores. It occurs when the magnetic core can no longer accept more magnetization, regardless of how much current you apply.

### The Phenomenon

When current flows through a core inductor:
1. Current creates magnetic field
2. Magnetic field magnetizes the core material
3. Core's magnetization increases with current
4. Eventually, core reaches maximum magnetization (saturation)
5. Beyond this point, increasing current doesn't increase magnetization
6. Inductor loses its inductance (becomes just wire resistance)

## Why Saturation Matters

### What Happens at Saturation

**Before saturation** (normal operation):
- L = L₀ (inductance is constant)
- Z = 2πfL (impedance increases with frequency, inductor works as designed)

**At saturation**:
- Inductance drops sharply (L drops to 10% of original, or less)
- Impedance plummets
- Circuit behavior changes completely

**Practical effect**: Inductor stops working. Whatever it was supposed to do (filtering, impedance matching, energy transfer) fails.

### In Power Supplies (Common Application)

A switching power supply uses an inductor to:
- Store energy during on-time
- Release energy during off-time
- Regulate output voltage

If the inductor saturates:
- Energy transfer fails
- Output voltage collapses
- Power supply fails

### In Transformers (Coupled Inductors)

A transformer with saturated core:
- No longer transfers power efficiently
- Draws excessive current (limited only by resistance)
- Can overheat and fail
- Can damage power supply

Transformer saturation is a common failure mode.

## Saturation Current: The Limit

Every inductor with a magnetic core has a **saturation current**—the maximum current before saturation begins.

This is specified in datasheets as:
- **Isat**: Saturation current (amperes)
- Sometimes given at different temperatures (saturation decreases at higher temperature)

### Example Specifications

- Small power inductor: Isat = 0.5A
- Medium power inductor: Isat = 5A
- Large power inductor: Isat = 50A+

### Why Saturation Current Decreases with Temperature

Magnetic core material's permeability decreases at higher temperature:
- Permeability drops → magnetization decreases
- Can't reach same magnetization at high temperature
- Saturation current is lower

Example:
- Iron core inductor: Isat = 10A at 25°C
- Same inductor: Isat = 8A at 85°C

Temperature derating is similar to capacitor voltage derating—a design margin.

## Saturation vs. DC Resistance

Don't confuse saturation with DC resistance:

**DC Resistance**:
- Inherent resistance of the wire coil
- Causes voltage drop: Vdrop = I × Rdc
- Occurs at any current level
- Energy dissipated as heat

**Saturation**:
- Loss of inductance at high currents
- Impedance changes
- Fundamentally different than resistance
- Circuit behavior changes

Both can occur together, making saturation analysis complex.

## Design Rule: Current Derating

Professional designers don't design to saturation current. Instead, they derate:

**Rule of thumb**: Use inductor at 50–70% of saturation current maximum.

Example:
- Inductor Isat = 10A
- Design maximum current: 5–7A
- Margin: 3–5A (30–50% safety buffer)

Why?
- Saturation is a sharp cliff (inductance drops suddenly)
- Operating near edge is risky
- Temperature effects reduce saturation current
- Safety margin prevents field failures

## Avoiding Saturation in Practice

### 1. Choose Large Enough Inductor
- Current requirements → need inductor with higher Isat
- Cost trade-off: Higher Isat inductors usually cost more

### 2. Use Air Core
- Air can't saturate (μ = 1, no core material to saturate)
- But air core means large size and low inductance

### 3. Design to Avoid Peak Current
- In some circuits (like switching power supplies), you can design to limit peak current
- Reduces inductor stress
- Improves efficiency

### 4. Multiple Inductors in Parallel
- Current divides among them
- Each handles less current
- Reduces saturation risk

**Example**: One 10A inductor vs. two 5A inductors in parallel. Two in parallel handle same total current but each saturates at higher current.

### 5. Account for Temperature
- Design for worst-case temperature
- If application reaches 85°C, use Isat at 85°C, not 25°C
- May require choosing larger inductor

## Soft vs. Hard Saturation

Not all cores saturate the same way:

**Hard saturation** (iron cores):
- Inductance drops sharply at saturation current
- Clear cliff in performance
- Easy to design against (stay below limit)

**Soft saturation** (some ferrites):
- Inductance decreases gradually with current
- No sharp cliff
- More forgiving, but still must respect limits

Different core materials and designs have different saturation characteristics.

## Measuring and Testing Saturation

If you need to verify saturation characteristics:

**DC test**:
- Apply increasing current, measure inductance with LCR meter at each level
- See where inductance starts to drop
- Graph the curve

**AC test**:
- Apply AC current at fixed frequency, measure impedance
- Increasing current decreases impedance
- Saturation shows as sharp impedance drop

Modern inductors often include saturation test data in datasheets showing L vs. I curves.

## Real-World Saturation Stories

### Power Supply Failure
- Switched power supply uses inductor
- Design changes increase peak current 10%
- Inductor reaches saturation
- Power supply output voltage collapses
- Device fails, months after product release
- Investigation: "Why is inductor inductance half of datasheet value?"
- Answer: Saturation (not accounted for in design)

### Transformer Blackout
- Step-down transformer rated 10A
- Installation draws 11A sustained (design error)
- Transformer partially saturates
- Draws excessive current from mains (protection trip)
- Building loses power
- Investigation: "Why did transformer fail?"
- Answer: Design overloaded inductor into saturation

## Key Takeaway

**Saturation is the primary failure mode for magnetic core inductors.** Professional design:
1. Identifies maximum current in application
2. Chooses inductor with Isat significantly higher (1.5–2× margin)
3. Accounts for temperature effects (Isat decreases at higher temp)
4. Verifies design with worst-case analysis
5. Tests prototypes at maximum expected current and temperature

Saturation is why inductor current rating matters—more than any other consideration.

Next: Understanding inductor losses and quality factor.
