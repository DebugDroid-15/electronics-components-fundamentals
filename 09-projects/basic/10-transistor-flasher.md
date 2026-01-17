# Basic Project 10: Simple LED Flasher with Transistor

**Difficulty**: ⭐⭐ (Beginner)  
**Time**: 25 minutes  
**Concept**: Transistor as switch, base current, switching oscillator, automatic timing

## What You'll Learn

- BJT transistor as electronically controlled switch
- How base current controls collector current
- Using capacitor + resistor for oscillation
- Building simple flasher (no microcontroller needed)

## Components Required

| Component | Qty | Specifications |
|-----------|-----|---|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 1 | Load being switched |
| 220Ω Resistor | 1 | LED current limiting |
| 10kΩ Resistor | 1 | Base current limiting |
| 100kΩ Resistor | 1 | Timing resistor |
| 470µF Capacitor | 1 | Timing capacitor |
| BJT Transistor | 1 | 2N2222 or 2N3904 NPN |
| Breadboard | 1 | Same as previous |
| Multimeter | 1 | Verify operation |

## Theory: Transistor as Switch

A **BJT (Bipolar Junction Transistor)** in saturation mode acts as a voltage-controlled switch.

**Switch behavior**:
- Base current HIGH: Transistor ON (saturated), collector acts like short circuit
- Base current LOW: Transistor OFF (cutoff), collector acts like open circuit

**Switch efficiency**:
$$I_C = \beta \times I_B$$

Where:
- I_C = collector current (switch load current)
- I_B = base current (control current)
- β (beta) = current gain (~100 for 2N2222)

Example:
- Desired I_C = 10mA (LED current)
- β = 100
- Required I_B = 10mA / 100 = 0.1mA = 100µA

**Power advantage**: Control LED (10mA) with tiny base current (100µA).

## Oscillator Principle

This flasher uses **RC oscillation**:

1. **Capacitor charges** through 100kΩ resistor toward 5V
2. **When capacitor reaches ~3V**: Base voltage high enough to turn ON transistor
3. **Transistor ON**: LED lights, capacitor discharges through transistor
4. **Capacitor drops below ~1.5V**: Transistor turns OFF
5. **Cycle repeats**: Capacitor charges again

**Frequency** (approximate):
$$f \approx \frac{1.4}{R \times C}$$

For 100kΩ × 470µF:
$$f \approx \frac{1.4}{100000 \times 0.00047} \approx 0.03 Hz \approx 1 flash every 30 seconds$$

(Very slow. Use smaller R or C for faster flashing.)

## Breadboard Layout

```
        +5V
         |
      [100kΩ R]
         |
    [C470µ]---+---[10kΩ R]
         |     |
        GND  [Transistor Base (B)]
              [Transistor Collector (C)]
                     |
                  [R220]
                     |
                   [LED]
                     |
        [Transistor Emitter (E)]
                     |
                    GND
```

## Building Instructions

### Step 1: Insert Timing Network
1. Insert 100kΩ resistor from +5V to Row 2
2. Insert 470µF capacitor: positive lead to Row 2, negative to Row 3
3. Connect Row 3 to GND

### Step 2: Insert Base Divider
1. Insert 10kΩ resistor from Row 2 to Row 4 (transistor base input)
2. This limits base current to safe level

### Step 3: Insert Transistor
1. Identify transistor leads:
   - B (base) = control input
   - C (collector) = from +5V side
   - E (emitter) = to GND
2. Insert base (B) into Row 4
3. Insert collector (C) into Row 5
4. Insert emitter (E) into GND rail

### Step 4: Insert LED Circuit
1. Insert 220Ω resistor from +5V to Row 6
2. Insert LED anode into Row 6
3. Insert LED cathode into Row 5 (same row as transistor collector)

### Step 5: Verify Connections
- Power supply: +5V and GND connected
- Timing capacitor between Row 2 (charging) and GND (ground)
- Base through 10kΩ resistor controlled by capacitor voltage
- LED switches as transistor turns on/off

### Step 6: Test
1. Power up
2. LED should flash slowly (on-off-on-off...)
3. Initially may seem off—capacitor slowly charging first time

## Measurement Plan

1. **Verify flashing frequency**:
   - Count LED flashes over 60 seconds
   - Expected: ~2 flashes/min (30-second period)
   - Actual: _____ flashes/min

2. **Measure capacitor voltage**:
   - Black probe: GND
   - Red probe: Row 2 (capacitor positive side)
   - Should oscillate between ~1.5V and ~4V
   - Charge/discharge cycle visible if multimeter samples slowly

3. **Measure base voltage**:
   - Black probe: GND
   - Red probe: Row 4 (transistor base)
   - Should track capacitor voltage
   - Between ~1.5V (OFF threshold) and ~4V (ON threshold)

4. **LED brightness**:
   - Should be normal brightness when ON
   - Completely off when transistor cutoff
   - No intermediate states (digital behavior)

## Visual Verification

- ✓ LED turns completely on (bright red)
- ✓ LED turns completely off (dark)
- ✓ Flashing pattern repeats regularly
- ✓ Transistor warm to touch when LED on (normal power dissipation)

## Key Insight: Astable Oscillator

This simple circuit is called **astable oscillator**:
- No stable state (always oscillating between ON and OFF)
- Uses capacitor charging/discharging for timing
- Simplest form of timing circuit (no microcontroller needed)

**Advantages**:
- Single transistor (cheap)
- No programming needed
- Adjustable frequency (change R or C)

**Disadvantages**:
- Frequency not stable (drifts with temperature)
- Frequency depends on supply voltage
- Limited control over on/off ratio

## Frequency Control

**Slower flashing** (lower frequency):
- Increase 100kΩ resistor to 220kΩ or higher
- Or increase capacitor to 1000µF
- Or both

**Faster flashing**:
- Decrease 100kΩ resistor to 47kΩ
- Or decrease capacitor to 100µF

**Experiment**: Try different values, observe frequency change.

## Troubleshooting

**LED doesn't flash**:
- Check capacitor polarity (positive to +5V side)
- Verify transistor orientation (check pinout)
- Measure capacitor voltage: should oscillate
- If static, transistor not switching

**LED always on** (doesn't turn off):
- Base voltage too high (capacitor stuck)
- Check 100kΩ resistor (might be shorted)
- Verify capacitor not shorted

**LED very dim or doesn't light**:
- Collector current path broken
- Check LED orientation
- Verify 220Ω resistor in series with LED
- Transistor might not be turning fully on

**Flashing too slow to see**:
- Reduce 100kΩ to 47kΩ
- Or reduce 470µF to 100µF
- Or both

## Challenge Extensions

1. **Fast flasher**:
   - Change 100kΩ to 47kΩ, capacitor to 100µF
   - Frequency: ~3 Hz (3 flashes/second)
   - Much more visible

2. **Adjustable frequency**:
   - Replace 100kΩ with potentiometer (1M to 1kΩ range)
   - Turn knob to adjust flashing speed
   - Creates adjustable flasher

3. **Duty cycle control**:
   - Add second resistor path (affects charge vs. discharge rate)
   - Makes LED on-time different from off-time
   - Advanced oscillator design

4. **Multiple LEDs**:
   - Add second transistor with different timing
   - Create alternating flasher pattern
   - Two LEDs flashing opposite phases

## Real-World Applications

- **LED flashers**: Camera flash triggers, warning lights
- **Oscillators**: Clock generation, timing circuits
- **PWM generators**: Power control, motor speed
- **Function generators**: Test equipment

## Advanced: Monostable Oscillator

Single-shot timer: Press button, LED on for fixed time, turns off.

Uses same RC principle but triggered by button press.

Preview: Will build in intermediate projects.

## Advanced: 555 Timer IC

Professional version: **555 timer IC** integrates oscillator into single chip.

Advantages:
- Very stable frequency
- Easy to adjust
- Built-in circuits for efficiency

Preview: Intermediate Project with 555 timer.

## Key Concepts Reinforced

- **Transistor as switch**: Base current controls collector current
- **RC oscillation**: Capacitor charge/discharge creates timing
- **Astable oscillator**: Automatically oscillates without external trigger
- **Frequency control**: R and C values determine flashing speed
- **Practical timing**: Single transistor creates useful timing circuit

## Next Steps

1. **Project 11: Series-Parallel Capacitors** - Control timing with multiple capacitors
2. **Project 12: Power Dissipation** - Calculate heat from transistor
3. **Intermediate Project 2: 555 Timer Flasher** - More precise timing with IC
4. **Intermediate Project 3: PWM Motor Control** - Use transistor for power control

---

**Key Takeaway**: A single BJT transistor, combined with RC timing network, creates a simple astable oscillator that flashes an LED without any microcontroller or programming. By adjusting the resistor and capacitor values, you control the flashing frequency—a practical demonstration of how simple circuits create useful timing behavior.
