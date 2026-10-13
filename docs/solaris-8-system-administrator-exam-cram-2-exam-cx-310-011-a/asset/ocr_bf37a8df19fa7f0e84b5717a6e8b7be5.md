+   - **Network or Internet**—The third layer is responsible for determining a path across the Internet between systems that want to communicate. It understands the data communication and switching technologies used to interconnect systems. This layer manages the network addressing and routing of data, locates the remote host based on its assigned IP address, and determines the data delivery path (the route) through the network. Data at this layer is typically referred to as *datagrams* or *packets*.

+   - **Transport**—The fourth layer provides end-to-end error recovery and flow control. These services provide reliability for the layer and ensure that the data is delivered without errors and in sequence without duplication. This layer controls data exchange and flow. Data at this layer is typically referred to as *packets*.

+   - **Application**—The fifth layer provides user utilities, such as remote login, file transfers, and so on. Data at this layer is typically referred to as *messages* or *streams*.

Figure 13.1 shows a side-by-side comparison of the OSI and TCP/IP networking models.

![](bbox=[0.116, 0.493, 0.539, 0.666])

**Figure 13.1** The OSI and TCP/IP network models.

# # TCP/IP Networking

The Solaris operating system supports the TCP/IP networking model. Although Solaris can use several types of networking hardware architectures, such as Ethernet, Token Ring, and Fiber Distributed Data Interface (FDDI), to communicate with other systems, Ethernet is the de facto networking architecture.