# MOSFETs: Detailed Files Reference

This section contains comprehensive MOSFET information covering fundamental concepts, types, operating modes, real-world behavior, and common design mistakes.

## Complete MOSFET Study Material

### File 1: mosfet-basics.md
Foundation concepts—gate voltage control, three terminals, enhancement/depletion modes, threshold voltage

### File 2: enhancement-vs-depletion.md
Two basic MOSFET types with opposite behaviors, when each is used

### File 3: switching-vs-amplification.md
MOSFETs primarily as switches (modern standard), audio amplification considerations

### File 4: real-world-behavior.md
Non-ideal effects—RDS(on), gate charge, frequency response, temperature dependence, thermal concerns

### File 5: common-mistakes.md
Design errors and how to avoid them

## MOSFET vs. BJT Quick Comparison

**MOSFETs** control with **voltage** on gate (input impedance very high)
**BJTs** control with **current** on base (input impedance moderate)

**MOSFETs** faster switching, lower power dissipation, preferred for modern power electronics
**BJTs** still used for audio, low-frequency switching, some legacy designs

## Key MOSFET Advantages

1. **Voltage control**: Gate needs almost no current (only charging/discharging capacitance)
2. **Very fast switching**: MHz to GHz capable
3. **Low on-resistance**: RDS(on) = 1mΩ–10Ω (minimal dissipation when on)
4. **Scalable**: Millions of MOSFETs integrated on single chip (modern CPUs)
5. **Efficient**: Switching power supplies rely on MOSFET switching

## Key MOSFET Disadvantages

1. **Gate oxide fragile**: Exceeding gate-source voltage causes permanent failure
2. **ESD sensitive**: Static discharge destroys gate
3. **Gate drive requirements**: Needs driver circuit for fast switching
4. **RDS(on) temperature dependent**: Increases with heat
5. **Complicated for learning**: More parameters than BJT

## Core MOSFET Parameters (Datasheet Reading)

| Parameter | Symbol | Meaning |
|-----------|--------|---------|
| Gate-source threshold voltage | Vth | Gate voltage needed to turn on |
| On-state drain-source resistance | RDS(on) | Resistance when fully on |
| Gate charge | Qg | Energy needed to switch |
| Drain-source voltage max | VDSR | Maximum voltage rating |
| Drain current max | ID(max) | Maximum current rating |
| Power dissipation | Pdiss | Maximum continuous power |
| Gate-source voltage max | VGS(max) | Maximum safe gate voltage |
| Switching frequency | fmax | Maximum switching frequency |

## Common MOSFET Types and Applications

**Enhancement N-Channel (NMOS)**:
- Most common type
- Used in switching power supplies, motor control
- Example: IRF510, IRFZ44

**Enhancement P-Channel (PMOS)**:
- Less common (NMOS usually preferred)
- Used in battery management, where NMOS not suitable
- Example: IRF9510

**Power MOSFETs**:
- High current capability
- Large silicon die
- Require heatsinks
- Used in motor drives, power supplies

**Small Signal MOSFETs**:
- Low current, fast switching
- No heatsink needed
- Used in logic circuits, RF

**High-Voltage MOSFETs**:
- Gate oxide designed for high gate voltage
- Rated 200V–600V or higher
- Used in industrial power conversion

## Professional MOSFET Design Approach

1. **Choose MOSFET** with sufficient voltage and current rating (1.5–2× margin)
2. **Select gate driver** appropriate for switching frequency
3. **Calculate RDS(on) heating** at maximum current
4. **Verify gate voltage** within maximum limits
5. **Add gate resistor** to control switching speed and reduce ringing
6. **Include snubber/clamp** for inductive loads
7. **Design thermal management** for power dissipation
8. **Test prototype** at worst-case conditions
9. **Measure actual RDS(on)** and switching frequency in circuit
10. **Validate thermal behavior** during operation

## When to Use MOSFETs

- Power converters and switching regulators
- Motor drives and PWM control
- Audio power amplifiers (Class D)
- Digital logic and high-speed switching
- Battery management systems
- RF and microwave circuits
- Any application needing fast, efficient switching

MOSFETs are the standard for modern power electronics.

## Key Takeaway

**MOSFETs are voltage-controlled, high-speed switches with low on-resistance. They're the foundation of modern power electronics but require careful gate drive design, thermal management, and protection against gate overvoltage and ESD.**

See detailed files for complete information on fundamentals, switching/amplification, real-world behavior, and common mistakes.
