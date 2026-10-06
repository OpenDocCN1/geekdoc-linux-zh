
# Chapter 15: Setting Up Network Connections and LANs 657

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_704_0.png)

Figure 15-13: The distance of obstructive objects from the wireless signal is called the clearance.

- **Distance** — Although the actual distances over which antennas can send and receive data varies greatly based on different factors, you can achieve distances of many miles with outdoor antennas. For example, two Orinco 24 dbi directional parabolic-grid antennas can theoretically achieve distances of up to 52 miles at an 11 Mbps transmission speed with a 180-meter clearance. Reduce transmission rate to 1 Mbps and you can achieve distances up to 149 miles with a 1200-meter clearance. Shorter distances are achieved with less expensive equipment, such as the Orinco 14 dbi directional antenna which can achieve distances up to 5.3 miles at 11 Mbps with a 13-meter clearance.
- **Cable factor** — The distances that transmissions travel on the cables between the wireless cards and the antennas can be a factor in choosing the right antenna. The shorter the cables, the greater the distance and speed you will get with your antenna.

The power of an antenna is rated in terms of *gain*. Gain is measured in decibels, based on a theoretic isotropic radiator (or dbi). Higher gains offer opportunities for reaching greater distances at greater speeds. However, the ability of the antenna to focus power (directional versus omnidirectional), affects the speeds and distances that can be achieved. If you want to see interesting home made antennas, search the Web for *cantenna*.

# Getting wireless drivers

If you are using a wireless card that includes a supported driver in Fedora or RHEL, the system might detect and load the proper driver, so that you will be able to configure it as described later in this section. In other cases, you will need to install the associated firmware for the driver that comes with the hardware (usually intended for Windows systems).

If the driver you need for your wireless card is not included with Fedora, you may be able to use ndiswrapper and a Windows driver to configure your wireless card. The following procedure contains an example of configuring ndiswrapper with a Linksys 802.11g wireless PCI adapter card.

# Part IV: Fedora RHEL Network and Server Setup

If you need further information about ndiswrapper, refer to the Fedora Ndiswrapper project page (ndiswrapper.sourceforge.net/).

> NOTE: Because there is now a BCM43xx driver available in Fedora, you can use the bcm43xx-fwcutter command to extract the firmware from the package to use with native Linux driver. After, a reboot should properly detect and load the modules needed for. For example, unzipping the wpc54g zip file shown in the procedure below, use the following command with the bcm51.sys file in the current directory:

```
# bcm43xx-fwcutter -w /lib/firmware/bcm51
```

If your wireless card is not working you can use ndiswrapper instead to get your wireless card working. Because Fedora will try to use the native driver instead of ndiswrapper, you may need to blacklist the driver that Fedora wants to use.

- 1. Determine if your wireless card is used by. If you have a PCI card, type:

```
# lspci -v | less
00:0a.0 Network controller: Broadcom Corporation BCM4306 802.11/g
 LAN Controller (rev 03)
Subsystem: Linksys: Unknown 0014
Flags: bus master, fast devel, latency 64, IRQ 5
Memory at ee000000 (32-bit, non-prefetchable) [size=8K]
```

In this example, the PCI card is a BCM4306 802.11/g Wireless Controller from Broadcom Corporation. (If your wireless card is a USB device, type the lsusb instead.)

- 2. Checking the list of wireless card drivers known to run under ndiswrapper, as mentioned previously.

- 3. If your card is supported, download the driver recommended. I used the Linksys WMP54GS-G PCI Adapter (which was replaced by the chipset BCM4306 802.11g, rev 03 shown in the preceding (lspci output). So I downloaded the driver as follows:

```
# mkdir wireless
# cd wireless
# wget http://ftp.linksys.com/pub/network/wpc54g_v2_driver_utility_v2.0.zip
```

- 4. After the file is downloading, unzip the driver file. For example, I typed:

```
# unzip wpc54g_v2_driver_utility_v2.0.zip
```

- 5. Install the kernel-dev and gcc packages. Then link the kernels directory to the modules directory or your current kernel (replacing <kernel-version> with the version of your kernel development package and current kernel, shown):

```
# yum install kernel-dev gcc
# ln -s /usr/src/kernels/<kernel-version> /lib/modules/<kernel-version>/build
```

# Chapter 15: Setting Up Network Connections and LANs 659

6. Get the ndiswrapper source code by downloading it to your Fedora or RHEL system from the following site: http://sourceforge.net/projects/ndiswrapper.

> NOTE: There are also ndiswrapper RPM packages available for Fedora at rpm.livna.org. If you decide to go route, instead of installing the source code, make sure that you find the ndiswrapper package that matches your kernel version. See Chapter 5 for information on enabling the rpm.livna.org repository.

7. With the ndiswrapper source code package in the current directory, unzip and untar it as follows:

```
# tar xvfz ndiswrapper*-tar.gz
```

8. As root user, change to the ndiswrapper directory and run the make command as follows:

```
# cd ndiswrapper*
# make install
```

9. Get the INF file from the unzipped driver package. From our example, the file we needed was lsbcmnds.inf. Then run the ndiswrapper -i command to install the driver. For example, with lsbcmnds.inf in the current directory, I ran:

```
# ndiswrapper -i lsbcmnds.inf
```

10. Check that the driver is now available and the hardware is available:

```
# ndiswrapper -l
```

11. To load the module, type the following:

```
# modprobe ndiswrapper
```

12. To see your wireless interface, type:

```
# ifconfig
```

13. To search for access point, use the following:

```
# iwlist wlan0 scan
```

14. To list wireless statistics, use the following:

```
# iwconfig
```

15. To check that the module loaded properly, check the /var/log/messages. These messages appeared:

```
Nov 20 12:34:56 kernel: ACPI: PCI interrupt 00:0a.0 -> 5
Nov 20 12:34:56 kernel: udev: creating device node '/dev/ndiswrapper'
Nov 20 12:34:56 kernel: ndiswrapper: using irq 5
Nov 20 12:34:56 kernel: wlan0: device: 00:66:f9:b3:00
Nov 20 12:34:56 kernel: wlan0: encryption modes supported:      WEP, WPA, TKIP, CCMP
Nov 20 12:34:56 kernel: ndiswrapper: using lbcmnds
Nov 20 12:34:56 kernel: (The Linksys Group, Inc., 07/17/2003, 3.30.15) added
```
