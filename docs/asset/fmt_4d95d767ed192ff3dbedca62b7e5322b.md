
/usr/sbin/httpd -S

```
```

此命令的输出取决于选择的虚拟主机方法。
对于基于 IP 的虚拟主机，VIP 和 RIP 地址都会出现在此份报告中：

```
#/usr/sbin/httpd -t -DUMP_VHOSTS

VirtualHost configuration:

10.1.1.2:80 www.yourdomain.com (/etc/httpd/conf/httpd.conf:1215)

209.100.103:80 www.yourdomain.com (/etc/httpd/conf/httpd.conf:1225)
```

此示例输出表明 `httpd.conf` 中的第 1215 行包含了这两个虚拟主机 IP 地址的定义。
对于基于名的虚拟主机，此命令的输出看起来如下：

```
#/usr/sbin/httpd -t -DUMP_VHOSTS

VirtualHost configuration:

wildcard NameVirtualHosts and _default_servers:

*:* www1.yourdomain.com (/etc/httpd/conf/httpd.conf:1215)

*:* www2.yourdomain.com (/etc/httpd/conf/httpd.conf:1225)
```

此示例输出表明 `httpd.conf` 中定义了两个基于名的虚拟主机。当 Apache 在此服务器上作为守护进程运行时，它将能够响应来自客户端计算机的 HTTP 请求，并这两个虚拟主机提供内容。

## 如果 DNS 配置不当

> 如果你正在使用基于 IP 的虚拟主机并使用了 `UseCanonicalName` 指令，此命令将导致 Apache 对你在 `VirtualHost` 容器中指定的 IP 地址进行反向 DNS 查询。如果你的集群节点上没有正确配置 DNS，Apache 将将会报错：

```
10.1.1.2:80 Bogus_host_without_reverse_dns (/etc/httpd/conf/httpd.conf:1200)
```

此错误表明 `/etc/httpd/conf/httpd.conf` 中的第 1200 行包含的 IP 地址（在此例中为 10.1.1.2 RIP 地址）在 DNS 中找不到。

# 索引

## A

- 绝对路径名, 403
- 无 Active Directory 的账户管理, 342–343
- 对于集群, 189–190
- 在 SSH 中, 78–79
- ACID 技术, 366
- 活跃服务器配置, 154
- 活跃连接, 203
- Active Directory, 341–343, 361
- `addclients` 程序, 100, 105
- 地址解析协议 (`ARP`)
    - `GARP`, 122–125
    - 用于 LVS-DR 集群广播, 233–234, 236–238
    - 地址。*参见* IP 地址
- 管理网络, 113
- ADSL（非对称数字）用户线路, 26
- 高级电源管理, 22
- 建议锁, 280
- `aep1000` 脚本, 21
- 亲性, 250
- Heartbeat 中的警报, 157
- `alns` Heartbeat, 157–158
- Mon, 302, 319
- SNMP, 28
- IP 别名
    - 创建和删除, 120–121
    - 故障转移, 116
    - 在 `haresource` 文件中, 148–149
    - 在 Heartbeat 中, 116–125
    - 源地址, 117
    - 在 `linuxconf` 中, 382
- `anacron` 脚本, 21–23, 29
- Apache
    - 下的 CGI 程序, 286
    - 配置, 397–398
    - `BindAddress` 条目, 399
    - 在集群节点中, 400–403
    - `DocumentRoot` 条目, 398
    - `Listen` 条目, 399
    - 端口条目, 400
    - 在真实服务器中, 218–219
    - 自引用 URL, 403–404
    - `SourceName` 条目, 398
    - 验证, 404–405
    - 对于 Ganglia, 330, 332
    - 多余消息, 260
- `apcmaster`
    - 主设备, 168
    - 备设备, 168
    - `mart` 设备, 168
    - API (应用程序接口), 3, 396
    - `nd` 脚本, 22
    - `AppConfig` 模块, 97
    - 仲裁, 5, 280
    - 内内核, 280–283
    - 用于 NLM, 284–285
    - 可能的方法, 395–396
- ARP（地址解析协议）
    - `GARP`, 122–125
    - 对于 LVS-DR 集群广播, 233–234, 236–238
