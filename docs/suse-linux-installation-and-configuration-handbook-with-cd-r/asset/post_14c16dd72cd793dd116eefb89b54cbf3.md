
The following is the output of the ping command before you set this rule:

```
# ping localhost
PING localhost (127.0.0.1): 56 data bytes
64 bytes from 127.0.0.1: icmp_seq=0 ttl=255 time=0.149 ms
64 bytes from 127.0.0.1: icmp_seq=1 ttl=255 time=0.124 ms
-- localhost ping statistics --
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.124/0.136/0.149 ms
```

The following is the output after you apply the rule:

```
PING localhost (127.0.0.1): 56 data bytes
-- localhost ping statistics --
2 packets transmitted, 0 packets received, 100% packet loss
```

As you can see, this causes 100 percent packet loss. Here's what happens inside the firewall. The firewall is looking at the packets on your machine. It picks up a packet, looks at its header, and tries to match it with the rules it has. You ping the machine, causing ICMP packets to be sent to your machine. The firewall picks up these packets, reads their headers, and finds out that these are ICMP protocol packets. The firewall then inspects the input family of rules and finds a rule for dealing with these packets. The rule tells the firewall to get rid of them, so the firewall simply gets rid of these packets and does not allow them to pass through to your network. Therefore, ping never gets a reply to the packets it sent because your machine never even received them, thanks to the firewall.

To remove this rule, just replace the -A with -D (for delete):

```
# ipchains -D input -p icmp -j DENY
```

If you ping yourself now, your machine will reply normally.

Let's see how you can enhance this rule. Say that a friend of yours is pinging your machine constantly with large packets. This will slow down your network connection because your machine will just sit there replying to the ping requests. You can block any incoming ICMP packets from only his IP. The following is the command for that, assuming his IP is 111.222.111.222:

```
#ipchains -A input -s 111.222.111.222 -p icmp -j DENY
```

The -s 111.222.111.222 argument tells ipchains to block from this source IP address. The rest of the arguments are the same as the previous command. What this rule is saying is “if you get any ICMP protocol packets from the IP address 111.222.111.222, get rid of them.” If someone else pings you, she will get a reply, but your friend is going to sit there wasting his network bandwidth trying to ping you, and you will never pay attention to him.

You also can control the packets' destination. For example, if you have a lot of users on your machine, you might not want them to be able to communicate with a certain machine. You can do this with the following command, assuming the machine is called badmachine.domain.com:

```
#ipchains -A input -d badmachine.domain.com -j DENY
```

All connections to this machine will be disallowed because you just told your firewall "do not accept any packets with the destination of (-d) badmachine.domain.com."

The -s and -d options can take IP address ranges as well as single IP addresses.

You can use the IP address/netmask combination to define entire networks. For example,

```
-s 123.123.123.0/255.255.255.0
```

signifies all IP addresses that start with 123.123.123—the 0/0 means everything, or all IP addresses.

You can specify ports and port ranges as well. For example, to define all ports from 1000 to 6000 for the IP address 123.123.123.123, the format would be as follows:

```
-s 123.123.123.123 1000:6000 -p TCP
```

To specify all ports up to 1000, you would use :1000, and to specify all ports starting with 1000 and up, you would use 1000:.

You can use ! (NOT) to inverse a match. For example, -s ! 123.123.123.123 signifies all IP addresses except 123.123.123. You can use ! in all the options—for example:

```
-d 123.123.123.123 ! 8080 -p TCP
```

This designates the IP address 123.123.123 and all ports except port number 8080. On the other hand, the following -d ! 123.123.123.123 8080 -p TCP means all IP addresses on port 8080 except IP address 123.123.123.

You must specify the protocol you want using the -p option. As you can see, the previous examples all dealt with the TCP protocol.

You even can specify the interface on which the rule will act by using the -i option. For example, to block ping requests that come to you through your dial-up connection, you use the following:

```
# ipchains -A input -i ppp0 -p ICMP -j DENY
```

This rule will act on the PPP interface called ppp0. If you have multiple interfaces that begin with the same name—for example, eth0 and eth1—you can use the plus sign (+) to group them:

```
# ipchains -A input -i eth+ -p ICMP -j DENY
```

This rule will apply to all interfaces that begin with eth.

The -j option can take DENY, ACCEPT, REJECT, MASQ, REDIRECT, and RETURN as options. You can get more information about each one of these from the ipchains man page (man ipchains).

## Saving Your Firewall Rules

All the rules you set will be lost when you reboot. You probably will want to save them and have them restored when the system boots up. This is easy; you can use the ipchains-save and ipchains-restore scripts. To save the firewall settings, add this line to your

```
/sbin/init.d/halt.local:
```

```
ipchains-save > /etc/firewall.rules
```

And to restore them on boot up, add this line to /sbin/init.d/boot.local:

```
ipchains-restore < /etc/firewall.rules
```

That's it. Your firewall settings will be saved and restored on boot up.

## Crash Course in ipchains Command-Line Arguments

The command ipchains has several command-line arguments you can use. The following is a brief list of the most common ones and what they mean:

- **-A**—This argument is followed by the name of a chain. It is used to append a new rule to the chain.
- **-D**—This argument is followed by the name of a chain. It is used to delete rules from the chain.
- **-R**—This command is used to replace a rule at some position in the chain. Position is the number of the rule you want to replace in that chain. For example, `ipchains -R input 2 ...` will replace rule number 2 in the input chain with the rule you are about to define.
- **-L**—This command can take the name of a chain and will list all the rules defined in that chain. If no argument is given, it will list all the chains, empty or not.
- **-N**—This command is used to create a new chain. This is a user-defined chain other than the default INPUT, OUTPUT, and so on. You can create your own chain of rules and use the -A to append rules to that chain. Then you can use that chain as a target for the -j argument.
- **-X**—This will delete a user-defined chain. The chain has to be empty, though. Delete all the rules you set in it.
- **-F**—This command takes the name of the chain as an argument. It then deletes all the rules in that chain.
- **-j**—This argument takes the name of an action of the chain. If the packet matches that rule, control is passed to that action of chain. You can, for example, enter the name of a user-defined chain. In that case, if the packet matches the rule, control will be passed to your chain.

-P—This command takes a name of a chain as an argument. It then sets an action as the default action (and only action) in this chain. For example, `ipchains -P input ACCEPT` will allow everything to pass.

These were the most commonly used command-line options for ipchains. You can get more detailed information from the man page (`man ipchains`).

## Troubleshooting

*I configured my network but I can't access any other machines.*

First check the physical side of the process. Are you sure that your network cable is properly connected? If you have another operating system installed, does it have network access? Are you sure that your network card is properly detected and running? You can find out from the output of the `ifconfig` command. Does it show an `eth0` device? If it doesn't show you one, restart the network and run the command `/sbin/init.d/network restart`. If you are using DHCP or BOOTP, check that their respective servers are up and running. Finally, is your route table properly configured? If the host you are trying to reach is on another network, you must have a gateway to that network.

*My network card doesn't seem to be supported. I can't find it in the list of cards.*

You might not find the exact name of the card in the list, so look for compatible cards. You should check the chipset of the card and try to find an entry that works for it. You can try the NE2000 family of cards because most cards are compatible with them. If none of them work, you can check to see whether there is a new release of the kernel; if there is, install it and try again.

*Now that my network is up, people can't access me using my hostname.*

You have to register your hostname with the network's DNS server. Ask your system administrator to do that for you. Hostnames are not like machine names in MS Windows—you must register them with a DNS machine.

*People can't telnet or FTP to my machine.*

Make sure that you turned on these services from YaST. Running the network service configuration module in YaST does this. You will find it in the menu choice System Administration, Network Configuration, Configure Network Services.
