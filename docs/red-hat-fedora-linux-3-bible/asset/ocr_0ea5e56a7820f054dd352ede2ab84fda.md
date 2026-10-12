(6) POSTROUTING chain rules — The POSTROUTING chain defines rules for packets that have been accepted, but need additional processing. This is where the actual network-address translation (NAT) work takes place. For the NAT table (-t nat), in the POSTROUTING chain, all packets that go out to the Internet have their addresses translated to that of the firewall's external interface (-to-source 123.45.67.89). In this case I used the Source Network Address Translation (SNAT) chain because I have a static IP address (123.45.67.89) associated with my Internet connection. If I were using a dynamic IP address (via DHCP), I would use MASQUERADE instead of SNAT. I would also have to change any references to -d 123.45.67.89 to -i eth0. (Of course, you would be using a different IP address and possibly a different Ethernet interface.)

# Example 2: Firewall for shared Internet connection (no servers)

In this scenario, the firewall is protecting a Linux system (firewall) and several systems on the LAN that only want to connect to the Internet. No servers are behind this firewall, so you want to prevent people from the Internet from requesting services.

You could use the same script shown in Example 1, but not use lines that request TCP services. So you could drop the user-defined chain in section 2 and drop the TCP rules from section 3. You could also remove the ICMP rules, if you don't want your firewall to be visible to ping requests (Type 8) and if you don't care about receiving messages when your packets exceed their time to live values (Type 11), such as when a packet runs into a broken router.

# Example 3: Firewall for single Linux system with Internet connection

In this example, there is one network interface, connecting your Fedora system to the Internet. You are not sharing that connection with other computers and you are not offering any services from your computer.

In this case, you could cut sections 2, 4, and 6. From section 3, you could cut all rules relating to incoming requests from the LAN and all TCP services. As I mentioned in Example 2, you could also remove the Type 8 ICMP rule to make your firewall invisible to ping requests from the Internet and the Type 11 ICMP rule to not accept messages about failed time-to-live packets.

# Understanding iptables

Now that you've seen something about what iptables rules look like and how you can get them going, step back a bit and see how iptables works.

The iptables feature works by having IP packets (that is, network data) that enter or leave the firewall computer, traverse a set of chains that define what is done with the packet. Each rule that you add essentially does one of the following:

+   - Checks whether a particular criterion is met (such as that a packet requests a particular service or comes from a particular address)

+   - Takes an action (such as dropping, accepting, or further processing a packet)