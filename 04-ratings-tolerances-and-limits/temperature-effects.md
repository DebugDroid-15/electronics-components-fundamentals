# Temperature Effects: Universal Component Behavior

## Temperature is Everywhere in Real Electronics

Every component changes with temperature.

Temperature effects are not exceptions—they're the rule.

Professional designs **predict and manage** temperature-dependent behavior.

## Why Temperature Matters

### Heat Sources
1. **Ambient temperature**: Environmental, seasonal variation
2. **Self-heating**: Component power dissipation generates heat
3. **Neighboring components**: Heat from other parts
4. **Equipment operation**: Continuous duty, no cooling
5. **Industrial environments**: Ovens, equipment enclosures

### Typical Temperature Ranges
- **Consumer products**: 0–50°C ambient
- **Automotive**: -40–85°C ambient (worse in summer heat soak)
- **Industrial**: -40–85°C ambient
- **Military**: -55–125°C ambient (extreme)
- **Junction temperature**: Can be 30–80°C hotter than ambient

**Design consequence**: Cannot assume room temperature (25°C).

## Temperature Coefficients: How Components Change

### Resistors: Positive Temperature Coefficient

**Resistance increases with temperature**: R(T) = R₀[1 + α(T - T₀)]

Where:
- α = temperature coefficient (ppm/°C)
- Typical: 100–500 ppm/°C

**Practical example**: 1kΩ resistor with α = 200 ppm/°C
```
At 25°C: 1000Ω
At 75°C: 1000 × (1 + 200e-6 × 50) = 1010Ω (+1%)
At 125°C: 1000 × (1 + 200e-6 × 100) = 1020Ω (+2%)
```

**Impact**: Affects current, voltage division, time constants.

### Capacitors: Complex Temperature Coefficient

**Capacitance changes**: C(T) = C₀[1 + TC(T - T₀)]

Where TC = temperature coefficient (varies wildly by type)

| Type | TC | Behavior |
|------|----|----|
| Ceramic X7R | ±0.05%/°C | Stable (±15% over -20 to +80°C) |
| Ceramic Z5U | ±0.22%/°C | Unstable (±56% over -20 to +80°C) |
| Film (polyester) | 0.03% to 0.1%/°C | Good stability |
| Electrolytic | Complex | Capacitance & leakage vary |

**Example**: 10µF ceramic Z5U
```
At 25°C: 10µF (nominal)
At 0°C: 10µF × (1 - 0.22% × 25) = 9.45µF (-5.5%)
At 85°C: 10µF × (1 + 0.22% × 60) = 10.132µF (+1.3%)
```

**Impact**: Timing, filtering, resonant circuits affected.

### Transistors: Gain and Leakage

**BJT gain increases**: hFE(T) = hFE(T₀) × [1 + 0.5%/°C × ΔT]

Typical: hFE increases ~0.5% per degree Celsius.

**Example**: 2N3904 with hFE = 100 at 25°C
```
At 25°C: hFE = 100
At 75°C: hFE ≈ 100 × 1.005^50 ≈ 128 (+28%)
At 0°C: hFE ≈ 100 × 0.995^25 ≈ 78 (-22%)
```

**Base-emitter voltage decreases**: VBE ≈ -2 mV/°C

**Leakage increases**: ICE0 (reverse leakage) doubles every 25°C.

**MOSFET threshold voltage decreases**: Vth ≈ -2 to -5 mV/°C

**Impact**: Transistor biasing drifts, gain varies, leakage increases.

## Design Derating: Safety Margins

### What is Derating?

**Derating** = designing below component maximum ratings to ensure safety across temperature.

Example: Component rated 100A at 25°C
- Derated for 85°C operation: 60A maximum
- 40% reduction from maximum rating
- Ensures safe operation even at worst-case temperature

### Thermal Derating Curves

Typical component datasheet shows:
```
Maximum Current vs. Temperature

100A |●
     |  ●
 80A |    ●  ← Derating
     |      ●
 60A |        ●
     |         ●
     |________●___
        0    85   125°C
```

Maximum rating valid only at 25°C.
At higher temperature, rating decreases (derating curve).

### Derating Example: Power MOSFET

IRF510 MOSFET datasheet:
- Max ID at 25°C: 3.3A
- Max power at 25°C: 43W
- θja (thermal resistance): 62°C/W without heatsink

**At 85°C ambient (without heatsink)**:
- Max power available: 43W - (85-25)°C × 62°C/W = 39W derating not applied
- Actually: Junction stays ≤ 150°C (max)
- Tj = 85°C (ambient) + (P × 62°C/W)
- 150°C = 85 + P × 62 → P = 1.05W maximum
- 43W rating reduced to ~1W (massive derating)

**With heatsink** (θja = 5°C/W):
- 150°C = 85 + P × 5 → P = 13W
- Much better, but still 30% derating

## Real-World Temperature Effects

### Electrolytic Capacitor Aging Acceleration

Electrolytic capacitor life strongly temperature-dependent.

**Arrhenius equation** predicts life:
$$\text{Life}_{T} = \text{Life}_{ref} \times 2^{-(T-T_{ref})/10°C}$$

Example: Capacitor rated 10,000 hours at 85°C
```
At 55°C: 10,000 × 2^(-(55-85)/10) = 10,000 × 2^3 = 80,000 hours
At 85°C: 10,000 hours
At 105°C: 10,000 × 2^(-(105-85)/10) = 10,000 × 2^(-2) = 2,500 hours
```

**Implication**: Every 10°C increase halves capacitor life.
Operating at 105°C instead of 85°C → 4× faster degradation.

### Battery Performance

Battery capacity and power delivery temperature-dependent:

Cold battery (0°C):
- Capacity ≈ 80% of rated
- Internal resistance increases
- Voltage sag under load
- Device may not start

Hot battery (60°C):
- Capacity ≈ 90% of rated
- Self-discharge accelerated
- Chemical degradation faster
- Lifetime shortened

### System Behavior: Cascading Effects

As temperature increases:
1. Component values drift
2. Gain increases (transistors)
3. Leakage increases (exponential)
4. Thermal runaway possible
5. Component failure

**Thermal runaway example**:
- Power dissipation increases heat
- Component operating point shifts
- Leakage current increases (exponential)
- More heat generated
- Cycle repeats until failure

## Temperature-Compensated Design

### Compensation Strategies

**1. Negative feedback**
- Active feedback corrects for temperature drift
- Op-amp with temperature compensation
- Most robust approach

**2. Matched pairs**
- Two transistors of same type, same temperature
- Temperature effects track (cancel out)
- Ratio accuracy instead of absolute accuracy

**3. Thermal compensation network**
- Add temperature sensor
- Adjust circuit parameters based on temperature
- Software compensation possible with microcontroller

**4. Design margin**
- Over-specify component ratings
- Wider tolerance acceptance
- Accept performance variation
- Simplest approach

### Example: Precision Temperature Sensor

Thermistor measuring temperature:
- Thermistor resistance: R(T) = R₀ × e^(β(1/T - 1/T₀))
- Very temperature-sensitive (desired for sensor)
- But high-impedance signal noise-prone
- Solution: Op-amp with precision resistor network
- Compensation network cancels measurement errors

## Professional Temperature Testing

### Mandatory Testing

**Temperature sweep**: Operate circuit at multiple temperatures
- 0°C: Cold condition
- 25°C: Room temperature (nominal)
- 50°C: Warm condition
- 85°C: Hot condition
- Above 85°C if required by specification

**For each temperature**:
- Measure all critical parameters
- Verify operation within specification
- Verify safety (thermal, electrical)
- Document results

### Accelerated Life Testing

**High-temperature operation**: Run at 85°C or above for extended period
- Typical: 1000 hours at 85°C
- Equivalent to years of field operation
- Identifies early failures
- Validates component aging models

### Environmental Stress Screening

**Thermal cycling**: Repeated temperature changes
- -20°C to +85°C, 10+ cycles typical
- Stresses solder joints, component interfaces
- Identifies weak connections
- Simulates seasonal temperature variation

## Common Temperature Mistakes

### Mistake 1: Design at Room Temperature

"Circuit works at 25°C, so it's fine"

**Reality**:
- Field temperatures vary seasonally
- Component heating adds to ambient
- Prototype at 25°C succeeds, field at 60°C fails

**Fix**: Test at temperature extremes (0°C and 85°C minimum)

### Mistake 2: Using Component Ratings at 25°C

"Datasheet says 10A, so I can use 10A"

**Reality**: 10A rating only valid at 25°C.
At 85°C: Maximum current ~60% of rating (40% derating typical)

**Fix**: Derate components 30–50% at operating temperature

### Mistake 3: Ignoring Thermal Runaway

"Power component gets hot, but should be okay"

**Reality**: Leakage increases exponentially with temperature.
Heat increases leakage, which increases heat (positive feedback).
Catastrophic failure if not managed.

**Fix**: Thermal management mandatory for power components.

### Mistake 4: No Thermal Testing

"Looks good on the bench, release to production"

**Reality**: Bench is room temperature, field is hot/cold.
Failures discovered in field, expensive recalls.

**Fix**: Thermal chamber testing mandatory before release.

---

## Key Takeaway

**Temperature effects are universal and mandatory to address in design. Components change value and behavior with temperature. Professional designs derate components at worst-case temperature, test across temperature extremes, and include thermal management as part of the design, not an afterthought.**

