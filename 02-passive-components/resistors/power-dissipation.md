# Power Dissipation and Thermal Management

## What Is Power Dissipation?

When current flows through a resistor, electrical energy is converted to **heat**. This is called power dissipation.

The relationship is:

$$P = I^2 \times R$$

Or equivalently:

$$P = V \times I$$

Or:

$$P = \frac{V^2}{R}$$

All three are the same; use whichever is most convenient for your situation.

## The Physics: Why Resistors Get Hot

Electrons moving through a resistor collide with atoms in the material. Each collision:
1. Slows the electron
2. Transfers energy to the atom
3. Causes the atom to vibrate
4. Vibrating atoms is what we perceive as heat

The more collisions (higher resistance), and the more electrons (more current), the more heat generated.

## Calculating Power Dissipation

### Example 1: LED Current Limiting Resistor

Setup:
- 5V power supply
- 2V LED forward voltage
- 20mA target current
- Resistor value: 150Ω

Power dissipated in resistor:
$$P = (5V - 2V) \times 0.02A = 3V \times 0.02A = 0.06W = 60mW$$

Or using I² × R:
$$P = (0.02A)^2 \times 150Ω = 0.06W = 60mW$$

**Conclusion**: This resistor dissipates 60 milliwatts. Choose at least a 1/4W (250mW) resistor.

### Example 2: Load Resistor on Power Supply

Setup:
- 12V power supply
- Load resistor: 24Ω
- Expected current: 12V / 24Ω = 0.5A

Power dissipated:
$$P = 12V \times 0.5A = 6W$$

Or:
$$P = (0.5A)^2 \times 24Ω = 6W$$

**Conclusion**: This resistor dissipates 6 watts. You need a substantial resistor (at least 10W rating) to handle this safely.

## Power Rating vs. Calculated Power

**Critical design principle**: Never choose a resistor rated exactly for calculated power.

### Why?

1. **Thermal Runaway**: As a resistor heats up, its resistance increases (in most cases). This increases power dissipation further, causing even more heating. The resistor can fail even if initially within rating.

2. **Resistor Aging**: Resistors degrade over time, especially when operating near their limits. A 0.25W resistor rated at 250mW might only safely dissipate 200mW after 5 years.

3. **Ambient Temperature**: Resistor ratings assume certain ambient conditions. If your resistor is in a hot enclosure or direct sunlight, it experiences higher temperature, reducing safe dissipation.

4. **Safety Margin**: Engineering requires margin. Using a component exactly at its limit is asking for failure.

### Design Rules

**Conservative approach (Recommended)**:
- Calculate power dissipation: P_calc
- Choose resistor rating: P_rating ≥ 3 × P_calc

**Moderate approach**:
- Choose resistor rating: P_rating ≥ 2 × P_calc

**Aggressive approach** (not recommended):
- Choose resistor rating: P_rating ≥ 1.5 × P_calc

**Example**:
- Your calculation: 0.3W
- Conservative: Choose 1W resistor (3.3× margin)
- Moderate: Choose 1W resistor (3.3× margin)
- Aggressive: Choose 0.5W resistor (1.7× margin)

The conservative approach adds $0.05 in component cost but dramatically improves reliability.

## Practical Heat Management

### Physical Cooling

In high-power applications, resistors must dissipate heat to the surroundings.

Factors affecting heat dissipation:
1. **Surface area**: Larger resistors dissipate heat better (more surface to air)
2. **Air flow**: Forced air cooling (fans) improves heat removal
3. **Mounting**: Resistors mounted on a PCB can use the board as a heat sink
4. **Spacing**: Resistors too close together heat each other

### Derating at High Temperature

As the resistor gets hotter, its safe power dissipation decreases.

Example wirewound resistor specification:
- Rating: 10W at 70°C
- Derating: 0.02W per °C above 70°C

At 100°C: 10W - (30°C × 0.02W/°C) = 10W - 0.6W = 9.4W safe

At 130°C: 10W - (60°C × 0.02W/°C) = 10W - 1.2W = 8.8W safe

Above 155°C (maximum temperature): Rating is zero. Component is out of spec.

### Series Thermal Path

Heat flows from the resistor through:
1. **Resistor element** → Connection leads
2. **Leads** → Mounting point (PCB pads or connector)
3. **PCB or mounting** → Air
4. **Air** → Surroundings (or cooling system)

Each interface has **thermal resistance**. Designers minimize total thermal resistance by:
- Using thicker wires or leads
- Using larger PCB pads
- Increasing air flow
- Using thermal paste or grease
- Using heat sinks

## Sensing Heat: Temperature Rise in Real Circuits

You can't see heat, but you can feel it.

**Important reality**: A properly operating resistor might be hot to touch!

- **Comfortable to touch**: < 50°C
- **Warm**: 50–70°C
- **Too hot to hold**: > 70°C

A 1W resistor at 1W dissipation will be quite hot, but operating normally.

A 0.25W resistor being used for 0.5W will be dangerously hot and failing.

**Rule of thumb**: If a resistor is hot enough to hurt when you touch it, check your design!

## Power Dissipation in Different Resistor Types

### Carbon Film
- Typical ratings: 1/4W, 1/2W, 1W
- Limited by small size
- Gets hot quickly with high power

### Metal Film
- Typical ratings: 1/4W, 1/2W, 1W
- Similar to carbon in small form factor
- Better thermal characteristics (lower TCR means less heating from resistance change)

### Wirewound
- Typical ratings: 5W to 500W+
- Designed for high power dissipation
- Metal construction provides excellent heat sinking
- Larger physical size allows better air circulation

## Power Dissipation in Special Cases

### Resistor Networks
When many resistors are on the same chip (integrated resistor arrays):
- Each resistor has individual power rating
- But thermal interactions between resistors matter
- Total power dissipation on chip is more limited than sum of individual ratings
- Heat from one resistor affects others

### SMD (Surface Mount Device) Resistors
- Very small, but used in high-volume production
- Power dissipation very limited (typical: 0.1W or less)
- Thermal management critical at board level
- PCB copper acts as heat sink

## Real-World Example: Power Supply Protection Resistor

**Scenario**: Power supply with 5V output can provide 3A maximum. A safety resistor limits current in case of short circuit.

**Design**:
- Desired max current: 2.5A (slightly less than supply limit)
- Maximum voltage drop when shorted: 5V (all supply voltage)
- Required resistance: R = V / I = 5V / 2.5A = 2Ω
- Power dissipation in short: P = 5V × 2.5A = 12.5W

**Reality**:
- A standard 2Ω resistor of small size can't handle 12.5W
- Solution: Use a 25W or 50W wirewound resistor
- This adds cost and size, but is necessary
- Resistor acts as a fuse, limiting damage during fault

This is why circuit protection isn't just about understanding components—it's about understanding power dissipation.

## Thermal Runaway (Advanced Concept)

**Thermal runaway** is a cascade failure mechanism:

1. Resistor dissipates power → gets hot
2. Resistance increases with temperature → more power dissipated
3. More power → hotter
4. Cycle repeats until resistor fails

This is especially bad with carbon film resistors (high temperature coefficient).

**Prevention**:
- Choose metal film resistors (lower TCR)
- Design with adequate margin
- Ensure good heat dissipation
- Never operate near maximum temperature

## Key Takeaway

**Power dissipation is the primary cause of resistor failure.** Professional designers:
1. Calculate exact power requirements
2. Choose resistor with 2-3× safety margin
3. Verify ambient temperature won't cause derating below requirements
4. Ensure adequate heat dissipation path
5. Test actual circuit to verify temperatures

The difference between hobbyist and professional electronics is often just this: understanding and respecting power dissipation.

Next: Understanding real-world resistor behavior and non-ideal effects.
