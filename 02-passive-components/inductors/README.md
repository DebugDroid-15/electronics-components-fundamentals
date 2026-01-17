# Inductors: Section Overview

## What This Section Covers

Inductors are the third fundamental passive component. While resistors dissipate energy and capacitors store it electrically, inductors **store energy in a magnetic field**.

In this section, you'll learn:
- What inductance is and the physical concept of magnetic energy storage
- How inductors work (intuitive understanding, not deep physics)
- Why different inductor types exist
- Real-world limitations and behaviors
- Common mistakes with inductors
- When and why you use inductors

## Why Inductors Are Important (But Rarely Used by Beginners)

Inductors are less common in beginner circuits than resistors or capacitors. But they're essential in:
- **Power supplies**: Switching regulators, energy transfer
- **Filters**: Frequency filtering (especially with capacitors)
- **RF circuits**: Tuning, matching, transmission lines
- **Energy harvesting**: Transformers, coupled circuits
- **Impedance matching**: Adapting signals between circuits

Understanding inductors completes your passive component knowledge.

## This Section Is Organized As:

1. **inductor-basics.md** — What is inductance? Energy storage. Fundamental concepts.
2. **inductor-types.md** — Different inductor designs and their trade-offs
3. **current-rating-and-saturation.md** — Why inductors have limits, what saturation means
4. **losses-and-q-factor.md** — Non-ideal effects: resistance, Q factor, efficiency
5. **real-world-behavior.md** — Frequency effects, temperature effects, parasitic capacitance
6. **common-mistakes.md** — The pitfalls unique to inductors

## Suggested Study Path

### Recommended Approach (Sequential)

Read files in this order:
1. inductor-basics.md → Understand magnetic energy storage
2. inductor-types.md → See the variety
3. current-rating-and-saturation.md → Understand saturation limits
4. losses-and-q-factor.md → Learn about efficiency and Q factor
5. real-world-behavior.md → Understand parasitic effects
6. common-mistakes.md → Learn where people slip up

**Estimated time: 1.5–2.5 hours**

### Quick Reference Approach

If you have some inductor background:
- Skim inductor-basics.md
- Review inductor-types.md
- Focus on current-rating-and-saturation.md
- Read losses-and-q-factor.md carefully
- Scan common-mistakes.md

**Estimated time: 45 minutes**

## Core Concepts You'll Learn

By the end of this section, you should understand:

✓ **Inductance**: What it means magnetically  
✓ **Energy Storage**: How L = ½ × L × I²  
✓ **Impedance at Different Frequencies**: How inductor behaves from DC to RF  
✓ **Self-Inductance**: How inductors affect themselves  
✓ **Mutual Inductance**: How inductors couple to each other  
✓ **Saturation**: Why current has limits  
✓ **Resistance and Q Factor**: Real inductors aren't lossless  
✓ **Parasitic Effects**: Capacitance and resistance in real inductors  
✓ **Temperature Effects**: How heat changes behavior  

## Key Questions This Section Answers

- What physically is inductance? How is it different from capacitance?
- Why do inductors oppose changes in current?
- Why do inductors have current limits (saturation)?
- What's the difference between a coil and a transformer?
- What is Q factor and why does it matter?
- When would you use an inductor instead of a capacitor?
- What causes inductor core saturation?
- How do frequency effects differ from capacitors?
- When and why do inductors fail?

## Prerequisites

- Understanding resistors and capacitors thoroughly
- Basic understanding of magnetic fields (conceptual, not mathematical)
- Algebra

## Common Misconceptions Addressed

**"Inductors are just coils, resistors are just wire, capacitors are just plates"**  
True conceptually, but the devil is in the details. Each component type has complex real-world behavior.

**"Inductors are like capacitors with current instead of voltage"**  
Conceptually useful analogy, but breaks down. Inductors resist changes in current; capacitors resist changes in voltage.

**"All inductors are the same, just different values"**  
False. Different core materials have vastly different properties (air core, iron core, ferrite core).

**"Saturation is rare, most circuits avoid it"**  
False. Saturation is common in power converters and is a limiting factor in many designs.

## Real-World Context

After this section, you'll understand:
- How switching power supplies use inductors to regulate voltage
- Why transformers (coupled inductors) exist and how they work conceptually
- How LC circuits filter signals
- Why RF circuits use inductors for tuning
- How transformer saturation causes power supply failure
- Why inductor selection is critical in switching power supplies

## What Happens Next

After passive components (resistors, capacitors, inductors), you'll move to:
- **Active Components**: Transistors and diodes that switch and amplify
- **Real Circuits**: How R, C, L work together
- **System Design**: Building practical circuits

Inductors are the least-used passive component in beginner circuits, but essential for understanding power electronics and RF.

---

**Ready to start?** Open **inductor-basics.md** to learn what inductance really is.
