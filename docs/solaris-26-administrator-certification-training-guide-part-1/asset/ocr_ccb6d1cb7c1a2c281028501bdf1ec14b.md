a serial port. a system can support as many character display terminals as it has serial ports. If you run out of ports, you can add more. The disadvantage with the alphanumeric display is it will not display windows or graphics and does not support a mouse.

The bit-mapped graphics display is connected to the system via a graphics adapter of some kind. You simply need to plug the monitor into the system to make it operational. On a bit-mapped graphics display, you don't have to perform any special steps to administer it. The drawback, however, is that most computers support only one graphics display.

# Modems

Modems are also connected to a system through a serial port and are used for remote access over telephone lines. Modems can be set up in three basic configurations:

+   - Dial-out
- Dial-in
- Bidirectional

A modem connected to the local computer might be set up to provide dial-out service, meaning you can access other computers but nobody outside can gain access to this computer. Dial-in service is just the opposite. It allows users to access a system from remote sites, but it does not permit calls to the outside world. Bidirectional access provides both dial-in and dial-out capabilities.

# Cabling

Finally, a few words about cabling. The RS-232 standard defines two types of equipment: Data Terminal Equipment (DTE) and Data Communications Equipment (DCE). Most computers are DTE; modems are always DCE. DTE uses pin 2 to transmit data and pin 3 to receive data; DCE does the reverse. To connect a computer to a modem or printer (DTE to DCE), you make the cable connection straight through. To make a connection between two computers (DTE to DTE) or between a computer and a terminal, you need a cable with pins 2 and 3 crossed. This is often called a null-modem or modem-eliminator cable. To save yourself a great deal of frustration, make sure you configured your cables properly before you configure the port monitor and services.

# Software Terminology

Now that I've described the hardware pieces, I will briefly describe the components of the operating system that add functionality to the ports, terminals, and modems.