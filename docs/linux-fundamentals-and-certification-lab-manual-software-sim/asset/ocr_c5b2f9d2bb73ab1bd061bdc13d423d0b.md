| Layer | Common Name | Responsibility |
|---|---|---|
| 1 | Physical | This layer defines the physical link between devices. Voltage levels, voltage changes, physical connectors, and other characteristics are defined. The physical layer delivers the bits, 1s and 0s, across the transmission media. |
| 2 | Data Link | The data-link layer is responsible for the physical addressing, network topology, error notification, and flow control. The computer's MAC address is defined at this layer. (A *MAC, Media Access Control*, address is provided by the manufacturer of the network interface card (*NIC*) and consists of six bytes, three that identify the manufacturer and three that identify the device. *Each device has a unique MAC address*.) Data link assembles the frames of information to be sent across a network. |
| 3 | Network | The network layer is responsible for path selection, routing, and logic addressing. The computer's logical network address, such as IP or IPX, is used to perform the network functions. The network layer assembles packets of information to be transmitted over the network. |
| 4 | Transport | The transport layer is the boundary between application issues and data flow issues. This layer provides connection protocols between computers. The transport layer segments the data from the upper layers for transmission over the network. |
| 5 | Session | The session layer establishes, manages, and terminates sessions between two computers. This layer provides exception reporting for session, presentation, and application layer problems. |
| 6 | Presentation | The presentation layer ensures that information from the application layer of one computer can be understood by the application layer of another. This layer ensures that there is a common data format. |
| 7 | Application | The application layer is closest to the user. It provides network service applications. |

For data to travel from one computer to another, the OSI model layers must be traversed. For example, suppose that you open the Mozilla Web browser to connect to a Web site. The first thing you do is type in the Uniform Resource Locator (URL) of the Web site you want. The URL is sent to the presentation layer, which ensures that it is in standard format, then sends it to the session layer. The session layer establishes session information for the data, then sends it to the transport layer. The transport layer segments the data stream from the upper layers into manageable segments that can be transmitted over a communication line and then sends the segments to the network layer. The network layer applies the computer's logical addressing information to the segments, forming packets that are then sent to the data-link layer. The data-link layer applies the MAC address information to the packet information, forming frames that are then sent to the physical layer. The physical layer sends the frames one bit at a time over the transmission media. After the bits are received by another computer the steps of the whole process just described are performed in reverse order.

# ## Network Components

Networks today have a lot of different components. There are the computers, called **hosts**, that connect to the network, hubs, switches, routers, and other devices that are too numerous to list here. In most cases, a Linux administrator will deal with hosts, hubs, switches, and routers. Other components are beyond the scope of this course.

Components include:

+   * **hosts** A host is any computer connected to the network and assigned a logical address. In most cases a logical address is the IP address, although there are other addressing schemes.

Table 7-1
Layers of the OSI model.