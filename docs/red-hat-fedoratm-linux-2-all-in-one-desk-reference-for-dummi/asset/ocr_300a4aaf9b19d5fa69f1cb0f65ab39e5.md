# Testing the modem

After you complete the physical installation of the modem and verify that the Linux kernel detects the serial port, you can try to dial out through the modem. The best approach is to use the Minicom serial communications program that comes with Fedora Core.

Minicom is similar to other communications software, such as Procomm or Crosstalk, that you may have used under MS-DOS or Windows.

To run Minicom, log in as *root* and type **minicom** at the shell prompt in the terminal window (or in a virtual console). Minicom runs and resets the modem. Figure 1-8 shows the result of running Minicom in a terminal window.

![](bbox=[0.14, 0.39, 0.63, 0.59])

If you don’t see the words OK, it probably means that this particular serial-device name is not set correctly. To set the serial device, follow these steps:

+   1. **Press Ctrl+A and then Z.**
+      Minicom displays its help screen.
+   2. **Press O.**
+      Minicom displays its configuration menu.
+   3. **Use the arrow key to select Serial port setup and press Enter.**
+      Minicom displays the serial port settings.
+   4. **Press A.**
+      Minicom puts the cursor in the line that shows the serial-device name. Edit the device name to match where your modem is connected. For example, if the modem device is set up with the /dev/modem symbolic link, make sure that the device name is set to /dev/modem.