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