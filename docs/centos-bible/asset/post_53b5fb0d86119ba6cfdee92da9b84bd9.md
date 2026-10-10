
## Supported Wireless Network Adapters and Modules

| Wireless Network Adapter | Module |
| --- | --- |
| 350 Series Wireless LAN Adapter (Cisco Systems) | airo_cs.ko |
| ADMtec ADM8211 wireless | adm8211.ko |
| Aironet PC4500 (Cisco Systems) | airo_cs.ko |
| Aironet PC4800 (Cisco Systems) | airo_cs.ko |
| AT&T WaveLAN Adapter | wavelan_cs.ko |
| Atheros 802.11 wireless | ath5k.ko |
| Atmel AT76C50x wireless | atmel_cs.ko |
| Atmel AT76C50x wireless (PCI version) | atmel_pci.ko |
| Broadcom 43xx wireless | bcm43xx.ko |
| Cabletron RoamAbout 802.11 DS | wlan_cs.ko |
| Compaq WL100 11 Mbps Wireless Adapter | orinoco_cs.ko |
| Digital RoamAbout/DS | wavelan_cs.ko |
| ELSA AirLancer MC-11 | wlan_cs.ko |
| Intel PRO/Wireless 2100 Network Connection mini PCI adapters | ipw2100.ko |
| Intel PRO/Wireless 2915ABG and 2200BG Network Connection mini PCI adapters | ipw2200.ko |
| Intel PRO/Wireless 3945ABG Network Connection adapter | iwifi.ko |
| Intel Wireless Wifi Link 4965AGN | iwifi.ko |
| Intersil PRISM2 11 Mbps Wireless Adapter | wlan_cs.ko |
| Lucent Technologies WaveLAN Adapter | wavelan_cs.ko |
| Lucent Technologies WaveLAN/IEEE Adapter | orinoco_cs.ko |
| MELCO WL1-PCM-L11 | orinoco_cs.ko |
| MELCO WL1-PCM-L11G | orinoco_cs.ko |
| NCR WaveLAN Adapter | wavelan_cs.ko |
| Orinoco PC Cards | orinoco_cs.ko |
| PLANEX GeoWave/GW-CF110 | orinoco_cs.ko |
| Planet WL3501 | wl3501_cs.ko |
| Prism54 PCI wireless | prism54pci.ko |
| Prism54 USB wireless | prism54usb.ko |
| Realtek RTL8187 USB wireless | rt18187.ko |
| Xircmod CreditCard Netwave | netwave_cs.ko |
| ZCOMAX AirRunnerXL-300 | orinoco_cs.ko |
| ZyDAS ZD1201 wireless LAN USB sticks | zdl201.ko |
| ZyDAS ZD1211 wireless LAN USB sticks | zdl211rw.ko |

While most wireless LAN cards don’t require a completely unobstructed line of sight, an obstacle can certainly slow reception. To get around this problem, an antenna such as the Orinoco IEEE range-extender can plug directly into an Orinoco Gold or Silver wireless LAN card. A 1.5-meter extension cable can bring the signal out from behind a closed door or out on top of a desk. When you set up the antenna, it is recommended that it be:

- Placed in a central location
- Mounted vertically
- Located away from obstructions (metal surfaces in particular, and, to a lesser extent, solid objects such as concrete walls or stacks of papers)

Refer to the instructions that come with your antenna for specific guidelines regarding placing and mounting the antenna.

## Using Outdoor Antennas

Choosing and setting up outdoor antennas for your wireless LAN can be more difficult and expensive than setting them up indoors. Once the outdoor antennas are in place, however, you can save money because you won’t need multiple Internet access accounts (monthly fees, DSL/cable modems, etc.).

Although a complete description of the use of outside antennas with your wireless LAN is outside the scope of this chapter, here are some tips that will help you choose the best antennas for your wireless LAN.

- **Point-to-Point versus Multipoint** — If you are creating a point-to-point link between two outdoor locations (e.g., to share a Internet connection between two buildings), a directional antenna can help you achieve greater distance and transmission speeds. However, if your antenna is providing multipoint access for several other outdoor antennas or wireless clients (such as students working from laptops on the campus lawn), an omnidirectional antenna may be more appropriate.
- **Clearance** — The clearer the line of sight between outdoor antennas, the greater the distance and transmission speed you can achieve. Placing antennas at the highest possible points can prevent diminished performance caused by trees, cars, buildings, and other objects. The amount of distance between obstacles and the coverage area of your wireless transmission is referred to as the clearance factor (see Figure 14-10).

![](img/2f265415ceec72538dd3c78ffca75c10_614_0.png)

- **Distance** — Although the actual distances over which antennas can send and receive data vary greatly based on different factors, you can achieve distances of many miles with outdoor antennas. For example, two Orinoco 24 dBi directional parabolic-grid antennas can theoretically achieve distances of up to 52 miles at an 11-Mbps transmission speed with a 180-meter clearance. Reduce the transmission rate to 1 Mbps, and you can achieve distances of up to 149 miles with a 1,200-meter clearance. Shorter distances are achieved with less expensive equipment, such as the Orinoco 14 dBi directional antenna, which can achieve distances of up to 5.3 miles at 11 Mbps with a 13-meter clearance.
- **Cable Factor** — The distances that transmissions travel on the cables between the wireless cards and the antennas can be a factor in choosing the right antenna. The shorter the cables, the greater the distance and speed you will get on your antenna.

The power of an antenna is rated in terms of gain. Gain is measured in decibels, based on a *theoretic isotropic radiator* (or dBi). Higher gain offers opportunities for reaching greater distances at greater speeds. However, the ability of the antenna to focus that power (directional vs. omnidirectional) greatly affects the speeds and distances that can be achieved. If you want to see some interesting home-made antennas, search the Web for the word *cantenna*.

### Getting Wireless Drivers

If you are using a wireless card that includes a supported driver in CentOS, the system might detect that card and load the proper driver, so that you will be able to configure it as described later in this section. In other cases, you will need to install the associated firmware for the driver that comes with the hardware (usually intended for Windows systems). If the driver you need for your wireless card is not included with CentOS, you may be able to use NDISwrapper and a Windows driver to configure your wireless card. The following procedure contains an example of configuring NDISwrapper with a Linksys 802.11g wireless PCI adapter card:

> If you find you need further information about using NDISwrapper, refer to the NDISwrapper project page at http://ndiswrapper.net/.

1. Determine the kind of wireless card you are using. If you have a PCI card, type:

```bash
# lspci -v | less

00:0a.0 Network controller: Broadcom Corporation BCM4306 802.11b/g Wireless LAN Controller (rev 03)
    Subsystem: Linksys: Unknown device 0014
    Flags: bus master, fast devsel, latency 64, IRQ 5
    Memory at ee000000 (32-bit, non-prefetchable) [size=8K]
```

In this example, the PCI card is a BCM4306 802.11b/g Wireless Controller from Broadcom Corporation. (If your wireless card is a USB device, type the `lsusb` instead.)

2. Check the following list of wireless card drivers known to run under NDISwrapper, as mentioned previously.

3. If your card is supported, download the driver recommended. I used the Linksys WMP54GS Wireless-G PCI Adapter (which was reflected by the chipset BCM4306 802.11g, rev 03 shown in the preceding `lspci` output). So I downloaded the driver as follows:

```bash
# mkdir wireless
# cd wireless/
# wget ftp://ftp.lnksys.com/pub/network/wpc54g_v2_driver_utility_v2.0.zip
```

4. After the file is done downloading, unzip the driver file. For the example, I typed:

```bash
# unzip wpc54g_v2_driver_utility_v2.0.zip
```

5. Install the kernel-devel and gcc packages. Then link the kernels directory to the modules directory or your current kernel (replacing `<kernel-version>` with the version of your kernel development package and current kernel, where shown):

```bash
# yum install kernel-devel gcc
# ln -s /usr/src/kernels/<kernel-version>/lib/modules/<kernel-version>/build
```

6. Get the NDISwrapper source code by downloading it to your CentOS system from the following site: http://sourceforge.net/projects/ndiswrapper.

7. With the NDISwrapper source code package in the current directory, unzip and untar it as follows:

```bash
# tar xvfz ndiswrapper*.tar.gz
```

8. As root user, change to the NDISwrapper directory and run the make command as follows:

```bash
# cd ndiswrapper*
# make install
```

9. Get the INF file from the unzipped driver package. From our example, the file we needed was lsbcmds.inf. Then run the `ndiswrapper -i` command to install the driver. For example, with the lsbcmds.inf file in the current directory, I ran:

```bash
# ndiswrapper -i lsbcmds.inf
```

10. Check that the driver is now available and the hardware is available:

```bash
# ndiswrapper -l
lsbcmds    driver present, hardware present
```

11. To load the NDISwrapper module, type the following:

```bash
# modprobe ndiswrapper
```

12. Type the following command to see your wireless LAN (WLAN) entry:

```bash
# iwconfig
```

13. Type the following to see your access point:

```bash
# iwlist wlan0 scan
```

14. Create an alias for your wireless device to wlan0, so that the interface is loaded automatically at boot time:

```bash
# ndiswrapper -m
```

15. To check that the NDISwrapper module loaded properly, you can check the /var/log/messages file. These messages appeared after the module was loaded:

```text
Nov  2 20:28:53 toys kernel: ndiswrapper version 1.42 loaded (preempt=no,smp=no)
Nov  2 20:28:53 toys kernel: ACPI: PCI interrupt 0000:00:00.0[A] -> 651 5 (level, low) -> IRQ 5
Nov  2 20:28:53 toys kernel: ndiswrapper: using irq 5
Nov  2 20:28:54 toys udev: creating device node '/dev/ndiswrapper'
Nov  2 20:28:54 toys kernel: wlan0: ndiswrapper ethernet device 00:0f:66:6f:b9:0a using driver lsbcmds
```

## Setting Up Network Connections and LANs
