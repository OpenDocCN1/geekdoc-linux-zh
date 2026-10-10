
![](img/ba85bb40c695c02adae8cbd6666f2e0c_49_0.png)

### **Figure 2.3** An IPX packet.

*   (Type 17) NetWare core protocol packet
*   (Type 20) IPX NetBIOS broadcast

- **Destination Network**. The destination network to which the destination node belongs. If the destination is local, this field is set to 0.
- **Destination Node**. The destination node address.
- **Destination Socket**. The destination node’s process socket address.
- **Source Network**. The source network to which the source node belongs. If the source is unknown, this field is set to 0.
- **Source Node**. The source node address.
- **Source Socket**. The source node’s process socket address that transmits the packet.
- **Data**. The IPX data, often including the header of a higher-level protocol.

Keeping in mind the fields in Figure 2.3, now take a look at Figure 2.4 to compare the fields an actual IPX header captures during transmission.

```text
------ IPX Header ------
IPX:
IPX: Checksum = 0xFFFF
IPX: Length = 32
IPX: Transport control = 01
IPX: 0000 .... = Reserved
IPX: .... 0001 = Hop count
IPX: Packet type = 0 (Novell)
IPX:
IPX: Dest network.node = BBE1.006008AA7DE0, socket = 16410 (Unknown)
IPX: Source network.node = FF.1, socket = 16385 (IPX Message)

------ IPX Header ------
IPX:
IPX: Checksum = 0xFFFF
IPX: Length = 32
IPX: Transport control = 00
IPX: 0000 .... = Reserved
IPX: .... 0000 = Hop count
IPX: Packet type = 0 (Novell)
IPX:
IPX: Dest network.node = FF.1, socket = 16385 (IPX Message)
IPX: Source network.node = BBE1.006008AA7DE0, socket = 16410 (Unknown)
```

### **Figure 2.4** IPX header sniffer capture.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_50_0.png)

### **Figure 2.5** SAP flow network diagram.

## Service Advertisement Protocol

The Service Advertisement Protocol (SAP) is a method by which network resources, such as file servers, advertise their addresses and the services they provide. By default, these advertisements are sent every 60 seconds. A SAP identifier (hexadecimal number) indicates the provided services; for example, Type 0x0007 specifies a print server. Let's take a look at a real world scenario of SAP in Figure 2.5.

In this scenario, the print and file server will advertise SAP messages every 60 seconds. The router will listen to SAPs, then build a table of the known advertised services with their network addresses. As the router table is created, it too will be sent out (propagated) to the network every 60 seconds. If a client (Station A) sends a query and requests a particular printer process from the print server, the router will respond with the network address of the requested service. At this point, the client (Station A) will be able to contact the service directly.

**Hacker's Note** Intercepting unfiltered SAP messages as they propagate the network relinquishes valuable network service and addressing information.

| Operation | Source Type | Service |
| :--- | :--- | :--- |
| Network Address | Node Address | Socket Address | Hops |

*Note: The original text presents a table structure that seems to split columns. Based on standard SAP packet structure and the text description "Figure 2.6 A SAP packet", the table likely represents the fields.*

### **Figure 2.6** A SAP packet.

## SAP Format, Header Snapshots, Filters

SAP packets can contain service messages for up to seven servers. Should there be more than seven, multiple packets will be sent. Let's examine the SAP format and fields in Figure 2.6:

- **Operation.** The type of operation: a SAP request or response.
- **Source Type.** The type of service provided:
    - Type 0x0004: File Server
    - Type 0x0005: Job Server
    - Type 0x0007: Print Server
    - Type 0x0009: Archive Server
    - Type 0x000A: Job Queue
    - Type 0x0021: SNA Gateway
    - Type 0x002D: Time Sync
    - Type 0x002E: Dynamic SAP
    - Type 0x0047: Advertising Print Server
    - Type 0x004B: Btrieve VAP
    - Type 0X004C: SQL VAP
    - Type 0x0077: Unknown
    - Type 0x007A: NetWare VMS
    - Type 0x0098: NetWare Access Server
    - Type 0x009A: Named Pipes Server
    - Type 0x009E: NetWare-UNIX
    - Type 0x0107: NetWare 386
    - Type 0x0111: Test Server
    - Type 0x0166: NetWare Management
    - Type 0x026A: NetWare Management
- **Service.** Contains the unique name of the server.
- **Network Address.** The server's network address.
- **Node Address.** The node's network address.
- **Socket Address.** Server request and response socket numbers.
- **Hops.** The number of routers or gateways between the client and server.

Now that you have a grasp on SAP operation and its associated header format, let's compare the fields in Figure 2.6 with real-world captures (during transmission) of SAP headers shown in Figure 2.7.

To conserve network throughput and avoid SAP flooding, SAPs can be filtered on a router or gateway's interfaces. In medium to large networks, with hundreds and sometimes thousands of advertised services, SAP filtering to specific routers is sometimes mandatory. It is recommended to employ SAP filters for services that are not required for a particular network; for example, remote sites in most cases do not require SAP advertising for printer services at another remote site.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_52_0.png)

```text
------ NetWare General Service Response ------
SAP: Service type = 03ED (Intel NetFortExpress XL)
SAP: Server name = "XEROX_01_71"
SAP: Network = 00B71601, Node = 00AA005E136A, Socket = E480
SAP: Intermediate networks = 5
SAP:
SAP: Service type = 030C (HP LaserJet)
SAP: Server name = "0010831C20C583DANP11C20C5"
SAP: Network = 00B59321, Node = 0010831C20C5, Socket = 400C
SAP: Intermediate networks = 6
SAP:
SAP: Service type = 0077 (Unknown service)
SAP: Server name = "TS@BR_SERVER_59"
SAP: Network = 00C59321, Node = 000000000001, Socket = 0000
SAP: Intermediate networks = 7
SAP:
SAP: Service type = 044C (ARCS server 5.0)
SAP: Server name = "AR80214306BR_SERVER_59"
SAP: Network = 00C59321, Node = 000000000001, Socket = 8600
SAP: Intermediate networks = 7
SAP:
SAP: Service type = 004B (Btrieve VAP 5.x)
SAP: Server name = "BSER4.00-6.10_00C59321000000000000100000"
SAP: Network = 00C59321, Node = 000000000001, Socket = 8059
SAP: Intermediate networks = 7
SAP:
SAP: Service type = 0107 (NetWare 386)
SAP: Server name = "BR_SERVER_59"
SAP: Network = 00C59321, Node = 000000000001, Socket = 8104
SAP: Intermediate networks = 7
```

### **Figure 2.7** SAP header sniffer capture.

Hackers who can penetrate a router or gateway can bring medium to large networks down by removing or modifying SAP filters. So-called SAP flooding is a common issue when analyzing bandwidth degradation in a Novell environment.

## Sequenced Packet Exchange

The most common NetWare transport protocol is the Sequenced Packet Exchange (SPX). It transmits on top of IPX. Like TCP, SPX provides reliable delivery service, which supplements the datagram service in IPX. For Internet access, Novell utilizes IPX datagrams encapsulated in UDP (which is encapsulated in IP) for transmission. SPX is a packet-oriented protocol that uses a transmission window size of one packet. Applications that generally use SPX include R-Console and P-Console. We'll talk more about these applications later in this book.

## SPX Format, Header Snapshots

The SPX header contains sequencing, addressing, control, and acknowledgment information (see Figure 2.8). Its fields are defined as follows:

- **Connection Control**. Controls the bidirectional flow of data.
- **Data Stream Type**. Type of data in the packet:
    - Type 0xFE: End of connection notification
    - Type 0xFF: End of connection acknowledgment
    - Type 0x00: Client defined

| Connection Control | Data Stream Type | Source Connection ID |
| :--- | :--- | :--- |
| Destination Connection ID | Sequence Number | Acknowledgment Number | Allocation Number |

*Note: The original OCR table structure for Figure 2.8 is fragmented. Standard SPX header layout typically follows: Connection Control (1 byte), Data Stream Type (1 byte), Source Connection ID (2 bytes), Destination Connection ID (2 bytes), Sequence Number (2 bytes), Acknowledgment Number (2 bytes), Allocation Number (1 byte). The OCR split it into rows.*

### **Figure 2.8** An SPX packet.

- **Source Connection ID.** IPX-assigned connection ID number, at the source, during connection establishment. Used for demultiplexing (refer to Chapter 1).
- **Destination Connection ID.** IPX-assigned connection ID number, at the destination, during connection establishment. During the connection establishment request, this field is set to 0xffff. It is used for demultiplexing (refer to Chapter 1).
- **Sequence Number.** The sequence number of the most recently sent packet. Counts packets exchanged in a direction during transmission.
- **Acknowledgment Number.** Specifies the next packet's sequence number. Used for reliable delivery service.
- **Allocation Number.** Specifies the largest sequence number that can be sent to control outstanding unacknowledged packets.

After reviewing the SPX header format, let's compare these findings to actual captures during transmission, as shown in Figure 2.9.

## *Connection Management, Session Termination*

Remember the reliable delivery connection establishment in Chapter 1? SPX uses the same type of methodology, whereby connection endpoints verify the delivery of each packet. During connection establishment, an SPX connection request must take place. This is somewhat similar to the three-way-handshake discussed in Chapter 1. These connection management packets incorporate the following sequence:

1. Connection request.
2. Connection request ACK.
3. Informed Disconnect.
4. Informed Disconnect ACK.

Using this connectivity, SPX becomes a connection-oriented service, with guaranteed delivery and tracking. Note that, in addition to Informed Disconnect, there is another method of session called the Unilateral Abort; it is used for emergency termination.

## Watchdog Algorithm

After a NetWare client logs in to a NetWare server and begins sending requests, the server uses the Watchdog process to monitor the client's connection. If the server does not receive any requests from the client within the Watchdog timeout period, the server will send a Watchdog packet to that client. A Watchdog packet is simply an IPX packet that contains a connection number and a question mark (?) in the data portion of the packet. If the client's communications are still active, the client responds with a Y, indicating that the connection is valid. The *watchdog algorithm* is technology that
