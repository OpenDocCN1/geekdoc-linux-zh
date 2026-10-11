# **CAUTION**

If you run cabling between rooms or floors, particularly in a business setting, you might need to pay attention to your locality's fire codes. For instance, you might need to purchase Ethernet cables that are fire-resistant, run them through sealed conduits, or take other special precautions. If you're in doubt, contact a network consultant or electrician.

One final advantage of twisted-pair cabling over coaxial cabling is in the ease with which you can add and remove computers. Because twisted-pair cabling uses connectors much like those on telephone wires, you can simply snap a cable into the hub or switch on one end and a computer on the other, and you're set up. The other computers on the network aren't disrupted by this activity, as they are when you add a computer to a thin coaxial network. What's more, if a cable is damaged or gets yanked out of its connector, only one computer's network service is disrupted, which makes diagnosing the problem much easier than it would be with coaxial cabling.

# Telephone Wiring Kits

With the increase in popularity of home networking, many companies have introduced Ethernet kits that are designed to be used over ordinary telephone wiring. Most home telephone wiring configurations include at least two pairs of wires. The better installations use twisted-pair wiring, but in many homes, the wiring isn't twisted and so is subject to greater interference than is common with Ethernet cabling. In any event, a single telephone line requires only one pair of wires, no matter how many extensions you have. The remaining pair or pairs can be used by a low-speed home network.

Such networks typically work at speeds of 10Mbps or lower. (2Mbps is common.) They typically use Ethernet cards that have been modified in various ways to support ordinary telephone wires rather than Ethernet cables. You should therefore be careful, if you decide to buy such a kit, to buy one that can be used with ordinary Linux Ethernet device drivers.

# Hubs and Switches

If you use twisted-pair Ethernet cables, you must link your computers in one of three ways:

+   - **Using a crossover cable**  A crossover cable is wired in such a way that two computers can communicate directly. If you want to network only two computers, you can link them directly using a crossover RJ-45 cable. Doing so has the advantage that the NICs can communicate in full duplex mode, which will probably increase the networking speed. It also saves you the cost of a hub or switch.