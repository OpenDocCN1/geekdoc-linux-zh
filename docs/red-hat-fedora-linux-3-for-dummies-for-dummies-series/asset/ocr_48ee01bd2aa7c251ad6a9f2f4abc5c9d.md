# # IEEE, Wi-Fi, and wireless networks

IEEE (pronounced “eye-triple-o”), or Institute of Electrical and Electronic Engineers, is a world-wide professional society of nerds (specifically, those nerds who care enough about technical matters to set consistent standards). The IEEE, the “triclops” of wireless networking (one eye, three Es, get it?), concerns itself with issues such as which frequency wireless networking devices should use. Fortunately, this group has devised this wonderful standard that now

enables everyone who is interested to communicate without stringing wires between machines.

The dominant wireless standard is a combination of ingredients. It’s based partly on the IEEE 802.11b standard (also called Wi-Fi, short for wireless fidelity)—and also two older standards (802.11a and the more recent 802.11g). Hey, call it shorthand: if you hear people talking about a Wi-Fi NIC, they’re just talking about wireless NICs.

The first order of business is to figure out how your wireless NIC (or network adapter) should connect to your network. Wireless NICs connect to a LAN in two ways:

+   ✔ **Adapter to adapter**: This type, referred to as an *ad-hoc* connection, is useful if you have two or more computers that you want to talk and form their own, exclusive private network.

+   ✔ **Adapter to wireless access point**: This type, called *infrastructure*, provides a single entrance (an access point) into a LAN. An *access point* allows one or more computers to be connected to a network. However, unlike an ad-hoc network, the individual computers can connect to any access point that allows them to.

The wireless-configuration instructions we provide work with either the infrastructure or ad-hoc connection methods. Your wireless NIC can connect to either the access point or other computers (Linux and Windows) as long as you correctly configure your network ID (ESSID) and your encryption key.

# # Why ad-hoc is better than infrastructure

Using ad-hoc mode provides several advantages:

+   ✔ **Lower costs**: You don’t have to purchase an access point; access points starts at around $50. Computers using wireless NICs running in ad-hoc mode communicate directly with each other, eliminating the need for a common access point.