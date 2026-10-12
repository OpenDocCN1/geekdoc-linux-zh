Table 11-1
Device Names for Serial Ports

| COM Port | Device Name | IRQ | I/O Address |
|----------|-------------|-----|-------------|
| COM1 | /dev/ttyS0 | 4 | 0x3f8 |
| COM2 | /dev/ttyS1 | 3 | 0x2f8 |
| COM3 | /dev/ttyS2 | 4 | 0x3e8 |
| COM4 | /dev/ttyS3 | 3 | 0x2e8 |

If you install Red Hat Linux from this book’s companion CD-ROMs, all these devices should already be in your system. If you check the /dev directory, you should find the /dev/ttyS* devices in which * is 0, 1, 2, and 3. From a terminal window, type ls -l /dev/ttyS* to see a listing of these device files.

# Checking if Red Hat Linux detects the serial devices

When you install Red Hat Linux from this book’s CD-ROMs, following the directions in Sessions 1 through 3, the necessary Linux serial devices are automatically created for you. You should have the /dev/ttyS* devices for dialing in and out through the modem.

To verify that Linux detects the serial port correctly, check the boot messages with the dmesg command:

```
dmesg | grep ttyS*
```

If you see a message such as the following, Linux detects a serial port in your PC:

```
ttyS01 at 0x02f8 (irq = 3) is a 16550A
```

In this case, the message indicates that Linux detects the second serial port (COM2). It shows the I/O address (0x2f8) and IRQ (3). The last part of the message — 16550A — refers to the identifying number of the universal asynchronous receiver/transmitter (UART) chip, which is at the heart of all serial communications hardware. (The UART converts each byte to a stream of ones and zeros and then back to bytes when needed.)