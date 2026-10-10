
```bash
# echo PATH
/usr/kerberos/bin:/usr/local/bin:bin:/sbin:/usr/X11R6/bin:home/richard/bin
```

内核 Shell 包含了一个特殊的变通方法，用于设置用户 ID 和有效用户 ID (`EUID` 和 `UID`)。

随后会设置 `USER`、`MAIL` 和 `LOGNAME` 变量，前提是提供用户 ID 的 `/usr/bin/id` 是可执行的。带有 `-un` 选项的 `id` 命令仅提供用户 ID 的文本名称，如 chris 或 richard。

`HISTSIZE` 被重新定义以包含更多的历史事件。这里还添加了 `HISTFILE` 变量的条目。通常，需要为所有用户设置服务器地址。所有的赋值都应由系统管理员在系统的 `/etc/profile` 文件中完成，而不是在每个用户自己的 `.bash_profile` 文件中。

注意：`/etc/profile` 文件还会执行 `/etc/profile.d` 目录中的任何脚本。这种设计允许更模块化的结构。与其通过编辑文件添加条目，只需向 `profile.d` 目录添加脚本即可。

注意：`/etc/profile` 文件不再运行 `/etc/inputrc` 文件，该文件配置你的命令行编辑器。

## /etc/profile

```bash
# /etc/profile

# 全局环境和启动程序，用于登录设置
# 函数和别名放在 /etc/bashrc
```

```bash
pathmunge () {
if ! echo $PATH | /bin/egrep -q "([^|^):$1"; then
    if [ "$2" = "prepend" ]; then
        PATH=$2:$PATH
    elif [ "$2" = "append" ]; then
        PATH=$PATH:$2
    fi
    export PATH
fi
```

你可以向 `.bashrc` 文件添加任何自定义命令或定义。如果你对 `.bashrc` 了更改，并希望这些更改在当前登录会话中生效，你需要使用 `.` 或 `source` 命令重新执行该文件。

```
$ .bashrc
```

# 系统 /etc/bashrc BASH 脚本

Fedora 也有一个为所有用户执行的系统 bash 文件，称为 `/etc/bashrc`。目前，`/etc/bashrc` 文件为登录 shell 设置了默认的 bash 提示符。如果是在交互式 shell 中，`/etc/bashrc` 文件将决定 `PATH` 并运行任何 `profile.d` 脚本（这些脚本由登录 shell 的 `/etc/profile` 运行）。

注意：`/etc/bash_completion.d` 目录下的 bash_completion 文件为应用程序提供了命令补全选项。

# BASH Shell 注销文件：.bash_logout

`.bash_logout` 文件也是一个配置文件文件，但它在用户注销时执行。它的设计是为了执行你在每次注销时希望发生的任何操作。与变量定义不同，`bash_logout` 通常包含 shell 命令，构成一种关机程序——即你在注销之前始终希望执行的操作。一种常见的注销命令是清除屏幕然后发出告别信息。这由 root 用户的 `.bash_logout` 文件执行，但在普通的 `.bash_logout` 文件中并不执行。

# .bash_logout

```
# ~/.bash_logout
clear
echo "Good-bye for now"
```

与 `.bash_profile` 一样，你可以将自己的 shell 命令添加到 `.bash_logout` 中。root 用户的 `.bash_logout` 文件包含了调用 `clear` 命令来清除屏幕的指令。在下一个示例中，用户在 `.bash_logout` 文件中添加了一个 `echo` 命令。

# 第 4 部分：网络服务

- 邮件服务器
- FTP 服务器
- Web 服务器
- 新闻和数据库服务器

# 20. 邮件服务器

- 邮件传输代理 (`MTA`)
- Postfix
- Sendmail
- POP 和 IMAP 服务器：Dovecot
- 垃圾邮件过滤器：SpamAssassin

邮件服务器为互联网用户提供电子邮箱服务。它们有各自的 TCP/IP 协议，例如简单邮件传输协议 (`SMTP`)、邮局协议 (`POP`) 和互联网邮件访问协议 (`IMAP`)。邮件通过服务本地域的邮件服务器在互联网上传输。一个域名可以是大型互联网的一个子网，拥有自己的服务器来处理从该子网发送或在该子网接收的邮件。当用户发送邮件时，邮件首先从其主机系统发送到邮件服务器。然后，邮件服务器通过互联网将消息发送到另一个邮件服务器，即接收者所在的接收子网。接收邮件然后将消息发送到接收者的主机服务器。

在每个阶段，都会使用不同的代理（程序）进行不同类型的操作。邮件用户代理 (`MUA`) 是邮件客户端程序，例如 Evolution、Thunderbird、Kmail 或 mail。通过 `MUA`，用户编写并发送邮件。然后，邮件传输代理 (`MTA`) 在互联网上传输消息。`MTA` 是使用 `SMTP` 在互联网上从一个邮件服务器向另一个邮件服务器发送消息的邮件服务器，它们在子网之间传输消息（原文：子网之间传输它们）。在 Fedora 上，常用的 `MTA` 是 Postfix 和 Sendmail。这些邮件守护进程不断检查来自其他邮件服务器的入站邮件，并向适当的服务器发送邮件（见表 20-1）。邮件服务器接收到的入站邮件通过投递代理 (`MDA`) 分发给用户。大多数 Linux 系统使用 `procmail` 作为它们的 `MDA`，将邮件服务器接收到的消息投递到用户账户（更多信息请参阅 www.procmail.org）。

# 邮件传输代理

在 Fedora 上，你可以安装和配置 Postfix、Exim 或 Sendmail。你还可以设置 Linux 系统运行 POP 服务器。POP 服务器会保存用户的邮件，直到他们登录并访问消息，而不是直接将邮件发送到他们的主机上。

| 代理程序 | 描述 |
| :--- | :--- |
| Sendmail | Sendmail 邮件传输代理，由 Sendmail 联盟 `www.sendmail.org` 支持 |
| Postfix | 快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并设计用于取代它 `www.postfix.org` |
| Qmail | 快速、灵活且安全的 MTA，具有其高效的实现方式和竞争力 `www.qmail.org` |
| Exim | 基于 smail3 的 MTA `www.exim.org` |
| Courier | Courier MTA `www.courier-major.org` |

表 20-1：邮件传输代理

Courier 是一种快速、小巧且安全的 MTA，与 Sendmail 保持某些兼容性。Courier 软件软件包还包含 POP、IMAP 和 webmail 服务器以及邮件列表服务。它支持广泛的验证方法，包括影子密码、PAM 和 LDAP。

Exim 是一个快速且灵活的 MTA，类似于 Sendmail。它在剑桥大学被开发，其实现方式与 Sendmail 非常不同。

Omail 是一个快速且安全的 MTA，但它与 Sendmail 的兼容性很差。它有自己的配置。

# Postfix

Postfix 是一个快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并设计用于取代它 `www.postfix.org`。

在 Fedora 上，你可以安装和配置 Postfix、Exim 或 Sendmail。你还可以设置 Linux 系统运行 POP 服务器。POP 服务器会保存用户的邮件，直到他们登录并访问消息，而不是直接将邮件发送到他们的主机上。

Postfix 是一个快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并设计用于取代它 `www.postfix.org`。

Omail 是一个快速且安全的 MTA，但它与 Sendmail 的兼容性很差。它有自己的配置。

# Postfix

Postfix 是一个快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并设计用于取代它 `www.postfix.org`。

Omail 是一个快速且安全的 MTA，但它与 Sendmail 的兼容性很差。它有自己的配置。

# Postfix

Postfix 是一个快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并设计用于取代它 `www.postfix.org`。

Omail 是一个快速且安全的 MTA，但它与 Sendmail 的兼容性很差。它有自己的配置。

# Postfix

Postfix 是一个快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并设计用于取代它 `www.postfix.org`。

Omail 是一个快速且安全的 MTA，但它与 Sendmail 的兼容性很差。它有自己的配置。

# Postfix
