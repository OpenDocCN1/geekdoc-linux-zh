# OffSec

This is exactly the type of situation in which port forwarding can be useful. We can create a port forward on CONFLU01 that listens on a port on the WAN interface, then forward all packets received on this port to the PGDATABASE01 on the internal subnet, where we will use Socat⁹⁰¹ to achieve this.

# 18.2.3 Port Forwarding with Socat

Now we are ready to create a port forward. We have an idea of how we want it to work: CONFLUENCE01 should listen on a port on the WAN interface and forward all packets received on this port to the PGDATABASE01 on the internal subnet. This concept is illustrated in the following diagram:

![](bbox=[0.125, 0.295, 0.875, 0.455])

Figure 243: The way we expect our port forward to work

We want to open TCP port 2345 on the WAN interface of CONFLUENCE01, then connect to that port from our Kali machine. We want all the packets that we send to this port to be forwarded by CONFLUENCE01 to TCP port 5432 on PGDATABASE01. Once we set up our port forward, connecting to TCP port 2345 on CONFLUENCE01 will be exactly like connecting directly to TCP port 5432 on PGDATABASE01.

As part of our enumeration of CONFLUENCE01, we will find Socat installed. Socat is a general-purpose networking tool that can set up a simple port forward in a single command.

> In this scenario, we find it already installed, Socat does not need to be installed by default on *NIX systems. If not already installed, it's possible to download and run a statically-linked binary version instead.

We will use Socat to set up the port forward we want on CONFLUENCE01. It will listen on a port on the WAN interface (that our Kali machine can connect to) and forward packets received on that port to PGDATABASE01.

⁹⁰ (dest-unreach, 2022), http://www.dest-unreach.org/socat/socat.html

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

571