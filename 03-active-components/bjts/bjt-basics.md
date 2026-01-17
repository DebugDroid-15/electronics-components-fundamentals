# BJTs: Detailed Files Reference

This section contains comprehensive BJT information across 5 files:
1. bjt-basics.md (overview, three terminals, current amplification)
2. operating-regions.md (cutoff, active, saturation)
3. practical-usage.md (switching, amplification, real circuits)
4. common-mistakes.md (design errors)

## Summary

**BJTs** are semiconductor devices with three terminals (emitter, base, collector) that allow a small base current to control a large collector current.

**Key equation**: IC = hFE × IB

**Two types**: NPN (common) and PNP (complementary)

**Three operating modes**:
1. **Cutoff**: Off (IB ≈ 0)
2. **Active**: Amplifying (IB × hFE = IC)
3. **Saturation**: On (fully conducting)

**Common uses**: Audio amplifiers, switching circuits, sensors

**Advantages**: Good audio properties, well-understood technology, available everywhere

**Disadvantages**: Require base current control, slower than MOSFETs, higher power dissipation

**Real-world considerations**: Temperature effects on gain, frequency limitations, heat management, base-emitter voltage drop (~0.7V), collector-emitter saturation voltage (~0.2V)

**Professional BJT Design Practices**:
1. Size for 2-3× margin on base current
2. Add flyback diode when switching inductive loads
3. Use heatsink for power applications
4. Account for temperature effects on gain
5. Test at temperature extremes
6. Choose transistor type appropriate for application

**Common BJT Types**:
- 2N3904/2N3906: Small signal (universal)
- 2N2222/2N2907: Fast switching
- 2N3055/2N2955: Power transistors (15A+)
- TIP41/TIP42: Medium power
- Darlingtons: Extra gain (2 transistors in one)

**When to Use BJTs**:
- Audio applications (good frequency response)
- Sensor amplification
- Logic switching
- Switching relays/solenoids
- Where base current control is acceptable

**Trending**: Being replaced by MOSFETs in new designs due to speed and efficiency advantages.

---

See detailed files for complete information on each topic.
