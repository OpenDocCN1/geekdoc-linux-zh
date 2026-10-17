
### 在两扩展扩展邮箱模式

### 从生成的文件夹名称中删除前缀

### 成对对文件夹进行同步（如果不存在则创建）

因此，IMAP 服务器上的文件夹 `INBOX.sent-mail` 将与本地文件夹 `Mail/sent-mail` 同步（前提是存在上述说明的定义）。各个文件夹之间的同步方式如下：

- 如果消息在双方都存在，则什么都不发生。
- 如果消息仅存在于一方且是新的（未列在 `msinfo` 文件中），则传输到那里。
- 如果消息仅存在于一方且是旧的（已列在 `msinfo` 文件中），则将其删除（因为显然存在于另一方的消息被删除了）。

要预先知道同步期间哪些消息将被传输，哪些消息将被删除，请通过带有通道和存储器的 `mailsync folder localdir` 启动 `mailsync`。此命令会生成本地主机上所有新消息的列表，以及在同步期间 IMAP 侧将被删除的所有消息列表。同样，命令 `mailsync folder imapdir` 会生成 IMAP 侧所有新消息的列表，以及在同步期间本地主机上将被删除的所有消息列表。

### 15.6.3 可能的问题

在发生数据丢失时，最安全的方法是删除相关的日志文件 `msinfo`。因此，所有仅存在于一方的消息都被视为新的，从而在下次同步期间进行传输。

只有带有 message ID 的消息包含在同步中。缺少 message ID 的消息将被简单忽略，这意味着它们既不会被传输也不会删除。缺少 message ID 通常是由于程序在发送或写入消息时出现故障引起的。在某些 IMAP 服务器上，主文件夹使用 `INBOX` 寻址，子文件夹使用随机选择名称（与 `INBOX` 和 `INBOX.name` 相反）。因此，对于此类 IMAP 服务器，无法专门指定模式。在成功传输到 IMAP 服务器后，邮件驱动程序（c-client）设置了特殊标记。可以通过 `-n` 禁用。

### 15.6.4 更多信息

`/usr/share/doc/packages/mailsync/` 中的 `README` 提供了额外信息。在此情况下，RFC 2076 “Common Internet Headers”具有特殊价值。

## 异构网络

除了连接其他 Linux 系统，Linux 还可以连接到 Windows 和 Macintosh 并在 Novell 网络上通信。本章展示了异构网络的要求和配置。

- 16.1 Samba . . . . . . . . . . . . . . . . . . . . . . . . . . 384
- 16.2 Netatalk . . . . . . . . . . . . . . . . . . . . . . . . . . 392
- 16.3 NetWare Emulation with MARSNWE . . . . . . . . . . . . . 398

## 16

## 16.1 Samba

### 16.1.1 Samba 简介

使用 Samba 程序可以将 UNIX 机器转换为 DOS、Windows 和 OS/2 机器的文件和打印服务器。Samba 项目由 Samba 团队运行，最初由澳大利亚的 Andrewidge 开发。

Samba 现在已成为一个完整且相当复杂的程序。本节介绍了其基本功能。在命令行中输入 `apropos samba` 可以显示某些帮助页，或者如果安装了 Samba，可以直接浏览 `/usr/share/doc/packages/samba` 目录。

从 9.1 版本开始，SUSE LINUX `samba` 软件包提供了 Samba 3 版本，它带来了一些功能：

- 支持 Active Directory
- 大支持 Unicode
- 内部验证机制已完全修订
- 改进了对 Windows 2x/XP 打印系统的支持
- 服务器可以作为 Active Directory 域的成员服务器
- 采用 NT4 域，允许从后者迁移到 Samba 域。

Samba 使用基于 NetBIOS 服务的 SMB 协议（服务器消息块）。由于 IBM 的压力，微软发布了该协议以便其他制造商能够连接到微软域网络。在 Samba 中，SMB 协议运行在 TCP/IP 协议之上，因此所有客户端必须安装 TCP/IP 协议。

### 迁移到 Samba3

从 Samba 2.x 迁移到 Samba 3 时需要注意一些特殊点。该主题的讨论包含在 Samba HOWTO Collection 中，其中有一个章节专门介绍它。在安装 `samba-doc` 软件包后，可以在 `/usr/share/doc/packages/samba/Samba-HOWTO-Collection.pdf` 中找到 HOWTO。

### 16.1.2 安装与配置服务器

如果你打算将 Samba 作为服务器，请安装 `samba`。Samba 所需的服务可以通过 `rcsmb start && rcsmb start` 启动，通过 `rcsmb stop` 停止。

Samba 的主配置文件是 `/etc/samba/smb.conf`。该文件可以分为两个逻辑部分。`[global]` 部分包含集中化和全局设置。`[share]` 部分包含各个单独的文件共享和打印机共享。通过这种方法，可以在 `[global]` 部分以不同的方式或全局方式设置共享细节，这增强了配置文件的结构透明度。

#### 全局部分 (Global Section)

`[global]` 部分的以下参数需要进行调整，以匹配你的网络设置要求，以便其他机器能够在 Windows 环境通过 SMB 访问你的 Samba 服务器。

- `group = TUX-NET`：此行将 Samba 服务器分配到一个工作组（workgroup）。请将 `TUX-NET` 替换为你工作环境中的适当工作组。你的 Samba 服务器将以其 DNS 名称显示，除非该名称已分配给网络中的其他机器。如果 DNS 名称不可用，请使用 `netbiosname=MYNAME` 设置服务器名称。有关此参数的更多细节请参见 `mansmb.conf`。
- `level = 2`：此参数触发 Samba 服务器是否尝试成为你工作组的 LMB（本地主浏览器）。选择一个非常低的值，以保护现有的 Windows 网络免受配置错误的 Samba 服务器引起的任何干扰。关于此重要主题的更多信息可以在软件包文档中 `docs` 子目录下的 `BROWSING.txt` 和 `BROWSING-Config.txt` 文件中找到。如果网络中没有其他 SMB 服务器（如 Windows NT 或 2000 服务器），且你希望 Samba 服务器保留本地环境中所有系统的列表，请将 `os level` 设置为较高的值（例如 65）。这样，你的 Samba 服务器将被选为本地网络的 LMB。在更改此设置时，请仔细考虑这将如何影响现有的 Windows 网络环境。配置错误的 Samba 服务器在尝试成为工作组的 LMB 时可能会导致严重问题。请联系你的管理员，或在隔离网络或非关键时间段对你的配置进行一些压力测试。
- `wins support and wins server`：要将 Samba 服务器集成到具有活动 WINS 服务器的现有 Windows 网络中，请启用 `wins server` 选项并将其值设置为该 WINS 服务器的 IP 地址。如果你的 Windows 连接到不同的子网并仍应相互感知，你需要设置一个 WINS 服务器。要将 Samba 服务器转换为 WINS 服务器，请设置选项 `wins support = Yes`。确保网络中只有一个 Samba 服务器启用了此设置。在你的 `smb.conf` 文件中，切禁同时启用 `wins server` 和 `wins support` 选项。

# 16 异构网络

### 共享

以下示例说明了如何向 SMB 客户端提供 CD-ROM 驱动器和用户目录（homes）。

`[cdrom]` 为了避免 CD-ROM 驱动器意外可用，这些行被注释标记禁用了（在本例中为分号）。删除第一列中的分号即可与 Samba 共享 CD-ROM 驱动器。

#### 示例 16.1：CD-ROM 共享

```ini
[cdrom]
; comment = Linux CD-ROM
; path = /media/cdrom
; locking = No
```

`[cdrom]` `comment` 是网络上所有 SMB 客户端可见的共享名称。可以添加额外的注释来进一步描述共享。`path = /media/cdrom` 导出目录 `/media/cdrom`。

通过非常严格的默认配置，此类共享仅对该系统上的现有用户可用。如果应让此共享对所有人可用，请在配置中添加行 `guest ok = yes`。此设置赋予网络上的任何人读取权限。建议非常小心地处理此参数。即使在 `[global]` 部分使用此参数也同样如此。

`[homes]` `[home]` 共享在这里具有特殊性。如果用户拥有 Linux 文件服务器及其自己的家目录的有效帐户和密码，他就可以连接到它。

#### 示例 16.2：homes 共享
