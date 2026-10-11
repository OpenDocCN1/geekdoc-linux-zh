
```
ip saddr $DNS_SERVER ip daddr $NAME_SERVER \
ct state new accept
```

```bash
$nft add rule filter forward iif $SERVER_LAN_INTERFACE oif $EXTERNAL_INTERFACE \
tcp sport $UNPRIVPORTS tcp dport 53 \
ip daddr $NAME_SERVER ip saddr $DNS_SERVER \
ct state new accept
```
