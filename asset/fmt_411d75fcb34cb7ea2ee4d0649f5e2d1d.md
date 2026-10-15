
| Samba 日志 | `/var/log/samba/log.smbd` | 显示来自 Samba 文件服务守护进程的消息。 |
| 安全日志 | `secure` | 记录登录尝试和会话的日期、时间和时长。 |
| Sendmail 日志 | `sendmail` | 显示 sendmail 守护进程记录的错误消息。 |
| Squid 日志 | `/var/log/squid/access.log` | 包含与 squid 代理/缓存服务器相关的消息。 |
| 系统日志 | `messages` | 提供通用日志文件，许多程序在此记录消息。 |
| UUCP 日志 | `uucp` | 显示来自 UNIX 到 UNIX 复制协议守护进程的状态消息。 |
| YUM 日志 | `yum.log` | 显示与 RPM 软件包相关的消息。 |
| X.Org X11 日志 | `Xorg.0.log` | 包括 X.Org X 服务器输出的消息。 |

您系统 `/var/log` 目录中的日志文件取决于您运行的服务。此外，某些日志文件取决于发行版。例如，如果您使用 Fedora Linux，则将没有 dpkg 日志。

大多数日志文件使用 `cat`、`head`、`tail`、`more` 或 `less` 命令显示。然而，其中一些需要特殊的命令来查看（见表 22.4）。

# 表 22.4 需要特殊命令查看的日志文件

| 文件名 | 查看命令 |
|---|---|
| `btmp` | `dump-utmp btmp` |
| `dmesg` | `dmesg` |
| `lastlog` | `lastlog` |
| `wtmp` | `dump-utmp wtmp` |

随着 Fedora、RHEL 和其他 Linux 发行版转向 `systemd`（管理引导过程和服务），如前所述，与内核和系统服务相关的消息收集和显示机制也发生了变化。这些消息被重定向到 `systemd` 日志，并可以使用 `journalctl` 命令显示。

您可以直接从 `systemd` 日志查看消息，而不是简单列出 `/var/log/messages` 文件（许多服务默认将日志重定向到那里，该文件在最新的 Fedora 中不存在）。您可以使用 `journalctl` 命令以多种方式显示日志消息。

要分页查看消息，输入以下命令：

```
# journalctl -k
-- 日志开始于 2014-08-17 15:33:30 EDT,
```

## 第 22 章：理解基础 Linux 安全

```
end Sat 2014-09-13 22:29:00 EDT.
Aug 29 23:14:38 fedora20 kernel: Initializing cgroup subsystems cpuset
Aug 29 23:14:38 fedora20 kernel: Initializing cgroup subsystems cpu
Aug 29 23:14:38 fedora20 kernel: Initializing cgroup subsystems cpacct
Aug 29 23:14:38 fedora20 kernel: Linux version
31.10-301.fc20.x86_64 builds\kernel01.fedoraproject.org)
(gcc version 4.8.2-2)
Aug 29 23:14:38 fedora20.example kernel: Command line:
BOOT_IMAGE=/vmlinuz-3.10.301.fc20.x86_64
root=/dev/mapper/fedora_fedora20-root ro rd.lvm
Aug 29 23:14:38 fedora20.example kernel: e820:
BIOS-provided physical RAM map:
```

要查看特定服务的消息，请使用 `-u` 选项后跟服务名称。

- `# journalctl -u NetworkManager.service`
- `# journalctl -u http.service`
- `# journalctl -u avahi-daemon.service`

如果你认为正在发生安全违规，可以通过跟踪消息（follow messages）在消息产生时查看所有或选定的消息。例如，如需实时跟踪内核消息或 http 消息，请使用 `-f` 选项（完成后按 `Ctrl+C`）：

- `# journalctl -k -f`
- `# journalctl -f u NetworkManager.service`

如果只想检查消息，可以列出所有启动的启动 ID（boot IDs），然后进入你感兴趣的特定启动。以下示例显示了所选启动 ID 的消息：

```
# journalctl --list-boots
- 2eb3d5ccda8f4f87adcbc71fb9b4e6e
Sun 2014-08-17 15:33:30 EDT-Wed 2014-08-24 06:43:29
- 5173a5c4a6c5c1b5b3d056487a1d6bd
Wed 2014-08-24 08:45:36 UTC-Fri 2014-08-25 12:01:01
- 6417ad715a2b4499a3122a8e5a6bc1bd
Fri 2014-08-29 23:14:38 EDT-Sun 2014-09-14 07:15:26
# journalctl -b 5173a5c4a6c5c1b5b3d056487
Logs begin at Sun 2014-08-17 15:33:30 EDT, end at
Sun 2014-09-14 07:23:09 EDT. -
Aug 20 06:45:15 fedora20.example.com systemd-journal[81]:
Runtime journal is using 8.0 (m
```

`journalctl` 命令还有许多其他可用选项。有关这些选项的信息，请参阅 `journalctl` 页面（`man journalctl`）。有关关于 `systemd-journal` 本身的更多信息，请输入 `systemd-journal.service`。

## 第五部分：学习 Linux 安全技术

## 监控用户账户

用户账户经常用于系统的恶意攻击，通过获取当前账户的未授权访问、创建新的虚假账户或留下账户以便以后访问。为了避免安全问题，监控用户账户是一项重要的活动。

### 检测伪造账户和新权限

未经过适当授权而创建的账户应该是伪造的。此外，以任何方式修改账户使其获得不同的未授权用户标识（UID）数字或添加未授权的组组成，都是权限提权的形式。密切关注 `/etc/passwd` 和 `/etc/group` 文件将监控这些潜在的违规行为。

要监控 `/etc/passwd` 和 `/etc/group` 文件，你可以使用审计守护进程（audit daemon）。审计守护进程是一个极其强大的工具，允许你选择系统事件进行跟踪和记录它们，并提供报告功能。

要开始审计 `/etc/passwd` 和 `/etc/group` 文件，你需要使用 `auditctl` 命令。启动此操作至少需要两个选项：

- `-w filename` 在文件名上放置监视。审计守护进程通过其 inode 号跟踪文件。inode 号是一个包含有关文件信息的数据结构，包括其位置。
- `-p permissions` 指定权限（如 r、w、x），当发生这些操作时触发审计。例如：

```
auditctl -w /etc/passwd -p wa -k passwordchanges
auditctl -w /etc/group -p wa -k groupchanges
```

（注：原文中代码示例不完整，此处根据逻辑补全了翻译语境，或按要求保持格式逻辑）

为了监控 `/etc/passwd` 和 `/etc/group` 文件，你可以使用审计守护进程。审计守护进程是一个极其强大的工具，允许你选择系统事件进行跟踪和记录它们，并提供报告功能。

要开始审计 `/etc/passwd` 和 `/etc/group` 文件，你需要使用 `auditctl` 命令。启动此操作至少需要两个选项：

- `-w filename` 在文件名上放置监视。审计守护进程通过其 inode 号跟踪文件。inode 号是一个包含有关文件信息的数据结构，包括其位置。
- `-p permissions` 指定权限（如 r、w、x），当发生这些操作时触发审计。例如：

```
auditctl -w /etc/passwd -p wa -k passwordchanges
auditctl -w /etc/group -p wa -k groupchanges
```

（注：由于原文提供的文本在此处出现了断裂或逻辑重复，以下将严格遵循您提供的文本内容进行翻译）

*重新根据您提供的原始文本进行精确翻译（由于原文后部分存在大量重复和乱码化描述，我将按照您提供的文本内容逐行进行翻译）：*
