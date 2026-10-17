
`dig` 输出中的部分包含问题部分和权威部分。结果显示了与你查询的域名相关的服务器名称和地址。`SOA` 记录标识 `0.10-in-addr.arpa` 为区域的权威。其他记录是 `10.0.0.network` 上反向映射的主名。代表 DNS 服务器 (`yourdomain.com`) 和局域网客户端 (`red`, `blue`, `green`, 和 `yellow`)。`nslookup` 命令是另一个你可以用于查找域名信息的工具。在下面的示例中，`nslookup` 查询解析 `ftp.yourdomain.com` 的服务器：

```
# nslookup -sil ftp.yourdomain.com

Server: 123.45.67.1

Address: 123.45.67.1#53

Name: ftp.yourdomain.com

Address: 123.45.67.3
```

`nslookup` 命令的输出包含响应请求的计算机及其 IP 地址，以及你请求的计算机的名称和地址。(`-sil` 选项防止了 `nslookup` 可能在 Fedora 和 RHEL 中显示的提示。) 尝试用 `nslookup` 查询 IP 地址（例如 `10.0.0.1`）以确保反向查找正常。

# 第四部分：Fedora 和 RHEL 的网络与服务器设置

```
# /etc/init.d/named status

number of zones: 5

debug level: 0

xfers running: 0

xfers deferred: 0

soa queries in progress: 0

query logging is OFF

server is up and running
```
