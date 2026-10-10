would also have to change any references to `-d 123.45.67.89` to `-i eth0`. (Of course, you would be using a different IP address and possibly a different Ethernet interface.)

# EXAMPLE 2: Firewall for Shared Internet Connection (No Servers)

In this scenario, the firewall is protecting a Linux system (firewall) and several systems on the LAN that are only used to connect to the Internet. No servers are behind this firewall, so you want to prevent people from the Internet from requesting services.

You could use the same script shown in Example 1, but not use lines that request TCP services. So you could drop the user-defined chain in Section 2 and drop the TCP rules from Section 3. You could also remove the ICMP rules, if you don’t want your firewall to be visible to ping requests (Type 8) and if you don’t care about receiving messages when your packets exceed their TTL values (Type 11), such as when a packet runs into a broken router.

# EXAMPLE 3: Firewall for Single Linux System with Internet Connection

In this example, there is one network interface, connecting your CentOS system to the Internet. You are not sharing that connection with other computers, and you are not offering any services from your computer.

In this case, you could cut Sections 2, 4, and 6. From Section 3, you could cut all rules relating to incoming requests from the LAN and all TCP services. As I mentioned in Example 2, you could also remove the Type 8 ICMP rule to make your firewall invisible to ping requests from the Internet and the Type 11 ICMP rule to not accept messages about failed TTL packets.

# Understanding iptables

Now that you’ve seen something about what iptables rules look like and you can get them going, step back a bit and see how iptables works.

The iptables feature works by having IP packets (i.e., network data) that enter or leave the firewall computer traverse a set of chains that define what is done with the packet. Each rule that you add essentially does both of the following:

+   Checks whether a particular criterion is met (such as that a packet requests a particular service or comes from a particular address).

+   Takes an action (such as dropping, accepting, or further processing a packet).

Different sets of rules are implemented for different types of tables. For example, tables exist for filtering (filter), network address translation (nat), and changing packet headers (mangle). Depending on the packet’s source and destination, it traverses different chains. Most of the rules you create will relate to the filter table, which is implied if no other table is given.

The chains associated with the filter table are INPUT, OUTPUT, and FORWARD. You can add user-defined chains as well. You will probably be most interested in adding or removing particular TCP and UDP services using the basic rules shown in the previous example. Assign ACCEPT