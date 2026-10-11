
`4000/tcp open remoteanything`

```
MAC Address: 00:0D:61:22:D3:11 (Giga-Byte Technology Co.)
Nmap run completed -- 1 IP address (1 host up) scanned in
```

输出显示在此地址扫描的 1653 个端口中有 6 个是关闭的（拒绝访问），6 个是开放的。未过滤的服务包括 TCP 端口 21, 22, 53, 80, 113 和 4000（这些是你之前在设置防火墙时开放的）。示例中显示为开放的七个服务都都有正在运行的服务器并在开放端口上进行监听。

你可能无法访问互联网上的 Linux 机器来测试到你计算机的访问。如果你在局域网内有另一台计算机，请尝试从那台计算机上运行 `nmap`。如果你只有 Windows 机器，你始终可以运行可启动的 Linux 并从那里尝试 `nmap`。

## 使用 iptables 进行 NAT 或 IP 伪装

你可以使用网络地址转换（`SNAT`）或 IP 伪装（`MASQUERADE`），允许局域网内具有私有 IP 地址的计算机通过你的 `iptables` 防火墙访问互联网。如果你为互联网连接有一个静态 IP 地址，请选择 `SNAT`。

# 第三部分 选择和安装 Linux 发行版

网络地址转换 (`DNAT`) 功能可将指向防火墙上特定端口的流量重定向到另一台计算机。

例如，如果你想将所有指向防火墙计算机 (`-d 15.15.15.15`) 的 Web 服务（端口 80）请求重定向到你局域网（LAN）上的另一台计算机（例如 `10.0.0.25`），你可以使用以下 `iptables` 命令：

```
# iptables -t nat -A PREROUTING -p tcp -d 15.15.15.15 --dport 80 \
-j DNAT --destination 10.0.0.25
```
