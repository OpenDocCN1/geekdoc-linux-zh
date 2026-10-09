will help you test your serial console configuration.

# **UEFI/BIOS Serial Console Configuration**

Once your BMC is ready, you must configure the server hardware to direct a serial port to the BMC. Go to the hardware’s Setup menu, where you configure your UEFI or BIOS. Somewhere in that maze of twisty little options, you’ll find something like “Serial Port Console Redirection.”

A vital question here is, how many serial ports does your host have? Maybe it has none. Maybe it has several. You can choose to redirect one of those ports or add an additional, virtual port. I encourage you to leave your existing serial ports alone and add a virtual port dedicated to SOL. It’s probably called something like “SOL Console Redirection.” Enable it, and go into the settings for that port.

Here are some settings I find helpful for FreeBSD and SOL:

+   - **Terminal type** vt100
+   - **Data bits** 8
+   - **Parity** none
+   - **Stop bits** 1
+   - **Flow control** none

The tricky part is the baud, speed, or bits-per-second setting. Stick with the default speed, but make a note of it. You’ll need the speed to connect.

Now that you have a serial console, set up FreeBSD.

# *Configuring FreeBSD’s Serial Console*

As FreeBSD boots, the loader decides where to print console messages and where to accept input from. While this defaults to the monitor and keyboard, with a few tweaks, you can redirect the console to a serial port. The serial console won’t grant BIOS access, but you can tweak the