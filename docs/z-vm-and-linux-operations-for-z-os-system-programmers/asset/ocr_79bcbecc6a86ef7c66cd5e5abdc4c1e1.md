```
UP BROADCAST MULTICAST MTU: 1500
vdev: 3000 type: QDIO ETHERNET portname: UNASSIGNED
ipv4 router type: NONROUTER ipv6: DISABLED
cpu: 0 forwarding: ENABLED
RX bytes: 3529660 TX bytes: 3354354
Ready; T=0.01/0.01 13:43:59
```

The NETSTAT commands show more detailed information about the system’s network. Issuing **NETSTAT** displays all the command options and a brief explanation of each. As an example, the NETSTAT GATE command displays the network gateway information, as shown in Example 5-18.

# *Example 5-18  Displaying network gateway information*

```
netstat gate
VM TCP/IP Netstat Level 530

Known IPv4 gateways:

Subnet Address   Subnet Mask      FirstHop Flgs PktSz Metric Link
--------------   ---------------  -------- -------- ------ --------
Default          <none>           9.12.4.1 UGS  1500   <none> OSA3020
9.12.4.0         255.255.252.0    <direct> UT   1500   <none> OSA3020

Known IPv6 gateways: None
Ready; T=0.01/0.01 13:55:46
```

# Checking system workload: indicate

The INDICATE LOAD command (abbreviated as **IND LOAD**) command gives an overview of the system resources uses. When issued from a class B user, the output is as shown in Example 5-19. The first line shows the average processor utilization, and the overall number of CPU in the system. Next three lines displays usage of expanded storage, minidisk cache and paging activity. Next four lines displays the number of users in each of four queues.

The last lines displays the current processor utilization. The system shown in the example was obviously doing nothing.

# *Example 5-19  Overview of system resources utilization*

```
ind load
AVGPROC-000% 04
XSTORE-000000/SEC MIGRATE-0000/SEC
MCD READS-000000/SEC WRITES-000000/SEC HIT RATIO-00%
PAGING-0/SEC STEAL-00%
```