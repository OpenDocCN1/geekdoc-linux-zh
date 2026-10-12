
## 338 网络工具

### `finger` 和 `who`

`ping` 命令检测系统是否正在运行。`ping` 的参数是要检查的系统名称。如果你想检查一个宕机系统，`ping` 会发出超时消息，指示无法建立连接。下一个示例检查 `redhat.com` 是否连接到网络：

```
# ping www.redhat.com
PING from www.redhat.com (209.132.177.50) 56(84) bytes of data.
64 bytes from www.redhat.com (209.132.177.50) icmp_seq=1 ttl=118 time=36.7 ms
64 bytes from www.redhat.com (209.132.177.50) icmp_seq=2 ttl=118 time=36.9 ms
64 bytes from www.redhat.com (209.132.177.50) icmp_seq=3 ttl=118 time=37.4 ms

--- www.redhat.com ping statistics ---
4 packets transmitted, 3 received, 25% packet loss, time 3000ms
rtt min/avg/mdev = 36.752/37.046/37.476/0.348 ms
```

你也可以用 IP 地址代替名称使用 `ping`。使用 IP 地址时，`ping` 可以尝试直接检测远程系统，无需通过域名服务器将域名翻译为 IP 地址。这对于你的网络域名服务器可能临时宕机且你想检查网络上的主机是否已连接的情况非常有帮助。在下一个示例中，用户使用其 IP 地址检查红帽站点：

```
# ping 209.132.177.50
PING 209.132.177.50 (209.132.177.50) 56(84) bytes of data.
64 bytes from 209.132.177.50: icmp_seq=1 ttl=118 time=37.4 ms
64 bytes from 209.132.177.50: icmp_seq=2 ttl=118 time=37.0 ms
64 bytes from 209.132.177.50: icmp_seq=3 ttl=118 time=36.7 ms
```
