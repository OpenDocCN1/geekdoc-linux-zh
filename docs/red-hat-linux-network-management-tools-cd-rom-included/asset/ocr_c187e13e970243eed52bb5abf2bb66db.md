Using the **foreach** built-in command of the csh, a list of IP addresses is assigned between the parentheses. When **foreach** is executed, it calls the **snmpstatus** command and replaces each of the IP addresses with the variable $\mathit{node}$. In the output above, it is obvious that it is very easy to use this tool to probe the network. In practice, it would be more reasonable to build a shell script to inventory these devices on a more continued basis, rather than interactively from the command line. Also, the output could be placed in a text file for later review.

# Snmptable Tool

The **snmptable** command probes an agent and displays an MIB table using the SNMP $\textit{getnext}$-request operation. The syntax of the command is as follows:

```
snmptable [ common options ] [additional options] host community tableID
```

The minimum required arguments include host, community, and tableID. The tableID must be a real SNMP table, such as $\mathit{interfaces.iffable}$. The iffable table contains a series of MIB objects that contain performance information and other characteristics of the interfaces within a device. Within MIB-II, which is described in Chapter 6, “Overview of MIB-II,” the following tables are defined and can be displayed with this command:

+   * interface table ($\mathit{interfaces.iffable}$)
+   
+   * IP address table ($\mathit{ip.ipAddrTable}$)
+   
+   * IP routing table ($\mathit{ip.ipRouteTable}$)
+   
+   * IP net media table ($\mathit{ip.ipNetToMediaTable}$)
+   
+   * TCP connection table ($\mathit{tcp.tcpConnTable}$)
+   
+   * UDP listener table ($\mathit{udp.udpTable}$)

Note that Chapter 6 describes the MIB-II tree. The basic purpose of this command is to give the user the ability to display SNMP tables and import the data into other programs for additional reporting and manipulation. For example, to display the TCP connection table, $\textit{tcpConnTable}$, use the following command: