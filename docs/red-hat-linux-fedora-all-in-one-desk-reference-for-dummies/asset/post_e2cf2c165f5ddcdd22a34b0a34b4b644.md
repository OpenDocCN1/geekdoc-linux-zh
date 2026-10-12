
## Chapter 5: Managing Devices and Printers

### In This Chapter

- Understanding device drivers
- Managing loadable driver modules
- Managing USB devices
- Managing print queues

Everything you use to work with your computer is a device. The keyboard and mouse you use to type and click around, the hard drive where you store everything, and the printer where you get your hard copies — these are all devices. And guess what — you have to manage them. It's not as hard as it sounds. All you have to do is load the device driver and (perhaps) configure the device a bit. This managing is easier to do if you understand device drivers a bit and get some practice using the tools Red Hat Linux includes to help you manage devices. In this chapter, I provide a brief overview of device drivers and explain how to manage driver modules. Because printers are a common type of device you have to manage, I also show you how to manage print queues.

### Understanding Device Drivers

The Linux kernel treats all devices as files and uses a device just as it would use a file — opens it, writes data to it, reads data from it, and closes it when done. This ability to treat every device as a file comes through the use of device drivers. A device driver is a special program that controls a particular type of hardware. When the kernel writes data to the device, the device driver does whatever is appropriate for that device. For example, when the kernel writes data to the floppy drive, the floppy device driver puts that data onto the physical medium of the floppy disk. On the other hand, if the kernel writes data to the parallel port device, the parallel-port driver sends the data to the printer connected to the parallel port.

Thus, the device driver isolates the device-specific code from the rest of the kernel and makes a device look like a file. Any application can access a device by opening the file specific to that device. Figure 5-1 illustrates this concept of a Linux device driver.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_507_0.png)

Figure 5-1:
An application can access a device through a special file that, in turn, uses a device driver.

### Device files

As Figure 5-1 shows, applications can access a device as if it were a file. These files are special files called device files, and they appear in the /dev directory in the Red Hat Linux file system.

If you use the ls command to look at the list of files in the /dev directory, you'll see several thousand files. This does not mean that your system has several thousand devices. The /dev directory has files for all possible types of devices — that's why the number of device files is so large.

So how does the kernel know which device driver to use when an application opens a specific device file? The answer is in two numbers called the major and minor device numbers. Each device file is mapped to a specific device driver through these numbers.

To see an example of the major and minor device numbers, type the following command in a terminal window:

```
ls -l /dev/hda
```

You should see a line of output similar to the following:

```
brw-rw---- 1 root disk 3, 0 Jul 23 14:50 /dev/hda
```

In this case, the major and minor device numbers appear just before the date. In this case, the major device number is 3 and the minor device number is 0. The kernel selects the device driver for this device file by using the major device number.

You don't really have to know much about the device files and the device numbers, except to be aware of their existence.

### Block devices

The first letter in the listing of a device file also provides an important clue. For the /dev/hda device, the first letter is a b, which indicates that /dev/hda is a block device — one that can accept or provide data in chunks (typically 512 bytes or 1KB). By the way, /dev/hda refers to the first IDE hard drive on your system (the C drive in Windows). Hard drives, floppy drives, and CD-ROM drives are all examples of block devices.

### Character devices

If the first letter in the listing of a device file is a c, then the device is a character device — one that can receive and send data one character (one byte) at a time. For example, the serial ports and parallel port are character devices. To see the specific listing of a character device, type the following command in a terminal window:

```
ls -l /dev/ttyS0
```

The listing of this device should be similar to the following:

```
crw-rw--- 1 root uucp 4, 64 Jul 23 14:50 /dev/ttyS0
```

Notice that the very first letter is a c because /dev/ttyS0 — the first serial port — is a character device.

### Network devices

Network devices that enable your system to interact with a network — for example, Ethernet and dial-up point-to-point protocol (PPP) connections — are somewhat special because they need no file to correspond to the device. Instead, the kernel uses a special name for the device. For example, the Ethernet devices are named eth0 for the first Ethernet card, eth1 for the second one, and so on. PPP connections are named ppp0, ppp1, and so on.

Because network devices aren't mapped to device files, there are no files corresponding to these devices in the /dev directory.

### Managing Loadable Driver Modules

To use any device, the Linux kernel must contain the driver. If the driver code is linked into the kernel as a monolithic program (a program that's in the form of a single large file), then adding a new driver means rebuilding the kernel with the new driver code. Rebuilding the kernel means you have to reboot the PC with the new kernel before you can use the new device driver. Luckily, the Linux kernel uses a modular design that does away with rebooting hassles. Linux device drivers can be created in the form of modules that the kernel can load and unload without having to restart the PC.

Driver modules are one type of a broader category of software modules called Loadable Kernel Modules. Other types of kernel modules include code that can support new types of file systems, modules for network protocols, and modules that interpret different formats of executable files.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_509_0.png)

### Loading and unloading modules

You can manage the loadable device driver modules by using a set of commands. You have to log in as root to use some of these commands. In Table 5-1, I summarize a few of the commonly used module commands.

Table 5-1 Commands to Manage Kernel Modules

| This Command | Does the Following |
|---|---|
| insmod | Inserts a module into the kernel |
| rmmod | Removes a module from the kernel |
| depmod | Determines interdependencies between modules |
| ksyms | Displays a list of symbols along with the name of the module that defined the symbol |
| lsmod | Lists all currently loaded modules |
| modinfo | Displays information about a kernel module |
| modprobe | Inserts or removes a module or a set of modules intelligently (for example, if module A requires B, then modprobe automatically loads B when asked to load A) |

If you have to use any of these commands, log in as root or type su - in a terminal window to become root.

To see what modules are currently loaded, type

```
lsmod
```

You should see a list of modules. For example, here is a list on one of my PCs:

```
Module Size Used by Not tainted
nls_iso8859-1 3516 1 (autoclean)
nls_cp437 5148 1 (autoclean)
sd_mod 13516 2 (autoclean)
vfat 13036 1 (autoclean)
fat 38808 0 (autoclean) [vfat]
usb-storage      74560  1 [sd_mod usb-storage]
scsi_mod        107576  2 [sd_mod usb-storage]
ide-cd          35712  0 (autoclean)
cdrom           33728  0 (autoclean) [ide-cd]
parport_pc      19076  1 (autoclean)
lp              9060   0 (autoclean)
parport         37056  1 (autoclean) [parport_pc lp]
iptables_filter 2444   0 (autoclean) (unused)
ip_tables       15224  1 [iptables_filter]
autofs          13268  0 (autoclean) (unused)
orinoco_cs      5556   1
orinoco         39724  0 [orinoco_cs]
hermes          8100   0 [orinoco_cs orinoco]
ds              8680   1 [orinoco_cs]
yenta_socket    13664  1
pcmcia_core     57248  0 [orinoco_cs ds yenta_socket]
3c59x           30736  0
floppy          56892  0 (autoclean)
keybdev         2976   0 (unused)
mousedev        5556   1
hid             22276  0 (unused)
input           5888   0 [keybdev mousedev hid]
usb-uhci        26412  0 (unused)
usbcore         79136  1 [usb-storage hid usb-uhci]
ext3            73340  2
jbd             52148  2 [ext3]
```

As you may expect, the list of modules depends on the types of devices installed on your system.

The first column lists the names of the modules in last-to-first order. Thus, the first module in the list is the last one to be loaded. The Size column shows the number of bytes that the module occupies in your PC's memory. The remaining columns show other information about each module, such as how many applications are currently using the module and the names of the modules that require the module.

The list displayed by `lsmod` includes all types of Linux kernel modules, not just device drivers. For example, the last two modules — `jbd`, and `ext3` — are all part of the EXT3 file system (the latest file system for Linux).

![](img/a7eec43a54473e95dc5ea333fecf1bd7_510_0.png)

Besides `lsmod`, one commonly used module command is `modprobe`. Use `modprobe` whenever you need to manually load or remove one or more modules. The best thing about `modprobe` is that you don't need to worry if a module requires other modules to work. The `modprobe` command automatically loads any other module that is needed by a module. On my system, for example, I can manually load the sound driver with the command

```
modprobe sound-slot-0
```
