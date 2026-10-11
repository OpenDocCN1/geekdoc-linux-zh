| **Table 15-8** | |
| --- | --- |
| **netstat Options** | |
| **Option** | **Use** |
| -r | Displays routing tables. |
| -i | Displays a table of all network interfaces. |
| -n | Displays numerical addresses. |
| -t | Displays TCP connection information. |
| -u | Displays UDP connection information. |
| --ip | Displays IP connection information. |
| -a | Displays all socket information. |

# ping

Earlier in this chapter, the operation of the ping utility was discussed. This utility is useful for troubleshooting problems in connectivity between hosts and on a local system. The ping utility when used with the loopback address (127.0.0.1, as mentioned earlier in this chapter) can verify the proper functioning of the TCP/IP protocol on a system. A successful ping of this address verifies that TCP/IP is installed and working on the local system. Successfully pinging the IP address of the local system verifies that the network adapter and TCP/IP are configured properly. Once you have pinged the local system successfully, the next step is pinging the default gateway; a response from that interface ensures that there are no cabling issues with the system and that it is able to access to the network.

All of these steps combined help isolate any problems that may exist in the network configuration of a system. Knowing which addresses to ping and what the response means can save valuable time in locating and resolving any network configuration problems.

# traceroute

The traceroute utility can also be useful when troubleshooting connectivity issues between hosts. By viewing the path data takes between the two hosts, you can see the point at which the communication is interrupted. Routing issues can be located using this command. One thing to look for is repeatedly seeing the same routers listed. Such repetition can mean that there is a routing loop due to an incorrect configuration. This information can be especially useful when calling your ISP or bandwidth provider with a problem. This information can also be used to determine where routing problems exist on your own network.