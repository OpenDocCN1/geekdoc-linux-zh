(See the LAN Card Numbering subsection.)

| parameters | One or more of the following operating parameters: |
| :--- | :--- |
| up | Mark an interface "up". Enables interface after an ifconfig down. Occurs automatically when setting the address on an interface. Setting this flag has no effect if the hardware is "down". |
| down | Mark an interface "down". When an interface is marked "down", the system will not attempt to transmit messages through that interface. If possible, the interface will be reset to disable reception as well. This action does not automatically disable routes using the interface. |
| broadcast | (Inet only) Specify the address that represents broadcasts to the network. The default broadcast address is the address with a host part of all 1's. |
| debug | Enable driver-dependent debugging code. This usually turns on extra console error logging. |
| -debug | Disable driver-dependent debugging code. |
| ipdst | (NS only) This is used to specify an Internet host that is willing to receive IP packets encapsulating NS packets bound for a remote network. In this case, an apparent point-to-point link is constructed, and the address specified is taken as the NS address and network of the destination. |
| metric n | Set the routing metric of the interface to n. The default is 0. The routing metric is used by the routing protocol (see gated(1m)). Higher metrics have the effect of making a route less favorable; metrics are counted as additional hops to the destination network or host. |
| netmask mask | (Inet only) Specify how much of the address to reserve for subdividing networks into subnetworks or aggregating networks into supernets. Mask can be specified as a single hexadecimal number with a leading 0x, with a dot-notation Internet address, or with a pseudo-network name listed in the network table (see |