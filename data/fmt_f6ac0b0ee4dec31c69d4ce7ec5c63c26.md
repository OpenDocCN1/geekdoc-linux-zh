
### 刷新过程

当需要刷新区域时，从服务器会查询出现在从服务器指令中的地址的每个主机的 DNS 服务器。当其中一个主机上的 DNS 服务器响应时，从服务器会比较其 SOA 记录中的序列号与查询服务器拥有的序列号。如果序列号不同，从服务器将用下载的副本替换其文件。

查询之间的间隔由 SOA 记录中的 `refresh` 字段控制。如果查询失败，从服务器将在 `retry` 字段指定的时间重试查询。如果在 `expire` 字段指定的时间还没有发生成功的查询，从服务器将丢弃其信息；在成功查询另一个服务器并检索最新文件之前，无法满足查询。

在大多数情况下，你应该只在 IP 列表中列出主服务器，以便旧数据传播。如果你决定在列表中列出从服务器，你应该确保主服务器是区域传输的首选，而从服务器作为备份，仅在主服务器长时间宕机时进行查询。

### db 文件

你必须为从服务器配置的 `db` 文件远少于主服务器维护的文件；实际上，只有 `db.127.0.0` 和 `db.cache`。这两个文件与域主服务器使用的文件完全相同。

从服务器也会自行维护若干 `db` 文件。这些文件保存了从主服务器和互联网其他 DNS 服务器下载的信息。由于从 DNS 服务器自行维护这些文件，你不需要深入研究它们。

到此，我们结束了如何配置从服务器的讨论。接下来，我们将描述如何配置主机使用你新建立的域名服务。

## 配置主机使用 DNS

到为止，我们已经向你展示了如何配置 DNS 服务器。然而，仍然有一个重要的问题：你如何让你的主机使用这个新服务呢？这个问题的答案位于配置文件中。在这种情况下，我们需要修改所有想要使用 DNS 的主机上的两个文件：`/etc/resolv.conf` 和 `/etc/host.conf`。

## 第12章：域名服务 – 从名称到 IP 地址 359

## /etc/resolv.conf

第一个要修改的文件是 `/etc/resolv.conf`。该文件指定了主机所属的域名，并列出了它可以联系以解析查询的服务器列表。它的内容如下：

```
domain           thisisanexample.com
search           anotherexample.com
nameserver       192.168.1.1
nameserver       192.168.1.100
```

该文件包含以下三个指令：

- **domain** – 设置主机搜索的域名。对于搜索时没有末尾点的名称（非完全限定域名），系统会自动在其后添加此域名。例如，如果你请求 DNS 搜索 `thor`，DNS 在执行搜索之前会将该名称翻译为 `thor.thisisanexample.com`。
- **search** – 指定要搜索的额外域名。上一个示例强制服务器在查找 `thisisanexample.com` 域名域之外，还要查找 `anotherexample.com` 域名下的所有主机。
- **nameserver** – 提供用作名称服务器的机器 IP 地址。上一个示例显示了两个 `nameserver` 指令：一个用于地址为 `192.168.1.1` 的机器（运行主 DNS 服务器的 `thor`），另一个用于地址为 `192.168.1.100` 的机器（运行备用 DNS 服务器的 `heimdall`）。这种形式适用于 `thor` 和 `heimdall` 本身以外的所有机器：因为这些主机各运行着 DNS 服务器，它们应该先指定本地回环接口（即 `127.0.0.1`），然后再指定另一台服务器。

在 SUSE 中，不建议直接编辑此文件。相反，你应该使用 YaST 为你进行设置，步骤如下：

1. 输入 `su` 进入超级用户 root ，然后输入命令 `yast` 启动 YaST。
2. 当 YaST 显示主菜单时，使用方向键选择“系统管理”（System administration）。
3. 当 YaST 显示系统管理菜单时，选择“网络管理”（Network administration）。
4. 当 YaST 显示网络管理菜单时，选择“配置名称服务器”（Configuration nameserver）。

## 第四部分：将 SuSE Linux 内网连接到互联网

![](img/2d491e465d582d1eb950efd30a94e3f9_385_0.png)

有关 YaST 的介绍请参见附录 A。
此时，YaST 会询问你是否访问名称服务器。按 Enter 键选择默认值 Yes（是）。
随后 YaST 会显示一个模板，你在其中输入要使用的名称服务器 IP 地址和其他要搜索的域名。这些内容分别对应 `nameserver` 和 `search` 指令。
输入信息后，使用方向键选择“继续”（Continue），然后按 Enter 键。YaST 将会处理设置 `resolv.conf` 的细节。

## /etc/host.conf

最后，你需要设置主机查找域名信息源的顺序。`/etc/host.conf` 文件决定了搜索源的顺序。例如：

```
order bind,hosts
multi on
```

`order` 指令设置了此主机搜索域名信息源的顺序。在上述的示例中，首先使用 DNS (`bind`)，然后使用 `/etc/hosts` 文件。制作名称服务器并不会让 `/etc/hosts` 文件消失。事实上，你仍然可以在其中查找名称——主机会先使用 DNS，如果 DNS 因任何原因失败，则会在 `/etc/hosts` 中查找该名称。
如果你已经在内网中配置了 DNS，我们建议首先使用 DNS，其次使用 hosts 文件。在任何情况下，我们都建议在 `/etc/hosts` 中尽可能保留少数条目，以消除配置错误。

## 开启 DNS

此时，你已经配置了内网的 DNS 服务器，配置了内网中的每台主机使用内网的域名服务和服务器，并配置了普通主机使用 DNS。现在是启动名为 `named` 的守护进程并对其测试了。
启动 `named` 最简单的方法是登录到配置了 DNS 服务器的系统，并从命令行调用 `named`：

```
/sbin/init.d/named start
```

## 自动启动 named

为了确保每次重启你的 SuSE Linux 系统时都自动启动 `named`，请使用 YaST 将配置变量 `START_NAMED` 设置为 `use`。如果你不知道如何使用 YaST 设置配置，请参阅附录 A 的指南。

## 重新读取配置文件

当你更改 `named` 的某个配置文件时，必须强制 `named` 重新读取它们，以便它使用新信息进行适当的重新配置。要强制 `named` 重新读取配置文件，请输入以下命令：

```
/sbin/init.d/named reload
```

到此，我们结束了如何在内网上配置和调用域名服务的讨论。接下来，我们将讨论如何使用 bind 包的工具来检查和调试你的域名服务。

## 检查和调试 DNS

既然我们已经讨论了如何设置 DNS，我们将回顾两个你在尝试调试名称服务器状态时经常会用的工具：`nslookup`，它返回主机的地址并执行调试任务，允许你观察过程的发生情况；以及 `host`，它是 `nslookup` 的简化版本。我们将逐一讨论。

### nslookup

`nslookup` 返回主机的地址并执行允许你实时观察过程的调试任务。`nslookup` 提供了两种模式：交互式和非交互式。要在交互式模式下使用 `nslookup`，只需输入 `nslookup` 而不带任何参数。这将为你提供一个提示符，你可以在其中输入命令。要在非交互式模式下使用 `nslookup`，输入 `nslookup` 后跟要查询的名称或 IP 地址。

### host

`host` 是 `nslookup` 的简化版本。它用于查找有关名称或 IP 地址的信息。要使用 `host`，输入 `host` 后跟你要查询的名称或 IP 地址。

## SERVER 和 LSERVER 命令

`nslookup` 的命令集更改了解析器的一个参数。例如，解析器默认查找 A 记录。然而，假设我们遇到向 `inetcorp.com` 投递邮件遇到问题。在这种情况下，A 记录无法帮助我们；相反，我们需要 MX 记录，以便我们可以看到哪个主机负责接收 `inetcorp.com` 的邮件。解析器的参数 `querytype` 设置了解析器检索的记录类型。因此，我们应该使用 `set` 命令将 `nslookup` 搜索的此参数从 A 改为 MX：

```
set querytype=mx
inetcorp.com
Server: localhost.thisisanexample.com
Address: 127.0.0.1
Non-authoritative answer:
inetcorp.com preference = 30, mail exchanger = ns0.inetcorp.com
inetcorp.com preference = 10, mail exchanger = smtp.inetcorp.com
inetcorp.com preference = 20, mail exchanger = gw.inetcorp.com
Authoritative answers can be found from:
inetcorp.com nameserver = gw.inetcorp.com
inetcorp.com nameserver = ns0.inetcorp.com
inetcorp.com nameserver = nic.near.net
inetcorp.com internet address = 172.16.1.87
inetmail.iss.inetcorp.com internet address = 172.16.2.94
gw.inetcorp.com internet address = 172.16.1.41
nic.near.net internet address = 192.52.71.44
```

这是我们针对一个不受管理的区域展示的第一个查询；这使得答案有所不同。请注意，`nslookup` 将答案标记为非权威的（nonauthoritative），然后给出可以从何处找到权威答案的名称服务器。正如俗说：“这里提供的答案来自 named 的缓存，自我上次查询以来可能已经发生了变化。如果这还不够，这里有一个可以让你获取真实结果的来源。”

如果你需要权威答案，可以使用 `server` 命令将你的默认名称服务器设置为列出的、能够返回 `inetcorp.com` 权威答案的服务器之一，然后重新执行查询。

- **server**: 更改你想切换的默认服务器。
- **lserver**: 恢复到 `nslookup` 启动时使用的服务器。
- **exit**: 退出 `nslookup`。

## 第四部分：将 SuSE 内网连接到互联网

## LS 命令

`nslookup` 的 `ls` 命令列出区域中的所有记录。这对于检查您的域名并确保在主服务器上正确设置一切非常有用。

`ls` 的语法如下：

```
ls [options] domain
```
