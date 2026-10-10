
## Advantages of Ring Topology

- Most of the hardware and software requirements for this network topology are readily available.
- The installation cost is quite low since the popular twisted pair cables that are required in plenty are quite inexpensive.
- The network is largely reliable since it does not rely on a single host machine.

## Demerits of Ring Topology

- Troubleshooting may be quite a task in the absence of specialized test equipment. Detection of a fault in cable is normally a serious challenge.
- Failure in one node leads to failure in the entire network since tokens have to go through each node for a complete cycle of communication from sender to destination.
- Addition of new network devices slows down the entire network.
- Communication delay increases with increasing nodes/network components.

## Star Topology

In this topology, a central computer, switch or hub connects all the nodes on the network. The central device is the server while the peripherals are clients. Coaxial cables or Ethernet’s RJ-45 are favored for connection of the network nodes to the server. Switches or hubs are preferred as the main connection devices in this topology. This is by far the most widely used topology in network implementations.

## Pros of Star Topology

- There is ease of troubleshooting since problems are handled at individual stations.
- Complex network control features can be implemented with ease at the server side-which also allows the automation of certain tasks.
- There’s limited failure since an issue in one cable does not translate into an entire network problem. The fault in a cable may only affect a single node on the network since the nodes are not interconnected via cables.
- Open ports on a switch or hub allow for easy expansion of the network.
- The use of inexpensive coaxial cables makes star topology highly cost effective to implement.
- It has the capacity to handle data speed of up to 100Mbps. Hence, it supports data transmission at very high speeds.

## Cons of Star Topology

- If the central connecting device fails or malfunctions, then the entire network goes down.
- Use of cabling at times makes routing an exhausting exercise-cable routing is normally difficult.

## Tree Topology

This topology puts the features of bus and star topologies in one basket. In this topology, all computers are interconnected, but in a hierarchical manner. The top-most node in this topology is referred to as a **root node** whereas all the others are descendants of the root node. There exists just a single path between two nodes for the transmission of data-forming a parent-child hierarchy.

## Merits of Tree Topology

- It supports broadband data transmission over long distances without issues of attenuation.
- Star topology allows for easy expansion of a network since new devices can be added to an existing network with little difficulty.
- Ease of management-networks are segmented into star networks that make it relatively easy to manage.
- Errors can be detected and corrected with ease.
- Malfunctioning or breakdown of a single node does not affect the other nodes on the network. Thus, there is limited failure on tree topology networks.
- It supports point-to-point wiring of each and every network segment.

## Demerits of Tree Topology

- It is always difficult to handle issues in respect of a fault in a node.
- It’s a high cost network topology since broadband transmission can cost an arm and a leg.
- Failure or faults in the main bus cable affects the entire network.
- There is difficulty in reconfiguring the network when new devices are added onto the network.

## Mesh Topology

All computers are interconnected via redundant connections in this topology. It offers different (multiple) paths from one node to another.

In mesh topology, there are no connecting devices like switches or hubs. For instance, the Internet.

WANs normally are implemented with mesh topology since communication failures are of serious concern. It is also largely implemented in wireless networks.

The formula for forming mesh topology is shown below:

**Number of Cables = (z*(z-1))/2**

Where;

z = the number of nodes on the network

There are 2 categories of this topology:

## Partially Connected Mesh

In this topology, not all the network devices are linked to the devices with which they have frequent communications. The devices are only connected to some of the devices with which they are normally in constant communication.

## Full Mesh Topology

Each network device has a link to every other device in the network in full mesh topology. In simple words, all computers are connected to one another via the redundant connections.

## Merits of Mesh Topology

- Mesh topologies are highly reliable since a breakdown in one single connection does not affect the working of the nodes in the network.
- Communication is fast since each computer has connections with all other computers on the network.
- Addition of new devices has no effect on other devices on the network-making reconfiguration quite easy.

## Demerits of Mesh Topology

- Mesh topology networks have the capacity to accommodate more devices and transmission media than any other network topology. This translates to a high cost of setting up mesh networks than all other networks.
- Mesh topology networks are normally too large to manage and maintain effectively.
- A lot of redundancy on the network reduces the network efficiency significantly.

## Hybrid Topology

The amalgamation of different network topologies (at least two of them) result in another topology that is conventionally referred to as hybrid topology. It is a connection among different links and computers for data transmission.

A hybrid can only be formed by a combination of dissimilar topologies. For instance, a combination of bus and star topologies. However, a combination of similar topologies does not result in a hybrid topology.

### Advantages of Hybrid Topology

- An issue in one part of the network does not mess with the entire network.
- Hybrid topology allows network to be scaled further by addition of more devices without messing with the existing network.
- This network topology is quite flexible. An organization can customize the nature of its network to suit its specific network needs and interests.
- The network topology is highly effective since it can be designed in a way that network strength is maximized, and the limitations of the network are minimized.

### Disadvantages of Hybrid Topology

- The network topology is quite complex. Thus, it is too difficult to come up with a suitable architectural design of a network.
- It is highly costly since hubs used in this sort of computer network are different from the ordinary hubs. The hubs used in this topology are more expensive. Besides, the overall infrastructure is highly costly since a lot of cabling is required plus many more network devices.

## Network Types

The following are the four major classifications of computer networks based on size:

### Local Area Network (or simply, LAN)

A LAN refers to any group of computers that are linked to one another in a small area like an office or a small building. In a LAN, two or more computers are connected via communication media like coaxial cables, twisted pair cable or fiber-optic cable.

It is easy and less costly to set up a LAN since it can do just fine with inexpensive network hardware such as switches, Ethernet cables and network adapters. The limited traffic allows for faster transmission of data over LANs.

Besides, LANs are easy to manage since they are set up in a small space. Thus, even security enforcement is also enhanced through closer monitoring of activities within the network's geographical location.

### Personal Area Network (PAN)

This network is arranged and managed in the space of its user(s)-normally a range not exceeding 10m. It is typically used to connect computer devices for personal use.

Components of a personal area network include a laptop, mobile phone, media player devices as well as play stations. Such components are located within an area of about 30ft of a person's space.

The idea of PANs was born by one Thomas Zimmerman-the first lead research scientist to conceive the idea of personal area networks.

There are 2 classes of PANs:

- **Wired PANs**: a wired personal area network is created when a person uses a USB cable to connect two different hardware devices. For instance, it is common practice nowadays to connect a phone to a computer via a USB cable-to share files, access the Internet, and many other things.
- **Wireless PANs**: a wireless PAN is set up by the use of existing wireless technologies such as Bluetooth and Wi-Fi. This is basically a low-range technology network type.

### Examples of PANs

There are 3 common types of personal area networks:

1. **Body Area Network**: it moves with an individual. A good example is a mobile network-when one establishes a network connection and then makes a connection with a different device within their range.
2. **Offline Network**: it is also called a home network. It can be set up in a home-linked computer, TV, printers and phones-but is not connected to the internet.
3. **Small Home Office Network**: different devices are connected to the Internet and
