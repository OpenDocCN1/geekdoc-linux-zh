
## 222 攻防 Linux 揭秘：Linux 安全秘密与解决方案

黑客进入 `Hunt` 中的 ARP 守护进程菜单并为两个主机设置了伪 MAC 地址：

```
-- arpspoof daemon - rcvpkt 2212, free/alloc 63/64 -----

s/k) start/stop relayer daemon

1/L) list arp spoof database

a) add host to host arp spoof      i/I) insert single/range arp spoof

d) delete host to host arp spoof      r/R) remove single/range arp spoof

t/T) test if arp spoof succeeded      y) relay database

x) return
```

在 `server` 上执行 `arp -a` 命令查看 ARP 缓存：

```
server$ arp -a
client (192.168.2.10) at 77:77:77:77:77:77 [ether] on eth0
nail (192.168.2.20) at 44:44:44:44:44:44 [ether] on eth0
```

在 `client` 上执行 `arp -a` 命令查看 ARP 缓存：

```
client$ arp -a
server (192.168.2.15) at 88:88:88:88:88:88 [ether] on eth0
nail (192.168.2.20) at 44:44:44:44:44:44 [ether] on eth0
gate (192.168.2.1) at 66:66:66:66:66:66 [ether] on eth0
```
