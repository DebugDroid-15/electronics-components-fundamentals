# Capacitor Basics: Charge Storage and Fundamental Concepts

## The Core Concept: What Is Capacitance?

A **capacitor** is a component that stores electrical charge (and thus electrical energy) when voltage is applied across it.

Imagine two metal plates separated by an insulating material:
- Apply positive voltage to one plate, negative to the other
- Electrons are repelled from the positive plate toward the negative plate
- But the insulating material stops them
- Charge accumulates on each plate
- This charge separation creates the storage effect

**Capacitance** is the measure of how much charge a capacitor can store per unit voltage applied.

### Unit: Farad (F)

Capacitance is measured in **farads**. A one-farad capacitor stores one coulomb of charge when one volt is applied:

$$C = \frac{Q}{V}$$

Where:
- C = capacitance (farads)
- Q = charge stored (coulombs)
- V = voltage applied (volts)

### Practical Units

The farad is huge. Real components use smaller units:

| Unit | Meaning | Abbreviation | Example |
|------|---------|--------------|---------|
| Farad | Base unit | F | Rare (supercapacitors) |
| Millifarad | 1/1000 F | mF | Large power supply caps |
| Microfarad | 1/1,000,000 F | µF | Common, everyday use |
| Nanofarad | 1 billionth F | nF | Small signal circuits |
| Picofarad | 1 trillionth F | pF | High-frequency circuits |

A typical capacitor might be 10 µF (microfarad) or 100 nF (nanofarad).

## The Capacitor Equation

The fundamental relationship is:

$$Q = C \times V$$

Where:
- Q = charge in coulombs
- C = capacitance in farads
- V = voltage in volts

### Practical Example

A 10 µF capacitor charged to 10V stores:
$$Q = 10 \times 10^{-6} \text{ F} \times 10 \text{ V} = 100 \times 10^{-6} \text{ C} = 100 \text{ µC}$$

100 microcoulombs—a tiny amount of charge, but enough for many applications.

## Energy Storage

When a capacitor is charged, it stores **electrical energy**:

$$E = \frac{1}{2} \times C \times V^2$$

This energy comes from the source charging it, and can be released when needed.

### Practical Example

A 10 µF capacitor charged to 10V stores:
$$E = \frac{1}{2} \times 10 \times 10^{-6} \times 10^2 = \frac{1}{2} \times 10 \times 10^{-6} \times 100 = 0.0005 \text{ J} = 0.5 \text{ mJ}$$

That's 0.5 millijoules—tiny, but enough to power a camera flash, trigger a signal, or perform useful work in circuits.

## Charging and Discharging

### Charging a Capacitor

When voltage is first applied:
- Initially, the capacitor is uncharged (acts like a short circuit)
- Current flows, charging the capacitor
- As charge accumulates, voltage across the capacitor rises
- Eventually, voltage matches the applied voltage
- Current stops (capacitor fully charged)

The **charging time** depends on the resistance in series and the capacitance:

$$\tau = R \times C$$

Where τ (tau) is the **time constant**. After one time constant, the capacitor charges to 63% of the final voltage.

This is why you see RC circuits everywhere—they create predictable time delays.

### Discharging a Capacitor

If a charged capacitor is connected to a resistor:
- Charge flows from positive to negative plate
- Current stops when capacitor is empty
- Takes about 5 time constants to fully discharge (95%)

This exponential charging/discharging is fundamental to analog circuits and timing.

## AC vs. DC Behavior

This is crucial: Capacitors behave very differently in DC and AC circuits.

### DC Behavior

In DC (direct current, constant voltage):
- Capacitor charges to the applied voltage
- Then **no current flows** (capacitor is fully charged)
- The capacitor blocks DC (acts like an open circuit)

This is used for:
- **DC coupling**: Blocking DC bias while passing AC signals
- **Filtering**: Removing noise that's superimposed on DC

### AC Behavior

In AC (alternating current, time-varying voltage):
- Voltage across capacitor constantly changes
- Capacitor constantly charges and discharges
- **Current continuously flows** (even though no charge reaches the dielectric)
- The capacitor passes AC (acts like it conducts AC)

The **impedance** (AC resistance) of a capacitor is:

$$X_C = \frac{1}{2\pi f C}$$

Where:
- XC = capacitive reactance (impedance, in ohms)
- f = frequency (in Hz)
- C = capacitance (in farads)

**Key insight**: At high frequencies, capacitive impedance is low (capacitor acts conductive). At low frequencies, impedance is high (capacitor acts resistive).

### Practical Example

A 1 µF capacitor:
- At 100 Hz: Impedance = 1/(2π × 100 × 10⁻⁶) ≈ 1600Ω
- At 1 kHz: Impedance ≈ 160Ω
- At 10 kHz: Impedance ≈ 16Ω
- At 1 MHz: Impedance ≈ 0.16Ω

The capacitor becomes more "conductive" as frequency rises.

## THINK ABOUT IT
> Why does a capacitor block DC but pass AC?

> Hint: DC is a constant voltage, so the capacitor charges once and then... nothing happens. AC is constantly changing, so the capacitor is constantly charging and discharging. This charge and discharge *is* the current.

## The Dielectric: Heart of the Capacitor

The material between the capacitor plates is called the **dielectric**. Its properties determine:

- **Capacitance value**: Higher dielectric constant = higher capacitance for same physical size
- **Voltage rating**: Dielectric breakdown voltage limits how much voltage it can withstand
- **Leakage**: How much the capacitor loses charge over time
- **Temperature stability**: How much capacitance changes with temperature
- **Frequency response**: How well it works at high frequencies

### Common Dielectrics

| Type | Dielectric Material | Relative Permittivity | Typical Use |
|------|---------------------|----------------------|-------------|
| Ceramic | Ceramic powder (titanium dioxide, etc.) | 100–10,000 | General purpose |
| Film | Plastic polymer (polypropylene, polyester) | 2–4 | AC signals, precision |
| Electrolytic | Aluminum oxide or tantalum oxide | 10–100 | Large values, power |
| Mica | Mica mineral | 5–7 | High precision, high Q |

Different dielectrics have different properties, which is why capacitor types matter (covered in next section).

## Practical Capacitor Models

### Ideal Capacitor
- Only capacitance
- No resistance
- Perfect dielectric (no leakage)
- Works perfectly at all frequencies

### Real Capacitor
- **Main capacitance** (what you paid for)
- **Leakage resistance** (charge slowly leaks away)
- **Series resistance** (ESR—Equivalent Series Resistance, from leads and plates)
- **Parasitic inductance** (from leads and plate geometry)
- **Frequency dependence** (impedance changes with frequency)

These real-world effects are explored in later sections.

## Capacitance in Series and Parallel

### Parallel Connection
When capacitors are connected in parallel, total capacitance **adds**:

$$C_{total} = C_1 + C_2 + C_3 + ...$$

This is opposite to resistors in parallel! Parallel capacitors behave like bigger plates, storing more charge.

### Series Connection
When capacitors are connected in series, total capacitance decreases:

$$\frac{1}{C_{total}} = \frac{1}{C_1} + \frac{1}{C_2} + \frac{1}{C_3} + ...$$

The smallest capacitance dominates.

**Practical example**: Two 10 µF in series = 5 µF

This is used to handle higher voltages (two capacitors rated for 50V can work with up to 100V if in series, assuming balanced voltage division).

## Voltage Rating and Why It Matters

Every capacitor has a **voltage rating**—the maximum voltage you can safely apply.

This rating is determined by the dielectric breakdown voltage. If you exceed this:
1. Voltage becomes strong enough to ionize the dielectric
2. Capacitor becomes conductive (short circuit)
3. Current surges, generating heat
4. Capacitor often fails explosively

**Unlike resistors where exceeding power rating is bad, exceeding capacitor voltage rating is catastrophic and immediate.**

## Polarity: A Critical Concept

### Unpolarized Capacitors
- Film and ceramic capacitors (usually)
- Can be connected either way
- No polarity marking

### Polarized Capacitors
- Electrolytic and tantalum capacitors (usually)
- Have + and - marks
- **Must be connected correctly**
- Reversing polarity causes immediate failure (often violently)

## Key Takeaway

**Capacitance is the ability to store charge. Capacitors charge and discharge based on applied voltage, block DC but pass AC, and store energy that can be released later.**

Understanding capacitors means:
- Knowing they store charge proportionally to applied voltage
- Understanding RC time constants for timing
- Recognizing that they pass AC but block DC
- Respecting voltage ratings
- Understanding that all real capacitors leak and degrade

Next: Why different capacitor types exist and how to choose between them.
