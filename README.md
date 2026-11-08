# Awesome Electronic Components

A curated list of electronic components, their uses, and links to datasheets — beginner-friendly.

## Contents

### Getting Started
- [Safety First](#-safety-first)
- [Essential Tools](#-essential-tools-for-beginners)
- [Basic Concepts](#-basic-concepts-every-beginner-must-know)
- [Beginner's Survival Guide](#-beginners-survival-guide)
- [Where to Buy Components](#-where-to-buy-components)
- [Recommended Starter Kits](#-recommended-starter-kits)
- [Beginner Project Ladder](#-beginner-project-ladder)
- [Commonly Asked Questions](#-commonly-asked-beginner-questions)
- [Learning Resources](#-learning-resources)
- [Open-Source & Free Tools](#-open-source--free-tools)

### Component Reference
- [Passive Components](#passive-components)
- [Semiconductors](#semiconductors)
- [Integrated Circuits](#integrated-circuits)
- [Microcontrollers & Processors](#microcontrollers--processors)
- [Optoelectronics](#optoelectronics)
- [Sensors & Transducers](#sensors--transducers)
- [Electromechanical Components](#electromechanical-components)
- [Power Components](#power-components)
- [Connectors & Interconnects](#connectors--interconnects)
- [Communication & Networking](#communication--networking)
- [Timing, Memory & Interface ICs](#timing-memory--interface-ics)

### Domain Applications
- [IoT — Protocols & Platforms](#iot--protocols--platforms)
  - [Communication Protocols](#communication-protocols-software-layer)
  - [Cloud & Device Platforms](#cloud--device-platforms)
  - [Time-Series & Visualization](#time-series--visualization)
  - [Edge & Gateway Software](#edge--gateway-software)
  - [IoT Reference Architecture](#iot-reference-architecture-starter-pattern)
- [Agricultural & Environmental Sensors](#agricultural--environmental-sensors)
  - [Soil Sensors](#soil-sensors)
  - [Soil — Advanced & Water Potential](#soil--advanced--water-potential)
  - [Weather & Climate Sensors](#weather--climate-sensors)
  - [Atmospheric & Microclimate](#atmospheric--microclimate)
  - [Water & Irrigation Sensors](#water--irrigation-sensors)
  - [Greenhouse & Precision Farming](#greenhouse--precision-farming)
  - [Livestock Monitoring](#livestock-monitoring)
  - [Crop Health & Imaging](#crop-health--imaging)
  - [Smart Irrigation Controllers](#smart-irrigation-controllers)
  - [IoT Agriculture Platforms](#iot-agriculture-platforms)

---

# Getting Started

## Safety First

- **Always check polarity** — Electrolytic caps, diodes, LEDs, and ICs can be destroyed (or explode) if reverse-biased.
- **Never short a power supply** — Especially batteries and bench supplies. Use a fuse or current-limit mode on your PSU.
- **Discharge capacitors** — Large electrolytic caps can hold a lethal charge for hours. Use a 1kΩ resistor to safely discharge.
- **Hot solder / lead exposure** — Solder in a ventilated area. Wash hands after soldering. Leaded solder is toxic if ingested.
- **Battery safety** — LiPo/Li-ion must not be over-discharged or over-charged (fire risk). Use a protection circuit (BMS) or a charger IC like TP4056.
- **Mains voltage is deadly** — Never prototype mains AC circuits on a breadboard. Use an isolation transformer or pre-built modules.
- **ESD (Electrostatic Discharge)** — Touch a grounded metal object before handling sensitive ICs (MOSFETs, CMOS logic). Wrist strap helps.
- **Resistor sizing** — Always calculate power dissipation: P = I²R. A 1/4W resistor will burn out with >250mW.

## Essential Tools for Beginners

- **Digital Multimeter (DMM)** — Measures voltage, current, resistance, continuity, diode drop. Get an auto-ranging one (e.g., Fluke 15B+, Aneng AN8008, or a cheap DT830 to start). [Buying Guide](https://www.sparkfun.com/datasheets/Components/General%20Guide%20to%20Multimeters.pdf)
- **Soldering Iron** — 60W adjustable temperature station (e.g., TS-100, Pinecil, Hakko FX-888D). Leaded solder (63/37) is easiest for beginners. [Guide](https://learn.adafruit.com/adafruit-guide-excellent-soldering)
- **Wire Strippers** — Strips insulation from 20–30 AWG wires cleanly. Self-adjusting ones are beginner-friendly.
- **Helping Hands (Third Hand)** — Clamps with magnifying glass for holding PCBs during soldering.
- **Desoldering Pump (Solder Sucker)** — Removes solder for corrections. Pair with desoldering wick.
- **Breadboard** — 830 tie-points. The #1 tool for solderless prototyping.
- **Precision Screwdriver Set** — For trimpots, terminal blocks, and enclosure screws.
- **Needle-Nose Pliers & Flush Cutters** — Bending leads and snipping excess wire.
- **Hot Glue Gun** — Securing wires and insulating exposed joints.
- **USB Power Bank (5V)** — Safe, portable power source for breadboard circuits.
- **Breadboard Power Supply Module** — Plugs into breadboard, provides 3.3V / 5V from a barrel jack.
- **Oscilloscope (Entry-level)** — Optional but invaluable. DSO150 (pocket), Rigol DS1054Z (budget), or a PC-based Hantek 6022BE. [DS1054Z Guide](https://www.eevblog.com/files/RigolDS1000ZGuide.pdf)

## Basic Concepts Every Beginner Must Know

### Ohm's Law
```
V = I × R      Voltage (V) = Current (A) × Resistance (Ω)
I = V / R      Current  = Voltage ÷ Resistance
R = V / I      Resistance = Voltage ÷ Current
```

### Power
```
P = V × I      Power (W) = Voltage × Current
P = I² × R     Power = Current² × Resistance
P = V² / R     Power = Voltage² ÷ Resistance
```

### Voltage Divider
```
Vout = Vin × (R2 / (R1 + R2))
```
Key rule: Use resistors ≤10kΩ for stable dividers (higher values are noisy and affected by load).

### Pull-up / Pull-down Resistors
- **Pull-up** → Connects pin to VCC through a resistor (e.g., 10kΩ). Pin reads HIGH when the switch is open.
- **Pull-down** → Connects pin to GND through a resistor. Pin reads LOW when the switch is open.
- Common values: 1kΩ–100kΩ (10kΩ is the sweet spot for microcontrollers).

### RC Time Constant
```
τ = R × C      Time constant (seconds) = Resistance (Ω) × Capacitance (F)
```
- After 1τ: charge reaches 63% of final voltage.
- After 5τ: fully charged (~99%).

### Reading Resistor Color Codes
| Color  | Digit | Multiplier  | Tolerance |
|--------|-------|-------------|-----------|
| Black  | 0     | ×1Ω         | —         |
| Brown  | 1     | ×10Ω        | ±1%       |
| Red    | 2     | ×100Ω       | ±2%       |
| Orange | 3     | ×1kΩ        | —         |
| Yellow | 4     | ×10kΩ       | —         |
| Green  | 5     | ×100kΩ      | ±0.5%     |
| Blue   | 6     | ×1MΩ        | ±0.25%    |
| Violet | 7     | ×10MΩ       | ±0.1%     |
| Gray   | 8     | ×100MΩ      | —         |
| White  | 9     | —           | —         |
| Gold   | —     | ×0.1Ω       | ±5%       |
| Silver | —     | ×0.01Ω      | ±10%      |

**Example**: Red-Red-Orange-Gold → 2 2 ×1kΩ ±5% = **22kΩ**.

### Common Circuit Symbols

| Component | Symbol |
|-----------|--------|
| Resistor  | ──▭── or ──\/\/── |
| Capacitor | ──┤├── (non-polarized), ──┤├── (polarized with +) |
| Diode     | ──▶|── (arrow + bar) |
| Ground    | ──⊥ or ──≡ |
| VCC       | ──⬜ (voltage source label) |
| LED       | ──▶|── with two arrows |
| Inductor  | ──◠◡◠── |

## Beginner's Survival Guide

Practical skills that tutorials skip but you'll need on day one.

### How to Read a Datasheet

A datasheet is the single source of truth for any component. Don't be intimidated — you only need a few sections:

1. **Absolute Maximum Ratings** — Never exceed these. Exceeding voltage/current ratings = dead component.
2. **Electrical Characteristics** — Typical operating values (forward voltage, gain, threshold voltage, etc.).
3. **Pinout / Pin Configuration** — Which pin does what. The dot/notch marks pin 1.
4. **Typical Application Circuit** — Copy-paste starting point. Datasheets often show you exactly how to wire it.
5. **Package / Mechanical Drawing** — Physical dimensions for PCB layout.

**Pro tip:** Search for the part number + "app note" for detailed design guidance beyond the datasheet.

### How to Identify Components Physically

| Component | How to Recognize |
|-----------|-----------------|
| Resistor | Small cylinder with color bands (through-hole) or tiny rectangle (SMD) |
| Ceramic Capacitor | Small orange/brown disc or cube (through-hole), tiny beige rectangle (SMD) |
| Electrolytic Capacitor | Cylindrical can, has a stripe marking negative lead, marked with µF |
| Diode | Small glass or black cylinder with a band marking the cathode (negative) |
| LED | Clear or colored dome with two leads (longer = anode/positive) |
| Transistor (TO-92) | Small black half-cylinder with 3 leads |
| Transistor (TO-220) | Larger package with metal tab for heat sinking, 3 leads |
| IC (DIP) | Black rectangle with 7.62mm-wide body, dual rows of pins |
| IC (SMD) | Tiny black rectangle with pads on underside or edges |

### How to Read IC Pinouts

- Find the notch or dot on the IC — that marks **pin 1**.
- Pins count counter-clockwise from pin 1 (down the left side, up the right).
- DIP packages: notch faces up or left.
- SMD SOIC: dot marks pin 1.

```
        ___
  1  o |   | o  8    ← Pin 1 = bottom-left (notch up)
  2    |   |    7
  3    |   |    6
  4    |___|    5
       notch
```

### Prototyping Tips (Breadboard)

- **Power rails are vertical** — The long strips on the sides run the full length. Connect them with jumpers if you need both VCC and GND rails.
- **Center gap disconnects** — The two halves of the breadboard are NOT connected across the center channel. This is where DIP ICs straddle.
- **Use consistent colors** — Red = VCC, Black = GND, other colors for signals. Future-you will thank present-you.
- **Keep wires short** — Long jumper wires create antennas for noise. Route wires close to the board.
- **One component per row** — Don't stack multiple leads in the same row unless they're meant to be connected.
- **Decoupling caps close to ICs** — Place a 100nF ceramic cap as close as physically possible to each IC's VCC/GND pins.

### Systematic Troubleshooting

When your circuit doesn't work (it won't, often), follow this order:

1. **Visual inspection** — Wrong component? Reversed polarity? Bent pin? Cold solder joint?
2. **Check power** — Is VCC actually 5V (or 3.3V) at the IC? Measure between VCC and GND pins directly.
3. **Check ground** — Is GND connected everywhere it should be? A floating ground causes mysterious behavior.
4. **Check signals with a multimeter** — Is the input signal what you expect? Is the output stuck high/low?
5. **Check with an oscilloscope** — Is there a signal at all? Is it the right frequency? Is there noise?
6. **Isolate the problem** — Disconnect subsystems one at a time. Binary search for the broken section.
7. **Read the datasheet again** — You probably missed a requirement (minimum pulse width, pull-up needed, timing constraint).

**The #1 beginner mistake:** Assuming the microcontroller is fine and the circuit is wrong. Test the microcontroller output first — blink an LED on the pin before connecting it to anything else.

### How to Use a Multimeter

| Mode | What It Does | How to Use |
|------|-------------|------------|
| DC Voltage (V⎓) | Measures DC voltage | Red probe to positive, black to ground. Circuit must be powered on. |
| AC Voltage (V~) | Measures AC voltage | Same probe placement. For mains — be careful. |
| Resistance (Ω) | Measures resistance | Circuit must be OFF and component isolated. |
| Continuity (beep) | Checks connection | Touch both probes — beeps if connected. Great for finding broken traces. |
| Diode mode (▶|) | Tests diodes | Red to anode, black to cathode. Shows forward voltage drop (0.5–0.7V for silicon). |
| Current (A) | Measures current | **Break the circuit** and insert the meter in series. Start with the 10A range. |

**Never measure resistance on a live circuit.** You'll get garbage readings and possibly damage the meter.

### Component Naming Conventions

Why is it called "1N4148" or "2N2222"?

| Prefix | Meaning | Example |
|--------|---------|---------|
| **1N** | 1-junction semiconductor (diode) | 1N4148, 1N4007 |
| **2N** | 2-junction semiconductor (transistor) | 2N2222, 2N2907 |
| **3N** | 3-junction semiconductor (FET) | 3N201 |
| **LM** | Linear Monolithic (TI/NS) | LM358, LM317, LM7805 |
| **NE/SE** | Original Signetics (now TI) | NE555, NE5532 |
| **CD/HEF** | CMOS logic (NXP/Philips) | CD4017, HEF4066 |
| **MC/MC14** | Motorola CMOS | MC14017 |
| **AT/ATMEL** | Atmel (now Microchip) | ATmega328P, ATtiny85 |
| **STM/STM32** | STMicroelectronics | STM32F103, STM32F407 |
| **ESP** | Espressif | ESP8266, ESP32 |
| **AMS** | Advanced Monolithic Systems | AMS1117 |

### Soldering Tips (When You're Ready)

- **Tin the tip** — Apply a thin layer of solder to the iron tip before each joint.
- **Heat the joint, not the solder** — Touch the iron to the pad and lead for 1–2 seconds, then apply solder to the joint (not the iron).
- **Good joint = shiny and cone-shaped** — Dull, blobby, or cracked joints are cold joints (bad).
- **Don't hold solder on the iron** — Solder should melt on the heated joint, not on the iron tip.
- **Lead-free is harder** — Starts with leaded solder (63/37 Sn/Pb). It melts at a lower temperature and flows better.
- **Use flux** — Especially for SMD. Flux removes oxidation and helps solder flow cleanly.
- **Practice on scrap first** — Solder 10 through-hole components on a junk board before attempting anything you care about.

### How to Read Schematics

- **Wires connected** = Lines that meet at a dot (●). Lines that cross without a dot are NOT connected.
- **Buses** — Thick lines or labels (VCC, GND, D0–D7) mean "all these pins connect to the same net."
- **GND symbols** — Every ground symbol means "connect to the common ground plane." Don't run a wire to each one.
- **VCC/Power symbols** — Same idea — every VCC symbol connects to the positive supply rail.
- **Net labels** — A label like "SDA" on two different wires means they're connected, even if they're on opposite sides of the page.
- **Bubbles on inputs/outputs** — A small circle means active-low or inverted signal.

### Understanding Datasheets: Key Parameters

| Parameter | What It Means | Why It Matters |
|-----------|--------------|----------------|
| **V_CC / V_DD** | Supply voltage range | Exceed it = dead IC |
| **I_CC / I_DD** | Supply current | Affects battery life |
| **V_IL / V_IH** | Input low/high voltage thresholds | Defines what the IC reads as 0 or 1 |
| **V_OL / V_OH** | Output low/high voltage | What the IC can drive |
| **I_OL / I_OH** | Output current | How much load the output can sink/source |
| **f_max** | Maximum clock/signal frequency | Defines speed limits |
| **t_r / t_f** | Rise/fall time | Signal speed, affects high-frequency performance |
| **P_D** | Power dissipation | Heat generated — affects thermal design |
| **θ_JA** | Junction-to-ambient thermal resistance | How hot the die gets per watt dissipated |
| **T_j** | Operating junction temperature | Maximum die temperature |

### How to Start When You Have Zero Parts

1. **Buy one starter kit** (Elegoo, SparkFun, Adafruit). Don't buy individual parts yet.
2. **Blink an LED** — The "Hello World." Verify your toolchain works.
3. **Read the kit's tutorial book** — Actually do the projects, not just read them.
4. **Break things on purpose** — Reverse an LED. Short a resistor. Watch what happens. This builds intuition.
5. **Build something YOU want** — A night light, a doorbell, a temperature display. Motivation > curriculum.
6. **Then buy individual parts** — After you know what you need, buy from DigiKey/Mouser/AliExpress.
7. **Keep a parts box** — Small ziplock bags or tackle boxes. Label everything. You WILL lose track otherwise.

## Where to Buy Components

### International (reliable, beginner-friendly)
- **[DigiKey](https://www.digikey.com/)** — Massive inventory, fast shipping, great filtering. Best for exact parts.
- **[Mouser](https://www.mouser.com/)** — Similar to DigiKey. Often has better stock for new ICs.
- **[AliExpress](https://www.aliexpress.com/)** — Cheapest, but ship in 2–6 weeks. Great for modules and bulk passive components. Stick to sellers with 95%+ positive feedback.
- **[LCSC](https://www.lcsc.com/)** — Cheap genuine Chinese parts. Good for JLCPCB assembly orders.
- **[Adafruit](https://www.adafruit.com/)** — Premium quality, excellent tutorials, beginner-focused.
- **[SparkFun](https://www.sparkfun.com/)** — Great for breakout boards and learning kits.
- **[Pololu](https://www.pololu.com/)** — Robotics and motor driver specialists.

### USA / Europe / Regional
- **[Amazon](https://www.amazon.com/)** — Fast (Prime), good for starter kits and tools. Overpriced for individual components.
- **[Tayda Electronics](https://www.taydaelectronics.com/)** — Budget-friendly passive components and ICs.
- **[eBay](https://www.ebay.com/)** — Good for vintage ICs and salvaged parts.
- **[RS Components](https://www.rs-online.com/)** — Industrial supplier, UK/Europe.
- **[Farnell / Newark](https://www.newark.com/)** — Professional distributor, strong in Europe.
- **[Reichelt](https://www.reichelt.de/)** — German supplier, good prices in EU.
- **[Botland](https://botland.com/)** — EU robotics and Arduino store.

## Recommended Starter Kits

- **[Elegoo UNO Project Super Starter Kit](https://www.elegoo.com/products/elegoo-uno-project-super-starter-kit)** — Best value. Includes Arduino-compatible board, breadboard, sensors, motors, LEDs, and a tutorial guide.
- **[Adafruit METRO 328 Starter Pack](https://www.adafruit.com/product/3333)** — Quality components, well-documented projects.
- **[SunFounder Ultimate Starter Kit](https://www.sunfounder.com/products/ultimate-starter-kit)** — Arduino + sensors + LCD + servo. Great tutorial structure.
- **[Freenove Ultimate Starter Kit](https://www.freenove.com/store/index.php?route=product/product&product_id=142)** — Excellent code documentation. Arduino and Raspberry Pi versions.
- **[SparkFun Inventor's Kit](https://www.sparkfun.com/products/15267)** — Quality board and components. Best for absolute beginners.
- **DIY Bundle from AliExpress** — Search "37 sensor kit Arduino" (~$12). Cheap way to collect 37 sensor modules, though quality varies.
- **[Raspberry Pi Starter Kit](https://www.raspberrypi.com/products/raspberry-pi-4-starter-kit/)** — Complete computer + GPIO. Great for Python-based electronics if you want to skip C++.

## Beginner Project Ladder

Work through these in order. Each builds on the last.

**Level 1 — No programming needed**
1. **Blink an LED** — Resistor + LED + battery. Understand forward voltage and current limiting.
2. **Voltage divider** — Two resistors + multimeter. Measure Vout. Understand ratio.
3. **Simple dimmer** — Potentiometer + LED. Variable resistance controls brightness.
4. **LDR night light** — LDR + transistor + LED. Circuit turns on when it gets dark.

**Level 2 — With a microcontroller (Arduino / ESP32)**
5. **Blink (software)** — Pin 13 LED. Hello world of MCUs.
6. **Push button input** — Read button state, turn LED on/off. Learn INPUT_PULLUP.
7. **PWM fade** — AnalogWrite() to fade LED. Understand PWM.
8. **Temperature display** — LM35 + serial monitor or LCD (I²C 1602). Learn ADC and serial.

**Level 3 — Sensors & Actuators**
9. **Ultrasonic distance meter** — HC-SR04 + buzzer. Learn timing-based sensors.
10. **PIR alarm** — PIR sensor + relay + siren (or buzzer). Motion-triggered output.
11. **Servo sweep** — Potentiometer controls servo position. Learn pulse-width control.
12. **Soil moisture monitor** — Moisture sensor + RGB LED (green = wet, red = dry).

**Level 4 — Communication & Displays**
13. **I²C temperature/humidity** — DHT22 + OLED display. Learn I²C protocol.
14. **Bluetooth remote** — HC-05 + phone app to control LED brightness. Learn serial UART.
15. **Wi-Fi weather station** — ESP8266/ESP32 + BMP280 → send data to ThingSpeak or MQTT.
16. **Joystick game controller** — Analog joystick + OLED. Draw a moving dot.

**Level 5 — Intermediate Projects**
17. **Line-following robot** — 2 IR sensors + L298N motor driver + 2 DC motors.
18. **Digital thermometer (1-Wire)** — DS18B20 + OLED. Learn parasitic power and 1-Wire protocol.
19. **Web-controlled relay** — ESP32 + relay module. Control a lamp from a web dashboard.
20. **Function generator** — AD9833 module + op-amp + rotary encoder. Generate sine/square/triangle.

**Level 6 — Advanced**
21. **Buck converter design** — Build a LM2596-based adjustable PSU module.
22. **PID temperature controller** — SSR + thermocouple + relay. Maintain a setpoint.
23. **Custom PCB** — Design a shield in KiCad/EasyEDA. Fab at JLCPCB. Solder SMD.
24. **RTOS on ESP32** — FreeRTOS tasks: Wi-Fi + sensor logging + OLED refresh concurrently.

**Level 7 — Smart Farm / AgTech (IoT + Agriculture)**
25. **LoRa soil monitor** — ESP32 + capacitive moisture + BME280 → LoRa → TTN. Battery + solar. Deploy in the garden.
26. **Closed-loop irrigation** — ESP32 + capacitive sensor + 12V solenoid valve. Water only when soil is dry (no timers).
27. **Weather station** — BME280 + anemometer + rain gauge + wind vane → publishes to MQTT/ThingSpeak.
28. **Greenhouse controller** — DHT22 + CO₂ (SCD30) + BH1750 + relay (fan/heater) + OLED. Maintain climate setpoints.
29. **Livestock ID gate** — RDM6300 RFID reader logs which animals pass a feeder to SD card / MQTT.
30. **Crop stress drone** — MLX90640 thermal camera on a gimbal/phone mount to spot under-watered field zones; map in Grafana.
31. **Farm gateway** — Raspberry Pi running Mosquitto + Node-RED + InfluxDB + Grafana; aggregates all field nodes into one dashboard.

## Commonly Asked Beginner Questions

**Q: What resistor do I use with an LED?**
```
R = (Vcc - Vf) / If
```
Example: Vcc=5V, Vf(red LED)=2V, If=20mA → R = (5-2)/0.02 = 150Ω (use 220Ω to be safe).

**Q: How do I choose a decoupling capacitor?**
Put a 100nF ceramic cap between VCC and GND as close to each IC's power pins as possible. This suppresses noise and prevents glitches.

**Q: Why does my breadboard circuit not work?**
Check: common mistakes —
1. Power rails not connected (verify row continuity with multimeter).
2. Pin headers inserted one row off.
3. IC orientation wrong (dot marks pin 1).
4. Missing pull-up resistor on reset pin (for AVR).
5. Ground not shared (all circuits must reference the same GND).

**Q: 3.3V vs 5V logic — can they talk?**
- 5V output → 3.3V input: Use a voltage divider (e.g., 4.7kΩ + 10kΩ) or a level shifter like BSS138 MOSFET.
- 3.3V output → 5V input: Often works (3.3V is HIGH enough for most 5V logic), but use a level shifter for reliability.
- Buy: [8-channel Bi-Directional Logic Level Converter](https://www.sparkfun.com/products/12009).

**Q: What's PWM and when do I use it?**
Pulse Width Modulation — rapidly switches a pin HIGH/LOW at a frequency (e.g., 490 Hz). Duty cycle (0–100%) simulates an analog voltage. Used for: LED dimming, servo control, motor speed control.

## Learning Resources

- [All About Circuits](https://www.allaboutcircuits.com/) — Tutorials and technical articles
- [SparkFun Tutorials](https://learn.sparkfun.com/) — Beginner-friendly electronics guides
- [Adafruit Learning System](https://learn.adafruit.com/) — Extensive project-based tutorials
- [EEVblog](https://www.eevblog.com/) — Electronics engineering blog and forum
- [CircuitLab](https://www.circuitlab.com/) — Online circuit simulator
- [Falstad Circuit Simulator](https://www.falstad.com/circuit/) — Interactive circuit simulation
- [EasyEDA / LCSC / JLCPCB](https://easyeda.com/) — PCB design + component sourcing + fabrication
- [Khan Academy — Electrical Engineering](https://www.khanacademy.org/science/electrical-engineering) — Free foundations course
- [GreatScott!](https://www.youtube.com/@greatscottlab) — YouTube: best project tutorials for beginners
- [ElectroBOOM](https://www.youtube.com/@ElectroBOOM) — YouTube: education through entertaining (and painful) mishaps
- [Ben Eater](https://www.youtube.com/@BenEater) — YouTube: build a computer on a breadboard from scratch
- [KiCad EDA](https://www.kicad.org/) — Free and open-source PCB design tool

## Open-Source & Free Tools

Everything you need — from schematic to soldering — without spending a cent on software.

### PCB Design & Schematic Capture
- **[KiCad](https://www.kicad.org/)** — Full EDA suite: schematic, PCB layout, Gerber export. The gold standard for open-source PCB design. [Docs](https://docs.kicad.org/)
- **[gEDA](http://www.geda-project.org/)** — Mature open-source EDA suite. Schematic (gschem), PCB layout (PCB), Gerber viewer. [Docs](http://wiki.geda-project.org/)
- **[Horizon EDA](https://horizon-eda.github.io/)** — Modern KiCad alternative. Schematic + PCB + pool manager. GTK-based. [Docs](https://horizon-eda.github.io/horizon-eda-docs/)
- **[Fritzing](https://fritzing.org/)** — Breadboard view + schematic + PCB. Designed for beginners and documentation. [Docs](https://fritzing.org/handbook/)
- **[EasyEDA](https://easyeda.com/)** — Free web-based EDA. Integrates with JLCPCB/LCSC for one-click ordering. [Docs](https://docs.easyeda.com/)

### Circuit Simulation
- **[ngspice](https://ngspice.sourceforge.io/)** — Open-source SPICE simulator. Industry-standard analog simulation. [Docs](https://ngspice.sourceforge.io/docs.html)
- **[QUCS-S](https://qucs-s-filter-design.github.io/)** — Quite Universal Circuit Simulator with SPICE integration. RF/analog/mixed-signal. [Docs](https://github.com/ra3xdh/qucs_s)
- **[LTspice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)** — Free from Analog Devices. Best-in-class switching regulator simulation. (Proprietary but free.) [Docs](https://www.analog.com/en/resources/reference-designs/circuits-from-the-lab/cn0252.html)
- **[Falstad Circuit Simulator](https://www.falstad.com/circuit/)** — Interactive web-based simulator. Instant visual feedback. Great for learning. [Docs](https://www.falstad.com/circuit/circuitjs.html)
- **[Digital](https://github.com/hneemann/Digital)** — Open-source logic simulator. Build CPUs, ALUs, FSMs from gates. [Docs](https://github.com/hneemann/Digital/wiki)
- **[Logisim](http://www.cburch.com/logisim/)** — Visual logic simulator for teaching digital circuits. (Original, unmaintained. Use [Logisim-evolution](https://github.com/logisim-evolution/logisim-evolution) fork.) [Docs](https://github.com/logisim-evolution/logisim-evolution/wiki)
- **[TINA-TI](https://www.ti.com/tool/TINA-TI)** — Free from TI. SPICE-based analog simulation. (Proprietary but free.) [Docs](https://www.ti.com/tool/TINA-TI)

### Firmware & Development IDEs
- **[Arduino IDE](https://www.arduino.cc/en/software)** — The classic. Write sketches, flash to Arduino/ESP32/ATmega. [Docs](https://www.arduino.cc/en/Guide)
- **[Arduino IDE 2.0](https://www.arduino.cc/en/software)** — Modern rewrite. Serial monitor, autocomplete, debugger. [Docs](https://docs.arduino.cc/software/ide-v2/)
- **[PlatformIO](https://platformio.org/)** — Build system + IDE plugin. Manages libraries, boards, frameworks. Supports 1000+ boards. [Docs](https://docs.platformio.org/)
- **[VS Code](https://code.visualstudio.com/)** — General-purpose editor. Extensions for Arduino, PlatformIO, ESP-IDF. [Docs](https://code.visualstudio.com/docs)
- **[ESP-IDF](https://docs.espressif.com/projects/esp-idf/)** — Espressif's official framework for ESP32. FreeRTOS-based. [Docs](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/)
- **[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)** — Free from ST. Debugger, code generation, HAL. (Proprietary but free.) [Docs](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_STM32CubeIDE)
- **[STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)** — Graphical pin/clock configurator for STM32. Generates initialization code. (Proprietary but free.)
- **[PlatformIO CLI](https://docs.platformio.org/en/latest/core/index.html)** — Command-line build tool. CI/CD-friendly. [Docs](https://docs.platformio.org/en/latest/core/cli.html)

### Embedded Languages & Frameworks
- **[MicroPython](https://micropython.org/)** — Lean Python for microcontrollers. ESP32, STM32, RP2040, etc. [Docs](https://docs.micropython.org/)
- **[CircuitPython](https://circuitpython.org/)** — Adafruit's fork of MicroPython. Hardware-focused libraries, USB HID, built-in REPL. [Docs](https://learn.adafruit.com/welcome-to-circuitpython)
- **[ESPHome](https://esphome.io/)** — YAML-configured firmware for ESP32/ESP8266. Integrates with Home Assistant. [Docs](https://esphome.io/)
- **[Tasmota](https://tasmota.github.io/)** — Open firmware for ESP-based smart plugs/switches/sensors. [Docs](https://tasmota.github.io/docs/)
- **[Zephyr RTOS](https://www.zephyrproject.org/)** — Industrial-grade RTOS. ARM, RISC-V, x86, ARC. [Docs](https://docs.zephyrproject.org/latest/)
- **[FreeRTOS](https://www.freertos.org/)** — Market-leading embedded RTOS. Arduino Core for ESP32 uses it. [Docs](https://www.freertos.org/Documentation.html)
- **[RIOT OS](https://riot-os.org/)** — Microkernel RTOS for IoT. Multi-threading, networking stacks. [Docs](https://doc.riot-os.org/)
- **[Mbed OS](https://os.mbed.com/)** — ARM's IoT OS. Broad MCU support. [Docs](https://os.mbed.com/docs/latest/)
- **[Emscripten](https://emscripten.org/)** — Compile C/C++ to WebAssembly. Run embedded code in the browser. [Docs](https://emscripten.org/docs/getting_started/)

### FPGA Development
- **[Yosys](https://github.com/YosysHQ/yosys)** — Open-source Verilog synthesis. The backbone of open-source FPGA toolchains. [Docs](https://github.com/YosysHQ/yosys/wiki)
- **[nextpnr](https://github.com/YosysHQ/nextpnr)** — Open-source place-and-route. Timing-driven. Supports Lattice, iCE40, ECP5, etc. [Docs](https://github.com/YosysHQ/nextpnr/wiki)
- **[Project IceStorm](https://github.com/flopp/icestorm)** — Open-source tools for Lattice iCE40 FPGAs. Synthesis + bitstream. [Docs](https://github.com/flopp/icestorm)
- **[Verilator](https://www.veripool.org/verilator/)** — Fast Verilog/SystemVerilog simulator. Compiles to C++. [Docs](https://www.veripool.org/verilator/manual/verilator.html)
- **[cocotb](https://github.com/cocotb/cocotb)** — Python testbench framework for HDL simulation. Works with Verilator, Icarus, etc. [Docs](https://docs.cocotb.org/)
- **[Icarus Verilog](https://steveicarus.github.io/iverilog/)** — Open-source Verilog simulator. Good for learning. [Docs](https://steveicarus.github.io/iverilog/)
- **[Amaranth HDL](https://amaranth-lang.org/)** — Python-based HDL. Build hardware with Python syntax. [Docs](https://amaranth-lang.org/docs/main/)
- **[Lattice Radiant](https://www.latticesemi.com/products/designsoftwareandipools/softwareradiant)** — Free for Lattice FPGAs. (Proprietary but free.)

### 3D CAD & Enclosures
- **[FreeCAD](https://www.freecad.org/)** — Parametric 3D modeler. Great for enclosures, mounts, brackets. [Docs](https://wiki.freecad.org/)
- **[OpenSCAD](https://openscad.org/)** — Script-based 3D modeling. Code-driven, reproducible designs. [Docs](https://en.wikibooks.org/wiki/OpenSCAD_User_Manual)
- **[OpenVoronoi](https://github.com/aewallin/openvoronoi)** — Voronoi diagram library for CNC/toolpath generation.
- **[Manifold](https://github.com/elalish/manifold)** — Fast mesh Boolean operations (CSG). For combining/ subtracting 3D shapes. [Docs](https://manifoldcad.org/)
- **[OpenJSCAD](https://openjscad.xyz/)** — JavaScript-based parametric CAD. Browser-based. [Docs](https://openjscad.xyz/)

### 3D Printing
- **[PrusaSlicer](https://www.prusa3d.com/page/prusaslicer_424/)** — Slicer for FDM printers. Tree supports, paint-on supports, organic supports. [Docs](https://help.prusa3d.com/category/prusaslicer_202)
- **[Cura](https://ultimaker.com/software/ultimaker-cura/)** — Ultimaker's slicer. Widely used, plugin ecosystem. [Docs](https://support.ultimaker.com/s/hc/en-us/360009792379-Cura)
- **[OrcaSlicer](https://github.com/SoftFever/OrcaSlicer)** — Fork of PrusaSlicer/BambuStudio. Multi-printer support. [Docs](https://github.com/SoftFever/OrcaSlicer/wiki)
- **[OctoPrint](https://octoprint.org/)** — Web interface for managing 3D printers. Webcam, G-code editor, plugins. [Docs](https://docs.octoprint.org/)
- **[Klipper](https://www.klipper3d.org/)** — 3D printer firmware. Runs on Raspberry Pi, offloads real-time to MCU. [Docs](https://www.klipper3d.org/Overview.html)
- **[Marlin](https://marlinfw.org/)** — Popular open-source 3D printer firmware. Runs on AVR/ARM MCUs. [Docs](https://marlinfw.org/meta/sk/)
- **[Repetier](https://www.repetier.com/)** — Open-source firmware for FDM printers. Multi-extruder support. [Docs](https://www.repetier.com/documentation/)

### Logic & Digital Simulation
- **[Digital](https://github.com/hneemann/Digital)** — Build CPUs, ALUs, FSMs from individual gates. Interactive step-through. [Docs](https://github.com/hneemann/Digital/wiki)
- **[Logisim-evolution](https://github.com/logisim-evolution/logisim-evolution)** — Fork of Logisim. Active development, 8-bit CPUs, teaching tools. [Docs](https://github.com/logisim-evolution/logisim-evolution/wiki)
- **[TLC (The Logisim Creator)](https://github.com/tlac/logisim-creator)** — Next-gen logic simulator. WIP but promising.
- **[Digitaljs](https://github.com/tilk/digitaljs)** — Browser-based digital logic simulator. [Docs](https://digitaljs.tilk.dev/)
- **[nand2tetris tools](https://github.com/ghaiklor/nand-2-tetris)** — Build a computer from NAND gates to OS. Based on the famous course. [Docs](https://www.nand2tetris.org/)

### Signal Analysis & Test
- **[Calculation Hub dB to Volume Calculator](https://calculation-hub.com/music/db-to-volume)** — Free explained amplitude/power ratio arithmetic for signal study; not loudness measurement, hardware calibration, or hearing-safety advice.
- **[Audacity](https://www.audacityteam.org/)** — Audio editor/analyzer. Great for analyzing sensor audio output, microphone signals. [Docs](https://support.audacityteam.org/)
- **[Inspectrum](https://github.com/miek/inspectrum)** — RF signal analysis tool. Visualize IQ data, demodulate signals. [Docs](https://github.com/miek/inspectrum)
- **[Universal Radio Hacker (URH)](https://github.com/jopohl/urh)** — IoT protocol analysis. Decode, analyze, and replay wireless signals. [Docs](https://github.com/jopohl/urh)
- **[GNU Radio](https://www.gnuradio.org/)** — Signal processing framework. SDR, filters, modulation/demodulation. [Docs](https://wiki.gnuradio.org/)
- **[Sigrok](https://sigrok.org/)** — Logic analyzer / protocol analyzer. Supports 100+ protocols. [Docs](https://sigrok.org/wiki/Documentation)
- **[PulseView](https://sigrok.org/wiki/PulseView)** — Sigrok's GUI. Capture and decode digital signals. [Docs](https://sigrok.org/wiki/PulseView)
- **[WaveView](https://sigrok.org/wiki/WaveView)** — Sigrok's waveform viewer. Analyze captured signals.

### Protocol Analyzers
- **[Wireshark](https://www.wireshark.org/)** — Network protocol analyzer. USB, Ethernet, Bluetooth, etc. [Docs](https://www.wireshark.org/docs/)
- **[nmap](https://nmap.org/)** — Network discovery and security auditing. [Docs](https://nmap.org/docs.html)
- **[mosquitto](https://mosquitto.org/)** — MQTT broker. Lightweight, runs anywhere. [Docs](https://mosquitto.org/documentation/)
- **[Mosquitto clients](https://mosquitto.org/)** — CLI tools for publishing/subscribing to MQTT topics.

### Home Automation & IoT Platforms
- **[Home Assistant](https://www.home-assistant.io/)** — Open-source home automation hub. Integrates Zigbee, Z-Wave, Wi-Fi, MQTT, 2000+ integrations. [Docs](https://www.home-assistant.io/docs/)
- **[OpenHAB](https://www.openhab.org/)** — Java-based home automation. Device-agnostic. [Docs](https://www.openhab.org/docs/)
- **[Domoticz](https://www.domoticz.com/)** — Lightweight home automation. Low resource usage. [Docs](https://www.domoticz.com/wiki/Main_Page)
- **[ThingsBoard](https://thingsboard.io/)** — Open-source IoT platform. Device management, dashboards, rules engine. [Docs](https://thingsboard.io/docs/)
- **[Node-RED](https://nodered.org/)** — Flow-based programming for IoT. Wires APIs, devices, services. [Docs](https://nodered.org/docs/)
- **[Blynk IoT](https://blynk.io/)** — Mobile app for IoT. Drag-and-drop dashboards. (Freemium.) [Docs](https://docs.blynk.io/)
- **[ThingSpeak](https://thingspeak.com/)** — MathWorks IoT platform. MATLAB visualization. (Free for non-commercial.) [Docs](https://thingspeak.com/pages/site_doc)
- **[MQTT Explorer](https://mqtt-explorer.com/)** — GUI for debugging MQTT. Visualize topics in real-time. [Docs](https://mqtt-explorer.com/)

### Embedded Debugging
- **[OpenOCD](https://openocd.org/)** — On-Chip Debugger. Flash and debug ARM, RISC-V, MIPS via JTAG/SWD. [Docs](https://openocd.org/doc/html/)
- **[GDB](https://www.gnu.org/software/gdb/)** — GNU Debugger. Step through code, inspect variables, breakpoints. [Docs](https://sourceware.org/gdb/documentation/onlinedocs/gdb/)
- **[probe-rs](https://probe.rs/)** — Modern Rust-based debugging toolkit. Supports CMSIS-DAP, ST-Link, J-Link. [Docs](https://probe.rs/docs/)
- **[Black Magic Probe](https://blackmagicdebug.com/)** — Open-source JTAG/SWD probe. No external debug adapter needed. [Docs](https://blackmagicdebug.com/)

### Hardware Documentation & Version Control
- **[Git](https://git-scm.com/)** — Version control. Track changes to schematics, firmware, documentation. [Docs](https://git-scm.com/doc)
- **[GitHub](https://github.com/)** — Code hosting. Issues, PRs, Actions CI/CD. Free for public repos. [Docs](https://docs.github.com/)
- **[GitLab](https://about.gitlab.com/)** — Alternative to GitHub. Self-hostable. Free tier includes CI/CD. [Docs](https://docs.gitlab.com/)
- **[Gitea](https://gitea.com/)** — Self-hosted Git service. Lightweight, easy to deploy. [Docs](https://docs.gitea.com/)
- **[HackMD](https://hackmd.io/)** — Collaborative markdown docs. Real-time editing. [Docs](https://docs.hackmd.io/)
- **[HackMD CLI](https://github.com/hackmdio/hackmd-cli)** — Create/edit HackMD docs from terminal.
- **[Docusaurus](https://docusaurus.io/)** — Static site generator for docs. Build a project wiki. [Docs](https://docusaurus.io/docs)
- **[KiBot](https://github.com/INTI-CMNB/KiBot)** — CI/CD for KiCad. Auto-generate Gerbers, BOMs, schematics on commit. [Docs](https://inti-cmnb.github.io/KiBot/)

### Antenna & RF Design
- **[4NEC2](https://www.qsl.net/on5au/Homep2/4NEC2.htm)** — NEC-based antenna modeler and optimizer. Windows. (Free.) [Docs](https://www.qsl.net/on5au/Homep2/4NEC2.htm)
- **[MMANA-GAL](https://hamwaves.com/mmana-gal/en/)** — Antenna analysis. Free, Windows. [Docs](https://hamwaves.com/mmana-gal/en/)
- **[openEMS](https://openems.de/)** — Open-source FDTD electromagnetic field solver. For antenna/filter simulation. [Docs](https://openems.de/Start/)
- **[Qucs](https://qucs.sourceforge.net/)** — Quite Universal Circuit Simulator. RF/AC/DC/transient. [Docs](https://qucs.sourceforge.net/)

### PCB Manufacturing & Assembly
- **[JLCPCB](https://jlcpcb.com/)** — $2 PCBs, SMT assembly. Integrates with EasyEDA/KiCad. [Docs](https://jlcpcb.com/helpArticle/440)
- **[PCBWay](https://www.pcbway.com/)** — PCB fabrication + assembly. 5pcs from $5. [Docs](https://www.pcbway.com/help.html)
- **[Fusion 360 Electronics](https://www.autodesk.com/products/fusion-360/electronics)** — Free for personal use. Schematic + PCB + mechanical. (Proprietary but free for hobbyists.)
- **[OpenSCAD export to STL](https://openscad.org/)** — Export 3D models for printing enclosures.

### Documentation & Knowledge
- **[Hackster.io](https://www.hackster.io/)** — Community for hardware projects. Find inspiration, share your work. [Docs](https://www.hackster.io/news)
- **[Instructables](https://www.instructables.com/)** — Step-by-step project guides. Electronics section is huge. [Docs](https://www.instructables.com/)
- **[Hackaday](https://hackaday.com/)** — Hardware hacking blog. Daily inspiration. [Docs](https://hackaday.com/)
- **[EEVblog](https://www.eevblog.com/)** — Electronics engineering blog. Dave Jones teardowns. [Docs](https://www.eevblog.com/forum/)
- **[All About Circuits](https://www.allaboutcircuits.com/)** — Tutorials and technical articles. [Docs](https://www.allaboutcircuits.com/)
- **[Electronics Tutorials](https://www.electronics-tutorials.ws/)** — Theory and circuit examples. [Docs](https://www.electronics-tutorials.ws/)

---

# Component Reference

## Passive Components

### Resistors
- **Resistor** — Limits current flow. Common values: 220Ω, 1kΩ, 10kΩ. [Datasheet](https://www.digikey.com/en/products/filter/through-hole-resistors/52)
- **Potentiometer** — Adjustable resistor (variable voltage divider). Used in volume knobs and tuning. [Datasheet](https://www.digikey.com/en/products/filter/trimmer-potentiometers/43)
- **Current Sense Resistor** — Low-value precision resistor for current measurement. [Datasheet](https://www.digikey.com/en/products/filter/through-hole-resistors/52)

### Capacitors
- **Capacitor (Ceramic)** — Stores and releases electrical energy. Used for filtering, decoupling, timing. [Datasheet](https://www.digikey.com/en/products/filter/ceramic-capacitors/60)
- **Electrolytic Capacitor** — High capacitance in small package. Polarity-sensitive. Good for power supply smoothing. [Datasheet](https://www.digikey.com/en/products/filter/aluminum-electrolytic-capacitors/58)

### Inductors & Transformers
- **Inductor** — Stores energy in a magnetic field. Used in filters, converters, and tuned circuits. [Datasheet](https://www.digikey.com/en/products/filter/fixed-inductors/71)
- **Transformer** — Transfers electrical energy between circuits via electromagnetic induction. Steps voltage up or down. [Datasheet](https://www.digikey.com/en/products/filter/power-transformers/129)

### EMI Suppression
- **Common Mode Choke** — Suppresses EMI/RFI noise on power and signal lines. [Datasheet](https://www.digikey.com/en/products/filter/filters/611)
- **Ferrite Bead** — Suppresses high-frequency noise on power lines. [Datasheet](https://www.digikey.com/en/products/filter/ferrite-beads-and-chips/72)
- **Ferrite Core (Toroid)** — Wound inductor core for EMI suppression and custom inductors. [Datasheet](https://www.digikey.com/en/products/filter/cores/398)
- **Varistor (MOV)** — Voltage-dependent resistor. Clamps voltage spikes for surge protection. [Datasheet](https://www.digikey.com/en/products/filter/tvk-varistors/301)

## Semiconductors

Discrete devices — a single function per package. See [Integrated Circuits](#integrated-circuits) for multi-transistor chips.

### Diodes
- **PN Junction Diode** — Standard rectifier diode (e.g., 1N4007). Used in power supplies. [1N4007 Datasheet](https://www.vishay.com/docs/88503/1n4007.pdf)
- **Schottky Diode** — Fast switching, low forward voltage drop. Great for high-frequency circuits. [1N5819 Datasheet](https://www.diodes.com/assets/Datasheets/1N5819.pdf)
- **Zener Diode** — Conducts in reverse at a specific breakdown voltage. Used for voltage regulation. [BZX84 Datasheet](https://www.diodes.com/assets/Datasheets/BZX84C.pdf)
- **Signal Diode** — Small-signal switching. 1N4148 is the most common diode in electronics. [1N4148 Datasheet](https://www.vishay.com/docs/81857/1n4148.pdf)
- **Fast Recovery Diode (FR107)** — Fast switching rectifier for SMPS applications. [FR107 Datasheet](https://www.vishay.com/docs/88503/1n4007.pdf)
- **TVS Diode (Transient Voltage Suppressor)** — Clamps voltage spikes for ESD/surge protection. [Datasheet](https://www.digikey.com/en/products/filter/tvs-diodes/144)

### Transistors
- **BJT Transistor (NPN/PNP)** — Current-controlled switch or amplifier. 2N2222 (NPN) and 2N2907 (PNP) are common. [2N2222 Datasheet](https://www.onsemi.com/pdf/datasheet/p2n2222a-d.pdf)
- **MOSFET (N-Channel / P-Channel)** — Voltage-controlled switch. Low on-resistance. IRF520, IRFZ44N are popular. [IRFZ44N Datasheet](https://www.infineon.com/dgdl/irfz44npbf.pdf)
- **JFET** — Voltage-controlled resistor. Used in high-input-impedance stages. [J201 Datasheet](https://www.onsemi.com/pdf/datasheet/j201-d.pdf)
- **IGBT** — Combines MOSFET gate with BJT output. For high-voltage switching. [IRG4PC40U Datasheet](https://www.infineon.com/dgdl/irg4pc40upbf.pdf)

### Thyristors & AC Switching
- **TRIAC (BTA16)** — Bidirectional AC switch. Used in dimmers and motor speed control. [BTA16-600BW Datasheet](https://www.st.com/resource/en/datasheet/bta16-600bw.pdf)
- **SCR (BT151)** — Silicon Controlled Rectifier. Latching switch for high-power AC/DC. [BT151 Datasheet](https://www.nxp.com/docs/en/data-sheet/BT151.pdf)
- **DIAC (DB3)** — Bidirectional trigger diode. Pairs with TRIACs for AC switching. [DB3 Datasheet](https://www.st.com/resource/en/datasheet/db3.pdf)
- **Opto-TRIAC (MOC3021)** — TRIAC driver with optical isolation. For AC load control. [MOC3021 Datasheet](https://www.onsemi.com/pdf/datasheet/moc3020-m.pdf)

## Integrated Circuits

Multi-transistor chips that perform a complete function.

### Analog ICs
- **Op-Amp (Operational Amplifier)** — Amplifies differential voltage. LM358, TL071, NE5532 are common. [LM358 Datasheet](https://www.ti.com/lit/ds/symlink/lm358.pdf)
- **Comparator (LM393 / LM311)** — Compares two voltages and outputs a digital signal. [LM393 Datasheet](https://www.ti.com/lit/ds/symlink/lm393.pdf)
- **555 Timer IC** — Generates precise timing pulses (astable/monostable modes). Used in oscillators and delay circuits. [NE555 Datasheet](https://www.ti.com/lit/ds/symlink/ne555.pdf)
- **Voltage Regulator (7805 / LM317)** — Provides stable DC output. 7805 = fixed 5V, LM317 = adjustable. [LM317 Datasheet](https://www.ti.com/lit/ds/symlink/lm317.pdf)
- **LDO Regulator (AMS1117)** — Low dropout linear regulator. 3.3V/5V fixed versions. [AMS1117 Datasheet](https://www.advanced-monolithic.com/pdf/ds1117.pdf)
- **ADC (ADS1115)** — 16-bit I²C ADC. 4 channels. For precision analog measurement. [ADS1115 Datasheet](https://www.ti.com/lit/ds/symlink/ads1115.pdf)
- **DAC (MCP4725)** — 12-bit I²C DAC. For analog signal generation. [MCP4725 Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/22039b.pdf)
- **Digital Potentiometer (MCP41xx)** — Programmable resistor over SPI. [MCP41010 Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/11195c.pdf)

### Digital & Logic ICs
- **Logic Gate ICs (74xx series)** — AND, OR, NAND, NOR, XOR gates for digital logic. 7400, 7402, 7408 are common. [74HC00 Datasheet](https://www.ti.com/lit/ds/symlink/sn74hc00.pdf)
- **Shift Register (74HC595)** — Converts serial data to parallel output. Used to expand output pins. [74HC595 Datasheet](https://www.ti.com/lit/ds/symlink/sn74hc595.pdf)
- **Logic Level Shifter (TXB0108)** — Bidirectional voltage translator. 3.3V ↔ 5V. [TXB0108 Datasheet](https://www.ti.com/lit/ds/symlink/txb0108.pdf)

### Power & Motor Drivers
- **Motor Driver IC (L298N)** — Dual H-Bridge driver. Controls 2 DC motors or 1 stepper. [L298N Datasheet](https://www.st.com/resource/en/datasheet/l298.pdf)
- **Stepper Driver (A4988)** — Microstepping stepper motor driver. Up to 1/16 step. [A4988 Datasheet](https://www.allegromicro.com/-/media/files/datasheets/a4988-datasheet.pdf)
- **MOSFET Driver (IR2110)** — Gate driver for high/low side MOSFETs. For H-bridge circuits. [IR2110 Datasheet](https://www.infineon.com/dgdl/ir2110.pdf)

## Microcontrollers & Processors

- **Microcontroller (MCU)** — Programmable chip with CPU, RAM, I/O. Arduino (ATmega328P), ESP32, STM32 are popular. [ATmega328P Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-7810-Automotive-Microcontrollers-ATmega328P_Datasheet.pdf)

## Optoelectronics

### Light Sources
- **LED (Light Emitting Diode)** — Emits light when forward biased. Available in red, green, blue, white, RGB. [Datasheet](https://www.digikey.com/en/products/filter/led-emitters/105)
- **RGB LED (Common Cathode/Anode)** — Single package with R, G, B dies. PWM-mixable full color. [Datasheet](https://www.digikey.com/en/products/filter/led-emitters/105)
- **Infrared LED (IR LED)** — Emits IR light. Used in remote controls and night vision. [Datasheet](https://www.vishay.com/docs/81181/tsal6200.pdf)
- **Laser Diode** — Coherent light source. Used in barcode scanners, alignment, and optical comms. [Datasheet](https://www.digikey.com/en/products/filter/led-emitters/105)
- **WS2812B (NeoPixel)** — Addressable RGB LED with built-in driver. Chainable via single data line. [Datasheet](https://cdn-shop.adafruit.com/datasheets/WS2812B.pdf)

### Displays
- **Seven-Segment Display** — Shows numeric digits (0–9). Common anode/cathode variants. [Datasheet](https://www.digikey.com/en/products/filter/display-modules-led-character-numeric/114)
- **LCD Character Display (1602)** — 16×2 character display, commonly driven by HD44780. [Datasheet](https://www.sparkfun.com/datasheets/LCD/HD44780.pdf)
- **OLED Display (SSD1306)** — Self-emissive display. 0.96" 128×64 I²C common. [Datasheet](https://cdn-shop.adafruit.com/datasheets/SSD1306.pdf)
- **e-Paper Display (SSD1680)** — Ultra-low power display. Visible in sunlight. For sensor readouts. [Datasheet](https://www.waveshare.com/w/upload/5/5e/SSD1680.pdf)

### Photodetectors
- **Photodiode** — Converts light into current. Used in light sensors and optical communication. [BPW21R Datasheet](https://www.vishay.com/docs/81532/bpw21r.pdf)
- **Phototransistor** — Light-sensitive transistor. Higher gain than photodiode. [Datasheet](https://www.digikey.com/en/products/filter/phototransistors/500)
- **LDR (Light Dependent Resistor)** — Resistance decreases with light. Simple light sensor. [GL5528 Datasheet](https://components101.com/sites/default/files/component_datasheet/LDR%20Datasheet.pdf)
- **IR Receiver (VS1838B)** — Demodulates 38kHz IR signals. For remote control decoding. [Datasheet](https://www.vishay.com/docs/82491/vs1838b.pdf)
- **Color Sensor (TCS3200)** — Detects RGB color using photodiode array. [Datasheet](https://www.fairchildsemi.com/datasheets/TCS/TCS3200.pdf)
- **ToF Sensor (VL53L0X)** — Time-of-Flight laser ranging. 2mm–1200mm range. [Datasheet](https://www.st.com/resource/en/datasheet/vl53l0x.pdf)

### Isolation
- **Optocoupler / Optoisolator** — Transfers signals across isolation barrier using light. PC817, 4N35 are common. [PC817 Datasheet](https://www.sharpsde.com/fileadmin/products/opto/PC817.pdf)

## Sensors & Transducers

### Temperature & Humidity
- **Thermistor (NTC / PTC)** — Resistance changes with temperature. NTC = negative coefficient. [NTC Datasheet](https://www.vishay.com/docs/29049/ntcle100.pdf)
- **LM35 / DS18B20** — Temperature sensor IC. LM35 = analog output, DS18B20 = 1-Wire digital. [DS18B20 Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/ds18b20.pdf)
- **DHT11 / DHT22** — Digital temperature and humidity sensor. [DHT11 Datasheet](https://www.mouser.com/datasheet/2/758/DHT11-Technical-Data-Sheet-Translated-Version-1143054.pdf)
- **IR Temperature Sensor (MLX90614)** — Non-contact infrared temperature measurement. I²C interface. [Datasheet](https://www.adafruit.com/datasheet/MLX90614.pdf)

### Pressure & Altitude
- **BMP180 / BMP280** — Barometric pressure and temperature sensor. [BMP280 Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bmp280-ds001.pdf)

### Motion & Position
- **HC-SR04 Ultrasonic Sensor** — Measures distance using sound waves (2–400 cm range). [Datasheet](https://www.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)
- **PIR Motion Sensor (HC-SR501)** — Detects infrared radiation from moving people/animals. [Datasheet](https://www.mpja.com/download/hc-sr501.pdf)
- **MPU6050 (Accelerometer + Gyroscope)** — 6-axis IMU for motion tracking. [Datasheet](https://invensense.tdk.com/wp-content/uploads/2015/02/MPU-6000-Datasheet1.pdf)
- **Hall Effect Sensor (A3144)** — Detects magnetic fields. Used for RPM sensing and proximity. [Datasheet](https://www.allegromicro.com/-/media/files/datasheets/a3144-datasheet.pdf)
- **Rotary Encoder (KY-040)** — Incremental optical encoder. Outputs quadrature signals. [Datasheet](https://components101.com/sensors/ky-040-rotary-encoder)
- **Vibration Sensor (SW-420)** — Detects vibration/shaking. Digital output. [Datasheet](https://components101.com/sensors/sw-420-vibration-sensor)
- **Tilt Sensor (SW-520D)** — Detects orientation/tilt. Simple mercury or ball switch. [Datasheet](https://components101.com/sensors/sw-520d-tilt-sensor)

### Light, Color & Proximity
- **Color Sensor (TCS3200)** — Detects RGB color using a photodiode array. [Datasheet](https://www.fairchildsemi.com/datasheets/TCS/TCS3200.pdf)
- **UV Index Sensor (VEML6075)** — Measures UV-A/UV-B radiation. I²C. [Datasheet](https://www.vishay.com/docs/84307/veml6075.pdf)
- **Ambient Light Sensor (BH1750)** — Measures light intensity in lux. I²C. [Datasheet](https://www.mouser.com/datasheet/2/348/bh1750fvi-e-186247.pdf)

### Gas & Air Quality
- **MQ-2** — Smoke, LPG, propane, CO. Analog output. [MQ-2 Datasheet](https://www.sparkfun.com/datasheets/Sensors/MQ-2.pdf)
- **MQ-135** — CO₂, NH₃, benzene, smoke (general air quality). [MQ-135 Datasheet](https://www.sparkfun.com/datasheets/Sensors/MQ-135.pdf)
- **MQ-137 (NH₃)** — Ammonia. Critical for poultry/pig barn air quality. [MQ-137 Datasheet](https://www.sparkfun.com/datasheets/Sensors/MQ-137.pdf)
- **MQ-4 (CH₄)** — Methane/biogas from manure lagoons and silage. [MQ-4 Datasheet](https://www.sparkfun.com/datasheets/Sensors/MQ-4.pdf)
- **MQ-3 (C₂H₅OH)** — Ethanol — fruit ripening gas for cold storage. [MQ-3 Datasheet](https://www.sparkfun.com/datasheets/Sensors/MQ-3.pdf)
- **CO₂ Sensor (SCD30 / MH-Z19B)** — NDIR CO₂. Greenhouse ventilation + livestock confinement safety. [MH-Z19B Datasheet](https://www.winsen-sensor.com/sensors/co2-sensor/mh-z19b.html)
- **Dust / PM2.5 (PMS5003 / PMS7003)** — Particulate matter from grain handling, feed mills. [PMS5003 Datasheet](https://www.seeedstudio.com/PMS5003-particle-sensor-module-p-3221.html)
- **Hydrogen Sulfide (H₂S)** — Toxic gas from manure. Safety-critical in confined animal buildings. [Winsen H₂S](https://www.winsen-sensor.com/)

### Radiation
- **Geiger Counter Module (SBM-20)** — Detects ionizing radiation. Pulse output proportional to count rate. [Datasheet](https://components101.com/sensors/geiger-counter-module)

### Touch & Force
- **Touch Sensor (TTP223)** — Capacitive touch detection. Active-high/low output. [Datasheet](https://components101.com/sensors/ttp223-touch-sensor)
- **Flex Sensor (SF150A)** — Resistance changes with bending. For gesture detection. [Datasheet](https://cdn-shop.adafruit.com/datasheets/FS150A.pdf)
- **Force Sensitive Resistor (FSR402)** — Resistance changes with pressure. For touch/weight sensing. [Datasheet](https://cdn-shop.adafruit.com/datasheets/FSR.pdf)
- **Load Cell + HX711** — Weight/force measurement. HX711 is 24-bit ADC for strain gauges. [HX711 Datasheet](https://www.dfrobot.com/wiki/index.php/HX711_Weight_Sensor_Kit_SKU_SEN0160)

### Current & Voltage
- **Current Sensor (ACS712)** — Hall-effect current sensor. 5A/20A/30A variants. [ACS712 Datasheet](https://www.allegromicro.com/-/media/files/datasheets/acs712-datasheet.pdf)

### Audio
- **Microphone (Electret)** — Converts sound to electrical signal. Used with op-amp for audio input. [Datasheet](https://www.digikey.com/en/products/filter/microphones/388)

### Water & Liquid
- **Water Level Sensor** — Analog output proportional to water depth. [Datasheet](https://components101.com/sensors/water-level-sensor)

## Electromechanical Components

### Switches
- **Switch (SPST, SPDT, DPDT)** — Makes or breaks a circuit connection. Toggle, slide, tactile, and push-button variants. [Datasheet](https://www.digikey.com/en/products/filter/toggle-switches/235)
- **Push Button (Tactile)** — Momentary contact switch. Common in keyboards and control panels. [Datasheet](https://www.digikey.com/en/products/filter/tactile-switches/236)
- **Reed Switch** — Magnetic proximity switch. Normally open, closes near magnet. [Datasheet](https://www.digikey.com/en/products/filter/reed-switches/215)
- **Micro Limit Switch** — Compact mechanical switch for position detection. [Datasheet](https://www.digikey.com/en/products/filter/basic-switches/194)

### Relays
- **Relay (Electromechanical)** — Electrically operated switch. Controls high-power loads with low-power signal. SRD-05VDC-SL-C is common. [Datasheet](https://www.songlerelay.com/upload/SRD.pdf)
- **Solid State Relay (SSR)** — No moving parts. Switches AC/DC via opto-isolation. [Datasheet](https://www.digikey.com/en/products/filter/solid-state-relays/236)

### Motors & Actuators
- **Motor (DC / Stepper / Servo)** — Converts electrical energy to motion. 28BYJ-48 (stepper), SG90 (servo) are common. [SG90 Datasheet](https://www.electronicoscaldas.com/datasheet/SG90_Servo.pdf)
- **Solenoid** — Electromagnetic actuator for linear motion. Used in locks and valves. [Datasheet](https://www.digikey.com/en/products/filter/solenoids-actuators/320)
- **Vibration Motor** — Eccentric rotating mass (ERM) motor. For haptic feedback. [Datasheet](https://www.digikey.com/en/products/filter/vibration-motors/973)
- **Gear Motor (N20)** — Small DC motor with gearbox. Low speed, high torque. [Datasheet](https://www.digikey.com/en/products/filter/dc-motors/174)

### Output Devices
- **Buzzer (Piezo / Magnetic)** — Generates sound tones. Piezo = high frequency, magnetic = low frequency. [Datasheet](https://www.digikey.com/en/products/filter/buzzers/148)
- **Cooling Fan** — DC brushless fan for thermal management. [Datasheet](https://www.digikey.com/en/products/filter/dc-brushless-fans/323)

## Power Components

### Batteries & Charging
- **Battery (AA, LiPo, Li-ion, CR2032)** — Portable DC power source. [Datasheet](https://www.digikey.com/en/products/filter/batteries-non-rechargeable-primary/101)
- **Battery Holder** — Mechanical holder for cells. [Datasheet](https://www.digikey.com/en/products/filter/battery-holders/390)
- **LiPo Charger Module (TP4056)** — 1A linear charger for single-cell LiPo. USB-powered. [TP4056 Datasheet](https://www.lcsc.com/datasheet/lcsc_datasheet_2304140030_TORCH-TP4056-1-USB-li-ion-battery-charging-module_C2731782.pdf)
- **BMS (Battery Management System)** — Protects LiPo from overcharge/overdischarge/short circuit. [Datasheet](https://components101.com/sensors/bms-battery-management-system)

### Power Supplies & Conversion
- **Power Jack (DC Barrel)** — Common 5.5mm × 2.1mm or 2.5mm barrel connector. [Datasheet](https://www.digikey.com/en/products/filter/barrel-power-connectors/409)
- **Power Supply Module (HLK-PM01)** — AC-DC converter module. 230V AC to 5V DC. [Datasheet](https://www.digikey.com/en/products/filter/ac-dc-converters/695)
- **Boost / Buck Converter Module (MT3608, LM2596)** — Steps voltage up (boost) or down (buck) efficiently. [MT3608 Datasheet](https://www.olimex.com/Products/Breadboarding/BB-PWR-3608/resources/MT3608.pdf)

### Protection
- **Fuse (Glass / Resettable PTC)** — Overcurrent protection. PTC resets automatically. [Datasheet](https://www.digikey.com/en/products/filter/ptc-resettable-fuses/244)
- **Voltage Supervisor (STM809)** — Resets MCU when supply drops below threshold. [Datasheet](https://www.st.com/resource/en/datasheet/stm809.pdf)

### Thermal Management
- **Heat Sink** — Dissipates heat from power components (TO-220, TO-92 packages). [Datasheet](https://www.digikey.com/en/products/filter/heat-sinks/306)

## Connectors & Interconnects

### Prototyping
- **Breadboard** — Solderless prototyping platform. Standard 830-point size. [Guide](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)
- **Jumper Wires (Male-to-Male / Male-to-Female)** — Interconnect breadboard and modules. [Guide](https://www.digikey.com/en/products/filter/jumper-wires/586)
- **Pin Headers (Male / Female)** — Standard 2.54mm pitch. Break-to-size strips. [Datasheet](https://www.digikey.com/en/products/filter/rectangular-connectors-headers-male-pins/306)
- **Dupont Connector** — Individual pin connector for breadboard jumper wires. [Datasheet](https://www.digikey.com/en/products/filter/headers-male-pins/306)

### Board-to-Board & Wire
- **Screw Terminal Block** — Securely connects wires to boards. [Datasheet](https://www.digikey.com/en/products/filter/terminal-blocks/298)
- **JST Connector** — Polarized connector for battery/speaker connections. 2/3/4 pin variants. [Datasheet](https://www.digikey.com/en/products/filter/wire-housings-plugs/319)
- **FFC/FPC Connector** — Flat flexible cable connector for displays and ribbon cables. [Datasheet](https://www.digikey.com/en/products/filter/ffc-fpc-connectors/321)

### Data & Network
- **USB Connector (Type-A, Micro, Type-C)** — Universal data and power interface. [Type-C Datasheet](https://www.usb.org/sites/default/files/USB%20Type-C%20Specification.pdf)
- **RJ45 / Ethernet Jack** — For wired networking (Ethernet). [Datasheet](https://www.digikey.com/en/products/filter/modular-connectors-jacks/410)
- **Audio Jack (3.5mm TRS)** — Stereo audio connector. [Datasheet](https://www.digikey.com/en/products/filter/audio-connectors/384)

### RF & Test
- **SMA Connector** — RF coaxial connector for antennas (Wi-Fi, GPS, LoRa). [Datasheet](https://www.digikey.com/en/products/filter/rf-connectors/389)
- **Banana Plug** — Test lead connector for multimeters and power supplies. [Datasheet](https://www.digikey.com/en/products/filter/test-connectors/752)
- **Alligator Clip** — Temporary spring-loaded test connection. [Datasheet](https://www.digikey.com/en/products/filter/test-probes-clips/753)

## Communication & Networking

### Wired Protocols
- **USB-UART Bridge (CH340G)** — USB to serial converter. Replaces FTDI FT232R. [CH340G Datasheet](https://www.wch-ic.com/downloads/CH340DS1_PDF.html)
- **RS485 Transceiver (MAX485)** — Differential communication for long-distance serial. [MAX485 Datasheet](https://www.ti.com/lit/ds/symlink/max485.pdf)
- **CAN Bus Transceiver (MCP2551)** — CAN bus interface for automotive/industrial. [MCP2551 Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/20001801C.pdf)
- **I²C Bus Extender (PCA9600)** — Extends I²C bus range and fan-out. [Datasheet](https://www.nxp.com/docs/en/data-sheet/PCA9600.pdf)
- **CAN Bus Module (MCP2515 + TJA1050)** — Industrial/automotive IoT communication. SPI-to-CAN interface. [Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP2515-Stand-Alone-CAN-Controller-with-SPI-20001801K.pdf)
- **RS485 to TTL Module (MAX3485)** — Long-distance (1200m) wired serial for industrial sensors. [Datasheet](https://www.ti.com/lit/ds/symlink/max3485.pdf)

### Short-Range Wireless
- **Bluetooth Module (HC-05 / HC-06)** — Serial-to-Bluetooth bridge. HC-05 = master/slave, HC-06 = slave-only. [HC-05 Datasheet](https://components101.com/sites/default/files/component_datasheet/HC-05%20Datasheet.pdf)
- **Wi-Fi Module (ESP8266 / ESP32)** — Adds Wi-Fi connectivity. ESP32 also has BLE. [ESP32 Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf)
- **NRF24L01+** — 2.4GHz short-range (10–100m) wireless. Ultra-cheap, SPI interface. [Datasheet](https://www.nordicsemi.com/Products/nRF24L01plus)
- **Zigbee Module (CC2530)** — Mesh networking for home automation. Low power. [Datasheet](https://www.ti.com/lit/ds/symlink/cc2530.pdf)
- **ESP-NOW** — Peer-to-peer protocol on ESP32/ESP8266. No router needed. Sub-millisecond latency. [Docs](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/networks/esp_now.html)
- **Matter/Thread Module (EFR32)** — New unified smart home standard. Mesh networking via Thread. [Docs](https://csa-iot.org/all-solutions/matter/)

### Long-Range & Cellular
- **LoRa Module (SX1276 / RFM95W)** — Long-range (2–15km), low-power radio. Ideal for rural/agricultural IoT. [SX1276 Datasheet](https://www.semtech.com/uploads/documents/DS_SX1276-7-8-9_WAPP174.pdf)
- **LoRaWAN Gateway Module (SX1301)** — Multi-channel LoRa concentrator. Receives from thousands of nodes. [Datasheet](https://wwwsemtech.com/uploads/documents/DS_SX1301.pdf)
- **LoRa Development Board (TTGO LoRa32)** — ESP32 + LoRa + OLED on one board. Fast prototyping. [Docs](https://github.com/LilyGO/TTGO-LoRa-Series)
- **GSM/GPRS Module (SIM800L)** — Cellular connectivity for remote IoT. SMS/data. [Datasheet](https://www.simcom.io/product/SIM800L)
- **NB-IoT Module (BC95)** — Narrowband IoT for deep indoor coverage. Ultra-low power. [Datasheet](https://www.quectel.com/product/lte-bc95)

### Positioning
- **GPS Module (NEO-6M / NEO-8M)** — Provides position and time data via UART. [NEO-6M Datasheet](https://www.u-blox.com/sites/default/files/products/documents/NEO-6_DataSheet_(GPS.G6-HW-09005).pdf)
- **GPS/GNSS Module (BN-220)** — Compact GPS with antenna. For asset tracking. [Datasheet](https://www.u-blox.com/sites/default/files/products/documents/NEO-6_DataSheet_(GPS.G6-HW-09005).pdf)

### Data & Audio Modules
- **SD Card Module** — SPI interface for SD/SDHC storage. [Datasheet](https://components101.com/sensors/sd-card-module)
- **DFPlayer Mini** — MP3 audio player module with serial control. [Datasheet](https://components101.com/sensors/dfplayer-mini-mp3-player)

## Timing, Memory & Interface ICs

### Clocks & Oscillators
- **Crystal Oscillator** — Provides precise clock frequency (e.g., 16 MHz for Arduino). [Datasheet](https://www.digikey.com/en/products/filter/crystals/172)
- **Crystal Resonator (Ceramic)** — Lower precision than crystal but cheaper. Used in simple timing circuits. [Datasheet](https://www.digikey.com/en/products/filter/resonators/173)

### Non-Volatile Memory
- **EEPROM (AT24Cxx)** — Non-volatile memory over I²C. Stores configuration data. [AT24C256 Datasheet](https://www.microchip.com/en-us/product/AT24C256)
- **SPI Flash (W25Qxx)** — Non-volatile memory over SPI. For firmware/data storage. [W25Q128 Datasheet](https://www.winbond.com/hq/product/code-storage-flash-memory/serial-nor-flash/?__locale=en&partNo=W25Q128JV)

### Real-Time Clocks
- **RTC Module (DS3231 / DS1307)** — Real-time clock with battery backup. [DS3231 Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/DS3231.pdf)

### Solar & Energy
- **Solar Charge Controller (CN3791)** — MPPT solar charger for LiPo/Li-ion. For remote IoT nodes. [Datasheet](https://www.consonance-e.com/datasheet/CN3791.pdf)
- **Energy Harvesting Module (BQ25570)** — Ultra-low power energy harvester. Solar/thermal/RF. For perpetual IoT nodes. [Datasheet](https://www.ti.com/lit/ds/symlink/bq25570.pdf)

---

# Domain Applications

## IoT — Protocols & Platforms

Software, protocols, and cloud platforms that make IoT projects work. Pair these with the radio modules in [Communication & Networking](#communication--networking).

### Communication Protocols (software layer)
- **MQTT** — Lightweight pub/sub protocol over TCP. The de-facto IoT standard. Broker + topics + QoS levels. [Spec](https://mqtt.org/)
- **CoAP** — Constrained Application Protocol. UDP-based, RESTful. For ultra-low-power sensor nodes. [RFC 7252](https://datatracker.ietf.org/doc/html/rfc7252)
- **HTTP / REST** — Simple request/response. Easy but heavier; fine for infrequent updates. [MDN Guide](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- **WebSocket** — Full-duplex real-time channel. Good for live dashboards. [Docs](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)
- **LoRaWAN** — Network layer for LoRa radios. Handles activation, encryption, adaptive data rate (ADR). [Spec](https://lora-alliance.org/lorawan-for-developers/)
- **NB-IoT / LTE-M** — Cellular LPWAN standards. Deep indoor coverage, licensed spectrum. [GSMA Guide](https://www.gsma.com/iot/mobile-iot/)
- **Z-Wave** — Sub-GHz mesh for smart homes. More reliable than 2.4GHz Wi-Fi/Zigbee. [Docs](https://www.z-wave.com/)
- **Matter** — Unified IP-based smart-home standard (Thread + Wi-Fi). Replaces vendor silos. [Docs](https://csa-iot.org/all-solutions/matter/)
- **OPC UA** — Industrial M2M protocol. Secure, extensible. For factory/SCADA. [Docs](https://opcfoundation.org/)
- **ESP-NOW** — Espressif peer-to-peer (no router). Already in [Short-Range Wireless](#short-range-wireless).
- **OTA Updates** — Over-The-Air firmware flashing (ArduinoOTA, ESP-IDF). Critical for field nodes. [ESP-IDF Docs](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/system/ota.html)
- **TLS / DTLS** — Encryption for MQTT/CoAP. Use certificates, not just passwords. [Learn TLS](https://tls13.ulfheim.net/)

### Cloud & Device Platforms
- **The Things Network (TTN)** — Free public LoRaWAN network + console. Perfect for farm-scale LoRa nodes. [Docs](https://www.thethingsnetwork.org/)
- **AWS IoT Core** — Managed MQTT broker + device shadows + rules engine. Scales to millions. [Docs](https://aws.amazon.com/iot-core/)
- **Azure IoT Hub** — Bi-directional cloud messaging + device twins + provisioning. [Docs](https://learn.microsoft.com/en-us/azure/iot-hub/)
- **Arduino Cloud** — Zero-config dashboards for Arduino/ESP32. Beginner-friendly. [Docs](https://create.arduino.cc/cloud/dashboard)
- **Blynk** — Mobile app platform for IoT device control. Drag-and-drop dashboard. [Docs](https://docs.blynk.io/)
- **Ubidots** — IoT app-enablement platform. Great charts + alerts out of the box. [Docs](https://help.ubidots.com/)
- **Losant** — Enterprise IoT app builder. Workflow engine + dashboards. [Docs](https://docs.losant.com/)
- **Kaa IoT** — Open-source IoT platform. Device management + data viz. [Docs](https://www.kaaiot.com/)
- **ThingSpeak** — Free IoT cloud for logging sensor data + MATLAB analysis. [Docs](https://thingspeak.com/)
- **ThingsBoard** — Open-source IoT platform for device management and data visualization. [Docs](https://thingsboard.io/)
- **Hologram / Things Mobile** — Cellular SIM + data platform for NB-IoT/LTE-M devices. [Hologram](https://hologram.io/)

### Time-Series & Visualization
- **InfluxDB** — Purpose-built time-series database. Stores sensor readings efficiently. [Docs](https://www.influxdata.com/)
- **Grafana** — Dashboard + alerting on top of InfluxDB / Prometheus. [Docs](https://grafana.com/)
- **Node-RED** — Flow-based programming for IoT. Wires together APIs, devices, services. [Docs](https://nodered.org/)
- **Home Assistant** — Open-source home automation hub. Integrates Zigbee, Z-Wave, Wi-Fi, MQTT. [Docs](https://www.home-assistant.io/)

### Edge & Gateway Software
- **Mosquitto** — Lightweight MQTT broker. Runs on Pi/ESP32. [Docs](https://mosquitto.org/)
- **Zigbee2MQTT** — Bridges Zigbee devices to MQTT via a CC2531/SONOFF dongle. [Docs](https://www.zigbee2mqtt.io/)
- **ESPHome** — YAML-configured ESP32/ESP8266 firmware. Integrates with Home Assistant. [Docs](https://esphome.io/)
- **Tasmota** — Open firmware for ESP-based smart plugs/switches/sensors. [Docs](https://tasmota.github.io/docs/)
- **OpenHAB** — Vendor-neutral home automation. Runs on Pi/NAS. [Docs](https://www.openhab.org/)

### IoT Reference Architecture (starter pattern)
```
[Sensor Node: ESP32 + Sensors]  --LoRa/WiFi/NB-IoT-->  [Gateway: Pi + Mosquitto]
        |                                                        |
        +-- publishes MQTT topic `farm/field1/moisture` --+--> [TTN / AWS IoT Core]
                                                          +--> [InfluxDB + Grafana dashboard]
                                                          +--> [Node-RED rule: if moisture<30% -> open valve]
```
Rule of thumb: **sensor node = dumb + low power**, **gateway = smart + always-on**. Keep the radio duty-cycle low (send every 10–60 min) to extend battery life for months.

## Agricultural & Environmental Sensors

Sensors for farming, irrigation, weather, and environmental science. Generic sensors (temperature, pressure, light, gas) are cataloged once in [Sensors & Transducers](#sensors--transducers); this section highlights agriculture-specific parts and how to combine them.

### Soil Sensors
- **Soil Moisture Sensor (Capacitive v2.0)** — Measures soil water content. Corrosion-resistant. [Datasheet](https://www.dfrobot.com/wiki/index.php/Capacitive_Soil_Moisture_Sensor_SKU_SEN0193)
- **Soil Moisture Sensor (Resistive)** — Cheaper but corrodes over time. Good for prototyping only. [Datasheet](https://components101.com/sensors/soil-moisture-sensor)
- **Capacitive vs Resistive (which to pick)** — Capacitive (v2.0) = no exposed metal, no corrosion, lasts years. Resistive = bare copper, corrodes in weeks. Always choose capacitive for real deployments.
- **Soil Temperature Probe (DS18B20 Waterproof)** — Stainless steel probe for buried temperature sensing. [Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/DS18B20.pdf)
- **Soil EC (Electrical Conductivity) Sensor** — Measures soil salinity/nutrient level. [Datasheet](https://www.dfrobot.com/wiki/index.php/Gravity:_Analog_Electrical_Conductivity_Sensor_(K=1)_SKU_SEN0244)
- **Soil pH Sensor (EN-1602)** — Measures soil acidity/alkalinity. Critical for crop health. [Datasheet](https://www.dfrobot.com/wiki/index.php/Gravity:_Analog_pH_Sensor_Meter_Kit_V2_SKU_SEN0161)
- **NPK Sensor (RS485)** — Measures Nitrogen, Phosphorus, Potassium. Industrial RS485 interface. [Datasheet](https://www.alibaba.com/product-detail/NPK-Soil-Sensor-RS485-Nitrogen-Phosphorus-Potassium_1600993548.html)

### Soil — Advanced & Water Potential
- **Soil Water Potential (Tensiometer / Watermark 200)** — Measures how hard roots must work to extract water (kPa), not just % moisture. The metric agronomists actually use for irrigation scheduling. [Watermark Datasheet](https://www.irrometer.com/pdf/watermark.pdf)
- **TDR Soil Moisture (TEROS-12)** — Time-Domain Reflectometry. Lab-grade accuracy, ±1%. Better than capacitive for research. [Datasheet](https://www.metergroup.com/en/agriculture/products/teros-12/)
- **FDR Soil Moisture** — Frequency-Domain Reflectometry. Cheaper than TDR, good field accuracy. [Guide](https://www.dfrobot.com/wiki/index.php/Capacitive_Soil_Moisture_Sensor_SKU_SEN0193)
- **Gypsum Block Sensor** — Cheap buried sensor; resistance changes with moisture. No corrosion, lasts a season. [Guide](https://extension.umn.edu/irrigation/soil-moisture-sensors)

### Weather & Climate Sensors
- **BME280** — Temperature + humidity + barometric pressure. I²C/SPI. [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf)
- **BME680** — BME280 + gas sensing (VOC). Indoor air quality. [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf)
- **DHT22 (AM2302)** — Temperature + humidity. Digital output. [Datasheet](https://www.mouser.com/datasheet/2/758/DHT11-Technical-Data-Sheet-Translated-Version-1143054.pdf)
- **Anemometer (Wind Speed Sensor)** — Measures wind speed. Pulse or analog output. [Datasheet](https://www.dfrobot.com/wiki/index.php/Wind_Speed_Sensor_SKU_SEN0174)
- **Wind Vane (Direction Sensor)** — Measures wind direction. Analog voltage output. [Datasheet](https://www.dfrobot.com/wiki/index.php/Wind_Vane_SKU_SEN0226)
- **Rain Gauge (Tipping Bucket)** — Measures rainfall in mm. Pulse output per 0.2mm. [Datasheet](https://www.dfrobot.com/wiki/index.php/Rain_Speed_Sensor_SKU_SEN0175)
- **Solar Radiation Sensor (pyranometer)** — Measures total solar irradiance (W/m²). For solar panel efficiency. [Datasheet](https://www.dfrobot.com/wiki/index.php/Solar_Radiation_Sensor_SKU_SEN0213)
- *UV and ambient light sensors (VEML6075, BH1750) are listed in [Light, Color & Proximity](#light-color--proximity).*

### Atmospheric & Microclimate
- **Lightning Sensor (AS3935)** — Detects lightning within 40km. Storm warning for field crews. [AS3935 Datasheet](https://www.ams.com/as3935)
- **Barometric Pressure (BMP280 / BME280)** — Falling pressure = incoming storms. Weather forecasting. [BMP280 Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bmp280-ds001.pdf)
- **Dew Point / Leaf Wetness** — See [Greenhouse & Precision Farming](#greenhouse--precision-farming). Combines with humidity for disease models.
- **Snow Depth (Ultrasonic JSN-SR04T)** — Tank-level sensor repurposed for snow pack. [Guide](https://www.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)
- **Solar Charge for Nodes (CN3791 + Panel)** — Powers remote sensors perpetually. See [Solar & Energy](#solar--energy).

### Water & Irrigation Sensors
- **Water Flow Sensor (YF-S201)** — Hall-effect flow meter. 1–30 L/min. [Datasheet](https://www.dfrobot.com/wiki/index.php/Water_Flow_Sensor_SKU_SEN0141)
- **Water Level Sensor (Ultrasonic JSN-SR04T)** — Waterproof ultrasonic for tank level. [Datasheet](https://www.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)
- **pH Sensor (EN-1602)** — Measures water pH (0–14). For hydroponics and aquaculture. [Datasheet](https://www.dfrobot.com/wiki/index.php/Gravity:_Analog_pH_Sensor_Meter_Kit_V2_SKU_SEN0161)
- **TDS Sensor (Total Dissolved Solids)** — Measures water purity/conductivity. [Datasheet](https://www.dfrobot.com/wiki/index.php/Gravity:_Analog_TDS_Sensor_Meter_SKU_SEN0244)
- **Dissolved Oxygen Sensor (SEN0237)** — Measures O₂ in water. For aquaculture/fish farming. [Datasheet](https://www.dfrobot.com/wiki/index.php/Gravity:_Analog_Dissolved_Oxygen_Sensor_SKU_SEN0237)
- **Water Turbidity Sensor (SEN0189)** — Measures water clarity. For irrigation quality. [Datasheet](https://www.dfrobot.com/wiki/index.php/Turbidity_Sensor_SKU_SEN0189)
- **Float Switch** — Liquid level detection. Simple on/off at threshold. [Datasheet](https://www.digikey.com/en/products/filter/float-switches/325)

### Greenhouse & Precision Farming
- **CO₂ Sensor (SCD30)** — NDIR CO₂ measurement. I²C. For greenhouse ventilation control. [Datasheet](https://www.sensirion.com/en/environmental-sensors/carbon-dioxide-sensors-cd)
- **PAR / Light Sensor** — Photosynthetically Active Radiation (400–700nm) drives plant growth. Use a [pyranometer](#weather--climate-sensors) or [ambient light sensor](#light-color--proximity); true PAR meters report µmol/m²/s.
- **Leaf Wetness Sensor** — Detects water on leaf surface. For disease prediction. [Datasheet](https://www.dfrobot.com/wiki/index.php/Leaf_Wetness_Sensor_SKU_SEN0522)
- **Stem Diameter Sensor (DYMH-103)** — Measures plant stem growth/dendrometer. [Datasheet](https://www.dfrobot.com/wiki/index.php/Strain_Gauge_Sensor_SKU_SEN0152)
- **NDVI Sensor (Red + NIR)** — Normalized Difference Vegetation Index. For crop health monitoring. [Docs](https://www.farmhack.org/tools/near-infrared-camera)
- **Servo + Solenoid Valve** — Automated irrigation control. 12V solenoid for water flow. [Datasheet](https://www.digikey.com/en/products/filter/solenoid-valves/460)

### Livestock Monitoring
- **RFID Ear Tag Reader (RDM6300 / EM4100)** — 125kHz RFID. Identifies individual animals at feeders/gates. [RDM6300 Datasheet](https://www.dfrobot.com/wiki/index.php/RFID_Reader_Module_SKU_DFR0032)
- **Animal GPS Tracker (GT06 / TK103)** — GPS + GSM collar/ear-tag. Geofencing + theft recovery. [Guide](https://www.traccar.org/)
- **Body Temperature Tag (BLE)** — Ingestible or ear-attached bluetooth tag. Early illness detection. [Guide](https://www.cainthus.com/)
- **Milk Yield Meter** — Flow meter on milking machine. Herd productivity. [Guide](https://www.delaval.com/)
- **Accelerometer (ADXL345)** — Ruminant activity/estrus/lame detection. Already in IMU modules. [ADXL345 Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/ADXL345.pdf)
- **Bird/Drone Deterrent (PIR + Ultrasonic)** — Protects crops from wildlife. [Guide](https://www.birdcontrolgroup.com/)
- *Barn air quality (NH₃, CH₄, CO₂, H₂S, dust) — see the consolidated [Gas & Air Quality](#gas--air-quality) list in Sensors & Transducers. NH₃ (MQ-137) and H₂S are safety-critical in confined animal buildings.*

### Crop Health & Imaging
- **Multispectral Camera (M5Stack Unit CAM / NDVI)** — Captures NIR + visible for vegetation index maps. Drone-mounted field scouting. [Docs](https://docs.m5stack.com/)
- **Thermal Camera (MLX90640)** — 32×24 IR array. Detects irrigation stress (hot leaves) and disease early. [MLX90640 Datasheet](https://www.melexis.com/en/documents/datasheet/mlx90640)
- **Sap Flow Sensor (heat-ratio)** — Measures water use by individual plants/trees. Research-grade. [Guide](https://www.dynamax.com/p-41-transpiration.aspx)
- **Chlorophyll Meter (SPAD / TCS3200 color)** — Leaf greenness ≈ nitrogen status. [Guide](https://www.konicaminolta.com/instruments/measure/spad/)
- **Fruit Ripeness (TCS34725 color)** — RGB color sensor for harvest timing / sorting. [TCS34725 Datasheet](https://www.adafruit.com/product/1334)

### Smart Irrigation Controllers
- **OpenSprinkler** — Open-source WiFi sprinkler controller (up to 8 zones). [Docs](https://opensprinkler.com/)
- **RainMachine** — Weather-aware irrigation (skips watering when it will rain). [Docs](https://rainmachine.com/)
- **Solenoid Valve Driver (12V / 24V AC)** — Controls mains-water valves from a relay/MOSFET. [Guide](https://www.digikey.com/en/products/filter/solenoid-valves/460)
- **Soil-Moisture-Based Controller** — ESP32 + capacitive sensor + solenoid = closed-loop irrigation. No timer needed. [Guide](https://www.instructables.com/Arduino-Automatic-Watering-System/)

### IoT Agriculture Platforms
- **Arduino + LoRa** — Low-cost sensor nodes for large farms. [Docs](https://www.arduino.cc/en/Tutorial/LoRa)
- **Raspberry Pi Gateway** — Aggregates sensor data, runs MQTT broker, serves dashboards. [Docs](https://www.raspberrypi.org/)
- **ThingsBoard** — Open-source IoT platform for device management and data visualization. [Docs](https://thingsboard.io/)
- **Farmbeats (Microsoft)** — End-to-end IoT solution for agriculture. [Docs](https://github.com/farmbeatsproject/FarmBeats-Student-Edition)
- **CropX** — Commercial soil sensor + analytics platform. [Docs](https://www.cropx.com/)
- **Libelium Waspmote** — Industrial IoT sensor node. Plug-and-play agriculture sensors. [Docs](https://www.libelium.com/products/waspmote/)
- **OpenAg (MIT Media Lab)** — Open-source food growing systems. [Docs](https://www.media.mit.edu/groups/open-ag/)

---

## Contributing

Have a component to add? Open a PR or issue. Keep entries beginner-friendly and link to reputable datasheets or guides.

## License

[MIT](LICENSE)
