# ## Debug Probe

Les Pounder was about to reach for a can of fly spray in an effort to rid his code of bugs, but then he spotted this.

**IN BRIEF**  
An RP2040-based board, but instead of writing code, this board helps debug our code. Aimed more at advanced users, typically C/C++ coders, Debug Probe is a useful tool for those who need it. The bonus USB serial adaptor makes it useful for serial consoles on Raspberry Pi and other SBCs.

![](bbox=[0.57, 0.24, 0.93, 0.41])

> Encased in plastic, this RP2040 board is here to help you debug your bare-metal Pico projects.

The latest RP2040 device from Raspberry Pi isn’t a Pico, rather it is something we can use to debug a Pico. The Raspberry Pi Debug Probe is an RP2040-powered board designed for use with debugging tools. With it, we can interactively step through and identify issues with code running on a Pico (or other compatible device). The probe is used to observe data from a running program and provides a bridge between the Serial Wire Debug (SWD) port of the Pico, the three unsoldered pins opposite the Micro USB port and USB on your machine. Using the standardised CMSIS-DAP protocol, the Debug Probe can be used with debug software applications such as OpenOCD.

The Debug Probe is contained in a frosted plastic case, there to protect it from stray wires. We elected to free our probe from its plastic prison and the green PCB really stood out from the crowd. The small PCB is clearly from the Raspberry Pi pedigree.

# **Soldering on**

The Debug Probe connects to the Pico via the UART pins and SWD pin header. Typically, the SWD pins are unsoldered, so you need to solder them on and use the included connectors to make the connection. Owners of a presoldered Pico, typically known as Pico H, can use the included JST-style connector. This makes it a breeze to connect up without worrying which wire is which.

After wiring up, we need to install the software, which is where you may hit an issue. First, the documentation is great, but there is a lot of it, and sometimes it can get overwhelming. It took us two coffees and a little head scratching to get everything working and for usable output to be visible. We also elected to use Microsoft’s VSCode as the main part of the test, as Raspberry Pi has put a lot of work into this editor. That said, *OpenOCD* via a terminal is also a very usable experience. We used the *hello_serial.c* example and clicking Build we had a compiled example in mere seconds. The serial monitor output confirmed that *LXF POOL2*, so we set the debugger to active and watched an extremely verbose stream of data fire through the debug console. Setting a breakpoint was just a click away, providing us with a pause in the code where we could take stock. After a successful debug, it was just a matter of compiling our code into a UF2 file, then flashing it to the Pico H. And with that, we had our code running with zero bugs.

So, who is the £12 Raspberry Pi Debug Probe for? Good question. If you are building code directly on the hardware (bare metal), no operating system, just your code and the processor, you need this. You could make your own using a £4 Pico and a few wires, but for the extra money you get a dedicated and quite frankly lovely looking board. If you don’t need debug functionality, and bear with us here, the Debug Probe can be used as a USB-to-serial adaptor. It can be connected to the serial port of any device. We connected it to a Raspberry Pi 4, used *Raspi-config* to enable the serial interface and login prompt, then we connected up using a spare Thinkpad and *Tio*, a great terminal/serial software tool.

The bottom line for the Raspberry Pi Debug Probe is that if you need it, you’ll buy it. This is aimed more at those creating bare-metal projects with their Raspberry Pi Pico, but it is not limited just to this.

![](bbox=[0.05, 0.78, 0.49, 0.93])

> Freed from its case, the Debug Probe is quite nice looking and matches the other Raspberry Pi boards.

# **VERDICT**

+   - **DEVELOPER**: Raspberry Pi
+   - **WEB**: www.raspberrypi.com
+   - **PRICE**: £12

| FEATURES | 8/10 | EASE OF USE | 8/10 |
|---|---|---|---|
| PERFORMANCE | 8/10 | VALUE | 8/10 |

If debugging bare-metal code or making serial connections, Debug Probe is the leading contender for your money.

# Rating **8/10**