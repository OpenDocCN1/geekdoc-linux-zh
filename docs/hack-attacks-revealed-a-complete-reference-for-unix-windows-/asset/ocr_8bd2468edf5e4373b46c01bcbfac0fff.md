Type 0xFF: End of connection acknowledgment

Type 0x00: Client defined

| Connection Control | Data Stream Type | Source Connection ID |

| Destination Connection ID | Sequence Number | Acknowledgment Number | Allocation Number |

**Figure 2.8** An SPX packet.

+   - **Source Connection ID.** IPX-assigned connection ID number, at the source, during connection establishment. Used for demultiplexing (refer to Chapter 1).
+   - **Destination Connection ID.** IPX-assigned connection ID number, at the destination, during connection establishment. During the connection establishment request, this field is set to 0xffff. It is used for demultiplexing (refer to Chapter 1).
+   - **Sequence Number.** The sequence number of the most recently sent packet. Counts packets exchanged in a direction during transmission.
+   - **Acknowledgment Number.** Specifies the next packet's sequence number. Used for reliable delivery service.
+   - **Allocation Number.** Specifies the largest sequence number that can be sent to control outstanding unacknowledged packets.

After reviewing the SPX header format, let's compare these findings to actual captures during transmission, as shown in Figure 2.9.

# *Connection Management, Session Termination*

Remember the reliable delivery connection establishment in Chapter 1? SPX uses the same type of methodology, whereby connection endpoints verify the delivery of each packet. During connection establishment, an SPX connection request must take place. This is somewhat similar to the three-way-handshake discussed in Chapter 1. These connection management packets incorporate the following sequence:

+   1. Connection request.
+   2. Connection request ACK.
+   3. Informed Disconnect.
+   4. Informed Disconnect ACK.

Using this connectivity, SPX becomes a connection-oriented service, with guaranteed delivery and tracking. Note that, in addition to Informed Disconnect, there is another method of session called the Unilateral Abort; it is used for emergency termination.

# Watchdog Algorithm

After a NetWare client logs in to a NetWare server and begins sending requests, the server uses the Watchdog process to monitor the client's connection. If the server does not receive any requests from the client within the Watchdog timeout period, the server will send a Watchdog packet to that client. A Watchdog packet is simply an IPX packet that contains a connection number and a question mark (?) in the data portion of the packet. If the client's communications are still active, the client responds with a Y, indicating that the connection is valid. The *watchdog algorithm* is technology that