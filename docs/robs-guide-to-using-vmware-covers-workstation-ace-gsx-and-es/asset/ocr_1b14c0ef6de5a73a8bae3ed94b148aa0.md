also bridge a second network adapter, and use it so that the private and public networks are both bridged, or you can use a second host only network adapter so that the private and public adapters are both working host only. It is up to you to decide which option you prefer.

The first adapter that you assign to your virtual machines (at creation time) will become the public adapter in the setup that you create in this chapter. Therefore, assign your servers a fixed IP address (on the network adapter that is in another subnet to your private network) that you will use between your cluster nodes.

In this chapter I use the following setup:

Table 23.1: IP addressing for the Microsoft Cluster example.

|  | Node 1 | Node 2 | Cluster management |
|---|---|---|---|
| Public Network Adapter | 192.168.1.101 | 192.168.1.102 | 192.168.1.150 |
| Private Network Adapter | 10.0.0.101 | 10.0.0.102 |  |

# 23.2 Install Two Servers in a Single Domain

Cluster services require that all your cluster nodes are in the same Active Directory domain. DNS must be configured, and all the servers must be configured as member servers or domain controllers. If a server is configured as a member server, then it needs to have access to a domain controller in your network. Since we are going to create a two node cluster in this chapter, it is important to assign the role of domain controller to both servers, because we do not want to have a single point of failure.

# 23.3 Pre-Configuring the Servers

At this point you should have created your virtual machines and installed the two Windows Server 2003 servers in a single domain. Now we can start with the necessary preparations inside the server operating systems.

+   1. Rename the first network adapter.

You have installed the servers with one network adapter each. This first network adapter will be your public network adapter. So, we are going to rename that adapter accordingly in order to be able to identify it easier later on. Go to Control Panel → Network Connections and rename the adapter to Public Network Adapter.