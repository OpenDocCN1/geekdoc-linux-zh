# Part IV: Fedora and RHEL Network and Server Setup

use it. Following that, you can refer to the “Configuring Print Servers” to learn how to make the server available to users from other computers on your network.

The printers that you set up can be connected locally to your computer (as a parallel or USB port) or to another computer on the network (for example, from another UNIX system, Windows system, or NetWare server).

# Configuring local printers

Add a local printer (in other words, a printer connected directly to your computer) with the Printer configuration window using the following procedure. (See the “Choosing Printer” sidebar if you do not have a printer).

> TIP: You should connect your printer before starting this procedure. With the printer connected, the Printer configuration window might be able to scan for the printer to determine the printer’s location and to test the printer immediately when you have finished adding it.

# Adding a local printer

To add a local printer, follow these steps as root user:

+   1. Make sure that the CUPS service (cupsd daemon) is running. Just to make sure, type the following:
```bash
# service cups restart
```
2. To open the Printer configuration window, either select System -> Printing from the panel or type the following from a Terminal window:
```bash
# system-config- &
```
The Printer configuration window appears. Note that printers detected on the local LAN appear under the Remote Printers heading.
3. Click New Printer. A New printer window appears, and click Forward. If it is not detected, choose the device to which the printer is connected
4. If the printer you want configure is detected, simply select it and connect (LPT #1 and Serial Port #1 is the first parallel and serial ports, respectively) and click Forward. (Type /usr/sbin/lpinfo -v | less to see all available ports.)nYou are asked to identify the printer’s driver.
5. To use an installed driver for your printer, choose Select Printer From Database, and then choose the manufacturer of your printer. As an alternative, you could select Provide PPD File and supply your PPD file (for example, if you have a printer that is not supported in Linux and you have a driver that was supplied with the printer). PPD stands