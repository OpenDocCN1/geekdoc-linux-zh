
在这里，`eth`接口指的是无线网卡。我修改了加密密钥和其他参数以隐藏这些细节，但示例输出显示了当无线链路运行时你通常会看到的内容。

# 第 4 章：管理网络

## 本章内容

- 了解 TCP/IP 配置文件
- 检查 TCP/IP 网络
- 在启动时配置网络

和 Linux 中几乎其他东西一样，TCP/IP 设置是准备许多配置文件的问题（可以使用任何文本编辑器编辑的文本文件）。大多数这些配置文件位于`/etc`目录中。Linux 安装程序试图通过隐藏 TCP/IP 配置文件的详细信息来提供帮助。尽管如此，如果你知道文件的名称及其用途，那么在必要时手动编辑文件会更容易。

## 发现 TCP/IP 配置文件

在安装 Linux 时，可以配置 TCP/IP 网络。但是，如果你想有效地管理网络，你需要熟悉 TCP/IP 配置文件，以便在必要时编辑这些文件。（例如，如果你想检查域名服务器是否指定正确，你必须了解`/etc/resolv.conf`文件，它存储了域名服务器的 IP 地址。）

表 4-1 总结了基本的 TCP/IP 配置文件。我将在接下来的章节中描述这些配置文件。

### 218 发现 TCP/IP 配置文件

| 表 4-1 | 基础 TCP/IP 网络配置文件 |
| --- | --- |
| 此文件 | 包含以下内容 |
| `/etc/hosts` | 本地网络的 IP 地址和主机，以及你经常访问的任何其他系统 |
| `/etc/networks` | 网络名称和 IP 地址 |
| `/etc/hosts.conf` | 如何将主机名转换为 IP 地址的指令 |
| `/etc/resolv.conf` | 域名服务器的 IP 地址 |
| `/etc/hosts.allow` | 关于哪些系统可以访问你系统互联网的指令 |
| `/etc/hosts.deny` | 关于哪些系统必须拒绝访问你系统互联网服务的指令 |
| `/etc/nsswitch.conf` | 如何将主机名转换为 IP 地址的指令 |

![](img/7605650e62fab537998f2b973dbf5a26_243_0.png)

> 文本文件中的井号 (`#`) 表示注释。

### `/etc/hosts`

`/etc/hosts`文本文件包含本地区域的 IP 地址和主机名列表。在没有域名服务器的情况下，系统上的任何网络程序都会查询此文件以确定与主机名对应的 IP 地址。将`/etc/hosts`视为本地电话簿，你可以在其中查询本地主机的 IP 地址（而不是电话号码）。

以下是一个系统的`/etc/hosts`文件，显示了典型局域网上其他主机的 IP 地址和名称：

```
127.0.0.1 localhost.localdomain

# 局域网上的其他主机

192.168.0.100 lnbp933

192.168.0.50 lnbp600

192.168.0.200 lnbp200

192.168.0.233 lnbp233

192.168.0.40 lnbp400
```

如示例所示，文件中的每行都以 IP 地址开头，随后是该地址的主机名。（你可以为给定的 IP 地址设置多个主机名。）在某些发行版中，如 openSUSE 10.3，`/etc/hosts`文件具有以下内容：IP-完全限定主机名、短主机名。在所有情况下，主机名后的任何内容（如短主机名）都被视为别名。

### 发现 TCP/IP 配置文件 219

### `/etc/networks`

`/etc/networks`是另一个包含网络名称和 IP 地址的文本文件。这些网络名称通常用于路由命令 (`/sbin/route`) 以指定网络名称而不是 IP 地址。

如果你的 Linux 电脑没有`/etc/networks`文件，不要感到惊讶。TCP/IP 网络在没有该文件的情况下工作。事实上，Linux 安装程序不会创建`/etc/networks`。

### `/etc.hosts`

Linux 使用一个名为`/etc/hosts`的特殊库来确定 IP 地址。这是一个`/etc/hosts`示例：

（注：第 244-245 页的 OCR 文本非常混乱且重复。我保留了源文中提供的独特句子。）

### `/etc/resolv.conf`

`/etc/resolv.conf`是另一个用于解析器获取 IP 地址的文本文件。这是一个`/etc/resolv.conf`示例：

```
nameserver 8.8.8
nameserver 8.8.4
```

### `/etc/hosts.allow`

`/etc/hosts.allow`文件指定哪些主机可以访问你系统的互联网服务（如 TELNET 和 FTP）。在启动服务之前会查询它。只有`hosts.allow`文件中的条目意味着请求主机允许使用。

### `/etc/hosts.deny`

`/etc/hosts.deny`文件是`/etc/hosts.allow`的相反。当`hosts.allow`指定哪些主机可以访问你系统的互联网服务（如 TELNET 和 TFTP）时，`hosts.deny`文件标识了

# 检查 TCP/IP 网络 221

必须被拒绝服务的主机。如果`/etc/hosts.allow`文件中没有适用于请求主机的规则，则会查询`/etc/hosts.deny`文件。如果`hosts.deny`文件中有适用于该主机的规则，则拒绝服务。

`/etc/hosts.deny`文件中的条目格式与`/etc/hosts.allow`文件中的条目相同；它们采用`服务器:IP地址`的格式，其中`服务器`指提供特定 Internet 服务的程序名称，`IP地址`标识不被允许使用该服务的主机。

如果您已经在`/etc/hosts.allow`文件中设置了用以访问特定主机的条目，您可以在`/etc/hosts.deny`中放置以下行，以拒绝所有主机访问您系统上的任何服务：

```
ALL:ALL
```

要了解`/etc/hosts.deny`文件中条目的详细语法，请在终端窗口的 shell 提示符处输入`man hosts.deny`。

### `/etc/nswitch.conf`

`/etc/nswitch.conf`文件被称为名称切换（NSS）文件，它指定了解析器库、NIS、NIS+ 以及本地配置文件（如`/etc/hosts`和`/etc/shadow`）等服务如何交互。

NIS 和 NIS+ 是网络信息系统——另一种类型的名称查找服务。较新版本的 Linux 内核使用`/etc/nswitch.conf`文件来确定优先级：是本地配置文件、DNS（域名命名系统）等服务还是 NIS。

例如，`/etc/nswitch.conf`文件中的以下 hosts 条目表示，解析器库首先尝试`/etc/hosts`文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts: files nisplus dns
```

您可以在终端窗口中输入`man nswitch.conf`来获取更多关于`/etc/nswitch.conf`文件的信息。

## 检查 TCP/IP 网络

在配置以太网和 TCP/IP 后（无论 Linux 安装期间还是通过运行网络配置工具或命令），您就可以没有问题地使用各种网络应用程序了。如果遇到问题，Linux 包含了几个工具来帮助您监控和诊断问题。

### 222 检查 TCP/IP 网络

### 检查网络接口

使用`/sbin/ifconfig`命令查看当前配置的网络接口（或使用`ifconfig`，将 IP 地址与网络设备关联）。如果您在运行`ifconfig`时带有任何命令行，该命令将显示有关当前网络接口的信息。以下是使用`/sbin/ifconfig`的典型输出：

```
eth0 Link: Ethernet  addr:00:08:54:c1:c1:60
inet addr:192.168.1.2/24  mask:255.255.255.0
inet6 addr:fe80::201:74ff:fec60/64  Scope:Link
UP BROADCAST MULTICAST MTU:1500 Metric:1
TX packets:51683 errors:0 dropped:0 overruns:0 frame:0
RX packets:57487 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txuelen:10000
eth1 Link: Ethernet  addr:00:02:d8:bc:58:c5
inet addr:192.168.1.3/24  mask:255.255.255.0
inet6 addr:fe80:d402:d8ff:fedc60/64  Scope:Link
UP BROADCAST MULTICAST MTU:1500 Metric:1
TX packets:38333 errors:0 dropped:0 overruns:0 frame:0
RX packets:54262 errors:0 dropped:0 overruns:0 carrier:0
```
