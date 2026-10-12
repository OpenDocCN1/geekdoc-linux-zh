The *modprobe* command consults the /etc/modprobe.conf file to convert an alias to the real name of a driver module as well as for other tasks, such as obtaining parameters for driver modules. For example, you can insert lines that begin with the *options* keyword to provide values of parameters that a driver may need.

For example, to set the debug level parameter for the Ethernet driver to 5 (this parameter generates lots of information in /var/log/messages), I add the following line to the /etc/modprobe.conf file:

```
options 3c59x debug=5
```

This line specifies *5* as the value of the parameter named *debug* in the *3c59x* module.

If you want to know the names of the parameters that a module accepts, use the *modinfo* command. For example, to view information about the *3c59x* driver module, I type

```
modinfo 3c59x | more
```

From the resulting output, I can tell that *debug* is the name of the parameter for setting the debug level.

Unfortunately, the information shown by the *modinfo* command can be somewhat cryptic. The only saving grace is that you may not have to do much more than use a graphical utility to configure the device, and the utility takes care of adding whatever is needed to configuration files, such as /etc/modprobe.conf.

# ## Managing USB Devices

Fedora Core comes with built-in support for the Universal Serial Bus (USB) — a serial bus that’s gradually replacing the functionality of the PC’s serial and parallel ports, as well as that of the keyboard and mouse ports. Nowadays, many PC peripherals — such as mouse, keyboard, printer, CD burner, scanner, modem, digital camera, memory card, and so on — are designed to connect to the PC through a USB port.

USB version 1.1 supports data-transfer rates as high as 12 Mbps — 12 million bits per second or 1.5MB per second — compared with 115 Kbps or the 0.115 Mbps transfer rate of a standard serial port. You can daisy chain up to 127 devices on a single USB bus. The bus also provides power to the devices, and you can attach or remove devices while the PC is running — a capability commonly referred to as *hotplug* or *hot swap*. USB version 2.0 (or USB 2.0 or

![](bbox=[0.15, 0.82, 0.22, 0.88])