![](bbox=[0.07, 0.11, 0.17, 0.19])

# IEEE and wireless networks

The dominant wireless standard is based on the IEEE 802-11b (and the older 802-11a and the about-to-be-released 802-11g) standard; 802-11b is also referred to as Wi-Fi (which is short for the wireless industry's trade term wireless fidelity). If you hear people talking about a Wi-Fi NIC, they're just talking about wireless NICs.

IEEE (pronounced "eye-triple-e"), or Institute of Electrical and Electronic Engineers, is a worldwide professional society of nerds. (Is it necessary to use words like nerds or geeks to convey some technical meaning?) The IEEE, the "triclops" of wireless networking, concerns itself with issues such as which frequency wireless networking devices should use. Fortunately, this group has devised this wonderful standard that now enables everyone who's interested to communicate without stringing wires between machines.

# Preparing to configure your wireless NIC

Before you can configure your wireless NIC, you need to figure out two things:

+   Which type of wireless NIC you have (or need)
How your wireless NIC should connect to your network

Two main types of wireless electronics (or chip sets) are now in use: Wavelan, built by Lucent Technologies, and Prism2, designed by Intersil. Both types are supported by Red Hat. The following list shows the manufacturers of each type. You can use the list to help figure out what kind of chip set your device uses:

+   **Wavelan:** Orinoco, Apple Airport Enterasys RoamAbout 802, Elsa AirLancer 11, and Melco/Buffalo 802.11b.
**Prism2:** D-Link DWL-650, LinkSys, Netgear, WPC11, and Compaq WL110. Other, less popular models include Addtron AWP-100, Bromax Freeport, GemTek WL-211, Intalk/Nokia, SMC 2632W, YDI, Z-COM X1300, and Zoom Telephonics Zoom Air 4100.

You need to figure out how your wireless NIC (or network adapter) should connect to your network. Wireless NICs can connect to a LAN in two ways:

+   **Adapter-to-adapter:** This type, referred to as an ad hoc connection, is useful if you have two or more computers that you want to talk and form their own, exclusive private network.