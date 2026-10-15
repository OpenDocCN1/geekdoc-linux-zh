
链接到 `/etc/rc?.d` 目录的脚本以 `K` 或 `S` 开头，后面跟两个数字和服务名。以 `K` 开头的脚本表示应该停止该服务，而以 `S` 开头的脚本表示应该启动它。两个数字遵循服务启动的顺序。以下是你可能在 `/etc/rc3.d/` 目录中发现的一些文件，它们被设置为启动（右侧是每个文件的描述）：

## 第四部分：成为 Linux 服务器管理员

- `S01sysstat`—启动系统统计收集。
- `S08iptables`—启动 `iptables` 防火墙。
- `S10network`—启动网络接口。
- `S12rsyslog`—启动系统日志记录。
- `S28autofs`—启动自动挂载器。
- `S50bluetooth`—启动蓝牙服务。
- `S55sshd`—启动安全外壳（Secure Shell）。
- `S58htntpd`—启动 NTP 时间同步服务。
- `S85httpd`—启动 Apache Web 服务器。
- `S90crond`—启动 cron 服务。
- `S91ms`—启动 samba 服务。
- `S97rhnsd`—启动红帽网络（Red Hat Network）。
- `S99local`—启动用户定义的本地命令。

这个从 `/etc/rc.d` 目录启动的少数服务示例，可以让你了解在进入运行级别 3 时进程启动的顺序。请注意，`sysstat` 服务（收集统计数据）和 `iptables` 服务（创建系统防火墙）在网络接口启动之前就已经启动了。随后是 `rsyslog`（系统日志服务），然后是各种网络服务。

当运行级别启动时，你的系统应该已经基本启动并运行。与某些其他 Linux 系统（它们按顺序执行运行级别 1、2、3 和 0 的脚本）不同，RHEL 会直接进入代表该运行级别的目录，首先停止所有以 `K` 开头的服务，并启动该目录下所有以 `S` 开头的服务。

当每个脚本执行时，你应该会看到显示服务是否已启动的消息。在系统启动的这一阶段，可能会出现以下问题：

- **服务可能会失败**。服务可能需要访问网络接口才能正常启动，或者需要访问未挂载的磁盘分区。大多数服务会超时并失败，然后允许下一个脚本运行。在你能够登录后，可以对该服务进行调试。调试服务的某些技术包括为守护进程添加调试选项以便将其数据转储到日志文件中，或手动运行守护进程以便让错误信息显示在你的屏幕上。有关手动启动服务的更多信息，请参阅第 15 章。
- **服务可能会挂起**。某些无法获取启动所需的服务的可能会无限挂起，导致你无法登录以调试问题。某些进程在全新安装后首次启动需要更长时间，因此你可能需要等待几分钟，看看脚本是否仍在运行，而不是在空转。

## 第 21 章：Linux 故障排除

如果你无法获取挂起的的服务，可以重启进入*交互式启动模式*，在启动每个会话之前，你都会收到提示。要在 RHEL 中进入交互式启动模式，重启并中断引导加载程序（在看到 5 秒倒计时时按任意键）。高亮你想启动的项并输入 `e`。高亮内核行并输入 `e`。然后在内核行末尾添加单词 `confirm`，按回车，然后输入 `b` 启动新内核。

图 21.1 显示了 RHEL 在交互模式下启动时出现的消息示例。

### 图 21.1

在 RHEL 交互式启动模式下确认每个服务。

| 欢迎使用 Red-Hat Enterprise Linux Server | OK |
|---|---|
| 设置主机名 triumph.example.com: | OK |
| 正在逻辑卷管理：卷组 "vg_ntriumph" 中现在有2 个逻辑卷 | OK |
| 检查文件系统 | OK |
| /dev/mapper/triumph-lv-root: clean, 80953/363680 blocks, 65645/145283 blocks | |
| /dev/sda: clean, 30/120816 files, 49837/512088 blocks | |
| 正在以读写模式重新挂载文件系统: | OK |
| 正在挂载本地文件系统: | OK |
| 启用本地文件系统: | OK |
| 启用 /etc/fstab 挂载 | OK |
| 进入交互式启动 | OK |
| Start service systemd-journald.service(continue? [Y]) _ | |

图 21.1 中的大部分消息由 `rc.sysinit` 生成。

消息之后，`*udev*`（用于监控连接到系统的新硬件并根据需要加载驱动）。主机名被设置，逻辑卷管理（LVM）卷被挂载，所有文件系统已检查（使用活动的 LVM 卷），未挂载的文件系统、根文件系统被重新挂载为读写，并启用了 LVM 交换。有关 LVM 以及其他分区和文件系统的更多信息，请参阅第 12 章。

最后一条“Entering interactive startup”消息告诉 `rc.sysinit` 已完成，所选运行级别的服务已准备就绪。由于服务是交互式的，会显示一条消息询问你是否要启动第一个 `sysstat`。输入 `Y` 启动并进入下一个。

当你看到损坏的服务请求启动时，输入 `N` 阻止服务启动。如果你在某个时刻觉得其余的服务可以安全地停止，输入 `C` 继续启动其余服务。如果你的系统启动了，且损坏的服务没有启动，你可以返回对这些单独的服务进行调试。

关于脚本的一条说明：`/etc/rc.local` 是最后运行的服务之一。在 RHEL 中，你可以使用 `/etc/rc.local` 添加在启动时运行的自定义脚本。然而，在 RHEL 6 及更高版本中，默认并不存在 `/etc/rc.local` 文件。你必须创建它并使其具有可执行权限。

`systemd` 系统是 RHEL 中管理服务的现代方法。在 `systemd` 中，你使用 `systemctl` 命令来管理服务。例如，要启动服务，使用 `systemctl start service_name`。要停止服务，使用 `systemctl stop service_name`。要检查服务状态，使用 `systemctl status service_name`。要在启动时启用服务，使用 `systemctl enable service_name`。要在启动时禁用服务，使用 `systemctl disable service_name`。

## 第四部分：成为 Linux 服务器管理员

`autofs.service` loaded active running

按需挂载文件系统

`cups.service` loaded active running

CUPS 打印服务

`httpd.service` loaded failed failed

Apache HTTP 服务器

从 `systemctl` 的输出中，你可以看到任何单元是否失败。在这种情况下，你可以看到 `httpd.service`（你的 Web 服务器）启动失败。要进一步调查，你可以运行 `journalctl -u service` 来查看报告了任何错误信息：

```bash
# journalctl -u httpd.service

Sep 07 18:40:52 host systemd[1]: Starting The Apache HTTP Server...
Sep 07 18:40:53 hostd[16365]: httpd: Syntax error on line 361 of
/etc/httpd/conf/httpd.conf: Expected <Directory> but saw
</Directory>
Sep 07 18:40:53 host systemd[1]: httpd.service:
   process exited, code=exited, status=1/FAILURE
Sep 07 18:40:53 host systemd[1]: Failed to start the Apache HTTP
Server.
Sep 07 18:40:53 host systemd[1]: Unit httpd.service entered failed state.
```

从输出中，你可以看到 `httpd.conf` 文件中的指令不匹配（我用了 `Direct` 而不是 `Directory`）。纠正后，我可以启动服务（`systemctl start httpd`）。如果出现更多单元显示失败，你可以运行 `journalctl -u` 命令，并将这些文件名作为参数。
