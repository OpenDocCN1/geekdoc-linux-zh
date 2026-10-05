# 318 Chapter 23 • Connecting to the Internet

Just replace the <local machine IP> with the IP of a particular machine. This line can occur as many times as needed for each machine that you want to allow to masquerade its IP. Keep in mind that we could also do this by manipulating the netmask instead of making an entry on a per machine basis. The per machine basis is easier to understand to the naked sys-admin eye, but a netmask is easier than your CPU.

So far, all that's set up is a simple masquerading firewall with For-warding rules. There are three other styles of rules: "Incoming, "Outgoing", and "A^accounting"

Incoming rules are generally the fastest of the rule types. Outgoing rules have a big advantage over Incoming and Forwarding rules, but they are slower in comparison of Incoming and Forwarding rules. Outgo-ing rules can block traffic from any machine on your network, while the out-ers cannot block traffic from the firewall itself. If you want to block traffic to a particular site, but your firewall machine itself is not secured from the indi-ividual in question, they could access a particular site by going to the firewall before going to the particular site.

Accounting rules do little other than allow you to monitor network traffic. The current version of ipfwadim will accept allow only you to measure traffic between two points. If you truly wish to monitor traffic I suggest monitoring all of the network traffic, and then the network traffic between the firewall and individual machines. This will give you a percentage of the traffic that one person, or machine, has created your network.

If you wish to block traffic to a particular site from your network, one approach could be

```
ipfwadim -F -a reject -W ppo -S 192.168.1.0/24 -D forbidden.site.com/32
```

The general format for all rules is the following. Please note that there are more options, including inserting rules, and logging that those mentioned here. this is just a brief overview of what is available

+   Flush the old rules to clear any previous erroneous rules.
* ipfwadim [-FIOA] -f
The "-f" means to flush all rules

+   Set up a default policy of deny.
* ipfwadim [-FIO] -p deny
The "-p" means policy standard values are accept (default) and deny.
Note: This does not apply to Accounting rules.