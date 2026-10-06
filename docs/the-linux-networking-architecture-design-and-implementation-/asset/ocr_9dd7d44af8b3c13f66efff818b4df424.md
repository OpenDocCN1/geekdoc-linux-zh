# CHAPTER 19

# Packet Filters and Firewalls

# 19.1 INTRODUCTION

Each network packet handled by a Linux computer passes a number of distinctive points within the network implementation on its way through the Linux kernel before it either is delivered to a local process or leaves the computer for further routing. Direct access to the packet stream in the kernel opens up a large number of ways to manipulate packets, which are also suitable for implementing a security strategy in the network. For example, functions were built into the routing code early in the course of the Linux development. These functions allow the system administrator to influence how packets are handled, depending on their source and destination addresses. In addition to the pure filtering function, which lets you drop packets completely, this includes more complex manipulations, including address-conversion mechanisms (Network Address Translation-NAT) or the support of transparent proxies. After its introduction in the form of ipfwadm in Linux Version 1.2, this packet-filter code underwent two complete revisions to ensure better manageability, extension of the control options, and better integration of additional functionality (e.g., NAT). This chapter discusses the differences between the packet-filter architecture of the current Linux Version 2.4 and that of the previous Linux Version 2.2.

# 19.1.1 The Functional Principle of a Firewall

In its original meaning, the term firewall denotes a fire-resistant wall constructed to prevent the spread of fire. In connection with computer networks, a firewall is a protection mechanism used in a specific and exactly limited network (e.g., a corporate intranet) at a transition point from a neighboring network (generally to the Internet) to protect the intranet against dangers from the outside.

A firewall consists normally of two types of components:

+   * Packet filters are normally implemented in routers and monitor the entire network traffic flowing through these routers. These routers use a well-defined set of