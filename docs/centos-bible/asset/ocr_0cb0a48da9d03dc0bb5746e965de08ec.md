# Part IV Networking

The printers that you set up can be connected locally to your computer (as on a parallel or USB port) or to another computer on the network (e.g., from another UNIX system, Windows system, or NetWare server).

# Configuring Local Printers

Add a local printer (in other words, a printer connected directly to your computer) with the Printer Configuration window using the following procedure. (See the “Choosing a Printer” sidebar if you don’t yet have a printer.)

> **TIP** You should connect your printer before starting this procedure. With the printer connected, the Printer Configuration window might be able to scan for the printer to determine the printer’s location and to test the printer immediately when you have finished adding it.

# Adding a Local Printer

To add a local printer, follow these steps as *root* user:

+   Make sure that the CUPS service (cupsd daemon) is running. Just to make sure, type the following:
+   ```bash
+   # service cups restart
+   ```

+   To open the Printer Configuration window, either select **System → Administration → Printing** from the panel or type the following from a Terminal window:
+   ```bash
+   # system-config-printer &
+   ```

+   The Printer Configuration window appears. Note that printers detected on the local LAN appear under the “Remote Printers” heading.

+   Click “New Printer.” A New Printer window appears, as shown in Figure 16-1.

+   If the printer you want to configure is detected, simply select it and click Forward. If it is not detected, choose the device to which the printer is connected (**LPT #1** and **Serial Port #1** are the first parallel and serial ports, respectively) and click Forward. (Type `ls /usr/bin/pinfo -v | less` in a shell to see all available ports.)

+   You are asked to identify the printer’s driver.

+   To use an installed driver for your printer, choose “Select Printer From Database,” and then choose the manufacturer of your printer. As an alternative, you could select “Provide PPD File” and supply your own PPD file (e.g., if you have a printer that is not supported in Linux and you have a driver that was supplied with the printer). PPD stands for “Postscript Printer Description.” Select Forward to see a list of printer models from which you can choose.

+   Select the printer model for your printer. If there are multiple drivers available for the model, you can choose which one you want from the Drivers box.