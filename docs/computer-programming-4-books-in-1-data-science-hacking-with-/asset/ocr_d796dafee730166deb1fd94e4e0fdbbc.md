+   - **Segmentation and reassembly**: this layer receives a message from its upper layer. It then splits the whole message into several small chunks. The layer assigns sequence numbers to each segment for identification.
+   
+   At the receiving end, the transport layer reconstitutes the segments based on the sequence numbers to form the original message.

+   - **Connection control**: there are 2 services that the transports offers: connectionless service and connection based.
+   
+   A connectionless service considers each segment to be a distinct packet. The packets travel through different routes to the destination. On the other hand, the connection-based service makes a connection with the destination machine's transport for before packets are delivered. In the connection-based service, all packets move in a single route.

+   - **Error control**: Just like in data control, this is achieved on an end-to-end basis-not across a single link. Transport layer at the source ensures that the message gets to its destination error-free.

+   - **Flow control**: this layer also ensures data control. The data control is done from end to end, but not across a one dedicated link.

# The Session Layer

This layer is used for the establishment, maintenance and synchronization of interaction between communicating network devices.

# Session Layer Functions

+   - **Dialog control**: this layer serves as a dialog controller. The layer achieves by initiating dialog between two processes. Alternatively, the layer can be said to authorize communication between one process and another. This can either be half-duplex or full duplex.

+   - **Synchronization**: the session layer adds checkpoints in a sequence during data transmission. In case of errors along the way, retransmission of data takes place from the specific checkpoint. The entire process is referred to as synchronization and recovery.

# The Presentation Layer

This layer primarily deals with the language and formatting of information that is transferred between two network devices. It is the network's “translator,"

The presentation layer is a section of the operating system. It is the portion of the operating