10. Each of these commands will take some time to finish executing, and a lot of text will scroll by—don't worry, this is normal. When all the commands have executed, reboot your system to load the new kernel.

When your system reboots, you can make sure that it worked by checking for the existence of the file /proc/net/ip_fwchains; you should find it now.

# Configuring the Firewall

The firewall is configured using the ipchains command. The configuration is pretty simple; you just need to know what you want to do. Using a firewall, you can control access to certain IP addresses, ports, and protocols. You can block their access or allow it, depending on what you want.

The firewall intercepts every packet that flows through your machine. The firewall then reads the packet's header, which contains information about where this packet came from and where it's going. Then, using some rules, the firewall decides what to do with this packet. These rules are what you will configure, and by doing so, you will be able to tell the firewall something like “all packets coming from www.badsite.com should not be allowed to get through,” or “do not answer any ping requests, ignore them.”

The firewall has three main families of rules: input, forward, and output. The input rules are first processed when a packet is being inspected; if any rule matches that packet, action is taken. Otherwise, the packet makes it to the forward family of rules, where again, if it matches any of its rules, action is taken. Finally, if the packet makes it through the forward family of rules, it is inspected by the output family. If all rules fail to match, a default action is executed. On well-configured firewalls, this default action is usually to reject the packet, just to be safe.

Let's look at some examples of how you can configure a firewall. You use the ipchains command to dictate rules to the firewall. Let's use blocking ping requests as an example. A ping request uses a protocol called ICMP—when someone pings your machine, they send you a certain type of ICMP packet. After your machine receives the packet, it replies with another type of ICMP packet. Ping is used to determine whether a remote machine is alive or not. You can block such ping packets from ever reaching your machine using the following command:

```
# ipchains -A input -p icmp -j DENY
```

The command looks cryptic, doesn't it? Not to worry; enlightenment is on the way. The first argument to the command -A input tells ipchains to add a rule to the input family of rules (-A is add). The second argument is -p icmp, which tells ipchains the ICMP protocol is being used (-p for protocol). Finally, -j DENY sets denying the package as the action to be taken (-j for jump to). In other words, this command is saying “Here's a rule to add to the input family of rules: If you ever see a packet that uses the ICMP protocol, get rid of it”.