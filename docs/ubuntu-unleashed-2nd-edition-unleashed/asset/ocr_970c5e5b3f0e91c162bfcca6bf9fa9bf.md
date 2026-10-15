# TIP

Linux kernel and network tools can be used to diagnose problems or troubleshoot problematic NICs. However, if you browse to Don Becker's Linux Ethercard Status, Diagnostic and Setup Utilities page at http://www.scyd.com/ethercard_diag.html, you will find more than two dozen hardware-specific utilities for a variety of PCI and legacy ISA Ethernet network cards. These tools can be extremely helpful if you run into trouble during NIC recognition or configuration.

# Using modprobe to Manually Load Kernel Modules

You do not have to use an /etc/modprobe.conf entry to initialize kernel support for your new network device. As root (using sudo), you can manually load or unload the device's kernel module using the modprobe command, along with the module's name. For example, use the following command line to enable the example RealTek NIC:

```
$ sudo modprobe 8139too
```

After you press Enter, you will see this device reported from the kernel's ring buffer messages, which can be displayed by the dmesg command. Here's a portion of that command's output:

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
eeprom100.c:v1.09j-t 9/29/99 Donald Becker http://cesdis.gsfc.nasa.gov/linux/
->drive
rs/eeprom100.html
eeprom100.c: $Revision: 1.36 $ 2000/11/17 Modified by Andrey V. Savochkin <sav@saw
->.sw.com.sg> and others
PCI: Found IRQ 10 for device 00:0d.0
eth0: Intel Corporation 82557 [Ethernet Pro 100], 00:90:27:91:92:B5, IRQ 10.
Board assembly 721383-007, Physical connectors present: RJ45
Primary interface chip i82555 PHY #1.
General self-test: passed.
Serial sub-system self-test: passed.
```