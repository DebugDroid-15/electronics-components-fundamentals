# Resistor Ratings and Tolerances

## What Are Ratings?

Every component comes with a **datasheet** that specifies its electrical and physical properties under defined conditions.

For resistors, the key ratings are:
- **Nominal resistance value** (the marked value)
- **Tolerance** (how much actual value can vary from nominal)
- **Power rating** (maximum power it can safely dissipate)
- **Temperature coefficient** (how much it changes with temperature)
- **Operating temperature range** (where it's guaranteed to work)
- **Maximum voltage** (some resistors have voltage limits)

Understanding these specifications is essential to using resistors reliably.

## Nominal Resistance Value

The **nominal value** is what's printed or color-coded on the resistor.

Examples:
- 1kΩ (one kilohm)
- 47Ω (forty-seven ohms)
- 2.2MΩ (two point two megaohms)

### Resistor Prefix Shorthand

| Prefix | Meaning | Example |
|--------|---------|---------|
| Ω or R | Ohms (base unit) | 47Ω |
| k | Kilo (thousand) | 1kΩ = 1,000Ω |
| M | Mega (million) | 1MΩ = 1,000,000Ω |
| G | Giga (billion) | Rare in resistors |

**Important**: Sometimes the letter substitutes for the decimal point:
- 4k7 means 4.7kΩ
- 1k5 means 1.5kΩ
- 2M2 means 2.2MΩ

This notation prevents decimal points from being misread in printing.

## Tolerance: The Actual Value Range

**Tolerance** specifies how much the actual resistance can differ from the nominal value.

### What Tolerance Means

A resistor marked **1kΩ ±5%** means:
- Nominal value: 1000Ω
- Maximum: 1000 + (1000 × 0.05) = 1050Ω
- Minimum: 1000 - (1000 × 0.05) = 950Ω
- **Actual value is somewhere in the range 950Ω to 1050Ω**

You don't know where in that range until you measure it.

### Common Tolerance Values

| Tolerance | Typical Resistor Type | Cost | Use Case |
|-----------|----------------------|------|----------|
| ±10% | Carbon film | Cheapest | Non-critical circuits |
| ±5% | Carbon film, some metal film | Cheap | General purpose |
| ±1% | Metal film | Moderate | Precision circuits |
| ±0.5% | Metal film precision | More expensive | High-precision design |
| ±0.1% | Metal film precision grade | Expensive | Test/measurement |

### Why Tolerance Matters: An Example

**Scenario 1: Non-Critical Use**  
You need approximate values for an indicator LED circuit:
- Design works from 100Ω to 200Ω
- A ±10% 1kΩ resistor (900Ω to 1100Ω) works fine
- Result: Save money, no problem

**Scenario 2: Precision Voltage Divider**  
You need exactly 1V ±2% from a 5V supply using two resistors in series:
- Using ±5% resistors: worst-case error is ±15% (too much!)
- Using ±1% resistors: worst-case error is ±3% (acceptable)
- Result: Must buy ±1% resistors, higher cost but necessary

### Calculating Worst-Case Circuit Performance

When you have multiple components with tolerance:
- **Worst case** is often when ALL tolerances are in the worst direction
- Example: 2 resistors at -5% and +5% extremes combine to create larger error

This is why professional designs:
1. Deliberately choose tight tolerances
2. Add adjustable components (trimmer resistors) for fine-tuning
3. Test designs across temperature and component variation extremes

## Power Rating

The **power rating** specifies the maximum power the resistor can safely dissipate as heat without burning out.

### Common Power Ratings

| Rating | Typical Size | Physical Size | Cost |
|--------|--------------|---|---|
| 1/4W | 0.25W | Tiny (1/8" long) | $ |
| 1/2W | 0.5W | Small (1/4" long) | $ |
| 1W | 1.0W | Medium (larger) | $$ |
| 2W | 2.0W | Larger | $$ |
| 5W | 5.0W | Much larger | $$$ |
| 10W+ | High power | Large/ceramic | $$$ |

### How to Calculate Power Requirements

Using P = I² × R:

**Example 1: Small Signal Application**
- Current: 5mA = 0.005A
- Resistance: 1kΩ
- Power: (0.005)² × 1000 = 0.025W = 25mW
- **Choose: 1/4W resistor (250mW rating)**

**Example 2: Current Limiting**
- Voltage drop: 3V
- Current: 100mA = 0.1A
- Power: 3V × 0.1A = 0.3W
- **Choose: 1/2W resistor (500mW rating)**

**Example 3: Load Resistor**
- Voltage: 12V
- Current: 500mA = 0.5A
- Power: 12V × 0.5A = 6W
- **Choose: 10W resistor**

### Design Margin (Critical!)

**Never use a resistor rated exactly for the calculated power.**

Why?
- Resistors age and lose efficiency
- Temperature changes the actual power dissipation
- Safety is important
- Reliability improves with margin

**Rule of thumb**: Choose a resistor with a rating **at least 2-3× your calculated power.**

**Example**:
- Calculated: 0.3W
- Minimum safe rating: 0.6W to 0.9W
- **Choose: 1W resistor** (3× margin)

This seems wasteful but is standard professional practice. A $0.10 resistor that's oversized is better than a $0.05 resistor that burns out.

### What Happens If You Exceed the Rating

If you apply more power than the rating allows:
1. Resistor gets hot (glowing red in extreme cases)
2. Protective coating or resistive element cracks
3. Resistance value changes unpredictably
4. Resistor fails—either opens (no current) or shorts (zero resistance)
5. In extreme cases, fire or explosion (rare but possible)

**This is not theoretical**—it's common in beginner mistakes.

## Temperature Coefficient

**Temperature coefficient** (TCR, measured in ppm/°C) describes how much the resistance changes per degree Celsius.

### What ppm/°C Means

- **ppm** = parts per million
- **±100 ppm/°C** means resistance changes by 0.01% per degree Celsius
- If you increase temperature by 50°C with ±100 ppm/°C resistor:
  - Change = 50 × 0.01% = 0.5%

### Common Coefficients

| Type | Temperature Coefficient | Stability |
|------|------------------------|-----------|
| Carbon film | ±500–1000 ppm/°C | Poor |
| Metal film | ±25–100 ppm/°C | Excellent |
| Wirewound | ±50–200 ppm/°C | Good |

### When Temperature Coefficient Matters

**Matters a lot**:
- Precision analog circuits
- Measurement systems
- Audio circuits (noise sensitive)
- Temperature-varying environments

**Doesn't matter**:
- Digital logic circuits
- Simple switching circuits
- Environments with stable temperature

## Operating Temperature Range

Every resistor specifies a **temperature range** where it operates within specifications.

Example: -40°C to +125°C

This means:
- **Above 125°C**: Resistor behavior becomes unpredictable; specifications not guaranteed
- **Below -40°C**: Same issue

Professional designs check:
- What's the **coldest** the circuit will encounter? (Winter storage? Outdoor use?)
- What's the **hottest** it will get? (Direct sun? Enclosed case? Near heat source?)
- Are there **local hot spots** where the resistor experiences higher temperature than ambient?

### Thermal Design

In real circuits, resistors are often the heat source. Designers must:
- Choose resistors to avoid thermal runaway (where resistance increase causes more heat)
- Provide adequate spacing for heat dissipation
- Choose larger power-rated resistors to reduce heat density
- Use heat sinks if necessary

## Maximum Voltage Rating

Some resistors (especially high-value ones) have a **maximum voltage** rating independent of power.

Example: A 10MΩ resistor might be rated for 5W at low voltage, but only safe to 500V.

Why? At very high voltages, the material between resistor leads can break down and arc.

**When this matters:**
- High-voltage power supply circuits
- Test equipment
- Industrial applications

**When it doesn't matter:**
- Battery-powered circuits (typically <50V)
- Standard consumer electronics (typically <48V)

## How to Read a Resistor Value

### Color Bands (Analog Coding)

Resistors often have colored bands that encode the value and tolerance:

**4-Band System** (most common):
1. First band: First digit
2. Second band: Second digit
3. Third band: Multiplier (number of zeros or power of 10)
4. Fourth band: Tolerance

**Example**: Brown-Black-Brown-Red
1. Brown = 1
2. Black = 0
3. Brown = ×10
4. Red = ±2%

Value: 1-0 × 10 = 100Ω ±2%

**5-Band System** (higher precision):
1. First digit
2. Second digit
3. Third digit
4. Multiplier
5. Tolerance

**Color Chart**:
| Color | Digit | Multiplier | Tolerance |
|-------|-------|-----------|-----------|
| Black | 0 | 1 | — |
| Brown | 1 | 10 | ±1% |
| Red | 2 | 100 | ±2% |
| Orange | 3 | 1,000 | — |
| Yellow | 4 | 10,000 | ±5% |
| Green | 5 | 100,000 | ±0.5% |
| Blue | 6 | 1,000,000 | ±0.25% |
| Violet | 7 | — | ±0.1% |
| Gray | 8 | — | — |
| White | 9 | — | — |
| Gold | — | 0.1 | ±5% |
| Silver | — | 0.01 | ±10% |

### Reading Resistors with Text Labels

Modern resistors (especially metal film) have values printed directly:
- 1k, 10k, 2M2, 4k7
- Much easier than color codes
- Clearer if marking doesn't fade

## Real-World Specification Example

**Vishay Metal Film Resistor Datasheet Excerpt:**

- **Nominal Resistance**: 10kΩ (labeled)
- **Tolerance**: ±1%
- **Temperature Coefficient**: ±50 ppm/°C
- **Power Rating**: 0.25W at 70°C
- **Derating**: Above 70°C, reduce power linearly
- **Operating Temperature**: -55°C to +155°C
- **Maximum Voltage**: 500V

**What this means**:
- Value is approximately 9.9kΩ to 10.1kΩ
- At 70°C, safely dissipate 0.25W
- At 100°C, dissipate less than 0.25W (derate)
- Resistance increases ~50 ppm/°C with temperature
- Works reliably from -55°C to +155°C
- Can't exceed 500V between its leads

## Key Takeaway

**Resistor ratings are not suggestions—they're limits.** Professional designers:
1. Calculate the exact power required
2. Choose resistors with rating 2-3× the calculated power
3. Verify temperature stability is acceptable
4. Verify tolerance is tight enough for the application
5. Test designs to confirm real-world performance matches theory

The $0.01 resistor that fails because you chose it exactly for the calculated power is more expensive than the $0.10 resistor with 3× margin that lasts for years.

Next: Understanding how resistors dissipate power and managing heat.
