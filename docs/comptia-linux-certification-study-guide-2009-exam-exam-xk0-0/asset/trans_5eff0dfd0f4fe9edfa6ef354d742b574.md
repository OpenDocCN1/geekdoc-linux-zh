
随后将有一系列行，用于指定域中的主服务器和从服务器，以及缓存语句。

```
:
:             domain              file
cache .                     named.ca
primary mydomain.com        named.hosts
primary 0.0.127.in-addr.arpa named.local
primary 10.100.100.in-addr.arpa named.rev
secondary my2dom.com        192.168.10.6 named.hosts
```

从第 8 版开始的 BIND 版本将包含相同的信息，但格式略有不同。下面展示了一个示例，说明了在较新版本的 named.conf 文件（通常位于 /etc 或 /etc/named.d）中如何设置主名称服务器或权威名称服务器：

```
zone "mydomain.com" IN {
    type master;
    file "mydomain.com.zone";
    allow-update {none;};
};
```

在较新的版本中，有一个名为 rndc 的控制实用程序，它允许你管理 named 守护进程。rndc 的配置文件是 /etc/rndc.conf，此外，你还需要在 /etc/rndc.conf 和 /etc/named.conf 中指定身份验证密钥，且两者必须匹配。你需要使用以下命令为这两个配置文件生成 HMAC-MD5 密钥：

```
dsnssec-keygen -a hmac-md5 -b <bit-length> -n HOST <key-file-name>
```

rndc 用于连接的默认端口是 953。一旦配置好命令，就可以使用 rndc 命令，其选项如表 9.1 所示。

### 表 9.1 rndc 选项

| 选项 | 描述 |
| :--- | :--- |
| `halt` | 立即停止 named 守护进程 |
| `refresh` | 刷新数据库 |
| `Reload` | 重新加载区域文件，但保留缓存文件 |
| `Stop` | 优雅地停止服务 |

## 练习 9.1：使名称服务器成为权威服务器

在本练习中，你将学习如何使从名称服务器成为某个域的权威服务器，当你即将停用现有的主名称服务器时，正在运行 Bind 9 的服务器即将被替换。

- 在从服务器的 `named.conf` 文件中，检查是否将你感兴趣的区域指定为从区域。
- 将 `type secondary` 更改为 `type master`。
- 将 `allow update` 选项更改为 `none`。
- 关闭主服务器电源，然后重新启动你刚刚更改为主服务器的服务器。
- 此时，这台新服务器应该已成为该域的权威服务器。

## 网络时间协议

NTP 是用于通过网络（包括互联网）同步计算机系统时钟的预定义协议。世界上有许多时间服务器，其时间源可以是原子钟或通过卫星接收器获取。获得的精度非常好，通常误差不超过几毫秒。与 DNS 服务器类似，存在一个层级结构，包括主服务器或一级（Stratum 1）时间服务器和从服务器或二级（Stratum 2）服务器。较低层级的服务器总是与较高层级的服务器同步。有大量的公共时间服务器可供选择，其中美国国家标准与技术研究院（NIST）和美国海军天文台（USNO）运营的时间服务器特别可靠。

在 Linux 系统中，有一个 NTP 客户端，它实现为一个持续运行的守护进程。由于计时的敏感性，该进程运行在内核空间。

NTP 的主配置文件是 /etc/ntp.conf，其中描述了你将同步的服务器以及哪些网络被允许同步到你的服务器。你需要定义多个服务器进行同步，以确保在网络或服务器故障时具有冗余性。要指定一对用于同步的服务器，需要修改 ntp.conf 文件如下：

```
server lerc-dns.lerc.nasa.gov # Stratum 1 server
server ntp.time.edu           # Stratum 2 server
```

然后，你必须限制你允许这些时间服务器访问的范围；例如，你不希望它们查询你的 NTP 服务器。

```
restrict lerc-dns.lerc.nasa.gov mask 255.255.255.255
nomodify noall no trap noquery
restrict ntp.time.edu mask 255.255.255.255 nomodify
notrap noquery
```

使用相同的命令，你可以允许本地网络上的主机查询你的时间服务器。

```
restrict 10.10.10.0 mask 255.255.255.0 nomodify
notrap
restrict 127.0.0.1
```

restrict 命令的使用可能会让人困惑；但应该将其理解为所有人都被允许查询你的服务器，而你只是在减少这种总体访问权限。此外请注意，在上面的代码中，本地主机（127.0.0.1）被允许完全访问。你需要使用 chkconfig 命令确保 ntpd 在启动时启动，并且首次使用 service 命令手动启动该服务。

```
chkconfig ntpd on
service ntpd start
```

为了轻松找到并使用 NTP 服务器，有一个服务器池供你使用。这些 NTP 池包含数百个公共 NTP 服务器，其运营商允许将其用于时间同步。你需要使用 DNS 名称 region.pool.ntp.org 来定义你想使用的池，其中 region 替换为你居住的国家或州。更多信息可在 www.pool.ntp.org 找到。实用程序 ntpq 可用于监控 NTP 守护进程以确定性能。该命令使用标准的 NTP 模式中的六种控制消息格式。使用 ntpq -p 可以查看当前正在轮询的时间服务器。

在较旧版本的 ntp 中，可以使用 ntpdate 设置本地日期和时间。此功能现在已集成到 ntpd 中，但旧版本仍在使用。该命令可以手动运行，或者通常在启动时自动运行。

## date 命令

date 命令可用于显示或设置未安装 NTP 服务器的系统上的日期。该命令的选项如表 9.2（date 选项）所示。

### 表 9.2 date 选项

| 选项 | 描述 |
| :--- | :--- |
| -a | 当时间发生漂移时调整日期。 |
| -u | 以 GMT 显示或设置时间 |
| -s datetime | 设置时间和日期 |

## 与 Windows 的互操作性

如今有大量的 Microsoft Windows 工作站和服务器在使用，与 Linux 的互操作性通常是系统管理员必须完成的重要任务。有许多实用程序可用于在系统之间共享文件，其中最常见的实用程序是 *Samba*。Samba 向所有服务器消息块/通用互联网文件系统（SMB/CIFS）客户端提供文件和打印服务，其中包括大多数版本的 Microsoft Windows 操作系统以及 Linux/UNIX 服务器和客户端。

> **注意**  
> SMB 是一种应用层网络协议，用作网络上不同机器之间的共享访问协议。Microsoft 修改了 SMB 的原始规范并产生了 CIFS，该协议在其产品中实施，直到 Microsoft Vista 发布（Vista 使用 SMB 2.0）。

## 远程桌面

在任何混合环境中，你可能需要管理 Linux 和 Microsoft *Windows* 客户端及服务器。在 Microsoft Windows 内部，有一个使用远程桌面协议（RDP）的远程桌面应用程序。在 Linux 中，可以使用开源产品 `rdesktop` 来显示目标桌面。这基于 X-Windows 系统。要连接到远程主机 http://hostname.myccorp.com（IP 地址为 10.10.100.23），可以使用以下任一命令：

```
rdesktop hostname.myccorp.com
rdesktop 10.10.100.23
```

> **注意**  
> 目标服务器或客户端必须启用远程桌面连接才能正常工作。此外，你可能需要提供适用于目标主机的用户名和密码凭据。该协议运行在 3389 端口，该端口需要在任何中间防火墙上保持开放。

## 虚拟网络计算

VNC 由 AT&T 开发，用于管理机器。这是一个客户端-服务器应用程序，目前有许多不同的版本，既有开源的也有商业版的。VNC 服务器本身通常内建于

