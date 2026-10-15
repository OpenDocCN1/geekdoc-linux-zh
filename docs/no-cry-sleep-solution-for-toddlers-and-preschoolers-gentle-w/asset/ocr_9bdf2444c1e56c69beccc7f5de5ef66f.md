| Option | Function |
|---|---|
| [!] -V | Prints package version. |
| ! | Negates an option or address. |
| -m | Specifies a module to use, such as state. |
| --state | Specifies options for the state module such as NEW, INVALID, RELATED, and ESTABLISHED. Used to detect packet's state. NEW references SYN packets (new connections). |
| --syn | SYN packets, new connections. |
| --tcp-flags | TCP flags: SYN, ACK, FIN, RST, URG, PS, and ALL for all flags. |
| --limit | Option for the limit module (-m limit). Used to control the rate of matches, matching a given number of times per second. |
| --limit-burst | Option for the limit module (-m limit). Specifies maximum burst before the limit kicks in. Used to control denial-of-service attacks. |

TABLE 19-5 iptables Options (continued)

In the following example, the user adds a rule to the INPUT chain to accept all packets originating from the address 192.168.0.55. Any packets that are received (INPUT) whose source address (-s) matches 192.168.0.55 are accepted and passed through (-j ACCEPT).

```
iptables -A INPUT -s 192.168.0.55 -j ACCEPT
```

# Accepting and Denying Packets: DROP and ACCEPT

There are two built-in targets, DROP and ACCEPT. Other targets can be either user-defined chains or extensions added on, such as REJECT. There are two special targets used to manage chains, RETURN and QUEUE. RETURN indicates the end of a chain and returns to the chain it started from. QUEUE is used to send packets to user space.

```
iptables -A INPUT -s www.myjunk.com -j DROP
```

You can turn a rule into its inverse with an ! symbol. For example, to accept all incoming packets except those from a specific address, place an ! symbol before the -s option and that address. The following example will accept all packets except those from the IP address 192.168.0.45:

```
iptables -A INPUT -j ACCEPT ! -s 192.168.0.45
```

You can specify an individual address using its domain name or its IP number. For a range of addresses, you can use the IP number of their network and the network IP mask. The IP mask can be an IP number or simply the number of bits making up the mask.