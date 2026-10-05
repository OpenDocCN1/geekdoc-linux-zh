# Chapter 15: Setting Up Your Internet Connection 255

![](bbox=[0.075, 0.115, 0.143, 0.203])

If you are not sure which resources are currently in use and which resources are available, you can look at the contents of the files /proc/interrupts and /proc/ioports. These files contain a list of the irq's and ioports currently used in your system.

# Finding the serial line

In this section, we discuss how to determine which serial line your modem is connected to. If you have an external modem, you should look at the outside of your computer and see COM port your modem is connected on. If you have an internal modem that is jumpered, you can open up your computer and look at the jumpers; or if you have Windows 95 on your system, you can see which port or COM line the modem is connected by following these steps:

+   1. Click Start -> Control Panel.
The Control Panel window appears.
2. Click the Modem icon.
The Modems Properties dialog box appears.
3. Click the Diagnostics tab.

You see your modem listed, with a COM line beside it. This is the Windows designation for your modem's serial communications line.

After you connect your modem, you have to tell Linux which serial line (or simulated serial line) is connected.

Another way to determine which serial line the modem is attached to is use the statserial program. This program is included in the SuSE Linux For Dummies CDROM, which is not installed by default. If you are not familiar with how to add programs (packages) using YaST, please refer to Chapter 5. By unhooking everything but the modem from your serial lines, you issue the statserial command to determine which port your modem is attached to. Each time you execute the program, you provide it with another serial line designation (/dev/tty0, /dev/tty1, /dev/ttyS3) and which of the designations have the Clear and Set Data Ready values to 1. For example, in Figure 15-1, those values are 0 for /dev/tty0.

Sometimes, the program fails to work and displays an error message like the following:

```
statserial: TIOCMGET failed: Input/output error
```

Yet you use the statserial command on a line with a modem on it, the CTS and LSR values are 1, as shown in Figure 15-2.