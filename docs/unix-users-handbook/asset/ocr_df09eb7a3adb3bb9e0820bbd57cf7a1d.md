# Physical Layer

The beginning is the physical interconnect between the systems on your network. Without the **physical layer**, you can’t communicate between systems, and all the great functionality you would like to implement is not possible. The physical layer converts the data you would like to transmit to the analog signals that travel along the wire (I’ll assume for now that whatever physical layer you have in place uses wires). The information traveling into a network interface is taken off the wire and prepared for use by the next layer.

# Link Layer

In order to connect to other systems local to your system, you use the link layer that is able to establish a connection to all the other systems on your local segment. This is the layer where you have either IEEE 802.3 or Ethernet. Your UNIX system supports both of these "encapsulation" methods. This is called encapsulation because your data is put in one of these two forms (either IEEE 802.3 or Ethernet). Data is transferred at the link layer in frames (just another name for data), with the source and destination addresses and some other information attached. You might think that because two different encapsulation methods exist, they must be much different. This assumption, however, is not the case. IEEE 802.3 and Ethernet are nearly identical. For this reason, many UNIX systems can handle both types of encapsulation. So with the bottom two layers, you have a physical connection between your systems and data that is encapsulated into one of two formats with a source and destination address attached. Figure 9-2 lists the components of an **Ethernet** encapsulation and makes comments about IEEE802.3 encapsulation where appropriate.

| destination address | 6 bytes | address data is sent to |
| :--- | :--- | :--- |
| source address | 6 bytes | address data is sent from |
| type | 2 bytes | this is the "length count" in 802.3 |