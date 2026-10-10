If a local news server is running on a machine in the DMZ, offering public service to select remote clients, a set of server rules allowing remote clients to connect to this machine's NNTP port is defined:

```
DMZ_NEWS_SERVER="192.168.1.70"
```

```
$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p tcp \
-s <my.news.client> --sport $SNUNPRIVPORTS \
-d $DMZ_NEWS_SERVER --dport 119 \
-m state --state NEW -j ACCEPT
```

If the local news server provides public Usenet newsgroups as well as local newsgroups, the local server requires a news feed from a remote server. The local server retrieves articles as a client to the remote server. The following rule allows access to a remote news server acting as a news feed:

```
NEWS_FEED="<my.remote.news.feed>"
```

```
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $DMZ_NEWS_SERVER --sport $SNUNPRIVPORTS \
-d $NEWS_FEED --dport 119 \
-m state --state NEW -j ACCEPT
```

# CHOKE NNTP CLIENT DMZ CONFIGURATIONS

The next rule allows local clients to access remote news servers in either the DMZ or on the Internet and would require a NEWS_SERVER constant to be defined:

```
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport $SNUNPRIVPORTS \
-d $NEWS_SERVER --dport 119 \
-m state --state NEW -j ACCEPT
```

# Telnet (TCP Port 23)

Some types of equipment, such as lower-end routers and other networking gear, allow only telnet connections for configuration. Therefore, you may find yourself forced to use it when you'd rather use a more secure protocol such as SSH.

The rules here allow LAN access to the DMZ machines using telnet. The DMZ hosts aren't allowed to connect to hosts in the LAN. The choke firewall is allowed telnet access to the LAN, however. You should not allow incoming telnet connections from remote sites; rather, you should use SSH to connect into the DMZ and then use telnet from the DMZ if you are absolutely forced to use telnet. These rules are applied to the choke firewall for telnet: