# Understanding Basic iptables

When you are running a firewall on a workstation, it’s typically not for protection of outside hosts; it’s to keep bad things from happening to your machine.

The simplest method on a Red Hat machine is to run the setup program (and select Firewall Configuration to run the lokkit program). In later versions, use the redhat-config-securitylevel program.

The interface enables you to set simple firewall rules that disallow any traffic other than the services you configure it to accept (see Figure 19.1).

![](bbox=[0.08, 0.33, 0.59, 0.49])

Figure 19.1 Firewall configuration interface.

The other and more complex method is to use the iptables command line to customize your rules for the allowing and denying of packets for the system. It’s when you run a firewall or boundary router with a firewall function on it that life and iptables gets much more interesting.

> Thankfully, the rules for **iptables** are not an exam item because it could take many pages along with much head-scratching and hmm’ing to get even seasoned but innocent sysadmins to understand how to write effective iptables rule sets. A thorough understanding of what’s going on will more than suffice, along with the ability to view your configuration.

For our purposes, a firewall that uses iptables is effectively made up of the following:

+   - **Chains**—Sets of rules that affect traffic.

+   - **Rules**—A criteria that attempts to match packets and send them to a target. If no match is found, the packet is inspected by the next rule in the chain.

+   - **Target**—It’s ACCEPT, DROP, QUEUE, or RETURN. A matched packet is accepted, dropped, queued for another chain, or returned to the parent chain.