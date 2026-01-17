# MOSFETs: Common Mistakes and Design Errors

## 1. Exceeding Gate-Source Voltage

### The Mistake
Applying gate voltage beyond maximum rating (typically ±20V):
- Gate oxide is only ~10–20 nanometers thick
- Tiny overvoltage breaks the insulator
- Permanent failure

### Example Failure
- MOSFET rated for 20V gate maximum
- Switching transient creates 25V spike on gate
- Gate oxide breaks down
- MOSFET becomes permanently leaky or short-circuit

### Why It Happens
- Bootstrap circuits sometimes fail to limit gate voltage
- Transient overshoot not accounted for
- ESD (electrostatic discharge) can damage gate

### The Fix
1. **Zener clamp diode**: Clamps gate voltage (cathode to gate, anode to source)
2. **TVS diode**: Ultra-fast protection for transients
3. **Gate resistor**: Reduces ringing (side benefit)
4. **Gate driver**: Designed to limit output voltage
5. **Bootstrap capacitor**: Ensures gate voltage stays bounded

### Professional Practice
- Always verify gate voltage stays within limits
- Include gate clamp diodes as standard protection
- Measure gate voltage on prototype with oscilloscope
- Verify at worst-case operating conditions

---

## 2. ESD Damage to Gate

### The Mistake
Handling MOSFET without ESD protection:
- Static discharge (even 100V) damages gate
- Gate oxide cannot withstand this
- Device damaged before circuit even powers on

### Why It Happens
- MOSFETs extremely ESD-sensitive (gate is capacitive, tiny inductance leads to high dI/dt)
- Single touch during assembly can cause failure
- Hard to diagnose (component may work initially, then fail intermittently)

### The Fix
1. **ESD wrist strap**: Ground yourself before handling
2. **Anti-static mat**: Ground work surface
3. **ESD-safe tools**: Avoid static discharge
4. **Protective packing**: Store MOSFETs in conductive bags
5. **Circuit protection**: Add gate resistor and clamp diodes

### Professional Practice
- Treat all MOSFETs as ESD-sensitive components
- Follow ESD procedures rigorously
- Use conductive foam, not styrofoam (which builds charge)
- Label boards with ESD warnings if MOSFETs exposed

---

## 3. Gate Floating (Unconnected Gate)

### The Mistake
Gate left floating (not driven to any voltage):
- High impedance gate picks up noise
- MOSFET turns on/off randomly
- Circuit becomes unpredictable

### Why It Fails
- Any nearby signal couples into gate (EMI)
- Temperature fluctuations change gate capacitance slightly
- MOSFET oscillates between states
- Load can be damaged (random on/off)

### The Fix
1. **Always drive gate** to known voltage (0V or positive)
2. **Gate resistor to ground**: Pulls gate to ground if not driven
3. **Pull-down resistor**: Typical value 10kΩ
4. **Gate driver IC**: Properly drives gate, never leaves floating

### Example: Safe Default
```
       Driver output
           |
         [1kΩ]
           |
    Gate--+
           |
         [10kΩ] <- Pull-down to ground
           |
         Ground
```

Pull-down ensures gate is LOW if driver disconnected.

### Professional Practice
- Never leave any gate floating
- Include pull-down resistor as default
- Document gate voltage in schematic
- Verify gate signal on prototype

---

## 4. Insufficient Gate Drive Current

### The Mistake
Using weak gate driver that cannot supply enough current:
- MOSFET gate capacitance not charged quickly
- MOSFET turns on slowly
- High switching losses during transition
- MOSFET heats up unnecessarily

### Why It Fails
Gate must be charged/discharged in finite time:
$$t = \frac{Q_g}{I_{gate}}$$

If Igate too small, t becomes large → switching losses → heat.

### Example Calculation
- Qg = 50nC (MOSFET datasheet)
- Weak driver: Igate = 10mA
- Switch time: t = 50nC / 10mA = 5µs
- At 100kHz switching frequency, unacceptable loss

Strong driver: Igate = 1A
- Switch time: t = 50nC / 1A = 50ns
- Acceptable (fast switching, low loss)

### The Fix
1. **Choose gate driver with sufficient current** (typically 0.5–2A minimum)
2. **Calculate required Qg** from MOSFET datasheet
3. **Verify switching time** meets frequency requirement
4. **Test on prototype** to ensure fast switching

### Professional Practice
- Gate driver current rating > typical requirement (2–3× margin)
- Measure gate voltage rise time with oscilloscope
- Ensure full gate drive voltage is reached before clock edge
- Simulate gate charging to verify performance

---

## 5. Gate Resistor Too Large (Slow Switching)

### The Mistake
Large gate resistor (100kΩ+) slows switching:
- MOSFET takes milliseconds to fully turn on
- Switching losses dominate
- Excessive heating
- Possible thermal runaway

### Why It Fails
Gate resistor limits charging current:
$$I_{gate} = \frac{V_{drive} - V_{gate}}{R_g}$$

Large Rg → small Igate → slow charging → slow switching.

### Example: 100kΩ Gate Resistor
- Drive voltage: 5V
- 100kΩ resistor
- Gate current: 5V / 100kΩ = 50µA
- To charge 50nC: Time = 50nC / 50µA = 1ms
- At 100kHz, unacceptable

### Why Large Gate Resistor Used
- Mistaken belief that it reduces ringing (it does, but too much)
- Lack of understanding of switching losses
- Trying to reduce EMI (wrong approach)

### The Fix
1. **Use smaller gate resistor** (1–100Ω typical)
2. **Use snubber circuit** to control ringing (not just resistor)
3. **Measure switching time** on prototype
4. **Balance speed and noise** (both matter)

### Professional Practice
- Default gate resistor: 10–50Ω
- Adjust based on ringing observed
- Use RLC circuit (resistor + capacitor + inductance) to model
- Simulate switching transient to verify performance

---

## 6. Gate Resistor Too Small (Ringing and EMI)

### The Mistake
Very small gate resistor (< 1Ω) causes:
- Excessive ringing (oscillation) during switching
- EMI emissions
- Possible gate voltage exceeding maximum
- Circuit radiates noise

### Why It Fails
Without resistor damping, parasitic inductances cause ringing:
- Gate-source loop inductance resonates with gate capacitance
- Voltage rings above/below target
- Frequency typically 100MHz–1GHz (strong EMI)

### Example: 0.1Ω Gate Resistor
- Gate capacitance: 10nF
- Parasitic inductance: 2nH
- Resonant frequency: f = 1/(2π√(LC)) ≈ 1.1 GHz
- Large ringing at this frequency
- EMI radiates from MOSFET area

### The Fix
1. **Use appropriate gate resistor** (10–50Ω typical)
2. **Use snubber circuit**: RC across drain-source (100Ω + 10nF example)
3. **Measure gate and drain voltage** with oscilloscope
4. **Minimize PCB inductance**: Short traces, wide copper

### Professional Practice
- Start with 20–50Ω gate resistor
- Measure ringing on prototype
- Increase resistor if ringing excessive
- Add snubber circuit if needed
- Test EMI emissions if required by standard

---

## 7. No Snubber for Inductive Load Switching

### The Mistake
Switching inductive load without clamp diode or snubber:
- Inductor voltage spike when switching
- Drain voltage exceeds VDSR(max)
- MOSFET fails avalanche breakdown

### Why It Fails
When MOSFET turns off, inductor fights current change:
$$V = L \times \frac{dI}{dt}$$

Example: 1µH inductor, 10A switching off in 10ns
$$V = 1µ \times \frac{10}{10n} = 1000V \text{ spike}$$

Even small inductance creates huge transient.

### Typical Scenario
- 12V supply, motor winding (inductor)
- No protection
- Switching off induces 12V + spike
- Spike exceeds 100V MOSFET rating
- Catastrophic failure

### The Fix
1. **Flyback diode**: Across motor/inductor (cathode at positive supply)
2. **TVS diode**: Across drain-source (clamps overvoltage fast)
3. **Clamp circuit**: RCD circuit (resistor-capacitor-diode) for precision control
4. **Gate driver**: Some integrate clamp function

### Professional Practice
- **ALWAYS use flyback protection** for inductive loads
- Measure spike voltage with oscilloscope (without protection initially, carefully)
- Choose diode fast enough for switching frequency
- Use 1N4148 (fast) for MHz+ frequencies

---

## 8. Thermal Management Neglected

### The Mistake
High-power MOSFET without heatsink:
- Junction temperature exceeds 150°C
- RDS(on) increases dramatically
- Thermal runaway possible
- MOSFET fails

### Why It Fails
$$T_j = T_a + P \times \theta_{ja}$$

Without heatsink, θja ≈ 60°C/W (poor).

Example: 10W at 25°C ambient
- Tj = 25 + 10 × 60 = 625°C (fails)

With heatsink, θja ≈ 5°C/W
- Tj = 25 + 10 × 5 = 75°C (safe)

### The Fix
1. **Calculate thermal resistance** (θja) needed for operating conditions
2. **Choose heatsink** with sufficient area
3. **Apply thermal grease** between MOSFET and heatsink
4. **Mount securely** (thermal contact is critical)
5. **Verify junction temperature** during operation

### Professional Practice
- Design for maximum junction temperature of 125°C (not 150°C absolute max)
- Thermal test at worst-case conditions
- Use temperature sensor if critical
- Verify heatsink contact is good (no air gaps)

---

## 9. RDS(on) Heating Not Accounted For

### The Mistake
Design assumes low heating in on-state:
- RDS(on) chosen without calculating power dissipation
- I²R heating not planned for
- Excessive temperature rise

### Why It Fails
$$P = I^2 \times R_{DS(on)}$$

Example: 50A, 0.1Ω MOSFET
$$P = 50^2 \times 0.1 = 250W$$

Massive power, requires large heatsink or thermal failure.

### The Fix
1. **Calculate RDS(on) power** at maximum current
2. **Verify heatsink** sufficient for this power
3. **Include temperature derating** in calculation
4. **Measure actual temperature** during operation
5. **Use thermography** to verify uniform heating

### Professional Practice
- Always calculate I²R heating as part of thermal design
- Thermal analysis mandatory before prototype
- Measure junction temperature on actual circuit
- Document thermal performance in design review

---

## 10. Ignoring Gate Charge (Qg)

### The Mistake
Choosing gate driver without verifying Qg:
- Driver unable to fully charge gate
- MOSFET doesn't fully turn on
- High RDS(on), excessive heating
- Low switching frequency performance

### Why It Fails
$$t_{switch} = \frac{Q_g}{I_{gate}}$$

If gate driver current insufficient:
- Qg charges slowly
- Switching takes longer
- Switching losses increase
- Frequency performance degrades

### The Fix
1. **Lookup Qg** from MOSFET datasheet
2. **Calculate required charging time** at expected frequency
3. **Choose gate driver** with sufficient current rating
4. **Verify on prototype** with oscilloscope

### Professional Practice
- Gate driver current must support fastest switching needed
- Typical: 1A minimum for fast switching applications
- High-frequency applications (MHz+): 2A or more
- Measure gate voltage rise time to verify

---

## 11. Assuming BJT Behavior from MOSFET

### The Mistake
Treating MOSFET like BJT:
- Expecting base current behavior (MOSFET has none)
- Insufficient gate voltage (only need voltage, not current)
- Misunderstanding gain (no hFE equivalent)

### Why It Fails
- MOSFET is voltage-controlled (gate impedance essentially infinite)
- BJT is current-controlled (base impedance moderate)
- Completely different control mechanisms

### Example Error
"Let me limit MOSFET gate current to protect it"
- MOSFET gate needs almost no DC current
- Limiting gate current slows switching
- Creates losses
- Wrong reasoning

### The Fix
1. **Understand MOSFET control**: Voltage, not current
2. **Gate driver supplies gate charge** (time-dependent, not continuous current)
3. **Gate voltage must reach specified level** (usually VGS(max) or close)
4. **Study MOSFETs** as distinct from BJTs

### Professional Practice
- Never confuse MOSFET and BJT control
- Study datasheet carefully
- Measure gate voltage (not current) on prototype
- Understand charging/discharging gate capacitance

---

## Professional MOSFET Design Checklist

Before finalizing MOSFET circuit:

- ✓ Voltage/current rating verified with 1.5–2× margin
- ✓ RDS(on) power dissipation calculated at maximum current
- ✓ Heatsink selected and thermally verified
- ✓ Gate voltage stays within maximum rating (±20V typical)
- ✓ Gate clamp diodes included for protection
- ✓ Gate drive circuit verified to supply sufficient current
- ✓ Flyback/TVS diode protection on inductive loads
- ✓ Gate resistor sized (10–50Ω typical) to balance speed and ringing
- ✓ PCB layout minimizes parasitic inductance
- ✓ Switching transients measured and verified on prototype
- ✓ Thermal performance tested at worst-case conditions
- ✓ Multiple units tested for consistency
- ✓ ESD protection during manufacture and assembly

---

## Key Takeaway

**Professional MOSFET design requires careful attention to gate voltage limits, gate drive sufficiency, thermal management, inductive load protection, and detailed prototype testing. MOSFETs are simple in concept but fail catastrophically if specifications are exceeded or protection is neglected.**
