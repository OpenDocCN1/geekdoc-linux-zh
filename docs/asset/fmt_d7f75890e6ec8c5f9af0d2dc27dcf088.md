
# 超级服务器

在提供众多网络服务的 Linux 系统上，同时运行 30 多个不同的服务会造成浪费。许多服务仅偶尔才需要。然而你仍然希望客户端对每个服务的请求都能得到处理，而无需你介入启动所需服务。解决方案是超级服务器（也称为元服务器），它监听多个网络端口，并在客户端为该端口建立连接时启动适当的服务。最广泛使用的超级服务器程序称为 `inetd`，即 Internet 守护进程。另一个日益流行的超级服务器是 `xinetd`，即扩展 Internet 守护进程。`xinetd` 是 Red Hat Linux 和 Fedora 的默认使用程序。

![](img/43f64015de86d989e30eff5bb284fb96_748_0.png)

> 有些网络服务不依赖超级服务器机制；它们设计为独立模式运行，而不会在新的客户端请求到达时由 `inetd` 或 `xinetd` 启动。

通常依赖超级服务器的网络服务示例有 `FTP`、`Telnet`、`SSH` 和标准电子邮件服务器。服务到默认端口号的映射通过 `/etc/services` 文件完成。

许多不同的程序都引用 `/etc/services` 来确定特定网络服务应使用哪个端口。超级服务器守护进程使用 `/etc/services` 中的端口号来确定应监视哪些端口以等待客户端连接。当客户端尝试连接到给定端口号时，超级服务器会启动适当的网络服务来处理客户端的请求。请求处理完毕后，网络服务会退出，从而将其资源释放给其他程序。唯一需要始终运行的程序是超级服务器本身。

`inetd` 和 `xinetd` 都使用 `/etc` 中的文本文件进行配置。配置文件指示超级服务器应监听哪些端口，以及如果客户端请求到达这些端口之一，超级服务器应启动哪个程序。`xinetd` 具有更复杂的配置模型和更好的安全性，而 `inetd` 在结合下一节中将学习的某些安全措施使用时也完全足够。

## 使用 xinetd

`xinetd` 程序是 `inetd` 的修订版，重点在于创建更安全的环境，并且其配置架构也更健全。随 Red Hat Linux 和 Fedora 一起提供的 `xinetd`（不包含 `inetd`）包含一个配置文件 `/etc/xinetd.conf`，该文件引用 `/etc/xinetd.d` 目录的内容。在该目录中，每个服务都由单独的文件配置。示例文件 `/etc/xinetd.d/wu-ftpd` 如下所示：

```
## default: on
## description: The wu-ftpd FTP server serves FTP connections.
It uses \
#normal, unencrypted usernames and passwords for authentication.
service ftp
{
socket_type= stream
wait= no
user= root
server= /usr/sbin/in.ftpd
server_args= -l -a
log_on_success+= DURATION USERID
log_on_failure+= USERID
nice= 10
disable= yes
}
```

`/etc/xinetd.d` 中每个文件的格式都命名一个服务，如上面的 `service` 行所示。方括号随后包含适用于该服务的选项。其中一些选项与下一节中描述的 `inetd.conf` 文件中的选项相匹配，例如 `socket_type`、`user` 和 `server`。还有几个选项扩展了 `xinetd` 的功能，超出了旧的 `inetd` 程序所提供的功能。例如，提供了各种日志选项来确定 `xinetd` 在尝试连接时写入系统日志的信息，以及多个安全选项来控制对服务的访问。例如，参数 `only_from`、`no_access`、`access_time` 和 `deny_time` 决定哪些主机可以访问服务以及何时可以访问。

`xinetd.conf` 的详细 man 手册描述了其可用选项。其中一个特别需要注意的选项是 `disable` 选项。Red Hat Linux 中的多个服务已完全配置但处于禁用状态，因此不接受任何连接。你可以通过将相应配置文件中的行更改为 `disable=no` 来启用它们。默认情况下，Red Hat Linux 中位于 `/etc/xinetd.d/` 的配置文件包含 `disable=yes` 行，以便服务在你手动更改此默认设置之前不处于活动状态（对客户端可用）。

对配置文件进行任何更改后，你还应重新启动 `xinetd`：

```
## service xinetd restart
```

## 使用 inetd

`inetd` 程序使用 `/etc/inetd.conf` 进行配置。以下是此文件的几行示例：

```
ftp      stream  tcp     nowait  root    /usr/sbin/tcpd in.ftpd -l -a
telnet   stream  tcp     nowait  root    /usr/sbin/tcpd in.telnetd
```

```
pop3    stream  tcp    nowait  root    /usr/sbin/tcpd ipop3d
imap    stream  tcp    nowait  root    /usr/sbin/tcpd imapd
telnet  stream  tcp    nowait  root    /usr/sbin/tcpd in.telnetd
```

你只需要关注 `inetd.conf` 中这些行的两个字段，即第一个和最后一个。最左边的第一个字段是服务名。该名称必须与 `/etc/services` 中的一个服务名相对应。服务名告诉 `inetd` 要监听哪个端口。每行最右边的项目定义了当客户端请求到达对应端口时 `inetd` 启动的服务器程序。

## TCP Wrappers

如果你回顾一下来自 `inetd.conf` 的示例行，你会注意到每行最后一部分，在要启动的服务器名称之前，包含文本 `/usr/sbin/tcpd`。这是一种安全机制。对于 `inetd` 管理的几乎每项服务，`inetd` 实际启动的程序都是 `tcpd`。`tcpd` 是一种名为 TCP Wrappers 的安全程序，它检查传入的网络连接并将其与配置文件进行比较，以确定是否允许该连接。如果允许，则启动“真正的”程序（如 `in.ftpd` 或 `in.telnetd`）。如果不允许，则简单地丢弃请求连接的数据包。

TCP Wrappers——`tcpd`——是一个应用级访问控制程序。它不是传统意义上的防火墙，因为它仅针对特定应用运行。理论上，TCP Wrappers 的安全性不如防火墙，因为相关的数据包已经在你的系统上运行的软件中被检查了。话虽如此，TCP Wrappers 提供了在已使用防火墙保护的系统上增加安全性的一种好方法。如果你对谁访问你的 Linux 系统有任何担忧，应该同时使用两者。

TCP Wrappers 由两个文件配置：`/etc/hosts.allow` 和 `/etc/hosts.deny`。这两个文件在控制对网络服务的访问时的交互关系如图 15-17 所示。开始使用这些文件很容易，但请注意，在依赖它之前应仔细测试配置。这种配置的灵活性意味着你可能并非按你所想的那样进行配置！格式很简单。你列出一个服务，后跟应允许或拒绝访问该服务的主机名或 IP 地址。还支持一些关键字，例如 `ALL` 和 `EXCEPT`。例如，假设 `hosts.deny` 文件包含以下行：

```
in.telnetd ALL
```

而 `hosts.allow` 文件包含以下行：

```
in.telnetd 192.168.
```

![](img/43f64015de86d989e30eff5bb284fb96_751_0.png)

## 图 15-17 通过 hosts.allow 和 hosts.deny 控制访问

你可以创建分配的复杂性。`ALL` 和 `EXCEPT` 关键字（以及其他几个）也可以在服务名字段中使用，以同时保护多个字段。例如，`hosts.deny` 文件可以包含以下行以阻止所有用户访问所有服务：

```
ALL ALL
```

每当你在 `inetd.conf` 文件中进行更改时，必须使用类似以下命令的系统脚本重新启动 `inetd` 程序：

```
## /etc/rc.d/init.d/inetd restart
```

请注意，`tcpd` 的默认操作是允许访问。首先检查 `hosts.allow` 文件，如果找到与待处理连接请求匹配的条目，则接受连接。如果未找到条目，则检查 `hosts.deny`。如果在那里找到条目，则拒绝连接；否则，接受连接。因此，对 TCP Wrappers 最安全的配置是先阻止所有用户访问所有服务，然后在 `hosts.allow` 中明确允许用户可以访问的任何服务，并对应 IP 地址、主机，甚至 `ALL` 指定。要了解这些选项，请仔细查阅 `hosts_access` 手册页。

![](img/43f64015de86d989e30eff5bb284fb96_752_0.png)
