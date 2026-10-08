

# 160 第 2 部分 分层安全与 Linux

> 注意

互联网（internet）和扩展互联网超级服务器（extended internet super server）使用的是小写的 "internet"，因为这两项服务都涉及网络互连，而不是指互联网（Internet）。

某些服务是扩展互联网超级服务器的一部分。此类服务的管理命令将在本章稍后介绍。

少数服务在 `/etc/init.d/` 目录下可能没有脚本，或者没有与扩展互联网超级服务器关联。在这种情况下，你只需要对服务守护进程执行 `kill` 或 `killall` 命令。例如，如果你的系统上运行着假设的守护进程，你可以运行 `killall` 命令。

或者，你可以找到与守护进程关联的进程标识 (PID)，并对该 PID 号执行 `kill` 命令。`kill` 命令更加灵活，因为它可以向当前运行的守护进程发送多个不同的信号。

## 修改服务默认值

通常，在命令行界面更改大多数 Linux 配置选项是最快的。用于实现此目的的两个相似命令是 `update-rc.d` 和 `chkconfig`。虽然命令不同，但它们都作用于运行级别 0, 1, 2, 3, 4, 5, 6 中的不同脚本。大多数 Linux 发行版的标准是在运行级别 2, 3, 4 和 5 中激活服务。同样，Linux 发行版应被设置为在运行级别 0, 1 和 6 中禁用。

主要的 Linux 发行版正在将其服务运行级别系统转换为 Upstart，配置在 `/etc/event.d/` 中。一旦脚本完成转换，你就可以通过 `service` 等命令更直接地使用守护进程。由于 Upstart 的开发仍在进行中，细节可能会发生。更多信息请参阅 http://startup.ubuntu.com/。

等一下，OCR 文本似乎弄乱了 `update-rc.d` 部分。让我重新对齐逻辑流：

## update-rc.d 命令

如果你使用的是 Ubuntu 系统，`update-rc.d` 命令控制运行级别中服务脚本的配置。如果你想从管理中移除某个服务——例如 Samba 服务——请运行以下命令：

```bash
update-rc.d samba remove
```

如果你更于确保服务在所有运行级别中都停止，以下命令将在标准模式下禁用该服务：

```bash
update-rc.d samba stop 0 2 3 4 5
```

在这种情况下，数字指定优先级。例如，如果你在 `/etc/rc.d/` 中看到 `abc` 和 `def`，则 `abc` 会在 `def` 之前停止。该命令不支持运行级别列表。

## 每个服务都是潜在的风险

当然，这个过程也可以反过来；以下命令将服务设置为运行级别 2, 3, 4 和 5 启动：

```bash
update-rc.d samba start 2 3 4 5
```

## chkconfig 命令

如果你使用的是 Red Hat 系统，`chkconfig` 命令可以提供帮助。首先，`chkconfig --list` 列出所有通过 SysV 配置的服务，并指示它们在系统移动到运行级别时是设置为关闭（off）还是启动（start）。以下是一个示例：

```bash
chkconfig smb 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

在这种情况下，Samba 服务将在运行级别 3 和 5 启动。你可以使用 `chkconfig` 命令根据你选择的运行级别设置服务的启动或停止。例如，以下命令将服务设置为运行级别 2, 3, 4 和 5 启动：

```bash
chkconfig smb --level 2345
```

该命令等同于 `chkconfig smb on`。你可以反转此过程；使用以下命令在运行级别 2, 3 和 4 禁用 Samba：

```bash
chkconfig smb --level 234 off
```

或者，`chkconfig smb off` 会在所有运行级别禁用 Samba。

## 涉及的服务

RHEL 5 的最小化安装包含比 Ubuntu Server 最小化安装更多的服务。但要为任何一种发行版设置服务器，你需要对每个服务有深入了解。本节检查了每个发行版的 `/etc/init.d/` 目录。在典型的安装中，你会在该目录下看到更多服务。

表 6-2 包含了比 RHEL 5 和 Ubuntu Server 最小化安装更多的活动服务。查看你系统中的这些服务。这些服务中的大多数只出现在其中一个发行版中。如果你保持这些任何服务处于激活状态，请务必理解其原因。这些知识在未来出现安全问题时会对你有帮助。应该保留的两个服务是 `halt` 和 `single`。这些服务分别与运行级别 0 和 1 关联。

`Action`（操作）列包含了适用于大多数服务的选项。如表格所示，大多数服务在大多数系统上都应该被禁用。对于某些服务，你的系统可能是例外。如果不确定，请仔细阅读这些选项。表 6-2 是一份长列表，但创建一个安全系统所需的工作同样如此。一旦你利用这些信息创建了安全的堡垒机（bastion），你就可以将其作为其他安全系统的模板。

### 表 6-2 Red Hat 中 /etc/init.d/ 目录下的服务脚本。

| 服务脚本 | 描述 | 操作 |
| :--- | :--- | :--- |
| acpid | 高级配置和电源接口 (ACPI) 守护进程；除非你不关心电源管理，否则应保持启用。 | Enable |
| anacron | 如果系统在计划任务运行时关机则运行 cron 脚本；如果服务器 24/7 处于机则禁用。 | Disable |
| apmd | 高级电源管理 (APM) 守护进程；如果启用了 ACPI 则不需要 APM，可以禁用。 | Disable |
| atd | AT cron 运行队列中的一次性任务，可以根据第 7 章进行管理。 | Maybe |
| auditd | 审计守护进程对于安全相关事件非常重要，包括 SELinux 高亮显示的事件。 | Enable |
| autofs | 自动挂载按需挂载移除式和网络目录。 | Disable |
| avahi-daemon | Avahi 守护进程是微软 zerconf 技术和 Apple Bonjour 协议的 Linux 实现。它使用端口 5353 发现本地网络上的打印机和共享目录。有时通过 Samba 共享媒体。 | Disable |
| avahi-dnsconf | 用于发现本地域名系统 (DNS) 服务器。 | Disable |
| bluetooth | 用于蓝牙硬件支持。 | Disable |
| bootlog | 用于记录启动信息。 | Enable |
| isdn | 用于 ISDN 调制调器。 | Disable |
| console-setup | 在启动过程中初始化键盘检测。 | Enable |
| crond | 用于常规管理任务的 cron 守护进程。 | Enable |
| cryptdisks-* | 磁盘加密。 | Enable |
| cups | 通用 Unix 打印系统。 | Disable |
| dnsmasq | 用于小型 DNS 和 DHCP 服务器。 | Disable |

