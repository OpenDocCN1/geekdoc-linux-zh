
![](img/a7eec43a54473e95dc5ea333fecf1bd7_511_0.png)

This command causes `modprobe` to load everything needed to make sound work. On one of my systems, the `modprobe sound-slot-0` command loads `soundcore`, `ac97_codec`, and `i810_audio` — in that order.

You can use `modprobe` with the `-r` option to remove modules. For example, to remove the sound modules, I use the following command:

```
modprobe -r sound-slot-0
```

This command gets rid of all the modules that the `modprobe sound-slot-0` command had loaded.

## Using the /etc/modules.conf file

How does the `modprobe` command know that it should load the `opl3sa2` driver module when I use a module name `sound-slot-0`? The answer is in the `/etc/modules.conf` configuration file. That file contains a line that tells `modprobe` what it should load when it sees the module name `sound-slot-0`.

To view the contents of `/etc/modules.conf`, type

```
cat /etc/modules.conf
```

On one of my Red Hat Linux PCs, the file contains the following lines:

```
alias parport_lowlevel parport_pc
alias eth0 eepro100
alias usb-controller usb-uhci
alias sound-slot-0 opl3sa2
```

Each line that begins with the keyword `alias` defines a standard name for an actual driver module. For example, the second line defines `eepro100` as the actual driver name for the alias `eth0`, which stands for the first Ethernet card. Similarly, the fourth line defines `opl3sa2` as the module to load when I use the name `sound-slot-0`.

The `modprobe` command consults the `/etc/modules.conf` file to convert an alias to the real name of a driver module as well as for other tasks such as obtaining parameters for driver modules. For example, you can insert lines that begin with the `options` keyword to provide values of parameters that a driver may need.

For example, to set the interrupt request (IRQ) parameter for the sound card to 5, I would add the following line to the `/etc/modules.conf` file:

```
options opl3sa2 irq=5
```

This line specifies 5 as the value of the parameter named `irq` in the `opl3sa2` module.

If you want to know the names of the parameters that a module accepts, use the `modinfo` command. For example, to view information about the `opl3sa2` driver module, type

```
modinfo opl3sa2
```

From the resulting output, you can tell that `irq` is the name of the parameter for the Interrupt Request parameter.

Unfortunately, the information shown by the `modinfo` command can be somewhat cryptic. The only saving grace is that you may not have to do much more than use a graphical utility to configure the device, and the utility will take care of adding whatever is needed to configuration files such as `/etc/modules.conf`.

## Managing USB Devices

Red Hat Linux comes with built-in support for the Universal Serial Bus (USB) — a serial bus that's gradually replacing the functionality of the PC's serial and parallel ports, as well as that of the keyboard and mouse ports. Nowadays, many PC peripherals — such as mouse, keyboard, printer, CD burner, scanner, modem, digital camera, memory card, and so on — are designed to connect to the PC through a USB port.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_512_0.png)

USB version 1.1 supports data-transfer rates as high as 12 Mbps — 12 million bits per second or 1.5 megabytes per second — compared with 115 Kbps or the 0.115 Mbps transfer rate of a standard serial port. You can daisy-chain up to 127 devices on a single USB bus. The bus also provides power to the devices, and you can attach or remove devices while the PC is running — a capability commonly referred to as hot plug or hot swap. USB version 2.0 (or USB 2.0 or USB2, for short) ups the ante by raising the data transfer rates to a whopping 480 Mbps, slightly faster than the competing IEEE 1394 (FireWire) bus. Nowadays many devices, such as CD burners and scanners, come with the high-speed USB2 interface. If your PC has older USB 1.1 ports, the USB2 devices can still work, albeit at lower data-transfer rates. Red Hat Linux supports both USB 1.1 and USB2 interfaces.

Using USB devices in Red Hat Linux is easy. You can hot-plug a device into a USB port, and the Linux kernel can detect and load the appropriate device drivers so applications can make use of the device. To be more precise, the `kudzu` hardware detection utility takes care of the chores necessary to make the USB device accessible to applications. For USB mass storage devices, such as CD drives or hard drives, `kudzu` can also mount the device on the Linux file system. For examples of using USB mass-storage devices, see Book II, Chapter 5 where I discuss how Red Hat Linux detects a USB CD burner and how to access the photos in a digital camera through the USB interface.

To use a USB printer in Red Hat Linux, simply connect the printer to the USB port, power it up, and then follow the steps in Book I, Chapter 3 to configure a locally connected queue for the printer. The printer should show up with a device name such as /dev/usb/lp0 (for the USB printer detected by kudzu), /dev/usb/lp1 (for the second USB printer), and so on.

Using USB scanners in Red Hat Linux is as simple as using USB printers. Just plug the scanner into the USB port, power it up, and you should be able to access it by using the xsane — a graphical front-end for scanners that you can start by choosing Main Menu→Graphics→Scanning. Of course, the USB scanner make and model must be supported by xsane. To quickly check whether kudzu has detected your USB scanner, log in as root and type sane-find-scanner in a terminal window.

Even when kudzu does not automatically mount a USB mass storage device for easy access, you can manually mount the device. Consider, for example, the USB keychain storage device. Just as the name says, these are small memory cards, capable of storing anywhere from 32MB to 1GB. You can carry them around on a keychain — in effect, taking all your data with you wherever you go. Here's how you can use a USB keychain storage device that's already formatted for use in Microsoft Windows:

- **1. Plug the keychain storage device into the PC's USB port.**

Sometimes the device plugs directly into the port, but for some devices you have to attach the keychain device to a USB cable and then plug the cable into the USB port.

Some USB keychain devices have a small switch on the side that controls whether the keychain is write-protected. If you plan to write to the device, first make sure it's not write-protected or locked.

- **2. Create a mount point for the storage device. For example, I log in as root and create the following directory:**

```
mkdir /mnt/key
```

- **3. If this is the only USB device plugged in, the device name is /dev/sda1 (USB storage devices appear as SCSI devices). Mount it with the following command:**

```
mount -o rw -t vfat /dev/sda1 /mnt/key
```

The -t vfat part of the command specifies that the file system on the keychain storage device is VFAT — the Windows file system that supports long filenames.

Now you can access the files on the keychain at the /mnt/key directory. To save a file to the USB keychain storage device, use a command of the following form:

```
cp filename /mnt/key
```

where filename is the name of the file you want to save.

When you're done using the device, unmount the USB keychain with this command:

```
umount /dev/sda1
```

That's it!

## Managing Print Queues in Red Hat Linux

PCs typically come with one parallel port, typically used for connecting the printer to the PC. You can set up a printer fairly easily by using Red Hat's graphical printer-configuration utility, but you also have to learn how to manage the print queue.

### Spooling and print jobs

Spooling refers to the capability to print in the background. When you print from a word processor in Windows, for example, the output first goes to a file on the disk. Then, while you continue working with the word processor, a background process sends that output to the printer. The Red Hat Linux printing environment also supports spooling.

Print job refers to what you print with a single print command. The printing environment queues print jobs by storing them in the spool directory. A background process periodically sends the print jobs from the spool directory to the printer.

Red Hat Linux uses the Common UNIX Printing System (CUPS) for its printing environment. CUPS is a printing system based on the Internet Printing Protocol (IPP) — a protocol for distributed printing using Internet technologies. IPP assumes a client/server model with the client being an application and the server a "Printer" — an abstraction of an output device or a printing service provider. IPP supports a distributed printing environment with the clients and Printer servers communicating over the Internet. You could use an IPP client to print on a printer anywhere on the Internet. The client and Printer exchange data using the HTTP 1.1 protocol — the
