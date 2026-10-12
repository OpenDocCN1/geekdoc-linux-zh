
# 匿名登录后，守护进程以用户/组 ftp 运行。

```
<Anonymous /home/ftp>
User ftp
Group ftp

# 客户端登录 'anonymous' 被别名为真实用户 'ftp'。
UserAlias anonymous ftp

# 禁止对所有目录进行写操作，'incoming' 目录除外，
# 该目录允许 'STOR' 操作（但禁止 'READ' 操作）

<Directory *>
<Limit WRITE>
DenyAll
</Limit>
</Directory>

<Directory incoming>
<Limit READ>
DenyAll
</Limit>
<Limit STOR>
AllowAll
</Limit>
</>
```

## 主动模式与被动模式

要理解主动模式和被动模式之间的区别，你首先需要理解防火墙中的常用功能。管理员通常允许内部机器向外部机器建立连接，但防止反向操作（少数情况除外）。

例如，公司的 Web 服务器可能位于防火墙之后。在主动模式下，客户端连接到服务器，然后服务器向客户端发起连接。防火墙通常会阻止这种来自服务器的入站连接。

在被动模式下，客户端同时发起控制和数据连接。这对防火墙更加友好，因为所有连接都是从客户端网络发出的。要使用被动模式，客户端发送 `PASV` 命令，服务器返回一个 IP 地址和端口号，客户端连接到该地址。

（注：原文中存在大量由于 OCR 识别导致的重复段落和乱码，译文已根据逻辑进行了合并和清理。）

## 复习题

这些复习题的答案位于附录 A。

- 1. `vsftpd.conf` 文件中的 `______` 指令允许匿名 FTP 连接。

- 2. 下列哪个 FTP 服务器不是通过配置文件配置的？
   a. `vsftpd`
   b. `Pure-FTPd`
   c. `ProFTPd`
   d. `FireFTPd`

- 3. `vsftpd.conf` 文件中的下列哪个指令用于启用或禁用本地用户登录到 FTP 服务器？
   a. `local_enable`
   b. `local_disable`
   c. `local_access`
   d. `local_login`

- 4. 如果 `vsftpd.conf` 文件中的 `disable_enable` 指令设置为 `YES`，则当 FTP 用户进入目录时，将显示 `______` 文件的内容。

- 5. 该文件被 PAM 用于通过在文件中列出不允许访问 FTP 服务器的用户列表，来拒绝用户访问 FTP 服务器。
   a. `/etc/pam.d/vsftpd`
   b. `/etc/access/vsftpd.deny`
   c. `/etc/vsftpd/ftpusers`
   d. `/etc/secure/deny.vsftpd`

- 6. 下列哪些 `vsftpd.conf` 指令与创建一个允许特定用户访问 FTP 服务器的列表有关？（选择所有适用）
   a. `userlist_enable`
   b. `userlist_file`
   c. `userlist_allow`
   d. `userlist_deny`

- 7. `vsftpd.conf` 文件中的 `______` 指令用于在 FTP 用户登录之前显示某个文件的内容。

- 8. `vsftpd.conf` 文件中的 `______` 指令用于限制从每个 IP 地址允许的连接数。

- 9. `Pure-FTPd` 守护进程的哪个选项不允许匿名用户访问？
   a. `-c`
   b. `-E`
   c. `-A`
   d. `-a`

- 10. `______` 模式旨在避免防火墙关于不允许外部系统建立连接的限制。

本章涵盖了以下主题：

- `SSH` 服务器配置
- `SSH` 客户端配置
- 高级 `SSH` 服务器功能

本章涵盖了以下学习目标：

- `212.3 Secure Shell (SSH)`

# 第 37 章

# Secure Shell (SSH)

Secure Shell (SSH) 旨在取代不安全的远程通信操作，例如 `telnet`、`ftp`、`login`、`rsh`、`rcp` 和 `rexec` 命令/协议。以前通信方法的主要问题是它们以明文形式在网络上传输数据，而不是加密格式。在某些情况下（如 `telnet` 和 `ftp`），这可能包括在网络上以明文形式发送用户账户数据（用户名和密码）。

Secure Shell (SSH) 协议通过对在网络上传输的数据进行加密提供了更高的安全级别。本章主要关注设置 Secure Shell 服务器，包括该协议工作原理的概念和关键配置选项。还涵盖了 Secure Shell 客户端工具，包括如何通过修改 SSH 客户端配置文件来自定义工具的行为。

## “我已经掌握这些了吗？”测验

“我已经掌握这些了吗？”测验可以帮助你评估应该阅读整个本章节，还是仅仅直接跳转到“考试准备任务”部分进行复习。如果你有疑问，请阅读整个章节。表 37-1 概述了本章的主要标题以及对应的“我已经掌握这些了吗？”问题。你可以在附录 A，“‘我已经掌握这些了吗？测验的答案”中找到答案。

| 表 37-1 “我已经掌握这些了吗？”基础知识章节与问题映射 |
| 基础知识章节 | 该章节涵盖的问题 |
| --- | --- |
| 配置 Secure Shell 服务器 | 1 |
| Secure Shell 客户端命令 | 2 |
| 高级 SSH 特性 | 3 |

- 1. 哪个文件用于配置 `SSH` 服务器软件？
   a. `/etc/ssh/ssh_config`
   b. `/etc/ssh/sshd_config`
   c. `/etc/ssh/server_config`
   d. `/etc/ssh/config`

- 2. 下列哪些命令是 `SSH` 客户端工具？（选择所有适用）
   a. `sget`
   b. `ssh`
   c. `scp`
   d. `sftp`

- 3. `__command` 命令用于管理用户的 `RSA` 密钥，以允许无密码的 `SSH` 认证。

# 基础知识点

`SSH` 已成为 Linux 的一种标准，以至于几乎所有的发行版默认都同时包含客户端和服务器软件。如果你的系统中没有安装这些软件，你应该安装 `openssh`、`openssh-server`、`openssh-clients` 和 `openssh-askpass` 包。

# 配置 Secure Shell 服务器

`/etc/ssh` 目录是存储 Secure Shell 配置文件的位置。`SSH` 服务器的配置文件是 `/etc/ssh/sshd_config` 文件。不要将其与 `/etc/ssh/ssh_config` 文件混淆，后者用于配置客户端工具，如 `ssh`、`scp` 和 `sftp` 命令。

# 基础配置设置

有两种编号为 1 和 2 的 `SSH` 协议。它们不是版本，而是两种为了提供安全数据连接而开发的协议。曾有一段时间两种协议都被经常使用，但现在几乎都使用协议 2。

## 影响用户访问的设置

你可以考虑不允许 `root` 登录。要禁止 `root` 用户登录，将 `PermitLogin` 值更改为：

```
PermitLogin no
```

有一个没有权限登录的普通用户怎么办？在这种情况下你有两个选择：`AllowUsers` 或 `DenyUsers`。如果你使用 `AllowUsers` 关键字，则允许这些用户连接服务器：

```
AllowUsers bob sue
```

如果你使用 `DenyUsers` 关键字，所有列表的用户都可以连接服务器。注意，如果你同时使用这两个关键字，`DenyUsers` 优先。你可以使用通配符匹配模式：

```
DenyUsers guest* #拒绝任何以 guest 开头的用户
DenyUsers ????app #拒绝任何包含 4 个字符并以 app 结尾的用户
```
