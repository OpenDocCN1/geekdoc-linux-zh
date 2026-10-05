# 252 Part V: Going Online

Modems, quite simply, do three main functions:

+   - Convert digital information into tones that go across telephone lines (and vice versa)
- Dial the telephone number you want to reach and make the connection with a modem at the other end
- Negotiate with the modem at the other end for the speed to use when sending bits of information

# Types of modems

Modems can be either internal or external. An external modem stays in its little box and usually plugs into a wall outlet for power, the telephone line for the connection, and into a serial connector on the back of your computer. An internal modem is usually plugged into a slot on the motherboard inside the computer case. (Some internal modems are built directly onto the motherboard.) To the computer and operating system, an internal modem appears as if it were two or more serial ports. Internal modems draw their power from the computer system, and they plug into the phone jack.

Usually, internal modems are less expensive than their external counterparts, but some people like external modems because they can hook them up to different computer systems by simply unplugging the serial line from one system box and plugging it into another.

A third type of serial line modem is a PCMCIA card (sometimes called a PC card). These are used most often with laptop computers.

Internal modems come in two flavors: hardware and software. Winmodems are not supported by Linux.

If you have an external modem or an internal modem that has jumpers and is jumpered for a specific serial port, you can skip ahead to the section titled "Finding the serial line." If you have a plug-and-play modem, you first have to configure your system, which is described in the next section.

![](bbox=[0.115, 0.655, 0.203, 0.725])

# Configuring a plug-and-play modem

If you have a plug-and-play modem, you need to create a configuration file for the modem. This must be done when you are logged in as the root user. The steps to do this are:

+   - Use the pnpdump program to probe your plug-and-play devices and direct that output to the plug-and-play config file: