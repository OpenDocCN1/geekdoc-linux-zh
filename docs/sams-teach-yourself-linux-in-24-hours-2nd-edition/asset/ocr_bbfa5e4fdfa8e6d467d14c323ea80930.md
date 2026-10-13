# Winmodems

Winmodems (part of a disgusting recent trend by PC and laptop manufacturers trying to save a few pennies per unit) are operating system-specific and will probably never be supported by Linux. These modems, which use less hardware than "real" modems, work through the use of software drivers (it's cheaper to offload all the work on your computer's CPU; besides, if you use Windows 9x, you're only doing one thing at a time anyway, right?). If you buy a PC or laptop with one of these modems, you're at the mercy of the manufacturer whether the modem is supported in the future or whether it works with another operating system.

![](bbox=[0.22, 0.42, 0.3, 0.5])

> Beware! Many manufacturers tout these modems as "56K ITU V.90 modems," but fail to mention they are winmodems. Ask if the modem can be used with DR-DOS, PCDOS, or MSDOS. If not, it's a winmodem. To be safe, buy an external modem that can be used with any computer operating system.

# Infrared Ports

Although software to support your computer's infrared port isn't included on this book's CD-ROM, the good news is that there is full infrared support for OpenLinux. This means that if you have a laptop or desktop with an IR port, you can now network, print to an IR printer (such as an HP 340Cbi or Canon BJC80), and even transfer or back up your 3Com Palm PDA without cables! Browse to this site:

http://www.cs.uit.no/~dagb/irda/irda.html

There are directions on how to download, install, and configure IR support for Linux. For complete directions in a HOWTO document format, browse to this site:

http://www.userpage.fu-berlin.de/~r2d2c3po/ir_howto.cgi

![](bbox=[0.22, 0.78, 0.3, 0.85])

> If you own a 3Com Palm Pilot Professional or Palm III, there are nearly two dozen Pilot support utilities included with OpenLinux. Kenneth Albanowski's pilot-xfer command makes backing up a Palm III as easy as this:
> 
> `pilot-xfer /dev/pilot -b pilotbackupdirectory`
> 
> If you use KDE, use the Kpilot client, installed from the `/col/install/RPMS` directory on your OpenLinux CD-ROM. This is a graphical interface to administering your Palm computer.

```
pilot-xfer /dev/pilot -b pilotbackupdirectory
```