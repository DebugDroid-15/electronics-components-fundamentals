# Capacitors: Section Overview

## What This Section Covers

Capacitors are the second fundamental passive component. While resistors dissipate energy as heat, capacitors **store electrical energy** temporarily.

In this section, you'll learn:
- What capacitance is and the fundamental concept of charge storage
- How capacitors work (not deep physics, but intuitive models)
- Capacitor types and why different types exist
- How voltage and temperature affect capacitors
- Real-world limitations (leakage, aging, reliability)
- Common mistakes and misunderstandings

## Why Capacitors Are Important

Capacitors are used in almost every circuit:
- **Power supplies**: Filtering and energy buffering
- **Signal processing**: Coupling and blocking DC
- **Timing circuits**: Oscillators and pulse generation
- **Audio**: Coupling amplifiers and filtering
- **Digital circuits**: Decoupling (removing noise)
- **Energy storage**: Camera flashes, touch screens

Understanding capacitors is essential before moving to active components.

## This Section Is Organized As:

1. **capacitor-basics.md** — What is capacitance? Charge storage. Fundamental concepts.
2. **capacitor-types.md** — Different capacitor technologies and their trade-offs
3. **voltage-and-temperature-effects.md** — How voltage and heat change capacitor behavior
4. **leakage-and-aging.md** — Non-ideal effects: why capacitors lose charge and degrade
5. **real-world-behavior.md** — Parasitic effects, equivalent series resistance (ESR), frequency response
6. **common-mistakes.md** — The pitfalls you'll encounter

## Suggested Study Path

### Recommended Approach (Sequential)

Read files in this order:
1. capacitor-basics.md → Understand what capacitance is
2. capacitor-types.md → See the variety of capacitor types
3. voltage-and-temperature-effects.md → Understand environmental effects
4. leakage-and-aging.md → Learn the failure mechanisms
5. real-world-behavior.md → Understand parasitic effects
6. common-mistakes.md → Learn where people slip up

**Estimated time: 2–3 hours**

### Quick Reference Approach

If you have some capacitor background:
- Skim capacitor-basics.md
- Review capacitor-types.md for unfamiliar types
- Focus on leakage-and-aging.md
- Read real-world-behavior.md carefully
- Scan common-mistakes.md

**Estimated time: 45 minutes**

## Core Concepts You'll Learn

By the end of this section, you should understand:

✓ **Capacitance**: What it means to "store charge"  
✓ **Charge and Energy**: The relationships Q = C × V and E = ½ × C × V²  
✓ **Dielectric Constant**: How material affects capacitance  
✓ **Voltage Ratings**: Why capacitors have voltage limits  
✓ **Leakage Current**: Why capacitors don't stay charged forever  
✓ **Aging**: How capacitors degrade over time  
✓ **Equivalent Series Resistance (ESR)**: Real capacitors aren't perfect  
✓ **Impedance at Different Frequencies**: How capacitor behavior changes with frequency  
✓ **Reliability**: Why capacitor failures are common in real systems  

## Key Questions This Section Answers

- What does "capacitance" really mean, physically?
- Why do capacitors work as filters?
- How much charge does a capacitor store?
- Why does capacitance have a voltage rating?
- What's the difference between a ceramic capacitor and an electrolytic capacitor?
- Why does a capacitor lose charge over time (leakage)?
- What is ESR and why does it matter?
- Why do old electronics have failed capacitors?
- How do you choose a capacitor for a specific application?
- What causes capacitor explosions?

## Prerequisites

- Understanding of voltage and current (from Section 01)
- Understanding of resistance from resistor section
- Basic algebra

## Common Misconceptions Addressed

**"A capacitor is like a battery—it stores charge and you can use it later"**  
Partially true, but capacitors leak charge and work best in AC/switching circuits, not long-term DC storage.

**"Once a capacitor is charged, it stays charged"**  
False. All real capacitors leak charge over time, especially when warm.

**"All capacitors are the same, just different values"**  
False. Different technologies (ceramic, film, electrolytic) have vastly different properties.

**"Capacitors are either good or bad"**  
False. They degrade gradually. Old capacitors might have 10% less capacitance and higher leakage, causing circuit failures.

**"Voltage rating isn't critical—it just should be higher than the supply"**  
False. Exceeding voltage rating causes immediate failure, sometimes explosively.

## Real-World Context

After this section, you'll understand:
- Why power supplies use large electrolytic capacitors
- How ceramic capacitors "decouple" noise from power supplies
- Why old computers have capacitor failure issues
- How capacitors work with resistors to filter signals
- Why capacitors fail in hot environments
- How to choose capacitor type for different applications

## What Happens Next

After mastering capacitors, you'll move to:
- **Inductors**: Energy storage in magnetic fields
- **Active Components**: Transistors and diodes that switch and amplify
- **Real Circuits**: How R, L, C work together

Capacitors are the second foundation. Resistors + Capacitors = RC circuits, which are everywhere.

---

**Ready to start?** Open **capacitor-basics.md** to learn what capacitance really is.
