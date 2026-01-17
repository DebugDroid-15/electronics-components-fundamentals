# Inductor Types: Designs and Trade-Offs

## Overview: Why Different Inductor Types?

All inductors store energy magnetically in coils, but they differ in:
- **Core material** (air, iron, ferrite, etc.)
- **Size** and physical form
- **Inductance value** achievable
- **Frequency range** of operation
- **Current rating** before saturation
- **Quality factor (Q)** and efficiency
- **Cost**
- **Frequency response**

Understanding inductor types is essential for practical design.

## Air Core Inductors

### Description
Coil of wire with no magnetic core material (empty space / air inside).

### Characteristics
- **Inductance**: Low inductance (requires many turns)
- **No saturation**: Can't saturate (air has low permeability)
- **Linear**: Inductance doesn't change with current
- **High Q**: Very good efficiency (low losses)
- **Large size**: Requires many turns to achieve significant inductance
- **High frequency**: Works well at RF frequencies
- **No core loss**: No losses from core material

### Typical Applications
- RF circuits (MHz, GHz ranges)
- High-frequency filters
- Precision circuits (no saturation)
- Antenna circuits

### Advantages
- Linear (inductance doesn't change with current)
- High Q factor (good efficiency)
- No saturation
- Works at extremely high frequencies

### Disadvantages
- Large for small inductance values
- Difficult to achieve large inductance
- Expensive (requires precise winding)
- Magnetic field is unshielded (can couple into nearby circuits, causing noise)

### When to Use
- High-frequency circuits
- When saturation must be avoided
- RF applications
- Precision tuning circuits

## Iron Core Inductors

### Description
Coil wound around an iron (ferromagnetic) core. Iron dramatically increases inductance.

### Characteristics
- **Inductance**: High inductance in small package (iron has high permeability ~10,000)
- **Saturation**: Can saturate at high currents (iron has limits)
- **Core loss**: Loss from magnetization/demagnetization cycles
- **Size**: Small for same inductance as air core
- **Frequency**: Works at lower frequencies (core losses increase at RF)
- **Current dependent**: Inductance decreases as current increases (nonlinear)

### Typical Applications
- Power supply inductors
- Audio frequency transformers
- Power transformers
- Any application needing large inductance at low/medium frequency

### Advantages
- Small size for large inductance
- High inductance achievable
- Efficient at low/medium frequencies
- Common and inexpensive

### Disadvantages
- **Saturation**: Limited by core saturation (current must be kept below saturation)
- **Nonlinear**: Inductance changes with applied current
- **Frequency limited**: Core losses increase dramatically at high frequencies
- **Temperature dependent**: Permeability changes with temperature

### Real-World Behavior
- As current increases, core magnetization increases
- Eventually core saturates (can't magnetize more)
- Beyond saturation, inductance drops sharply
- Circuit behavior changes dramatically (inductor is no longer effective)

This is why power supply inductors have current ratings—you must stay below saturation current.

## Ferrite Core Inductors

### Description
Coil wound around ferrite (ceramic magnetic material) core. Ferrite has moderate permeability (~100–1000) with lower core loss than iron.

### Characteristics
- **Inductance**: Moderate to high (less than iron, more than air)
- **Saturation**: Can saturate but typically at higher currents than iron
- **Core loss**: Low loss (better at high frequencies than iron)
- **Size**: Smaller than air core, larger than iron core
- **Frequency**: Works well from DC to RF range
- **Versatility**: Good balance of properties

### Typical Applications
- Switching power supplies (10 kHz–1 MHz)
- EMI filters
- RF circuits
- Broadband transformers
- High-frequency power inductors

### Advantages
- Good compromise between size and frequency response
- Lower core loss than iron (works well up to MHz)
- Higher saturation current than iron
- Moderately priced
- Good Q factor

### Disadvantages
- More expensive than iron
- Still limited by saturation
- Not as efficient as air core at very high frequencies

### Real-World Behavior
- Saturation occurs at higher currents than iron
- Frequency response extends higher than iron
- Core loss increases with frequency but more slowly than iron
- Most versatile for modern switching power supplies

## Toroidal Inductors

### Description
Inductor wound on toroidal (doughnut-shaped) core. Can use iron, ferrite, or other materials.

### Characteristics
- **Shielding**: Magnetic field contained within torus (minimal external field)
- **Coupling**: Minimal coupling to nearby circuits (no EMI generation)
- **Efficiency**: Efficient use of core space
- **Cost**: Usually more expensive (specialized winding)
- **Frequency**: Depends on core material

### Advantages
- Excellent shielding (field contained)
- Compact
- Minimal EMI radiation
- Professional-grade quality

### Disadvantages
- More expensive
- Difficult to wind manually
- Less common in consumer electronics

### When to Use
- When EMI must be minimized
- Noise-sensitive environments
- Professional audio/test equipment
- Shielded power supplies

## PCB Trace Inductors

### Description
Intentional (or parasitic) inductance from PCB traces or printed circuits.

### Characteristics
- **Parasitic**: Often unintentional (every trace has inductance!)
- **Tiny values**: Typically nanohenries to microhenries
- **Distributed**: Spread throughout circuit
- **Frequency dependent**: Effects prominent at high frequencies

### Practical Significance
- In high-speed digital circuits (GHz), parasitic inductance is critical
- Can cause ringing, reflections, impedance mismatches
- Professional designs must account for and minimize parasitic inductance

### When Relevant
- High-frequency digital (GHz)
- RF circuits
- Transmission line effects

## Comparison Table

| **Type** | **Inductance** | **Frequency** | **Saturation** | **Size** | **Cost** |
|----------|---|---|---|---|---|
| Air | Low | Very High (RF) | None | Large | High |
| Iron | Very High | Low–Med | Yes (low current) | Small | $ |
| Ferrite | High | Med–High | Yes (mod current) | Med | $$ |
| Toroidal | High | Med–High | Yes (material dependent) | Compact | $$$ |

## How to Choose an Inductor

1. **Determine inductance value** needed (from circuit design)
2. **Determine current** that will flow through it
3. **Determine frequency range** of operation
4. **Choose core type**:
   - **Air**: High frequency (RF/MHz)
   - **Iron**: Low frequency, high current needs (power supplies)
   - **Ferrite**: Switching power supplies, moderate frequency
   - **Toroidal**: When EMI must be minimized
5. **Verify saturation current** exceeds expected current by safety margin (typically 1.5–2×)
6. **Check frequency response** suitable for application
7. **Verify Q factor** acceptable (higher is better, means more efficient)
8. **Check availability** and cost

## Key Takeaway

**Different inductor types exist because different applications have different priorities.**

For learning:
- **Air core**: RF circuits, no saturation concerns
- **Iron core**: Large inductance, low frequency (power supplies)
- **Ferrite**: Switching power supplies, good frequency range
- **Toroidal**: Professional applications, minimal EMI

Most real circuits use ferrite or iron core inductors depending on frequency range.

Next: Understanding saturation and current limits.
