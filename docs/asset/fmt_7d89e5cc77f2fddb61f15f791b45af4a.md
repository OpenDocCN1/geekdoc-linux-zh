
```
iptables -A OUTPUT -p ALL -s 127.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 10.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 123.45.67.89 -j ACCEPT
```

# (6) POSTROUTING chain rules

```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 123.45.67.89
```
