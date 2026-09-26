# Autonomous Horseradish Weeding Robot

**Role:** Undergraduate Research Assistant (Electrical Engineer)
**Lab:** Digital Precision Agriculture Lab, Agricultural and Biological Engineering Department, University of Illinois at Urbana-Champaign

---

## Project Overview

This project was initiated to reduce the intense manual labor requirements for horseradish farmers in central and southern Illinois. Due to EPA food safety regulations and the unavailability of herbicide-resistant horseradish varieties, farmers cannot rely on broadcast chemical applications. The alternative — walking fields to manually weed — is extremely labor-intensive, costly, and often incomplete. Our goal is to automate this process to reduce labor demands and improve overall weed removal efficiency.

---

## Platform & System Architecture

The foundation of our system is the all-electric **Farm-ng Amiga** micro-tractor. This modular robotics platform is ideal for our application because its clearance and adjustable track width allow it to straddle horseradish crops without crushing the plants. The robot utilizes computer vision to differentiate between crops and weeds, dynamically aiming our onboard intervention systems.

Originally, the lab explored a mechanical weeding approach using a hoe attached to a pneumatic cylinder. While somewhat effective for weeding between crop rows, it was ineffective between individual plants. This limitation drove our transition to a dual-pronged, highly precise approach:

**Spot Sprayer**
Targets weeds located between rows. It delivers a contained chemical dose directly to the weed without saturating the surrounding soil or contacting the horseradish plant.

**Targeted Laser System**
Eliminates weeds growing directly between the horseradish plants where chemicals and mechanical hoes cannot safely operate.

---

## My Contributions

As the sole Electrical Engineer on the project, I serve as the lab's resident EE consultant, advising on the electrical components of the spot sprayer and leading the development of the hardware and firmware for the laser system.

### Custom Hardware & PCB Design

**Peripheral Integration**
Designed and routed a custom PCB (see included KiCad files) to serve as the central interface connecting the robot's peripheral hardware and motor drivers to the main processing computer.

**System Documentation**
Drafted and formalized the complete electrical schematic for the entire laser system to ensure proper power management and future maintainability.

### Firmware & Motor Control (C++ & TMC2209)

**Sensorless Homing**
Currently developing a robust C++ control loop utilizing UART communication with a TMC2209 stepper motor driver. This script monitors motor load to achieve sensorless homing, accurately detecting when the laser mount reaches the physical limits of its linear track.

**Positional Tracking**
By recording the stepper motor's state when it contacts the rail edge, the script calibrates absolute positional data. This data is fed back into the aiming program so the computer vision algorithm can accurately target the laser.

### Mechanical Integration & Future Enhancements

**Hardware Mounting**
Collaborated on mechanical design decisions for the laser mounting system to ensure proper electrical routing and reliable sensor integration.

**Dynamic Targeting — Rotational Degree of Freedom**
Currently working alongside mechanical team members to add a rotational degree of freedom to the laser mount using a servo motor. Combined with the stepper motor, this will allow the system to continuously track a targeted weed while the Amiga platform remains in motion, significantly improving the robot's field speed and operational efficiency.

---

## Repository Contents

| Folder | Contents |
|--------|----------|
| `kicad/` | Interface board schematic and PCB layout |
| `python/` | Computer vision and servo tracking code |
| `docs/` | Electrical schematics and wiring diagrams |