# Voltage and Temperature Effects on Capacitors

## How Voltage Affects Capacitance

This is a critical non-ideal effect: **the capacitance value actually changes with the applied voltage.**

### The Phenomenon

For certain capacitor types (especially ceramic), capacitance is **voltage dependent**:
- Applied voltage changes the dielectric properties
- Capacitance value decreases as voltage increases
- Effect is more pronounced at higher voltages

### Why This Happens

In ferroelectric materials (used in some ceramics):
- Electric field aligns molecular dipoles
- Higher voltage means stronger alignment
- This changes the effective dielectric constant
- Result: capacitance changes

### Practical Example

A ceramic capacitor rated 100 µF at 10V:
- At 1V: might measure 105 µF
- At 5V: might measure 100 µF (nominal)
- At 10V: might measure 95 µF
- At rated voltage: -5% change

For X7R ceramic (better stability): -15% change over full voltage range
For Z5U ceramic (cheaper, worse): -60% change or more

### Design Implications

If your circuit is designed for 100 µF and you only get 85 µF due to voltage dependence:
- Timing changes if it's an RC circuit
- Filter characteristics change
- Power supply ripple filtering might be inadequate

**Professional solution**: Either choose film capacitors (voltage-independent) or derate the expected capacitance value in calculations.

## How Temperature Affects Capacitance

Temperature is the **most significant environmental effect** on capacitors.

### Temperature Coefficient

Like resistors, capacitors have a **temperature coefficient** describing how capacitance changes with temperature:

$$\Delta C = C_0 \times (\text{TC} \times \Delta T)$$

Where:
- ΔC = change in capacitance
- C₀ = nominal capacitance
- TC = temperature coefficient (ppm/°C)
- ΔT = temperature change (°C)

### Ceramic Capacitors

Ceramic capacitors are labeled with **temperature characteristic codes** (e.g., X7R, Z5U, Y5V):

**X7R** (best for temperature stability):
- Temperature range: -55°C to +125°C
- Maximum change: ±15% over entire range
- Cost: Moderate
- Typical TC: ~0 ppm/°C (very stable)

**Z5U** (cheap, but temperature-dependent):
- Temperature range: +10°C to +85°C (narrower!)
- Maximum change: +22% to -56% (huge!)
- Cost: Cheapest
- Typical TC: Highly nonlinear

**Y5V** (moderate stability):
- Temperature range: -30°C to +85°C
- Maximum change: +22% to -82% (very nonlinear)
- Cost: Cheap

**Implication**: Cheap ceramics are very temperature-dependent. At 0°C, a Z5U capacitor might only be 50% of its rated value!

### Film Capacitors

Film capacitors are much more stable:
- Temperature coefficient: ±0.3% to ±0.5% (very low)
- Change over -55°C to +125°C: < 1%
- Linear change with temperature
- Much more predictable

### Aluminum Electrolytic Capacitors

Electrolytics are temperature-dependent:
- Capacitance decreases at lower temperatures
- At 0°C: might be 80% of nominal value
- At 85°C: might be 95% of nominal value
- Temperature coefficient: ~300–500 ppm/°C (nonlinear)

**Critical issue**: Leakage current increases dramatically at higher temperatures (doubles every 10°C roughly). A capacitor rated 1 mA at 85°C might leak 10 mA at 125°C.

## Practical Temperature Effects: An Example

**Scenario**: Power supply decoupling capacitor for digital circuit

**Design**: 100 µF electrolytic, rated at 85°C

**At different temperatures**:

| Temperature | Nominal | Change | Actual | Leakage |
|-------------|---------|--------|--------|---------|
| -20°C | 100 µF | -15% | 85 µF | 0.1 mA |
| +25°C | 100 µF | 0% | 100 µF | 0.3 mA |
| +85°C | 100 µF | +5% | 105 µF | 1 mA |
| +125°C | 100 µF | -10% | 90 µF | 5 mA |

At 125°C, the capacitor is both smaller and leaks much more. This can affect power supply stability.

**Solution**: Use a 220 µF capacitor instead (ensures 100 µF even at lowest temperature and accounts for aging).

## Heat Dissipation in Capacitors

Capacitors generate internal heat from:
1. **Leakage current**: Charge leaking through the dielectric dissipates power
2. **ESR losses**: Current flowing through ESR generates I²R heat
3. **Dielectric loss**: Material absorption dissipates RF energy

The heat generated is minimal in most applications but becomes significant in:
- High-frequency switching power supplies (ESR losses dominate)
- Circuits with large ripple current (AC superimposed on DC)
- High ambient temperature environments

## Thermal Cycling (Heating and Cooling)

Repeated temperature changes stress capacitors:
- Material expands and contracts
- Solder joints can crack
- Internal structure can develop microcracks
- Leakage current increases over time

This is why electronics in harsh environments (automotive, industrial) fail eventually—thermal cycling degrades components.

## Voltage and Temperature Interaction

**Important**: Effects combine negatively:
- High voltage + high temperature = worst case
- A capacitor rated for 85°C and 50V might only safely handle 40V at 85°C
- At higher temperature, voltage rating often decreases

This is why datasheets show **derating curves**: voltage rating vs. temperature.

Example derating:
- 50V at 25°C
- 50V at 85°C (no derating)
- 40V at 125°C (derated)
- 30V at 155°C (heavily derated)

**Design rule**: Use only 80% of rated voltage to maintain safety margin. If you need 50V capacity, choose a 63V capacitor.

## Long-Term Effects: Aging and Degradation

Even without any applied voltage, capacitors degrade over time due to:
- Chemical reactions in the dielectric
- Moisture absorption
- Migration of ions in electrolyte
- Thermal effects even at room temperature

### Typical Aging Rates

**Aluminum electrolytics**: Most affected
- Capacitance decreases ~1% per year (at room temperature)
- Leakage increases by similar amount
- After 10 years: 10% loss of capacitance (noticeable in precision circuits)
- After 20 years: 20% loss (significantly affects circuits)

**Film capacitors**: Very stable
- Aging < 0.1% per year
- Imperceptible over decades

**Ceramic capacitors**: Moderate
- Aging ~0.5% per year (typical)
- Depends on ceramic type

### Real Implication: Why Old Electronics Fail

Electronics from 10–20 years ago often experience capacitor failure:
- Electrolytic capacitors have aged significantly
- Capacitance has drifted, leakage increased
- Power supply stability decreases
- Circuits designed with tight tolerances now fail

This is why **capacitor plague** affected older computers—millions of failed electrolytic capacitors from specific manufacturers/batches.

## Environmental Conditions Beyond Temperature

### Humidity Effects

Moisture affects different capacitors differently:
- **Ceramic unpolarized**: Moderate effect (2–5% change with humidity)
- **Film plastic**: Minimal effect (< 0.1%)
- **Electrolytic**: Significant effect (evaporation/absorption cycles)
- **Sealed components**: Protected from humidity

In tropical or coastal environments (high humidity), cheap ceramics degrade faster.

### Altitude and Atmospheric Pressure

For most applications: negligible effect

For extreme applications (aerospace): significant consideration

### Vibration and Mechanical Stress

Repeated flexing of circuit board due to vibration:
- Can crack solder connections
- Can crack component leads
- Especially problematic in automotive applications
- Vibration testing is standard for harsh-environment designs

## Real-World Design Practices

Professional engineers account for temperature and voltage effects:

1. **Derate voltage**: Use capacitor at 80% of rated voltage maximum
2. **Account for temperature**: Assume lowest expected temperature when calculating capacitance requirements
3. **Add margin**: Choose capacitor 1.5–2× what you calculate you need
4. **Choose stable types**: Film for precision, high-quality ceramics (X7R) for general
5. **Test extremes**: Prototype testing at temperature extremes validates design
6. **Consider aging**: For long-term applications, calculate capacitance loss after 10–20 years

## Key Takeaway

**Voltage and temperature are the primary factors determining real capacitor behavior.** 

The nominal value printed on the capacitor is just one point in its operating envelope. Real designs must:
- Account for voltage dependence
- Plan for temperature changes
- Consider thermal interaction effects
- Verify designs work at temperature extremes
- Account for long-term aging

The difference between hobbyist and professional design is often this attention to environmental effects.

Next: Understanding leakage current and why capacitors lose charge over time.
