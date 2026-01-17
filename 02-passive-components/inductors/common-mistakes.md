# Common Inductor Mistakes

## Mistake 1: Exceeding Saturation Current

### The Error
Designing a power supply inductor without accounting for peak current, leading to saturation.

**Example**:
- Application needs 8A peak current
- Chose inductor with Isat = 8A (thinking it's just the limit)
- At temperature 85°C: Actual Isat drops to 6A
- Inductor saturates, inductance collapses
- Power supply fails to regulate

### Why It Fails
- Saturation is a hard cliff (inductance disappears)
- Circuit designed assuming inductance will work
- At saturation, inductor is useless (just wire resistance)

### The Fix
1. **Calculate peak current** in application (including headroom)
2. **Check datasheet Isat** at operating temperature (not just 25°C)
3. **Use 1.5–2× saturation margin**:
   - Peak current: 8A
   - Choose: Isat ≥ 12–16A
4. **Verify with prototype** at temperature extremes

## Mistake 2: Wrong Core Type for Frequency

### The Error
Using iron core inductor in high-frequency switching supply (MHz range).

**Result**: 
- Iron core losses excessive at MHz frequencies
- Inductor gets extremely hot
- Efficiency terrible
- Component fails

### Why It Fails
- Iron core designed for low-frequency (<1 kHz) use
- Hysteresis and eddy current losses skyrocket at MHz
- Heat generation exceeds component rating

### The Fix
1. **Identify frequency** of operation (kHz? MHz?)
2. **Choose appropriate core**:
   - Low frequency (<1 kHz): Iron core OK
   - Medium frequency (1–100 kHz): Ferrite core
   - High frequency (> 100 kHz): Air core or specialized
3. **Verify in datasheet** that core type is rated for frequency

## Mistake 3: Not Accounting for Temperature Derating

### The Error
Designing power supply to saturation margin at 25°C, forgetting it will operate at 85°C.

**Result**:
- Saturation current at 25°C: 10A (Isat per datasheet)
- Actual saturation at 85°C: 8A (30% lower)
- Design runs at 9A peak current
- In hot environment, inductor saturates
- Power supply fails in field (hot operating conditions)

### The Fix
1. **Identify worst-case temperature** (expected max operation)
2. **Use saturation current at that temperature**, not room temperature
3. **Add margin** on top of derated value

**Example**:
- Worst case: 85°C operation
- Datasheet: Isat = 10A at 25°C
- Derated: Isat ≈ 8A at 85°C
- Design for: 4–5A (50% margin)

## Mistake 4: Ignoring Parasitic Capacitance

### The Error
Using inductor above its self-resonant frequency (SRF), expecting it to work as inductor.

**Result**:
- Impedance doesn't increase with frequency as expected
- At SRF and above: Impedance dominated by parasitic capacitance
- Inductor doesn't filter or work as designed

### The Fix
1. **Find SRF** on inductor datasheet
2. **Keep operating frequency** well below SRF (typically < 50% of SRF)
3. **If circuit frequency is above available SRF**: Choose air core or physically smaller component

**Example**:
- Circuit frequency: 5 MHz
- Available ferrite inductor SRF: 10 MHz (seems OK)
- Safe operation: Below 5 MHz (50% of SRF)
- Problem: Circuit is AT the SRF limit
- Better: Choose air core inductor with SRF > 50 MHz

## Mistake 5: Magnetic Coupling Between Inductors

### The Error
Placing two inductors close together in circuit, not realizing they magnetically couple.

**Result**:
- Magnetic field from one affects the other
- Intended inductance values are different than marked
- Circuit doesn't work as designed
- Noise coupling between circuits

### The Fix
1. **Physically separate inductors**
2. **Orient inductors so fields cancel** (coils perpendicular)
3. **Shield inductors** (Faraday shield reduces coupling)
4. **Use software simulation** to model coupling effects

## Mistake 6: Forgetting Inductor During Power Shutdown

### The Error
Switching off current through an inductor without providing a path for the magnetic energy to go.

**Result**:
- Current through inductor tries to stop abruptly
- Magnetic field collapses
- Inductor generates huge voltage spike (Lenz's law)
- Voltage spike damages transistor (or other switching element)
- Power supply fails catastrophically

### Why It Happens
- Inductor equation: V = L × dI/dt
- If dI/dt is very large (fast switch), V becomes huge
- Example: L = 1 µH, dI/dt = 1A per nanosecond → V = 1000V spike

### The Fix
1. **Always provide a "flyback diode"** across the inductor
2. **Diode provides path for current** when inductor tries to de-energize
3. **Diode prevents voltage spike**

This is not optional in switching circuits—inductor must have a flyback path or circuit dies.

## Mistake 7: Assuming All Inductors Are Linear

### The Error
Using iron core inductor in precision circuit, expecting inductance to be constant with current.

**Result**:
- As current increases, core magnetization increases
- Inductance decreases (soft saturation)
- Circuit behavior changes with current level
- Circuit doesn't work linearly as designed

### The Fix
1. **Use air core** for linear applications (inductance truly constant)
2. **Or use ferrite** and operate well below saturation (inductance approximately constant)
3. **Test circuit** with varying current to verify linearity

## Mistake 8: Ignoring DC Resistance

### The Error
Calculating power supply efficiency assuming ideal inductor (no losses).

**Result**:
- Calculated efficiency: 95%
- Measured efficiency: 85%
- 10% loss unaccounted for
- Thermal management inadequate
- Power supply overheats

### Why It Fails
- Real inductor has DC resistance (often 0.1–1Ω for power inductors)
- Current through this resistance dissipates power: P = I²Rdc
- At high current (10A), 0.1Ω means 10W loss (significant!)

### The Fix
1. **Find DCR** on inductor datasheet
2. **Calculate power loss**: P = I² × DCR
3. **Account for this loss** in efficiency and thermal design

## Mistake 9: Thermal Management Neglect

### The Error
Installing high-current inductor on PCB with no consideration for heat dissipation.

**Result**:
- Inductor dissipating 20W
- Mounted on small PCB, no airflow
- Temperature rises 100°C+ above ambient
- Core properties degrade
- Saturation current drops dramatically
- Inductor fails from thermal stress

### The Fix
1. **Calculate power dissipation**: P = I² × Rdc
2. **Plan for cooling**: Airflow, thermal vias, heat sinks
3. **Verify temperature** with thermal simulation or testing

## Mistake 10: Choosing by Inductance Value Alone

### The Error
Selecting inductor based only on needed inductance, ignoring saturation and temperature.

**Example**:
- Need 100 µH
- Choose first 100 µH inductor found
- Datasheet says Isat = 2A
- Application needs 5A
- Inductor saturates immediately

### The Fix
1. **Create a requirements list**:
   - Inductance value (µH)
   - Peak current (amps)
   - Operating frequency (Hz)
   - Temperature range (°C)
   - Space available (size)
2. **Filter inductors** by all criteria, not just inductance
3. **Verify margin** on saturation (1.5–2× rule)

## Practical Checklist: Before Choosing an Inductor

- [ ] **Inductance**: Correct value in µH
- [ ] **Saturation current**: At least 1.5–2× peak current at operating temperature
- [ ] **DC resistance**: Acceptable for power budget
- [ ] **Core type**: Appropriate for frequency range
- [ ] **Self-resonant frequency**: Well above operating frequency
- [ ] **Temperature range**: Covers application (-40 to +85°C? or more?)
- [ ] **Thermal management**: Adequate cooling for power dissipation
- [ ] **Magnetic shielding**: Necessary? (toroidal if critical)
- [ ] **Cost/availability**: Within budget, can be sourced
- [ ] **Flyback diode**: Required if inductor current switches abruptly

## Key Takeaway

**Most inductor failures are due to saturation, not resistance.**

Design properly by:
1. Calculating peak current with margin
2. Derat saturation current for temperature
3. Choosing core type for frequency
4. Providing flyback paths for energy dissipation
5. Managing thermal stress

Inductors are less forgiving than resistors or capacitors—saturation is a binary failure (works or doesn't), not gradual degradation.

---

You've now completed the passive components section (resistors, capacitors, inductors). Next: Active components (diodes, BJTs, MOSFETs).
