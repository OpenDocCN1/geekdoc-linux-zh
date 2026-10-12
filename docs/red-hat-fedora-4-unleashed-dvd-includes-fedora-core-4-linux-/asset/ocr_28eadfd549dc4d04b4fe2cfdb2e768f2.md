In this example, the characteristics of /dev/ttyS0 are displayed. The setserial command can also be used to configure or fine-tune a port's characteristics using 32 different command-line options and values.

One option for using a legacy serial device such as a modem on PC that does not have a serial port but supports USB is to use a USB-to-serial converter. These devices provide a serial port dongle and plug in to a USB hub or port. You can see the output and designated serial port by looking at the output of the dmesg command:

```
usb.c: registered new driver serial
usbserial.c: USB Serial support registered for Generic
usbserial.c: USB Serial Driver core v1.4
usbserial.c: USB Serial support registered for Keyspan PDA
usbserial.c: Keyspan PDA converter detected
usbserial.c: Keyspan PDA converter now attached to ttyUSB0 \
(or usb/tts/0 for devfs)
usbserial.c: USB Serial support registered for Keyspan PDA - (prenumeration)
usbserial.c: USB Serial support registered for Xircom PGS - (prenumeration)
usbserial.c: USB Serial support registered for Entegra PGS - (prenumeration)
keyspan_pda.c: USB Keyspan PDA Converter driver v1.1
```

# ### Configuring a Fax Modem

Linux should recognize and configure a designated serial port (such as /dev/ttyUSBX in the example) when the device is plugged in. Fedora also comes with a number of fax utilities that can be used to configure a system to send or receive phone faxes. One of the easier to configure fax utilities is the fax command. As root, you can configure the software by editing a few entries in the /usr/bin/fax shell script:

```
DEV=modem
FROM="1 555 555-1212"
NAME="Company Name"
```

The most important entry is DEV=, which will not need to be changed as long as /dev/modem points to an active fax-capable modem. You can also edit /usr/bin/fax to customize other entries, such as the fax viewing command. Use the test command-line option to check the settings like this:

```
# fax test
```

Sending a fax using the fax command is straightforward:

```
# fax send 5551212 document.txt
```

# ### Configuring minicom for Modem Use

Use the minicom or xminicom script (used for launching minicom in a terminal window during an X session) for dial-up connections and terminal sessions to remote Linux