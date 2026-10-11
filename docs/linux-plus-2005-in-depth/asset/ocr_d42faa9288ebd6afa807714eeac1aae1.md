(section 1 of the manual pages) is displayed. To display the manual page for the whowami file format instead, you simply type `man 5 whowami` to display the whowami file format (section 5 of the manual pages).

Recall that many commands are available to the Linux user; thus, it might be cumbersome to find the command that you need to perform a certain task without using a Linux command dictionary. Fortunately, you have the ability to search the manual pages by keyword. To find all of the commands that have the word “usb” in their name or description, type the following:

```
```
[root@server1 root]# man -k usb
```
```

This command produces the following output:

energizerups | (8) | - Driver for Energizer (Megatec protocol) over USB to RS232 Interface (V1.0) BaudRate 2400bps) UPS equipment | fxlload | (8) | - Firmware download to EZ-USB devices | lsusb | (8) | - List all USB devices | sane-canon630u | (5) | - SANE backend for the Canon 630u USB flatbed scanner | sane-find-scanner | (1) | - find SCSI and USB scanners and their device files | sane-gt68xx | (5) | - SANE backend for GT-68XX based USB flatbed scanners | sane-ma1509 | (5) | - SANE backend for Mustek BearPaw 1200F USB scanner | sane-mustek_usb | (5) | - SANE backend for Mustek USB flatbed scanners | sane-plustek | (5) | - SANE backend for Plustek parallel port and LM983(1/2/3) based USB flatbed scanners | sane-sm3600 | (5) | - SANE backend for Microtek scanners with M011 USB chip | sane-usb | (5) | - USB configuration tips for SANE | usbmodules | (8) | - List kernel driver modules available for a plugged in USB device

```
```
[root@server1 root]#
```
```

After you find the command needed, you can simply run the `man` command on that command without the `-k` option to find out detailed information about the command.

# NOTE

> > You can also use the `apropos` usb command to perform the same function as the `man -k` usb command. Both commands yield the exact same output on the terminal screen.

> > If you do not see any output from the `man -k` or `apropos` commands following a Linux installation, you might need to run the `makewhatis` command to index the manual page database.