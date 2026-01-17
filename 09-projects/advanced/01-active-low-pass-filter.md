# Advanced Project 1: Active Low-Pass Filter (Op-Amp Based)

**Difficulty**: ⭐⭐⭐ (Advanced)  
**Time**: 90 minutes  
**Concept**: Op-amp feedback, frequency response, filter design, Butterworth characteristics

## What You'll Learn

- Op-amp negative feedback principles
- Frequency response and Bode plots
- Butterworth filter design
- Active vs. passive filtering advantages
- Stability and compensation
- Real-world audio/measurement filtering

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| Op-Amp IC | 1 | TL072, LM358, or OPA2134 |
| Resistors | 4 | 1kΩ, 10kΩ (1% tolerance recommended) |
| Capacitors | 2 | 100nF, varies by cutoff frequency |
| Potentiometer | 1 | 10kΩ variable (optional, for gain tuning) |
| Power Supply | 1 | Dual ±5V to ±15V (or single supply with offset) |
| Function Generator | 1 | 1Hz to 100kHz sine wave |
| Oscilloscope | 1 | 2-channel minimum |
| Breadboard | 1 | Standard |

## Theory: Active Filtering

### Why Active Filters?

**Passive filters** (RC circuits):
- Simple (2 components)
- No power needed
- Limited dynamic range (voltage divider effect)
- Attenuation at passband

**Active filters** (op-amp + RC):
- Can have gain (amplification)
- Sharp rolloff (higher order)
- Buffered output (low impedance)
- No loading effects

### Butterworth Low-Pass Filter

**Characteristics**:
- Maximally flat passband (no ripple)
- -3dB point at cutoff frequency (-3dB = 0.707V output)
- -20dB/decade rolloff (first-order)
- -40dB/decade rolloff (second-order)

**First-order equation**:
$$\frac{V_{out}}{V_{in}} = \frac{1}{\sqrt{1 + (f/f_c)^2}}$$

Where f_c = cutoff frequency = 1/(2πRC)

**Cutoff frequency** (f_c):
$$f_c = \frac{1}{2\pi RC}$$

Example: R = 10kΩ, C = 100nF
$$f_c = \frac{1}{2\pi \times 10000 \times 0.0000001} = 159 Hz$$

## Op-Amp Configuration: Non-Inverting Low-Pass

**Circuit**: Standard non-inverting amplifier with capacitor feedback (Miller effect).

```
     +5V (or ±power)
      |
     [+15V]
      |
In ---[R1]---+---[Cfb]---+--- Out
             |           |
             [Op-Amp+]   [Load]
                 |
                [R2]---+---GND
                       |
                     [-15V]
                      |
                     GND
```

**Gain**: A = 1 + Rf/Rg (unity gain if Rf = open, Rg = GND)

**Feedback capacitor** (Cfb) creates frequency-dependent impedance:
$$Z_f = \frac{1}{2\pi f C}$$

At DC: Z_f = ∞ (high impedance, feedback open, gain = 1 + Rf/Rg)
At high frequency: Z_f ≈ 0 (short circuit, gain = 1)

## Breadboard Layout - Unity-Gain Butterworth

```
      +15V
        |
   [100nF Cfb]
        |
In --[10kΩ]--+--[TL072 Output]--+--Out
             |                  |
             [Op-Amp input+]    |
             [Op-Amp input-]----+
                   |
                  GND
         [Negative feedback]

Connections:
Pin 1: Input +
Pin 2: Feedback -
Pin 3: GND
Pin 4: -15V
Pin 5: +15V
Pin 6: Output
Pin 7: (tied to GND)
Pin 8: (tied to +15V)
```

## Building Instructions

### Part 1: Set Up Power Supply

1. **Connect dual supply**:
   - Op-amp requires ±15V (or ±5V minimum)
   - Connect +15V to pin 8
   - Connect -15V to pin 4
   - Connect GND to pin 3 (reference)

2. **Add bypass capacitors**:
   - 100µF + 100nF on +15V rail (near IC)
   - 100µF + 100nF on -15V rail (near IC)
   - Essential for stability!

### Part 2: Build Filter Network

1. **Insert input resistor**:
   - Insert 10kΩ resistor from signal input to inverting input (pin 2)

2. **Insert feedback capacitor**:
   - Insert 100nF capacitor from output (pin 6) to inverting input (pin 2)
   - This creates the cutoff frequency

3. **Connect non-inverting input**:
   - Connect pin 3 (non-inverting) directly to GND

4. **Close feedback loop**:
   - Connect output (pin 6) to input capacitor
   - This creates negative feedback

### Part 3: Connect Test Equipment

1. **Function generator input**:
   - Connect to input resistor (before 10kΩ)
   - Start with 100mV amplitude
   - 1kHz test frequency

2. **Oscilloscope channel 1**:
   - Probe input signal (at resistor input)
   - Measure amplitude, frequency

3. **Oscilloscope channel 2**:
   - Probe output (pin 6)
   - Measure amplitude, phase shift

## Measurement Plan - Frequency Response

Sweep frequency from 10Hz to 100kHz and record gain and phase:

| Frequency | Input V | Output V | Gain (V_out/V_in) | Gain (dB) | Phase |
|-----------|---------|----------|-------------------|-----------|-------|
| 10 Hz | 100mV | _____ | _____ | _____ | _____ |
| 100 Hz | 100mV | _____ | _____ | _____ | _____ |
| 159 Hz | 100mV | _____ | _____ | -3dB | -45° |
| 500 Hz | 100mV | _____ | _____ | _____ | _____ |
| 1 kHz | 100mV | _____ | _____ | _____ | _____ |
| 10 kHz | 100mV | _____ | _____ | _____ | _____ |
| 100 kHz | 100mV | _____ | _____ | _____ | _____ |

### Gain Calculations

Gain (linear):
$$G = \frac{V_{out}}{V_{in}}$$

Gain (dB):
$$G_{dB} = 20 \log_{10}(G)$$

At -3dB point: G = 0.707 (70.7% of input)

### Phase Shift Measurement

Use oscilloscope to measure phase difference:
$$\text{Phase} = \frac{\Delta t}{T} \times 360°$$

Where:
- Δt = time difference between zero crossings
- T = period of signal

At cutoff frequency: Phase = -45°

## Bode Plot Construction

Plot measured data on graph:

**X-axis**: Frequency (log scale, 10Hz to 100kHz)
**Y-axis (top)**: Gain in dB (-20 to +20)
**Y-axis (bottom)**: Phase (-90° to 0°)

**Expected shape**:
- Below 159Hz: Flat response (0dB, 0° phase)
- At 159Hz: -3dB point, -45° phase
- Above 159Hz: -20dB/decade slope (single pole)
- High frequencies: Approaches -90° phase (lag)

## Visual Verification

**Oscilloscope observations**:
- ✓ At 10Hz: Output same amplitude as input, no phase shift
- ✓ At 159Hz: Output reduced to 70.7% amplitude, 45° phase lag
- ✓ At 1kHz: Further reduced amplitude (~55%), more phase lag (~70°)

## Key Insights

### Negative Feedback

**Feedback factor** (β):
$$\beta = \frac{1}{1 + f/f_c}$$

This feedback mechanism:
- Stabilizes gain (less dependent on op-amp A₀)
- Reduces distortion (increases linearity)
- Extends bandwidth (trades off with gain)

### Frequency-Dependent Impedance

Capacitor impedance (XC):
$$X_C = \frac{1}{2\pi f C}$$

- At DC (f=0): X_C = ∞ (open circuit)
- At f_c: X_C = R (equal to resistance)
- At high f: X_C ≈ 0 (short circuit)

This frequency dependence creates automatic filter action.

### Pole Placement

This is a **single-pole filter**:
- One capacitor = one pole
- -20dB/decade rolloff
- Transfer function: H(s) = ω_c / (s + ω_c)

For steeper rolloff:
- Add second capacitor stage → -40dB/decade
- Or use higher-order design

## Practical Applications

**Audio**: Remove high-frequency noise, prevent aliasing
**Measurement**: Filter 60Hz/50Hz mains interference
**Data acquisition**: Anti-aliasing before ADC
**Power supplies**: Smooth noisy rectified DC

## Stability Analysis

**Potential oscillation** (op-amp ringing):
1. Capacitive output load
2. Parasitic inductance in wires
3. Insufficient damping

**Stabilization**:
- Add small series resistor (100Ω) at output
- Ensure good bypass capacitors on power
- Keep connections short
- Use star grounding

## Advanced Variations

### Higher Cutoff Frequency
Change capacitor to smaller value (10nF for ~1.6kHz)
$$f_c = \frac{1}{2\pi \times 10000 \times 0.00000001} = 1591 Hz$$

### Different Op-Amp Topologies
- **Inverting**: Same filter behavior, inverts signal
- **Sallen-Key**: Two-pole filter, no inversion
- **Multiple feedback**: More complex frequency response

### Second-Order Butterworth
Add second RC stage:
- Steeper rolloff (-40dB/decade)
- Better high-frequency rejection
- More complex design

## Troubleshooting

**No output signal**:
- Power supply not connected (check both ± rails)
- Capacitor backwards (nonpolar capacitor assumed)
- Op-amp damaged (test with DC offset)

**Oscillation (ringing/instability)**:
- Add 100Ω resistor in series with output
- Add capacitor across input resistor (1nF)
- Check power supply bypass capacitors

**Gain wrong**:
- Verify capacitor value (look at label)
- Check all connections solid
- Measure frequency with oscilloscope directly

**Cutoff frequency wrong**:
- Measure actual R and C values (use meter)
- Calculate: f_c = 1/(2πRC)
- Component tolerance affects frequency

## Challenge Extensions

1. **Design different cutoff frequency**:
   - Choose new cutoff frequency (1kHz, 10kHz)
   - Calculate required C: C = 1/(2πRf_c)
   - Build and measure
   - Verify Bode plot matches prediction

2. **Add adjustable gain**:
   - Replace feedback resistor with potentiometer
   - Gain = 1 + Rf/Rg
   - Adjust gain and verify effect on response

3. **Build second-order filter**:
   - Add second RC section
   - Cutoff frequency same, but steeper rolloff
   - Compare -20dB/dec vs -40dB/dec

4. **Measure step response**:
   - Use square wave input
   - Observe rise time (proportional to frequency)
   - Relate to frequency response

5. **Test with audio**:
   - Connect microphone input
   - Listen to high-frequency rolloff
   - Compare with/without filter

## Real-World Examples

### Speaker Crossover
- Separate bass (low-pass) and treble (high-pass)
- Cutoff at 2kHz typical
- Multiple stages for steep rolloff

### Anti-Aliasing Filter
- Analog-to-digital converter requirement
- Cutoff at Nyquist frequency (sample rate / 2)
- Prevents aliasing errors

### Audio Interface
- Removes noise above 20kHz (human hearing limit)
- Protects high-frequency amplifiers from oscillation
- Critical in professional audio

## Mathematics Deep Dive

### Transfer Function
$$H(s) = \frac{\omega_c}{s + \omega_c}$$

Where ω_c = 2πf_c (radian frequency)

### Bode Magnitude
$$|H(jω)| = \frac{1}{\sqrt{1 + (f/f_c)^2}}$$

### Bode Phase
$$\angle H(jω) = -\arctan(f/f_c)$$

At f = f_c: ∠H = -45°

## Key Concepts Reinforced

- **Negative feedback**: Stabilizes gain, enables precise frequency response
- **Pole frequency**: Determines filter cutoff
- **Butterworth response**: Maximally flat, well-behaved
- **Frequency dependence**: Capacitor impedance drives filtering action
- **Active vs passive**: Active allows gain, better isolation

## Next Steps

1. **Project 2: Voltage Follower** - High-impedance buffer
2. **Project 3: Comparator** - Digital threshold detection
3. **Project 4: Precision Amplifier** - Variable gain amplifier
4. **Advanced lab: Multi-stage filter** - Cascade filters for audio crossover

---

**Key Takeaway**: Active filters using op-amps and capacitors provide precise frequency response control without passive loading effects. Understanding frequency-dependent impedance and negative feedback principles enables design of stable, high-performance analog circuits used in audio, measurement, and signal processing systems.
