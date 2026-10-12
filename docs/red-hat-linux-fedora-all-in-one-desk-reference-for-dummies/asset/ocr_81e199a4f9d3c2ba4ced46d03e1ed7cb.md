If you see a message such as the following, then Linux has detected a serial port in your PC:

```
ttyS0 at 0x03f8 (irq = 4) is a 16550A
```

In this case, the message indicates that the Linux kernel has detected the first serial port (COM1). It shows the I/O address (in hexadecimal), 0x3f8, and IRQ 4. The last part of the message — 16550A — refers to the identifying number of the universal asynchronous receiver/transmitter (UART) chip, which is at the heart of all serial communications hardware (the UART converts each byte to a stream of 1s and 0s, and vice versa when it receives such a stream).

You can also check for the serial ports with the setserial command. Type the following command to see detailed information about the serial ports:

```
setserial -g /dev/ttyS?
```

Any device that is listed in the output of this command with an unknown UART is either not installed or not detected by the Linux kernel.

![](bbox=[0.15, 0.28, 0.25, 0.4])

# Testing the modem

After you complete the physical installation of the modem and verify that the Linux kernel detected the serial port, you can try to dial out through the modem. The best approach is to use the Minicom serial communications program that comes with Red Hat Linux.

Minicom is similar to other communications software, such as Procomm or Crosstalk, that you may have used under MS-DOS or Windows.

To run Minicom, log in as root and type minicom at the shell prompt in the terminal window (or in a virtual console). Minicom runs and resets the modem. Figure 1-8 shows the result of running Minicom in a terminal window.

If you don't see the OK, it probably means that this particular serial-device name is not set correctly. To set the serial device, follow these steps:

+   1. Press Ctrl+A and then Z.
+      Minicom displays its help screen.
+   2. Press O.
+      Minicom displays its configuration menu.
+   3. Use the arrow key to select Serial port setup and press Enter.
+      Minicom displays the serial port settings.
+   4. Press A.