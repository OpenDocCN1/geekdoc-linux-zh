
Linux creates network interfaces in memory when the kernel recognizes that a NIC or other network device is attached to the system. These interfaces are unlike other Linux interfaces, such as serial communications ports, and do not have a corresponding device file in the /dev directory. Unless support for a particular NIC is built in to your kernel, Linux must be told to load a specific kernel module to support your NIC. More than 100 such modules are located in the /lib/modules/2.6.XX-XX/kernel/net directory (where XX-XX is your version of the kernel).

You can initialize a NIC in several ways when using Linux. When you first install Ubuntu, automatic hardware probing detects and configures your system to use any installed NICs. If you remove the original NIC and replace it with a different make and model, your system will not automatically detect and initialize the device unless you configure Ubuntu to use automatic hardware detection when booting. Ubuntu should detect the absence of the old NIC and the presence of the new NIC at boot time.

If you do not use automatic hardware detection and configuration, you can initialize network hardware by

- Manually editing the /etc/modprobe.conf file to prompt the system to recognize and support the new hardware upon reboot
- Manually loading or unloading the new device's kernel module with the modprobe command

The following sections explain the first and last of the preceding methods.

## Editing the /etc/modprobe.conf File

This file may not be present when you first look for it, so you may need to create a blank file in a text editor. You can manually edit the /etc/modprobe.conf file to add a module dependency entry (also known as a directive) to support a new NIC or other network device. This entry includes the device's name and its corresponding kernel module. After you add this entry, the Linux kernel recognizes your new networking hardware upon reboot. Ubuntu runs a module dependency check upon booting.

For example, if your system uses a RealTek NIC, you could use an entry like this:

```
alias eth0 8139too
```

The example entry tells the Linux kernel to load the 8139too.o kernel module to support the eth0 network device. On the other hand, if you have an Intel Ethernet Pro NIC installed, you would use an entry like this:

```
alias eth0 eeprom100
```

Other parameters can be passed to a kernel module using one or more option entries, if need be, to properly configure your NIC. See the modprobe.conf man page for more information on using entries. For more specifics regarding NIC kernel modules, examine the module's source code because no man pages exist (a good opportunity for anyone willing to write the documentation).

## Using modprobe to Manually Load Kernel Modules

You do not have to use an /etc/modprobe.conf entry to initialize kernel support for your new network device. As root (using sudo), you can manually load or unload the device’s kernel module using the modprobe command, along with the module’s name. For example, use the following command line to enable the example RealTek NIC:

```
$ sudo modprobe 8139too
```

After you press Enter, you will see this device reported from the kernel’s ring buffer messages, which can be displayed by the dmesg command. Here’s a portion of that command’s output:

```
$ dmesg
...
eth0: RealTek RTL8139 Fast Ethernet at 0xce8ee000, 00:30:1b:0b:07:0d, IRQ 11
eth0: Identified 8139 chip type 'RTL-8139C'
eth0: Setting half-duplex based on auto-negotiated partner ability 0000.
...
```

Note that at this point, an IP address or other settings have not been assigned to the device. Linux can use multiple ethernet interfaces, and the first ethernet device will be numbered eth0, the second eth1, and so on. Each different ethernet device recognized by the kernel might have additional or different information reported, depending on its kernel module. For example,

```
$ dmesg
...
eep100:cv:1.09j-t 9/29/99 Donald Becker http://cesdis.gsfc.nasa.gov/linux/drivers/eep100.html
eep100.c: $Revision: 1.36 $ 2000/11/17 Modified by Andrey V. Savochkin <saw@saw.sw.com.sg> and others
PCI: Found IRQ 10 for device 00:d0.0
eth0: Intel Corporation 82557 [Ethernet Pro 100], 00:90:27:91:92:B5, IRQ 10.
 Board assembly 721383-007. Physical connectors present: RJ45
 Primary interface chip i82555 PHY #1.
 General self-test: passed.
 Serial sub-system self-test: passed.
 Internal registers self-test: passed.
```
