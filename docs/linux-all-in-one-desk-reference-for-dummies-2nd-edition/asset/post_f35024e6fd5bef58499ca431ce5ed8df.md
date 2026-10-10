
## Understanding Linux Devices

Linux treats all devices as files and uses a device just as it uses a file — opens it, writes data to it, reads data from it, and closes it when done. This ability to treat every device as a file comes through the use of device drivers. A *device driver* is a special program that controls a particular type of hardware. When the kernel writes data to the device, the device driver does whatever is appropriate for that device. For example, when the kernel writes data to the floppy drive, the floppy device driver puts that data onto the physical medium of the floppy disk. On the other hand, if the kernel writes data to the parallel port device, the parallel port driver sends the data to the printer connected to the parallel port.

Thus the device driver isolates the device-specific code from the rest of the kernel and makes a device look like a file. Any application can access a device by opening the file specific to that device. Figure 1-7 illustrates this concept of a Linux device driver.

![](img/792720823146d68f19fd50c99ebfce4b_426_0.png)

### Device files

As Figure 1-7 shows, applications can access a device as if it were a file. These files are special files called *device files*, and they appear in the `/dev` directory in the Linux file system.

If you use the `ls` command to look at the list of files in the `/dev` directory, you see several thousand files. These files do not mean that your system has several thousand devices. The `/dev` directory has files for all possible types of devices — that’s why the number of device files is so large.

So how does the kernel know which device driver to use when an application opens a specific device file? The answer is in two numbers called the *major* and *minor device numbers*. Each device file is mapped to a specific device driver through these numbers.

To see an example of the major and minor device numbers, type the following command in a terminal window:

```bash
ls -l /dev/hda
```

You see a line of output similar to the following:

```text
brw-rw---- 1 root disk 3, 0 Aug 16 14:50 /dev/hda
```

In this line, the major and minor device numbers appear just before the date. In this case, the major device number is 3 and the minor device number is 0. The kernel selects the device driver for this device file by using the major device number.

You don't really have to know much about the device files and the device numbers, except to be aware of their existence.

![](img/792720823146d68f19fd50c99ebfce4b_427_0.png)

In case you are curious, all the major and minor numbers for devices are assigned according to device type. The *Linux Assigned Names And Numbers Authority (LANANA)* assigns these numbers. You can see the current device list at `www.lanana.org/docs/device-list/devices.txt`.

### Block devices

The first letter in the listing of a device file also provides an important clue. For the `/dev/hda` device, the first letter is a **b**, which indicates that `/dev/hda` is a *block device* — one that can accept or provide data in chunks (typically 512 bytes or 1K). By the way, `/dev/hda` refers to the first IDE hard drive on your system (the C: drive in Windows). Hard drives, floppy drives, and CD-ROM drives are all examples of block devices.

### Character devices

If the first letter in the listing of a device file is a **c**, the device is a *character device* — one that can receive and send data one character (one byte) at a time. For example, the serial port and parallel ports are character devices.

To see the specific listing of a character device, type the following command in a terminal window:

```text
ls -1 /dev/ttyS0
```

The listing of this device is similar to the following:

```text
crw-rw----  1 root  uucp    4, 64 Aug 16 14:50 /dev/ttyS0
```

Notice that the very first letter is a c because `/dev/ttyS0`—the first serial port—is a character device.

### Network devices

Network devices that enable your system to interact with a network—for example, Ethernet and dialup *Point-to-Point Protocol* (PPP) connections—are somewhat special because they need no file to correspond to the device. Instead, the kernel uses a special name for the device. For example, the Ethernet devices are named `eth0` for the first Ethernet card, `eth1` for the second one, and so on. PPP connections are named `ppp0`, `ppp1`, and so on.

Because network devices aren’t mapped to device files, no files corresponding to these devices are in the `/dev` directory.

### Persistent device naming with udev

Linux kernel 2.6 introduces a new approach for handling devices, based on the following features:

- **sysfs**: Kernel 2.6 provides the `sysfs` file system that is mounted on the `/sys` directory of the file system. The `sysfs` file system shows all the devices in the system as well as lots of information about each device. The information includes location of the device on the bus, attributes such as name and serial number, and the major and minor numbers of the device.
- `/sbin/hotplug`: This program is called whenever a device is added or removed. It can then do whatever is necessary to handle the device.
- `/sbin/udev`: This program takes care of dynamically named devices based on device characteristics such as serial number, device number on a bus, or a user-assigned name based on a set of rules that are set through the text file `/etc/udev/udev.rules`.

The udev program’s configuration file is `/etc/udev/udev.conf`. Based on settings in that configuration file, udev creates device nodes automatically in the directory specified by the `udev_root` parameter. For example, to manage the device nodes in the /dev directory, udev_root should be defined in /etc/udev/udev.conf as follows:

```text
udev_root="/dev/"
```

## Managing Loadable Driver Modules

To use any device, the Linux kernel must contain the driver. If the driver code is linked into the kernel as a monolithic program (a program that's in the form of a single, large file), adding a new driver means rebuilding the kernel with the new driver code. Rebuilding the kernel means you have to reboot the PC with the new kernel before you can use the new device driver. Luckily, the Linux kernel uses a modular design that does away with reboot-ing hassles. Linux device drivers can be created in the form of modules that the kernel can load and unload without having to restart the PC.

> Driver modules are one type of a broader category of software modules called Loadable Kernel Modules. Other types of kernel modules include code that can support new types of file systems, modules for network protocols, and modules that interpret different formats of executable files.

![](img/792720823146d68f19fd50c99ebfce4b_429_0.png)

### Loading and unloading modules

You can manage the loadable device driver modules by using a set of commands. You have to log in as root to use some of these commands. In Table 3-13, I summarize a few of the commonly used module commands.

**Table 3-13 Commands to Manage Kernel Modules**

| This Command | Does the Following |
| :--- | :--- |
| `insmod` | Inserts a module into the kernel |
| `rmmod` | Removes a module from the kernel |
| `depmod` | Determines interdependencies between modules |
| `ksyms` | Displays a list of symbols along with the name of the module that defines the symbol |
| `lsmod` | Lists all currently loaded modules |
| `modinfo` | Displays information about a kernel module |
| `modprobe` | Inserts or removes a module or a set of modules intelligently. (For example, if module A requires B, then modprobe automatically loads B when asked to load A.) |

If you have to use any of these commands, log in as `root` or type `su –` in a terminal window to become `root`.

To see what modules are currently loaded, type:

```text
lsmod
```

You see a long list of modules that depend on the types of devices installed on your system.

The list displayed by `lsmod` includes all types of Linux kernel modules, not just device drivers. For example, if you use the Ext3 file system, you typically find two modules — `jbd`, and `ext3` — that are all part of the Ext3 file system (the latest file system for Linux).

![](img/792720823146d68f19fd50c99ebfce4b_430_0.png)

Besides `lsmod`, one commonly used module command is `modprobe`. Use `modprobe` whenever you need to manually load or remove one or more modules. The best thing about `modprobe` is that you don't need to worry if a module requires other modules to work. The `modprobe` command automatically loads any other module needed by a module. On one of my systems, for example, I manually load the sound driver with the command:

```text
modprobe snd-card-0
```

This command causes `modprobe` to load everything needed to make sound work.

![](img/792720823146d68f19fd50c99ebfce4b_430_1.png)

You can use `modprobe` with the `-r` option to remove modules. For example, to remove the sound modules, I use the following command:

```text
modprobe -r snd-card-0
```

This command gets rid of all the modules that the `modprobe snd-card-0` command had loaded.

### Using the /etc/modprobe.conf file

How does the `modprobe` command know that it needs to load the `snd-intel8x0` driver module when I use a module name `snd-card-0`? The answer is in the `/etc/modprobe.conf` configuration file. That file contains a line that tells `modprobe` what it should load when it sees the module name `snd-card-0`.

To view the contents of `/etc/modprobe.conf`, type:

```text
cat /etc/modprobe.conf
```
