
# The Installation Guide for Red Hat Linux 6.0

- If you find a mouse that you are certain is compatible with your mouse, highlight that entry.
- Otherwise, select one of the Generic entries, based on your mouse's number of buttons, and its interface. To determine your mouse's interface, follow the mouse cable back to where it plugs into your system. If the connector at the end of the mouse cable plugs into a rectangular connector, you have a serial mouse. On the other hand, if the connector is round, you have a PS/2 mouse. If you are installing Red Hat Linux on a laptop computer, in most cases the pointing device will be PS/2 compatible.

The Emulate 3 Buttons check box allows you to use a two-button mouse as if it had three buttons. In general, it's easiest to use the X Window System if you have a three-button mouse. If you select this check box, you can emulate a third, “middle” button by pressing both mouse buttons simultaneously.

If you've selected a mouse with a serial interface, you will then see a screen similar to the one shown in Figure 6-2. Simply highlight the appropriate serial port for your mouse, select Ok, and press [Space].

![](img/46f4935125ba89e12897afbe9d77a097_137_0.png)

Figure 6-2: Serial Mouse Port Selection

If you wish to change your mouse configuration after you have booted your Red Hat Linux system, you may use the /usr/sbin/mouseconfig command. If wish to configure your mouse as a left-handed mouse, you can reset the order of the mouse buttons. This may be done after you have booted your Red Hat Linux system, by typing gpm -B 321.

## Configuring Networking

Next, the installation program gives you an opportunity to configure (or reconfigure) networking. If you are installing from CD-ROM or from a local hard disk, the installation program asks if you want to configure networking. If you choose No, your Red Hat Linux system will be a standalone workstation. If you choose Yes, you may configure networking as described below. If you are installing via network media you have already entered temporary networking information that was used during the installation. The install program offers you three choices (see Figure 6-3 and 6-4):

![](img/46f4935125ba89e12897afbe9d77a097_138_0.png)

Figure 6-3: Network Configuration Options — Local Media Install

### Figure 6-4: Network Configuration Options — Network Install

- Keep this setup — Keeps the network configuration you used during the installation. All the networking information you entered previously becomes part of your system’s permanent configuration.
- Reconfigure network now — The installation program presents the network configuration dialogs in Network Driver Configuration. The values you used during installation will be filled in as defaults. Choose this if your system will be installed on a network other than the one you used to install Red Hat Linux.
- Don’t setup networking — Don’t set up networking at all. Your system will not have networking configured. Choose this if you installed your system over a network, but it will be used as a standalone workstation.

## Network Configuration Dialogs

If you elected to configure networking at this time, you will be presented with a series of dialog boxes. Please turn to Configuring TCP/IP Networking for more information.

## Configuring the Time Zone

Next, the installation program presents a dialog to help you configure your system's time zone (see Figure 6-5).

If you wish to set the hardware (CMOS) clock to GMT (Greenwich Mean Time, also known as UTC, or Coordinated Universal Time), select Hardware clock set to GMT. Setting it to GMT means your system will properly handle daylight saving time, if your time zone uses it. Most networks use GMT.

> Please Note: If your computer runs another operating system from time to time, setting the clock to GMT may cause the other operating system to display the incorrect time. Also keep in mind that if more than one operating system is allowed to automatically change the time to compensate for daylight saving time, it is likely that the time will be improperly set.

![](img/46f4935125ba89e12897afbe9d77a097_140_0.png)

Figure 6-5: Configuring Time Zones

Select the time zone your system will be operating in from the list, and press [Enter].
