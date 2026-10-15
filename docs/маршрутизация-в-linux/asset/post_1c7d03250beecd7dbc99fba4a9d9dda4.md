
exchange UPDATE messages. These messages contain different information depending on their purpose. For example, an UPDATE message advertising a new route contains:

- **The ORIGIN Type code.** This code tells BGP whether the route it's dealing with is inside the AS that the UPDATE message came from or from outside of it. AS border routers do share information about paths outside of their control as well as internal paths.
- **The AS_PATH segment type.** This code specifies whether the list of autonomous systems the new route information passed through to get to this AS border router is in a specific order or unordered.
- **The ASs that this route information passed through.** The ordered or unordered list of AS numbers.
- **The IP address for the AS border router this one must send data to get packets to the specified new route.** This is called also the Next Hop attribute.
- **The number of bits in the following IP address portion.** Because routing is done for networks and subnetworks, not individual IP addresses, the information sent between AS border routers is a collection of IP address prefixes or the portion of the address that identifies the network or subnetwork in question.
- **The IP prefix that identifies the network or subnetwork to which this route applies.** This prefix has to end at one of the dots in the IP address. If the definition applies to 192.14.14.51, and it's a full unsubnetted class C network, the entry would be 192.14.14.

There can be only one new route per UPDATE message. However, BGP can withdraw as many existing routes as it likes in the same UPDATE message. Each of these route withdrawals includes all or part of the following information:

- **The total length of the withdrawn routes section.** This item ensures that there is no confusion from section to section, given that withdrawn routes can be any length. A zero means that there are no routes to remove.
- **The number of bits in the IP address portions.** Once again, the information sent between AS border routers is a collection of IP address prefixes, or the portion of the address that identifies the network or subnetwork in question.
- **The IP prefix that identifies the network or subnetwork to which this route applies.** Again, the prefix has to end at one of the dots in the IP address.
- **The total length of the Path Attributes section.** Once again, including this information avoids misread data.

How does the BGP AS border router decide about which routes to notify its neighbors? Each of these machines has a Policy Information Base (PIB) containing rules that the administrator sets by hand. Each machine also has a set of separate databases, each with a specific function. All of the routes this router is aware of are listed in its Adj-RIB-In database. Routing Information Base (RIB) is another term for the routing table. The BGP AS border router takes its PIB and applies the rules to every route in Adj-RIB-In. Anything that fits the rules is copied to the Adj-RIB-Out database.

One piece of data calculated using the PIB rules is the preference rating for each particular route. After this information is put together, the BGP AS border router looks at each destination it has routing information for and chooses the best route to each according to its PIB rules and preference ratings. The best routes are all stored in the Loc-RIB database.

There is still one more chunk of processing to do. Keep in mind that these databases are maintained from moment to moment. Each time new information goes into Adj-RIB-In or Loc-RIB, there's a trickle-down effect. Adj-RIB-Out relies on both of these databases and so must change whenever one or both of them does. Adj-RIB-Out is trimmed further than Loc-RIB in some BGP implementations. Duplicate routes are removed from this version of the database so that there is only one way for data to get from point A to B. This ensures that the databases don't get too large or redundant. Whenever there is a change to Adj-RIB-Out, that change is sent as an UPDATE message to the BGP neighbors.

Perhaps now you have an idea of why BGP is preferred over EGP in many situations. It is simply a smarter protocol with more internal checks and balances for route tuning. The programs under Linux that implement this protocol are zebra and the unicast version of gated. Once again, BGP is a unicast border protocol.

## Border Gateway Multicast Protocol (BGMP)

Multicast protocols need AS border router attention too. This section deals with the Border Gateway Multicast Protocol, or BGMP. BGMP comes with the capability of building multicast group trees in the style of PIM-SM, where only group members belong to the tree at any given time. However, these trees don't consist of individual routers. Instead, each tree has only BGMP border routers as members. Once this tree is built, some domains build their own internal trees from there, depending on the protocol they are using.

The multicast domain advertising the availability of a specific range of multicast channels is considered the root for that range. Remember that multicast channels each consist of a single class D Internet address, which range from 224.0.0.0 through 239.255.255.255. So, perhaps our AS has the range of multicast channels from 231.15.19.120 through 231.15.19.140. BGMP would consider our AS the root domain for that range.

When a user joins a multicast group outside their domain or AS, their request is passed to the BGMP router. This router looks up the address for the router handling the root domain containing this particular channel. Once the BGMP router knows which domain to send the request to, it generates a BGMP UPDATE message containing the following information:

- Address prefix. This prefix tells BGMP the length of the included netmask.
