By contrast, the twisted-pair technology requires that a star topology be used, as shown in Figure 1.3. In such a network, the computers are not usually connected directly to each other, but to a central device (a hub or switch) that processes all the network's traffic.

![](bbox=[0.3, 0.285, 0.85, 0.655])

# FIGURE 1.3

A star topology links all computers to a central point.

# Alternatives to Ethernet

Ethernet is not the only networking hardware available. Most others are in decline, however, at least for use in small networks. You might find that you need to use one of these network types if you're connecting computers to an existing network. In some cases, though, you might want to set up a small Ethernet network and link it to another network by configuring your Linux computer to use both types, and use it as a router.

# Serial and Parallel Ports

You can use the serial or parallel ports found on most PCs to create a simple but low-speed network. In general, you would use the point-to-point protocol (PPP) tools for doing serial-line networking, and the parallel line Internet protocol (PLIP) for parallel port networking. Both of these are Linux kernel protocols, and both require additional configuration. In general, neither of these protocols is very useful for most practical local networks because they're so slow compared to Ethernet. Also, they can be used to connect only two computers. Finally, you lose the use of whichever port is required on both computers. With Ethernet boards selling for $30 and less, the cost of setting up a two-computer network is well under $100.