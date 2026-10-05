# Review Genuino 101

![](bbox=[0.035, 0.055, 0.965, 0.535])

# Mini PC

# Genuino 101

| SoC | |
| --- | --- |
| Intel Curie | CPU |
| Single-core 32MHz Intel Quark | Co-Processor |
| Single-core 32MHz Intel Quark-RISC Core (ARM) | RAM |
| 8KB SRAM (24KB user-accessible) | Storage |
| 1026KB Flash |
| 14 digital (4x PWM), 6 analog | Sensors |
| 6-axis accelerometer and gyroscope | Wireless |
| Bluetooth Low Energy | Logic |
| 3.3V (5V tolerant) | Price |
| €28 (primloni.com) |

For Intel's desire to break into the maker market dominated by ARM and microcontrollers, is the third time the charm?

Intel has been trying to make headway for a few years now, having seen the success of the Arduino project and the Raspberry Pi. The Intel Genuino thanks to poor IO performance from the Quark processor, its successor, the Edison (reviewed in Li&S Issue 138), a unpopular processor issues but is its old form and high-density connectors are off-putting.

which, at a casual glance, looks just like the classic microcontroller-based Arduino Uno. Yet, while it shares the Uno's layout, the Genuino 101 is a different beast.

It seems to be the crack of the whip. Abandoning its previous approach of producing an Arduino-compatible microcontroller, the company has partnered with the Arduino project to create a fully official device; however, the Arduino 101 in the US and Genuino 101 elsewhere avoid trademark issues. The result is a device

an ultra-compact, low-power system-on-chip (SoC) designed primarily for wearable projects, this chip is part of the Intel Quark-RISC processor, with a 32MHz Argon RIS Core (ARC) - a tacit admission from Intel that Quark's ability to directly drive GPIO isn't quite where it should be.

The presence of two processors splits the Genuino in an interesting manner. The Quark, which is fully compatible with an architecture processor based on the company's old Pentium microarchitecture, runs a real-time operating system (RTOS); the ARC