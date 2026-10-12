
other objects. The amount of distance between obstacles and the coverage area of your wireless transmission is referred to as the *clearance factor*, as shown in Figure 15-11.

![](img/1744bde8c889adfab3fc911e1687fecf_647_0.png)

**Figure 15-11:** The distance of obstructive objects from the wireless signal is called the *clearance*.

- **Distance** — Although the actual distances over which antennas can send and receive data varies greatly based on different factors, you can achieve distances of many miles with outdoor antennas. For example, two Orinoco 24 dBi directional parabolic-grid antennas can theoretically achieve distances of up to 52 miles at an 11 Mbps transmission speed with a 180-meter clearance. Reduce that transmission rate to 1 Mbps and you can achieve distances of up to 149 miles with a 1200-meter clearance. Shorter distances are achieved with less expensive equipment, such as the Orinoco 14 dBi directional antenna (about $149) which can achieve distances of up to 5.3 miles at 11 Mbps with a 13-meter clearance.
- **Cable factor** — The distances that transmissions travel on the cables between the wireless cards and the antennas can be a factor in choosing the right antenna. The shorter the cables, the greater the distances and speeds you will be able to achieve on your antenna.

The power of an antenna is rated in terms of *gain*. Gain is measured in decibels, based on a *theoretic isotropic radiator* (or *dBi*). Higher gains offer opportunities for reaching greater distances at greater speeds. However, the ability of the antenna to focus that power (directional versus omnidirectional), greatly affects the speeds and distances that can be achieved.

## Installing wireless Linux software

If you did a Laptop or an "Everything" installation of Red Hat Linux on your computer, the software packages you need to create your wireless LAN may already be installed. Drivers and modules needed to support PCMCIA cards and wireless cards should already be built into your Linux system.

Besides the wireless drivers, the following software packages contain tools for configuring and working with your wireless LAN cards in Red Hat Linux:

- **Kernel-pcmcia-cs** — Contains commands and configuration files to support PCMCIA cards. Included in the package is the `wireless` script (for starting the wireless LAN interface) and the `wireless.opts` file (which sets default options for each type of wireless card).
- **Wireless-tools** — Contains commands for setting extensions for your wireless LAN interface. Commands include `iwconfig` (for configuring your wireless interface) and `iwlist` (for listing wireless statistics).

Once you have established a wireless LAN interface, you can use a variety of Linux software to monitor and control access to that interface. You will need to install the appropriate software packages as well.

## Configuring the wireless LAN

Before you begin testing the distances you can achieve with your wireless Linux LAN, I recommend that you configure wireless cards on two computers within a few feet of each other. Once the two computers are communicating, you can change wireless settings to tune the connection and begin experimenting with transmission distances.

The following sections describe the steps you need to take to set up a wireless LAN between two Linux systems. Although only two nodes are described, you can add more computers to your wireless LAN once you know how. This procedure describes how to operate your wireless Linux LAN in two different modes:

- **Ad hoc** — All the computers in your wireless LAN are gathered into a single virtual network made up of only one cell. A single cell means that you cannot roam among different groups of wireless nodes and continue your communication invisibly. To do that requires a managed network.
- **Managed** — As I noted earlier, many wireless cards supported in Linux cannot operate as access points. A Linux wireless card, however, can operate as a node in a managed network. The wireless-configuration tools that come with Red Hat Linux let you identify the access point for Linux to use by indicating the access point's MAC address.

## Choosing equipment

Start with two computers. (You can add more computers later, once you understand how to get your wireless interfaces working.) For this procedure, I used computers that had the following characteristics (you can use different computers and cards, if you like):

- **Computers** — One computer was a laptop with an available PCMCIA slot; the other was a desktop system with only PCI slots.
- **Wireless cards** — As I mentioned earlier, I purchased two Agere (Lucent Technologies) Orinoco wireless LAN cards: one Gold Label and one Silver Label. For the desktop computer, I purchased a PCI adapter card because it had no PCMCIA slot in it. Both cards come with built-in antennas, so I had no need for additional antennas while setting up the two computers (in the same room) for wireless communication.

> **NOTE:** The only difference between the Gold and Silver Label cards is that the Gold card offers support for more secure encryption, so there was no reason for me to choose two different types of cards. If I had it to do over again, I would have used two Silver cards and saved a few dollars.

- **Red Hat Linux** — I installed Red Hat Linux on both machines, selecting a Laptop install for the laptop and an "Everything" install for the desktop computer. (The "Everything" install was not strictly necessary, but I wanted to be able to use the GUI and various server features.)

Because I was using the desktop computer as a gateway to the Internet, that computer also had a wired Ethernet card that was connected to my DSL modem to provide a route to the Internet for any computers on my wired or wireless networks.

### Inserting wireless cards

To physically install the wireless cards, follow the directions that come with the cards. For my laptop, I simply inserted one Orinoco card into a PCMCIA slot. For the desktop computer, I powered down, inserted the PCI adapter into a vacant slot, powered up, and inserted the other Orinoco PCMCIA card into the adapter.

### Loading the modules

The cardmgr daemon monitors the PCMCIA slots on computers that have them. If a card is recognized and listed in the PCMCIA database when the card is inserted, the appropriate module is loaded. You should also hear two beeps indicating that the card has been recognized.

On my laptop, my Orinoco wireless card was recognized and its modules loaded. On my desktop computer (with the PCI adapter), the card was not recognized, so I had to do some extra configuration.

### PCMCIA only

To see what modules are loaded after a card is inserted on a computer that has only PCMCIA slots, type the `lsmod` command. In my case, because the Orinoco card uses the orinoco and orinoco_cs modules (along with the hermes helper module), output from the `lsmod` command included the following lines:

```
# lsmod
Module                  Size Used by    Not tainted
orinoco_cs              5640  1
orinoco                34368  0 [orinoco_cs]
hermes                 5344  0 [orinoco_cs orinoco]
ds                     8608  1 [orinoco_cs]
yenta_socket           12384  1
pcmcia_core    50752  0 [orinoco_cs ds yenta_socket]
```

You can see that the orinoco_cs module was loaded and that the referring modules included the orinoco module, the hermes module, the ds (PC Card Driver Services) module, and the pcmcia_core module. If you are using a different card, you may instead see one of the following modules: airo_cs, wavelan_cs, wlan_cs, ray_cs, or netwave_cs.

> **TIP:** You may need to load one or more modules yourself if the hardware is not properly detected. I needed to load the yenta_socket module before my Orinoco PC card was properly detected. I type the following command: insmod yenta_socket to load that module. To make the change more permanent, I added a line to the /etc/init.d/pcmcia script (the line I added is in bold):

```bash
if [ -d $PC ] ; then
	echo -n $" modules"
	/sbin/insmod $PC/pcmcia_core.o $CORE_OPTS
	/sbin/insmod $PC/$PCIC.o $PCIC_OPTS
	/sbin/insmod $PC/yenta_socket.o
	/sbin/insmod $PC/ds.o
else
```

### PCMCIA with adapter card

If your computer has only ISA or PCI slots, you will need an adapter to use your PCMCIA wireless LAN card. When I installed a PCI adapter card Linux didn't detect it, which meant that Linux didn't detect the PCMCIA wireless LAN card either. Therefore, I added the following lines to the /etc/sysconfig/pcmcia file so that the PCI adapter card would be recognized and the PCMCIA service would start automatically at boot time:

```
PCMCIA=yes
PCIC=182365
```

The 182365 driver is a PCMCIA controller driver that includes the Yenta register specification. Yenta is used for CardBus bridges made by Cirrus Logic for a variety of manufacturers (Texas Instruments, IBM, Toshiba, and others). The Orinoco PCI adapter was detected as a Texas Instruments PCI-1410 CardBus Controller. (To see the options available with the 182365 driver, type man 182365.)

Figure 15-12 shows an example of an Orinoco Silver Card using a PCI adapter.
