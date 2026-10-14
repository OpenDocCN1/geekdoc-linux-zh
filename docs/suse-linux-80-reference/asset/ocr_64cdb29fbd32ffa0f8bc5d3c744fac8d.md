Test the accessibility of the USB printer as user root by entering
`echo -en "\rHello\r\f" >/dev/usb/lp0`. Provided that a printer is connected to the first USB port `/dev/usb/lp0` and can print ASCII text, the output should be a page with the word Hello.

At times, the USB printer can no longer be accessed, such as cases when the USB plug is pulled while printing. You normally only need to use these commands to restart the USB system:

```
earth:  # rchotplug stop
earth:  # rchotplug start
```

If this does not help, all processes accessing `/dev/usb/lp0` need to be terminated. Then the kernel modules for the USB printer must be unloaded and reloaded. First, find out which USB modules (`usb-uhci`, `usb-ohci`, or `uhci`) are loaded and whether further module dependencies exist with the command `lsmod`.

```
usbcore  ...  [printer usb-uhci]
```

This indicates that the module usbcore is required by the printer and usb-uhci modules. In a case like this, the printer and usb-uhci modules must be unloaded before usbcore.

Enter the following commands as user root. Depending on your system, you may have to substitute usb-uhci with usb-ohci or uhci:

```
earth:  # fuser -k /dev/usb/lp0
earth:  # rchotplug stop
earth:  # rmmod printer
earth:  # rmmod usb-uhci
earth:  # umount usbdevfs
earth:  # rmmod usbcore
earth:  # modprobe usbcore
earth:  # mount usbdevfs
earth:  # modprobe usb-uhci
earth:  # modprobe printer
earth:  # rchotplug start
```

# Serial Ports

The *LPRng Howto* in `file:/usr/share/doc/packages/lprng/LPRng-HOWTO.html`, particularly the file `/usr/share/doc/packages/lprng/LPRng-HOWTO.html#SECERIAL` section, and the man page for `printcap` (man printcap) describe how to operate a printer using an LPRng spooler on the serial port.

Here, you will find additional indications for BSD and plp spoolers.