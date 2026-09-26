# Autonomous Horseradish Weeding Robot

**Role:** Undergraduate Research Assistant (Electrical Engineer)
**Lab:** Digital Precision Agriculture Lab, Agricultural and Biological Engineering Department, University of Illinois at Urbana-Champaign

---

## Project Overview

This project was started to reduce the manual labor load for horseradish farmers in central and southern Illinois. Due to EPA food safety regulations and the unavailability of herbicide-resistant horseradish varieties, farmers cannot rely on broadcast chemical spraying. The alternative whihch is walking fields to manually weed is extremely labor-intensive, costly, and somtimes inmplete. Our goal is to automate this process to reduce labor load and improve overall weed removal efficiency.

---

## Platform & System Architecture

The foundation of our system is the all-electric **Farm-ng Amiga** micro-tractor. This modular robotics platform is great for our use because its clearance and adjustable track width allow it to straddle horseradish crops without harming the plants. The robot uses computer vision to differentiate between crops and weeds, and uses this data to aim our weed removal systems.

Originally, the lab explored a mechanical weeding approach using a hoe attached to a pneumatic cylinder. While this was somewhat effective for weeding between crop rows, it was ineffective between the plants. This limitation drove our change to a dual-pronged, laser, spot sprayer approch:

**Spot Sprayer**
Our current goal with this is to have the computer vision spot a weed then the system targets weeds located between rows. After it delivers a contained chemical dose directly to the weed without saturating the surrounding soil or spraying the horseradish plant.

**Targeted Laser System**
Eliminates weeds growing directly between the horseradish plants where chemicals and mechanical methods cannot effectivly operate.

---

## My Contributions

As the sole Electrical Engineer on the project as of now, I act as a sort of EE consultant, aiding in desgin of the electrical components of the spot sprayer and helping in the development of the hardware and firmware for the laser system.

### Custom Hardware & PCB Design

**Peripheral Integration**
Designed and routed a custom PCB (see included KiCad files) to serve as the central interface connecting the robot's peripherals and motor drivers to the main processing computer.

**System Documentation**
Drafted and formalized the complete electrical schematic for the entire laser system to aid in debugging and allow for other lab personel to use as a reference.

### Firmware & Motor Control (C++ & TMC2209)

**Sensorless Homing**
Currently developing a C++ control loop utilizing UART communication with a TMC2209 stepper motor driver. This script monitors motor load to achieve sensorless homing, by detecting when the laser mount reaches the limits of the track.

**Positional Tracking**
By recording when the stepper motor contacts the rail edge, the script calibrates positional data. This data is going to be fed back into the aiming program so the computer vision algorithm can target the laser. We may also switch to using UART for all mount movement.

### Mechanical Integration & Future Enhancements

**Hardware Mounting**
Aided on mechanical design decisions for how the laser is mounted to aid in electrical routing and sensor placement.

**Dynamic Targeting — Rotational Degree of Freedom**
Currently working with mechanical team members to add a rotational degree of freedom to the laser mount using a servo motor. Combined with the stepper motor, this will allow the system to continuously track a targeted weed while the Amiga platform continues to move, hopfuly improving the robot's speed and efficiency.

---