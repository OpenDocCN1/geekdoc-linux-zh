
![](img/5fe8f856723cde0b366f73584b9e64b8_135_0.png)

### **Figure 11-1** *Minicom’s setup menu*

With the Modem and Dialing entry highlighted, press Enter. Minicom displays another menu (see Figure 11-2) with a list of settings that you can change. Minicom places the cursor on the first line, as shown in Figure 11-2. Press A to change the modem initialization string.

![](img/5fe8f856723cde0b366f73584b9e64b8_135_1.png)

### **Figure 11-2** *Setting modem and dialing parameters in Minicom.*

You can then use the Backspace key to edit that line and type the AT command you need to initialize the modem. For example, consider a 56K modem that the user initializes with the following AT command (check your modem manual for the appropriate initialization string):

AT &F1 E1 V1

After you enter the modem initialization string, press Enter to return to the top-level menu.

## Session 11—Using Modems in Red Hat Linux

The AT commands are commands that you can use to control a modem and perform tasks such as dialing a number, turning the modem’s speaker on or off, and setting the modem to answer an incoming call. These commands start with the two characters AT (for attention). You can use AT commands for situations in which the communications software is primitive and all the software does is send the modem whatever you type.

After making your changes, if any, use the up and down arrow keys to highlight the item labeled Save as dfl (meaning save as default) and then press Enter. Minicom saves the settings in the /etc/minirc.dfl file—its default configuration file. You can exit Minicom by selecting Exit from Minicom and pressing Enter.

### Running Minicom as an ordinary user

You also need to do the following before any user can run Minicom:

- Open the text file /etc/minicom.users in a text editor and verify that it has a line with the word, ALL. (This enables all users to access Minicom’s default configuration file.) If not, add a line with the word, ALL.
- Assuming that you want all users to be able to dial out using the modem, enable any user to read from and write to the serial port where the modem is connected. For example, if the modem is on COM1 (/dev/ttyS0), type chmod o+rw /dev/ttyS0 to give everyone write permission for that device.
- Establish a link between the /dev/modem and the serial port device where the modem is connected. If the modem is on COM1 (/dev/ttyS0), you should type the following command:
  `ln -s /dev/ttyS0 /dev/modem`

After that, you can run Minicom as an ordinary user. When Minicom first runs, it resets the modem. Figure 11-3 shows the result of running Minicom in a terminal window.

```txt
Welcome to minicom 1.83.1
OPTIONS: Icrtity,Buffer, Fkey Macros, Search History,Buffer, I18n
Compiled on Feb 23 2001, 07:31:40
Press CTRL-\n 2 for help on special keys
ST, #F1, EV V1
```

![](img/5fe8f856723cde0b366f73584b9e64b8_136_0.png)

Press Ctrl+A to get the attention of the Minicom program. Then if you press Z, a help screen appears in the form of a text window (as shown in Figure 11-4).

![](img/5fe8f856723cde0b366f73584b9e64b8_137_0.png)

### Figure 11-4 The Minicom help screen

In the help screen, you can get information about other Minicom commands. From the help screen, press Enter or Esc to return to online mode. In online mode, you can use the modem's AT commands to dial out. In particular, you can use the ATDT command to dial the phone number of another modem, such as with your Internet Service Provider's (ISP's) computer or a system where you work (see Figure 11-5). Once you get the login prompt, you can log in as usual and use the remote system.

![](img/5fe8f856723cde0b366f73584b9e64b8_137_1.png)

### Figure 11-5 Connecting to a remote system using Minicom

When you log out of the other system and want to exit Minicom, press Ctrl+A and then type X to exit the program. Press Enter again in response to the Minicom prompt.

### Troubleshooting

If `setserial` shows the UART as unknown, as you see in the following example, the kernel has not detected your serial port or the modem attached to it:

```
/dev/ttyS2, UART: unknown, Port: 0x03f8, IRQ: 10
```

This usually occurs because your PC’s BIOS is set up to expect a Plug and Play (PnP) operating system. To solve the problem, reboot the PC and, as it powers up, press the key that permits you to access the system’s BIOS. Typically, this is a function key, such as F2, but the exact key depends on your PC’s BIOS. In the setup screen, locate the option for the PnP operating system (often labeled “Plug & Play O/S”) and turn off that option. Then save the BIOS settings and exit. This causes the PC to reboot. This time, when Red Hat Linux boots, the kernel should be able to detect the PC’s serial port correctly.

If your serial ports are correctly detected but the modem does not respond, make sure that `/dev/modem` is linked to the proper device file in `/dev`. This is especially common with PCI modem cards, which typically do not use COM1 (`/dev/ttyS0`) or COM2 (`/dev/ttyS1`) by default. For example, `sudo dmesg | grep ttyS` shows the following:

```
ttyS2 at port 0x6800 (irq = 10) is a 16550A
```

In this case, execute the following command to make sure that `/dev/modem` is linked to the proper device file:

```
ln -sf /dev/ttyS2 /dev/modem
```

If your modem does not appear to be detected, use the Windows Device Manager to obtain its IRQ and I/O address, and compare those values to the values the `setserial` command reports for that port.

Presently, some modems simply do not work with Linux. These are so-called “WinModems,” which rely on the Windows operating system and a special, Windows-specific device driver to function. WinModems, also called software modems, rely on a device port, rather than hardware, to function. In this case, your only recourse is to replace the modem with a hardware modem.

### Review

You started the session by learning the device names for serial ports in Red Hat Linux. You used the Minicom serial communications program to dial out with a modem. In the course of dialing out, you learned several AT commands used to control the modem.

## QUIZ YOURSELF

- What is the device name for the second serial port (COM2)? (See "Learning the serial port device names.")
- How can you check to see if Linux detects any serial ports in your PC? (See "Checking if Red Hat Linux detects the serial devices.")
- What program can you use to dial out through the modem? (See "Dialing Out with Minicom.")
- What AT command do you use to make the modem dial a phone number? (See "Running Minicom as an ordinary user.")
- What do you have to do to establish a link between the /dev/modem and the serial port device where the modem is connected? (See "Running Minicom as an ordinary user.")

![](img/5fe8f856723cde0b366f73584b9e64b8_140_0.png)

## Networking Your Red Hat Linux PC

**Session Checklist**

- Setting up an Ethernet LAN
- Configuring TCP/IP networking in Linux
- Using TCP/IP diagnostic commands in Linux
- Examining TCP/IP network configuration files

![](img/5fe8f856723cde0b366f73584b9e64b8_140_1.png)

**R**ed Hat Linux includes extensive built-in networking capabilities. In particular, Red Hat Linux supports TCP/IP (Transmission Control Protocol/Internet Protocol) networking over several physical interfaces, including Ethernet cards, serial ports, and parallel ports. You typically use an Ethernet network for your local area network (LAN). TCP/IP networking over the serial port enables you to connect to other networks by dialing out over a modem.

This session focuses on Ethernet LANs. You learn how to set up, configure, and monitor an Ethernet TCP/IP network. Much of what you learn also applies to TCP/IP networking over a dial-up connection, discussed in the next session.

### Setting Up an Ethernet LAN

Ethernet is a standard way to move packets of data among two or more computers connected to a single cable. To set up an Ethernet LAN, you need an Ethernet card for each PC. Linux supports a wide variety of Ethernet cards for the PC.

Ethernet is a good choice for the physical data-transport mechanism because it’s a proven, low-cost technology that provides good data transfer rates—typically 10 million bits per second (10 Mbps) although there is now 100 Mbps and even Gigabit (1000 Mbps) Ethernet.

In an Ethernet LAN, computers are connected to the network with cables. Nowadays, there are two popular forms of Ethernet cables. The first option is 10Base2, sometimes
