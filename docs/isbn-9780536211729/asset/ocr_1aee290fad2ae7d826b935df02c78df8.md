# iptables Syntax

A simple example of this is a rule pair for a local DNS server operating as a cache-forward name server. A DNS forwarding name server uses server-to-server communication. DNS traffic is exchanged between source and destination ports 53 on both hosts. UDP client/server relationship can be made explicit. The following rules explicitly outline outgoing (NEW) requests, incoming (ESTABLISHED) responses, and any (RELATED) ICMP error messages:

```
iptables -A INPUT -m state \
  --state ESTABLISHED,RELATED -j ACCEPT
```

```
iptables -A OUTPUT --out-interface <interface> -p udp \
  -s $IPADDR --source-port 53 -d $NAME_SERVER --destination-port 53 \
  -m state NEW, -j ACCEPT
```

DNS uses a simple query-and-response protocol. But what if an application can maintain an ongoing connection for extended periods, such as an FTP control session or a telnet or SSH session? If the state table entry is cleared out for some reason, future packets won't have a state entry to be matched or identified as part of an ESTABLISHED exchange.

The following rules for an SSH connection allow for that possibility:

```
iptables -A INPUT -m state \
  --state ESTABLISHED,RELATED -j ACCEPT
```

```
iptables -A OUTPUT -m state \
  --state ESTABLISHED,RELATED -j ACCEPT
```

```
iptables -A OUTPUT --out-interface <interface> -p tcp \
  -s $IPADDR --source-port $UNPRIVPORTS \
  -d $REMOTE_SSH_SERVER --destination-port 22 \
  -m state NEW, -j ACCEPT
```

```
iptables -A INPUT --out-interface <interface> -p tcp ! --syn \
  -s $IPADDR --source-port $UNPRIVPORTS \
  -d $REMOTE_SSH_SERVER --destination-port 22 \
  -j ACCEPT
```

```
iptables -A INPUT --in-interface <interface> -p tcp ! --syn \
  -s $REMOTE_SSH_SERVER --source-port 22 \
  -d $IPADDR --destination-port $UNPRIVPORTS \
  -j ACCEPT
```