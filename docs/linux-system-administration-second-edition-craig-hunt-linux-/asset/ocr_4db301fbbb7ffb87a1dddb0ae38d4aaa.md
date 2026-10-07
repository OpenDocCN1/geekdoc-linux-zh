# # Chapter 11: Serial Communications, Terminals, and Modems

# ## Overview

Throughout much of the history of computing, serial ports have been important hardware devices. Serial ports allow us to connect two computers together or to connect a computer to another device, such as a printer or mouse. The general-purpose nature of serial ports has allowed them to be used for a wide variety of tasks. The downside to serial ports is that they're slow. The traditional RS-232 serial port on x86 computers is usually capable of a maximum transfer rate of 115,200 bits per second (bps). A more recent type of serial port, the Universal Serial Bus (USB) is faster, at 12,000,000bps (12Mbps), with an even faster version beginning to emerge. This rate compares to 100Mbps for modern Ethernet devices. All in all, the RS-232 serial port is not as important today as it once was, but the USB port has become an important interface method for low-speed external devices. Nonetheless, there are many jobs for which the RS-232 serial port is still well-suited. This chapter covers those jobs, which include linking “dumb” text terminals to a Linux system, using modems to connect to other systems over telephone lines, and using printers connected via serial ports. (Although mice are often connected via the serial port, their configuration and use is comparatively simple; it is covered in Chapter 13, “The X Window System.” Most printers are connected via parallel ports, and their configuration is covered in Chapter 10, “Printers and the Spooling Subsystem.”) This chapter also covers USB configuration, which is very different from RS-232 configuration.

# ## Understanding Serial Devices

Before digging into the details of how to use serial ports to accomplish specific goals, it's helpful to understand precisely what a serial port is and how Linux treats the low-level serial port hardware. These details dictate what can and cannot be done with a serial port under Linux, and how you communicate with the serial hardware.

# ## Standard Serial Devices

Most x86 computers come with two built-in RS-232 serial ports. These devices typically use 9-pin male connectors on the computer, as shown in Figure 11.1, but some serial ports (particularly on older computers and noncomputer devices) use 25-pin connectors. The connectors on modems, printers, and other serial devices are usually female.