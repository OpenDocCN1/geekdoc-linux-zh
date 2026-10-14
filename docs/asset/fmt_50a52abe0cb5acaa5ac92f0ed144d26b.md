
- 此规则允许用户连接到 MySQL 服务器（或任何其他绑定 3306 端口的服务器），使其穿过防火墙并进行伪装：

`iptables -t nat -A POSTROUTING -o eth2 -p tcp -j SNAT --to 209.127.112.3:3306`

- 此规则对 ICMP 流量进行伪装：

`iptables -t nat -A POSTROUTING -i -p ICMP -j SNAT --to 209.127.112.3`

- 以下五条规则将来自 80 端口、25 端口、POP3（110 端口）、FTP（21 端口）和 MySQL（3306 端口）的流量转发到相应的系统：

```
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 80 -j DNAT --to 192.168.10.2:80
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 25 -j DNAT --to 192.168.10.3:25
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 110 -j DNAT --to 192.168.10.3:110
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 21 -j DNAT --to 192.168.10.4:21
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 3306 -j DNAT --to 192.168.10.5:3306
```

- 接下来的四条规则稍微动点脑筋，将 Webmin 流量通过防火墙转发到 10000 端口上的相应系统。请注意 IP 与端口匹配的用法：

```
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10002 -j DNAT --to 192.168.10.2:10000
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10003 -j DNAT --to 192.168.10.3:10000
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10004 -j DNAT --to 192.168.10.4:10000
iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 10005 -j DNAT --to 192.168.10.5:10000
```
