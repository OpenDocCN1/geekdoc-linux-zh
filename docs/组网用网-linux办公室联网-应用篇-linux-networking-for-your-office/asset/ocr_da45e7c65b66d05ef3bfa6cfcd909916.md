If you’re using a distribution other than Red Hat 6.0, you might need to modify these directions somewhat, by changing the path to the Samba binaries or changing the method used to remove the existing Samba startup code.

# Workgroups, Domains, and Browsing

Windows networking is organized around the similar concepts of the workgroup and the domain. As a practical matter, you’re probably familiar with these concepts from browsing through the network with the Windows Network Neighborhood tool, shown in Figure 11.5. You might not know quite what workgroups and domains are, though, or how they differ from one another.

![](bbox=[0.24, 0.42, 0.62, 0.68])

FIGURE 11.5
Windows lets you browse a network in a hierarchical manner, as if it were a disk drive.

# What Are Workgroups and Domains?

Workgroups and domains are extremely similar networking structures in practice. They’re both groups of computers that use NetBIOS and SMB to share resources. Both feature machine names for individual computers and a name for the workgroup or domain. Even a small network can contain more than one workgroup or domain, although the network depicted in Figure 11.5 has only one. They differ primarily in how they handle authentication. A domain is more centralized; one computer in a domain serves as the domain controller, which is a computer that authenticates users on the domain. In contrast, in a workgroup, each machine is responsible for authenticating its users, and in passing that authentication information on to other machines in the workgroup.