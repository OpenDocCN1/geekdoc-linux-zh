# SUMMARY TABLE 26
BASIC FEATURES OF THE BOURNE, C, AND KORN SHELLS

| Feature | Bourne | C | Korn |
|---|---|---|---|
| Syntax compatible with sh | Yes | No | Yes |
| Job control | Yes | Yes | Yes |
| History list | No | Yes | Yes |
| Command-line editing | No | Yes | Yes |
| Aliases | No | Yes | Yes |
| Single-character abbreviation | No | Yes | Yes |
| Protect files from overwriting | No | Yes | Yes (noclobber) |
| Ignore Ctrl+D (ignoreeof) | No | Yes | Yes |
| Enhanced cd | No | Yes | Yes |
| Initialization file separate | No | Yes | Yes |
| Logout file | No | Yes | No |

| ISO/OSI Layer | Function |
|---|---|
| Data Link | Layer 2 splits data into frames for sending on the physical layer and receives acknowledgement frames. It performs error checking and retransmits frames not received correctly. |
| Network | Layer 3 manages the delivery of data via the Data Link layer and is used by the Transport layer. The most common network layer protocol is IP. |
| Transport | Layer 4 determines how to use the Network layer to provide a virtual error-free, point-to-point connection so that host A can send messages to host B, and they will arrive uncorrupted and in the correct order. |
| Session | Layer 5 uses the Transport layer to establish a connection between processes on different hosts. It handles security and creation of the session. |
| Presentation | Layer 6 performs functions such as text compression and code or format conversion to try to smooth out differences between hosts. Allows incompatible processes in the application layer to communicate via the Session layer. |
| Application | Layer 7 is concerned with the user's view of the network (that is, formatting electronic mail messages). The Presentation layer provides the Application layer with a familiar local representation of data independent of the format used on the network. |

# The Solaris Network Environment

In the ISO/OSI model, individual services that are required for communication are arranged in seven layers that build on one another. Think of the layers as steps that must be completed before you can move on to the next step and ultimately, communicate between systems. Summary Table 27 describes the function of each individual layer.

# SUMMARY TABLE 27
NETWORK LAYERS

| ISO/OSI Layer | Function |
|---|---|
| Physical | Layer 1 describes the network hardware, including electrical and mechanical connections to the network. |

# Network Definitions

Following are network definitions:

+   - Packet. A packet is the basic unit of information to be transferred over the network.
- Ethernet. Ethernet is a standard that defines the physical components a machine uses to access the network and the speed at which the network runs. It includes specifications for cabling, connectors, and computer interface components.