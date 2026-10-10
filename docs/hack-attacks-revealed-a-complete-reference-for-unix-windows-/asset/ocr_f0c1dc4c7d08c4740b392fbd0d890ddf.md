+   - **Operation.** The type of operation: a SAP request or response.

+   - **Source Type.** The type of service provided:

+     - Type 0x0004: File Server
+     - Type 0x0005: Job Server
+     - Type 0x0007: Print Server
+     - Type 0x0009: Archive Server
+     - Type 0x000A: Job Queue
+     - Type 0x0021: SNA Gateway
+     - Type 0x002D: Time Sync
+     - Type 0x002E: Dynamic SAP
+     - Type 0x0047: Advertising Print Server
+     - Type 0x004B: Brieve VAP
+     - Type 0X004C: SQL VA
+     - Type 0x0077: Unknown
+     - Type 0x007A: NetWare VMS
+     - Type 0x0098: NetWare Access Server
+     - Type 0x009A: Named Pipes Server
+     - Type 0x009E: NetWare-UNIX
+     - Type 0x0107: NetWare 386
+     - Type 0x0111: Test Server
+     - Type 0x0166: NetWare Management
+     - Type 0x026A: NetWare Management

**Service.** Contains the unique name of the server.

**Network Address.** The server's network address.

**Node Address.** The node's network address.

**Socket Address.** Server request and response socket numbers.

+     - **Hops.** The number of routers or gateways between the client and server.

Now that you have a grasp on SAP operation and its associated header format, let's compare the fields in Figure 2.6 with real-world captures (during transmission) of SAP headers shown in Figure 2.7.

To conserve network throughput and avoid SAP flooding, SAPs can be filtered on a router or gateway's interfaces. In medium to large networks, with hundreds and sometimes thousands of advertised services, SAP filtering to specific routers is sometimes mandatory. It is recommended to employ SAP filters for services that are not required for a particular network; for example, remote sites in most cases do not require SAP advertising for printer services at another remote site.