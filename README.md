# DIY Wire Fault Detector

> **Cost:** ~50–75 Rs | **Skill Level:** Intermediate | **Time:** 2–3 hours

A low-cost, non-contact wire fault detector that uses electromagnetic field coupling to detect breaks, shorts, and melts in electrical wiring without touching the insulation.

## How It Works

```
┌─────────────────────┐         ┌──────────────────┐
│  9V Battery + 555   │         │  Pickup Coil     │
│  (1kHz Signal)      │         │  + LM358 Amp     │
└──────────┬──────────┘         └────────┬─────────┘
           │                             │
           └─────→ WIRE UNDER TEST ←────┘
                        ⚡ (FAULT DETECTED)
```

**Step-by-step:**
1. **Transmitter** injects a ~1kHz AC signal into the test wire
2. The wire radiates a weak **electromagnetic field**
3. A **pickup coil** in the probe detects this field as you glide it over the wire
4. When the field changes or drops (at a fault), the **LM358 amplifier** boosts the signal
5. The **buzzer sounds** — you've found the fault!

## Features

✅ **Non-contact** — detect faults through insulation  
✅ **Glide-over detection** — slide probe along wire to locate fault  
✅ **Low power** — runs on a single 9V battery  
✅ **Budget-friendly** — ~60 rupees in parts  
✅ **Portable** — fits in a small box  

## Parts List

| Component | Spec | Cost (Rs) |
|-----------|------|-----------|
| NE555 IC | Astable oscillator (~1kHz) | ~5 |
| LM358 IC | Dual op-amp, signal amplifier | ~5 |
| Resistors | 10kΩ, 47kΩ, 100kΩ (×1 each) | ~3 |
| Capacitor | 10µF electrolytic | ~3 |
| Ferrite rod + wire | 20 turns of thin copper wire | ~10 |
| Piezo buzzer | 5V passive type | ~10 |
| 9V battery + clip | — | ~15 |
| Breadboard / PCB | Small size | ~10 |
| **TOTAL** | | **~61 Rs** |

## Circuit Schematic

```
TRANSMITTER SIDE              RECEIVER PROBE SIDE
═══════════════               ══════════════════

    9V
     │
     ├─→ NE555 ──→ ~1kHz output
     │  (555 timer)
     │
     └─ [R1, R2, C1] ─ TIMING NETWORK

              ↓ SIGNAL TO WIRE
              
     TEST WIRE (Under Test)
              ↑ Pickups up signal change at fault
              
              ↓ COIL (20 turns on ferrite)
              
         LM358 Amplifier
         (100kΩ feedback)
         
         Buzzer Output ← BEEP WHEN FAULT FOUND
```

## Build Instructions

### Transmitter (Signal Injector)

1. **Wire the 555 timer in astable mode:**
   - Connect 9V battery +ve to VCC (pin 8)
   - Connect 9V battery -ve to GND (pin 1)
   - Add 10kΩ resistor between VCC and pin 7
   - Add 47kΩ resistor between pin 7 and pin 6
   - Connect pin 2 and pin 6 together
   - Add 10µF capacitor between pin 2 and GND
   - Output comes from pin 3 (~1kHz square wave)

2. **Connect output to test wire:**
   - One end of the wire: Pin 3 of 555
   - Other end: Leave open (for break detection) or ground (for short detection)

### Receiver (Pickup Probe)

1. **Wind the pickup coil:**
   - Wrap 20 turns of thin copper wire around a ferrite rod (or iron nail)
   - Keep turns tight and neat

2. **Wire the LM358 amplifier:**
   - Connect coil output to pin 3 (+input)
   - Connect 100kΩ feedback resistor between output (pin 1) and -input (pin 2)
   - Connect pin 4 to GND, pin 8 to 9V

3. **Connect buzzer:**
   - Positive wire to LM358 output (pin 1)
   - Negative wire to GND

### Testing

1. Build a test wire with a deliberate fault (break, short, or melt)
2. Power on the device
3. Slowly glide the probe over the wire
4. Listen for buzzer changes:
   - **Continuous beep** → normal wire
   - **Beep stops or changes** → fault found!
5. Mark the location and verify the fault

## Troubleshooting

| Issue | Solution |
|-------|----------|
| No buzzer sound | Check battery voltage, verify coil windings |
| Always beeping | Reduce feedback resistor (less sensitive) |
| Can't find fault | Increase feedback resistor (more sensitive) |
| Weak signal pickup | Ensure coil is close to wire (~1cm) |

## Safety Guidelines

⚠️ **IMPORTANT:**
- Only use on **de-energized (OFF) wires**
- Never test on live mains wiring (220V AC)
- This device works with 9V signal injection only
- Always use proper safety precautions when testing electrical systems

## Optional Enhancements

- Add an LED indicator for visual feedback
- Use a speaker instead of buzzer for different tones
- Add frequency adjustment potentiometer for tuning
- Build a PCB for permanent installation
- Add sensitivity adjustment dial

## File Structure

```
DIY_wire_fault_detector/
├── index.html              ← Interactive guide & demo
├── wire-fault-detector.html ← Standalone circuit guide
├── README.md              ← This file
└── .github/
    └── workflows/
        └── deploy.yml     ← Auto-deployment to GitHub Pages
```

## Live Demo

View the interactive circuit guide with animations:
👉 **[Click here for live demo](https://athestatom.github.io/DIY_wire_fault_detector/)**

---

**Author:** DIY Electronics  
**License:** MIT (feel free to modify and share)  
**Last Updated:** 2026-05-07
