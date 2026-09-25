# Weeding Robot Interface Board

**[View the KiCad project on KiCanvas](https://kicanvas.org/?repo=https%3A%2F%2Fgithub.com%2Fian-t-a%2Fian-t-a.github.io%2Ftree%2Fmain%2Fprojects%2Fweeding-robot%2Fkicad%2F)**

## Description

This board was designed to clean up the wiring previously used to connect all the peripherals to our main computational board, the Jetson Orin Nano. We were originally using breadboards and jumper wires to connect the peripherals, including the laser driver board, stepper motor driver, stepper motor, and edge detection modules. This was neither a sustainable nor a reliable way to connect our peripherals, and it often caused connectivity and signal integrity issues during testing. It also made debugging difficult, since it was hard to tell whether an issue was caused by a bad connection or an actual software bug. To move the project further along and improve our debugging and development efficiency, we needed a better long-term solution: a PCB.

## Design Decisions

There were a number of constraints for this board, mainly the UART and PWM traces to the stepper motor and laser driver, and the requirement to connect to the Jetson Orin Nano while being powered partially by the Jetson and partially by an external power source. Other constraints included providing the appropriate connectors for the edge detection modules, stepper motor, and laser driver board.

**Connectors — JST**
For the peripheral connectors, I went with JSTs. This decision was based on needing a connector with a latching mechanism, as well as the ability to detach quickly from the board for easy transport and debugging. The board has a max output of around 5A to the laser driver board, which the JST connectors could comfortably handle. Most of our peripherals also already used JST connectors, so standardizing on JST let me avoid changing the existing connectors on the peripherals themselves.

**Jetson Interface — Long-Lead 2x20 Header**
To connect to the Jetson, I used a long-lead female 2x20 pin header. This makes the board a HAT that sits directly on top of the Jetson. I chose long-lead headers specifically so jumper wires could still be connected to the Jetson's pins while the HAT was installed, which made debugging and prototyping much easier.

**Two-Layer Stackup**
I originally thought the board would be fairly simple, so I made it a two-layer board to reduce manufacturing costs, which in hindsight was an oversight. That decision has some downsides, mainly the lack of a solid ground plane, which can cause signal integrity issues, especially on the UART lines. We also recently upgraded to a new, more powerful laser with different voltage and current requirements. Between that change and my concerns about the lack of a proper ground reference, I'm currently working on a new board in Altium.

## Planned Improvements

- **Four-layer stackup** to provide a solid ground plane
- **Smaller form factor**, if possible
- **Improved signal integrity** and reduced EMI