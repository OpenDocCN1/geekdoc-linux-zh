830

Chap. 13 Networking

| Layer Number | Layer Name | Data Form | Comments |
| :---: | :---: | :---: | :---: |
| 1 | Physical |  | Physical connection between systems. Usually thinner or twisted pair. |
|  |  |  |  |

![](bbox=[0.19, 0.22, 0.85, 0.24])

I start reviewing Figure 13-2 at the bottom with layer 1 and then describe each of the four bottom layers. This is the International Standards Organization Open Systems Interconnection (ISO/OSI) model. It is helpful to visualize the way that networking layers interact.

# *Physical Layer*

The beginning is the physical interconnection between the systems on your network. Without the **physical layer**, you can’t communicate between systems, and all the great functionality you would like to implement is not possible. The physical layer converts the data you would like to transmit to the analog signals that travel along the wire (I’ll assume for now that whatever physical layer you have in place uses wires). The information traveling into a network interface is taken off the wire and prepared for use by the next layer.

# *Link Layer*

In order to connect to other systems local to your system, you use the link layer that is able to establish a connection to all the other systems on your local segment. This is the layer where you have either IEEE 802.3 or Ethernet. Your UNIX system supports both of these "encapsulation" methods. This is called encapsulation because your data is put in one of these two forms (either IEEE 802.3 or Ethernet). Data is transferred at the link layer in frames (just another name for data), with the source and destination addresses and some other information attached. You might think that because two different encapsulation methods exist, they must be very different. This assumption, however, is not the case. IEEE 802.3 and Ethernet are