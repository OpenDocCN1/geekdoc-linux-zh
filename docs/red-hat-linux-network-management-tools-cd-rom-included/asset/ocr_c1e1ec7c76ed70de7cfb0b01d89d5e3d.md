cols, the length of the fields will depend on the type of network. Figure 3.21 shows the standard ARP and RARP message format.

The hardware type field defines the hardware interface type for which the sender requires an answer. Standard values include 1 for Ethernet and 2 for FDDI. The protocol type specifies the high-level protocol type the sender is using, which for IP is 0800 in hexadecimal (decimal is 2048). The operation field notes if the message is an ARP request (1), ARP response (2), RARP request (3), or RARP response (4). The Hlen and Plen fields define the hardware and high-level protocol address field lengths. The Hlen and Plen fields permit ARP to work with any arbitrary datalink protocol because the sizes of the hardware type and protocol fields can be determined by inspecting the ARP packet directly. The sending entity will supply, if possible, the Sender HA and/or Sender IP field information when issuing the request. The Sender HA is used with the ARP request, while the Sender IP is used with an RARP request. The Target HA is used when responding to the ARP message; otherwise, the Target IP is used when responding to RARP.

![](bbox=[0.2, 0.47, 0.85, 0.64])

**Figure 3.21** **ARP/RARP Message Format.**

# ARP Cache

At first glance, the ARP service may seem inefficient because it will send a broadcast packet each time a device wishes to communicate with another. However, ARP implementations, on many systems, include the use of an ARP cache to temporarily store address bindings from previous ARP requests. In fact, before an ARP request is made, the higher-level software scans the ARP cache to see if the required datalink address mapping already exists in the