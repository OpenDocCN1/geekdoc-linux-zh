
```
lrwxrwxrwx 1 root root 15 Jan 20 21:08 named -> ../sbin/init.d/named
```

如果你想关闭 `named`，可以使用以下命令：

```
chkconfig --level 35 named off
```

你可以使用 `chkconfig` 查看所有服务的状态，包括通过 `xinetd` 启动的服务。例如，你可以通过输入以下命令查看所有服务的状态：

```
chkconfig --list | more
```

# 第四：管理 Red Hat Linux

输出显示了由脚本启动的独立服务以及由 `xinetd` 服务器管理的服务：

```
snmpd       0:off 1:off 2:off 3:off 4:off 5:off 6:off
snmpptrap  0:off 1:off 2:on  3:on 4:on 5:off 6:off
iptables    0:off 1:off 2:on  3:on 4:on 5:off 6:off
gpm         0:off 1:off 2:off 3:on 4:on 5:off 6:off
kudzu       0:off 1:off 2:off 3:on 4:on 5:off 6:off
winbind    0:off 1:off 2:off 3:off 4:off 5:off 6:off
tntpd        0:off 1:off 2:off 3:off 4:off 5:off 6:off
syslog      0:off 1:off 2:on  3:on 4:on 5:off 6:off
atd        0:off 1:off 2:off 3:on 4:on 5:off 6:off
netfs       0:off 1:off 2:off 3:on 4:on 5:off 6:off
network     0:off 1:off 2:on  3:on 4:on 5:off 6:off
random      0:off 1:off 2:on  3:on 4:on 5:off 6:off
... 删除了多行输出 ...
xinetd based services:
charged:    off
rync:      off
charging:   off
daytime-udp: off
daytime:    off
echo-udp:   off
echo:       off
services:    off
servers:    off
time-udp:   off
time:       off
cups-lpd:   off
sgi_fam:    on
kotalk:     off
ktalk:      off
imap:      off
imaps:     off
ipop2:     off
ipop3:     off
ipop3s:    off
finger:     off
ntalk:      off
talk:       off
netlet:     on
reexec:     off
rlogin:     off
rsh:        off
```

输出显示了从 0 到 6 的每个运行级别的每个服务的状态。对于每个运行级别，服务要么开启要么关闭。在列表的最末尾，`chkconfig` 显示了 `xinetd` 控制的服务列表（有关 `xinetd` 的更多信息请第 6 章）。每个基于 `xinetd` 的服务也被标记为开启或关闭，取决于是否配置了 `xinetd` 启动该服务。

# 第 20 章：高级系统管理

## 使用 Red Hat 服务配置工具

如果你不喜欢输入 `chkconfig` 命令，可以使用图形化服务配置实用程序来配置服务。要运行服务配置实用程序，请以 root 身份登录，并在 GNOME 桌面选择“菜单->系统设置->服务设置”。然后你就可以在服务配置窗口中开启或关闭服务（图 20-1）。

![](img/b418dfc0d37b54b9876d5e801170c507_598_0.png)

图 20-1：使用 Red Hat 服务配置工具选择你想要自动启动的服务。

服务配置实用程序在滚动列表中显示服务的名称。列表中的每行都显示一个服务的名称，名称前面有一个方框。方框中的勾选表示该服务已选择在当前运行级别下于启动时启动。当对话框出现时，许多服务已经处于选中。

（注：原文中此处存在大量重复的段落，已根据要求仅翻译并处理，不再重复输出。）

## 第 20 章：高级系统管理 567

| 服务名称 | 说明 |
| --- | --- |
| keytable | 加载 `/etc/sysconfig/keyboard` 文件中指定的键盘映射表。您应该让此服务在您的系统中运行。 |
| kudzu | 探测新硬件并配置更改的硬件 |
| lpd | 管理打印作业队列并将打印作业发送到打印机的服务器。如果您想从 Red Hat Linux 系统进行打印操作，则需要此服务。 |
| named | 这是一个域名命名系统（DNS）服务器，用于将主机名转换为 IP 地址。如果您需要，可以在您的系统上运行副本。 |
| netfs | 允许您挂载和卸载所有网络文件系统（NFS, Samba 和 Netware） |
| network | 允许您激活或禁用所有配置为系统启动时启动的网络接口 |
| nfs |允许使用网络文件系统 (NFS) 协议共享 `/etc/exports` 文件中指定的文件系统 |
| nfslock | 为使用网络文件系统 (NFS) 协议的文件系统提供文件锁定能力，以便其他系统（运行 NFS 的系统）共享您系统中的文件 |
| ntalk | 提供与不同系统上的用户聊天的支持 |
| ntpd | 这是网络时间协议版本 4 (NTP4) 的服务器，用于同步网络中计算机的时钟 |
| pcmcia | 提供对 PCMCIA 设备的支持 |
| pop3s | 支持 SSL 的远程 POP3（邮局协议版本 3）客户端安全地下载邮件。您必须启用 `xinetd` 以运行此服务。 |
| portmap | 任何依赖远程过程调用 (RPC) 的软件使用的服务器。例如，NFS 需要 `portmap` |
| postgres | 启动或停止处理数据库请求的 PostgreSQL 服务器。（PostgreSQL 是 Red Hat Linux 自带的免费数据库。） |
| pxe | 预启动执行环境 (PXE) 服务器，用于通过网络启动其他系统 |
| random | Red Hat Linux 系统上生成高质量随机数所需的服务器 |
| rawdevices | 为设备块分配原始设备（如 Oracle 等应用程序需要） |
| reexec | 支持基于用户名和密码身份验证的远程执行。您必须启用 `xinetd` 以运行此服务。 |
| rhndsd | 定期连接到 Red Hat 网络服务服务器以检查更新和通知 |
| rlogin | 支持远程登录的服务器。您必须启用 `xinetd` 以运行此服务。 |

## 第四部分：管理 Red Hat Linux

### 表 20-2：（续）

| 服务名称 | 说明 |
| --- | --- |
| rsh | 支持远程执行命令的服务器。您必须启用 `xinetd` 以运行此服务。 |
| rsync | 支持远程复制文件的服务器。您必须启用 `xinetd` 以运行此服务。 |
| saslauthd | 支持使用 Cyrus-SASL（简单身份验证和安全层）软件进行认证 |
| sendmail | 将邮件从一台机器移动到另一台机器。如果您想从您的 Red Hat Linux 系统发送邮件，请启动此服务。如果您计划将 Red Hat Linux 系统作为邮件服务器，请不要启动 `sendmail` 服务器，因为可能会慢慢启动过程并消耗不必要的资源。 |
| sgi_fam | 实现文件分配监控器 (FAM)，可在发生更改时获取报告 |
| smb | 启动和停止 Red Hat Linux 系统上支持 LAN 管理器的 Samba `smbd` 和 `nmbd` 服务 |
| snmpd | 用于管理功能的简单网络管理协议 (SNMP) 服务 |
| squid | 互联网对象的缓存服务器——任何可以通过 HTTP 和 FTP 访问的资源 |
| sshd | OpenSSH（安全外壳）安全远程登录设施服务器 |
| syslog | 许多其他程序（包括其他服务）用于在日志文件中记录错误和状态消息（通常是 `/var/log/messages` 文件）。您应该始终运行此服务。 |
| talk | 支持与其他系统上的用户聊天的服务器。您必须启用 `xinetd` 以运行此服务。 |
| telnet | 支持 `telnet` 远程登录会话的服务器。您必须启用 `xinetd` 以运行此服务。 |
| tux | 这是基于内核的 HTTP 服务器 |
| vsftpd | 用于文件传输协议 (FTP) 进行文件传输的安全 FTP 进程 |
