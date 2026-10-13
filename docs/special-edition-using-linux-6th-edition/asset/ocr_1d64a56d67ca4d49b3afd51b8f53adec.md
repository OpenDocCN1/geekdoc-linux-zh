# SOFTWARE CONSIDERATIONS

After the kernel is built, you can look over the system for software that isn’t required for operation. Extraneous software should be removed. This is especially true of compilers, games, and other unnecessary software. The use of the X Window software is discouraged because this binds to ports 6000–6255 (though most commonly just 6000–6010). If you feel that it is needed, consider using iptables to deny output on the untrusted network side. This includes nfs and other services that are not used or needed. If an intruder breaches the firewall, it doesn’t make sense to provide tools to use or services to activate, and most certainly not provide bridges to other systems.

The use of a secure shell (OpenSSH) program is also highly recommended. Running TCP wrappers on ports that are not forwarded and not used (normal services do not run on a firewall), as well as using Tripwire to watch files, is a good idea.

# OTHER CONSIDERATIONS

A firewall should not be considered a normal network host, and it should not be treated like one. This system should not enable normal users to log in or share files or directories on the network, and should never run RPC services such as NIS or NFS. The need to use good passwords for the accounts on the firewall, along with the necessity of using of shadow passwords, goes without saying. What might need to be said is that the firewall should not have the same password as any other host on your network. The fact that the host is broken and the attacker now has the password and shadow files should not automatically provide access to other hosts on the internal network.

This host needs to also be physically separated from the rest of the hosts, and placed in a secure area where unauthorized individuals cannot gain physical access to it. Any machine to which a knowledgeable individual has access can be broken, often in minutes. The case needs to be locked, and access to the system setup password must be protected.

# IPTABLES GENERAL INFORMATION

To understand how to proceed with iptables, you need to understand how iptables works. The next few sections walk you through some of the finer points. Most iptables text makes the assumption that all packets run through the tables, or list of rules. In fact, however, iptables only sees a packet if that packet is the first or only packet. Subsequent packet fragments do not traverse the rules. The reason for this is simple—a host cannot reassemble the fragments into a packet until it has the first packet. If the first packet is dropped, the others time out and are dropped. However, if you load conntrack, the connection tracking module, or are doing masquerading, the firewall will reassemble all packet fragments before doing anything with the packet.

Three default chains are built into netfilter. If you add the NAT code, two additional chains are created.