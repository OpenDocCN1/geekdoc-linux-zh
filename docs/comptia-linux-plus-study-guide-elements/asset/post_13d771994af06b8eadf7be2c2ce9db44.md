
## Managing Hardware

Most hardware manufacturers ensure that their products work properly under Windows. Some do the same for Linux, but you’re usually on your own when you use Linux. Fortunately, tools and resources exist to help with these tasks. You can check for hardware compatibility before you even buy it, using Internet resources. Once hardware is installed, Linux provides tools to help you identify that hardware and to configure it properly.

### Finding Compatible Hardware

When you shop for hardware for use on a Linux computer, you must remember that not all hardware works with Linux. Several resources exist to help in this regard:

- The **Hardware Compatibility List (HCL)** This resource, located at http://www.linuxquestions.org/hcl, is the closest thing to a comprehensive source for Linux hardware compatibility. You can use it to check on the compatibility of a specific product or to find products in a category that are known to be compatible.

- The **OpenPrinting Database** This site (http://www.linuxprinting.org/printer_list.cgi) maintains a list of printers along with comments on their compatibility with Linux.

- The **SANE Database** The Scanner Access Now Easy (SANE) project maintains a database of scanners, with information on their compatibility with the SANE software, which is the main scanner package for Linux. Check http://www.sane-project.org for more details.

- The **ALSA Project** The Advanced Linux Sound Architecture (ALSA) project maintains the mainstream Linux sound drivers. Its Web page, http://alsa-project.org, includes notes on compatibility with specific devices.

These databases are maintained by driver developers and end users. As such, they're necessarily incomplete and therefore of limited value. Even limited value is better than no value, though, so you should definitely check these sites before buying hardware or to evaluate the compatibility of hardware you already own.

Another resource you may want to consult is your hardware's manufacturer. Check both the Web site for the company that made the product and, if you know it, the company that made the chipset that drives the product. To Linux, the chipset is what's important, but the hardware's manufacturer may have information or even drivers available for download.

Broadly speaking, products that are most likely to give problems are those that include circuitry that requires specialized drivers—video cards, network cards, scanners, printers, and so on. Some products, by contrast, are extremely standardized and so seldom cause problems. Examples in this category include RAM, hard disks, CD-ROM and DVD-ROM drives, keyboards, mice, and monitors.

## Identifying Hardware in Linux

If you've installed Linux on a computer and aren't sure what hardware is available or if you've just installed a device and want to verify that it's accessible, you can use various Linux tools to help identify the hardware. Tools to identify PCI cards and USB devices exist. You can also query the kernel drivers that are loaded and examine a special directory to locate hardware information.

## Identifying PCI Devices

The Peripheral Component Interconnect (PCI) standard defines a physical and logical set of parameters that enable plug-in cards to be used in any PCI-supporting computer. PCI devices plug into the computer's motherboard or are built into the motherboard directly. In Linux, the `lspci` command displays information on PCI devices. Table 1.1 summarizes the options to this command.

**Table 1.1 Options for lspci**

| Option | Effect |
| :--- | :--- |
| -v | Increases verbosity of output. This option may be doubled (-vv) or tripled (-vvv) to produce yet more output. |
| -n | Displays information in numeric codes rather than translating the codes to manufacturer and device names. |
| -nn | Displays both the manufacturer and device names and their associated numeric codes. |
| -x | Displays the PCI configuration space for each device as a hexadecimal dump. This is an extremely advanced option. Tripling (-xxx) or quadrupling (-xxxx) this option displays information about more devices. |
| -b | Shows IRQ numbers and other data as seen by devices rather than as seen by the kernel. |
| -t | Displays a tree view depicting the relationship between devices. |
| -s [ [[domain]:]bus:] [slot][:.func] | Displays only devices that match the listed specification. |
| -d [vendor]:[device] | Shows data on the specified device. |
| -i file | Uses the specified file to map vendor and device IDs to names. (The default is /usr/share/misc/pci.ids.) |
| -m | Dumps data in a machine-readable form, intended for use by scripts. A single -m uses a backward-compatible format, whereas doubling (-mm) uses a newer format. |
| -D | Displays PCI domain numbers. These numbers normally aren't displayed. |
| -M | Performs a scan in bus-mapping mode, which can reveal devices hidden behind a misconfigured PCI bridge. This is an advanced option that can be used only by root. |
| --version | Displays version information. |

## Identifying USB Devices

Universal Serial Bus (USB) devices normally attach externally to the computer. You can check to see what USB devices are connected using the `lsusb` command, which is similar in many ways to `lspci`. Table 1.2 summarizes `lsusb` options.

**Table 1.2 Options for lsusb**

| Option | Effect |
| :--- | :--- |
| -v | Increases verbosity of output |
| -t | Displays a tree view depicting the relationship between devices |
| -s [ [bus] :[devnum] | Displays only devices that match the listed specification |
| -d [vendor] :[device] | Shows data on the specified device |
| -D device | Displays information on the specified device, which is a device file in the /dev directory tree |
| --version or -V | Displays version information |

Note that `lsusb` displays information on both the devices that are attached to your computer and on the USB controller in the computer itself.

## Identifying Kernel Drivers

Hardware in Linux is handled by kernel drivers, many of which come in the form of *kernel modules*. These are stand-alone driver files, typically stored in the `/lib/modules` directory tree, that can be loaded and unloaded to provide access to hardware. Typically, Linux loads the modules it needs when it boots, but you may need to load additional modules yourself.

You can learn about the modules that are currently loaded on your system by using `lsmod`, which takes no options and produces output like this:

```
$ lsmod
Module                 Size  Used by
isos                   35820   0
zlib_inflate           21888   1 isofs
floppy                  65200   0
nls_iso8859-1            5568   1
nls_cp437               7296   1
vfat                   15680   1
fat                    49536   1 vfat
sr_mod                 19236   0
ide_cd                 42848   0
cdrom                  39080   2 sr_mod,ide_cd
```

> The example output for `lsmod` has been edited for brevity. Although outputs this short are possible with certain configurations, they're rare.

The most important column in this output is the first one, labeled Module; this column specifies the names of all the modules that are currently loaded. You can learn more about these modules with modinfo, as described shortly, but sometimes their purpose is fairly obvious. For instance, the floppy module provides access to the floppy disk drive. All the entries have a number, which indicates the number of other modules or processes that are using the module. For instance, in the preceding example, the isofs module (used to access CD-ROM file systems) isn't currently in use, as revealed by its 0 value; but the vfat module (used to read VFAT hard disk partitions and floppies) is being used, as shown by its value of 1. If one of the modules is being used by another module, the using module's name appears in the Used by column. For instance, the isofs module relies on the zlib_inflate module, so the latter module's Used by column includes the isofs module name. This information can be useful when you're managing modules. For instance, if your system produced the preceding output, you couldn't directly remove the zlib_inflate module because it's being used by the isofs module; but you could remove the isofs module, and after doing so you could remove the zlib_inflate module. (Both modules would need to be added back to read most CD-ROMs, though.)

> **NOTE**
> The `lsmod` command displays information only about kernel modules, not about drivers that are compiled directly into the Linux kernel. For this reason, a module may need to be loaded on one system but not on another to use the same hardware because the second system may compile the relevant driver directly into the kernel.

## Using the /proc Filesystem

Linux uses a special filesystem, /proc, to control and provide information about much of the hardware on the computer. Although `lspci`, `lsusb`, `lsmod`, and some other tools provide useful information about specific subsystems, you can use /proc to obtain information on still more hardware. For instance, the /proc/scsi subdirectory hosts information on SCSI devices (as well as devices that look like SCSI devices, such as most SATA disks), /proc/cpuinfo delivers information on your CPU, and /proc/interrupts displays the interrupts used by hardware devices.

You may want to peruse your /proc filesystem to see what sorts of information it can provide. You can use the cat command to display the contents of a file, as in cat /proc/interrupts. Be aware that many of the files contained in this directory tree hold extremely technical information that may be mystifying unless you have a deep understanding of the hardware involved.

> **WARNING**
> Don't try to modify the files in /proc. Writing to these files can cause your hardware to malfunction. In extreme cases you could wipe out your Linux installation!
