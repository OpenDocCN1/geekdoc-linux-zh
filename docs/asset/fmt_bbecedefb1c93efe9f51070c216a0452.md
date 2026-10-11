
出于安全考虑，`ftp` 不可用于没有密码的登录。（我们指的是服务器端的登录名。你本人可以在没有密码的登录账户下工作，但你无法访问未受保护的远程账户。）此外，在 `/etc/ftpusers` 文件中，可以将用户列出为不允许使用 `ftp`。通常，出于安全考虑，`root` 会被列在该文件中。

运行 `RedHat 3.0.3` 发行版的计算机，在作为 `ftp` 服务器时，只有当安装了 `7.3-2` 版本的 `tcp-wrappers` 包时才可行（默认版本为 `7.3-1`；升级位于 CD-ROM 的 `updates` 目录中）。此外，必须安装包含 `ftp` 守护进程的 `wu-ftpd` 包。

除了 `ftp` 之外，其他一些网络服务也应该可以直接工作：`telnet` 或 `login`。出于安全考虑，通常可以直接以 `root` 身份登录。请尝试先用另一个名称登录，然后执行。

## 访问控制

如果你想精确控制谁被允许使用哪些网络服务，可以修改 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。这些文件中的语法为：`user:`

在 `hosts.allow` 中使用 `192.168.1.` 允许局域网的所有成员使用 `ftp`。在 `hosts.deny` 中使用 `ALL:ALL` 拒绝所有用户访问任何其他网络服务。`allow` 的优先级高于 `deny`；因此，对网络服务的访问在很大程度上受到了保护，防止了未经授权的访问。（此示例设置设置非常严格，例如，它不允许访问 `telnet` 和 `rlogin`。）

```
# /etc/hosts.allow
ftpd: 192.168.1.
# /etc/hosts.deny
ALL:ALL
```

在内部，访问控制通过 `tcpd` 执行，这是一个启动其他网络守护进程的守护进程。当请求网络服务时，`tcpd` 本身由 `inetd` 启动。配置存储在 `/etc/inetd.conf` 中。其中，有一行用于 `ftp` 的（默认）配置：

```
# a line from /etc/inetd.conf
ftp stream tcpd root /usr/sbin/tcpd -l -a
```

因此，当请求 `ftp` 服务时，`inetd` 根据 `inet.ftpd -l -a` 中的参数启动 `tcpd`。`tcpd` 首先评估 `hosts.allow`，如果请求的服务与模式匹配，则允许访问。如果没有找到匹配，`tcpd` 会检查 `hosts.deny` 文件，如果找到匹配行，则拒绝访问。如果 `hosts.allow` 和 `hosts.deny` 都不包含匹配项（即两者都为空），则 `tcpd` 允许访问。

## NFS 服务器配置

如果整个文件系统（或部分文件系统）需要配置，我们将简要处理一个相当简单的微型网络设置。必要的配置非常简单且易于遵循。

前提条件是计算机已经联网并按照上述描述进行了配置。对于所有计算机，必须使用相同的域名和广播地址。主机名和 IP 地址必须单独设置，例如（以三台计算机为例）：

- IP 地址：`192.168.1.5`, `192.168.1.6`, `192.168.1.7`

- 主机名：`jupiter`, `uranus`, `saturn`

- 通用域名：`galactic.network`

- 通用子掩码：`255.255.255.0`

- 通用广播地址：`192.168.1.0`

下一步是向 `/etc/hosts` 文件中插入自己的 IP 地址以及另外两台计算机的 IP 地址。因此，在所有计算机上，这些文件是完全相同的：

```
# /etc/hosts
127.0.0.1       localhost
192.168.1.5     jupiter.galactic.network jupiter
192.168.1.6     uranus.galactic.network uranus
192.168.1.7     saturn.galactic.network saturn
```

这确保了计算机在重启或重启网络程序后可以立即相互访问。在 `ping` 命令中，你可以指定 IP 地址、全名或短名（`/etc/hosts` 中的第三列）。如果不起作用，请检查接线是否正确、所有计算机的内核是否识别了以太网卡、以太网卡接口是否激活（使用 `config`）以及本地网络是否在路由表中（使用 `route`）。

```
# ping uranus
PING uranus.galactic.network (192.168.1.6): 56 data bytes
64 bytes from 192.168.1.1: icmp_seq=0 ttl=255 time=2.0 ms
64 bytes from 192.168.1.1: icmp_seq=1 ttl=255 time=1.2 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=255 time=1.2 ms
--- uranus.galactic.network ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 1.2/1.4/2.0 ms
```

直接写入软盘的前几个扇区。因此，软盘上没有文件系统，而是一系列的数据块。（如果在执行 `cp` 或 `dd` 命令之前已经存在文件系统，则它将被覆盖。）在这张软盘上，在不破坏第一个文件的情况下，无法存储任何其他文件。

创建启动软盘时，在 `rdev` 中指定正确的根分区至关重要（否则，内核将加载，但一旦运行，它将找不到包含 `LINUX` 文件系统的分区）。找到根分区正确名称（上例中为 `/sdb2`）最简单的方法是不带任何参数地调用 `rdev`。

接下来的两个 `rdev` 命令是可选的。通过第一个命令，你可以修改内核以使用扩展 `VGA` 模式。第二个命令导致文件系统首先以只读模式挂载。随后，`LINUX` 会检查系统是否有错误，如果是这种情况，它将进入读写模式。这可以为你节省好几个警告和错误信息。

在介绍 `LILO` 期间，你会发现也可以在软盘上安装 `LILO`。结果是一个所谓的 `LILO` 启动软盘，根据你的选择，它可能有自己的内核，也可以使用硬盘上的内核。在第一情况下，你获得了比这里描述的纯启动软盘更大的灵活性，因为你可以在启动期间指定启动选项。在第二情况下，你获得了速度，因为使用了硬盘内核。然而，你必须依赖于内核可以在硬盘的指定位置找到这一事实，而这并不正是启动软盘的初衷。更多细节请见第 170 页。

如果由于某种原因 `LILO` 无法启动且不存在软盘该怎么办？每个 `Linux` 发行版都允许你从软盘启动最小的 `LINUX` 系统（可以在 `DOS` 下创建），或通过 `root` 选项直接从 CD-ROM 启动，你可以指定使用已安装的 `LINUX` 的根分区，而不是软盘或 CD-ROM 上的最小系统。在大多数情况下，你的 `Linux` 系统的启动将成功。显然，你必须知道你根分区的名称（例如，如果 `Linux` 安装在第一个 `SCSI` 磁盘的第三个分区，则为 `root=/dev/sda3`）。你还可以在第 31 页和附录中找到关于从安装软盘启动的信息。

## 从 DOS/Windows 启动 LINUX (LOADLIN)

通过 `LOADIN.EXE` 程序，你可以从 `DOS` 启动 `LINUX`。`LOADIN` 是 `LILO` 的一个有趣的替代方案，尽管稍微慢一点。`LOADIN.EXE` 的最大优势是你不需要触碰引导区——这是 `LILO` 配置的一部分，但并非完全没有危险。例如，你可以配置 `Windows 95` 的启动文件，使得 `Windows` 启动程序根据你的选择启动 `DOS`、`Windows` 或 `LINUX`。如果你想在不重启电脑的情况下从 `DOS` 切换到 `LINUX`，也可以使用 `LOADIN`。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_186_0.png)

## 162 配置与管理

`LOADIN` 同样能够启动 `Umsdos`。`Umsdos` 是一种安装在 `DOS` 分区中的 `LINUX` 变体。在之前的版本中，无法通过 `LILO` 启动 `Umsdos`，必须使用一个名为 `LOADLIN` 的程序。在 `LOADIN` 和 `LOADLIN` 之间没有区别。较新版本的 `LILO` 也能启动 `Umsdos`（我还没有尝试过）。

你可以在随附的 CD-ROM 的 `deutils` 目录下找到 `LOADIN.EXE`。文件目录包含相应的 `C` 源代码，而 `LOADIN.doc` 包含了非常有价值的在线文档（可以从 `DOS` 读取）。

`LOADIN` 只能由 `DOS` 使用，不能从 `Windows` 使用。在启动 `LOADIN` 之前，始终退出 `Windows` 并切换到 `DOS` 模式！

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_187_0.png)

## 准备

使用 `LOADIN` 假设你知道根分区的设备名称。如果不确定，执行 `df` 并记录下挂载在挂载点 `/` 的文件系统名称（在本例中，将是 `/dev/sda15`）。
