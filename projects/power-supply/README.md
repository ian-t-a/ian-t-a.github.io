## Project Overview

I designed and built a dual-output bench power supply with adjustable +10V and -10V outputs at up to 3A per rail. The goal was to build a supply useful for electronics prototyping while including the protection, monitoring, and thermal management needed for higher-current operation.

Both rails have independent voltage adjustment, current limiting, voltage monitoring, and current monitoring. The design also includes reverse-polarity protection, overvoltage protection, and thermal management.

Link to view board and schematic on the web: [Power Supply](https://kicanvas.org/?repo=https%3A%2F%2Fgithub.com%2Fian-t-a%2Fian-t-a.github.io%2Ftree%2Fmain%2Fprojects%2Fpower-supply%2Fkicad)

---

## Design Requirements

| Requirement | Target |
|-------------|--------|
| Positive output | 0 to +10V |
| Negative output | 0 to -10V |
| Output current | 3A per rail |
| Input | 13.7V, 40A |
| Voltage monitoring | Both rails |
| Current monitoring | Both rails |
| Protection | Reverse polarity, overcurrent, overvoltage |
| Cooling | Forced-air cooling |
| PCB | 4-layer, 2oz outer copper |

---

## Input Protection

The input stage protects the supply from wiring mistakes and voltage transients using three main components:

- **15A fuse** for primary overcurrent protection
- **SMAJ15A TVS diode** to clamp voltage transients
- **SI4403DDY P-channel MOSFET** to block reverse polarity

If the input is connected backwards, the MOSFET prevents the reverse voltage from reaching the rest of the circuit.

---

## Positive Rail

The positive rail uses **LT3083** linear regulators. The LT3083 uses a current-source-based voltage reference rather than a traditional feedback divider, which makes allows voltage regulation down to 0V.

---

## Negative Rail

The negative rail uses two stages.

**LM2596 Inverting Converter**
Generates approximately -11V from the +13.7V input to provide headroom for the negative regulator stage.

**LT3091 Output Stage**
Two LT3091 regulators in parallel produce the final negative output. The LT3091 was chosen for its programmable current limiting and current monitoring. Each regulator has a small 10mΩ impedance-matched trace to help with current sharing.

---

## Current & Voltage Monitoring

A 7.5mΩ shunt resistor measures current on each rail. Each rail has its own DSN-VC288 dual 7-segment meter showing output voltage and current in real time.

The meters use isolated power converters so the negative rail can be measured without creating unwanted ground loops.

---

## Thermal Management

The linear regulators can dissipate significant power at high current, so thermal management was a big part of the design. The regulators are spread across the board to improve airflow rather than concentrating all the heat in one spot. They are all placed with a future case and air cooling system in mind. In the future I plan on making 3D printed case with mounts for fans for active cooling. So the components are placed in a way to maximize air flow across the heat sinks and other compenents.

- **LT3083 pair:** Near the fan intake
- **LT3091 pair:** Downstream of the positive rail heatsinks
- **LM2596:** On a large copper pour with stitching vias

---

## PCB Design

The board uses a 4-layer stackup with 2oz outer copper.

| Layer | Purpose |
|-------|---------|
| Layer 1 | Signals and power traces |
| Layer 2 | Ground plane |
| Layer 3 | Ground plane |
| Layer 4 | Signals and return paths |

The dedicated ground planes keep the switching converter's noise away from the more sensitive analog circuits. The LM2596 is placed away from the analog circuitry, and stitching vias are used across the board to improve heat dissipation and reduce EMI.

---

## Lessons Learned

- **Paralleling regulators** using a current-source architecture is much simpler than paralleling traditional feedback-divider types
- **Isolated meter supplies** are necessary when measuring a rail referenced below ground
- **Thermal design has to start early** — regulator placement and airflow path matter as much as the electrical design
- **4-layer PCBs make a real difference** in power electronics by providing clean ground planes and separating noisy switching circuits from analog ones

---

## Project Takeaway

This project gave me end-to-end experience designing a power system, including regulator architecture, protection circuits, current sensing, thermal management, and PCB layout. It was a good exercise in balancing electrical performance with practical constraints like heat, noise, and component placement.
