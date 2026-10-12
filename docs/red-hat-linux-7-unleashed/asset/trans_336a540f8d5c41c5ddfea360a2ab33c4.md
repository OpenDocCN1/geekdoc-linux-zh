
![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_203_0.png)

输入 `y` 并按 Enter 接受设置。然后，设置脚本将报告：

```
Adjusting /etc/ppp/ppoe.conf
Adjusting /etc/resolv.conf
  (But first backing it up to /etc/resolv.conf~bak)
Adjusting /etc/ppp/pap-secrets and /etc/ppp/chap-secrets
  (But first backing it up to /etc/ppp/pap-secrets~bak)
  (But first backing it up to /etc/ppp/chap-secrets~bak)

Congratulations, it should be all set up!
```

输入 `adsl-start` 来建立您的 ADSL 连接，输入 `adsl-stop` 来断开连接。

要启动您的连接，请像这样使用 `adsl-start` 命令：

```
# adsl-start
```

请注意，与拨号连接不同，DSL 连接应该几乎是瞬间完成的。如果无法连接，请确保您的 DSL 调制解调器已与电话公司的中心局同步，所有电缆都正确连接，您的接口已正确配置，并且您已设置脚本输入了正确的信息。如果您有一个运行正常的设置但无法启动，那么您这边几乎没有需要排查的故障。更有可能的是，如果活动连接变得不活动，问题在于 ISP 一侧，而不是您的设置内部。如果 ISP 的 DNS 或认证服务器宕机，这种情况可能会发生。在首次建立连接时，您应该明确遵循 ISP 的初始指示以建立活动连接。在您拥有活动连接后，您可以尝试不同的设置，例如用于以太网接口的最大传输单元的大小。要分享想法、提出问题或了解更多关于您所在地区的 ISP 的信息，请查看 comp.dcom.xdsl Usenet 新闻组。

在此示例中，启用了 IP 伪装。这意味着您可以与 LAN 上其他使用相同子网地址的计算机共享您的 DSL 连接。例如，如果具有 DSL 连接的主机计算机名为 `stinky`，IP 地址为 `192.168.2.30`，则您 LAN 上 `192.168.2.XXX` 范围内的其他计算机可以通过使用 `route` 命令以及 `default` 和 `gateway` 选项快速访问互联网服务，如下所示：

```
# route add default gw stinky
```

要停止您的连接，请像这样使用 `adsl-stop` 命令：

```
# adsl-stop
```

除了 `adsl-setup`、`adsl-start` 和 `adsl-stop` 命令的手册页外，您还可以在 `/usr/share/doc/rp-ppoe-2.2` 目录下找到有关 DSL 连接和 Roaring Penguin 软件的额外信息。

## 设置 SLIP

一些不支持 PPP（如今这很罕见）的 ISP 使用 SLIP。您还可能发现 SLIP 被一些不使用互联网在线服务（如银行接入程序和股票交易）所支持。过去，SLIP 通常被编译到 Linux 内核中，SLIP 的一种修改版本 CSLIP（压缩 SLIP）也是如此。然而，在 Red Hat Linux 中，SLIP 支持是作为可加载的内核模块提供的。

要使用 SLIP，您需要为其专用一个端口。这意味着该端口不能由其他应用程序使用。这是必要的，因为 SLIP 处理端口的方式如果与其他程序共享会导致冲突。

### 注意

如果您希望 SLIP 安装在内核中，您需要重新构建内核。有关更多信息，请参见第 27 章“配置和构建内核”。

## 配置 SLIP

配置 SLIP 的最快方法是使用 `slattach` 程序。这需要指定 SLIP 将使用的端口名称（通常该端口连接了用于连接的调制解调器）。设置 `slattach` 的命令如下：

```
# slattach /dev/ttyS0 &
```

在这种情况下，我将 `/dev/ttyS0` 端口（COM1）配置为 SLIP 端口。您可以使用系统连接的任何其他端口。行末的 `&` 符号将 `slatch` 程序置于后台，以便您可以取回 shell 提示符。

当运行 `slattach` 时，端口将被重命名为 `/dev/s10`，表示它是第一个 SLIP 设备。无论您使用什么设备名称作为串行端口，第一个 SLIP 设备总是被称为 `/dev/s10`。如果您使用的是 `/dev/ttyS2`（例如，它变为 `/dev/s11`），这可能会导致一些混淆。如果创建了一个以上的 SLIP 端口，它们会按顺序编号为 `/dev/s11`、`/dev/s12`，等等。Linux 通常支持多达八个 SLIP 线路，但您不太可能需要这么多。要检查是否创建了 SLIP 设备，您可以使用 `fgrep` 在 `/proc/net` 目录下搜索名为 `dev` 的文件，如下所示：

```
# fgrep s10 /proc/net/dev
s10:     0     0     0     0     0     0     0     0
...
```

Linux 默认对大多数 SLIP 线路使用 CSLIP，因为它在相同空间内比 SLIP 打包了更多的信息。如果您的 ISP 或您正在连接的对方不支持 CSLIP，您需要强制 Linux 仅使用 SLIP。您可以在 `slattach` 行中做到这一点：

```
# slattach -p slip /dev/ttyS0 &
```

这告诉 `slatch` 仅使用 SLIP 协议。`-p` 选项后的其他有效参数是 `cslip`（用于 CSLIP）、`adaptive`（根据连接另一端进行调整）、`ppp` 和 `kiss`（用于分组无线电）。

既然 SLIP 设备已创建，您需要使用 `ifconfig` 程序来告诉 Linux 内核关于它，并设置虚拟接口。建立接口的 `ifconfig` 行需要远程系统的名称：

```
ifconfig sl0 mymachine-slip pointopoint remoteremote machine
```

`sl0` 是接口的名称（在这种情况下是 `/dev/s10`）；`mymachine-slip` 是本地 SLIP 接口的名称（您应该替换为您的机器名称，例如 `merlin-slip` 或 `darkstar-slip`）；`pointopoint` 告诉 `ifconfig` 该接口是点对点连接（不要与 PPP 混淆）；`remoteremote machine` 是连接另一端机器的名称。例如，如果远程机器的名称是 `darkstar`，您的机器名称是 `dogbert`，则 `ifconfig` 命令如下所示：

```
ifconfig sl0 dogbert-slip pointopoint darkstar
```

下一步是发出 `route` 命令将到远程机器的路由添加到系统数据库中。语法与您设置虚拟接口时相同：

```
route add darkstar
```

在这种情况下，您正在添加一条到名为 `darkstar` 的远程机器的路由。您应该替换为实际的远程机器名称。

### 注意

许多 ISP 不会告诉您其远程机器的名称。这没关系，因为这些机器名称只是占位符；所需的重要信息是 IP 地址。虽然不推荐，但您可以替换任何标识连接另一端的名称，只要该名称在您定义的 `/etc/hosts` 文件中。但是，相关的 IP 地址必须正确。

## 设置拨入 PPP 服务器

您还可以在 Linux 系统上设置一个简单的服务，为拨入用户提供 PPP。虽然 ISP 等商业企业必须投资于租用线路、交换服务、调制解调器池和路由器，但您可以轻松配置一个独立的 Linux 盒子来响应调制解调器并启动 PPP。一般步骤可能包括

- 选择电话线、调制解调器和串行端口
- 正确配置调制解调器以响应来电（使用 AT 命令并通过 `AT&W` 保存调制解调器配置）
- 安装一个线路监控应用程序（如 `agetty`、`getty` 或 `ngetty`）以监控串行端口（在 `/etc/inittab` 中）
- 可能配置 DNS 服务器（有关更多信息，请参见第 14 章“域名服务和动态主机配置协议”）
- 配置 Linux 在用户登录后自动启动 `pppd` 守护进程

通常，对于许多调制解调器，`ATE1Q0V1&CI&S0=S0=1&W` 调制解调器字符串将设置调制解调器以自动响应来自不同终端监控程序的来电。（一些，如 `ugetty`，具有配置文件以自动为特定的串行端口设置调制解调器。）

下一步是在 `/etc/inittab` 文件中创建适当的条目：

```
3:2345:respawn:/sbin/ugetty ttyS1 38400 vt100
```

此条目假设您在 `ttyd`/`ttyS1` 上连接了调制解调器。如果您使用 `ugetty` 命令监控调制解调器的串行端口，您还需要将文件 `ugetty.autoanswer` 从 `/usr/doc/getty_ps-2.0.7/Examples/default` 目录复制到 `/etc/default` 目录。然后，您应该编辑此文件并查找 `ALTLOCK` 条目：

```
# alternate lockfile to check… if this lockfile exists, then ugetty is
# restarted so that the modem is re-initialized
ALTLOCK=cua2
```

将 `ALTLOCK` 条目更改以匹配您调制解调器的串行端口。使用上述 `/etc/inittab` 条目，字符串 `cua2` 将更改为 `ttyS1`。然后，该文件应以名称 `ugetty` 保存在 `/etc/default` 目录中。使用匹配串行端口的后缀（例如 `ugetty.ttyS0`）。然后，您应该从远程计算机拨入以检查登录过程。

下一步是创建一个用户以测试 PPP 服务。使用 `adduser` 命令创建一个名为 `ppp` 的用户，然后分配密码。虽然用户可以登录到您的系统并从命令行启动 `pppd`（假设您已将 `pppd` 设置为 SUID），您可以

