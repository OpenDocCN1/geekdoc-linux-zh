

## 584 学习安全测试方法

表 4-2（续）
| 文件路径 | 权限 | 描述 |
| --- | --- | --- |
| /etc/sysconfig | 755 | 系统配置文件 |
| /etc/sysctl.conf | 644 | 内核配置参数 |
| /etc/syslog.conf | 644 | 记录消息的 syslogd 服务器配置文件 |
| /etc/vsftpd | 600 | 极安全服务器 (Very Secure FTP Daemon) 配置文件 |
| /etc/vsftpd.ftpusers | 600 | 不允许使用 FTP 传输文件的列表 |
| /etc/xinetd.conf | 644 | xinetd 服务器配置文件 |
| /etc/xinetd.d | 755 | 包含 xinetd 服务器启动的特定服务的配置目录 |
| /var/log | 755 | 所有日志文件的目录 |
| /var/log/lastlog | 644 | 所有之前登录的信息 |
| /var/log/messages | 644 | 主系统消息日志文件 |
| /var/log/secure | 400 | 安全相关日志文件 |
| /var/log/wtmp | 664 | 当前登录的信息 |

另一种权限检查是寻找具有 **setuid** 权限的可执行程序文件。如果一个程序具有 setuid 权限且所有者为 root，那么无论实际由谁运行该程序，该程序都将以 root 权限运行。你可以使用以下命令找到所有 setuid 程序：

```
find -perm +4000 -print
```

你可能想将输出结果保存到文件中（只需在命令末尾添加 `> filename`），然后检查该文件是否存在任何异常的 setuid 程序。例如，用户主目录下的 setuid 程序是不寻的。

## 密码安全

验证密码、组组和影子密码（shadow）文件是否受到保护。特别是，影子密码文件必须是受写保护的，且仅允许 root 读取。文件名及其推荐权限如表 4-3 所示。

## 学习安全测试方法

| 表 4-3 密码文件的所有权和权限 |
| 文件路径 | 所有者 | 权限 |
| /etc/group | root.root | 644 |
| /etc/passwd | root.root | 644 |
| /etc/shadow | root.root | 400 |

## 应急响应

应急响应是回答“系统发生异常情况时该怎么办”这一问题的策略——它告诉你如果有人入侵了你的系统，该如何处理。

你对事件的响应取决于你如何使用系统以及它对你或你的业务有多重要。对于全面的应急响应，这里是需要记住的关键点：

- 确定你的计算机和网络的关键性和重要性，并识别哪些资源可以保护你的系统。
- 采取措施防止并减少潜在的损害和中断。
- 开发并记录一份全面的应急计划。
- 定期测试应急计划并根据情况修订流程。

## 网络安全审查

网络安全审查侧重于评估以下每个领域的安全机制：

- 预防：设置防火墙，启用数据包过滤，禁用不需要 xinetd 服务，关闭不需要的互联网服务，使用 TCP wrappers 进行访问控制，并使用 SSH 进行远程登录。
- 检测：使用网络入侵检测并捕获系统日志。
- 响应：制定应急响应流程。

我简要描述评估网络安全的关键步骤。

## 由 xinetd 启动的服务

xinetd 服务器启动许多互联网服务，如 TELNET 和 sgi_fam（sgi_fam 监控文件变化）。启动其中某些服务的决策取决于系统如何连接到互联网以及系统如何被使用等因素。你通常可以关闭 xinetd 服务。

使用以下方法之一检查启用了哪些 xinetd 服务：

- 检查 `/etc/xinetd.d` 目录下的配置文件，列出 xinetd 可以启动的所有服务。如果某个服务被禁用，配置中会有像下面这样的一行：

```
disable = yes
```

记住：如果通过行首放置 `#` 导致该行被注释掉，则 `disable = yes` 这一行是不生效的。

- 输入以下命令禁用 xinetd 可以启动的服务：

```
chkconfig servicename off
```

其中 `servicename` 是服务的名称（例如 telnet 或 sgi_fam）。要检查 xinetd 可以启动的服务的名称，请输入以下命令：

```
chkconfig --list | more
```

在输出中，查找后续的行：

xinetd based services list 列出了 xinetd 可以启动的所有服务以及它们是开启还是关闭。例如，这里有几行显示系统上 xinetd 状态的代码：

```
telnet:               on
sgi_fam:             on
echo-udp:           off
charger:             off
cups-lpd:            off
services:            off
finger:              off
lines deleted ...
```

在这种情况下，telnet（一个允许用户远程登录系统的服务器）和 sgi_fam（一个报告任何文件变化的服务器）服务是开启的，但其他所有内容都是关闭的。

还要检查以下文件，查看是否有用于 xinetd 服务的任何访问控制：

- `/etc/hosts.allow` 列出了允许访问特定服务的宿机。
- `/etc/hosts.deny` 列出了拒绝访问服务的宿机。

## 独立服务

许多服务（如 http（Web 服务器）和 sendmail（邮件服务器））在启动时会自动启动，因为它们被配置为这样启动。你可以使用 `chkconfig` 命令检查这些独立服务是否在不同的运行级别下启动（有关运行级别的更多信息，请参阅第 VI 卷第 1 章）。通常，Fedora Core 系统在级别 3（文本日志）或级别 5（图形日志）启动。因此，重要的是级别 3 和级别 5 中服务的设置。要查看服务列表，输入以下命令：

```
chkconfig --list | more
```

以下是你可能看到的内容列表：

| xinetd | 1:off | 2:off | 3:on | 4:off | 5:on | 6:off |
|---|---|---|---|---|---|---|
| syslog | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| rhnsd | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| dc23 | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| sendmail | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| iptables | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| smarthd | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| ypxfr | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| dcserver | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| sasld | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| mdmon | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| nflock | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| apca | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| reada | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| microcode | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |
| psacct | 0:off | 1:off | 2:off | 3:on | 4:off | 5:off |

（注：源中的表格数据在类似 | 的行存在严重的 OCR 错误，这些已根据标准的 service 输出进行了清理。）

## 588 探索安全工具

## 渗透测试

渗透测试是了解运行哪些服务的最佳方法。渗透测试涉及尝试获取系统的访问。通常，你从互联网执行此测试以查看哪些是开启。渗透测试的一个方面是查看系统上哪些端口是开启的。端口号仅仅是识别特定 TCP/IP 连接的数字。当连接请求到达时，该端口被认为是开启的。

渗透测试的第一步是执行端口扫描。端口扫描一词用于描述尝试连接每个端口以查看是否有有效响应的过程。许多自动化工具可以执行端口扫描 —— `nmap`（我在本章稍后部分描述）。

有很多自动化工具可用于安全测试。其中某些工具旨在查找 IP 地址范围内每个系统的开启端口。另一些工具寻找与开启端口相关的漏洞。其他工具可以捕获（或嗅探）这些漏洞并帮助你进行分析，从而获得有关网络状况的有用信息。

你可以在 www.insecure.org/tools.html 浏览前 75 个安全工具列表（基于 nmap 用户的非正式调查）。表 4-4 按类别列出了其中一些工具。我将在接下来的几节中描述一些免费的漏洞扫描器。

