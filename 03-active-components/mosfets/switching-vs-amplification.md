# MOSFETs: Switching vs. Amplification

## Primary Use: Switching (99% of Applications)

MOSFETs are designed and optimized for **switching** (on/off), not linear amplification.

### Why MOSFETs Excel at Switching

**Low on-resistance (RDS(on))**:
- When on: Resistance is milliohms to ohms
- Power dissipation = I² × RDS(on) (very small)
- Example: 10A through 0.1Ω MOSFET → 10W (very efficient)

**Fast transitions**:
- Microseconds to nanoseconds
- Enables high-frequency switching (kHz to MHz easily)
- Switching power supplies rely on this

**Binary behavior**:
- Voltage control (not current)
- Either fully on or fully off
- No linear region needed

**Gate impedance**:
- Essentially capacitive
- No continuous current needed
- Logic circuits can drive directly (with careful design)

### Switching Circuit Example: Motor Control

```
        VCC (+12V)
         |
    [Motor 1A]
         |
    Drain (D)
         |
    [ NMOS ]
         |
    Source (S)
         |
       Ground

    Gate (G) <- PWM signal (0-5V, 10kHz)
```

**Operation**:
- Gate = 0V: MOSFET off, motor stops
- Gate = 5V: MOSFET on, motor runs at full speed
- Gate = PWM (varying duty cycle): Motor runs at variable speed

**Power dissipation**:
- Off: ≈ 0W (no current)
- On: 1A² × 0.1Ω = 0.1W (minimal, efficient)
- Total: 5–10mW average (excellent)

### Switching Applications (Where MOSFETs Dominate)

**1. Switching Power Supplies (Buck, Boost, Flyback)**
- MOSFET switches at kHz–MHz
- Inductor stores/releases energy
- Highly efficient (85–95%)
- All modern chargers, power adapters use MOSFETs

**2. Motor Control (PWM)**
- PWM signal drives gate
- MOSFET switches motor current on/off rapidly
- Speed controlled by duty cycle
- Extremely efficient

**3. Digital Logic (CMOS)**
- CPU/GPU: Billions of MOSFETs
- Switching between 0V and VCC
- Power consumption from switching transients
- Modern electronics depend entirely on this

**4. Relay/Solenoid Drivers**
- Digital signal drives MOSFET gate
- MOSFET switches 24V or 48V coil current
- Fast switching enables fast relay response

**5. LED Dimming**
- PWM signal controls brightness
- MOSFET switches LED current
- Works at 1kHz (human eye can't see flicker)

---

## Secondary Use: Amplification (Rare, Specialist Applications)

MOSFETs **can** be used for linear amplification but are **not optimal** compared to alternatives:

### Why Amplification Is Possible

**Linear region exists**:
- Between fully off and fully on
- Drain current varies smoothly with gate voltage
- Can amplify small signals to larger signals

**Voltage gain possible**:
- Gain ≈ gm × RD (depends on biasing and drain resistor)
- Typical gain: 1–10 (much lower than BJT or op-amp)

### MOSFET Amplifier Advantages

1. **Very high input impedance** (gate is capacitive, essentially infinite DC impedance)
2. **Low input current** (only capacitive transient current during switching)
3. **Can operate at very high frequencies** (MHz to GHz)
4. **High input impedance reduces loading on source**

### MOSFET Amplifier Disadvantages

1. **Low gain** compared to BJT (BJT: 50–200, MOSFET: 1–10 typical)
2. **Poor linearity** (gain varies with operating point)
3. **Temperature-dependent** (RDS(on) and Vth vary with temperature)
4. **Complex biasing** (need to establish Q-point carefully)
5. **Lower bandwidth** than specialized RF transistors
6. **More noise** than carefully designed op-amp circuits

### When MOSFET Amplification Is Used

**1. RF Amplifiers (Very High Frequency)**
- MOSFETs work up to GHz frequencies
- BJTs have frequency limitations
- Specialized RF MOSFETs designed for this
- Used in wireless, satellite, radar

**2. High-Input-Impedance Buffers**
- Electrometers and sensors need ultra-high impedance
- MOSFET buffer allows connection without loading
- Specialized low-leakage MOSFETs (JFET similar)

**3. Parametric Amplifiers**
- Specialized RF application
- Gain by varying capacitance with clock
- Advanced technique

**4. Transimpedance Amplifiers**
- Photodiode amplifiers (light sensing)
- High input impedance crucial
- Often use JFET or MOSFET input for low input capacitance
- Followed by op-amp for low-noise gain

### MOSFET Amplifier Example: Cascode RF Buffer

```
Input signal (high impedance source)
    |
    [Source follower MOSFET]
    |
    +---> Output (lower impedance, buffered)
```

- Input impedance: Very high (gate capacitance only)
- Output impedance: Low (reduced by source follower configuration)
- Gain: Close to 1 (buffers, doesn't amplify much)
- Used: RF circuits where impedance matching critical

---

## MOSFET vs. BJT vs. Op-Amp for Amplification

| Feature | MOSFET | BJT | Op-Amp |
|---------|--------|-----|--------|
| Input impedance | Extremely high | Moderate (kΩ) | Very high (non-inv) |
| Voltage gain | Low (1–10) | Moderate (10–200) | Very high (1000+) |
| Input current | Essentially zero | nanoamps (base) | Picoamps |
| Frequency | MHz to GHz | DC to few MHz | DC to MHz |
| Linearity | Moderate | Good | Excellent |
| Noise | Moderate | Low | Very low (with care) |
| Simplicity | Complex (biasing) | Simple (3 resistors) | Simple (op-amp IC) |
| Power efficiency | Excellent | Good | Fair (draws quiescent current) |
| Preferred for amplification | NO (use BJT or op-amp) | YES (low noise) | YES (most apps) |

---

## Why Not Use MOSFETs for Amplification?

1. **Op-amps exist** (cheaper, simpler, more stable)
2. **Op-amps have higher gain** (1000+ vs. 1–10 for MOSFET)
3. **Op-amps have better linearity** (designed for this purpose)
4. **BJTs work well for audio** (better gain, well-understood)
5. **MOSFETs are for switching** (what they're optimized for)

The **"if it's not switching, why are you using a MOSFET?"** principle guides electronics design.

---

## Switching Dominates Modern Electronics

### By the Numbers
- **Switching applications**: >99% of MOSFET usage
- **Amplification applications**: <1%, mostly specialized RF
- **Trend**: MOSFETs increasingly displace other technologies in switching
- **Future**: More MOSFETs integrated into power-on-chip designs

### Why Switching Dominates
1. **Efficiency**: Switching is more efficient than linear (where heat is wasted)
2. **Integration**: Billions of MOSFETs on single chip (CPU, GPU)
3. **Power supplies**: All switching power supplies use MOSFETs
4. **Cost**: Switching designs can be cheaper (no bulky heat sinks for linear)
5. **Modern digital**: Everything is digital/switching (not analog)

---

## Professional Design Perspective

### For Switching Applications
**MOSFETs are the obvious choice:**
- Fast switching
- High efficiency
- Widely available
- Well-understood
- Best tools available (gate drivers, simulation)

### For Amplification Applications
**Choose based on requirement:**
- **Low-noise audio**: Use BJT or op-amp
- **Very high frequency (RF)**: Specialized RF MOSFET or BJT
- **Very high input impedance**: MOSFET or JFET
- **General purpose**: Op-amp (easiest, most robust)

The rule: **"Use the tool optimized for the job"**
- MOSFETs optimized for switching
- Op-amps optimized for amplification
- BJTs good at both (historical technology)

---

## Key Takeaway

**MOSFETs are optimized for switching (on/off) and dominate power electronics due to efficiency and speed. While MOSFETs can amplify, they're not optimal for this application—use BJT or op-amp for linear amplification instead. The 99/1 split (switching vs. amplification) defines MOSFET usage in modern electronics.**
