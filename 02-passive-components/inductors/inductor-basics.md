# Inductor Basics: Magnetic Energy Storage

## The Core Concept: What Is Inductance?

An **inductor** is a component that opposes changes in electric current flowing through it. It stores electrical energy as a **magnetic field**.

When current starts to flow through an inductor:
- Magnetic field builds around it
- Building the field takes energy (stored energy)
- When current tries to change (increase or decrease), the magnetic field opposes that change
- This opposition to change is inductance

**Inductance** is measured in **henries (H)**. The unit is named after Joseph Henry, an early researcher in electromagnetism.

## The Fundamental Relationship

The voltage across an inductor is related to how fast current is changing:

$$V = L \times \frac{dI}{dt}$$

Where:
- V = voltage across inductor
- L = inductance (henries)
- dI/dt = rate of change of current (amperes per second)

**Key insight**: An inductor only has voltage across it when current is **changing**. If current is constant (DC), there's no voltage drop (ideal inductor).

### Practical Example

An inductor with L = 1 henry experiences:
- 1 ampere per second change in current → 1 volt appears across it
- 10 amperes per second change → 10 volts appears
- Constant current (no change) → 0 volts

This is opposite to resistors (voltage depends on current magnitude) and capacitors (voltage doesn't directly cause current).

## Energy Storage in an Inductor

When current flows through an inductor, energy is stored in the magnetic field:

$$E = \frac{1}{2} \times L \times I^2$$

Where:
- E = energy (joules)
- L = inductance (henries)
- I = current (amperes)

**Practical example**:
- 1 henry inductor with 1 ampere flowing through it stores:
  - E = ½ × 1 × 1² = 0.5 joules
- If current increases to 2 amperes: E = ½ × 1 × 4 = 2 joules

The energy increases with the square of current—doubling current stores 4× energy.

## DC vs. AC Behavior

### DC Behavior

In DC (constant current):
- Inductor current doesn't change (dI/dt = 0)
- V = L × 0 = 0 volts
- Inductor has no voltage drop
- **Inductor looks like a short circuit (wire) in DC**

This is why you can't just connect an inductor to a battery—it would look like a wire, current would surge, and the wire resistance would limit it.

### AC Behavior

In AC (time-varying current):
- Current constantly changes (dI/dt ≠ 0)
- Voltage appears across the inductor
- Inductor **impedes** current flow (acts like resistance)

The **inductive reactance** (impedance) is:

$$X_L = 2\pi f L$$

Where:
- XL = inductive reactance (ohms)
- f = frequency (Hz)
- L = inductance (henries)

**Key insight**: At higher frequencies, inductive impedance increases. A 1 Henry inductor:
- At 60 Hz: XL = 2π × 60 × 1 ≈ 377Ω
- At 1 kHz: XL ≈ 6,283Ω
- At 1 MHz: XL ≈ 6,283,185Ω

At MHz frequencies, inductors are highly resistive to current flow.

## THINK ABOUT IT
> Why does an inductor oppose changes in current?

> Hint: Lenz's law. When current tries to increase, the magnetic field increases, creating a magnetic field that opposes the current increase. When current tries to decrease, the magnetic field opposes the decrease. The inductor "fights" any change in current.

## Inductors vs. Capacitors: Duality

Inductors and capacitors have complementary (dual) behavior:

| Property | Resistor | Capacitor | Inductor |
|----------|----------|-----------|----------|
| Opposes... | Voltage (V = IR) | Voltage change | Current change |
| DC behavior | Conducts | Open circuit (blocks) | Short circuit (conducts) |
| AC impedance | R (constant) | XC ↓ with frequency | XL ↑ with frequency |
| Stores... | Heat | Electric field | Magnetic field |
| Phase shift | None | -90° | +90° |

This duality is useful: Many circuit analysis techniques work for both, just with roles swapped.

## Physical Construction

An inductor is physically a **coil of wire**. The simplest inductor is just a wire wound into multiple loops.

The inductance depends on:
1. **Number of turns** (N): More loops = more inductance (proportional to N²)
2. **Loop area** (A): Larger loops = more inductance
3. **Core material**: What's inside the loop (air, iron, ferrite)
4. **Loop length** (l): How spread out the coil is

**Formula (simplified)**:
$$L = \mu_0 \mu_r \frac{N^2 A}{l}$$

Where:
- μ₀ = permeability of free space (constant)
- μᵣ = relative permeability of core material
- N = number of turns
- A = cross-sectional area
- l = length of core

**Practical insight**: Iron cores have much higher μᵣ than air (iron ≈ 100–10,000; air ≈ 1), so iron core inductors are much smaller and more efficient than air core for the same inductance.

## Inductance in Series and Parallel

### Series Connection
Inductances add like resistors in series:
$$L_{total} = L_1 + L_2 + L_3 + ...$$

**Exception**: If inductors are magnetically coupled, this formula doesn't apply directly. (Advanced topic, not covered here.)

### Parallel Connection
Inductances add like resistors in parallel (inverse sum):
$$\frac{1}{L_{total}} = \frac{1}{L_1} + \frac{1}{L_2} + \frac{1}{L_3} + ...$$

## Practical Inductor Values and Ranges

Real inductors come in values:
- **Small**: 1 nH to 1 µH (used in RF circuits, high frequencies)
- **Medium**: 1 µH to 1 mH (power supply regulators, audio)
- **Large**: 1 mH to 100 H+ (power supplies, transformers)

The range is enormous compared to resistors or capacitors, because applications vary widely.

## Current Rating

Unlike resistors (power rating) or capacitors (voltage rating), inductors have a **current rating**:

- This is the maximum DC current the inductor can handle before it **saturates**
- Saturation is unique to inductors with magnetic cores
- We'll cover this in detail in a later section

## Key Takeaway

**Inductance is the property of opposing changes in current. Inductors store energy in magnetic fields and are characterized by their response to current changes.**

Understanding inductors means:
- Knowing they're essentially coils of wire
- Understanding they oppose current changes (not current itself)
- Recognizing they have zero impedance in DC but high impedance in AC
- Knowing they store energy magnetically

Next: Why different inductor types exist and how to choose between them.
