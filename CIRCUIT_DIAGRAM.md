# Clap Switch Using IC555 Timer - Circuit Diagram & Pin Configuration

## IC555 Timer Pin Diagram

```
        ┌─────────────┐
        │   IC555     │
        │             │
    GND │ 1         8 │ VCC (+5V)
    TRIG│ 2         7 │ DISCHARGE
   CTRL │ 3         6 │ THRESHOLD
  RESET │ 4         5 │ OUT
        │             │
        └─────────────┘

PIN CONFIGURATION:
Pin 1: GND (Ground)
Pin 2: TRIGGER (Active LOW, input)
Pin 3: OUTPUT (Connected to Transistor Base)
Pin 4: RESET (Active LOW, usually tied to VCC)
Pin 5: CONTROL VOLTAGE (0.01µF capacitor to GND)
Pin 6: THRESHOLD (Connected to Pin 2 for Monostable mode)
Pin 7: DISCHARGE (Connected through Resistor to Pin 6/2)
Pin 8: VCC (+5V Power Supply)
```

---

## BC547 NPN Transistor Pin Diagram

```
        COLLECTOR
           │
           ├─────────────────┐
           │                 │
        ┌──┴──┐              │
        │  │  │   BC547      │
        │  │  │    NPN       │
        │  │  │              │
        └──┬──┘              │
           │                 │
           ├─────────────────┤
           │        B        │ BASE (Input from IC555)
           │                 │
           ├─────────────────┤
           │        E        │ EMITTER (To GND)
           │                 │
        ┌──┴──┐            ┌─┴──┐
        │  C  │            │ B  │
        │  O  │            │    │
        │  L  │   (E=Emitter
        │  L  │    connected to GND)
        │  E  │
        │  C  │
        │  T  │
        │  O  │
        │  R  │
        └─────┘
```

---

## Complete Clap Switch Circuit Diagram

```
                    ┌──────────────────────────────────┐
                    │         POWER SUPPLY             │
                    │          (+5V, GND)              │
                    └────────┬───────────────┬──────────┘
                             │               │
                             │               │
                    ┌────────┴───────────────┴────────┐
                    │                                 │
                    │                                 │
                  ┌─┴──┐                             VCC(+5V)
                  │    │                              │
                  │ IC │                       ┌──────┴─────────┐
                  │555 │                       │                │
                  │    │                       │                │
                  └────┘                       │                │
                  │ │ │ │                      │                │
           ┌──────┼─┼─┼─┼──────┐               │                │
           │      │ │ │ │      │               │                │
           │      │ │ │ │      │               │                │
        ┌──┴──┐  │ │ │ │   ┌──┴──┐      ┌─────┴────┐       ┌───┴────┐
        │GND  │  │ │ │ │   │RESET│      │OUTPUT(3) │       │ RC547  │
        │  1  │  │ │ │ │   │  4  │      │          │       │        │
        │     │  │ │ │ │   │     │      │ ┌────────┴────┐  │        │
        └─────┘  │ │ │ │   └──┬──┘      │ │             │  │        │
                  │ │ │ │      │        │ │  220Ω Res   │  │        │
                  │ │ │ │     VCC       │ │  (Base)     │  │        │
                  │ │ │ │      │        │ └────────┬────┘  │        │
                  │ │ │ │      │        │          │       │        │
              ┌───┘ │ │ │      │        │       ┌──┴───┐   │        │
              │     │ │ │      │        │       │  B   │   │        │
           ┌──┴───┐ │ │ │      │        │       └──┬───┘   │        │
           │ TRIG │ │ │ │   ┌──┴──┐    │          │       │        │
           │  2   │ │ │ │   │ VCC │    │          │       │        │
           └──┬───┘ │ │ │   │     │    │          │       │        │
              │     │ │ │   └─────┘    │          │       │    C   │
    ┌─────────┘     │ │ │              │          │       ├───┐    │
    │               │ │ │         ┌────┴────┐     │       │   │    │
    │         ┌─────┴─┘ │         │ CTRL V  │     │       │   │    │
    │         │ DISCHARGE         │  5      │     │       │   │    │
    │         │  7                │         │     │       │   │    │
    │         │     ┌─────────────┴────┬────┘     │       │   │    │
    │         │     │                  │          │       │   │    │
    │       ┌─┴─────┴─────────┐        │      ┌───┴───┐   │   │    │
    │       │  1kΩ Resistor  │        │      │0.01µF │   │   │    │
    │       │                │        │      │Capacitor  │   │    │
    │       └────┬────────────┴────────┴──────┴───┬───┘   │   │    │
    │            │                               │       │   │    │
    │         ┌──┴──────────────────────────┐   │       │   │    │
    │         │ 10µF Timing Capacitor       │   │       │   │    │
    │         │                             │   │       │   │    │
    │         └──────────────┬──────────────┘   │       │   │    │
    │                        │                  │       │   │    │
    │                    ┌───┴────┐             │       │   │    │
    │                    │ Diode  │             │       │   │    │
    │                    │        │             │       │   │    │
    │                    └───┬────┘             │       │   │    │
    │                        │                  │       │   │    │
    │                       GND                GND     GND  E   │
    │                                                   │    ├───┘
    │                                                   │    │
    │ ┌──────────────────────────────────────────────────────┘
    │ │
    │ │  MICROPHONE SIGNAL
    │ │  (Condenser Microphone)
    │ │
    │ ├─────────┬────────────────────────┐
    │           │                        │
    │         ┌─┴──┐                   ┌─┴──┐
    │         │ 10k│ Resistor          │100k│ Resistor
    │         │    │                   │    │
    │         └────┴────────────────────┴─┬──┘
    │              │                      │
    │              │                      │
    │         ┌────┴──────────────────────┴──┐
    │         │  100nF Capacitor (Coupling)  │
    │         │                              │
    │         └──────────────┬───────────────┘
    │                        │
    └────────────────────────┴─────────► To IC555 Pin 2 (TRIGGER)


                    OUTPUT STAGE
                    ┌─────────────────┐
                    │   BULB (LOAD)   │
                    │   40W or Less   │
                    └────────┬────────┘
                             │
                             ├─────────────────┐
                             │                 │
                          Collector     ┌──────┴──────┐
                          │             │ 220Ω Resistor
                          │             │ (Current Limiting)
                          │             │
                          │             └──────┬──────┐
                          │                    │      │
                         GND                  GND    AC Power

```

---

## Component Connection Summary

### Microphone Circuit (Input Stage)
- Condenser Microphone → 10kΩ Resistor → 100nF Coupling Capacitor → IC555 Pin 2 (TRIGGER)
- 100kΩ Pulldown Resistor connected to GND

### IC555 Configuration (Monostable Mode)
- Pin 1: GND
- Pin 2 & Pin 6: Connected together (TRIGGER and THRESHOLD)
- Pin 4: Connected to VCC (RESET, Active HIGH)
- Pin 5: 0.01µF Capacitor to GND (CONTROL VOLTAGE)
- Pin 7 (DISCHARGE): Connected through 1kΩ Resistor to Pin 6/2
- Pin 8: VCC (+5V)
- 10µF Timing Capacitor: Connected between Pin 6/2 and GND
- Diode: Connected in parallel with the 1kΩ Resistor (to control discharge path)

### IC555 Output Stage
- Pin 3 (OUTPUT): Connected to 220Ω Base Resistor
- 220Ω Resistor: Connected to BC547 Base

### Transistor Switch (BC547)
- Base: Connected from IC555 Pin 3 (through 220Ω Resistor)
- Collector: Connected to the Bulb and +5V Power
- Emitter: Connected to GND

### Output Load (Bulb)
- Bulb is powered between Collector of BC547 and +5V
- When transistor conducts (Base is HIGH), Bulb turns ON
- When transistor is OFF (Base is LOW), Bulb turns OFF

---

## Pin Connection Details

| Component | Pin/Terminal | Connected To | Purpose |
|-----------|--------------|--------------|---------|
| IC555 | Pin 1 (GND) | Ground | Power reference |
| IC555 | Pin 2 (TRIGGER) | Microphone via Coupling Cap | Sound input |
| IC555 | Pin 3 (OUTPUT) | BC547 Base via 220Ω | Control signal |
| IC555 | Pin 4 (RESET) | VCC (+5V) | Always enabled |
| IC555 | Pin 5 (CTRL V) | 0.01µF Cap to GND | Noise filtering |
| IC555 | Pin 6 (THRESHOLD) | Pin 2 & Timing Capacitor | Timing feedback |
| IC555 | Pin 7 (DISCHARGE) | 1kΩ Resistor to Pin 6 | Timing control |
| IC555 | Pin 8 (VCC) | +5V Power Supply | Power input |
| BC547 | Base | IC555 Pin 3 via 220Ω | Switching control |
| BC547 | Collector | Bulb anode | Load switching |
| BC547 | Emitter | GND | Current return path |
| Microphone | Positive | 10kΩ to Coupling Cap | Signal output |
| Microphone | Negative | GND | Reference |
| Bulb | Anode | BC547 Collector | Load cathode |
| Bulb | Cathode | +5V Power | Power supply |

---

## Working Voltage & Current Specifications

- **Supply Voltage:** +5V DC
- **IC555 Operating Range:** 4.5V - 15V (5V recommended for this project)
- **BC547 Maximum Collector Current:** 100mA
- **Microphone Signal Level:** 5mV - 50mV (weak signal)
- **IC555 Output Logic:** TTL compatible (HIGH = 5V, LOW = 0V)
- **Bulb Rating:** 40W maximum at 5V

---

## Timing Formula

The IC555 output pulse width (time the bulb stays ON) is determined by:

**T = 1.1 × R × C**

Where:
- R = 1kΩ Resistor value
- C = 10µF Capacitor value
- T = Time duration in seconds

**Example:** T = 1.1 × 1000Ω × 10µF = 11 milliseconds (approximately 0.011 seconds)

This means the bulb will remain ON for about 11ms after each clap is detected.

---

## Breadboard Layout Guide

1. Place IC555 in the center of the breadboard
2. Connect power rails: Left rail = GND (bottom), Right rail = VCC (top)
3. Connect microphone input circuit on the left side
4. Connect RC timing network below the IC555
5. Connect BC547 transistor on the right side
6. Connect bulb output stage to the far right
7. Use color-coded wires: Red = +5V, Black = GND, Other colors = Signal lines

---

## Safety Notes

- Ensure all connections are secure before powering on
- Check polarity of capacitors and diodes before assembly
- Use a regulated 5V power supply
- Avoid touching live circuits while powered
- Keep the breadboard away from moisture

