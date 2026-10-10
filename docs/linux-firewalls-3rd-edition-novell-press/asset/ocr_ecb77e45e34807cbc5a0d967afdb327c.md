Table 4.12 lists the control and data streams for a local client.

| TABLE 4.12 |  |  |  |  |  |  |
|---|---|---|---|---|---|---|
| RealAudio Protocol |  |  |  |  |  |  |
| DESCRIPTION | PROTOCOL | REMOTE ADDRESS | REMOTE PORT | IN/OUT | LOCAL ADDRESS | LOCAL PORT | TCP FLAG |
| Local client control request | TCP | ANYWHERE | 554,7070 | Out | IPADDR | 1024:65535 | Any |
| Remote server control response | TCP | ANYWHERE | 554,7070 | In | IPADDR | 1024:65535 | ACK |
| Local client TCP data request | TCP | ANYWHERE | 7071 | Out | IPADDR | 1024:65535 | Any |
| Remote server TCP data response | TCP | ANYWHERE | 7071 | In | IPADDR | 1024:65535 | ACK |
| Remote server UDP data stream | UDP | ANYWHERE | 1024:65535 | In | IPADDR | 6970:71709 | — |

The next rule pair establishes the control connection with the server:

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
    -m multiport --source-port 554,7070 \
    --syn -s $IPADDR --sport $UNPRIVPORTS \
    -m state --state NEW -j ACCEPT
fi
```

```
$IPT -A OUTPUT -o $INTERNET -p tcp \
  -m multiport --destination-port 554,7070 \
  --syn -s $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

```
$IPT -A INPUT -i $INTERNET -p tcp \
  -m multiport --destination-port 554,7070 \
  ! --syn -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

The next rule allows the preferred incoming UDP data stream from the server:

```
$IPT -A INPUT -i $INTERNET -p udp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 6970:7170 -j ACCEPT
```