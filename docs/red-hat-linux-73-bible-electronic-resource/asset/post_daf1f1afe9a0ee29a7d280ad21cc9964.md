
## Example 2: Firewall for shared Internet connection (no servers)

In this scenario, the firewall is protecting a Linux system (firewall) and several systems on the LAN that only want to connect to the Internet. No servers are behind this firewall, so you want to prevent people from the Internet from requesting services.

You could use the same script shown in Example 1, but not use lines that request TCP services. So you could drop the user-defined chain in section 2 and drop the TCP rules from section 3. You could also remove the ICMP rules, if you don’t want your firewall to be invisible to ping requests (Type 8) and if you don’t care about receiving messages when my packets exceed their time to live values (Type 11), such as when a packet runs into a broken router.

## Example 3: Firewall for single Linux system with Internet connection

In this example, there is one network interface, connecting my Red Hat Linux system to the Internet. You are not sharing that connection with other computers and you are not offering any services from your computer.

In this case, you could cut sections 2, 4, and 6. From section 3, you could cut all rules relating to incoming requests from the LAN and all TCP services. As I mentioned in Example 2, you could also remove the Type 8 ICMP rule to make your firewall invisible to ping requests from the Internet and the Type 11 ICMP rule to not accept messages about failed time-to-live packets.

## Understanding iptables

Now that you’ve seen something about what iptables rules look like and how you can get them going, step back a bit and see how iptables works.
