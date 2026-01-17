# MOSFETs: Enhancement vs. Depletion

## Two MOSFET Families

MOSFETs come in two fundamentally different types:
1. **Enhancement MOSFET**: Default off, turns on with gate voltage (common)
2. **Depletion MOSFET**: Default on, turns off with gate voltage (rare)

## Enhancement MOSFET (Normal Type)

### Definition
**Without gate voltage**: No channel, transistor is **off**
**With gate voltage above threshold**: Channel forms, transistor conducts (**on**)

### Why "Enhancement"?
Gate voltage **enhances** (creates) a conduction channel that doesn't naturally exist.

### Behavior

**Off state** (VGS < Vth):
- No conduction channel
- Drain-source path open circuit
- ID ≈ 0
- Used as "normally off" switch

**On state** (VGS > Vth):
- Conduction channel formed
- Current flows drain-source
- ID determined by VGS and drain-source voltage
- Used as "normally on" switch

### Threshold Voltage (Vth)

Minimum gate voltage needed to form channel:
- N-Channel: Positive Vth (gate pulled positive relative to source)
- P-Channel: Negative Vth (gate pulled negative relative to source)

Typical values: 1–5V depending on type

### IV Characteristic

```
ID
|       VGS = 8V (highest)
|     /
|    / VGS = 6V
|   /
|  / VGS = 4V (above threshold)
| /
+------- VGS < Vth (below threshold, essentially no current)
       VDS
```

- **Below Vth**: Essentially no current (excellent off state)
- **Above Vth**: Current increases with gate voltage
- **Higher gate voltage**: Larger current (until VDS voltage limit reached)

### Design Advantage
Enhancement MOSFET is naturally "off" (safe state if gate driver fails). This makes it ideal for switching applications.

### Common Applications
- **Switching power supplies**: Default off ensures safety
- **Motor control**: Default off is safe during startup
- **Logic circuits**: Normal state is off
- **Battery disconnects**: Default off if driver fails
- **Essentially all modern power electronics**

### Examples
- N-Channel: 2N7000, IRF510, IRFZ44
- P-Channel: IRF9510, BS250

---

## Depletion MOSFET (Rare Type)

### Definition
**Without gate voltage**: Channel exists, transistor is **on**
**With gate voltage**: Channel depleted, transistor turns **off**

### Why "Depletion"?
Gate voltage **depletes** (removes) the natural conduction channel.

### Behavior

**On state** (VGS = 0):
- Natural channel exists
- Maximum drain-source current
- Transistor conducts with no gate signal
- Used as "normally on" configuration

**Off state** (VGS significantly negative):
- Channel depleted
- Drain-source path blocks
- ID ≈ 0
- Gate voltage must be large negative to turn off

### Gate Voltage Range
- VGS = 0: Full on (maximum current)
- VGS = -Vth: Transition point
- VGS < -Vth: Off

### IV Characteristic

```
ID
|
|      VGS = 0V (full on)
|    /
|   /  VGS = -1V
|  /
| /   VGS = -2V (approaching off)
+-------
      VGS = -5V (off)
       VDS
```

- **VGS = 0**: Maximum on current
- **VGS increasingly negative**: Current decreases
- **VGS < -Vth**: Transistor off

### Design Disadvantage
Depletion MOSFET is naturally "on" (dangerous if gate driver fails).

If gate driver disconnects, transistor remains on → load stays powered/conducting (safety issue).

### Applications
Depletion MOSFETs rare in modern designs because:
- Safety concern (naturally on is problematic)
- Enhancement MOSFETs superior for switching
- More specialized RF/microwave uses
- Historical designs still in field

### Examples
- JFET (Junction FET): Similar "depletion" behavior
- Rare MOSFET types (mostly GaAs/RF)

---

## Comparison: Enhancement vs. Depletion

| Feature | Enhancement | Depletion |
|---------|-------------|-----------|
| Default state | Off | On |
| Gate voltage for on | Positive (N-Ch) or Negative (P-Ch) | Zero or more negative |
| Gate voltage for off | Near zero or negative | Large negative |
| Safety (if gate driver fails) | Safe (stays off) | Unsafe (stays on) |
| Applications | Almost all modern power electronics | Rare (RF/microwave) |
| Frequency | Excellent | Excellent |
| Availability | Common | Rare |
| Cost | Low | High (specialized) |

---

## N-Channel vs. P-Channel (Supplementary)

This is different from enhancement vs. depletion. Enhancement MOSFETs come in **two polarities**:

### N-Channel Enhancement
- Electrons are majority carriers
- Source connected to negative rail (typically)
- Gate pulled positive to turn on
- More common (better performance)
- Used in high-side and low-side switching

### P-Channel Enhancement
- Holes are majority carriers
- Source connected to positive rail (typically)
- Gate pulled negative to turn on
- Less common
- Sometimes used for high-side switching

### Why N-Channel More Common
- Better carrier mobility (faster switching)
- Lower on-resistance for same die size
- Simpler gate drive requirements
- Standard choice for power electronics

---

## Depletion JFET (Junction Field-Effect Transistor)

**JFET** behaves like depletion MOSFET:
- Built differently (junction instead of oxide)
- Naturally conducting (VGS = 0)
- Gate voltage becomes increasingly negative to turn off
- Very low input leakage current
- Used in analog circuits (extremely high input impedance)

### JFET vs. Depletion MOSFET
Similar behavior but:
- **JFET**: True junction-based device
- **MOSFET**: Oxide-based device
- **JFET advantages**: No gate leakage, simpler gate drive
- **Depletion MOSFET advantages**: Higher current capacity, scalable

---

## Practical Consideration: Gate-Source Voltage Limits

### Enhancement MOSFET Gate Rating
- Maximum gate-source voltage (VGS(max)): 10–20V typically
- Exceed this: Gate oxide breaks down
- Permanent failure
- Cannot be repaired

### Design Implication
- Gate voltage must always stay within specified limits
- Logic signal (5V) usually okay for most MOSFETs
- High-side switching requires special consideration (gate bootstrap circuit)
- Protection diodes or clamp needed if overvoltage possible

### Gate Driver Responsibility
- Ensure gate voltage never exceeds maximum
- Often gate driver enforces this through design
- Bootstrap circuits must clamp voltage
- Protection diodes on gate-source junction

---

## Modern Trend: Enhancement Only

Modern power electronics uses **exclusively enhancement MOSFETs** because:
1. **Safety**: Naturally off (fail-safe)
2. **Simplicity**: Standard gate drive circuits
3. **Performance**: Adequate for all applications
4. **Cost**: Depletion MOSFETs more expensive
5. **Availability**: Enhancement MOSFETs everywhere

Depletion MOSFETs and JFETs confined to:
- Specialized RF/microwave circuits
- Analog circuit design (JFET input stages)
- Historical designs
- Academic study

---

## Key Takeaway

**Enhancement MOSFETs (naturally off) are the modern standard for power switching because they're safe (fail-safe), simple to drive, and widely available. Depletion MOSFETs (naturally on) are rarely used in modern designs due to safety concerns, though they have niche applications in RF and analog circuits.**

For learning electronics, focus on **enhancement MOSFETs** (N-channel typical). Depletion types are historical/specialized knowledge.
