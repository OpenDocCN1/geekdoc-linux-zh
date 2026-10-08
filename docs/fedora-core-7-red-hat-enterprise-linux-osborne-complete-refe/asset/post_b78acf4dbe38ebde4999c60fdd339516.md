
## /proc 设备信息文件

| File | Description |
|---|---|
| **/proc/devices** | Lists the device drivers configured for the currently running kernel |
| **/proc/dma** | Displays the DMA channels currently used |
| **/proc/interrupts** | Displays the IRQs (interrups) in use |
| **/proc/loports** | Shows the I/O ports in use |
| **/proc/pci** | Lists PCI devices |
| **/proc/asound** | Lists sound devices |
| **/proc/ide** | Directory for IDE devices |
| **/proc/net** | Directory for network devices |

**TABLE 32-2** *Proc Device Information Files*

which lists all your PCI devices, and **sound**, which lists all your sound devices. The **sound** file lists detailed information about your sound card. Several subdirectories, such as **net**, **ide**, and **scsi**, contain information files for different devices. Certain files hold configuration information that can be changed dynamically, such as the IP packet forwarding capability and the maximum number of files. You can change these values with the sysctl tool (Kernel Tuning in the System Tools menu) or by manually editing certain files. Table 32-2 lists several device-related */proc* files (see Chapter 32 for other entries).

## udev: 设备文件

Devices are now treated as *hotplugged*, meaning they can be easily attached and removed. Their configuration is dynamically detected and does not rely on manual administrative settings. The hotplug tool used to detect device files is udev, user devices. Each time your system is booted, udev will automatically detect your devices and generate device files for them in the */dev* directory. This means that the */etc/udev* directory and its files are recreated each time you boot. It is a dynamic directory, no longer static. udev uses a set of rules to direct how device files are to be generated, including any corresponding symbolic links. These are located in the */etc/udev/rules.d* file. You can find out more about udev at www.kernel.org/pub/linux/utils/kernel/hotplug/udev.html and docs.fedoraproject.org/udev.

As part of the hotplug system, udev will automatically detect kernel devices that are added or removed from the system. When the device interface is first created, its corresponding **sysfs** file is located and read, determining any additional attributes such as serial numbers and device major and minor numbers that can be used to uniquely identify the device. These can be used as keys in udev rules to create the device interface. Once the device is created, it is listed in the udev database, which keeps track of currently installed devices.

If a device is added, udev is called by hotplug. It checks the sysfs file for that device for the major and minor numbers, if provided. It then uses the rules in its rules file to create the device file and any symbolic links to create the device file in */dev*, with permissions specified for the device in the udev permissions rules. Once the device file is created, udev runs the programs in */etc/dev.d*.

> **NOTE** *When the system starts, it invokes* `/sbin/udevstart`, *which runs udev and creates all the kernel devices making device files in the* `/dev` *directory.* `udevstart` *is first run by initrd and then again by* `rc.sysinit` *to simulate a hotplug process on system startup.*

As `/etc/dev` is now dynamic, any changes you would make manually to the `/etc/dev` directory will be lost when you reboot. This includes the creation of any symbolic links such as `/dev/cdrom` that many software applications use. Instead, such symbolic links have to be configured udev rules files located in the `/etc/udev/rules.d` directory. Default rules are already in place for symbolic links, but you can create rules to add your own.

## udev 配置

The configuration file for udev is `/etc/udev/udev.conf`. Here are set global udev options such as the location of the udev database; the defaults for device permissions, owner, and group; and the location of udev rules files. The udev tool uses the udev `rules.d` file to dynamically create your device files. Be very careful in making any changes, particularly to rules file locations. Support for all devices on your system relies on these rules. The default `udev.conf` file is shown here:

```text
# udev.conf
# The main config file for udev
#
# This file can be used to override some of udev's default values
# for where it looks for files, and where it places device nodes.
#
# WARNING: changing any value can cause serious system breakage!

# udev_root - where in the filesystem to place the device nodes
udev_root="/dev/"

# udev_db - The name and location of the udev database.
udev_db="/dev/.udev.tdb"

# udev_rules - The name and location of the udev rules file
udev_rules="/etc/udev/rules.d/"

#udev_permissions - The name,location of the udev permission file
udev_permissions="/etc/udev/permissions.d/"

# default_mode - set the default mode for all nodes that have no
# explicit match in the permissions file
default_mode="0600"

#default_owner - set the default owner for all nodes that have no
# explicit match in the permissions file
default_owner="root"

#default_group - set the default group for all nodes that have no
# explicit match in the permissions file
default_group="root"

# udev_log - set to "yes" if you want logging, else "no"
udev_log="no"
```

The location of the device files directory is set by **udev_root** to /dev. This is the official device directory on Linux systems and should never be changed. The **udev_rules** file specifies where the rules files that udev uses to generate the device files are located. The **udev_log** option lets you turn logging on and off, useful for detecting errors. The **udev_permissions** option specifies the location of the permission files that hold the permissions to be applied to certain devices. Default permissions are already listed for you. In the case where a device has no permission listed in a permission file, then the defaults set by **default_mode**, **default_owner** and **default_group** are used. These function more like fail-safes. A device permission should be set in a udev permission file.

## 设备名称与 udev 规则: /etc/udev/rules.d

The name of a device file is designed to reflect the task of the device. Printer device files begin with lp for “line print.” Because you could have more than one printer connected to your system, the particular printer device files are distinguished by two or more numbers or letters following the prefix lp, such as lp0, lp1, lp2. The same is true for terminal device files. They begin with the prefix tty, for “teletype,” and are further distinguished by numbers or letters such as tty0, tty1, tty50, and so on. You can obtain a complete listing of the current device filenames and the devices for which they are used from the kernel.org web site at [www.kernel.org/pub/linux/docs/device-list/devices.txt](http://www.kernel.org/pub/linux/docs/device-list/devices.txt).

With udev, device names are determined dynamically by rules listed in the udev rules files. These are located in /etc/udev/rules.d. The rules files that you will find in this directory are generated by your system during installation. You should never edit them. If you need to add rules of your own, you should create your own rule file. The rules files are named, beginning with a number to establish priority. They are read sequentially, with the first rules overriding any conflicting later ones. All rules files have a .rules extension. The primary rules file is 50-udev.rules. Here you will find the rules for most of your system devices. Other rules files may be set up for more specialized devices like 60-rules-libsane for scanners, 60-rules-libbmp for music players, 60-pcmcia.rules for PCMCIA devices, and 90-alsa.rules for the sound driver.

The rules files already present in the rules.d directory have been provided for your Fedora distribution and are designed specifically for it. You should never modify these rules. To customize your setup, create your own separate rules files in /etc/udev/rules.d. In your rules file you would normally define only symlinks, using SYMLINK fields alone, as described in the following sections. These set up symbolic links to devices, letting you access them with other device names. NAME fields are used to create the original device interface, a task usually left to udev itself.

Each line maps a device attribute to a device name, as well as specifying any symbolic names (links). Attributes are specified using keys, of which there may be more than one. If all the keys match a device, then the associated name is used for it and a device file of that name will be generated. Instead of listing a device name, a program or script may be specified instead to generate the name. This is often the case for DVD/CD-ROM devices, where the device name could be a dvdwriter, cddiriter, cdrom, or dvdrive.

The rules consist of a comma-separated list of fields. A field consists of a field name and its assigned value. The udev fields are listed in Table 32-3. Check the udev Man page for detailed descriptions.
