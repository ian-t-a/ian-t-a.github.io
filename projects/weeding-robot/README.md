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

There are some limitations to this system. One being that some chemicals have different methods of action. Some of these methods of action require the chemical to enter the plant via the root system. We want to avoid this, as it may cause EPA compliance issues. Another issue is that some chemicals need to be applied more generously than others. When spot spraying, only a small dose is applied to the plant, which may not be effective with chemicals that require higher dosing. We are currently testing these limitations to determine the most effective approach to addressing these concerns.

**Targeted Laser System**
Eliminates weeds growing directly between the horseradish plants where chemicals and mechanical methods are either ineffective or not permitted.

---

## My Contributions

As the only Electrical Engineer on the project as of now, I act as a sort of EE consultant, aiding in desgin of the electrical components of the spot sprayer and helping in the development of the hardware and firmware for the laser system.

### Custom Hardware & PCB Design

**Peripheral Integration**
Designed and routed a custom PCB (see included KiCad files) to serve as the central interface connecting the robot's peripherals and motor drivers to the main processing computer.

**System Documentation**
Drew out complete electrical schematic for the entire laser system to help debugging efforts and let other lab personel to use as a reference.

### Firmware & Motor Control (C++ & TMC2209)

**Sensorless Homing**
Currently developing a C++ control loop utilizing UART communication with a TMC2209 stepper motor driver. This script monitors motor load form the output from TMC2209 to have sensorless homing, by detecting when the laser mount reaches the end of the track.

**Future Enhancements**

**Positional Tracking**
By recording when the stepper motor contacts the rail edge, the script calibrates positional data. This data is going to be fed back into the aiming program so the computer vision algorithm can target the laser. We may also switch to using UART for all mount movement.

**Dynamic Targeting — Rotational Degree of Freedom**
Currently working with mechanical team members to add a rotational degree of freedom to the laser mount using a servo motor. Combined with the stepper motor, this will allow the system to track a weed while the Amiga platform moves in the field, hopfuly improving the robot's speed and weeding effectivness.

---