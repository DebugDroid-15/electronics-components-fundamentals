# MOSFETs: Real-World Behavior and Design Considerations

## RDS(on): The On-State Resistance

### Definition
**RDS(on)** = resistance measured between drain and source when MOSFET is fully on.

### Practical Impact

**Power dissipation when conducting**:
$$P = I^2 \times R_{DS(on)}$$

Example: 10A through 0.1Ω MOSFET
$$P = 10^2 \times 0.1 = 10W$$

This is why RDS(on) specification is critical—directly determines efficiency.

### Typical Values
- **Small signal MOSFET** (2N7000): 50–100Ω (low current devices)
- **Power MOSFET** (low RDS(on)): 0.01–0.1Ω (millions of transistors in parallel)
- **Extreme power devices**: 0.001Ω possible but very expensive

### Temperature Dependence
**Critical**: RDS(on) **increases** with temperature (~0.4–0.8%/°C)

Example: 0.1Ω at 25°C
- At 75°C: RDS(on) ≈ 0.13–0.16Ω (+30–60% increase)
- Power dissipation increases further with temperature (positive feedback)

### Design Consequence
- Choose MOSFET with RDS(on) **rated at maximum operating temperature**
- Worst-case analysis essential
- Measure actual RDS(on) on prototype during operation
- Temperature testing mandatory

---

## Gate Charge (Qg) and Switching Speed

### Definition
**Gate charge**: Total charge (Coulombs) needed to switch MOSFET from off to on (or on to off).

### What It Means
To charge gate from 0V to operating voltage:
$$Q = C_{iss} \times V_{gs}$$

Where Ciss = input capacitance (gate to source/drain).

Typical: 10–100 nanofarads depending on MOSFET size.

### Switching Transient Current
Switching takes finite time:
$$t_{switch} = \frac{Q_g}{I_{gate}}$$

Where Igate = current supplied by gate driver.

**Example**: Qg = 50nC, gate driver supplies 1A
$$t_{switch} = \frac{50 \times 10^{-9}}{1} = 50 \text{ nanoseconds}$$

### Gate Driver Responsibility
1. Supply sufficient gate current to charge/discharge quickly
2. Source Qg from supply to gate
3. Sink Qg from gate to ground
4. Must be fast enough for operating frequency

Typical gate driver can supply 0.5–2A gate current.

### Design Consideration
- At very high frequency (MHz+), gate driver becomes limiting factor
- May need stronger gate driver
- Larger gate resistor = slower switching = higher losses
- Smaller gate resistor = faster switching = more ringing/noise

---

## Threshold Voltage (Vth) and Temperature

### Definition
**Vth** = gate-source voltage where drain current starts to flow (~0.1mA convention).

Below Vth: MOSFET essentially off.
Above Vth + margin: MOSFET fully on.

### Typical Values
1–5V depending on MOSFET type.

### Temperature Coefficient
**Vth changes with temperature**: Typically **-2 to -5mV/°C**

Example: Vth = 2.5V at 25°C
- At 75°C: Vth ≈ 2.3V (decreases ~0.2V)
- At 0°C: Vth ≈ 2.65V (increases ~0.15V)

### Design Impact

**At high temperature (turn-on easier)**:
- Lower Vth means MOSFET turns on at lower gate voltage
- Could turn on unintentionally from noise
- Gate voltage creeps lower with thermal stress
- Less safety margin

**At low temperature (turn-on harder)**:
- Higher Vth means MOSFET harder to turn on
- Gate voltage must be more positive
- May not reach sufficient overdrive
- Switching slows down, losses increase

### Professional Practice
- Design gate voltage at least 2V above Vth at worst-case temperature
- If Vth range is 1–3V, ensure gate voltage ≥ 5V minimum
- Test at temperature extremes
- Use gate-source clamp diode if high-voltage transients possible

---

## Gate Oxide: The Fragile Component

### Gate Oxide Structure
Thin insulating layer (tens of nanometers) between gate and channel.

### Gate Voltage Limits
- **Typical rating**: 10–20V maximum gate-source voltage
- **Exceed this**: Oxide breaks down permanently
- **Result**: MOSFET leaks or shorts (fails)
- **Irreversible**: Once broken, cannot be repaired

### Example Failure Scenario
- MOSFET rated for ±20V gate voltage
- Gate spike from switching transient reaches 25V
- Gate oxide breaks down
- MOSFET becomes leaky or short circuit
- Entire circuit may fail

### Protection Strategies
1. **Gate resistor**: Limits di/dt, reduces ringing
2. **Zener diode**: Clamps gate voltage to safe level (gate-source path)
3. **TVS diode**: Ultra-fast protection for fast transients
4. **Gate driver**: Limits output voltage to safe level
5. **Bootstrap circuit**: Ensures gate voltage never exceeds limit
6. **PCB layout**: Minimize parasitic inductance to reduce ringing

---

## Drain-Source Voltage and Safe Operating Area (SOA)

### Maximum Ratings
**VDSR(max)**: Maximum drain-source voltage

- Typical ratings: 30V, 60V, 100V, 200V depending on type
- Exceed this: Avalanche breakdown, MOSFET fails
- Example: 100V MOSFET, spike to 150V = failure

### Safe Operating Area (SOA)
Region where MOSFET can operate without failure:
- Maximum drain current
- Maximum drain-source voltage
- Maximum power dissipation
- Thermal limits

All must be satisfied simultaneously.

### Example: IRF510 (Power MOSFET)
- VDSR(max) = 100V
- ID(max) = 3.3A at 25°C
- Pdiss(max) = 43W at 25°C (with heatsink)
- θja = 62°C/W (without heatsink)

At 50°C junction temperature (not 25°C):
- Maximum power ≈ 25W (derated)
- Maximum current ≈ 1.5A (estimated derated)

### Protecting Against Overvoltage
**Transient voltage suppression (TVS) diode** across drain-source:
- Clamps voltage to safe level
- Conducts only during overvoltage
- Absorbs energy from inductive spike
- Standard protection practice

---

## Frequency Response and Parasitic Capacitances

### High-Frequency Parasitic Capacitances

**Gate-Source Capacitance (Cgs)**:
- Primary capacitance for gate charging
- Contributes to gate charge Qg
- Controls switching speed

**Gate-Drain Capacitance (Cgd)** (also called Miller capacitance):
- Problem capacitance for fast switching
- During switching transient, drain voltage changes rapidly
- Capacitive coupling feeds voltage back to gate
- Can prevent MOSFET from turning off cleanly
- Causes ringing, oscillation

**Drain-Source Capacitance (Cds)**:
- Affects switching speed
- Contributes to total gate charge

### Miller Effect
When drain voltage changes rapidly (dV/dt), gate voltage affected through Cgd:

$$i_{gate} = C_{gd} \times \frac{dV_D}{dt}$$

This coupling can cause oscillation or prevent clean switching at very high frequencies.

### Frequency Limitations
- MOSFETs work excellently to MHz range
- At very high frequency (>100MHz), parasitic capacitances become limiting
- Specialized RF MOSFETs designed to minimize these effects
- GHz operation possible but requires careful design

---

## Gate Drive Requirements

### Voltage Levels
- Logic signal (0–5V) can directly drive MOSFET rated for 5V gates
- Gate must be driven to full operating voltage
- Partial gate drive = higher RDS(on), more loss

### Current and Speed
- Gate capacitance requires charging current
- Larger MOSFET = larger gate capacitance = more current needed
- At high frequency, gate current becomes significant

### Bootstrap Circuit (High-Side Switching)
When switching high-side of circuit (above load):
- Gate must be driven relative to source (which floats with switching)
- Requires bootstrap capacitor
- Charges from low-side, supplies gate drive to high-side
- Common in buck converters and bridge drivers

---

## Thermal Management

### Heat Generation
$$P = I^2 \times R_{DS(on)}$$

Only occurs when MOSFET is conducting (on state).

If duty cycle = 50%, average power = 0.5 × peak power.

### Heatsink Sizing
$$T_j = T_a + P \times \theta_{ja}$$

Where:
- Tj = junction temperature
- Ta = ambient temperature
- P = power dissipation
- θja = thermal resistance junction to ambient

Example: 10W at 25°C ambient, θja = 5°C/W
$$T_j = 25 + 10 \times 5 = 75°C$$

At 75°C, RDS(on) increases by ~25% (positive feedback).

### Temperature Derating
At high temperature, maximum power and current decrease:
- At 150°C: Power halved compared to 25°C rating
- Design with this in mind
- Thermal testing mandatory

---

## Switching Transients and Ringing

### Switching Speed
MOSFET transitions between off and on in nanoseconds to microseconds.

### Parasitic Inductances
PCB traces have parasitic inductance:
- Gate loop inductance: Causes gate voltage ringing
- Drain-source loop inductance: Causes drain voltage ringing
- Source-ground inductance: Increases effective source voltage during switching

### Ringing Effects
- Voltage overshoot on drain (can exceed maximum rating)
- Gate voltage overshoot
- Switching loss increased (ringing dissipates energy)
- EMI emissions

### Mitigation
1. **Gate resistor** (10–100Ω): Damps gate oscillations
2. **Snubber circuit** (RC across drain-source): Damps drain voltage ringing
3. **TVS diode** (drain-source): Clamps overvoltage
4. **PCB layout**: Minimize parasitic inductance

---

## Body Diode and Reverse Conduction

### Intrinsic Body Diode
Every MOSFET has internal parasitic diode between source and drain.

When source voltage is pulled above drain (reverse bias attempt):
- Body diode conducts instead
- Current bypasses MOSFET channel
- Forward voltage drop ~0.7V (typical diode)

### Significance
- Freewheeling path for inductive loads
- Can prevent voltage overshoot
- Has finite recovery time (affects switching behavior)
- Can carry high currents if not carefully managed

---

## Real Circuit Effects Summary Table

| Effect | Behavior | Design Impact |
|--------|----------|----------------|
| RDS(on) temperature rise | Increases 0.4–0.8%/°C | Use high-temp rating, thermal management |
| Vth temperature | Decreases -2 to -5mV/°C | Gate voltage margin at cold temperature |
| Gate oxide breakdown | ~15–20V maximum (device dependent) | Gate voltage clamp protection required |
| Gate charge | 10–100 nC typical | Gate driver current must be sufficient |
| Switching transients | Ringing at nanosecond timescale | Gate resistor, snubber circuits needed |
| Frequency response | MHz to GHz range | Miller capacitance limits very high frequency |
| Body diode conduction | Occurs during reverse voltage | Can cause unexpected currents |

---

## Key Takeaway

**Real MOSFETs have temperature-dependent on-resistance, gate oxide limits, parasitic capacitances, and switching transients that must all be managed through proper gate drive design, thermal management, and protection circuits. Professional designs account for all these effects through analysis, simulation, and prototype testing.**

