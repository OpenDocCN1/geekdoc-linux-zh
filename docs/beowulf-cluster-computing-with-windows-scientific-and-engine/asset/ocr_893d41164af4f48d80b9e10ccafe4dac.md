![](bbox=[0.37, 0.21, 0.63, 0.25])

**Figure 5.2**
Ethernet NIC architecture.

# Data Link Layer.

The Data Link Layer provides the logical interface between the host processor and the Physical Layer of the Ethernet. When a message is to be transmitted, the Data Link Layer accepts, temporarily stores, and encapsulates the message and controls the transmission process of the Physical Layer. When a message is being received, it accepts the packet from the Physical Layer, determines whether the node is the correct destination, verifies bit integrity, unpacks the data into byte sequence, temporarily buffers the data, and passes it on to the processor. The Data Link Layer is made up of the Logical Link Control sublayer and the Media Access Control sublayer.

For most current-generation Beowulf nodes, the Logical Link Control sublayer incorporates an interface to the PCI bus. This element of the Ethernet controller provides all logical control required to accept commands from the host processor and to provide direct memory access to the node main memory for rapid data transfers between memory and the network. Usually included is some form of FIFO buffering within the Data Link Layer to hold one or more incoming or outgoing messages in the node. The Logical Link Control sublayer presents variable-length byte sequences to the Media Access Control sublayer and accepts data byte sequences from it. The exact form and operation of the Logical Link Control sublayer is not standardized, and manufacturer differences are a source of headaches for device driver writers.

The Media Access Controller (MAC) is largely responsible for conducting the Ethernet protocol for both transmitted and received messages. Its two principal tasks are message encapsulation and packet collision handling. To transmit a message, the MAC accepts the byte sequence of the data to be sent, as well as