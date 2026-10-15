Now, onto the Hello messages and Poll commands. When an EGP AS border router receives a Hello message, it sends back an I-Heard-you (IHU or I-H-U) message, verifying that it is up and running and received the Hello message. Then there’s Poll. Remember that when an EGP AS border router receives a Request command it, sets how often Poll commands are sent to the requesting neighbor and then starts the timer that counts the number of seconds till the next time it needs to send the Poll command.

When the timer reaches the interval value, the machine sends a Poll command to the specified neighbor. When the neighbor receives the Poll command, the response depends on what state and mode this neighbor is in. An EGP AS border router ignores Poll commands if it is in the Down state or Passive mode. If it is not in this state or mode, the neighbor responds with an Update. It is this message that transmits actual information about the networks available in each autonomous system. The data contained in an Update consist of:

+   - **All gateways within the AS.** Remember that gateways are devices that connect two or more networks.
+   - **All gateways the router knows about outside of the AS.** This allows for a more complete routing table with less querying.
+   - **All networks available through each gateway.** The AS border router’s neighbors need to know where to send information. Your router doesn’t need to do as much “thinking” if the neighbors already know to send data directly to a specific gateway for a specific network.
+   - **How many routers and gateways data must pass through to reach each specific network from your AS border router.** This information allows for shortest path calculations internally within the AS.
+   - **Each neighbor’s current state.** This information ensures that each of the routers know what kind of data each is expecting from the other.

As you can see, EGP has quite a job to do. Without some kind of method for AS border routers to share information, there would have to be a centralized list of where to send data for all specific networks. The program under Linux that implements this protocol is the unicast version of gated.

# Border Gateway Protocol (BGP)

The child of EGP is the Border Gateway Protocol (BGP-4). This protocol has been through a number of versions, and the most current is BGP-4. All references to BGP in this chapter are to this fourth version. One of the primary issues that BGP-4 adds to the mix is that EGP was unable to handle some of IP version 6’s capabilities, which are covered in depth in Chapter 4, “IPv4 and IPv6 Addressing.”