
`ptpd` `0:off` `1:off` `2:off` `3:off` `4:off` `5:off` `6:off`

*(注：原文示例 6.27 似乎存在重复/截断错误，译文已按原文逻辑保留)*

# 列表 6.30: 检查 systemd 挂载单元的状态

```
systemctl status home-temp.mount
```

• `home-temp.mount` - Test Mount Units
Loaded: loaded (`/etc/systemd/system/home-temp.mount; ...`)
Active: active (mounted) since Sat 2019-09-14 16:34:2[...]
Where: `/home/temp`
What: `/dev/sdb1`
Process: `3998` `ExecMount=/bin/mount /dev/sdb1 /home-temp[...]`
[...]

还需要一个额外的步骤。为了确保 `systemd` 能够持久地挂载文件，必须启用挂载单元文件以便在启动时运行，就像其他 `systemd` 单元一样。示例 6.31 所示。

# 列表 6.31: 启用 systemd 挂载单元

```
systemctl enable home-temp.mount
```

Created symlink from
`/etc/systemd/system/multi-user.target.wants/home-temp.mount` to
`/etc/systemd/system/home-temp.mount.`

这看起来应该非常熟悉！请记住，只有在你需要微调持久文件系统配置时，才使用挂载单元文件。如果不需要，最好使用 `/etc/fstab` 记录来持久地挂载文件系统。

# 探索自动挂载单元 (Automount Units)

通过 `systemd`，你可以使用自动挂载单元配置按需挂载以及并行挂载。此外，你还可以设置文件系统在无活动时自动卸载。

自动挂载单元文件的工作与挂载单元文件类似。命名约定相同，只是文件扩展名为 `.automount`。

在自动挂载单元文件中，对于 `[Automount]` 部分，只有以下三个指令：

- `Where`
- `DirectoryMode`
- `TimeOutIdleSec`

`DirectoryMode` 指令是所需的。它的配置方式与挂载单元文件完全相同。通过它，你可以设置挂载点。

`DirectoryMode` 指令不是可选选项。此设置决定了任何自动创建的挂载点及其父目录的权限。默认设置为八进制代码 `0755`。

## 考试要点

你可以在 `/etc/fstab` 文件中配置自动挂载点。
但请记住，如果在 `/etc/fstab` 文件中配置了自动挂载点且存在单元文件，则单元文件的配置将具有优先级。

`TimeoutIdleSec` 指令并非必需。此特定指令允许你设置挂载的文件系统空闲的最大时间（以秒计）。当达到时间限制时，文件系统将被卸载。默认此指令是禁用的。

## 总结

管理服务器最后的单元初始化阶段是初始化守护进程的任务。该守护进程必须根据你在适当配置文件中提供的信息，确定启动哪些服务。此外，守护进程可以在系统运行期间管理服务。

经典的系统初始化守护进程 `SysV init` 仍然存在，尽管仅限于旧版发行版。这种流行的现代系统在当前的 Linux 发行版中被广泛使用。它不仅允许更快的服务器启动速度，还提供了额外的服务，例如文件系统的自动挂载。系统管理员经常发现自己正在从 `SysV init` 单元迁移到 `systemd` 服务器，因此理解这两种系统初始化方法都是重要的。

## 考试要点

描述 init 程序。`init` 程序或 `systemd` 都是 Linux 系统上每个服务的父进程。它的 `PID` 通常为 `1`。该程序位于 `/etc/`、`/bin/` 或 `/sbin/` 目录。在 `systemd` 服务器上，此程序是指向 `/usr/lib/systemd/system` 的符号链接。

总结系统单元概念。`systemd` 单元定义了一个服务、一组服务或一个操作，目前有 `12` 种不同的系统单元类型。要加载单元，使用 `systemctl list-units` 命令。需要关注的四个系统单元是 `service`、`target`、`mount` 和 `automount`。

解释服务单元及其文件。服务单元控制如何启动、停止和管理服务。单元文件通过三个主要单元部分之一的 `[Unit]`、`[Service]` 和 `[Install]` 中的指令包含配置信息。诸如 `After` 和 `Before` 等指令配置了服务何时启动。虽然 `[Unit]` 和 `[Install]` 是所有单元文件共有的，但 `[Service]` 部分及其指令是服务特有的。单元文件可能存在三个目录位置之一，其位置非常重要，因为如果某个单元存在多个文件，将根据它们的位置决定一个优先级高于另一个。

解释 `systemd target` 单元及其文件。`Target` 单元负责启动一组服务。在系统初始化时，默认 `target` 单元确保所有所需和期望的服务都启动。它被设置成指向另一个 `target` 单元的符号链接。用于系统初始化的主要 `target` 单元有 `graphical.target`、`multi-user.target` 和 `runlevel.target`，其中 `n=1-5` 代表所所需的 `SysV` 运行级别。还有额外的 `target` 单元处理关机、停止、重启以及紧急和救援模式。`target` 单元文件类似于服务单元文件，但通常包含较少的指令。

演示如何通过命令管理 `systemd` 单元。`systemctl` 工具包含许多允许你管理和控制 `systemd` 单元的命令。可以使用 `systemctl isolate` 命令跳转到启动时的系统启动。可以使用 `systemctl enable` 命令设置特定服务自动启动。其他命令允许你停止、启动、重启和重新加载你的文件。

总结 `SysV init`。经典的系统初始化方法由 `/etc/init.d/` 中的脚本组成。运行级别（Runlevels）决定启动哪些服务。`target` 类型单元类似于服务单元文件，但通常包含较少的指令。

描述 `systemd` 初始化和挂载单元。如果你的服务器采用 `systemd`，除了管理初始化，它还可以挂载文件系统。这些文件系统可以通过其关联的单元文件进行挂载或自动挂载。`mount` 和 `automount` 单元名称基于挂载点，但分别使用 `.mount` 或 `.automount` 扩展。每个单元有三个部分，类似于服务单元文件，挂载单元的中间部分是 `[Mount]`；而自动挂载单元文件的中间部分是 `[Automount]`。

5. 在你的服务器上，你需要让 `Service-B` 在 `Service-A` 之前启动。在 `systemd` `Service-A` 单元文件中，你应该检查并可能修改哪个指令？

- A. `Conflicts`
- B. `Wants`
- C. `Requires`
- D. `Before`
- E. `After`

6. 为了在单元文件中设置环境参数，你可能应该使用哪些指令？选择所有适用项。

- A. `Type`
- B. `Environment`
- C. `EnvironmentParam`
- D. `EnvironmentFile`
- E. `PATH`

7. 你尝试使用 `systemctl isolate` 命令跳转到一个 `systemd` `target`，但不起作用。你决定查看该 `target` 单元文件。你可能在那里看到什么导致了这个问题？

- A. `static`
- B. `AllowIsolate=yes`
- C. `Type=oneshot`
- D. `AllowIsolate=no`
- E. `disabled`

8. 你修改了 `OpenSSH` 服务的配置文件 `/etc/ssh/ssh_config`。该服务正在运行。使用 `systemctl` 的哪个命令可以使该文件立即生效？

- A. `reload`
- B. `daemon-reload`
- C. `restart`
- D. `mask`
- E. `unmask`

9. 你的系统使用 `systemd`，并且有一个服务被设置为系统启动时不启动。你想更改此行为让它启动。对于该服务你应该使用哪个 `systemctl` 命令？

- A. `restart`
- B. `start`
- C. `isolate`
- D. `disable`
- E. `enable`

10. 你需要更改系统的默认 `target`。你应该使用哪个 `systemctl` 命令完成此任务？

- A. `get-default`
- B. `set-default`
- C. `isolate`
- D. `is-enabled`
- E. `is-active`

11. 你的 `systemd` 系统启动需要很长时间，你需要缩短启动时间。哪个 `systemd-analyze` 命令最适合开始缩小需要优先调查的单元范围？

- A. `time`
- B. `dump`
- C. `failure`
- D. `blame`
- E. `verify`

12. 你旧的基于 `Debian` 的 Linux 发行版使用 `SysV init`。它很快将升级到使用 `systemd` 的 `Debian` 发行版。为了开始某些分析

- A. `N 5`
- B. `3 5`
- C. `N 2`
- D. `2 3`
- E. `1 2`

13. 你最近成为一个旧版 Linux 服务器的系统管理员，该服务器仍使用 `SysV init`。你确定其默认 `runlevel` 为 `3`。你在哪个文件中找到该信息的？

- A. `/etc/initabtab`
- B. `/etc/rc.d`
- C. `/etc/init.d/rc`
- D. `/etc/rc.d/rc`
- E. `/etc/rc.local`

14. 旧版 `SysV init` 系统上的哪个目录存储服务启动脚本？

- A. `/usr/lib/systemd/system/`
- B. `/etc/rc.d/rc.d/`
- C. `/etc/init.d/`
- D. `/etc/systemd/system/`
- E. `/run/systemd/system/`

15. 你正在管理一个 `SysV init` 系统，需要在 `runlevel` `1` 执行一些紧急维护。为了做到这一点，你需要切换 `runlevel`。你可以使用哪个命令？（选择所有适用项。）

- A. `telinit 5`
- B. `telinit 1`
- C. `init one`
- D. `init s`
- E. `init 1`

16. 客户抱怨你 `SysV init` 系统上的某个服务无法工作。以下哪个命令是检查该服务的最佳命令？

- A. `service start`
- B. `service status`
- C. `service --status-all`
- D. `service stop`
- E. `service reload`

17. 你需要在基于 `Red Hat` 的 `SysV init` 系统上为 `runlevel` `3` 和 `5` 启用 `DHCP` 服务。你应该使用以下哪个命令？

- A. `service enable dhcp 3,5`
- B. `chkconfig --levels 3,5 dhcp on`
- C. `chkconfig --levels 35 on dhcp`
- D. `chkconfig --levels 35 dhcp on`
- E. `service enable dhcp 35`

18. 你需要在基于 `Debian` 的 `SysV init` 系统上为默认 `runlevel` 启用 `DHCP` 服务。你应该使用以下哪个命令？

- A. `update-rc.d dhcp default`
- B. `chkconfig --default dhcp on`
- C. `update-rc.d default dhcp`
- D. `update-rc.d defaults dhcp`
- E. `update-rc.d dhcp defaults`

19. 下哪项对于在 `/var/log/` 挂载点挂载文件系统的 `mount` 单元文件是合适的 `base`？

- A. `/var/log.mount`
- B. `/var/log.unit`
- C. `var-log.mount`
- D. `var-log.unit`
- E. `var/log.mount`

20. 你正在管理一个 `systemd` 系统，需要创建一个自动挂载（`automount`）挂载单元文件。你应该检查哪些指令以可能包含在该文件的 `[Automount]` 部分？（选择所有适用项。）

- A. `Where`
- B. `Options`
- C. `DirectoryMode`
- D. `TimeoutIdleSec`
- E. `What`

# 配置网络连接

- 目标 1.3：给定一个场景，配置并验证网络连接参数

![](img/0c1e7d2699b9d354c8d2f84669d18d73_242_0.png)

![](img/0c1e7d2699b9d354c8d2f84669d18d73_243_0.png)

如今，让你的 Linux 系统连接到某种网络几乎是必须的。无论是因为需要在局域网上共享文件和打印机，还是因为需要连接互联网下载更新和安全补丁，大多数 Linux 发行版都带有某种网络。本章将介绍如何配置你的系统，以及在出现问题时如何进行网络故障排除。首先，我们将介绍常见的位置。接下来，我们将检查你可以使用的不同工具。

# 配置网络功能

在 Linux 系统中，你需要配置五项主要信息：

- 主机地址
- 网络子网掩码
- 默认路由器（有时称为网关）
- 系统主机名
- `DNS` 服务器地址

在 Linux 中有三种不同的方法来配置这些信息：

- 手动编辑网络配置文件
- 使用自带的图形工具
- 使用命令行工具

# 网络配置文件

每个 Linux 发行版都使用网络配置文件来定义网络设置。然而，并不是所有发行版都使用同一个配置文件。相反，不同的发行版使用不同的配置文件。表 7.1 显示了你会遇到的常见网络配置文件。

### 表 7.1 网络配置文件

| 发行版 | 网络配置位置 |
|---|---|
| 基于 `Debian` | `/etc/network/interfaces` |
| 基于 `Red Hat` | `/etc/sysconfig/network-scripts` |
| `openSUSE` | `/etc/sysconfig/network` |

虽然每个 Linux 发行版定义网络设置的方法不同，但它们具有相似的功能。列表 7.1 显示了一个基于 `Debian` 的 Linux 示例。

### 列表 7.1： Debian 网络静态设置示例

```
auto eth0

iface eth0 inet static

    address 192.168.1.77

    netmask 255.255.255.0

    gateway 192.168.1.254

iface eth0 inet6 static

    address 2003:aef0::23d1::0a18:00a1

    netmask 64
```

列表 7.1 中所示的示例为名为 `eth0` 的物理网络接口分配了 `IP` 和 `IPv6` 地址。列表 7.2 显示了如何使用网络上的 `DHCP` 服务器自动定义 `IP` 网络设置。

### 列表 7.2： Debian 网络 DHCP 设置示例

```
auto eth0

iface eth0 inet dhcp

iface eth0 inet6 dhcp
```

如果你想分配一个 `IPv6` 链路地址（`link local address`），该地址可以唯一标识局域网上的设备，但从 `DHCP` 服务器获取 `IPv6` 地址，请将 `inet6` 行替换为：

```
iface eth0 inet6 auto
```

## 第 7 章 配置网络连接

`auto` 属性告诉 Linux 分配链路地址，这允许 Linux 系统与本地网络上的任何其他 `IPv6` 设备通信，但不是全局地址。

> 从 `17.04` 版本开始，`Ubuntu` 发行版偏离了标准的 `Debian` 方法，利用 `Netplan` 工具管理网络设置。`Netplan` 使用 `/etc/netplan` 文件夹中的简单 `YAML` 文本文件定义系统上安装的每个网络接口的网络设置。默认情况下，`Netplan` 仅将网络设置传递给 `NetworkManager` 工具，因此你不需要担心 `Netplan` 配置文件是如何设置的。

对于基于 `Red Hat` 的系统，你需要在两个单独文件中定义网络设置。第一个文件在以网络接口名称命名的文件中定义网络地址和子掩码地址（例如 `ifcfg-eth-en0s3`）。列表 7.3 显示了来自 `CentOS` Linux 系统的示例。

### 列表 7.3：CentOS 网络网络接口配置设置示例

```
TYPE=Ethernet

PROXY_METHOD=none

BROWSER_ONLY=no

BOOTPROTO=dhcp

DEFROUTE=yes

IPV4_FAILURE_FATAL=no

IPV6_INIT=yes

IPV6_AUTOCONF=yes

IPV6_DEFROUTE=yes

IPV6_FAILURE_FATAL=no

IPV6_ADDR_GEN_MODE=stable-privacy

NAME=en0s3

UUID=c8752366-33e1-47e3-8162-c0435ec6d451

DEVICE=en0s3

ONBOOT=yes

IPV6_PRIVACY=no
```

基于 `Red Hat` 的系统所需的第二个文件是网络文件，它定义了主机名和默认网关，如列表 7.4 所示。

### 列表 7.4：CentOS 网络文件配置设置示例

```
NETWORKING=yes

HOSTNAME=system

GATEWAY=192.168.1.254

IPV6FORWARDING=yes

IPV6_AUTOCON=no

IPV6_AUTOTUNNEL=no

IPV6_DEFAULTGW=2003:aef0::23d1::0a10:0001

IPV6_DEFAULTDEV=eth0
```
