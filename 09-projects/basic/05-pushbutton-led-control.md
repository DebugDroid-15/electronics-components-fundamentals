# Basic Project 5: Pushbutton LED Control

**Difficulty**: ⭐ (Absolute beginner)  
**Time**: 15 minutes  
**Concept**: Digital switching, pushbutton interaction, on/off control

## What You'll Learn

- How switches work (open vs closed circuit)
- Pushbutton as digital input device
- Simple on/off LED control
- Debouncing concept (preview)
- Logic states (HIGH/LOW, on/off)

## Components Required

| Component | Qty | Specifications |
|-----------|-----|-----------------|
| 5V Power Supply | 1 | USB or battery |
| Red LED (5mm) | 1 | Indicator |
| 220Ω Resistor | 1 | Current limiting |
| Pushbutton Switch | 1 | Momentary contact (normally open) |
| Jumper wires | 5 | Breadboard connections |
| Breadboard | 1 | Same as previous |

## Theory: Pushbutton Switches

A **pushbutton** is a switch that closes circuit when pressed, opens when released.

**Normally open (NO)**: Default state is open circuit (no contact).

**Two-terminal pushbutton**:
- Terminal 1: One side of switch
- Terminal 2: Other side
- When pressed: Terminals electrically connected (0Ω)
- When released: Terminals disconnected (open, ∞ Ω)

**Four-terminal pushbuttons** (common in breadboards):
- Pins A & B connected when pressed
- Pins C & D connected when pressed
- Pins A & C always separate
- (Allows space in breadboard middle)

**Circuit behavior**:
- Switch closed → path for current → LED on
- Switch open → no path for current → LED off

## Breadboard Layout

```
        +5V
         |
       [LED]
         |
       [R220Ω]
         |
         +--------[Button Leg 1]
         |
       [Button Leg 2]
         |
        GND
```

LED in series with pushbutton. Circuit completes when button pressed.

## Building Instructions

### Step 1: Insert LED
1. Insert LED cathode (short leg) into Row 2
2. Insert LED anode (long leg) into Row 1

### Step 2: Insert Current-Limiting Resistor
1. Insert 220Ω resistor from Row 1 to Row 3

### Step 3: Insert Pushbutton
1. Identify two legs of pushbutton (usually corner legs work)
2. Insert one leg from Row 3 to Row 4
3. Insert other leg from Row 4 to GND rail

### Step 4: Connect +5V
1. Use jumper wire from +5V rail to Row 1
2. Verify: Circuit path is +5V → R220 → LED → Button → GND

### Step 5: Test
1. Press button
2. LED lights up (circuit complete)
3. Release button
4. LED turns off (circuit open)

## Measurement Plan

**No circuit elements to measure** (it's digital: on/off).

**Functional verification**:
1. **LED off state**:
   - Button released
   - LED not glowing
   - Measure voltage across button with multimeter
   - Expected: 5V (full supply, circuit open, no current)

2. **LED on state**:
   - Button pressed
   - LED glowing brightly
   - Measure voltage across button
   - Expected: 0V (button shorted, no voltage drop)

3. **Button voltage change**:
   - This demonstrates digital switching

## Visual Verification

- ✓ LED **off** when button released
- ✓ LED **on** when button pressed
- ✓ LED responsive (lights immediately on press)
- ✓ No ghost glow when released

## Key Insight: Switching vs. Dimming

Unlike Projects 1-4 (where we controlled current with resistors):
- Here we're controlling whether current flows at all
- Switch is either on or off (digital)
- No intermediate brightness

This is **digital logic**, foundation of microcontroller interfaces.

## Push-Release Behavior

**Pressing button**:
1. Contacts touch
2. Resistance drops to near 0Ω
3. Current flows through LED
4. LED glows

**Releasing button**:
1. Contacts separate
2. Resistance goes to ∞ (open)
3. Current stops
4. LED turns off (immediately)

**No delay** (DC circuit responds instantly).

## Mechanical Bounce (Preview)

Real pushbuttons **bounce** slightly when pressed—contacts make/break multiple times in microseconds.

At DC (human timescale): invisible.

But microcontrollers see this as multiple rapid on/off cycles.

Solution: **debouncing** (filter out bounces with capacitor or code).

More on this in later projects.

## Troubleshooting

**LED doesn't light when button pressed**:
- Check button orientation (try rotating 90°)
- Verify connections (all in series)
- Test button: measure resistance directly with multimeter
  - Released: should be ∞ (open) or very high (>10MΩ)
  - Pressed: should be 0Ω or very low (<1Ω)

**LED stays on**:
- Button stuck in pressed position (mechanically)
- Or connection is making permanent path to GND

**LED flickers when button held**:
- Button contacts bouncing (normal mechanical behavior)
- Flickers very fast (human eye might see as "unstable")

## Challenge Extensions

1. **Add second button**:
   - Second button in series: both must be pressed to light LED
   - Series logic (AND gate)
   - Try it!

2. **Two parallel buttons**:
   - Each button has own LED
   - Press first: LED1 lights
   - Press second: LED2 lights
   - Press both: both light (OR gate in breadboard)

3. **Debounce with capacitor**:
   - Add 100nF capacitor across button leads
   - Smooths contact bouncing
   - Advanced, saves for later

4. **Button + analog control**:
   - Add potentiometer in series with LED
   - Button turns circuit on
   - Potentiometer controls brightness
   - Combines digital (button) + analog (pot)

## Real-World Application

**Power button**: Turns device on/off.

**Momentary switches everywhere**:
- Doorbell: Button pressed → electromagnet activates
- Light switch: Button pressed → relay closes → lights on
- Game controller: Button presses detected by microcontroller

**Digital vs. analog distinction**:
- Digital: Button either presses or doesn't
- Analog: Previous projects varied voltage/current smoothly
- Together: Powerful combo for interactive circuits

## Key Concepts Reinforced

- **Digital switching**: On/off logic
- **Momentary switch**: Returns to normal state when released
- **Circuit completion**: Switch provides path for current
- **Boolean logic**: Button states (pressed/released) map to circuit states (on/off)
- **Interactive design**: User input directly controls circuit behavior

## Next Steps

1. **Project 6: LED Brightness Control** - Combine button with potentiometer
2. **Project 7: Capacitor Charging** - Add timing element
3. **Project 10: Transistor LED Flasher** - Use button to trigger timing

---

**Key Takeaway**: Pushbuttons provide digital switching—either complete the circuit (on) or break it (off). This is the foundation for all interactive electronics, from simple switches to complex microcontroller interfaces.
