# Dividing a Network into Subnetworks

Take a look at the network in Figure 6-8.

![](bbox=[0.06, 0.28, 0.86, 0.42])

Network/netmask: 192.168.1.0/255.255.255.0

Figure 6-8 A large network shared by 100 users.

This network has 100 host computers connected to a single network, 192.168.1.0. Because all computers share the same physical network cable, the traffic load is likely to be quite heavy at peak hours. For example, if all marketing people start using the network at the same time as the engineers in the engineering department, things become very slow, as every host has to share the network bandwidth. So what’s the solution? Subnetworks. Now take a look at Figure 6-9.

Here we divide the 192.168.1.0 network into two networks — 192.168.1.0 and 192.168.1.128. Both of these subnetworks are connected to each other using a gateway (or router) with two network interfaces. When we configure each host computer on each of these two networks properly, we separate the network traffic between these networks. For example, when a user in the marketing department wants to communicate with another computer in the same department, the network traffic between these two computers remains in their network. The same is true for the engineering side. However, when users from different departments want to communicate with each other’s computers, it is allowed. The gateway computer forwards such inter-network traffic to and from these networks. The result is a speedier network because not all users are on the same, large network anymore. Now see how you can implement such a solution.