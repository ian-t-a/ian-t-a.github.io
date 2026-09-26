# DIY Adjustable ±10V / 3A Bench Power Supply

[View the KiCad Project](https://kicanvas.org/?repo=https%3A%2F%2Fgithub.com%2Fian-t-a%2Fian-t-a.github.io%2Ftree%2Fmain%2Fprojects%2Fpower-supply%2Fkicad)

---

## Project Overview

I designed and built a **dual-output bench power supply** capable of producing adjustable **+10V and -10V outputs at up to 3A per rail**.

The goal was to build a supply that was useful for electronics prototyping while also including the protection, monitoring, and thermal management needed for higher-current operation.

Both rails have independent:

* Voltage adjustment

* Current limiting

* Voltage monitoring

* Current monitoring

The design also includes reverse-polarity protection, overvoltage protection, short-circuit protection, and thermal management.

---

## Design Requirements

The main design targets were:

| Requirement        | Target                                     |
| ------------------ | ------------------------------------------ |
| Positive output    | 0 to +10V                                  |
| Negative output    | 0 to -10V                                  |
| Output current     | 3A per rail                                |
| Input              | 13.7V, 40A                                 |
| Voltage monitoring | Both rails                                 |
| Current monitoring | Both rails                                 |
| Protection         | Reverse polarity, overcurrent, overvoltage |
| Cooling            | Forced-air cooling                         |
| PCB                | 4-layer, 2oz outer copper                  |

---

# Input Protection

The input stage is designed to protect the rest of the supply from common wiring mistakes and voltage transients.

### Reverse-Polarity Protection

The input protection circuit uses three main components:

* **15A fuse** for primary overcurrent protection

* **SMAJ15A TVS diode** to clamp voltage transients

* **SI4403DDY P-channel MOSFET** to block reverse polarity

The MOSFET is combined with an **8.2V Zener clamp** and a **10kΩ pull-down resistor** to keep the gate-to-source voltage within a safe range.

This means that if the input supply is accidentally connected backwards, the MOSFET prevents the reverse voltage from reaching the rest of the circuit.

---

# Positive 10V Rail

The positive rail uses **LT3083 linear regulators**.

The LT3083 was a good fit for this design because it uses a current-source-based voltage reference rather than a traditional feedback divider.

### Key Features

* 3A-capable linear regulator

* Programmable output voltage

* Integrated current limiting

---

# Negative 10V Rail

The negative rail uses two stages.

### LM2596 Inverting Converter

The LM2596S-ADJ is used to generate approximately **-11V** from the +13.7V input.

This provides enough headroom for the negative linear regulators.

The converter uses:

* 100µH output inductor

* SS34 Schottky diode

* 1nF C0G feedforward capacitor

* 8.87kΩ / 1kΩ feedback network

* 68µF and 47µF filtering capacitors

### LT3091 Output Stage

Two **LT3091 regulators** are connected in parallel to produce the final negative output.

The LT3091 was selected because it includes programmable current limiting and current monitoring.

Each regulator has a small **10mΩ impedance matched trace** to help with current sharing.

---

# Current Limiting & Monitoring

Both rails use dedicated current sensing circuits.

### Current Sensing

A **7.5mΩ shunt resistor** measures the current flowing through each rail. This is done by use of the proprietary voltage and current sensors.

---

# Voltage & Current Display

Each output rail has its own **DSN-VC288 dual 7-segment meter**.

Each meter displays:

* Output voltage

* Output current

The meters use:

* Red display for voltage

* Blue display for current

The meters are configured for the supply's 0–10V and 0–3A operating range.

### Isolated Meter Power

The positive and negative meters use isolated power converters so that the negative rail can be measured without creating unwanted ground-reference connections.

The negative meter is especially dependent on this isolation because its measurement is referenced to a voltage below system ground.

---

# Protection & Safety

Several layers of protection are included throughout the design.

### Reverse Polarity

The P-channel MOSFET blocks current when the input is connected backwards.

### Input Overvoltage

The SMAJ15A TVS diode clamps high-voltage transients, while the input fuse provides additional protection.

### Thermal Protection

The LT3083 and LT3091 devices have built-in thermal shutdown. Heatsinks and forced-air cooling are used to keep the devices well below their thermal limits during normal operation.

# Thermal Management

Thermal management was a major part of the design because the linear regulators can dissipate significant power at high current.

Instead of putting all of the heatsinks in one location, the regulators are distributed across the enclosure to improve airflow.

### Heatsink Layout

* **LT3083 pair:** Mounted near the main fan intake

* **LT3091 pair:** Mounted downstream of the positive rail heatsinks

* **LM2596:** Mounted in large copper pour with lots of stitching vias for improved heat dissipation

Air enters through the front of the enclosure, passes over the main regulator heatsinks, and exits through the rear exhaust fans.

### Worst-Case Dissipation

At 3A output with a 10V output voltage:

```text
(13.7V - 10V) × 3A = 11.1W
```

This results in significant heat that must be removed by the heatsinks and fans.

The selected heatsinks are rated around **1°C/W**, with the goal of keeping regulator junction temperatures below approximately 80°C during normal operation.

---

# PCB Design

The power supply uses a **4-layer PCB with 2oz outer copper**.

### Layer Stackup

| Layer   | Purpose                  |
| ------- | ------------------------ |
| Layer 1 | Signals and power traces |
| Layer 2 | Ground plane             |
| Layer 3 | Ground plane             |
| Layer 4 | Signals and return paths |

The 4-layer design helps with both power distribution and noise management.

The inner planes provide low-impedance power and ground paths while helping keep the switching converter's high-frequency noise away from the more sensitive analog circuits.

### Component Placement

The PCB layout was organized around both electrical and thermal considerations.

Key placement decisions included:

* Input protection and main fuse placed near the input connector

* LM2596 switching converter separated from sensitive analog circuitry

* Current-sense circuitry kept away from noisy switching sections

* Heatsink clearance included in the PCB layout

* Thermal vias used around larger thermal pads

* Signal and ground planes arranged to reduce noise coupling

* Large amounts of stitching vias used across the board to improve heat dissipation and reduce EMI.

---

# Lessons Learned

### Paralleling Linear Regulators

One of the most interesting parts of the design was learning how regulators such as the LT3091 can be paralleled using their current-source-based architecture.

This made current sharing much simpler than it would be with traditional feedback-divider regulators.

### Isolation Matters

The isolated supply for the negative voltage meter was important for avoiding ground-reference problems when measuring a rail below ground.

### Thermal Design Has to Start Early

Thermal management affected the enclosure, PCB layout, and component placement from the beginning. The regulator placement and airflow path ended up being just as important as the electrical design.

### PCB Layout Matters in Power Electronics

Using a 4-layer PCB allowed the design to have dedicated ground and power planes, which helped separate the switching converter from the lower-noise analog circuitry.

### Dedicated Current-Sense ICs

Using the INA199 made the current-sensing portion of the design simpler and cleaner than building the same function from a discrete op-amp circuit.

---

## Project Takeaway

This project gave me experience designing a power system from the ground up, including the **regulator architecture, protection circuits, current sensing, thermal management, and PCB layout.

It was also a good exercise in balancing electrical performance with practical design constraints such as heat, noise, component placement, and usability.
