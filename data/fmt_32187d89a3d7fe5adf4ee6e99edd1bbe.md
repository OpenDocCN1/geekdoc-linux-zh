
在此示例中，`QUESTION SECTION` 显示了查询的内容，`ANSWER SECTION` 显示了响应：域名 `ripe.net` 的 DNS 服务器列表。

`ADDITIONAL SECTION` 列出了某些 DNS 服务器的 IP 地址。关于查询的数据（如查询时间、回答查询的服务器和查询日期）列在输出末尾。

使用 `dig` 测试 DNS 解析结果的示例。

# nslookup 命令

`nslookup` 命令比 `dig` 和 `host` 命令更老。它可能会在未来的 BIND 工具版本中移除，但在当前版本中可以使用它来查询网络上服务器的 IP 地址或名称。

`nslookup` 命令的基本语法为：

`nslookup server_name/IP_address nameserver`

例如，输入 `nslookup dal.digitalairlines.com` 将返回回答查询的服务器 IP 地址以及所查询服务器的名称，如下所示：

```
$da10:~# nslookup da-host.digitalairairlines.com

Server: 172.17.8.101

Address: 172.17.8.101#53

Name: da-host.digitalairairlines.com

Address: 172.17.8.1
```
