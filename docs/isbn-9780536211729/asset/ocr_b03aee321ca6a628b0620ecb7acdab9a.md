# MATCH SYNTAX

The match examples require the -m or --match command to load the module, followed by any relevant match options.

# multipart filter TABLE MATCH EXTENSION

multipart port lists can include up to 15 ports per list. Whitespace isn't allowed. There can be no blank spaces between the commas and the port values. Port ranges cannot be interspersed in the list. Also, the -m multiport command must exactly follow the -p <protocol> specifier.

Table 6.12 lists the options available to the multiport match extension.

| Table 6.12 multipart Match Extension |
| m | --match multiport Option | Description |
| --source-port <port> [,port> | Specifies the source port(s). |
| --destination-port <port> [,port> | Specifies the destination port(s). |
| --port <port>[<port> | Source and destination ports are equal, and they match a port in the list. |

The multiport syntax can be a bit tricky. Some examples and cautions are included here. The following rule blocks incoming packets arriving on interface eth0 destined for the UDP ports associated with NetBIOS and SMB, common ports that are exploited on Microsoft Windows computers and targets for:

```
iptables -A INPUT -i eth0 -p udp -m multiport --destination-port 135,136,137,138,139 -j DROP
```

The next rule blocks outgoing connection requests sent through the eth0 interface to high ports using the TCP services NFS, socks, and squid:

```
iptables -A OUTPUT -o eth0 -p tcp -m multiport --destination-port 2049,1080,3128 --syn -j REJECT
```

What is important to note in this example is that the multiport command must exactly follow the protocol specification. A syntax error would have resulted if the --syn were placed between the -p tcp and the -m multiport.

To show a similar example of the --syn placement, the following is correct:

```
iptables -A INPUT -i <interface> -p tcp -m multiport --source-port 80,443 ! --syn -j ACCEPT
```