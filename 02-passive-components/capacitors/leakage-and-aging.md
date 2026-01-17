# Leakage and Aging: Why Capacitors Degrade

## The Core Problem: Real Capacitors Aren't Perfect

**Ideal model**: A charged capacitor retains its charge indefinitely.

**Real world**: All capacitors lose charge over time, even when disconnected. They also degrade with age and use.

This section explains why.

## Leakage Current: What It Is

**Leakage current** is the small current that continuously flows through the dielectric of a capacitor, even when no external circuit is connected.

This current causes charge to slowly drain from the capacitor:

$$I_{leak} = \frac{V}{R_{leak}}$$

Where:
- Ileak = leakage current
- V = applied voltage
- Rleak = leakage resistance (often gigaohms, but not infinite)

### The Capacitor Self-Discharge Time

A charged capacitor will self-discharge through its leakage resistance. The time for the charge to drop to 37% of initial value is:

$$\tau_{leak} = R_{leak} \times C$$

**Example**: 
- Capacitance: 10 µF
- Leakage resistance: 1 GΩ (1,000,000,000Ω)
- Self-discharge time constant: 10 × 10⁻⁶ × 10⁹ = 10,000 seconds ≈ 2.8 hours

This charged capacitor will be 37% discharged after 2.8 hours with no external circuit drawing current.

## Leakage Current by Capacitor Type

Different technologies have vastly different leakage characteristics:

### Ceramic Capacitors
- **Leakage**: High (poorest performers)
- **Typical values**: 10–100 nanoamps (10–100 µA per joule of energy stored)
- **Temperature dependent**: Doubles every 10–15°C
- **Problem**: Leakage is significant at high temperature

**Example**: 10 µF ceramic at room temperature might leak 10 nanoamps. At 85°C, it leaks 100+ nanoamps. At 125°C, maybe 1 microampere.

### Film Capacitors
- **Leakage**: Excellent (best performers)
- **Typical values**: 0.01–1 nanoamps
- **Temperature dependent**: Much less affected by temperature
- **Advantage**: Retains charge for hours or days

**Example**: 10 µF film capacitor might leak 0.1 nanoamp at room temperature and only 1 nanoamp at 85°C. Stays charged for days.

### Aluminum Electrolytic Capacitors
- **Leakage**: Moderate to high
- **Typical values**: 0.1–10 microamps (at rated voltage and temperature)
- **Temperature dependent**: Heavily dependent on temperature
- **Problem**: At high temperature, leakage becomes significant

**Example**: 100 µF electrolytic at 85°C, rated voltage: 1 mA leakage. At 125°C: 5 mA leakage. At room temperature: 0.1 mA.

### Tantalum Capacitors
- **Leakage**: Very good
- **Typical values**: 0.1–1 microamp (at rated voltage)
- **Temperature dependent**: Moderate
- **Advantage**: Much better than aluminum electrolytics

## Why Leakage Exists: The Physics

The dielectric material is supposed to be a perfect insulator, but it's not:

1. **Material imperfections**: No material is a perfect insulator
2. **Ionic conduction**: Ions in the material slowly move through it (faster when hot)
3. **Surface leakage**: Along the surface of the component, moisture allows conduction
4. **Bulk leakage**: Through the bulk material

At higher temperatures:
- Thermal energy increases ion mobility
- Leakage current increases exponentially (roughly doubling every 10°C)
- This is why hot capacitors leak much more than cold ones

## Real-World Impact of Leakage

### Power Supply Hold-Up Time

When power is removed from a circuit, energy stored in large capacitors can keep circuits running briefly. This is "hold-up time."

**With leakage:**
- Capacitor voltage decays over time
- Leakage determines how long power is maintained
- Important for graceful shutdown of systems

**Example**: Computer needs 1 second to shut down cleanly. If capacitor discharges too fast due to leakage (or other load), shutdown might be interrupted.

### Sensor Circuits

If a capacitor is charging a sensor or measurement circuit:
- Leakage causes measurement error
- Error increases over time
- Error increases with temperature

**Example**: Precision voltage measurement circuit using 1 µF capacitor. If capacitor leaks 1 nanoamp at room temperature, but 10 nanoamps at 85°C, the measurement error changes with temperature.

### Charge Pumps (Converting DC to Higher Voltage)

Some circuits use capacitors to generate higher voltage from lower voltage:
- Leakage reduces efficiency
- Leakage limits how much voltage can be generated
- High-leakage capacitors (like cheap ceramic) don't work well

## Aging: Gradual Degradation Over Time

Beyond leakage, capacitors physically degrade with age, even if they're not used.

### Capacitance Drift

Capacitance value changes with age:
- **Aluminum electrolytics**: Capacitance decreases (water loss from electrolyte)
- **Ceramics**: Varies by type, generally decreases slightly
- **Film**: Very stable, minimal change

**Typical rates**:
- Electrolytics: -1% per year at room temperature (faster at higher temperature)
- Ceramics: -0.5% per year
- Film: -0.01% per year

After 10 years:
- Electrolytic: -10% capacitance
- Ceramic: -5% capacitance
- Film: -0.1% capacitance

### Leakage Current Increase

Over time, leakage current increases due to material degradation.

**Aluminum electrolytics**: Most affected
- Initial leakage: 0.1–1 mA
- After 5 years: Might increase 20–30%
- After 10 years: Might double or triple
- Causes power supply heating

**Ceramics**: Moderate increase
**Film**: Minimal increase

### Electrolyte Drying (Electrolytics Only)

Aluminum electrolytic capacitors contain a wet electrolyte. Over decades:
- Water in electrolyte gradually evaporates
- Even in sealed components, tiny amounts leak out
- Evaporation rate increases with temperature and age
- Eventually, electrolyte becomes too dry to function

**Failure mode**: After 20–30 years in hot environments, electrolytics often fail due to dry electrolyte.

This explains why 1980s–1990s electronics develop capacitor failures now (2020s).

## Thermal Cycling Acceleration

Repeated heating and cooling (thermal cycling) dramatically accelerates aging:

1. **Material expands and contracts** with each cycle
2. **Internal structure stresses** accumulate
3. **Cracks develop** in solder joints or material
4. **Moisture penetrates** through cracks
5. **Degradation accelerates**

An electrolytic capacitor at constant 85°C might last 5000 hours.  
The same capacitor cycling -40°C to +85°C might last 500 hours (10× worse!).

This is why automotive and aerospace components have shorter rated lifetimes than "room temperature" ratings would suggest.

## Environmental Factors Accelerating Aging

### Humidity
- Moisture penetrates unsealed components
- Increases leakage current
- Accelerates corrosion
- Especially problematic in tropical environments

### Mechanical Vibration
- Stresses component leads
- Can cause solder joint cracking
- Creates paths for moisture ingress
- Automotive and aerospace: significant concern

### Electrical Stress
- High ripple current increases heating
- Increases leakage
- Causes electrolyte decomposition in electrolytics
- Accelerates aging dramatically

## Reliability Life Prediction

Manufacturers provide **reliability ratings** in terms of:
- **Lifetime hours** (at specific temperature and conditions)
- **Expected failure rate** (FIT: Failures In Time, per billion hours)

**Example specifications**:
- Electrolytic: 10,000 hours at 85°C (degrades exponentially at higher temp)
- Film: No specified lifetime (indefinite at normal conditions)
- Ceramic: No specified lifetime (generally reliable)

The **life equation** for electrolytics:
$$L_1 = L_2 \times 2^{\frac{T_2 - T_1}{10}}$$

Where:
- L₁ = life at temperature T₁
- L₂ = life at temperature T₂
- Doubling period: 10°C (for electrolytics)

**Example**:
- Rated: 5000 hours at 85°C
- At 95°C: 5000 × 2^((95-85)/10) = 5000 × 2 = 10,000 hours (doubled!)
- At 75°C: 5000 × 2^((75-85)/10) = 5000 × 0.5 = 2,500 hours (halved)

This shows why cooler operation dramatically extends capacitor life.

## Design Practices for Long Life

Professional designers extend capacitor life by:

1. **Thermal management**: Keep capacitors as cool as possible
   - Proper ventilation
   - Thermal design for power supply components
   - Using capacitors away from heat sources

2. **Derating**: Use capacitors at significantly less than rated voltage/current
   - Rated at 85°C, but design for 65°C operation
   - Rated at 50V, but use at 40V maximum

3. **Redundancy**: Use more capacitance than needed
   - Ensures circuit works even as capacitors age
   - Better reliability

4. **Capacitor selection**: Match application to type
   - Use quality electrolytics (long-life rating)
   - Use film for precision applications
   - Avoid cheap ceramics in critical paths

5. **Testing**: Validate designs with accelerated aging
   - Thermal cycling tests
   - Humidity tests
   - Electrical stress tests

## Key Takeaway

**Real capacitors leak charge continuously and degrade over time.** All real applications must account for:

- Immediate leakage (affects circuit operation, especially at temperature)
- Long-term aging (capacitor values drift, leakage increases)
- Environmental stress (temperature cycling, humidity, vibration)
- Application-specific needs (power supply requirements, precision needs)

The difference between a design that works initially and one that works for 10 years is usually attention to these aging and leakage effects.

Next: Understanding parasitic effects and high-frequency behavior.
