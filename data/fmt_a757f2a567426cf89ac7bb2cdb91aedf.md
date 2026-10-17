
在离开协议主题之前，我们应该快速提到反向 ARP协议（RARP）。正如其名称所示，它是 ARP 的相反。它不是请求 IP 地址，而是广播以太地址。`RARP` 使用 `ethers` 文件来映射以太地址到 IP 地址。它向客户端提供 IP 地址。一个示例 `ethers` 文件如下：

```
00:00:C4:3E:00:D3 duck
00:10:4B:87:00:D4 jay
00:20:82:F0:00:D5 raven
00:00:C4:38:00:B0 osprey
```

文件中的每一行包含一个以太地址，后面跟着主机名或 IP 地址。主机最常用，但它们必须是有效的名称。我们提到这个协议是因为第 4 章“Linux 服务”中的 `nsswitch.conf` 文件包含了它。然而，你不应该使用 `RARP`。`RARP` 只为客户端提供 IP 地址，不提供其他配置信息。这种 适用于大多数网络。

### 安装 DHCP 服务器

许多 Linux 发行版都包含了 DHCP 守护进程（`dhcp`），`dhcp` 只需要在服务器上运行。客户端不需要运行 DHCP。稍后提供配置 DHCP 信息。

`DHCP` 服务器软件是在初始安装时可以选择的组件。如果 `DHCP` 服务器没有作为初始安装的一部分，请现在使用包管理器（如 `rpm` 命令或 Windows 工具 `gmixer`）进行安装。如果你使用 `gnnorm`，可以在 `System/Daemons` 目录中找到 `dhcp`。

当然，你的 Linux 系统可能没有自带 DHCP 软件，或者你想要比系统自带更更新的版本。在任何情况下，你都可以从 `http://www.isc.org`（或通过匿名 FTP）的 `ftp.isc.org/dhcp` 下载 DHCP 代码。解压 tar 包，进入创建的目录，并运行那里的 `/config` 脚本。`configure` 会确定你运行的系统类型并为系统创建 `Makefile`。运行 `make` 来编译软件。（如果你使用的是过旧的 Linux 系统，请参考下文“在旧版 Linux 内核使用 DHCP”，有关你可能会遇到的问题）。在当前的 Linux 系统上，`dhcp` 应该可以无错误编译。当然，未来的发布可能会发生变化。如果你遇到错误，请向 `dhcp-server@isc.org` 邮件列表发送邮件，描述你的配置和遇到的具体问题。该列表大多数使用 DHCP 的人都会阅读，以及已经解决过你问题的人。要加入邮件列表，请访问 `www.isc.org/services/public/lists/dhcp-lists.html` 并填写表单。

### 在旧版 Linux 内核上使用 dhcpd

`dhcpd` 与 Linux 2.4 内核配合良好。然而，如果你的 Linux 系统使用了过时的内核，仅安装 `dhcpd` 可能不足以让其运行。在这种情况下，有一些潜在问题需要通过特定于系统的配置来解决。解决这些问题的最佳方法是更新到新内核。如果由于某些原因你不愿意更新内核，请阅读此侧边栏。

如果你为 Microsoft Windows DHCP 客户端提供服务，可能会遇到有限广播地址的问题。如果 Microsoft Windows 客户端似乎看不到服务器的 DHCP 消息，而其他类型的客户端可以看到，则你需要在你的 Linux 服务器上为有限广播地址定义特定的路由。为此，首先在 `/etc/hosts` 表中添加 `all-ones`：

```
255.255.255.255 all-ones
```

然后，为有限广播地址添加路由：

```
route add -host all-ones dev eth0
```

为了在每次启动后重新安装该特殊路由，请将路由语句添加到 `rc.local` 启动脚本中。需要此类内核的旧版发行版通常会在用于启动 `dhcpd` 的 `/etc/rc.init.d/dhcpd` 脚本包含包含有限广播路由的代码。

除了有限广播问题外，还有与其他旧版 Linux 内核相关的问题。

- **多网络接口**：在 2.0.31 之前的 Linux 内核上，`dhcpd` 无法使用多个接口。

- **SO_ATTACH_FILTER 未定义**：在 Linux 2.2 下编译 `dhcpd` 时可能会出现此错误。符号链接 `/usr/include/asm` 可能是的。此时链接应指向 Linux 的 `asm` 头文件。

- **协议未配置**：要在 Linux 2.1 和 2.2 下运行，`dhcpd` 需要在内核中配置 `CONFIG_PACKET` 和 `CONFIG_FILTER` 选项。如果在 `dhcpd` 启动期间显示消息 `Set CONFIG_PACKET=y and CONFIG_FILTER=y`，则你需要重新配置内核并启用这些选项。请参见第 13 章“故障排除”获取有关配置内核的信息。

- **IP BootP Agent**：Linux 2.1 仅在启用 BootP 代理的情况下才会运行 `dhcpd`。（BootP 代理是 `dhcpd` 的一部分。）检查 `/proc/sys/ipv4/ip_bootp_agent` 是否存在。如果存在，检查它是否包含 `1`。如果不存在或不包含 `1`，将该行插入启动脚本以创建 `ip_bootp_agent` 文件：

```
echo 1 > /proc/sys/ipv4/ip_bootp_agent
```

Linux 内核 2.4 解决了所有问题。然而，随着 Linux 内核版本的变化和 `dhcpd` 新版本的发布，可能会出现新问题。请查看 `dhcpd` 分发带的 `README` 文件获取最新信息。

### 运行 dhcpd

在 Red Hat Linux 7.2 中，DHCP 守护通过 `/etc/init.d/dhcpd` 脚本启动。该脚本接受与第 4 章描述的 `/etc/init.d/named` 脚本相同的参数。常用的参数有 `start`、`stop` 和 `restart`。例如，以下命令将启动 `dhcpd`：

```
[root]# service dhcpd start
Starting dhcpd: [ OK ]
```

使用如 `chconfig` 或 `lksys` 等工具来确保每次系统重启时都会运行 `/etc/init.d/dhcpd` 启动脚本。在我们的示例 Red 系统，以下 `chconfig` 命令会导致 `dhcpd` 在系统处于级别 3 或 5 且重启时运行时运行：

```
[root]# chconfig --list dhcpd
dhcpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root]# chconfig --level 35 dhcpd on
[root]# chconfig --list dhcpd
dhcpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

`/etc/init.d/dhcpd` 脚本使用 `dhcpd` 命令启动 DHCP 服务器。`dhcpd` 命令的语法为：

```
dhcpd [-p port] [-f] [-d] [-q] [-cf file] [-lf file] [interface-list]
```

- **`-p`**：定义备用端口。通常，`dhcpd` 在端口 67 上监听客户端请求，并在端口 68 上响应。使用 `-p` 选项更改为非标准端口。

- **`-f`**：作为前台进程运行 `dhcpd`。这用于调试。

- **`-d`**：将错误消息发送到 `stderr` 而不是 `syslog`。

- **`-cf`**：指定 `dhcpd` 应从哪个文件读取配置。默认情况下，`dhcpd` 从 `/etc/dhcpd.conf` 读取配置。

- **`-lf`**：指定 `dhcpd` 应向哪个文件写入租信息。默认情况下，`dhcpd` 将租信息写入 `/var/lib/dhcpd/leases`。

- **`interface-list`**：列出 `dhcpd` 应监控的接口名称。默认情况下，`dhcpd` 监听所有支持广播的接口。

要在 Red 系统上设置 `dhcpd` 命令行参数，请在 `/etc/sysconfig/dhcpd` 文件中参数。`/etc/init.d/dhcpd` 脚本在启动守护进程之前会从该文件读取参数。例如，创建一个 `/etc/sysconfig/dhcpd` 文件，包含以下内容：

```
DHCPARGS=-cf /var/lib/dhcpd/test.conf
```

这导致 `dhcpd` 从 `/var/lib/dhcpd/test.conf` 读取其配置，但 `/etc/dhcpd.conf` 文件仍然是！

### 初始化 dhcpd.leases 文件

`dhcpd` 将其分配的租约数据库存储在 `/var/lib/dhcpd/leases` 中。为了让 `dhcpd` 启动，该文件必须存在。当首次安装时，创建一个空的 `dhcpd.leases` 文件以确保守护进程正确启动。`dhcpd` 以 ASCII 文本格式写入条目。如果你感兴趣，可以查看文件查看分配了哪些租约。文件中的条目格式如下：

```
lease address (statements)
```

每个租约都以 `lease` 关键字和分配的 IP 地址开始。随后是一组定义租约特征的语句。语句列表中可能出现的值包括：
