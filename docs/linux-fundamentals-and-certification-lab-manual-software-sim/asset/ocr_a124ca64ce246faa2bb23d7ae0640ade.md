a module name is listed in brackets, the module in the brackets is dependent on the loaded module.

For example, from Figure 8–27, **parport_pc** has been used one time and may be autocleaned, **parport** has been used one time and may be autocleaned, and parport_pc and lp are dependencies.

# ## ■ ADDING HARDWARE

Available devices that can be added to a computer system are too numerous to list here. Typical devices that will be added are printers, scanners, modems, Ethernet adapters, sound adapters, video adapters, RAM, and storage devices. The only thing that these devices have in common is the sequence of events used to add them:

+   1. Configure the new device.
2. Physically install or connect the device to the computer system.
3. Install the driver for the device and configure it for use.
4. Test the device.
5. Make the device available.

# ### External Hardware Connections

Some devices only require connections to existing ports on a computer system, whereas others must be installed inside the system case. The connections (ports) available on most computer systems are shown in Figure 9–28.

![](bbox=[0.03, 0.48, 0.91, 0.65])

+   * **PS2 Mouse/Keyboard**  Some keyboards and mice use other connectors. The older keyboards have a much larger connector, and the newer models may connect to a USB port.
* **Ethernet**  This connection is used to connect to the Internet. It is a standard Ethernet connector and usually 100BASE-T type (100 Mbps). The speed range can be from 10 to 1000 Mbps.
* **Parallell**  The parallel port is usually used for a printer connection, but other devices can use it to connect as well. Parallel devices can receive more than one bit at a time.
* **Game**  The game port is used to connect a joystick or other game-type device. Game devices can connect to other ports as well.
* **USB**  Universal Serial Bus. These connections are a relatively new standard that supports transfer speeds up to 12 Mbps to and from devices. Devices connected to a USB can be daisy-chained. Up to 127 devices can be connected to a single USB port.
* **Serial**  Serial ports are used to connect a mouse, an external modem, and many other devices. Serial ports communicate one bit at a time.
* **Video**  Typically a VGA monitor will be connected to this port. This port could also connect to an overhead projector.