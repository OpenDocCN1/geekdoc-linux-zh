
`www`      IN A  192.168.0.1

       IN A  192.168.0.2

       IN A  192.168.0.3

## 17.3 给急躁的人的 DNS

在开始详细介绍 DNS 之前，先简单回答大家最常见的问题：

- 如何向使用 DNS 的网络添加新机器？
- 如何将新机器作为客户端？

以下是菜谱式的方案，不涉及你的系统管理员策略。

## 向 DNS 中添加新机器

如果你的网络设置了动态主机配置协议 (`DHCP`)，可能不需要对 DNS 进行任何手动配置。当新计算机连接时，`DHCP` 服务器会告知它将使用的 DNS 服务器。对于不使用 `DHCP` 的网络，下面的方案显示了如何通过本地系统管理员或上游 ISP 选择空闲的主机名和 IP 地址来更新 DNS。

1. 在同一子网内识别一台类似的机器。你将使用该机器的记录作为新记录的模型。在本例中，我们使用 `208.77.188.0/24` 子网上的机器 `template.example.com` 作为模型。
2. 登录主名称服务器机器。如果你不知道哪台机器是主服务器，可能你不应该操作它，但可以使用 `dig` 命令（`dig domainname`）来识别它。（如果未安装 `dig`，也可以使用 `drill`。）
3. 对于运行 `BIND` 服务器的站点步骤：
    - 找到名称服务器配置文件，通常为 `/etc/named.conf`。
    - 在 `named.conf` 的 `options` 语句中，找到存储区域文件的目录行。区域文件包含实际的主机和 IP 地址数据。
    - 根据区域语句，验证此服务器确实是该域的主服务器（类型为 `master`，而不是 `slave` 或其他值）。如果是，你就找错了！
4. 为你的新 IP 地址创建适当的正向区域和反向区域文件。复制模板机器的记录并针对新机器进行修改。
5. 更新 `named.conf` 中的区域语句，指向你的新区域数据文件。
6. 重启名称服务器服务以应用更改。

### 为 DNS 添加新机器

```
zone "example.com" (
type master;
file "filename";
...
```

反向区域语句应该如下：

```
zone "188.77.208.in-addr.arpa" (
type master;
file "filename";
...
```

- 请记录下正向和反向区域定义中作为 `file` 参数列出的文件名。

运行 `NSD` 的站点的第 4b 步：

- 打开 `NSD` 配置文件 `/etc/nsd/nsd.conf`。
- 在 `nsd.conf` 中找到你域名的区域语句（使用 `name` 关键字标识每个区域）。
- 确认你确实位于主服务器上。你可以通过该域名的区域部分是否包含 `provide-xfr` 子句来判断。如果它包含 `request-xfr` 子句，则它是该区域的从服务器，你找错机器了。正向区域的区域语句应该如下：

```
zone:
name: example.com
file: /var/nsd/primary/example.com
provide-xfr: ip-addr tsig.key name
notify: ip-addr NOKEY
```

反向区域的语句如下：

```
zone:
name: 188.77.208.in-addr.arpa
file: /var/nsd/primary/188.77.208.in-addr.arpa
provide-xfr: ip-addr tsig.key name
notify: ip-addr NOKEY
```

- 请记录下正向和反向区域定义中作为 `zonefile` 关键字参数列出的文件名。

第 5 步：进入区域目录并编辑正向区域文件。找到你之前识别的模板主机记录。它们看起来如下：

| template | A | 208.77.188.100 |
| IN | MX | 10 mail-hub |
| IN | MX | 20 template |

# 第 17 章 DNS：域名系统

你的版本可能不包含用于邮件路由的 `MX` 行。你的区域文件也可能不包含 `IN` 符（它是默认的）或没有使用大写字母。

**第 6 步：** 复制这些记录并针对你的新主机进行相应的修改。区域文件必须按主机名排序；请遵循现有的约定。

**第 7 步：** 修改文件开头 `SOA` 记录中的序列号（`serial number`）——它是 `SOA` 记录中五个数字中的第一个。序列号应该只增不减。如果你的站点使用任意序列号，请在其加 1；如果你的站点使用日期作为约定，请将该字段设置为当前日期。

**第 8 步：** 编辑反向区域文件并查找如下所示的记录：

```
100 IN PTR template.example.com.
```

带有相应的更改并复制此记录。注意主机名后面有一个点点；不要省略它。如果你的反向区域文件显示的不仅仅是每个主机 IP 地址的最后一个字节，你必须按反序输入字节。例如，记录

```
100.188 IN PTR template.example.com.
```

对应 IP 地址 `208.77.188.100`（此处）。

**第 9 步：** 按照第 7 步所述，更新反向区域文件 `SOA` 记录中的序列号。

**第 10a 步：** 如果你使用 `B` 且比较懒，请运行 `rndc reload`。如果服务器很忙，你可以重新加载更改过的区域（或视图）：

```
$ sudo rndc reload forward-zone-name
$ sudo rndc reload reverse-zone-name
```

**第 10b 步：** 如果你使用 `NSD`，使用 `nsdc rebuild` 然后执行 `nsdc restart`。

**第 11 步：** 使用 `dig` 或 `drill` 检查配置；参见第 677 页。你也可以尝试 `ping` 你的新主机名或对其进行 `traceroute`，即使新主机尚未设置。“unknown”消息意味着你搞错了；“host not responding”意味着一切可能没问题。

常见的错误有：

- 忘记更新区域序列号（第 7 和 9 步）
- 忘记重新加载名称服务器（第 10 步）
- 忘记在反向区域 `PTR` 资源记录的主机名末尾添加点（第 8 步）

日期约定还包括一个两位更改数字，因此你每天可以进行 99 次更改。

# 配置 DNS 客户端

网络上的每个主机都必须是一个名称服务器客户端。你在 `/etc/resolv.conf` 文件中配置 DNS 客户端，该文件列出了当用户尝试解析主机名时（即请求网页、发送电子邮件或使用互联网时）主机查询的 DNS 服务器。

如果你的主机从 `DHCP` 服务器获取 IP 地址和网络参数，`/etc/resolv.conf` 文件将自动为你设置。否则，你必须手动编辑该文件。格式如下：

```
search domainname
option optionname ...
nameserver ipaddr
```

可以列出三个名称服务器。这里是一个完整的示例：

```
search atrust.com booklab.atrust.com
nameserver 63.173.189.1 ; ns1
nameserver 63.173.189.2 ; ns2
nameserver 63.173.189.3 ; ns3
```
