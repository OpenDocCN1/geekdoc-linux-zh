
这些公告是发布周期信息的一部分。

Usenet 讨论组 `comp.protocols.smb` 可以通过搜索前端 dejanews (`www.deja.com`) 找到。请务必访问 `comp.protocols.smb` 论坛。

Samba Kernel Cousins (`http://kt.linuxcare.org/KG/samba/`) 提供了有关 Samba 版本与微软对 Windows 客户端所做的“调整”之间交互的信息。

最后，`www.ntbudgetraq.com` 是一个专门致力于 NT 安全的站点。

不要忘记在你的安全图中包含微软。在 Windows 服务包或 9x 更新发布后，检查微软知识库和新闻组是非常重要的，以查看连接到非 Windows 服务器时可能会出现什么（如果有的话）问题。某些元素是无害的且。

# 创建即用系统

## 第二部分

通过限制服务为服务器提供最小权限访问。由于此服务器的主要目的是服务 Windows 客户端，传统的 UNIX Shell 可能不需要。通过将 `/etc/passwd` 中的 shell 部分设置为 `/bin/false` 来移除它们。

# 与密码相关的安全参数

你的密码选项由你的环境决定。你的环境仅是 Samba 和 NT 的组合吗？如果你在使用 PDC 进行身份验证，那么你唯一的选择是检查域控制器的安全策略。如果你没有访问权限（例如，你正在运行未经授权的 Samba 服务器），请重新你想要实现的内容以及它如何符合公司的基础设施。

假设你的公司基础设施良好，并且你控制密码文件的内容，你需要保护这些文件。需要处理的是 `/etc/passwd` 和 `/etc/smbpasswd`（注意，你的 `smbpasswd` 可能在其他位置）。`/etc/smbpasswd` 需要限制为仅 root 可写。你可以通过运行 `pwconv` 将现有密码系统转换为影子密码系统：

```
pwconv /etc/passwd
```

这会将普通的密码文件转换为影子密码文件。相反，`pwconv` 可以取消此操作。对于组文件也有类似的工具：`grcpconv` 和 `grpunconv`。在处理密码和组文件之前，务必运行检查工具 `pwck` 和 `grpck` 以发现任何错误。

检查网络传输中的密码安全性——使用的是 LANMAN“明文等效物”还是 NT 哈希加密？对于 Windows 客户端，NT 服务包 3 和 Windows 98 引入了加密密码。Windows Workgroups 和 Windows 95 仍在使用“明文等效物”密码。

# Samba 安全

第 15 章

你可以在 does 的 html 部分的 `smbpasswd.5.html` 文档中阅读更多关于 LANMAN 哈希以及 Samba 使用的其他密码保护机制。你至少应该为你的网络制定一个密码策略，避免字典单词和八位密码。LANMAN 哈希会将 Windows 密码拆分为七个字符部分，因此一个八位密码会被处理为一个七位密码和一个单位密码。理想情况下，你的密码长度应该是七位或十四位。Open Solution Providers 的文档 `www.osp.nl/infobase/ntpass.html` 对此主题进行了详细说明。

你可以通过运行来自 `www.openwall.com/jnh/` 的 `John the Ripper` 来检查现有密码的有效性。这是一个尝试解密密码的破解程序。获取最新源码，然后编译并安装程序。在你的文件上运行它，查看哪些密码在一天内被破解。这为你检测弱账户提供了一个起点。

# 密码同步

密码同步性是为了在你的 NT 和 Samba 服务器上保持匹配的用户名/密码对。这允许用户从 Windows 客户端更改密码（可以在你 PDC 上用户账户的密码老化选项中设置为强制执行，从而减轻对 UNIX shell 提示符的需求）。以下是 `smb.conf` 中的参数：

```
unix password sync = yes

passwd program = /usr/bin/passwd %u

passwd chat = *New*UNIX*password* %n*ReType*new*UNIX*password* %n\n*password:**authentication*tokens*updated*successfully*
```

# 从 Windows NT 更改密码

如果你没有使用 `security = server` 来向域控制器验证登录请求，你的用户仍然可以通过按 Ctrl+Alt+Del 并选择“更改密码”在 Samba 服务器上手动同步他们的密码。他们首先需要更改域密码并重复此操作，这次将域更改为 `\\servername` 格式，如对话框所示。Samba 服务器不会出现在下拉列表中。

将在 Samba 服务器上启动一个密码会话会话。

![](img/3a3dd42091ecc215c9b779bbd31cd990_486_0.png)

# 使用 passwd chat 调试

如果 `passwd chat` 失败，你可以启用 `passwd chat` 调试：

```
passwd chat debug = True
```

`passwd chat debug` 允许对 `passwd chat` 脚本进行调试，但它的副作用是在 `smbd` 日志文件中记录明文密码。如果你将其用于开发，请确保在完成后将其设置为 `false`（默认值）并清除日志。你可能还需要检查并清除已轮转的日志。

# 基于 PAM 的密码同步

可插认证模块 (`PAM`) 提供了一种增加身份验证方法灵活性的方法。这是一个复杂的问题，最好由 PAM 自带的文档进行介绍。简而言之，应用程序中的 PAM 支持意味着你可以在无需重新编译应用程序的情况下选择和配置认证方法及数据库。PAM 模块会处理这些。

你可以使用 `ldd` 验证你的 Samba 安装是否使用 `--with-pam` 选项编译：

```
[root@server ~]$ ldd /usr/sbin/smbd

libs1.so.1 => /lib/libsn1.so (0x04018000)

readline.so.3 => /usr/lib/readline.so.3 (0x0402f000)

libd1.so.2 => /lib/libd1.so (0x04051000)

crypt.so.1 => /lib/libcrypt.so.1 (0x04050000)

libpam.so.0 => /lib/libpam.so.0 (0x04001000) << 在这里

libc.so.6 => /lib/libc.so.6 (0x04069000)

libtermcap.so.2 => /lib/libtermcap.so.2 (0x0417c000)

/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x04000000)

[root@server ~]
```

这显示 PAM 已编译到此版本的 Samba 中，以下是 PAM 的 Samba 配置文件：

```
[root@server]# cat /etc/pam.d/samba

auth required

account required

/lib/security/pam_pwdb.so shadow
```

（注：原文后续文本包含大量重复和错误，已处理其有效内容。）

# 访客访问问题

你可能希望允许没有账户的用户登录你的服务器（例如，为了打印资源或共享信息）。由于 Samba 始终需要某种形式的有效账户，因此必须对“无账户”登录进行映射。

`map to guest` 适用于 user、server 和 domain 安全模式，并允许登录映射到定义的访客用户账户。共有三种模式可用：`never`（从不）、`bad user`（错误用户）和 `bad password`（错误密码）。默认值是 `never`，它会拒绝所有使用错误或无效密码的用户登录。

`bad user` 模式在密码错误时拒绝有效账户的用户登录。如果用户账户不存在，则会生成访客登录，并映射到访客账户。

`bad password` 模式会将密码错误的用户登录视为访客登录，并将其映射到访客账户。

# guest ok = yes

如果设置 `guest ok = yes`，则允许在该服务上进行访客登录，权限将访客账户的权限。默认 `guest ok = no`。

# guest account = ftp

当进行访客登录时，该账户将映射到 `guest account` 中指定的用户。出于安全起见，该账户存在于密码文件中，但无法登录。这通常是 "nobody"，但在某些系统上，该账户可能无法打印。如果你的 Samba 是一个匿名 FTP 服务器，可以使用安装服务时通常创建的 ftp 账户。然而，由于最常见的匿名 FTP 服务器软件包频繁触发安全警报，你可能最好为无账户分配选择访客登录点。

# 安全问题

`home` 服务允许 Samba 动态生成格式为 `\servername\U` 的共享，这非常适合存储用户的邮件箱、浏览器缓存等。它也是用户的常规 UNIX 主目录。你**绝不能**在此服务中使用任何访客参数，因为这样做会使所有主目录对访客登录开放，这绝对不是你想要的结果。

# Samba 安全级别

Samba 可以在不同的安全级别上模拟不同类型的 Windows“服务器”。最简单的方案是回退到 Windows 工作组（Windows for Workgroups），最复杂的是当前的 NT 域级别，或域成员级别。

# security = share

此设置类似于 Windows 工作组共享。每个共享点或服务都有一个预定义的密码。在 `security = share` 模式下，`smbd` 始终使用 UNIX 用户账户来代表客户端操作。

# security = user

在用户级安全中，连接到资源时必须提供用户名/密码对。如果你有使用加密密码的 NT 客户端，你需要这种级别的安全设置。

# security = server

此模式允许你使用另一个服务器的账户资源，例如 PDC。

# security = domain

如果你使用 `smpasswd` 将 Samba 服务器添加到域中，则可以使用域级安全设置。密码必须经过加密。Samba 将尝试通过将用户名/密码对传递给 NT 域控制器（PDC 或 BDC）来验证该用户名/密码对。这与已加入域并对域账户进行身份验证的 NT 服务器行为相同。需要注意的是，Samba 服务器上必须仍然存在一个有效的用户账户，它才能映射文件访问。这与 `security = server` 形成对比，后者会动态生成账户。

# Samba 风险与泄露

大多数 Linux 发行版和默认 Windows 安装都被设置为中等到低安全级别。你始终需要修改环境，以在你的 Samba 服务器和 Windows 客户端上落实安全性。Samba 还可能出现配置错误，导致不必要地降低安全级别。

# 显而易见的泄露：hosts equiv=

这与 `hosts allow` UNIX 服务访问文件不同。`hosts equiv` 设置后，会指定一个包含主机名和用户名的文件，这些主机和用户无需指定密码即可获得访问权限。这在安全的网络中没有立之地。

# admin users =

当指定了 `admin users` 时，他们可以作为 root 执行执行文件操作。如果这种罕见的情况正是你所需要的，你可以遵循某些 NT 约定并将服务作为隐藏共享提供。例如，如果你访问 `/etc` 文件系统，可以将其共享为 `etc`，它不会出现在服务列表中。请记住，你正在登录 NT 工作站的本地 Administrator 账户并使用 Administrator 作为透传账户，工作站的本地 SAM 是一个可能被“破解”的进入你服务器 root 权限的门户。

# 滥用风险：wide links = yes

共享点内的链接始终被允许；`wide links = yes` 设置控制是否可以跟踪共享点外的链接。

# 用户可操纵的 suid root 可执行文件

像处理任何 UNIX 类型系统一样，防范 `suid root` 可执行文件。

# 增强安全性

允许加密密码。NT SP3 引入了强制加密密码，比 LANMAN 哈希提供了更大的保护。

从你的 `inetd.conf` 文件中删除不需要的服务。如果你不熟悉每个条目的的功能，请研究它，并决定是否删除。你可以在修改 `inetd.conf` 文件并删除它而无需重启服务器。我建议从服务器终端执行此操作，以避免网络连接中断。你还应该安装保护程序（如 Tripwire）来监控你的连接。Tripwire 和其他 UNIX 安全工具可以在 `http://ciac.lnl1.gov/ciac/ToolsUnixSysMon.html` 。

# 防止 Shell 登录

Samba 服务器通常用于替换 Windows 环境中的 NT 服务器。除非你有特定的应用程序需要传统的 UNIX 登录，可以将所有普通用户的登录 shell 设置为 `/bin/false` 来提高 Samba 服务器的安全性。结合删除所有明文密码服务（如 ftp、telnet 和 rsh），增加了入侵者搜寻文件系统的难度。

# SMB 网络的诊断工具

你可以从 Samba 网站获取 `tcpdump-smb`，它是 `tcpdump` 的一个扩展，用于调查 NetBEUI 和 TCP/IP 上的网络问题。请查看下载部分。通常情况下，由于硬件访问级别和提供的信息，它必须以 root 身份运行。这是一个示例：

```
[root@server]#usr/sbin/tcpdump port 139
```

这会捕获所有发送到运行 tcpdump 机器的 SMB 数据包，并提供大量输出供你查看。当你有特定问题需要调查（最好是可以重复的问题）且所有其他简单诊断都失败时，使用它。

要调试解析问题，使用端口 137。对于浏览包问题（例如错误或不完整的网络列表），使用端口 138。

要调查当前的用户和文件访问，使用 `smstatus`。用户账户会被映射到进程 ID (`PID`)。文件和服务的访问将与该 PID 关联。要获取用户账户 PID，请执行：

```
smstatus | grep username
```

注意返回的 PID。然后你可以执行：

```
smstatus | grep pid
```

以找到所有用户认为未在使用但报告为锁定的文件。

要解决文件问题，首先找到与文件相关的 PID：

```
smstatus | grep filename
```

然后查看与当前文件访问关联的用户。例如，用户可能遇到了过期锁，在用户走过来与你讨论问题期间，锁可能已经释放。

Samba 事件日志保存在按机器命名的单独日志中，以及常规系统日志文件中，格式为 `sm.computername`，其中 `computername` 是拥有 Samba 连接的计算机的 NetBIOS 名称。

如果你遇到服务性的重复性问题（例如客户端尝试连接到 Samba 服务器时出现“服务器太忙”错误消息），你可以在 Samba 消息中动态查看发生的情况：

```
tail -f /var/log/log.smb
```

## Samba 安全

第 15 章

这揭示了元凶：
`connection denied from 192.168.1.5`
`gethostbyaddr failed for 192.168.1.5`

现在你可以看出，Samba 的名称解析工作未正常。

## 客户端与服务端安全协同工作

Windows 的设计要求你结合使用客户端和服务端的安全方法，从在 Windows 9x 和 NT 上应用系统策略，到仅针对 NT 的 ACL 锁定和用户组级别。Samba 是存储锁定脚本和策略文件的正确位置。

## 使用系统策略提高安全性

系统策略文件在第 27 章“Samba 企业级备份策略”中有更详细的介绍，涉及其位置和应用方式。从安全的角度来看，你可以使用它们来“锁定” Windows 9x 机器；在某些方面，它的行为更像 NT，通过阻止对机器配置的访问并强制执行网络登录，从而消除没有有效登录的用户对机器的访问。在规模合理的网络中，强制域域登录是一个好主意。以前的问题是“当服务器宕机时该怎么办？”答案是“使用 Samba 让它不要宕机！”强制登录可以防止不受欢迎的访客使用你的电脑调查你的网络；它们无法阻止某个开启了 DHCP 的设备插上插座、配置域名并四处尝试。最大的优势是为你的 9x 电脑带来了类似 NT 的保护。结合防止用户从软盘启动的 BIOS 配置，你将获得一种可行的（尽管并不高）的安全水平。

## 系统策略——95/98

指定一台主策略编辑机器并在其上创建你的策略文件。如果你拥有一个混合操作系统的网络，你需要一台 NT 机器和一台 9x 机器。策略编辑器对于 NT 和 9x 来说是同一个可执行文件，但它只会产生与生成时操作系统兼容的策略文件——NT 策略必须使用 NT 创建，9x 策略必须使用 9x 创建。

# 创建开箱即用的 Samba 系统

## 第二部分

你的策略文件将存储在 Samba 服务器的 `netlog` 共享中，当 Samba 作为 PDC 时自动使用，或当 Samba 是域的一部分时被引用。为 NT 客户端和 9x 客户端使用不同命名的文件。以下是对应的 `smb.conf` 条目：

```
[netlog]

comment = Network Logon Service

path = /home/netlog

guest ok = yes

writable = no

share modes = no
```
