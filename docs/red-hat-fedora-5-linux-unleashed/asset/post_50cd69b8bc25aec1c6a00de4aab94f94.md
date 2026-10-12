
Configuration problems can arise, especially if your sound card's manufacturer will not or cannot release specifications to help open source developers create working drivers. If your sound card is not recognized or is recognized but does not work, and using ALSA fails, you can turn to commercial sound drivers from 4Front Technologies. These relatively inexpensive drivers support more than 350 sound systems and are installed, configured, and controlled using shell scripts. Browse to http://www.opensound.com for more information.

Fedora also includes a Red Hat-derived graphical sound card configuration client that can be used during an X session. Start the `system-config-soundcard` client by clicking your desktop panel's System Settings Soundcard Detection menu or item, or by using the command at a terminal window like so:

```
$ system-config-soundcard
```

After you press Enter, you are prompted for the root password. Enter the password and click OK. The `system-config-soundcard` tries to automatically detect and configure your sound card. You then see a dialog you can use to test your sound card settings, as shown in Figure 4.5. Click the play button to listen to a sample sound.

![](img/2045828cf45e5632bf056f9ca99d6755_134_0.png)

**FIGURE 4.5** The `system-config-soundcard` client is used during an X session to configure a sound card for Fedora.

## Detecting and Configuring a Modem

More than 38 million users in the United States and another 85 million users around the world now connect to the Internet with cable or DSL service, but for many users a modem is the standard way to connect with an Internet service provider (ISP) using the Point-to-Point Protocol (PPP). Other common tasks for modems include sending and receiving faxes. If you add or change your modem after the initial installation, you will need to configure Fedora to use the new modem to perform all these tasks.

Fedora includes several tools you can use to configure and use an internal or external modem in your notebook or PC. Chapter 18, "Network Connectivity," contains the details about configuring Fedora to connect to the Internet using a modem. This section covers how to configure and use modems using serial ports (using a standard formerly known as RS232, but now called EIA232) or USB.

### Configuring a Serial-Port Modem

Linux uses `/dev/ttySX`, `/dev/ttyUSBX` or `/dev/usb/ttyUSBX` for serial ports, where *X* can range from 0 to 15. Many additional ports can be added to a system using multiport cards or chained USB devices. A PC’s integral serial ports are generally recognized at boot time. To see a list of recognized ports for your system, pipe the `dmesg` command output through the `fgrep` command like so:

```
$ dmesg | fgrep tty
ttyS00 at 0x03f8 (irq = 4) is a 16550A
ttyS01 at 0x02f8 (irq = 3) is a 16550A
```

In this example, the `fgrep` command reports that two serial ports have been recognized in the `dmesg` output. Note that the device matching `ttyS00` is `/dev/ttyS0`, despite the kernel output. The PC’s external modem can be attached (most likely using a male DB9 adapter) to either port. Under Linux, nearly all modem-dependent software clients look for a symbolic link named `/dev/modem` that points to the desired device. This link is not created by default, but as root, you can create this device manually using the `ln` command like this:

```
$ ln -s /dev/ttyS0 /dev/modem
```

In this example, `/dev/modem` will point to the first serial port.

You can also use the graphical X client `neat` to configure a modem after the initial installation. Internet connection software such as Fedora’s `system-config-network` client (shown in Figure 4.6) will try to probe the system for an available modem. If a modem is not found, you can manually enter modem data.

KDE provides the `kppp` client (shown in Figure 4.7) that can also be used to look for and set up a modem when you set up a new Point-to-Point Protocol (*PPP*) connection. Click the Query Modem button in `kppp`’s dialog to search for an installed modem.

![](img/2045828cf45e5632bf056f9ca99d6755_136_0.png)

**FIGURE 4.6** Fedora’s system-config-network client will probe for an available modem.

![](img/2045828cf45e5632bf056f9ca99d6755_136_1.png)

**FIGURE 4.7** KDE’s kppp client can be used to find and configure an available modem.

Fedora includes command-line–based diagnostic and serial port configuration tools for the system administrator. For example, to get more information about a specific port, you can use the `statserial` command, along with a designated device like this:

```
# statserial /dev/ttyS0
Device: /dev/ttyS0

Signal  Pin  Pin  Direction  Status  Full
Name     (25)  (9)  (computer)           Name

FG          1               Frame Ground
TxD         2    3     out     Transmit Data
RxD         3    2     in      Receive Data
RTS         4    7     out    1    Request To Send
CTS         5    8     in     0    Clear To Send
DSR         6        in     0    Data Set Ready
GND         7    5              Signal Ground
DCD         8    1     in     0    Data Carrier Detect
DTR        20    4     out    1    Data Terminal Ready
RI         22    9     in            Ring Indicator
```

The sample output is a display of the associated device's port signals. Another tool is the `stserial` command that can be used to display port statistics and reconfigure a serial port's system interrupt or speed. This can be handy when using some serial devices, such as a cellular phone that requires specific serial port characteristics. To get information about a specific port, use `stserial`, along with the device name like this:

```
# stserial -a /dev/ttyS0
/dev/ttyS0, Line 0, UART: 16550A, Port: 0x03f8, IRQ: 4
          Baud_base: 115200, close_delay: 50, divisor: 0
          closing_wait: 3000
          Flags: spd_normal skip_test
```

In this example, the characteristics of `/dev/ttyS0` are displayed. The `stserial` command can also be used to configure or fine-tune a port's characteristics using 32 different command-line options and values.

One option for using a legacy serial device such as a modem on a PC that does not have a serial port but supports USB is to use a USB-to-serial converter. These devices provide a serial port dongle and plug in to a USB hub or port. You can see the output and designated serial port by looking at the output of the `dmesg` command:

```
usb.c: registered new driver serial
usbserial.c: USB Serial support registered for Generic
usbserial.c: USB Serial Driver core v1.4
usbserial.c: USB Serial support registered for Keyspan PDA
usbserial.c: Keyspan PDA converter detected
usbserial.c: Keyspan PDA converter now attached to ttyUSB0 \
            (or usb/tts/0 for devfs)
usbserial.c: USB Serial support registered for Keyspan PDA  -  (prerenumeration)
usbserial.c: USB Serial support registered for Xircom PGS - (prerenumeration)
usbserial.c: USB Serial support registered for Enrega PGS - (prerenumeration)
keyspan_pda.c: USB Keyspan PDA Converter driver v1.1
```

### Configuring a Fax Modem

Linux should recognize and configure a designated serial port (such as `/dev/ttyUSBX` in the example) when the device is plugged in. Fedora also comes with a number of fax utilities that can be used to configure a system to send or receive phone faxes. One of the easier-to-configure fax utilities is the `fax` command. As root, you can configure the software by editing a few entries in the `/usr/bin/fax` shell script:

```
DEV=modem
FROM="1 555 555-1212"
NAME="Company Name"
```

The most important entry is `DEV=`, which will not need to be changed as long as `/dev/modem` points to an active fax-capable modem. You can also edit `/usr/bin/fax` to customize other entries, such as the fax viewing command. Use the `test` command-line option to check the settings like this:

```
# fax test
```

Sending a fax using the `fax` command is straightforward:

```
# fax send 5551212 document.txt
```

### Configuring minicom for Modem Use

Use the `minicom` or `xminicom` script (used for launching `minicom` in a terminal window during an X session) for dial-up connections and terminal sessions to remote Linux systems. To configure this terminal program for use with an attached modem, start the client as root with its `-s` or setup option like this:

```
# minicom -s
```

After you press Enter, you will see a setup dialog. Select Serial-Port Configuration and press Enter. You will then see a Configuration Settings dialog as shown in Figure 4.8 that you can use to configure the program to work with an attached modem.
