Figure 14.2
10Base-T networks use a star topology.

![](bbox=[0.26, 0.17, 0.55, 0.35])

# Ethernet Hubs

Ethernet hubs typically have from 4 to 24 ports for Ethernet connections. Some hubs run at only one speed (10 or 100 Mbps), whereas others are dual-speed. Cheaper dual-speed hubs will force all ports to be the same speed, so adding a 10 Mbps Ethernet interface to a network that is otherwise 100 Mbps will substantially decrease network performance. However, most modern dual-speed hubs will automatically detect the correct connection speed for each port individually; these are called auto-sensing hubs. Some hubs are stackable, which means that one or more ports can be used for connecting a second hub. Obviously, stackable hubs give far more opportunity for expanding a network after its original installation.

# Switches

One of the distinguishing features of Ethernet rejoices in the name CSMA/CD, or Carrier Sense Multiple Access with Collision Detection. CSMA/CD is an approach for deciding what to do when more than one device on the Ethernet tries to send a frame of data simultaneously (since only one frame can be active at any given moment). Each device detects this "collision." At this point, the devices must be able to re-send their frames at different times, without communicating between themselves or using any external arbitration. The approach that Ethernet adopts is for each device to wait a random length of time before re-sending the frame.

In normal operation, this is entirely adequate. However, if a network is heavily loaded, performance degrades severely, as the Ethernet devices end up spending more and more of their time waiting for collision situations to be resolved. The network becomes saturated.

Ethernet switches get around this problem. They behave in a similar way to hubs, but where hubs create a single Ethernet out of multiple independent cables, a switch essentially puts each of its ports on a separate Ethernet, and transmits (or switches) frames between each network. You can put a network hub on each port of a switch. Alternatively, you can directly connect a single host; this would be useful for a heavily used server that many other hosts must communicate with.